# Codex Direct-Site Recheck

- Validation date: 2026-04-16
- Validation environment: Codex web browsing environment
- Request shape: `interface/examples/research-request.example.json`
- Goal: verify whether the Codex adapter can now justify `validated_direct`

## Direct URLs Attempted

- `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%B8%8D%E9%94%88%E9%92%A2%20%E4%BF%9D%E6%B8%A9%20%E9%A5%AD%E7%9B%92`
- `https://detail.1688.com/offer/672143711850.html`
- `https://detail.1688.com/offer/594037284720.html`
- `https://detail.1688.com/offer/641818247570.html`

## Observed Outcome

Browser-side open attempts on the direct URLs above did not yield readable page content in the Codex browsing tool during this pass.

Additional shell-level checks showed a more nuanced result:
- the direct search URL returned a punish / anti-bot script instead of a normal readable results page
- the direct product detail URL for `672143711850` returned normal HTML, including the product title `304不锈钢保温饭盒多层午餐盒成人学生带饭盒分格便当盒商超礼品`

So the current environment shows some direct HTTP reachability, but not a clean browser-readable direct workflow for the Codex adapter.
Because the search path was degraded and the browser-side result was still not stable, supplier-page validation was not advanced in this pass.

## What This Recheck Proves

- the Codex adapter still supports the shared contract and canonical-output rules
- direct `1688.com` browser validation is still incomplete in the current environment
- direct product detail HTML may be reachable outside the browser tool, but that does not satisfy the browser-first validation requirement
- `validated_direct` is still not justified for the Codex adapter

## Resulting Adapter State

- keep `adapters/codex/adapter-manifest.json` at `validation_status = validated_partial`
- continue treating mirror-assisted evidence as the highest validated path for Codex in this environment

## Next Step

If direct-site validation is required, rerun the same request in a Codex environment that can lawfully open:
- one direct `1688.com` search results page
- one direct product detail page
- one direct supplier page
