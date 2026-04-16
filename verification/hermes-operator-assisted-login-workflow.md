# Hermes Operator-Assisted Login Workflow

- Purpose: enable a lawful operator-provided 1688 / Taobao login session for Hermes direct-site validation
- Status: documented workflow only; not yet executed in this repository's current headless environment

## Why This Exists

Current Hermes validation established:
- local headless browser automation is real
- direct detail access can be redirected to login
- mirror-page reading works

What is still missing:
- a Hermes run that reuses an already-authenticated browser session and then continues direct-site reading

Hermes supports attaching browser tools to a live Chrome session via CDP.
That is the right path when login must be performed by a human operator.

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

## Step 4. Run The Post-Login Validation Prompt

Use:
- `verification/hermes-post-login-direct-validation-query.txt`

The prompt assumes:
- the connected live Chrome session is already logged in
- Hermes should reuse the current authenticated browser context
- Hermes must stop if the session is no longer valid

## Step 5. Record The Outcome

If the run succeeds, persist:
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

## Important Boundary

This workflow is for:
- operator-assisted authenticated browsing

It is not for:
- credential sharing with Hermes
- captcha bypass
- hidden-interface fallback
- unattended login automation
