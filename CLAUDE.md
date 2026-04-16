# 1688 Supplier Discovery For Claude Code

Use this repo as an agent-agnostic supplier research package.
If your harness prefers machine-readable exchange over prompt-only exchange, use the schemas in `interface/`.

Start from:
- [core/agent-capability-contract.md](core/agent-capability-contract.md)
- [core/host-preflight.md](core/host-preflight.md)
- [core/brief-template.md](core/brief-template.md)
- [core/supplier-rubric.md](core/supplier-rubric.md)
- [core/output-contract.md](core/output-contract.md)

Rules:
- keep the run to one product direction
- use only visible page evidence
- separate facts, heuristics, and unknowns
- do not attempt captcha bypass or hidden-interface fallback
- if direct `1688.com` access fails, use the downgrade path in [core/failure-playbook.md](core/failure-playbook.md)

Evidence and examples:
- [examples/example-happy-path-report.md](examples/example-happy-path-report.md)
- [examples/example-failure-report.md](examples/example-failure-report.md)
- [examples/live-validation-2026-04-16-mirror-happy-path.md](examples/live-validation-2026-04-16-mirror-happy-path.md)
- [examples/live-validation-2026-04-16-direct-site-failure.md](examples/live-validation-2026-04-16-direct-site-failure.md)
