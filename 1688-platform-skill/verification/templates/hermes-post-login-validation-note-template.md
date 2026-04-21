# Hermes Post-Login Direct Validation

- Validation date: YYYY-MM-DD
- Validation environment: Hermes CLI attached to a live Chrome session via CDP
- Prompt file: `verification/hermes-post-login-direct-validation-query.txt`
- Report artifact: `reports/hermes-post-login-direct-YYYY-MM-DD.md`
- Run-result artifact: `verification/hermes-post-login-direct-YYYY-MM-DD.run-result.json`

## Operator Session

- Browser type: Chrome | Chromium | Edge
- CDP endpoint: `http://localhost:9222`
- Login state prepared by operator: yes | no
- Direct product page visibly open before run: yes | no

## Pages Attempted

- direct search page:
- direct product detail page:
- direct supplier page:

## Outcome

- Final status: success | partial | blocked
- Evidence mode: direct_1688 | mirror_assisted | none
- Did Hermes emit a final canonical report: yes | no

## Collected Evidence

- Supplier names collected:
- Product pages successfully read:
- Supplier pages successfully read:

## Blockers Or Limitations

- ...

## Notes

- Record whether the session stayed logged in for the whole run
- Record whether a login redirect reappeared mid-run
- Record whether supplier-page access failed separately from search or product-detail access
