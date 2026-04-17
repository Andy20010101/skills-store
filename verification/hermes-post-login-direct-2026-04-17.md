# Hermes Post-Login Direct Validation

- Validation date: 2026-04-17
- Validation environment: Hermes CLI attached to a live Chrome session via CDP
- Workflow mode: phased operator-assisted validation
- Prompt files:
  - `verification/hermes-direct-detail-probe-2026-04-16.txt`
  - `verification/hermes-post-login-search-harvest-query.txt`
  - `verification/hermes-post-login-evidence-pass-query.txt`
  - `verification/hermes-post-login-report-synthesis-query.txt`
- Report artifact: `reports/hermes-post-login-direct-2026-04-17.md`
- Run-result artifact: `verification/hermes-post-login-direct-2026-04-17.run-result.json`

## Operator Session

- Browser type: Chrome
- CDP endpoint: `http://172.18.144.1:9223`
- Login state prepared by operator: yes
- Direct product page visibly open before run: yes

## Phase Artifacts

- Preflight raw probe: `reports/hermes-direct-detail-probe-post-login-2026-04-17.raw.txt`
- Preflight canonical probe: `reports/hermes-direct-detail-probe-post-login-2026-04-17.md`
- Search-harvest raw transcript: `verification/hermes-post-login-candidate-set-2026-04-17.raw.txt`
- Search-harvest canonical artifact: `verification/hermes-post-login-candidate-set-2026-04-17.json`
- Supplemental search-harvest raw transcript: `verification/hermes-post-login-candidate-set-supplement-2026-04-17.raw.txt`
- Supplemental search-harvest canonical artifact: `verification/hermes-post-login-candidate-set-supplement-2026-04-17.json`
- Merged candidate-set artifact: `verification/hermes-post-login-candidate-set-merged-2026-04-17.json`
- Evidence-pass raw transcript: `verification/hermes-post-login-evidence-notes-2026-04-17.raw.txt`
- Evidence-pass canonical artifact: `verification/hermes-post-login-evidence-notes-2026-04-17.json`
- Supplemental evidence-pass raw transcript: `verification/hermes-post-login-evidence-notes-hongfu-compact-2026-04-17.raw.txt`
- Supplemental evidence-pass canonical artifact: `verification/hermes-post-login-evidence-notes-hongfu-2026-04-17.json`
- Merged evidence-notes artifact: `verification/hermes-post-login-evidence-notes-merged-2026-04-17.json`
- Report-synthesis raw transcript: `reports/hermes-post-login-direct-2026-04-17.raw.txt`
- Supplemental merged report-synthesis raw transcript: `reports/hermes-post-login-direct-2026-04-17-merged.raw.txt`
- Report-synthesis canonical artifact: `reports/hermes-post-login-direct-2026-04-17.md`

## Pages Attempted

- direct search page: `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%BF%9D%E6%B8%A9%E9%A5%AD%E7%9B%92`
- supplemental direct search page: `https://s.1688.com/selloffer/offer_search.htm?keywords=304%20%E4%B8%8D%E9%94%88%E9%92%A2%20%E5%88%86%E6%A0%BC%20%E9%A5%AD%E7%9B%92`
- direct product detail pages:
  - `https://detail.1688.com/offer/672143711850.html`
  - `https://detail.1688.com/offer/908205986518.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=9cf026eabacb4ac1ba0bdbbbf7347e0e&sessionid=22e952944ca91af1bdfc0d05ba3385c4`
  - `https://detail.1688.com/offer/1028813801883.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=02001f4b42ac49e1904647a6b1d37fc1&sessionid=22e952944ca91af1bdfc0d05ba3385c4`
  - `https://detail.1688.com/offer/992411055961.html?offerId=992411055961&sortType=&pageId=&abBizDataType=cbuOffer&hotSaleSkuId=6225815567309&trace_log=normal&uuid=a54ddddc99c94568a9c6f562ce83c61c&forcePC=1776388637674`
- direct supplier pages:
  - `https://chaozhougc.1688.com/`
  - `https://shop87n77471lx561.1688.com/`
  - `https://cahongfu.1688.com/?offerId=992411055961&td_page_id=PC-DEFAULT-2025`

## Outcome

- Final status: success
- Evidence mode: direct_1688
- Did Hermes emit a final canonical report: yes

## Collected Evidence

- Supplier names collected:
  - `潮州市宏富五金制品有限公司`
  - `潮州市潮安区彩塘镇广成不锈钢制品厂`
  - `龙港市萱甄工艺品厂`
- Product pages successfully read:
  - `672143711850` in the preflight probe
  - `908205986518` in the phased evidence pass
  - `1028813801883` in the phased evidence pass
  - `992411055961` in the supplemental single-candidate probe
- Supplier pages successfully read:
  - `https://chaozhougc.1688.com/`
  - `https://shop87n77471lx561.1688.com/`
  - `https://cahongfu.1688.com/?offerId=992411055961&td_page_id=PC-DEFAULT-2025`

## Blockers Or Limitations

- The phase-1 raw transcript still required normalization because Hermes emitted a natural-language summary instead of schema-valid JSON before the turn limit.
- The supplemental search-harvest raw transcript ended before the closing brace and had to be normalized into a canonical candidate-set artifact.
- The supplemental single-candidate probe required a hard-scoped prompt because the generic evidence-pass prompt kept drifting back to previously reviewed suppliers.
- The final merged report raw transcript still required normalization because Hermes emitted duplicated report content.

## Notes

- The session stayed logged in for the whole phased run.
- No login redirect reappeared once the operator-prepared session was in place.
- This 2026-04-17 phased run is stronger than the 2026-04-16 one-shot direct run because it completed the whole search-harvest -> evidence-pass -> report-synthesis chain with reusable intermediate artifacts and a supplemental third-supplier probe.
- Hermes now has a direct 3-supplier shortlist in repo artifacts, but `validation_status` still stays `validated_partial` because the workflow depends on an operator-prepared authenticated browser session rather than a self-sufficient host path.
