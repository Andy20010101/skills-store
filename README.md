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

## Important Boundary

This package defines a low-frequency supplier research workflow.
It is not:
- a crawler platform
- an anti-bot toolkit
- a hidden-interface reverse-engineering project
- a runtime orchestration framework
