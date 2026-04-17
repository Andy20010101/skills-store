# Agent Capability Contract

This is the shared adapter boundary for any host or agent.
The machine-readable form of this boundary is [../interface/capability-manifest.schema.json](../interface/capability-manifest.schema.json).

## Required Capabilities

A compatible host must be able to do all of these:
- navigate to a search page, product page, and supplier page
- read visible page content with enough stability to capture facts
- follow links across a small candidate set
- write a Markdown report to a file or return it as final output
- emit clean Markdown directly or support adapter-side normalization of raw host output into a canonical report artifact

## Optional But Useful Capabilities

- structured intermediate-output writing such as `candidate-set.json` and `evidence-notes.json`
- keyword search assistance
- page screenshots
- tab management
- file append or report revision

## Capability Mapping Rule

Every adapter should map native tools to the same conceptual operations:
- `navigate_page`
- `read_visible_content`
- `open_supplier_or_product_link`
- `write_candidate_set` when the host supports phased execution
- `write_evidence_notes` when the host supports phased execution
- `write_markdown_report`
- `normalize_final_output`

The adapter may rename those operations, but it must not change the underlying business contract.

## Authentication Mode Rule

Some hosts can lawfully browse direct marketplace pages only after a human operator logs in first and hands over the live browser session.
That should be modeled as a supported authentication mode, not as an automatic failure of the workflow.

Use this split:
- `validation_status` describes whether the workflow is proven
- authentication metadata describes under which session mode it is proven

So a host may be considered direct-capable when:
- the direct workflow is proven end to end
- and the validated session mode is explicitly `operator_authenticated`

## Output Normalization Rule

Adapters are responsible for the final saved report artifact, not just the host's raw transcript.

That means the adapter should:
- preserve the exact page that was inspected as `Evidence page link`
- preserve the underlying `1688.com` URL separately as `Source 1688 link` when a mirror or proxy exposes one
- strip banners, duplicated completions, session ids, and other non-report wrappers before saving the canonical Markdown artifact
- point `run-result.json` at the canonical report artifact, not the noisy raw transcript

If the raw transcript is still useful, store it separately and reference it through `run_notes_ref`.

When the host is brittle or the authenticated session is expensive, the adapter should prefer:
1. bounded search harvest into `candidate-set.json`
2. bounded evidence review into `evidence-notes.json`
3. final report synthesis from the reviewed evidence

Do not force search expansion, supplier review, and report synthesis into one long run when the host is more stable with staged execution.

## Non-Goals

This contract does not require:
- hidden API access
- captcha solving
- long-running crawl queues
- background jobs
- structured database writes

## Compatibility Test

Before claiming a host is supported, confirm that one real run can:
- open a target result page
- open at least one representative product page
- open at least one supplier page when available
- write a clean supplier-first Markdown report after any required normalization

When the host uses staged execution, also persist the intermediate `candidate-set.json` and `evidence-notes.json` artifacts so the compatibility test can be audited step by step.
When the host uses the structured interface, persist this check as a validated `capability-manifest.json`.
