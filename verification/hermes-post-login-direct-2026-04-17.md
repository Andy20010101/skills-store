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
- Evidence-pass raw transcript: `verification/hermes-post-login-evidence-notes-2026-04-17.raw.txt`
- Evidence-pass canonical artifact: `verification/hermes-post-login-evidence-notes-2026-04-17.json`
- Report-synthesis raw transcript: `reports/hermes-post-login-direct-2026-04-17.raw.txt`
- Report-synthesis canonical artifact: `reports/hermes-post-login-direct-2026-04-17.md`

## Pages Attempted

- direct search page: `https://s.1688.com/selloffer/offer_search.htm?keywords=%E4%BF%9D%E6%B8%A9%E9%A5%AD%E7%9B%92`
- direct product detail pages:
  - `https://detail.1688.com/offer/672143711850.html`
  - `https://detail.1688.com/offer/908205986518.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=9cf026eabacb4ac1ba0bdbbbf7347e0e&sessionid=22e952944ca91af1bdfc0d05ba3385c4`
  - `https://detail.1688.com/offer/1028813801883.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=02001f4b42ac49e1904647a6b1d37fc1&sessionid=22e952944ca91af1bdfc0d05ba3385c4`
- direct supplier pages:
  - `https://chaozhougc.1688.com/`
  - `https://shop87n77471lx561.1688.com/`

## Outcome

- Final status: partial
- Evidence mode: direct_1688
- Did Hermes emit a final canonical report: yes

## Collected Evidence

- Supplier names collected:
  - `潮州市潮安区彩塘镇广成不锈钢制品厂`
  - `龙港市萱甄工艺品厂`
- Product pages successfully read:
  - `672143711850` in the preflight probe
  - `908205986518` in the phased evidence pass
  - `1028813801883` in the phased evidence pass
- Supplier pages successfully read:
  - `https://chaozhougc.1688.com/`
  - `https://shop87n77471lx561.1688.com/`

## Blockers Or Limitations

- The phased flow completed end to end, but the bounded phase-1 harvest only surfaced 2 reviewable candidates, so the final shortlist stayed below the usual 3-supplier target.
- The phase-1 raw transcript still required normalization because Hermes emitted a natural-language summary instead of schema-valid JSON before the turn limit.
- The phase-3 raw transcript still required normalization because Hermes emitted duplicated report content and a trailing `session_id`.

## Notes

- The session stayed logged in for the whole phased run.
- No login redirect reappeared once the operator-prepared session was in place.
- This 2026-04-17 phased run is stronger than the 2026-04-16 one-shot direct run because it completed the whole search-harvest -> evidence-pass -> report-synthesis chain with reusable intermediate artifacts.
- Hermes remains `validated_partial`, not `validated_direct`, because the authenticated direct workflow still produced only 2 credible suppliers and still depends on operator-prepared login state.
