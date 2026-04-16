# Live Validation: Mirror-Accessible Happy Path

- Validation date: 2026-04-16
- Validation environment: Codex web browsing environment, not a full OpenClaw host
- Validation result: partial happy path succeeded through accessible 1688 mirror pages that expose source `detail.1688.com` links

## Scope

This validation checks whether the skill can still produce a supplier-first shortlist when direct `1688.com` pages are not openable in the current environment, but mirror pages remain accessible.

## Research Brief Used

- Product direction: stainless steel insulated lunch box
- Search intent: shortlist reviewable suppliers for a first sourcing pass
- Constraints: prefer visible MOQ, repeated category evidence, and clear stainless-steel / insulation signals

## Path Used

The current environment could not open direct `1688.com` search or detail URLs, so the run used mirror pages that exposed:
- mirror product page URL
- direct source `detail.1688.com` product URL
- visible price and MOQ
- supplier name
- visible related-product snippets in some cases

## Shortlist

### 1. Shitai / `shitai stainless steel`
- Mirror page: `https://sino2b.com/us/products/641818247570.html`
- Source URL shown by mirror: `https://detail.1688.com/offer/641818247570.html`

#### Page-Visible Facts
- MOQ shown as `>=2 piece`
- 90-day sales shown as `200k`
- product details show `304 stainless steel`
- visible capacities include `1.2L`, `1.6L`, and `2.6L`
- the mirror page shows `Insulation or not: Yes`
- the mirror page shows `Box layers: Three layers`
- the mirror page shows `Printed LOGO: OK`
- the mirror page shows `Customized processing: Yes`

#### Heuristic Judgments
- strongest visible evidence in this run
- product detail completeness is higher than the other candidates
- looks more reviewable for a follow-up sourcing pass than weaker single-listing candidates

#### Unknowns
- factory ownership is still not directly proven
- supplier page itself was not directly validated in this environment
- certification, lead time, and export experience remain unknown

### 2. 潮州市潮安区辛博尔不锈钢制品厂
- Mirror page: `https://www.1688wholesale.com/en/1688/china_alibaba_item/672143711850.html`
- Source URL shown by mirror: `https://detail.1688.com/offer/672143711850.html`

#### Page-Visible Facts
- main product page shows `US.$4.29` and MOQ `>=2`
- the mirror page lists multiple related stainless-steel lunch-box products from the same supplier
- visible related lunch-box prices include `US.$3.86`, `US.$6.87`, `US.$3.29`, and `US.$4.29`
- visible related lunch-box MOQs include `>=2`, `>=30`, and `>=32`
- the same supplier page also shows a related stainless-steel soup pot listing

#### Heuristic Judgments
- strongest repeated category evidence among the mirror pages hosted on `1688wholesale.com`
- looks more category-focused than a seller with only one lunch-box listing and unrelated follow-on products

#### Unknowns
- supplier profile page was not directly validated
- no visible proof of factory-direct status in the current environment
- material claims beyond listing titles were not independently confirmed

### 3. 潮州市潮安区奔展不锈钢制品有限公司
- Mirror page: `https://www.1688wholesale.com/en/1688/china_alibaba_item/594037284720.html`
- Source URL shown by mirror: `https://detail.1688.com/offer/594037284720.html`

#### Page-Visible Facts
- main product page shows `US.$4.25` and MOQ `>=2`
- supplier name is visible on the mirror page
- at least one related product snippet is visible from the same supplier: classic stainless-steel kettle at `US.$4.35`, MOQ `>=2`

#### Heuristic Judgments
- still usable as a low-confidence candidate because the product itself is on target and MOQ is visible
- weaker than the first two suppliers because visible related-product breadth is thinner and less lunch-box-specific

#### Unknowns
- no clear supplier-page validation
- category focus is less certain than supplier 1 and supplier 2
- no visible proof of manufacturing depth

## Outcome

This environment was able to produce a real 3-supplier shortlist for one product direction, but only through mirror-accessible pages.

## Important Limitation

This does **not** prove that:
- direct `1688.com` pages are reachable in the target host
- supplier profile pages are stable in the target host
- the operator already has a lawful reusable 1688 session in the target host

It proves a narrower claim:
- the skill logic, report shape, and fact / heuristic / unknown separation remain usable when mirror pages with source links are available
