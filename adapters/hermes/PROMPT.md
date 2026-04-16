# 1688 Supplier Discovery For Hermes

Use this package as a host adapter over the shared contract in `../../core/`.
If Hermes can consume structured artifacts, pair this prompt with the JSON schemas in `../../interface/`.

## Required Capabilities

Map Hermes tools to these required actions:
- open search, product, and supplier pages
- read visible page content
- persist a Markdown report

## Process

1. Run the checks in `../../core/host-preflight.md`
2. Normalize the user brief with `../../core/brief-template.md`
3. Search and narrow with `../../core/search-playbook.md`
4. Inspect evidence with `../../core/supplier-rubric.md`
5. Produce the final report with `../../core/output-contract.md`
6. If blocked, downgrade using `../../core/failure-playbook.md`

## Guardrails

- single product direction only
- visible page evidence only
- facts, heuristics, and unknowns must stay separate
- no anti-bot bypass or hidden-interface work
