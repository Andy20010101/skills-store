# Hermes Operator-Assisted Login Workflow

- Purpose: enable a lawful operator-provided 1688 / Taobao login session for Hermes direct-site validation
- Status: executed on April 17, 2026; the direct workflow is now treated as `validated_direct` under `operator_authenticated` mode after a 3-supplier direct shortlist was completed

## Why This Exists

Current Hermes validation established:
- local headless browser automation is real
- direct detail access can be redirected to login
- mirror-page reading works

What is still missing:
- a stable direct-site path that reaches a full 3-supplier shortlist without consuming the whole turn budget inside noisy search pages

Hermes supports attaching browser tools to a live Chrome session via CDP.
That is the right path when login must be performed by a human operator, and it is now the recommended direct-site validation mode for Hermes.

## Preconditions

- a machine with Chrome, Chromium, Edge, or another Chromium browser that exposes Chrome DevTools Protocol
- a human operator who can lawfully log into 1688 / Taobao
- Hermes CLI available on the same machine that will run the validation

## Step 1. Launch Chrome With Remote Debugging

Use a dedicated profile so the debug browser session does not interfere with your normal browser profile.

### Linux

```bash
google-chrome --remote-debugging-port=9222 --user-data-dir="$HOME/.hermes/chrome-debug" --no-first-run --no-default-browser-check
```

### macOS

```bash
open -a "Google Chrome" --args --remote-debugging-port=9222 --user-data-dir="$HOME/.hermes/chrome-debug" --no-first-run --no-default-browser-check
```

### Windows

```powershell
chrome.exe --remote-debugging-port=9222 --user-data-dir="$HOME\\.hermes\\chrome-debug" --no-first-run --no-default-browser-check
```

If you already have a Chrome instance exposing CDP on another endpoint, note that URL.

## Step 2. Manually Log In

In that browser instance:
- open 1688 / Taobao login as needed
- complete all manual login steps yourself
- confirm that a direct `detail.1688.com` product page is visible in the same browser session

Do not hand the credentials to Hermes.
The point is to reuse the authenticated browser state, not to automate login.

## Step 3. Start Hermes And Attach To Live Chrome

Start Hermes interactive CLI and run:

```text
/browser connect
```

If you are using a non-default endpoint, run:

```text
/browser connect http://host:port
```

Then confirm with:

```text
/browser status
```

Expected result:
- Hermes reports `connected to live Chrome via CDP`
- the endpoint is reachable

## Step 4. Run A Narrow Preflight Probe

Use:
- `verification/hermes-direct-detail-probe-2026-04-16.txt`

Expected result:
- confirm that Hermes can still read one direct `detail.1688.com` page in the live authenticated session
- stop early if the session has silently fallen back to login again

## Step 5. Run Search Harvest

Use:
- `verification/hermes-post-login-search-harvest-query.txt`

Save the output as:
- `verification/hermes-post-login-candidate-set-YYYY-MM-DD.json`

Execution rule:
- keep the run bounded
- do not let Hermes expand into open-ended search browsing
- stop after the candidate set is written

## Step 6. Run Evidence Pass

Use:
- `verification/hermes-post-login-evidence-pass-query.txt`

Before running, replace `{{CANDIDATE_SET_PATH}}` in the prompt body with the actual candidate-set path.

Save the output as:
- `verification/hermes-post-login-evidence-notes-YYYY-MM-DD.json`

Execution rule:
- inspect only the harvested candidates
- collect visible facts, judgments, unknowns, and representative-product links
- do not branch back into broad search

## Step 7. Run Report Synthesis

Use:
- `verification/hermes-post-login-report-synthesis-query.txt`

Before running, replace `{{EVIDENCE_NOTES_PATH}}` in the prompt body with the actual evidence-notes path.

Save the output as:
- `reports/hermes-post-login-direct-YYYY-MM-DD.md`

Execution rule:
- synthesize only from the reviewed evidence
- if fewer than three credible suppliers remain, emit a partial report rather than padding the shortlist

## Step 8. Record The Outcome

If the run succeeds, persist:
- `verification/hermes-post-login-candidate-set-YYYY-MM-DD.json`
- `verification/hermes-post-login-evidence-notes-YYYY-MM-DD.json`
- a canonical Markdown report
- a `run-result.json`
- a validation note describing that the run used operator-assisted login through live Chrome CDP

Use these templates:
- `verification/templates/hermes-post-login-validation-note-template.md`
- `verification/templates/hermes-post-login-run-result.success-template.json`
- `verification/templates/hermes-post-login-run-result.partial-template.json`
- `verification/templates/hermes-post-login-run-result.blocked-template.json`

If the run fails, record:
- whether the failure was login expiry, redirect to login, page instability, or supplier-page access failure

The earlier monolithic prompt remains available here:
- `verification/hermes-post-login-direct-validation-query.txt`

Treat it as a regression or comparison prompt only.
For new validations, prefer the phased prompts above.

## Important Boundary

This workflow is for:
- operator-assisted authenticated browsing

It is not for:
- credential sharing with Hermes
- captcha bypass
- hidden-interface fallback
- unattended login automation
