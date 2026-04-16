# Live Validation: Direct 1688 Failure Path

- Validation date: 2026-04-16
- Validation environment: Codex web browsing environment, not a full OpenClaw host
- Validation result: direct `1688.com` access failed in this environment

## Direct URLs Attempted

- `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%B8%8D%E9%94%88%E9%92%A2%20%E4%BF%9D%E6%B8%A9%20%E9%A5%AD%E7%9B%92`
- `https://detail.1688.com/offer/672143711850.html`
- `https://detail.1688.com/offer/594037284720.html`
- `https://detail.1688.com/offer/625220039727.html`

## Observed Failure

In the validation environment above, opening direct `1688.com` search and detail pages returned non-retryable errors instead of readable page content.

## Why This Matters

This is a real failure-path example for the skill because it exercises one of the documented risk cases:
- target pages are not reachable or readable in the current environment

## Required Downgrade Behavior

When this happens, the skill should:
- state that direct `1688.com` access failed in the current environment
- avoid pretending supplier-page validation succeeded
- avoid hidden-interface fallback or bypass attempts
- either stop with a blocker report or continue only on clearly labeled mirror-accessible evidence

## Operator Next Step

If the goal is a direct-site run instead of a mirror-based partial run, the next step is:
- provide a host environment that can open direct `1688.com` search, product, and supplier pages through lawful operator-controlled access

## Validation Conclusion

This file is the real failure-path evidence paired with the mirror-based partial happy path from the same date.
It confirms that the skill's downgrade path is necessary and not theoretical.
