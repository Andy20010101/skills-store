# Codex vs Hermes Report Convergence

- Date: 2026-04-16
- Compared reports:
  - `reports/lunch-box-suppliers.md`
  - `reports/hermes-lunch-box-suppliers.md`

## Drift Found

1. Link semantics drift
   - Codex used mirror pages as `Supplier link`.
   - Hermes promoted the underlying `detail.1688.com` URLs into `Supplier link`.
   - This made it unclear which page was actually inspected.

2. Representative-product drift
   - Codex sometimes created extra product rows from snippet evidence on the same mirror page.
   - Hermes kept a single anchor product row and summarized the repeated variants in prose.

3. Raw-output drift
   - Hermes emitted a banner, a duplicated report body, and a session trailer in its raw output.
   - Codex produced a cleaner report artifact directly.

## Convergence Decisions

- The canonical report now uses `Evidence page link` for the page that was actually inspected.
- `Source 1688 link` is kept as a separate field when a mirror or proxy exposes the underlying `1688.com` URL.
- Each supplier must have one anchor representative product.
- Additional representative products should only be added when they have a distinct inspected page or a distinct linkable listing.
- Hosts must save a clean canonical Markdown artifact before writing `run-result.json`.
- Noisy raw transcripts can still be preserved through `run_notes_ref`.

## Touched Contract Files

- `core/output-contract.md`
- `core/agent-capability-contract.md`
- `interface/README.md`
- `interface/capability-manifest.schema.json`
- `adapters/*/adapter-manifest.json`
