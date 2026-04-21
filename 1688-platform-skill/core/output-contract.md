# Output Contract

Use this Markdown shape unless the host requires a different wrapper.

```md
# 1688 Supplier Discovery Report

## Research Brief
- Product direction:
- Search phrases used:
  - <phrase 1>
  - <phrase 2>
- Constraints:
  - <constraint 1>
  - <constraint 2>

## Run Notes
- Evidence mode: direct_1688 | mirror_assisted | none
- Host capability assumptions:
- Access limitations:
- Important caveats:

## Supplier Shortlist

### 1. <Supplier Name>
- Evidence page link:
- Source 1688 link: <required when the inspected page is a mirror or proxy that exposes one>
- Why shortlisted:

#### Page-Visible Facts
- ...

#### Heuristic Judgments
- ...

#### Unknowns
- ...

#### Representative Products
1. <Product title>
   - Evidence link:
   - Source 1688 link: <required when different from the inspected page and visibly exposed>
   - Visible price / MOQ:
   - Notes:

### 2. <Supplier Name>
- ...

## Rejected or Lower-Priority Candidates
- Candidate:
- Why not prioritized:

## Next Actions
- Which suppliers to revisit first
- Which unknowns need manual confirmation
```

## Rules

- Supplier-first ordering is required.
- `Search phrases used`, `Constraints`, and `Next Actions` should prefer one item per line instead of semicolon-packed prose.
- `Evidence page link` must point to the exact page that was actually inspected.
- `Source 1688 link` is required whenever a mirror or proxy page visibly exposes the underlying `1688.com` URL.
- Every supplier needs at least one inspected-page link.
- Every representative product needs its own inspected-page link.
- Every supplier needs one anchor representative product. Add extra representative products only when they have a distinct inspected page or a distinct linkable listing. If repeated variants are only visible as snippets on the same page, summarize them in `Page-Visible Facts` or `Notes` instead of creating duplicate rows.
- Unknowns are mandatory whenever key information is not visible.
- Hosts that emit banners, duplicated completions, or session trailers must strip them before persisting the canonical Markdown report artifact referenced by `run-result.json`.
- If there are fewer than 3 credible suppliers, say so explicitly instead of padding the list.
