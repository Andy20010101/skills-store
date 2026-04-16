---
name: "1688-supplier-discovery"
description: "Run low-frequency, browser-first 1688 supplier research for a single product direction and produce a supplier-first Markdown shortlist with visible facts, heuristic judgments, unknowns, and source links. This root SKILL.md is the Codex adapter over an agent-agnostic 1688 supplier discovery contract."
---

# 1688 Supplier Discovery For Codex

This root `SKILL.md` is the Codex-facing adapter for the shared supplier-discovery contract in `core/`.
If another host or agent is being used, prefer the matching adapter in `adapters/` or reuse the shared docs directly.

Use this skill when the user wants a reusable 1688 supplier research workflow for one product direction.

Do not use it for:
- bulk crawling
- captcha bypass or access-circumvention work
- host-platform runtime changes
- cross-marketplace research as a default path

## Preconditions

Before starting, confirm all of these:
- The host can navigate browser pages, read visible page content, and write a Markdown report.
- The operator can lawfully access the target 1688 pages or provide an already-valid session when login is required.
- The brief is narrow enough for one pass: one product direction, not a whole catalog.

If any prerequisite is missing, stop and report the blocker instead of widening scope.
Use [agent-capability-contract.md](core/agent-capability-contract.md) and [host-preflight.md](core/host-preflight.md) for the exact pre-run check.

## Required Inputs

Ask for or infer only the minimum needed:
- product direction or target item
- suggested search keywords or synonyms
- price band, MOQ, or region preferences if the operator has them
- any must-have or must-avoid supplier traits
- preferred output file path if the host requires one

If the brief is incomplete, use [brief-template.md](core/brief-template.md).

## Workflow

### 1. Normalize the brief

- Restate the product direction in one sentence.
- Convert the brief into 2 to 5 search phrases.
- Keep only constraints that affect supplier filtering in the first pass.

### 2. Search and narrow

- Use host browser tools to inspect 1688 search results.
- Build an initial supplier candidate set from visible result pages.
- Prefer breadth first, then depth: do not spend the whole pass on one seller too early.

Use [search-playbook.md](core/search-playbook.md) when choosing phrases, deciding when to branch, or narrowing a noisy search result set.

### 3. Inspect candidate evidence

For each shortlisted supplier:
- open the supplier page when available
- open 1 to 3 representative product pages
- record only page-visible evidence
- separate facts, heuristics, and unknowns

Use [supplier-rubric.md](core/supplier-rubric.md) while reading pages.

### 4. Rank conservatively

- Rank suppliers by how strong and reviewable the visible evidence is.
- Do not pretend missing information was verified.
- If two candidates are close, preserve both and state the uncertainty.

### 5. Produce the report

- Output a supplier-first Markdown report.
- Follow [output-contract.md](core/output-contract.md).
- Include original links for every supplier and representative product cited.

## Quality Rules

- Facts are only what is visibly present on the page.
- Heuristics are allowed, but they must be labeled as judgment.
- Unknowns must stay explicit.
- Do not convert sparse signals into pseudo-precision scoring.
- Prefer 3 to 8 suppliers in the first pass unless the market is clearly thinner.

## Failure Behavior

If the run is blocked or degraded:
- follow [failure-playbook.md](core/failure-playbook.md)
- explain what was attempted
- state whether the issue is no results, page structure instability, login restriction, captcha, or missing host capability
- give the operator the narrowest next step needed to continue

## Output Reminder

The final report must make it easy for another operator to see:
- what was searched
- which suppliers were shortlisted
- what evidence supports each supplier
- what remains unknown
- which links should be revisited next

## Example Material

The repo includes illustrative examples for format and judgment discipline:
- [example-happy-path-report.md](examples/example-happy-path-report.md)
- [example-failure-report.md](examples/example-failure-report.md)

They are examples, not proof that the current host or account can already complete a real run.

Current environment validation artifacts:
- [live-validation-2026-04-16-mirror-happy-path.md](examples/live-validation-2026-04-16-mirror-happy-path.md)
- [live-validation-2026-04-16-direct-site-failure.md](examples/live-validation-2026-04-16-direct-site-failure.md)

Those two files are real validation notes from April 16, 2026. They prove the current research environment could gather partial supplier evidence through accessible mirror pages, while direct `1688.com` page opening still failed in the same environment.
