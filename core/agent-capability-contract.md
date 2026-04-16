# Agent Capability Contract

This is the shared adapter boundary for any host or agent.
The machine-readable form of this boundary is [../interface/capability-manifest.schema.json](../interface/capability-manifest.schema.json).

## Required Capabilities

A compatible host must be able to do all of these:
- navigate to a search page, product page, and supplier page
- read visible page content with enough stability to capture facts
- follow links across a small candidate set
- write a Markdown report to a file or return it as final output

## Optional But Useful Capabilities

- keyword search assistance
- page screenshots
- tab management
- file append or report revision

## Capability Mapping Rule

Every adapter should map native tools to the same conceptual operations:
- `navigate_page`
- `read_visible_content`
- `open_supplier_or_product_link`
- `write_markdown_report`

The adapter may rename those operations, but it must not change the underlying business contract.

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
- write a supplier-first Markdown report

When the host uses the structured interface, persist this check as a validated `capability-manifest.json`.
