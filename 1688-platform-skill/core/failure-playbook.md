# Failure Playbook

Use this when the happy path is blocked or degraded.

## No Useful Results

- Say which search phrases were tried.
- Suggest 1 to 3 narrower or alternative phrases.
- Do not fabricate a shortlist from weak matches.

## Login Or Captcha Restriction

- State that access is restricted.
- Ask for a lawful operator-provided session or a manual page-open assist.
- Do not attempt bypass, automation tricks, or hidden-interface fallback.

## Page Structure Instability

- Explain which page type became unreadable.
- Fall back to whichever visible surfaces still work, such as search results or product pages.
- Mark the report as partial and identify the missing evidence.

## Missing Host Capability

- If browser navigation, page reading, or file writing is unavailable, stop early.
- Report the missing capability as the blocker.

## Partial Report Rule

If a full run is impossible but some evidence was collected:
- produce a partial report
- label it partial near the top
- list the exact blocker
- separate collected facts from missing validation
