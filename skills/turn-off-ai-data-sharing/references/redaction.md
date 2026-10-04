# Handling the report

A completed privacy audit is itself sensitive. It enumerates, in one place, which AI products a person uses, which third-party accounts those products can reach, what their workspace is called, and where their configuration is weakest. That is a useful document for the owner and a useful document for an attacker.

Apply these rules before the report leaves your hands.

## Mask by default

Replace these with a stable placeholder, keeping enough shape that the owner can tell entries apart:

| Item | Write instead |
|---|---|
| Account email | `r****@gmail.com` — first character, masked local part, real domain |
| Workspace / org / tenant name | `[workspace A]`, `[tenant B]` |
| Connected third-party account identifiers | the service name only: "Google Drive connector", not the account it points at |
| Document, file, repo, and channel names seen while reading a settings page | omit entirely; they are not findings |
| Device names | `[laptop]`, `[phone]` |
| API access values, tokens, session cookies, or any sign-in detail | never record one, in any form, masked or not |

Keep unmasked: product names, plan tiers, setting labels, toggle states, regions, and dates. Those are the findings. Masking them would make the report useless.

## Header every report

Put this at the top, above the summary:

> **Sensitive — handle as confidential.** This report describes the current security posture of the named accounts. Share it only with the account owner and anyone they explicitly designate. Do not paste it into a group chat, shared channel, ticket, or AI assistant.

That last clause is not a joke. Pasting a privacy audit into a chatbot whose retention settings the audit just criticized is a real and recurring mistake.

## Where it is written

- Default to writing the report **locally**, never to a shared drive, wiki, or channel.
- Do not publish an audit as a web page, artifact, or link unless the owner asks for that specifically and knows the contents.
- If the audit was run for a client, the client owns the report. Send it to them directly and keep your copy only as long as the engagement needs it.
- `reports/` is git-ignored in this repo. Keep it that way. A completed audit must never be committed, and no real account data belongs in this repository — including in examples.

## Screenshots

Screenshots of settings pages are strong evidence and are also the easiest way to leak something. If one is included:

- Crop to the setting in question.
- Check the browser chrome, tab strip, sidebar, and any notification toast for names, emails, and document titles before attaching it.
- When a page cannot be cropped clean, describe the observed state in words instead. A sentence saying what you saw is adequate evidence.
