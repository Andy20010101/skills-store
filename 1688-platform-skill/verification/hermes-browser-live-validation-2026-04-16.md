# Hermes Browser-Side Live Validation

Update later on 2026-04-16: this note remains a historical record of the unauthenticated host state. Hermes was later raised to `validated_partial` via the operator-assisted login flow documented in `verification/hermes-post-login-direct-2026-04-16.md`.

- Validation date: 2026-04-16
- Validation environment: Hermes CLI with `browser` and `web` toolsets enabled
- Prompt file: `verification/hermes-browser-live-query-2026-04-16.txt`
- Raw stdout artifact: `reports/hermes-browser-live-validation-2026-04-16.raw.txt`

## Validation Goal

Verify whether the Hermes adapter can complete a real browser-side supplier-discovery run in the current host, preferably through direct `1688.com` pages and otherwise through a clearly labeled mirror-assisted downgrade path.

## What Was Confirmed About The Host

- `hermes tools list` showed both `browser` and `web` enabled for the CLI profile
- the live run launched Playwright / Chromium rather than staying in local-only text mode

## Observed Runtime Behavior

- Hermes started a live `chat` run against the validation prompt
- the run launched a headless Chromium session and browser automation subprocesses
- the browser flow advanced past the initial prompt and entered page-navigation actions
- runtime inspection showed Hermes opening the mirror fallback page `https://www.1688wholesale.com/en/1688/china_alibaba_item/672143711850.html`
- the browser flow then stalled in repeated interaction steps, including a visible `click @e50` action
- later runtime inspection showed another mirror-page open attempt for `https://www.1688wholesale.com/en/1688/china_alibaba_item/671382445624.html`
- no final Markdown report was emitted to stdout before the run had to be terminated

## Why This Does Not Count As Validation

This run proves that Hermes can launch real browser automation in the current host.
It does **not** yet prove that Hermes can complete a stable browser-side supplier-discovery run and produce a canonical report artifact.

Because the run never emitted a final report:
- no supplier shortlist can be claimed from this attempt
- no evidence mode above `none` should be recorded for the completed run artifact
- `validation_status = not_validated` should remain in `adapters/hermes/adapter-manifest.json`

## Resulting Adapter State

- keep `adapters/hermes/adapter-manifest.json` at `validation_status = not_validated`
- treat the earlier local-only report-generation run as useful output-normalization evidence, not as browser validation

## Next Step

The next useful Hermes test should be narrower than a full workflow:
- run a single-page browser probe against one direct detail URL
- run a single-page browser probe against one mirror page
- only after one of those produces stable visible-page extraction should Hermes be retried on the full supplier-discovery workflow
