# Host Preflight

Run this check before attempting a real supplier research pass.

## Capability Check

Confirm the host can do all of these:
- open a 1688 search result page
- open at least one supplier page or shop page
- open at least one product detail page
- read visible page content in a stable way
- save or write a Markdown result

If any one of these is missing, stop and report:
- which capability is missing
- whether the blocker is host-side or access-side
- what the operator would need to provide next

## Access Check

Confirm:
- the operator has a lawful access path to the needed 1688 pages
- if login is required, the session already exists and is operator-controlled
- the run does not require bypassing captcha or access limits

If access is unstable:
- do not escalate into hidden-interface work
- do not invent a workaround
- downgrade to a blocker report or partial report

## Brief Sanity Check

Reject or narrow the brief when:
- it mixes unrelated product directions
- it asks for marketplace-wide crawling
- it implies procurement execution rather than supplier discovery
- it requires fields that are usually not visible on-page

## Ready-To-Run Summary

Before the run starts, you should be able to state:
- target product direction
- search phrases to try first
- key filtering constraints
- output location or report handoff path
