# Codex Operator-Authenticated Direct Recheck

- Validation date: 2026-04-17
- Validation environment: Codex + operator-provided authenticated Chrome session
- Goal: determine whether Codex can now justify `validated_direct` under `operator_authenticated` mode

## Direct Pages Rechecked

- Search query: `304不锈钢 保温饭盒`
- Search query: `304不锈钢 午餐盒`
- Product detail: `https://detail.1688.com/offer/672143711850.html`
- Supplier page: `https://cahongfu.1688.com/?offerId=992411055961&td_page_id=PC-DEFAULT-2025`

## Observed Outcome

The operator-authenticated Chrome session materially improved Codex direct access, but not enough to justify a full status upgrade.

Stable direct reads in this pass:
- the product detail page for `672143711850` was readable in-browser and exposed visible title, supplier name, price band, MOQ, and product attributes
- the supplier page for `潮州市宏富五金制品有限公司` was readable in-browser and exposed visible shop age, service score,主营类目, 回头率, region, and establishment date

Search-path behavior in this pass:
- earlier operator-authenticated probes in the same session showed readable direct search-result text for `304不锈钢 保温饭盒` and `304不锈钢 午餐盒`, including visible product snippets and supplier names
- a follow-up lightweight recheck for `304不锈钢 午餐盒` redirected to the direct `验证码拦截` punish flow instead of a stable result page

## What This Recheck Proves

- Codex can now read direct `1688` detail pages in-browser when an operator-provided authenticated Chrome session is available
- Codex can now read direct `1688` supplier pages in-browser under the same authenticated session
- Codex direct search is still unstable in the current environment; repeated automated search loads can fall back into punish / slider verification
- `validated_direct` is still not justified for Codex because the end-to-end direct search -> detail -> supplier workflow was not stable in the same run

## Resulting Adapter State

- keep `adapters/codex/adapter-manifest.json` at `validation_status = validated_partial`
- record `validated_auth_mode = mixed`
- interpret the current Codex validation state as:
  - mirror-assisted path proven without authenticated direct browsing
  - operator-authenticated direct detail and supplier reads proven
  - direct search still unstable

## Next Step

If `validated_direct` is required for Codex, the narrowest remaining step is:
- start from an operator-opened readable direct search results page in the authenticated Chrome session
- let Codex continue from that live search page into one retained product detail page and one supplier page without re-triggering punish
