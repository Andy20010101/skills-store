# Hermes Post-Login Direct Validation

- Validation date: 2026-04-16
- Validation environment: Hermes CLI attached to a live Chrome session via CDP
- Prompt file: `verification/hermes-post-login-direct-validation-query.txt`
- Report artifact: `reports/hermes-post-login-direct-2026-04-16.md`
- Run-result artifact: `verification/hermes-post-login-direct-2026-04-16.run-result.json`

## Operator Session

- Browser type: Chrome
- CDP endpoint: `http://172.18.144.1:9223`
- Login state prepared by operator: yes
- Direct product page visibly open before run: yes

## Pages Attempted

- direct search page: `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%BF%9D%E6%B8%A9%E9%A5%AD%E7%9B%92` and `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%B8%8D%E9%94%88%E9%92%A2%20%E4%BF%9D%E6%B8%A9%20%E9%A5%AD%E7%9B%92`
- direct product detail page: `https://detail.1688.com/offer/672143711850.html` in the preflight probe, plus `https://detail.1688.com/offer/851436523899.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=55c752d094ad4fbe8038167439cb31f9&sessionid=c10c76944aa96f5cd0afae76266cb818` in the full run
- direct supplier page: `https://shop07866986b0436.1688.com/?offerId=851436523899&td_page_id=PC-DEFAULT-2025`

## Outcome

- Final status: partial
- Evidence mode: direct_1688
- Did Hermes emit a final canonical report: yes

## Collected Evidence

- Supplier names collected: `潮州市潮安区彩塘镇轩匠五金制品厂`
- Product pages successfully read: `672143711850` in the narrow preflight probe and `851436523899` in the full run
- Supplier pages successfully read: `https://shop07866986b0436.1688.com/?offerId=851436523899&td_page_id=PC-DEFAULT-2025`

## Blockers Or Limitations

- The authenticated session removed the login blocker, but direct search results stayed too thin or noisy to support a 3-supplier shortlist inside Hermes's 24-turn budget.
- The run depended on an operator-provided authenticated Chrome session; automated login was not validated.
- Hermes still emitted a raw transcript with a banner and session trailer, so the canonical report had to be normalized before saving.

## Notes

- The session stayed logged in throughout the successful preflight probe and the full validation run.
- No login redirect reappeared once the operator-prepared session was in place.
- This pass proves that Hermes can traverse a real authenticated direct `1688.com` workflow far enough to read search, product-detail, and supplier pages and emit a supplier-first partial report.
- This is enough to raise `adapters/hermes/adapter-manifest.json` to `validation_status = validated_partial`, but not enough to justify `validated_direct`.
- Supporting raw artifacts:
  - `reports/hermes-direct-detail-probe-post-login-3-2026-04-16.raw.txt`
  - `reports/hermes-post-login-direct-2026-04-16.raw.txt`
