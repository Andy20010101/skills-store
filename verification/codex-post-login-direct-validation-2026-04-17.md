# Codex Operator-Authenticated Direct Validation

- Validation date: 2026-04-17
- Validation environment: Codex + operator-provided authenticated Chrome session
- Goal: determine whether Codex can now justify `validated_direct` under `operator_authenticated` mode

## Live Search-Page Step

The operator first cleared the direct-search slider challenge in the live Chrome session.
Codex then took over the readable direct search page at:

- `https://s.1688.com/selloffer/offer_search.htm?keywords=304%E4%B8%8D%E9%94%88%E9%92%A2%20%E4%BF%9D%E6%B8%A9%E9%A5%AD%E7%9B%92`

Visible search-page evidence in that live page included:
- a readable hongfu product result for `304不锈钢食品级两三格分格饭盒便当盒减脂餐定量密封不串味跨境`
- visible search-page commercial clues: `¥11.8`, `全网5200+件`, `回头率56%`
- visible supplier name: `潮州市宏富五金制品有限公司`

The search-box value itself still rendered as mojibake in the page input field, but the visible result-list text was readable and commercially usable.

## Direct Traversal Completed

In the same operator-authenticated session, Codex then read:

- hongfu direct product page: `https://detail.1688.com/offer/992411055961.html`
- hongfu direct supplier page: `https://cahongfu.1688.com/`

This completed a real direct `search -> product detail -> supplier page` path for a retained candidate in the current host.

Codex then revisited two additional retained direct candidate pairs in the same session:

- guangcheng product + supplier
- xuanzhen product + supplier

Those pages were directly readable and were used to generate the canonical direct report artifact.

## Outcome

- Final status: success
- Evidence mode: direct_1688
- Authentication mode: operator_authenticated
- Did Codex emit a canonical direct report: yes

## Resulting Adapter State

- upgrade `adapters/codex/adapter-manifest.json` to `validation_status = validated_direct`
- set `validated_auth_mode = operator_authenticated`

## Why The Upgrade Is Now Justified

- Codex previously lacked a stable readable direct search step in-browser
- this validation completed from a live readable direct search-results page into a direct product page and a direct supplier page without dropping back to mirror evidence
- the same session also supported direct-page review for three retained suppliers and produced a canonical direct report artifact

## Remaining Boundary

- fresh automated direct-search loads may still re-trigger slider verification
- the supported Codex path is therefore:
  - operator prepares an authenticated Chrome session
  - operator clears the initial direct-search challenge when needed
  - Codex takes over the readable direct results page and continues the workflow

That boundary does not block `validated_direct` under `operator_authenticated` mode, but it does rule out a self-sufficient Codex host path.
