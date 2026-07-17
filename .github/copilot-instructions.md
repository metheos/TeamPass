# TeamPass Local Intent Guidance

This repository regularly merges from upstream `nilsteampassnet/TeamPass`.

Our objective is to keep important local goals intact while still accepting upstream fixes and improvements.

## What To Preserve

Preserve local changes when they directly support one of these goals:

- Security hardening and safer defaults
- Encryption and key-management correctness
- Operational stability for self-hosted/on-prem deployments
- Backward compatibility for existing TeamPass instances
- PHPStan compliance and safer input handling

## Merge Preference Rules

When syncing with upstream:

1. Prefer upstream changes by default.
2. Keep local changes only when they clearly implement a listed goal.
3. If both sides solve the same problem, prefer the safer and more maintainable version.
4. If uncertain, keep upstream behavior and re-apply local intent in a small follow-up commit.

## Commit Message Convention For Local Intent

For local commits that should survive future merges, include an intent marker:

- `[intent:security]`
- `[intent:encryption]`
- `[intent:stability]`
- `[intent:compat]`
- `[intent:quality]`

Example:

`[intent:security] Validate item access before OTP retrieval`

## Required Maintenance

When creating a local intent commit, update `.github/COMMIT_INTENT.md` with:

- Why the change exists
- What behavior must remain true after upstream merges
- How to verify the behavior quickly

This gives future merge work a durable, reviewable source of truth.
