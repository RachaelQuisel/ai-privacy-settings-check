# Fictional example: a two-product audit

This is invented material to demonstrate the skill. It is not a real person's account,
and the observed states below were not read from anything — they illustrate the output
shape, the confidence labels, and the severity arithmetic.

## Input

> "Audit my ChatGPT and Gemini. I'm on ChatGPT Plus and a personal Google account,
> both in the US. I use ChatGPT for client work. Go ahead and read the live settings."

## Sample output

> **Sensitive — handle as confidential.** This report describes the current security posture
> of the named accounts. Share it only with the account owner and anyone they explicitly
> designate. Do not paste it into a group chat, shared channel, ticket, or AI assistant.

# AI privacy audit — r****@example.com — 2026-10-02

## Scope

- **Products audited:** ChatGPT (Plus, personal), Gemini (personal Google account)
- **Region:** United States
- **Read method:** live read for both; documented baseline used where a page did not render
- **Audit date:** 2026-10-02
- **Baseline last verified:** 2026-10-02 (both vendor files current)
- **Not covered:** mobile OS permissions (manual annex below); no Workspace or Business tenant

## Summary

Four settings are exposing more than intended, and one of them — a public ChatGPT share link
from February that still resolves — is the only finding here that is already irreversible.
The account is otherwise configured better than the out-of-box default: ChatGPT training is
off and Gemini's auto-delete has been shortened. The highest-value remaining change is
disconnecting the Google Drive connector during document-summarization work, because that
combination is what turns an ordinary prompt into an exfiltration path.

## Findings

### 1. A public share link resolves logged-out — ChatGPT — **High** · *verified*

- **Observed:** Settings → Data controls → Shared links lists three links. One, created
  2026-02, opened in a logged-out private window and rendered the full conversation,
  including an uploaded PDF.
- **Exposes:** The entire conversation and its attached file, to anyone holding the URL.
  No account needed, no expiry, and the recipient can forward it.
- **Recommend:** Delete all three links now; audit this page quarterly.
- **Fix:** Settings → Data controls → Shared links → Manage → delete each.
- **Evidence:** vendors/chatgpt.md §4 — https://help.openai.com/en/articles/7925741 — checked 2026-10-02
- **Severity:** S3 (client file) · X3 (open internet) · R3 (already public, may be cached)
  · P1 (the client named in it) · A1 → **11, High.** Overrides 1 and 3 both fire.

### 2. Google Drive connector enabled while summarizing external documents — ChatGPT — **High** · *verified*

- **Observed:** Settings → Plugins shows Google Drive connected with the `drive` (full) scope,
  and the account-wide Default permission reads "Allow low-risk tools."
- **Exposes:** This is the lethal trifecta — private data access (Drive), untrusted content
  (documents from clients), and an outbound channel (live web). The AgentFlayer research
  demonstrated exactly this shape against ChatGPT connectors.
- **Recommend:** Disconnect Drive except during tasks that need it, and set Default
  permission to "Always ask."
- **Fix:** Settings → Plugins → Google Drive → disconnect. Then Plugins → Permissions → Always ask.
- **Evidence:** vendors/chatgpt.md §3; evidence-base.md incident ledger, 2025-08-06 — checked 2026-10-02
- **Severity:** S3 · X3 · R3 · P2 · A3 → **14, High.** Overrides 1, 2, 3 and 5 fire.

### 3. Gemini "Keep Activity" is on — Gemini — **Medium** · *verified*

- **Observed:** myactivity.google.com/product/gemini shows Keep Activity enabled,
  auto-delete already shortened to 3 months.
- **Exposes:** Prompts, responses, uploads and Gemini Live transcripts are used to improve
  Google's services including model training, and a subset is read by human reviewers.
  **Human-reviewed chats are retained up to three years and survive your deletion.**
- **Recommend:** Turn Keep Activity off. The 3-month auto-delete already set is the right
  order of operations — shorten first, then turn off, because turning off is not retroactive.
- **Fix:** https://myactivity.google.com/product/gemini → Keep Activity → off.
- **Evidence:** vendors/gemini.md §1, §5 — https://support.google.com/gemini/answer/13594961 — checked 2026-10-02
- **Severity:** S2 · X1 · R3 · P0 · A2 → **8, Medium.** No override fires. Irreversible, but
  not third-party-exposed — this is the honest rating, not the High that most listicles give it.

### 4. Android Phone/Messages/WhatsApp connectors still attached — Gemini — **High** · *unresolved*

- **Observed:** gemini.google.com/apps did not finish rendering the connector list on two
  attempts. **State not determined.**
- **Exposes:** If attached, these four keep operating **even with Keep Activity off** —
  the one documented bypass of the control recommended in finding 3. Conversations still
  sit in the Google Account for 72 hours.
- **Recommend:** Check manually and disconnect all four.
- **Fix:** https://gemini.google.com/apps → disconnect Device assistance, Phone, Messages, WhatsApp.
- **If unresolved:** The page failed to render; this was not read as "off." Verify on-device.
- **Evidence:** vendors/gemini.md §3 — checked 2026-10-02
- **Severity:** rated on documented behavior, not observed state. High if attached.

## Already configured well

- **ChatGPT "Improve the model for everyone" is off.** This is the non-default state; the
  consumer default is on.
- **Gemini auto-delete set to 3 months**, the shortest available.
- **No reference photo set** in ChatGPT personalization — the biometric-adjacent store is empty.

## Manual annex — mobile and OS permissions

Cannot be read from a desktop. Walk these on each device:

| Check | iOS path | Android path |
|---|---|---|
| ChatGPT contacts access | Settings → ChatGPT → Contacts → off | Apps → ChatGPT → Permissions → Contacts → deny |
| Gemini as default assistant | n/a (Siri is not replaceable) | Apps → Default apps → Digital assistant app → None |
| Gemini lock screen | n/a | Gemini → Settings → Gemini on lock screen → both off |
| Photo access | Selected Photos, not full library | Per-item, not full library |

## Limits

- Finding 4 is **unresolved**, not clean. The page did not render.
- Gemini's `Web & App Activity` default could not be verified against official documentation;
  it governs AI Mode and Search separately from everything above and was **not** audited here.
- No mobile device was available, so the entire annex is unverified.
- ChatGPT ad personalization defaults are **contested** between sources; the live state was
  read as off, but the default it started from is unknown.

## Re-check

90 days, or sooner on any of: a vendor policy-change notice, a plan upgrade, a new connector
grant, a new device, or an app update. Per the dark-pattern catalog, a toggle verified once is
only verified as of that date — `recheck_after` on every finding above is 2026-11-01.
