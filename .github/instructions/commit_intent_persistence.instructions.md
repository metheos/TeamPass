---
alwaysApply: true
always_on: true
trigger: always_on
applyTo: "**"
description: Preserve local commit intent during upstream merges
---

# Local commit intent policy

This repository accepts upstream updates frequently.

When modifying code, reviewing diffs, or resolving merge conflicts:

- Prefer upstream changes unless local behavior is required by a documented local intent.
- Use `.github/COMMIT_INTENT.md` as the source of truth for which local behaviors must persist.
- If a local behavior from `.github/COMMIT_INTENT.md` would be lost, preserve or re-apply it in a minimal patch.
- Keep changes small and local. Do not refactor unrelated code.
- Keep compatibility with current TeamPass runtime and upgrade paths.
- Keep security and encryption flows correct; never weaken access checks or key handling.

## Conflict resolution checklist

1. Identify whether the conflicted code is covered by a documented local intent.
2. If not covered, prefer upstream.
3. If covered, preserve the behavior with the smallest possible change.
4. Ensure resulting code remains readable and compatible with project conventions.
5. If behavior changes, update `.github/COMMIT_INTENT.md`.
