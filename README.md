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

Different hosts should exchange the same three surfaces:
- `request.json`: validated by [interface/research-request.schema.json](interface/research-request.schema.json)
- `capability-manifest.json`: validated by [interface/capability-manifest.schema.json](interface/capability-manifest.schema.json)
- `run-result.json`: validated by [interface/run-result.schema.json](interface/run-result.schema.json)

The human-readable report still follows [core/output-contract.md](core/output-contract.md).
See [interface/README.md](interface/README.md) for the full flow.

## Important Boundary

This package defines a low-frequency supplier research workflow.
It is not:
- a crawler platform
- an anti-bot toolkit
- a hidden-interface reverse-engineering project
- a runtime orchestration framework
