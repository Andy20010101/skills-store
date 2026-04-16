---
name: "1688-supplier-discovery-openclaw"
description: "OpenClaw adapter for the shared 1688 supplier discovery contract. Use when the host is OpenClaw and the task is low-frequency browser-first supplier research for one product direction."
---

# 1688 Supplier Discovery For OpenClaw

This adapter wraps the shared contract in `../../core/`.
If the host wants a machine-readable exchange layer, pair this adapter with `../../interface/`.

Use these files as the source of truth:
- [agent-capability-contract.md](../../core/agent-capability-contract.md)
- [host-preflight.md](../../core/host-preflight.md)
- [brief-template.md](../../core/brief-template.md)
- [search-playbook.md](../../core/search-playbook.md)
- [supplier-rubric.md](../../core/supplier-rubric.md)
- [output-contract.md](../../core/output-contract.md)
- [failure-playbook.md](../../core/failure-playbook.md)

OpenClaw-specific expectation:
- use the host's existing browser and page-reading tools
- write a Markdown report as the final artifact
- keep `Evidence page link` and `Source 1688 link` separate when mirror-assisted evidence is used
- normalize the saved report artifact if the host emits any non-report wrappers
- do not require runtime-core changes to execute the workflow
