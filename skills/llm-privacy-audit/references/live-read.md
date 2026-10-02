# Live read playbook

The documented baseline in `vendors/` says what a setting's default *is*. A live read says what *this account* is set to. The two are different claims and the report must never blur them.

## Before touching a browser

1. **Confirm the person running this is the account owner.** Never request, accept, or use another person's credentials. If the subject is a client, they run the audit on their own machine, or they drive their browser while you read the screen and record what they report.
2. **Confirm they want a live read.** It means opening their logged-in accounts. Some people would rather walk the checklist themselves. That is a complete audit too.
3. **State what you will open** — the list of settings URLs, from the vendor files — before opening the first one.

## Choosing a driver

Use whatever browser automation the host environment already has, in this order:

1. **The user's own logged-in browser, driven by an existing tool** — a browser-automation MCP, a CLI for their browser, or an extension they have already installed. Sessions are already authenticated; nothing new is granted.
2. **The user driving manually while you read.** Slower, works everywhere, zero automation risk. The right choice for a client engagement and the fallback whenever automation misbehaves.

Do not install a browser automation tool, create a new browser profile, or ask for a login in order to complete an audit. If no driver is available, run the documented-baseline audit and say in **Limits** that no account state was observed.

## Reading a settings page

For each setting in the vendor file:

1. Navigate to the deep link recorded in the vendor file. Do not guess a URL by pattern — a guessed settings URL that happens to resolve is how an audit ends up describing the wrong page.
2. Wait for the page to finish rendering. These are login-gated single-page apps; a toggle that has not hydrated yet frequently reads as "off."
3. Locate the control by its **visible label text**, as recorded in the vendor file — not by a CSS selector, class name, or DOM position. Labels survive redesigns; selectors do not.
4. Record the observed state, the label text you matched, and the date.
5. Read the page for settings the vendor file does not list. Vendors add toggles. Anything new goes in the report as a finding and into the vendor file as a new entry.

## When a read fails

These are the expected failure modes. Each has one correct response.

| What happened | Record it as | Never |
|---|---|---|
| Page did not load, or timed out | **unresolved**, with the URL and the error | …assume the default |
| Login expired, hit an SSO wall or MFA prompt | **unresolved** — ask the owner to log in; do not attempt to authenticate | …enter credentials, or ask for them |
| Label from the vendor file is not on the page | **unresolved**, and flag the vendor entry as stale | …match a similar-looking toggle instead |
| Setting is visible but greyed out | **verified**, noting it is admin-locked — this is itself a finding | …report it as the owner's choice |
| Page rendered but the toggle area is blank | **unresolved** — a hydration failure, not an "off" state | …read absence as off |
| A consent or policy-update modal is blocking the page | **unresolved** — report that the owner has a pending consent decision | …dismiss or accept it |

**Never click a toggle, button, or form control that changes state.** Navigate and read. The only clicks permitted are navigation and expanding a disclosure that reveals a setting's current value. If a page requires a destructive or state-changing click to reveal a setting, stop and record it as unresolved.

Avoid triggering JavaScript dialogs. A modal blocks the automation channel and ends the session.

## Admin-locked settings

When the subject is on a Team, Enterprise, or Workspace plan, read the admin plane **before** the member settings. An admin-locked toggle makes the member-level reading irrelevant, and a member-level recommendation the owner cannot act on is a wasted finding. If the subject is the admin, the admin plane is the highest-leverage section in the report.

## Recording evidence

For each observed setting, record: product, setting label as displayed, observed state, URL, timestamp, and `verified`. Screenshots are optional and must follow the cropping rules in [redaction.md](redaction.md).

Do not paste raw page text into the report. Page dumps carry document titles, account names, and notification content that have nothing to do with the finding.
