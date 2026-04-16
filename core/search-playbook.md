# Search Playbook

Use this reference when translating a sourcing brief into a first-pass browsing plan.

## Search Phrase Strategy

Start with 2 to 5 phrases:
- one direct product phrase
- one synonym or alternate wording
- one material or form-factor phrase if relevant
- one buyer-language phrase only if it helps narrow results

Do not explode into dozens of searches in the first pass.

## Search Progression

Recommended order:
1. start with the clearest direct phrase
2. inspect the first result page for category fit
3. branch to one synonym only if the first phrase is noisy or too sparse
4. add a constraint term only when the market is too broad

## Candidate Selection Rule

From result pages, shortlist suppliers that visibly show at least some of:
- repeated relevance to the target item
- enough listing detail to revisit later
- enough variety to suggest real category engagement
- visible commercial clues such as price bands, MOQ, or packaging options

Avoid spending too long on listings that are obviously generic or off-target.

## When To Open Supplier Pages

Open the supplier page when:
- the result page shows several relevant items from the same seller
- the supplier identity appears stable enough to review
- a supplier page may clarify whether the seller is category-focused

Stay on result and product pages only when supplier-page access is blocked or absent.

## When To Stop Expanding Search

Stop broadening when:
- you already have 3 to 8 reviewable suppliers
- further results are repeating low-value candidates
- the operator's core constraints are already represented in the shortlist

If you only have weak candidates:
- say that the market pass was weak
- keep the shortlist small
- recommend the next best keyword adjustment

## Constrained Host Mode

Use this mode when:
- the browser session is operator-authenticated and expensive to reacquire
- the host has a tight turn budget
- search-result pages are noisy enough that open-ended browsing is likely to waste the run

Recommended hard bounds:
1. start with exactly one direct phrase
2. use at most one fallback phrase
3. open at most two product pages per phrase before deciding whether the phrase is viable
4. stop harvesting after five candidate URLs or two credible suppliers, whichever comes first
5. persist a `candidate-set.json` artifact before deeper supplier review

If a search page is visibly thin or noisy:
- say that explicitly in the candidate set
- keep only the highest-signal URLs
- move into evidence review instead of continuing to expand search
