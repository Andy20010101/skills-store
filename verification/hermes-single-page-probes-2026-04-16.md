# Hermes Single-Page Browser Probes

- Validation date: 2026-04-16
- Goal: separate browser-read stability from full-workflow complexity after the earlier Hermes browser validation stalled

## Probe Artifacts

- Prompt: `verification/hermes-direct-detail-probe-2026-04-16.txt`
- Raw output: `reports/hermes-direct-detail-probe-2026-04-16.raw.txt`
- Canonical report: `reports/hermes-direct-detail-probe-2026-04-16.md`

- Prompt: `verification/hermes-mirror-page-probe-2026-04-16.txt`
- Raw output: `reports/hermes-mirror-page-probe-2026-04-16.raw.txt`
- Canonical report: `reports/hermes-mirror-page-probe-2026-04-16.md`

## Results

### Direct detail probe

- Target page: `https://detail.1688.com/offer/672143711850.html`
- Outcome: blocked
- Hermes completed the run and emitted a final report
- The reported visible surface was a login page rather than the requested product detail page

### Mirror page probe

- Target page: `https://www.1688wholesale.com/en/1688/china_alibaba_item/672143711850.html`
- Outcome: success
- Hermes completed the run and emitted a final report
- The report captured visible heading, source URL, price, MOQ, local express, and seller name from the opened mirror page

## What These Probes Prove

- Hermes browser automation is real, not simulated
- Hermes can complete a narrow browser read and emit a final Markdown artifact
- direct detail access can degrade into login gating in the current Hermes host
- mirror-page reading is viable in the current Hermes host

## Why Hermes Still Stays `not_validated`

The compatibility test for a supported host still expects one real workflow that can:
- open a result page
- open at least one representative product page
- open at least one supplier page when available
- write a clean supplier-first Markdown report

The single-page probes prove page-level capability, but they do not yet prove that Hermes can complete the full supplier-discovery workflow end to end.

## Next Step

The next Hermes validation should be a constrained multi-step run that starts from one readable mirror page and then attempts exactly one supplier-page hop, instead of a full shortlist workflow.
