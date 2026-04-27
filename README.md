# asteby/renovate-config

Shared **Renovate preset** for the Asteby + Metacore ecosystem.

## Why this exists

Every consumer app of the Metacore platform (`metacore-kernel` for Go, `@asteby/metacore-*` for the SDK) should ride the same release train. Instead of copy-pasting the same `renovate.json` into 25+ repos, each repo extends from this preset:

```json
{ "extends": ["github>asteby/renovate-config"] }
```

When the policy changes, we change it here, and the whole ecosystem inherits the update on the next Renovate run.

## What the preset does

- Groups every `@asteby/metacore-*` (npm) and `github.com/asteby/metacore-*` (gomod) bump into a single PR per release train.
- **Auto-merges minor and patch** updates of platform packages — kernel/SDK releases land in consumer apps automatically.
- Major bumps stop and ask for human review (breaking changes need a migration).
- Groups React/TanStack/Radix and Fiber/GORM together to avoid peerDep churn.
- Generic patches across the ecosystem auto-merge.

## How to adopt it

In any repo, add `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>asteby/renovate-config"]
}
```

Need to override a rule for a specific repo? Add it after `extends`:

```json
{
  "extends": ["github>asteby/renovate-config"],
  "packageRules": [
    {
      "matchPackagePatterns": ["^@asteby/metacore-"],
      "automerge": false
    }
  ]
}
```

## Notes

- This repo is **public** so Renovate can resolve it without a token from any repo (public or private) in the org.
- No secrets here — only Renovate policy.
