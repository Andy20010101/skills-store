# 1688 Supplier Discovery

Agent-agnostic 1688 supplier research package.

This repo is structured so the same business logic can be reused across:
- Codex
- Claude Code
- OpenClaw
- Hermes
- other browser-capable agents

## Layout

- `core/`: shared research contract, rubric, output schema, and failure policy
- `interface/`: machine-readable request, capability, and run-result schemas
- `examples/`: sample reports and live validation evidence
- `reports/`: canonical run artifacts produced by specific agent executions
- `verification/`: interop notes, prompts, and convergence records for agent-to-agent checks
- `adapters/`: host-specific prompt or skill entrypoints
- root `SKILL.md`: Codex adapter

## Minimal Host Capability Contract

Any host can use this package if it can provide:
- browser navigation
- visible page reading
- product and supplier page traversal
- Markdown output writing

See [core/agent-capability-contract.md](core/agent-capability-contract.md).

## Agent Interface

Different hosts should exchange the same three final surfaces:
- `request.json`: validated by [interface/research-request.schema.json](interface/research-request.schema.json)
- `capability-manifest.json`: validated by [interface/capability-manifest.schema.json](interface/capability-manifest.schema.json)
- `run-result.json`: validated by [interface/run-result.schema.json](interface/run-result.schema.json)

For staged or turn-constrained hosts, the repo now also recommends two intermediate surfaces:
- `candidate-set.json`: validated by [interface/candidate-set.schema.json](interface/candidate-set.schema.json)
- `evidence-notes.json`: validated by [interface/evidence-notes.schema.json](interface/evidence-notes.schema.json)

The human-readable report still follows [core/output-contract.md](core/output-contract.md).
The saved report artifact should be a clean canonical Markdown file, not a raw host transcript with banners or session metadata.
See [interface/README.md](interface/README.md) for the full flow.

## Validation Artifacts

This repo keeps both human-readable reports and machine-readable run metadata:
- canonical reports live under `reports/`
- raw or noisy host transcripts may also live under `reports/` when worth preserving
- interop prompts, request files, and convergence notes live under `verification/`

When a raw transcript is kept, `run-result.json` should still point at the cleaned canonical Markdown artifact.
When a host is better served by phased execution, the intermediate `candidate-set.json` and `evidence-notes.json` artifacts should live under `verification/` so search harvesting, evidence review, and report synthesis can be debugged separately.

For Hermes specifically, the repo now also includes an operator-assisted login path for direct-site validation:
- [verification/hermes-operator-assisted-login-workflow.md](verification/hermes-operator-assisted-login-workflow.md)
- [verification/hermes-post-login-search-harvest-query.txt](verification/hermes-post-login-search-harvest-query.txt)
- [verification/hermes-post-login-evidence-pass-query.txt](verification/hermes-post-login-evidence-pass-query.txt)
- [verification/hermes-post-login-report-synthesis-query.txt](verification/hermes-post-login-report-synthesis-query.txt)
- [verification/hermes-post-login-direct-validation-query.txt](verification/hermes-post-login-direct-validation-query.txt)
- `verification/templates/` for post-login validation note and `run-result.json` templates

## Important Boundary

This package defines a low-frequency supplier research workflow.
It is not:
- a crawler platform
- an anti-bot toolkit
- a hidden-interface reverse-engineering project
- a runtime orchestration framework
