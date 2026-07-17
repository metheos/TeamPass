# Local Commit Intent Ledger

Purpose: document why local commits exist so their goals can be preserved across upstream merges while still adopting important upstream changes.

## Durable Local Goals

These are the goals that justify preserving local changes when conflicts happen:

- Security hardening
- Encryption correctness and key lifecycle safety
- On-prem operational stability
- Backward compatibility for upgrades and existing instances
- Static analysis and code quality constraints

## How To Use This File

For each local change that should survive upstream merges, add one entry.

Keep entries short, concrete, and testable.

## Entry Template

- ID: INTENT-XXXX
- Scope: file(s) or feature area
- Category: security | encryption | stability | compat | quality
- Why this exists: one short sentence
- Must remain true after merge: concrete behavior requirement
- Fast verification: 1-3 quick checks
- Related commits/PRs: hash or link text

## Intent Entries

- ID: INTENT-0001
- Scope: Repository-wide guidance
- Category: quality
- Why this exists: Ensure AI-assisted work preserves local goals during upstream syncs.
- Must remain true after merge: merge and conflict resolution workflows reference this ledger before dropping local behavior.
- Fast verification: confirm `.github/copilot-instructions.md` and `.github/instructions/commit_intent_persistence.instructions.md` both exist and reference this file.
- Related commits/PRs: pending

- ID: INTENT-0002
- Scope: Item tree refresh and search flow (`pages/items.js.php`, `sources/items.queries.php`, `sources/tree.php`)
- Category: stability
- Why this exists: Reduce unnecessary tree refreshes and improve responsiveness when browsing/searching items.
- Must remain true after merge: item tree/search requests avoid forced full refresh unless state requires it, and folder refresh requests preserve support for scoped path handling/search term propagation.
- Fast verification: 1) run item search and confirm tree does not fully reload on every keystroke, 2) navigate folders and confirm refresh behavior is state-aware, 3) confirm item and tree requests still return successfully when include-path style options are used.
- Related commits/PRs: cf762a99a863c87658d05efcf79a20d221579f82, e07bcdf996c3fc86018dd1bf89ed93d68a000d81, f50b945b6148f49ccc080de65d086ae2dc587c0b, 32a090c7c58c88488478c0112db911bacb6f9c6a, c5e9df6c19920597bd616fcd84707799364559c1, dd9f4e79aa3dc0dd0172a8d193542b39062aac56, 80a6d455f623ba9b521a011dc7f8215552b58fb9

- ID: INTENT-0003
- Scope: Item and tree observability/performance safeguards (`sources/items.queries.php`, `sources/tree.php`)
- Category: quality
- Why this exists: Preserve lightweight performance instrumentation and guardrails for payload/response behavior.
- Must remain true after merge: server timing visibility for key item/tree requests remains available and large item detail payloads are constrained to prevent oversized responses.
- Fast verification: 1) inspect response headers for item/tree endpoints and confirm server timing data is present, 2) request item details with large field data and confirm trimmed/controlled response size behavior remains in place.
- Related commits/PRs: f7729a6f9b090b0fa78926a07766bc2fbba765e3, 4bcf7a583c9a35618567b519d1a57b20ccfec337

- ID: INTENT-0004
- Scope: Mobile-friendly UI for items/search pages (`pages/items.php`, `pages/items.js.php`, `pages/search.php`, `pages/search.js.php`)
- Category: compat
- Why this exists: Keep the items/search experience usable on small screens without regressing desktop behavior.
- Must remain true after merge: item form actions, metadata layout, titles/alerts/dropdowns, and search interactions remain functional and readable on mobile widths.
- Fast verification: 1) test items and search pages at mobile viewport width, 2) confirm item actions and dropdowns remain usable, 3) confirm empty item titles are not rendered with broken spacing.
- Related commits/PRs: ea6567630c58098f76e17c8305e890fb18937dcb, 7962ebeaed9ad1055645bb2ad5962b1b57c3b491, bd63b823a41b908aaf434ab44406d80d59f11853, 6a1731a88a959d9baad9d2cc6df52762fb647c4e, 1f073629f5464587aac5533b00c5ff1708a15333, 28d70dc2e79dd5f8d6ee69cb2e86329cbcf07104

- ID: INTENT-0005
- Scope: Folder creation rights shim (`api/custom/folder_create_with_rights_shim.php`)
- Category: compat
- Why this exists: Preserve custom compatibility behavior for folder creation workflows requiring explicit rights management.
- Must remain true after merge: the shim endpoint remains available and continues to enforce intended role/rights mapping during folder creation flows.
- Fast verification: 1) invoke shim flow for folder creation and verify success response, 2) verify resulting folder permissions match expected role rights, 3) confirm unauthorized callers cannot create folders through shim flow.
- Related commits/PRs: 3ef122f7a35bd1aafa79cb1c46f6117b1c8c3ad4

- ID: INTENT-0006
- Scope: Install/upgrade parity for local item behavior changes (`install/install-steps/run.step5.php`, `install/upgrade_run_3.1.7.php`)
- Category: compat
- Why this exists: Ensure local runtime behavior changes do not diverge between fresh installs and upgraded instances.
- Must remain true after merge: any local defaults/flags tied to item behavior continue to be applied in both installation and upgrade paths.
- Fast verification: 1) verify new install path seeds expected values, 2) verify upgrade path sets the same values for existing instances, 3) confirm items page behavior matches between both environments.
- Related commits/PRs: 4bcf7a583c9a35618567b519d1a57b20ccfec337
