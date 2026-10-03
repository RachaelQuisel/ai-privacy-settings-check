# Grok (xAI / SpaceXAI)

> **Last verified:** 2026-10-02 · **second gap-fill pass same day** — ten of twelve open defaults resolved; see *Second pass* at the end of this file, including a correction to the connector inventory
> **Surfaces covered:** grok.com + standalone Grok apps · Grok-on-X (a **separate control plane**) · Grok Build CLI · Grok Bot · xAI API

## Method notes — read before trusting a default here

- `x.ai/*` and `help.x.com/*` return **HTTP 403 to all automated fetching** (Cloudflare). Official text from those domains was read via Wayback Machine snapshots.
- Where an **exact UI label** is given, it was extracted from the **live production string bundles** on 2026-10-02: `abs.twimg.com/responsive-web/client-web/i18n/en.236349331ade24e4a.js` (X web client) and `cdn.grok.com/_next/static/chunks/376vlecp-jky0.js` (grok.com settings). These are the strings a user actually sees.
- The corporate entity is now **SpaceXAI LLC** in its own legal pages (Privacy Policy effective 2026-08-24); the X help center still says "xAI"; the iOS listing says developer "X Corp."; Google Play says "SpaceXAI". **Not cosmetic** — it changes which privacy policy governs which surface.
- **Defaults are the weakest part of this record.** Neither xAI nor X publishes default states for most consumer toggles. Every unverified default is marked `reported` or `unresolved`. The only `verified` defaults are in the API and agentic planes, where xAI documents them properly.

## 1. Training on your data

### (a) The grok.com / Grok app account toggle

- **Setting:** `Improve the Model` *(helper text, verbatim: "By allowing your data to be used for training our models, you help enhance your own experience and improve the quality of the model for all users. We take measures to ensure your privacy is protected throughout the process.")*
- **Where:** grok.com → Settings → **Data Controls** → Improve the Model. The settings overlay is driven by a `_s` query param; observed deep-link form is `https://grok.com/?_s=data`. Mobile: Settings → Data Controls → "Improve the model".
- **Default:** **ON outside the EEA/UK · OFF in the EEA/UK · row hidden entirely for enterprise and government tenants.** Resolved in the second pass from shipped client code plus xAI's own EU privacy addendum — a **regional** default, which the first pass missed by treating it as one global value. xAI's Consumer FAQ still never names a default. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.
- **Exposes:** Every prompt, uploaded file, image, document and voice input you send, plus Grok's responses, is retained against your account and used by SpaceXAI to train and fine-tune its models, with a limited number of authorized personnel able to read conversations.
- **Recommend:** **OFF.** The only account-level switch that stops your chat content entering the training corpus. Turning it off is forward-only and does not retract anything already ingested.
- **Risk:** High
- **Evidence:** label/path verified live at `cdn.grok.com/_next/static/chunks/376vlecp-jky0.js` (key `settings-data.improve-model.title`); FAQ at `web.archive.org/web/20260928235916/https://x.ai/legal/faq` — checked 2026-10-02
- **Confidence:** `verified` — label and path from the live string table, regional defaults from shipped code and xAI's EU addendum, corroborated by independent reporting.

- **Setting:** `Private Chat` *(in-chat mode, not a settings toggle. Blurb: "This chat won't appear in your history and will not be used to train models.")*
- **Where:** Ghost-shaped icon at the top right of the grok.com chat screen / Grok app. No settings-page location, no deep link.
- **Default:** **OFF** — a per-conversation mode you must activate each time.
- **Exposes:** Left off, the conversation is stored in your history and is eligible for training.
- **Recommend:** Use it for anything sensitive — the only path that is training-exempt regardless of your account toggle. **Two caveats:** Private Chat is **not available in Build mode**, and the **team-workspace** variant of the blurb reads only "This chat will not appear in your history" — **it drops the no-training promise.**
- **Risk:** Medium
- **Evidence:** blurb verified live in `cdn.grok.com/_next/static/chunks/3uxm6ke72rhac.js` (keys `private-conversation-blurb`, `private-conversation-blurb-team`); Build-mode exclusion at https://docs.x.ai/developers/faq/security — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Feedback (thumbs-up / thumbs-down)
- **Where:** Inline under any Grok response. **No opt-out.**
- **Default:** N/A — user-initiated.
- **Exposes:** xAI states explicitly that **even if you opt out of model training**, voluntarily submitted feedback and the associated conversation may be used for training.
- **Recommend:** Do not rate responses in conversations you care about. There is no setting; abstention is the only control.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** *(no setting)* — unauthenticated use
- **Default:** Content collected and retained on an anonymous basis; **no opt-out available, except in the EU/UK.** xAI verbatim: *"in some regions (excluding the EU/UK), when you use Grok without logging in, you won't have the option to opt out of model training."*
- **Recommend:** **Do not use Grok logged out as a privacy strategy** — outside the EU/UK it is strictly worse than a logged-in account with "Improve the Model" off.
- **Risk:** High
- **Confidence:** `verified`

### (b) The X-side training toggle — the single highest-value item on this page

- **Setting:** `Allow your public data as well as your interactions, inputs, and results with Grok and xAI to be used for training and fine-tuning`
  *(section header `Grok & Third-party Collaborators`; sub-heading `Data Sharing`; description verbatim: "X may share with xAI your X public data as well as your user interactions, inputs and results with Grok on X to train and fine-tune Grok and other AI models developed by xAI.")*

  ⚠️ **The label has drifted.** The 2024 wording was "Allow your **posts** as well as your interactions, inputs, and results **with Grok**…". The live 2026 wording is "**public data** … with Grok **and xAI**" — a broader scope (public posts, post metadata/engagement/reposts, public Spaces, public profile) wearing a similar label. **Do not search for the old string; you will not find it.**
- **Where:** X → Settings and privacy → Privacy & Safety → Data sharing and personalization → Grok & Third-party Collaborators → Data Sharing. Deep link: **`https://x.com/settings/grok_settings`** (route confirmed live and archived continuously since 2024-07-25).
- **Default:** **ON — now `verified`**, on the strength of a **Swiss FDPIC regulator document** plus X's own opt-out framing, corroborated by independent reporting. Enabled retroactively in July 2024 without prior consent.
- **And it does *not* ship OFF for EEA/EU accounts.** This was explicitly open and is now answered: **the 2024 Irish undertaking was a dataset-specific deletion commitment, not a change to the toggle's default.** Same default-on toggle, same regions. The DPC's April 2025 inquiry into *ongoing* EU/EEA training remains open with no decision. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.
- **Exposes:** X hands xAI your public posts, their engagement metadata, public Spaces and public profile, **plus every Grok-on-X prompt, result, voice input and voice transcription**, for training and fine-tuning.
- **Recommend:** **OFF, and do it first** — it is a distinct switch from the grok.com toggle and turning off one does nothing to the other. Note the residual: X states the opt-out *"does not prevent a deployed model from learning as a result of its normal use"* when you use Grok-powered X features such as recommendations.
- **Risk:** High
- **Evidence:** label verified live at `abs.twimg.com/.../en.236349331ade24e4a.js` (string ids `i586f3e0`, `ff4b3818`, `a8d516a4`); path verified at `web.archive.org/web/20260902121507/https://help.x.com/en/using-x/about-grok`; default-ON reported at https://www.bleepingcomputer.com/news/security/x-begins-training-grok-ai-with-your-posts-heres-how-to-disable/ — checked 2026-10-02
- **Confidence:** label `verified`; path `verified`; default `reported`

- **Setting:** `Protect your posts`
- **Where:** X → Settings and privacy → Privacy & Safety → **Audience and tagging** → Protect your posts
- **Default:** **OFF** (public account) for standard accounts.
- **Exposes:** While public, your posts remain available to Grok for training and for surfacing in answers to other users' queries, **independently of the Grok toggle.**
- **Recommend:** ON if you want posts out of the training corpus belt-and-braces — X explicitly names this as a second, stronger lever than the Grok opt-out.
- **Risk:** Medium
- **Confidence:** path/effect `verified`; default `reported`

### Regional differences (EU / UK / EEA / Switzerland)

- **The EU is still opt-out, not opt-in.** SpaceXAI's Europe Privacy Policy Addendum (effective 2026-08-24) lists "To train and improve our models" under **legitimate interests**, processing *"Publicly available data, User Content, X Public posts for over 18 year olds and Feedback Data"*, and tells Europeans: *"you can object to our use of your information to train our models in your settings."* **Consent is not the legal basis**, so the toggle is still something you must go switch off.
- **X gave the Irish DPC a permanent undertaking.** On 2024-08-08 X agreed to suspend processing EU/EEA users' public-post personal data for Grok training; proceedings were struck out 2024-09-04 *"on the basis of X's agreement to continue to adhere to the terms of the undertaking on a permanent basis."*
- **…and the DPC then opened a statutory inquiry anyway.** On 2025-04-11 the DPC commenced an inquiry into **X Internet Unlimited Company (XIUC)** over *"the processing of personal data comprised in publicly-accessible posts … for the purposes of training generative artificial intelligence models, in particular the Grok Large Language Models,"* examining *"the lawfulness and transparency of the processing."* Open as far as could be confirmed.
- **A second, separate DPC inquiry opened 2026-02-17** into XIUC over *"the apparent creation, and publication on the X platform, of potentially harmful, non-consensual intimate and/or sexualised images"* via Grok on X.
- **Unresolved:** whether the X-side training toggle currently *ships* OFF for EU/EEA accounts. No official statement either way, and the X help center documents no regional variation. **Do not assume the undertaking means your EU account's toggle is off — check it.**
- **Evidence:** https://dataprotection.ie/en/news-media/press-releases/data-protection-commission-welcomes-conclusion-proceedings-relating-xs-ai-tool-grok ; https://dataprotection.ie/en/news-media/latest-news/data-protection-commission-announces-commencement-inquiry-x-internet-unlimited-company-xiuc ; https://dataprotection.ie/en/news-media/press-releases/data-protection-commission-opens-investigation-x-xiuc — checked 2026-10-02
- **Confidence:** `verified` except the EU toggle default, which is `unresolved`

## 2. Memory, history & personalization

- **Setting:** `Personalize Grok with your conversation history` *("Allow Grok to remember details from your previous conversations. Private chats are never stored.")*
- **Where:** grok.com → Settings → Data Controls
- **Default:** **Unresolved.** The live config exposes `enable_memory_toggle: true` (feature present) but not the per-user default.
- **Exposes:** Grok derives and stores a persistent profile of you from past chats and injects it into future ones, so a detail disclosed once resurfaces in unrelated conversations.
- **Recommend:** OFF unless you specifically want cross-chat continuity — persistent memory converts a one-off disclosure into a standing record.
- **Risk:** Medium
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Memory from your chats` → `View` / `Delete memory` *(subtitle: "This summary is regenerated periodically from your conversations."; delete dialog: "This will permanently delete all of your saved memory. This action cannot be undone.")*
- **Where:** grok.com → Settings → Data Controls → Memory from your chats. Also `Make a correction`, `Edit`, `Update with Grok`.
- **Exposes:** Nothing extra; this is where you see what Grok has concluded about you.
- **Recommend:** **Read it once before deciding on the memory toggle.** Most people have never looked, and the contents are the honest answer to "what does Grok know about me."
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Personalize Grok using 𝕏` *("Allow your 𝕏 data to be used for personalizing and enhancing your Grok experience. This data includes: 𝕏 user profile, 𝕏 account information and location, 𝕏 settings, 𝕏 preferences, posts viewable on your 𝕏 account.")*
- **Where:** grok.com → Settings → Data Controls
- **Default:** **Unresolved**
- **Exposes:** Pulls your X profile, account info **and location**, X settings/preferences and the posts visible to your X account into grok.com to shape responses.
- **Recommend:** OFF. **Note the scope creep in the small print** — "𝕏 account information and location" is broader than the setting name suggests.
- **Risk:** Medium
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Personalize Grok with your device location` *("Allow Grok to include your browser location in requests when available.")*
- **Default:** **Unresolved.** The Privacy Policy says consent is obtained before collecting *precise* location, implying off-by-default, but does not say so about this toggle.
- **Recommend:** OFF; combined with retained chat history it builds a movement record.
- **Risk:** Medium
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Import memory from other AI providers` *("Bring relevant context and data from another AI provider to Grok.")*
- **Default:** OFF (explicit user action required).
- **Exposes:** Moves your ChatGPT/Claude/Gemini profile into Grok's memory, where it becomes subject to Grok's retention and (unless opted out) training.
- **Recommend:** **Avoid.** It launders another vendor's accumulated profile of you into a vendor with weaker published defaults.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Allow Grok to remember your conversation history` **(X side)**
- **Where:** `https://x.com/settings/grok_settings`
- **Default:** **Unresolved**
- **Recommend:** OFF — a separate switch from the grok.com memory toggle.
- **Risk:** Medium
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Allow X to personalize your experience with Grok` **(X side)**
- **Where:** X → Privacy & Safety → Data sharing and personalization → Grok & Third-party Collaborators → Grok Personalization
- **Default:** **Unresolved**
- **Exposes:** X shares your profile, public posts, top posts, engagement, inferred interests **and voice-input transcriptions/translations** with xAI to personalize Grok.
- **Recommend:** OFF — **a second X→xAI data pipe that survives turning the training toggle off.**
- **Risk:** High
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Customize Grok's Response` / `What would you like Grok to know about you?`
- **Where:** grok.com → Settings → Personality / Customize; on X, "Customize Grok"
- **Default:** Empty.
- **Exposes:** Whatever you type becomes a standing instruction attached to your account — and is User Content for training purposes like anything else.
- **Recommend:** Keep it free of real identifiers. People routinely put employer, role, location and family details here and forget it is retained.
- **Risk:** Medium
- **Confidence:** `verified`

## 3. Connectors & OAuth scopes

⚠️ **Corrected in the second pass.** An earlier reading of this file listed Slack, Notion, Power BI and X Ads as built-in connectors, inferred from i18n strings shipped in the client. **That over-reads the strings.** `docs.x.ai/grok/connectors` lists exactly **seven built-ins**: Gmail & Google Calendar · Google Drive · OneDrive · Outlook Mail & Calendar · Microsoft Teams · SharePoint · Salesforce. Slack and Notion strings do ship in the client, but those services sit in the **connector catalog** — third-party-hosted MCP servers xAI surfaces but does not build or maintain. One catalog maintainer reports Slack is absent from both the picker and the docs table altogether. **Treat Slack and Notion as catalog-or-absent, not as built-ins.** `verified` for the seven-item built-in list.

- **Setting:** Connector consent screen — `Access your files` / `Access your messages` / `Search your emails` / `Search your calendar` / `Access your pages` / `Manage your X ads`, with `We never train on your data`
- **Where:** grok.com → attach/connectors menu → pick a service → OAuth consent. Team: Settings → Team settings → Connectors.
- **Default:** **No connectors enabled** out of the box; each requires an explicit OAuth grant.
- **Exposes:** Per-connector retention promises are explicit and **narrow**: *"We don't store your emails. Grok searches Gmail in real-time when you ask questions"* (same pattern for Outlook, Google Calendar, Outlook Calendar, Power BI). **Notably, Google Drive, OneDrive, SharePoint, Slack and Notion carry no such "we don't store" promise**, and there is a separate `Google Drive (sync)` connector described as *"track and **sync** your Google Drive files"* — ingestion, not live search.
- **Recommend:** Connect nothing you would not paste. **Prefer the real-time-search connectors over the sync/file ones; never connect Drive-sync to an account holding client data.**
- **Risk:** High
- **Evidence:** `cdn.grok.com/_next/static/chunks/376vlecp-jky0.js` (`syncing-connector.*`) — checked 2026-10-02
- **Confidence:** labels and retention text `verified`; defaults `verified` (no connector exists until granted)

- **Setting:** Google OAuth training carve-out *(policy, not a toggle)*
- **Where:** SpaceXAI Privacy Policy §2, "Google Apps Using Google OAuth"
- **Default:** Verbatim: *"For users who opt to connect to Google Apps via Google OAuth, SpaceXAI shall not use any Google Apps content for any of its internal AI or other training purposes (such as training its machine learning models), including developing new products or services based on such content."* A genuine, contractual no-training commitment — **and it is Google-specific**; no equivalent clause exists for Microsoft, Slack or Notion content.
- **Recommend:** If you must connect a document store, Google's is the one with a written training exclusion.
- **Risk:** Low (for Google) / Medium (asymmetry for the others)
- **Confidence:** `verified`

- **Setting:** X → Grok account linking consent — *"By clicking the 'Authorize app' button, you are authorizing xAI to access your data from X, including: Your conversation history for Grok on X."*
- **Default:** Not linked.
- **Exposes:** Signing into Grok with X directs X to send xAI your X public profile and image, username, numeric X ID, date of birth, X Premium status, **and your Grok-on-X conversation history** — merging the two previously separate planes into one profile.
- **Recommend:** **Keep the planes separate.** Sign into grok.com with email rather than X if you want the X-side and app-side histories to stay unjoined.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Connected apps` *(X side, reverse direction)*
- **Where:** X → Settings and privacy → Security and account access → Connected apps
- **Recommend:** Audit and revoke anything stale; this is where you cut a Grok↔X link you no longer want.
- **Risk:** Medium
- **Confidence:** label `verified`; exact deep-link path `reported`

- **Setting:** Granular OAuth scope strings
- **Default:** **Resolved in the second pass.** The earlier conclusion — that scopes are server-side and undocumented — was wrong about the *documentation*, though right about the client bundle: the scopes are not in the JS, but **`docs.x.ai/grok/connectors/*` publishes a per-connector scope table** for all seven built-ins. Full tables are in the second-pass section.
- **Exposes:** The headline findings: **connecting Outlook, OneDrive or Teams hands Grok write/send authority in a single click with no read-only option** · enabling Drive writes grants the **full `drive` scope**, not a scoped one · SharePoint's *recommended* mode is tenant-wide read **plus a background index that keeps its own separate grant** under a second Entra app registration.
- **Recommend:** Read the provider's own consent screen — and know that **xAI's own opt-in scope picker exists in the shipped code but is flagged off in production**, so the provider's screen is currently the only place a user sees what they are granting.
- **Risk:** High
- **Confidence:** `verified` for all seven built-in scope tables, for the Microsoft-only scope-consent gate, and for the picker being disabled in production. `unresolved` for **catalog** connectors (GitHub, Notion, Linear, Box, …) — by construction, since their scopes are defined by each provider's own MCP endpoint, not by xAI. That is N provider-side lists, not one missing xAI list. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.

## 4. Sharing & publication defaults

### The 2025 indexing incident, and the current state

xAI's Consumer FAQ carries this warning verbatim: *"Any share link you generate will be accessible to anyone you choose to share the link with. For example, if you share the link publicly on a social media platform, it may be subject to indexing by a search engine (e.g., Google) just like any other publicly shared content."* That language is the residue of the August 2025 episode in which large numbers of shared Grok conversations became reachable through Google.

**What is verifiable today is better news than the FAQ implies:**

- `https://grok.com/robots.txt` (fetched live) contains `Disallow: /share-links`, `Disallow: /c/`, `Disallow: /chat/`, `Disallow: /project/*`, plus a blanket `Disallow: /` for `GPTBot`, `ChatGPT-User`, `PerplexityBot`, `ClaudeBot`, `Google-Extended` and `Applebot-Extended`.
- More decisively, a live fetch of a `/share/*` URL returns `<meta name="robots" content="noindex, nofollow, noarchive, nosnippet, noimageindex"/>`. Checked against `/`, `/chat`, `/c/<id>`, `/share-links` and `/project` — **none of them carry that meta tag. It is served specifically on share pages.** A deliberate post-incident remediation, in place now.

**Caveat not to paper over:** `/share/` has no `robots.txt` rule of its own (it falls under the top-level `Allow: /`), so **the protection rests entirely on the page-level `noindex`** — and the FAQ's own warning text has not been updated to reflect the fix. The commonly cited ~370,000-conversation figure could not be confirmed in this pass and is **not asserted here.**

- **Setting:** `Share` *(per-conversation)* → creates a public share link
- **Default:** No link exists until you create one. Once created, the link is **unlisted-but-public**: grok.com's own management page states verbatim *"Shared links can be viewed by anyone with the link."*
- **Exposes:** The full conversation transcript to anyone who obtains the URL — no account needed, no expiry.
- **Recommend:** Treat a share link as publication. Revoke after use. **The `noindex` stops search engines, not forwarding, scraping, or anyone the link reaches.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Allow chat link sharing` *("Allow sharing chats using only your chat link.")*
- **Where:** grok.com → Settings → Data Controls
- **Default:** **ON — resolved in the second pass, and it is the dangerous answer.** Confirmed from shipped client code in two independent places, with a third-party screenshot corroborating. **On in all regions, including the EEA/UK and enterprise** — unlike the training and personalization toggles, this one has no regional carve-out. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.
- **Exposes:** If on, a chat becomes viewable from its link without the explicit per-conversation share step.
- **Recommend:** OFF. Keep sharing an explicit, per-conversation act.
- **Risk:** High
- **Confidence:** `verified` — label from the shipped string table, default from shipped code (two places) plus a corroborating screenshot.

- **Setting:** `See Shared Links` → `Manage` *(page title `Shared Conversations`; per-row `Remove`)*
- **Where:** grok.com → Settings → Data Controls → See Shared Links, or directly **`https://grok.com/share-links`** (fetched live, HTTP 200 — the URL in xAI's FAQ is correct)
- **Recommend:** **Visit it now.** Anyone who has used Grok since 2025 likely has forgotten live links here.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Watermark Imagine generations` / `Share to X`
- **Default:** **Unresolved** for the watermark toggle; `enable_share_to_x_button: true` live.
- **Recommend:** Leave the watermark on — it is provenance, not a privacy cost.
- **Risk:** Low
- **Confidence:** label `verified`; default `unresolved`

- **Setting:** `Block modifications by Grok` *("Prevent Grok from modifying this content"; related: "Images from this post are not editable by Grok")*
- **Where:** X, per-post. **Exact click path unresolved** — the string is live in X's bundle but whether it sits in the composer, post settings, or an account-level preference could not be confirmed without an authenticated session.
- **Default:** **Unresolved**
- **Exposes:** Left unset, other users can have Grok edit/remix images in your posts.
- **Recommend:** **Worth finding and enabling if you post original imagery** — the only lever found against third-party Grok remixing of your media, and directly relevant to the subject of the DPC's February 2026 inquiry.
- **Risk:** Medium
- **Confidence:** label `verified`; location and default `unresolved`

## 5. Retention & deletion

- **Setting:** `Delete All Conversations`
- **Default:** Conversations retained indefinitely — xAI: *"You can keep your data on your SpaceXAI account for as long as you wish."*
- **Recommend:** Periodic purge. **Note the 30-day tail:** deleted conversations and Private Chats *"will be deleted from SpaceXAI systems within 30 days unless it is necessary that they be kept longer for legal, compliance, or safety purposes,"* and anything already de-identified or pseudonymized is **exempt from deletion.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `See Deleted Conversations` → `Manage` *("View and restore conversations that you have deleted. Deleted conversations are permanently removed after 30 days.")*
- **Default:** A 30-day recycle bin exists; deleted chats remain restorable — and therefore present — for 30 days.
- **Exposes:** **"Delete" is a soft delete for 30 days.** If you deleted something to get it off xAI's systems, it is still there.
- **Recommend:** Understand this before relying on deletion for anything time-sensitive. There is no documented immediate-purge option.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Delete Account` *("Permanently delete your account and associated data from the xAI platform. **Deletions are immediate and cannot be undone.**")*
- **Exposes:** ⚠️ **Documented contradiction.** The in-product string says deletion is "immediate"; the Consumer FAQ says *"After you indicate that you want your data deleted, it will take up to 30 days to delete from SpaceXAI systems,"* and the Privacy Policy says account deletion data is removed *"within 30 days."* **Assume 30 days, not immediate.**
- **Recommend:** Export first, then delete. Do not rely on the "immediate" claim.
- **Risk:** Medium
- **Confidence:** `verified` (both strings read directly; the conflict is real)

- **Setting:** `Export Account Data` *("You can download all data associated with your account below. This data includes everything stored in all xAI products.")*
- **Recommend:** Run it once to see the true extent of what is held, before deciding what to delete.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `See Files and Assets` → `Manage`
- **Default:** Uploads retained indefinitely, **independent of conversation deletion.**
- **Exposes:** Documents and images you uploaded persist as separate objects; purging conversations does not obviously purge these.
- **Recommend:** Clear this separately. **The most commonly missed residue.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Delete All Imagine Data` / `Delete All Imagine Posts`
- **Default:** Retained. A separate store with its own delete controls.
- **Recommend:** Purge alongside conversations; "Delete All Conversations" does **not** cover it.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Delete conversation history` **(X side)**
- **Where:** X → Privacy & Safety → Data sharing and personalization → Grok → Delete Conversation History
- **Default:** Retained. X states deleted conversations *"are removed from our systems within 30 days, unless we have to keep them for security or legal reasons."*
- **Recommend:** **Delete on both planes.** Clearing one leaves the other intact.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Privacy portal / DSAR
- **Where:** `https://x.ai/privacy-portal/`. On X: "Privacy Policy Inquiries" form via the help center.
- **Recommend:** The route for correction/objection/erasure requests beyond what the UI offers. EU/UK users: the Addendum confirms you can **object** to model training as a GDPR right, not merely toggle it.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Cookie Settings` → `Manage`
- **Default:** **Unresolved**; regionally gated by OneTrust (`cdn.cookielaw.org` loads on the home page). Per the Privacy Policy, cookie data is used in part to *"Deliver relevant content and targeted advertising."*
- **Recommend:** Reject non-essential.
- **Risk:** Low
- **Confidence:** label `verified`; default `unresolved`

## 6. Voice, audio & camera

- **Setting:** `Enter voice mode` / `Voice settings` / `Microphone`
- **Default:** Voice mode available (`enable_voice_mode: true` live); microphone requires a browser/OS permission grant.
- **Exposes:** Audio and voice are classified as **User Content** in the Privacy Policy (*"files, images, audio, voice, video"*) — they fall under the same training and retention regime as text. **There is no separate voice training toggle;** "Improve the Model" is the only control. On X it is worse: X's help center states your *"voice inputs, transcriptions or translations may be shared with xAI,"* and the training opt-out text explicitly names *"voice inputs and transcriptions and translations of the voice inputs."*
- **Recommend:** Assume voice is transcribed, retained and (absent opt-out) trained on. Use Private Chat for voice, or don't use voice for anything sensitive.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Activate screen share` → `Entire screen` / `Browser tab`
- **Where:** Inside grok.com voice mode
- **Default:** OFF — requires an explicit browser screen-capture grant per session.
- **Exposes:** When active, Grok receives a live video feed of your entire screen or a chosen tab, including anything incidentally on it — other apps, notifications, client data.
- **Recommend:** Prefer `Browser tab` over `Entire screen`, and never while credentials, client systems or other customers' data are visible. **The highest-bandwidth exposure on the consumer surface.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Call transcript` / `Voice Chat` history
- **Default:** Transcripts retained with the conversation. A recording player exists in the codebase but is gated off (`voice_chat_view_recording_player: false`).
- **Recommend:** Delete voice conversations explicitly; note "Voice call rating" feedback is a training channel that **survives the training opt-out.**
- **Risk:** Medium
- **Confidence:** strings and flags `verified`; retention duration for audio specifically `unresolved`

- **Setting:** `Custom Voice` / voice cloning *("Voice cloning is available on the Grok mobile app")*
- **Default:** No custom voice exists until created.
- **Exposes:** Creating one means supplying voice samples — **biometric-adjacent data.** The Privacy Policy says xAI does *"not aim to collect sensitive personal information (ex. … biometric scans)"* and asks you not to provide it — **a request, not a control.**
- **Recommend:** Do not clone your own or anyone else's voice here. **There is no documented retention or deletion path specific to voice models.**
- **Risk:** High
- **Confidence:** feature `verified`; retention/deletion `unresolved`

- **Setting:** Camera / live vision in voice mode
- **Default:** The live grok.com config shows **`voice_mode_camera_rollout: false`** — camera-in-voice-mode is flagged off for web at time of check. Where enabled, images are User Content; the Privacy Policy adds one narrow assurance: *"nor is any uploaded image used for identification purposes."*
- **Recommend:** Deny camera at the OS level unless actively needed (§10).
- **Risk:** Medium
- **Confidence:** web flag `verified`; mobile camera feature name, path and default `unresolved`

## 7. Agentic / computer-use permissions

Two distinct agentic products: **Grok Build** (a CLI coding agent) and **Grok Bot** (an agent with a cloud computer, plus optional access to your local machine). Both are documented with **real, verified defaults** — the best-documented plane in the product.

- **Setting:** Permission mode — `Ask` / `Auto` / `Always-approve`
- **Where:** Grok Build CLI. `/auto`, `/always-approve`, `Ctrl+O`, `Shift+Tab` (cycles Normal → Plan → Auto → Always-approve), or `grok --always-approve`. Config: `[ui] permission_mode` in `~/.grok/config.toml`.
- **Default:** **`Ask`** — *"Prompt for anything not already allowed."* Stated as the default in xAI's own table.
- **Exposes:** Under `Always-approve`, tool calls auto-execute (deny rules and PreToolUse hooks still apply); under `Auto`, a classifier auto-approves "safe" tools.
- **Recommend:** Stay on `Ask`. Add explicit deny rules (`{ action = "deny", tool = "bash", pattern = "rm -rf *" }`) — *"`deny` always wins over `allow`."* Note a remembered "always allow" grant still prompts for dangerous patterns like `rm` and `git push`, **but an explicit config allow-rule silences even those.**
- **Risk:** High
- **Evidence:** https://docs.x.ai/build/features/permissions — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Execution on Local Computer` — `Ask every time` / `Always allow` / `Never allow`
- **Where:** Settings → General → Bot → Execution on Local Computer. Once your account has registered computers the control moves to Settings → Computer → Computers, with a per-machine `Execution on this computer`.
- **Default:** **`Ask every time`** — stated explicitly.
- **Exposes:** At `Always allow`, **any Bot** can run commands on your actual Mac/Windows machine and its files. First prompt reads *"Allow Grok Bot and all Bots to run commands on your local computer?"* — and `Always allow`/`Never` set the policy for **every** Bot, not just the one asking.
- **Recommend:** **`Never allow`.** xAI's own documentation says so: *"Use Never allow unless a Bot has a specific reason to work on your local files."* It does not restrict the cloud computer.
- **Risk:** High
- **Evidence:** https://docs.x.ai/grok-bot/approvals-security-and-privacy (page last updated 2026-09-28) — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Auto-review` rules — `Ask first` / `Allow automatically`
- **Default:** Rule table empty; `Ask first` wins when both kinds of rule match. Team admins can enforce locked team rules you cannot edit or weaken — your own rules *"can only make behavior stricter."*
- **Recommend:** Write narrow `Ask first` rules around consequential actions. xAI's own guidance: avoid broad rules like "allow everything in the browser," and treat Auto Review as a complement to least privilege, **not a replacement.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Shared cloud computer (`Computer`, `Take control`, `Teach a task`)
- **Default:** **One cloud computer per user account, shared across all your Bots.**
- **Exposes:** xAI is blunt: *"Files, browser sessions, and command line credentials on that computer are available across your Bot roster. **Do not use separate Bots as a security boundary.**"* Also: *"Deleting a Bot does not remove shared-computer files or browser sessions."* `Teach a task` records your screen activity.
- **Recommend:** Sign out of services on the shared computer when done, remove sensitive files from `/workspace`, and never log a client system into a Bot computer you also use for anything else. **Enter passwords, 2FA codes, CAPTCHAs and payment confirmations yourself via `Take control` — never in chat.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Use hardware security keys`
- **Default:** **ON** on macOS and Windows; not supported on Linux. Every use still prompts for approval.
- **Exposes:** The Bot's browser can use a security key physically plugged into your desktop.
- **Recommend:** Acceptable given the per-use prompt, but **know it is on by default on your Mac.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Sharing a Bot
- **Default:** Not shared. xAI: *"A public share link lets others copy the Bot's configuration. It does not share your computer or logins. Still, do not put secrets, customer data, or internal URLs in a Bot you share."*
- **Recommend:** Keep credentials, client names and internal hostnames out of Bot instructions entirely.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Grok Bot account/data plane
- **Exposes:** ⚠️ xAI's own Grok Bot doc states *"**Grok Bot uses Cursor authentication and account data settings**,"* that it *"requires data storage and does not support Legacy Privacy Mode,"* and that *"Training opt-out follows the applicable Cursor account and privacy settings."* **So Grok Bot's training opt-out is not governed by your grok.com "Improve the Model" toggle.**
- **Recommend:** If you use Grok Bot, set the opt-out in the Cursor account settings it actually reads. Note Grok Bot **cannot run in a no-storage mode at all.**
- **Risk:** High
- **Confidence:** `verified` that the doc says this; the underlying xAI/Cursor relationship is `unresolved`

## 8. Admin / workspace plane

- **Setting:** `Product sharing` — scopes `Private` / `Team` / `Organization` / `Public`, per resource (`Conversations`, `Projects`, `Skills`)
- **Where:** grok.com → Settings → Team settings → **Organization Sharing & Retention**. Team rows show *"Limited by organization policy."* when the org ceiling is stricter.
- **Default:** **Unresolved** — could not be determined without an admin account.
- **Exposes:** If the ceiling is left at `Public`, members can mint anyone-with-the-link share URLs for team conversations and projects.
- **Recommend:** **Cap `Conversations` at `Team` or `Organization`.** The single most valuable admin control, because it removes the ability of any member to publish a conversation.
- **Risk:** High
- **Confidence:** labels and scope values `verified`; default `unresolved`

- **Setting:** `Conversation retention` → `Custom period` / `Retain indefinitely`
- **Where:** Settings → Team settings → Organization Sharing & Retention. Org level *"overrides retention for all teams."*
- **Default:** **Unresolved.** `Retain indefinitely` is an available option; whether it is the shipped state is unconfirmed.
- **Recommend:** Set a finite period matching your client data-handling commitments, **and set it at the org level** so it overrides per-team settings.
- **Risk:** Medium
- **Confidence:** labels `verified`; default `unresolved`

- **Setting:** `Migrate Personal Content` *("Move your personal conversations, projects, files, tasks, and share links into this team workspace. This is a one-time, one-way operation." / "This action cannot be undone." / "Your share links keep working but follow this team's sharing settings from now on.")*
- **Default:** Not migrated.
- **Exposes:** **Irreversibly** moves your personal chat history — including anything personal — into an employer-visible team workspace governed by team retention and sharing policy.
- **Recommend:** **Do not run this on a personal account.** One-way, undoable, and it transfers your whole history.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** No training on business/enterprise data *(policy)*
- **Default:** Excluded by default: *"No, we do not use your business data, including inputs (prompts) or outputs (answers), for training our models."* **One carve-out, in xAI's words:** *"In some instances we may offer free credits in exchange for you agreeing to permit us to train on your business data."*
- **Recommend:** **Make sure nobody in your org accepts a credits-for-training offer.** Get the DPA in place (`x.ai/legal/data-processing-addendum`); a BAA is available for HIPAA via questionnaire.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** Team settings surface — `Overview`, `Usage`, `Analytics`, `Connectors`, `Marketplaces`, `Advanced`
- **Default:** **Unresolved**
- **Exposes:** `Connectors` is where an admin authorizes org-wide connectors; `Analytics` includes conversation-topic reporting (`enterprise_usage_conversation_topics_pie_chart_enabled: true` live) — **admins get aggregate visibility into what members ask about.**
- **Recommend:** Tell staff that team-workspace conversations are subject to admin analytics. Also note **the team-variant Private Chat blurb drops the no-training promise** (§1).
- **Risk:** Medium
- **Confidence:** tab names and flags `verified`; per-setting defaults `unresolved`

- **Setting:** Grok Bot org controls
- **Default:** **Unresolved.** Per xAI: *"Organization administrators can restrict local-computer execution and may provide managed setup for the cloud computer,"* and a team admin can cap the setting for the whole team; when the team's policy is stricter than yours, the team's applies.
- **Recommend:** **Cap `Execution on Local Computer` org-wide at `Never allow`.**
- **Risk:** High
- **Confidence:** capability `verified`; default `unresolved`

## 9. API / developer plane

- **Setting:** API training *(policy)*
- **Default:** **No training on API traffic.** Verbatim: *"SpaceXAI never trains on your API inputs or outputs without your explicit permission."*
- **Recommend:** **The cleanest plane in the product.** For sensitive work, prefer the API over consumer Grok.
- **Risk:** Low
- **Evidence:** https://docs.x.ai/developers/faq/security — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Default 30-day audit retention
- **Default:** **ON (30 days).** Verbatim: *"By default, all API requests and responses are stored on our servers (encrypted at rest) for 30 days for auditing purposes in the event of suspected abuse or misuse. SpaceXAI does not train on this data, and it is automatically deleted after 30 days."*
- **Recommend:** Fine for most work. If a client contract forbids third-party retention of their data, you need ZDR.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Zero Data Retention (ZDR)` → `Enable` / `Disable`
- **Where:** xAI Console → Team Settings → the Zero Data Retention row → Enable. Requires team-admin rights; you must first delete existing Files and Collections.
- **Default:** **OFF.** xAI **actively discourages it**: *"For most customers, we do not recommend enabling ZDR… For most teams, the default 30-day retention is the better choice."*
- **Exposes:** With it on, prompts and outputs are *"never persisted to disk"* — but it **disables** the stateful Responses API (`store_messages`, `previous_response_id`), Files, Collections, the Batch API, deferred completions, per-key request logging, and server-hosted image/video outputs.
- **Recommend:** Enable **only** if a compliance obligation demands it, and architect around the losses first. Verify via the `x-zero-data-retention: true` response header, the `Active` badge on the Team Settings row, and the ZDR badge in the Console team picker.
- **Risk:** Low *(enabling reduces risk; the trap is silent feature loss)*
- **Confidence:** `verified`

- **Setting:** Regional endpoint
- **Where:** Use `https://us.api.x.ai/v1` instead of `https://api.x.ai`
- **Default:** The default endpoint **does not guarantee a processing region.** By default, request handling, inference, moderation and retained request data may be processed outside the US. The US endpoint currently serves only `grok-4.7` and `grok-4.6`, has no image/video/voice APIs, costs 10% more, and explicitly does **not** cover Files, Collections or server-side tools.
- **Recommend:** Use the regional endpoint if you have data-residency commitments — **and read the exclusions, because they are broad.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Grok Build CLI — `/privacy`, `/settings`
- **Default:** On first use you are shown *"a screen to allow us to retain data to improve the product and model."* **The shipped state of that prompt is unresolved** — xAI says only that *"We will also provide a setting to change your choice."*
- **Exposes:** Without ZDR, code and trace data may be retained; with ZDR enabled, *"no trace or code data is retained."*
- **Recommend:** **Run `/privacy` immediately after install** and disable code data retention — xAI confirms you can do this *"even if ZDR is not enabled."* Do not rely on the first-run screen having defaulted your way.
- **Risk:** High
- **Confidence:** commands and behavior `verified`; first-run default `unresolved`

- **Setting:** Enterprise API retention
- **Default:** *"Inputs and outputs are automatically deleted within 30 days,"* unless otherwise agreed in writing or legally required.
- **Recommend:** If a client needs shorter, negotiate it in writing — the FAQ contemplates exactly that.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** API key hygiene
- **Where:** xAI Console → API Keys → ⋮ → Disable key / Delete key
- **Default:** Keys are team-scoped and live until revoked.
- **Recommend:** Hold keys in a secret manager rather than in shell configuration, never share them between teammates, and rotate them regularly.
- **Risk:** Medium
- **Confidence:** `verified`

## 10. Mobile & OS app permissions

- **Setting:** iOS **App Privacy** label — `Data Linked to You`
- **Where:** https://apps.apple.com/us/app/grok-ai/id6670324846 → App Privacy
- **Default:** As declared by **X Corp.**, app version **1.4.47**, listing updated **2026-10-01**: **Analytics** — Email Address, Name, User ID, Device ID. **App Functionality** — Email Address, Name, User ID, Device ID, Crash Data, Performance Data, Other Diagnostic Data. **No `Data Used to Track You` and no `Data Not Linked to You` section** are declared.
- **Exposes:** Your email, name and device/user IDs are linked to your identity and used for analytics. Apple's disclaimer applies: *"This information has not been verified by Apple."*
- **Recommend:** **Note the gap** — the iOS label declares no collection of User Content, Photos, Audio or Search History, which does **not** match what the Privacy Policy says is collected (files, images, audio, voice, video, conversation history). **Trust the Privacy Policy over the label.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Android **Data safety** declaration
- **Where:** https://play.google.com/store/apps/datasafety?id=ai.x.grok
- **Default:** As declared by **SpaceXAI**, app version **1.2.42-release.01**, updated 2026-10-01. **Data shared** with other companies: Crash logs, Diagnostics, Other app performance data · Device or other IDs · App interactions (Analytics, **Personalization**) · **`Photos` (Fraud prevention, security, and compliance)**. **Data collected:** Name, Email address, User IDs · Approximate location · Files and docs · Crash logs/Diagnostics · Device or other IDs · App interactions, **In-app search history**, **Other user-generated content**, Other actions · Photos. Security: *"Data is encrypted in transit"*; *"You can request that data be deleted."*
- **Exposes:** **The Android declaration is materially broader than the iOS one** — it admits collecting your prompts (`Other user-generated content`), in-app search history, files and docs, approximate location and photos, and **shares `Photos` and `App interactions` with other companies.** There is no "No data shared with third parties" badge.
- **Recommend:** **On Android, assume photos you hand Grok leave xAI.** Grant Photos per-item rather than full-library.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** OS runtime permission grants — Microphone, Camera, Photos, Location, Notifications, Contacts
- **Where:** iOS: Settings → Grok. Android: Settings → Apps → Grok → Permissions.
- **Default:** Both platforms require explicit runtime consent; nothing granted at install.
- **Exposes:** Microphone feeds voice mode (retained, transcribed, training-eligible); Photos/Camera feed image understanding and Imagine; approximate location is declared collected on Android.
- **Recommend:** Microphone only while using voice; deny Camera unless needed; Photos as "Selected Photos" only; deny Location. **The OS layer is your only hard control over the camera and mic, since Grok exposes no in-app toggle for either.**
- **Risk:** High
- **Confidence:** recommendation `verified` as sound practice; **the exact declared permission list for each app is `unresolved`** — it could not be confirmed without decompiling the APK or an installed device, and no permission list is asserted here

- **Setting:** `Clear Cache`
- **Recommend:** Use on shared or client-facing devices.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Allow NSFW Content (I'm 18+)`
- **Default:** **Unresolved** (presumably off, age-gated — not confirmed).
- **Exposes:** Not a data-flow setting, but relevant given the DPC's February 2026 inquiry into Grok-generated sexualised imagery on X.
- **Recommend:** Leave off, especially on any device a minor can reach.
- **Risk:** Medium
- **Confidence:** label `verified`; default `unresolved`

## Volatile

1. **The X training toggle's label changed and may change again.** 2024: "Allow your **posts** … **with Grok**". Live 2026: "Allow your **public data** … with Grok **and xAI**". The scope broadened under a similar label. Any guide quoting the old string is stale.
2. **The legal entity renamed to SpaceXAI LLC**, Privacy Policy effective 2026-08-24 (a `previous version` link and a `previous-2026-04-04` URL both exist — the policy changed at least twice in 2026). X help says "xAI"; iOS says "X Corp."; Play says "SpaceXAI". Governing-policy questions keep shifting until these converge.
3. **The `noindex` on grok.com `/share/*` pages** is the live remediation of the 2025 indexing incident, but the Consumer FAQ **still warns that share links "may be subject to indexing by a search engine."** Doc and implementation disagree; one will move.
4. **`Allow chat link sharing`** is a new-looking setting with no documentation anywhere, an unknown default, and a flag literally named `enable_temp_always_request_share_link`. **Highest-churn item here.**
5. **Memory got rebuilt.** Live config carries `enable_memory_v2_management: false`, `enable_memory_v2_explicit_tools: false`, `enable_memory_summary: false`, `force_allow_memory_settings: false` — a v2 memory system is staged but not shipped. Expect §2 labels and defaults to change.
6. **`Import memory from other AI providers`** is new and unmentioned in any xAI legal page.
7. **The team / org plane is actively under construction.** `Organization Sharing & Retention`, `Product sharing` scopes, `Conversation retention`, `Migrate Personal Content` and `Team settings → Connectors` all exist in the shipped bundle with **zero public documentation.** Defaults here are the biggest gap in this file.
8. **Grok Bot's dependence on "Cursor authentication and account data settings"** (xAI's own words, doc updated 2026-09-28) is both surprising and unlikely to be the long-term arrangement. Re-check its training opt-out path.
9. **Connector roster is mid-rollout.** Live flags show GitHub and Notion off, SharePoint frontend off, `grok_web_connector_scope_consent_enabled: false` and `grok_web_live_connector_setup: false` — a scope-consent UI is staged but not live. OAuth scopes remain undocumented.
10. **Voice/camera is partly gated.** `voice_mode_camera_rollout: false`, `voice_chat_view_recording_player: false`, plus the contradictory pair `disable_voice_mode: true` / `enable_voice_mode: true`. Voice-mode screen sharing and custom voice cloning are new since 2025 and carry **no dedicated privacy controls yet.**
11. **Two open Irish DPC matters against X Internet Unlimited Company** — the 2025-04-11 Grok-training inquiry and the 2026-02-17 non-consensual-imagery inquiry. Either could force default or regional changes on the X side.
12. **xAI's US regional endpoint** is flagged `New` with a restricted model list and a 10% premium; expect coverage to expand and the exclusions to shrink.
13. **ZDR is now self-serve in the Console** (previously sales-gated) and xAI explicitly recommends *against* it — a notable posture. The disabled-feature list will likely shrink.

### Two things that could not be established, stated plainly

- **Defaults for most consumer toggles.** Neither xAI nor X publishes them. Every *label* and *path* was verified from live production code, but the only `verified` defaults are in the API and agentic planes. For the consumer toggles — **including both training toggles** — defaults are `reported` or `unresolved`. The honest instruction to a user is: **open both settings pages and look.**
- **Mobile runtime permission manifests.** Store data-safety declarations are verified above, but the actual list of requested Android/iOS permissions is not published in either listing, and no device or APK was available.


---

# Second pass — gap-fill, 2026-10-02

The first pass verified every setting's **label** and **path** from live production JavaScript, because
`x.ai` and `help.x.com` return HTTP 403 to automated fetching. What it could not verify was most
**default states**. This pass resolved ten of twelve by reading shipped code, regulator filings and
xAI's own developer documentation rather than the blocked help pages.

## The four results that change the audit

1. **`Allow chat link sharing` is ON by default**, in **all** regions including the EEA/UK and
   enterprise. The first pass flagged this as the single highest-priority unknown on the grounds that a
   default-on state would materially lower the bar to accidental exposure. It is default-on. Unlike the
   training and personalization toggles, it has **no regional carve-out**.
2. **The consumer defaults are regional, not global.** `Improve the Model`, `Personalize with
   conversation history` and `Personalize using 𝕏` are **ON outside the EEA/UK and OFF inside it**, with
   the rows hidden entirely for enterprise and government tenants. The first pass treated each as one
   global value and would have given an EEA client the wrong answer.
3. **The X-side training toggle is default-ON, and it does *not* ship off for the EEA.** The ON default
   is now `verified` from a **Swiss FDPIC regulator document**. And the open EEA question is answered:
   **the 2024 Irish undertaking was a dataset-specific deletion commitment, not a change to the
   toggle's default.** Anyone who read the undertaking as "EU accounts are opted out" read it wrong.
4. **Connector OAuth scopes are published after all** — at `docs.x.ai/grok/connectors/*`, not in the
   client bundle the first pass grepped. Full tables below. The operative findings: **Outlook, OneDrive
   and Teams grant write/send authority in one click with no read-only option**, Drive writes grant the
   **full `drive` scope**, and SharePoint's recommended mode is tenant-wide read plus a background index
   holding its own separate grant under a second Entra app registration. xAI's own opt-in scope picker
   exists in the shipped code and **is switched off in production**, so the provider's consent screen is
   currently the only place a user sees what they are granting.

## One contradiction, deliberately not resolved

`Watermark Imagine generations` reads **`false`** in the client preference and its row is hidden — but
`docs.x.ai/grok/faq` says Imagine output **is** watermarked with no way to remove it. Both facts are
`verified` and they do not reconcile. **Do not publish "watermarking is off by default"** on the
strength of the preference value; what that preference actually changes is unknown.

## Still open

The server-side stored defaults for the two X-side toggles (`allow_grok_memory`,
`allow_xai_personalization`) rest on a single outlet's hands-on and stay `unresolved`; closing them
needs a brand-new X account read before anything is touched. The shipped team **conversation-retention**
value is undocumented across all 185 pages of `docs.x.ai`. And catalog-connector scopes are
`unresolved` **by construction** — they are defined by each third party's own MCP endpoint, so that is
N provider-side lists rather than one missing xAI list.

## A regulator finding that fits but cannot be attributed

The DPC's AI Insights Report (Sept 2026, p. 36) describes an unnamed controller whose *"opt out for
processing personal data for AI training for a particular chatbot was not available to non-subscribers
using mobile devices"* — ~7.7 million EEA mobile users, identified Jan 2025, fixed Feb 2025, with a
commitment not to train on data collected during the gap. **It fits X/Grok**: Grok was open to all users
and the opt-out was long web-only. **The report does not name it, so it stays unattributed here.** Noted
because it is the kind of thing that gets confidently misattributed once it enters circulation.

---

**Method note.** `x.ai/*` and `help.x.com/*` still 403 to automated fetching. The breakthrough came from
Route 1, done deeper than the previous pass: the previous pass had only the **84 chunks referenced by
grok.com's landing-page HTML**. Those 84 chunks internally reference ~1,885 more lazily-loaded chunks.
Crawling that graph (1,969 files total) surfaced the real client-side default objects, the GDPR branch,
and the settings UI bindings. Separately, `x.com/settings/grok_settings` returns HTTP 200 and serves the
legacy `responsive-web/client-web` stack, whose chunk id→name→hash maps are inlined in that HTML; that
let me pull all 1,093 X chunks from `abs.twimg.com` and find the X-side Grok code.

**Reproduction / provenance (hashed filenames rotate on deploy):**

grok.com (Next.js / Turbopack, `https://cdn.grok.com/_next/static/chunks/<name>.js`):
- `26x_v88vhivnt.js` — user-settings store: default object `B`, GDPR/enterprise object `M`, preference
  defaults `P`, `this.userSettings=B`, `initializeGdprUserSettings`, `initializeEnterpriseUserSettings`
- `1-rislvj__i6c.js` — GDPR country set `dv` and the init dispatcher that chooses `B` vs `M`
- `1-jsl8v3kdkhp.js` — Settings → Data Controls UI (`settings-data.*` toggle bindings)
- `3gfgjmgykxhkq.js` — team "Organization Sharing & Retention" panel
- `00wwe6evlg5_z.js` — `MIN_RETENTION_DAYS`, `retentionModeFromSettings`, `RetentionPeriodControl`
- `0kcqgmleanlog.js` — connector scope-consent helpers (`seedScopeGroupSelection`, `mayRequireScopeConsent`)
- `1tx97cquvu2z2.js` — generated REST client for `/rest/user-settings`
- `376vlecp-jky0.js` — en i18n string table

x.com (legacy stack, app-version `131ee3c4f16a0ba87fd52ca174db2b8554e9cd70`,
`https://abs.twimg.com/responsive-web/client-web/<name>.<hash>a.js`):
- `ondemand.SettingsRevamp.3f7a1da9c7e92895a.js` — `/settings/grok_settings` screen + the three toggles
- `shared~bundle.ComposeMedia~bundle.TwitterArticles.76a18f777fc2197ca.js` — "Block modifications by Grok"
- `i18n/en.236349331ade24e4a.js` — en i18n string table

Two further routes opened up that the brief did not anticipate, and both are **live production config,
not code**:

- **`docs.x.ai` is reachable** (unlike `x.ai/*`). It 308-redirects `/docs/*` → `/*`, serves 200, and
  every page is available as markdown by appending `.md`. `docs.x.ai/sitemap.xml` enumerates all 185
  pages. This is xAI's official documentation and it resolved items 11a and 12.
- **Both apps inline their live feature-flag payload in the HTML they serve to an unauthenticated
  request.** `https://x.com/settings/grok_settings` carries **1,390** X feature switches as
  `"<name>":{"value":…}`; `https://grok.com/` carries **727** xAI flag keys in its SSR payload. These
  are the real production values, so they settle the "is this row even visible?" questions that the
  bundle alone could not. Caveat, stated once and applying everywhere below: switch values can be
  bucketed per account, per subscription tier and per geography, and these were read from one
  unauthenticated request from a US egress — so they are *a* production value, authoritative for the
  anonymous/default bucket, not provably the value every user gets.

Production flag values used below (all read today):

| Flag | Surface | Value | Governs |
|---|---|---|---|
| `enable_temp_always_request_share_link` | grok.com SSR payload | `true` | the brief's flag — exists, server-side only (no client consumer) |
| `show_auto_share_settings` | grok.com SSR payload | `true` | server-side only; "Allow chat link sharing" row |
| `enable_memory_toggle` | grok.com SSR payload | `true` | item 4 row is rendered |
| `enable_browser_geo_location` | grok.com SSR payload | `false` | item 6 row is **not** rendered |
| `enable_watermark_setting` | grok.com SSR payload | **absent** | item 9 falls back to `false` → row hidden |
| `grok_web_connector_scope_consent_enabled` | grok.com SSR payload | `false` | the connector scope-consent dialog is **off** |
| `nsfw_enabled` / `disable_sharing` / `hide_files_page` | grok.com SSR payload | `false` / `false` / `false` | sharing is enabled; files page shown |
| `grok_settings_memory_visibility` | x.com switches | `"hide"` | item 7 row is **not** rendered |
| `grok_settings_age_restriction_enabled` / `grok_settings_restriction_age` | x.com switches | `true` / `18` | all three X Grok toggles `disabled` for under-18s |
| `responsive_web_grok_media_block_edit_enabled` | x.com switches | `true` | item 10 row **is** rendered |
| `responsive_web_grok_tweet_actions_edit_image_enabled` | x.com switches | `false` | in-timeline "edit image with Grok" entry point off |
| `responsive_web_grok_tweet_media_edit_image_button_enabled` | x.com switches | `false` | ditto, media viewer |
| `responsive_web_grok_tweet_media_detail_edit_image_button_enabled` | x.com switches | `false` | ditto, media detail |
| `responsive_web_grok_link_edit_image_to_grok_com_enabled` | x.com switches | `true` | image-edit instead routes out to grok.com |
| `responsive_web_grok_edit_image_attribution_mode` | x.com switches | `"free"` | attribution mode for Grok-edited images |

**Gating variables used throughout the Data Controls panel** (`grokjs2/1-jsl8v3kdkhp.js`), resolved so
the row-visibility claims below are checkable:
```js
s = useFeatureFlags()                                        // server flag map
c = useSession()
d = c.user?.organizationRole === OrganizationRole.ADMIN      // shows the org Sharing & Retention block
g = useIsActiveGrokBusinessSession()                         // true inside a team/business workspace
K = useSubscriptions().isEnterpriseUser
H = useIsGovernment()
C = useSettingsStore(e => e.userSettings)                    // the live settings object
T = fetchSetUserSettings ; P = fetchSetPreference
```
Consequence worth carrying into the audit: the rows gated on `!g` — **memory, chat-link sharing,
watermark and NSFW — disappear entirely inside an active Grok Business session**, where team policy
governs instead. "Improve the Model" is gated on `!K && !H`, i.e. hidden for enterprise and government
tenants regardless of workspace.

**The single most load-bearing new fact:** grok.com ships **two different default sets**, chosen by
account country. Everything below that says "non-EEA default" vs "EEA/UK default" rests on this:

```js
// 26x_v88vhivnt.js — non-GDPR default (also the pre-fetch placeholder: this.userSettings = B)
B = { excludeFromTraining:!1, allowXPersonalization:!0, preferences:P, enableMemory:!0,
      allowShareIndexing:!0, allowCompanionNotifications:!1, allowAutoShare:!0,
      allowGrokFinishedNotification:!1, agentCustomizations:[], agentLibrary:[],
      imagineEnabledConnectors:{connectorIds:[]} }

// 26x_v88vhivnt.js — GDPR / enterprise default, written to the server on first init
M = { excludeFromTraining:!0, allowXPersonalization:!1, preferences:P, enableMemory:!1,
      allowShareIndexing:!1, allowCompanionNotifications:!1, allowAutoShare:!0,
      allowGrokFinishedNotification:!1 }

initializeGdprUserSettings = () => settingsGetUserSettings().then(e => {
  (e.excludeFromTraining === undefined || e.enableMemory === undefined)
    ? fetchSetUserSettings(M)      // no stored value yet -> write the privacy-protective set
    : U(e, t) })                   // otherwise honour what the server already has

initializeEnterpriseUserSettings = () => settingsGetUserSettings().then(e =>
  e.excludeFromTraining ? U(e,t) : fetchSetUserSettings(M))
```

```js
// 1-rislvj__i6c.js — which accounts get M
dv = new Set(["AT","BE","BG","HR","CY","CZ","DK","EE","FI","FR","DE","GR","HU","IE","IT","LV","LT",
              "LU","MT","NL","PL","PT","RO","SK","SI","ES","SE","IS","LI","NO","GB"]);   // EU27 + IS/LI/NO + GB
// ...
if (user.email?.endsWith("@x.ai")) { /* skipped */ }
else if (countryCode && dv.has(countryCode)) {
   logEvent("initialize_gdpr_user_settings", countryCode, {...});
   if (!hasPreviouslyInitUserSettings)            // localStorage guard, once per browser
       useSettingsStore.getState().initializeGdprUserSettings()...
} else if (isEnterpriseUser) { initializeEnterpriseUserSettings() }
```

Note on the country list: it is **EU 27 + Iceland + Liechtenstein + Norway + GB**, and
**Switzerland (`CH`) is absent** — even though xAI's privacy policy groups Switzerland with Europe and
the Swiss FDPIC closed its own investigation into X/Grok in March 2025. A Swiss grok.com account
therefore receives the permissive set `B`, not `M`. Worth a line in the audit.

End-to-end confirmation of the mechanism: `countryCode` is **server-detected and inlined in the same
SSR payload** — my request came back with `"countryCode":"US","region":"California","regionCode":"CA"`,
which is why the US flag/default bucket is what I read. The GDPR branch would have fired on the same
code path had that value been one of the 31 in `dv`. (No prefetched `user-settings` object appears in
an anonymous payload — searched for `excludeFromTraining`, `exclude_from_training`, `allowAutoShare`,
`allowShareIndexing`: all absent — so the server-side stored default for a *fresh authenticated*
account is still inferred from the client's write-on-absent behaviour, not observed directly.)

Caveat to carry into the audit file: these are the **client's** defaults. For every field the client
writes `M` only when the server reports the field as absent, so the client default and the server
default coincide for a fresh account — but a value the server has already stored always wins. Where a
value is read straight off the server with no client fallback (all three X-side toggles) the bundle
proves nothing about the default, and I have said so — item 3 is resolved from the regulatory and
official record instead, items 7 and 8 remain unresolved.

**Full Data Controls panel, in shipped render order** (`grokjs2/1-jsl8v3kdkhp.js`), so the audit can
state the click path exactly. Toggles are marked T, action rows A, with the gate that controls each:

| # | Row | Type | Gate |
|---|---|---|---|
| — | "Organization Sharing & Retention" block | section | `d` (org admin) |
| 1 | Improve the Model | T | `!K && !H` |
| 2 | Personalize Grok using 𝕏 | T | `c.user?.xUserId` |
| 3 | Personalize Grok with your device location | T | `s.ENABLE_BROWSER_GEO_LOCATION` (prod: `false`) |
| 4 | Personalize Grok with your conversation history | T | `s.ENABLE_MEMORY_TOGGLE && c.user && !g` (prod flag: `true`) |
| 5 | Memory from your chats (summary) / Import memory | A | `ENABLE_MEMORY_SUMMARY` (prod: `false`) / `ENABLE_MEMORY_IMPORT` |
| 6 | Allow chat link sharing | T | `c.user && !g` |
| 7 | Watermark Imagine generations | T | `IMAGINE_CONFIGS.get("enable_watermark_setting", !1)` (prod: key absent) |
| 8 | Allow NSFW Content (I'm 18+) | T | `c.user && !g && s.NSFW_ENABLED` (prod: `false`) |
| 9 | See Files and Assets | A | `c.user && !s.HIDE_FILES_PAGE` (prod: `false` → shown) |
| 10 | See Shared Links | A | `c.user` |
| 11 | See Deleted Conversations | A | `c.user` — *"Deleted conversations are permanently removed after 30 days."* |
| 12 | Cookie Settings | A | `window.OneTrust` |
| 13 | Clear Cache / Export Account Data / Delete All Conversations / Delete All Imagine Data / Delete Account | A | — |

In the US/anonymous bucket that means the panel actually shows four privacy toggles — Improve the
Model, Personalize using 𝕏 (if X-linked), conversation history, and Allow chat link sharing — and the
location, watermark and NSFW rows are flagged off.

---

### 1. `Allow chat link sharing` (grok.com → Settings → Data Controls)

**Resolved default: ON — in every region, including EEA/UK and enterprise tenants.**

**How established — `verified`, read from shipped code, two independent places in the bundle:**
- `grokjs2/1-jsl8v3kdkhp.js`, the toggle's own render:
  ```js
  title: n("settings-data.allow-auto-share.title","Allow chat link sharing"),
  description: n("settings-data.allow-auto-share.description","Allow sharing chats using only your chat link."),
  checked: C.allowAutoShare ?? !0,      // absent server value renders as ON
  onCheckedChange: e => { ...; T({allowAutoShare:e}) }
  ```
  The `?? !0` is decisive: when the account has **no stored value**, the switch is drawn ON.
- `26x_v88vhivnt.js`: `allowAutoShare:!0` in `B` (non-GDPR) **and** `allowAutoShare:!0` in `M`
  (the GDPR/enterprise set). It is the only privacy-relevant field in `M` that is **not** flipped to
  the restrictive position — `M` turns off training, X-personalization, memory and share-indexing, and
  leaves chat-link sharing on. I checked every reference to `M` in that chunk: it is used only by
  `initializeGdprUserSettings` and `initializeEnterpriseUserSettings`, nowhere else.

Backing-flag note — resolved, and the brief's flag is real. `enable_temp_always_request_share_link`
is **not present in any of the 1,969 grok.com JS chunks** (grepped the literal plus
`always_request_share_link`, `alwaysRequest`, `tempAlways` across `grokjs/` + `grokjs2/` — zero hits),
which is why the previous pass could not place it. It **is** present in grok.com's server-delivered
flag payload, inlined in the HTML of `https://grok.com/`, with value **`true`**:
```json
"enable_notifications":true,"notifications_fetch_interval_ms":0,
"enable_temp_always_request_share_link":true,"enable_imagine_delete_button":true, …
"enable_enterprise_teams_connectors_and_collections":true,"show_auto_share_settings":true, …
```
Both it and the adjacent `show_auto_share_settings` (also `true`) have **no client consumer** — greps
over all 1,969 chunks return nothing for either name — so they are server-side flags governing
share-link issuance and the exposure of the Data Controls row respectively. The user-facing stored
field is `allowAutoShare`; the API surface is `POST /rest/user-settings` with body field
`allowAutoShare` (`1tx97cquvu2z2.js`), and shared-link objects are managed at
`/rest/app-chat/share_links` (+ `/share_links/summaries`). `disable_sharing` is `false` in production,
so sharing is on platform-wide.

Related, and worth adding to the audit as its own line: **`allowShareIndexing` defaults to `true`**
(`B`) and **has no UI anywhere in the shipped bundle** — grepped all 1,969 chunks for
`shareIndexing`, which appears only in the API client and the defaults object, never in a
`SettingsToggleRow`. It is flipped to `false` only by the GDPR/enterprise set `M`. So outside
EEA/UK/enterprise, a user cannot turn off indexing of shared chats from the product UI.

**Independent corroboration — `reported`, with a screenshot:** DeleteMe's "Grok Privacy Settings
Guide" (29 Jun 2026) shows this exact row **toggled on**
(https://joindeleteme.com/ai-privacy-settings/grok-privacy-settings-guide/#turn-off-grok-chat-link-sharing ,
screenshot https://joindeleteme.com/wp-content/uploads/2026/06/grokallowchatlinksharingtoggleon-1024x106.png )
and describes the semantics: *"a toggle that governs the Share feature, which generates a public URL for
one of your conversations. When it's turned on, you can click 'Share' on a chat, and Grok will create a
link that anyone with the URL can use to view the full conversation without needing an account."*

**Essential context — this toggle is a post-incident addition, and it shipped ON.** In August 2025,
Grok's share button published conversations to a public, search-indexed URL with no per-user control at
all. `corroborated reported`, and the contemporaneous coverage is unanimous that no setting existed:
- Forbes, Iain Martin, 20 Aug 2025 — *"Anytime a Grok user clicks the 'share' button… a unique URL is
  created… that unique URL is also made available to search engines, like Google, Bing and
  DuckDuckGo… hitting the share button means that a conversation will be published on Grok's website,
  **without warning or a disclaimer to the user**."*
  https://www.forbes.com/sites/iainmartin/2025/08/20/elon-musks-xai-published-hundreds-of-thousands-of-grok-chatbot-conversations/
  (mirror, Forbes blocks fetchers: https://www.forbes.com.au/news/innovation/xai-published-hundreds-of-thousands-of-grok-chatbot-conversations/ )
- PCMag, Aug 2025 — the only remedies offered were behavioural, not a setting: *"to stop Grok from
  publishing your chats online, **avoid using its share button**"*, plus revoking at
  `grok.com/share-links`.
  https://uk.pcmag.com/ai/159688/groks-share-button-is-a-privacy-disaster-heres-why-you-should-avoid-it
- TechCrunch, 20 Aug 2025: https://techcrunch.com/2025/08/20/thousands-of-grok-chats-are-now-searchable-on-google/
- BBC, 21 Aug 2025 — contrasts with OpenAI, whose chats were *"private by default and users had to
  explicitly opt-in to sharing them."* https://www.bbc.com/news/articles/cdrkmk00jy0o
- Also Fortune (22 Aug 2025), eWeek, Vice.

xAI's FAQ has since added an explicit disclosure, which did not exist at the time of the incident —
archived 13 Sept 2026, https://web.archive.org/web/20260913161312/https://x.ai/legal/faq :
> "**Note:** Any share link you generate will be accessible to anyone you choose to share the link
> with. For example, if you share the link publicly on a social media platform, **it may be subject to
> indexing by a search engine (e.g., Google)** just like any other publicly shared content."

`unresolved`: the exact ship date of the "Allow chat link sharing" toggle. No archived grok.com
settings page and no dated xAI announcement found.

**Confidence: high (verified) on the default; `corroborated reported` on the incident history;
`unresolved` on the ship date.**

**What changes for a user:** two toggles' worth of exposure sits ON by default and the brief's
prioritisation was right. Anyone who possesses a Grok chat link can open the chat without further
permission, and the GDPR carve-out does not help here. Outside EEA/UK there is additionally no
in-product way to opt shared chats out of indexing.

---

### 2. `Improve the Model` (grok.com)

**Resolved default: ON for consumer accounts outside EEA/UK (`excludeFromTraining:false`).
OFF for EEA/UK accounts and for enterprise accounts. Row hidden entirely for enterprise and
government tenants.**

**How established — `verified`, shipped code:**
- `grokjs2/1-jsl8v3kdkhp.js`:
  ```js
  !K && !H && SettingsToggleRow({                       // K = isEnterpriseUser, H = useIsGovernment()
    title: n("settings-data.improve-model.title","Improve the Model"),
    checked: !C.excludeFromTraining,
    onCheckedChange: e => T({excludeFromTraining: !e}) })
  ```
  The toggle is the **inverse** of the stored field, and the row is suppressed for enterprise/government.
- `26x_v88vhivnt.js`: `B.excludeFromTraining = !1` (training on) vs `M.excludeFromTraining = !0`
  (training off), with `M` written for `dv` countries and for enterprise users.

Two mechanical details worth recording, both `verified`:
- The EEA/UK write is **guarded once per browser** by a `hasPreviouslyInitUserSettings` localStorage
  flag, and additionally only fires when the server reports `excludeFromTraining`/`enableMemory` as
  absent. So it establishes the default; it does not re-assert it against a user's later choice.
- The **enterprise** write has **no such guard**: `initializeEnterpriseUserSettings` runs on every
  load and re-writes `M` whenever `excludeFromTraining` is falsy. An enterprise user who deliberately
  turns training *on* should expect it to be forced back off on the next session. (It is reached via
  the `else if (isEnterpriseUser)` arm, i.e. only for enterprise accounts **outside** the 31-country
  set; inside it, the GDPR arm handles them first.)

**Independent corroboration — `corroborated reported`:**
- DeleteMe, 29 Jun 2026, screenshot of the row **toggled ON** with the exact description string:
  https://joindeleteme.com/ai-privacy-settings/grok-privacy-settings-guide/ (image
  https://joindeleteme.com/wp-content/uploads/2026/06/grokimprovethemodel-1024x184.png )
- **xAI's own FAQ page embeds a mobile Data Controls screenshot showing "Improve the Model" and
  "Personalize Grok using X" both switched ON** —
  https://media.x.ai/cdn-cgi/image/fit=scale-down,onerror=redirect,f=auto/v1/website/app-data-6d629376.webp
  (embedded on https://x.ai/legal/faq ). Caveat worth noting: the *web* screenshot on the same page
  shows both OFF, because it illustrates the opted-out state, and it is stale — it predates the memory,
  location, link-sharing and watermark rows
  (https://media.x.ai/cdn-cgi/image/fit=scale-down,onerror=redirect,f=auto/v1/website/web-data-15f61728.webp ).
- Ars Technica, Jul 2024 (X side) — *"X is training Grok… and that's opt-out, not opt-in."*
  https://arstechnica.com/ai/2024/07/x-is-training-grok-ai-on-your-data-heres-how-to-stop-it/ ;
  ZDNET: https://www.zdnet.com/article/elon-musks-x-now-trains-its-grok-ai-on-your-data-by-default-heres-how-to-opt-out/
- Tom's Guide (privacy-settings comparison across chatbots); plus several smaller guides stating the
  opt-out posture directly.

**Official confirmation of the legal posture — `verified`:** xAI's **Europe Privacy Policy Addendum**
(https://x.ai/legal/europe-privacy-policy-addendum ) names **legitimate interests**, not consent, as the
basis for training — *"This is necessary for our legitimate interests in improving the accuracy and
performance of our models"* — and then: *"You can **object** to processing of your personal information
when our processing is based on our legitimate interests… Please note you can object to our use of your
information to train our models in your settings."* Legitimate interests plus a right to object is the
legal signature of an opt-out, i.e. on by default. (The EEA/UK client behaviour above means EEA/UK users
start already objected-out; the addendum still governs the non-default case.)

**Timeline, `verified` from Wayback:** in November 2024 **there was no toggle at all** —
https://web.archive.org/web/20241105123923/https://x.ai/legal/faq read *"You can opt-out of training by
**emailing us at privacy@x.ai**. Once you opt out, new conversations will not be used to train our
models."* By June 2025 the toggle existed —
https://web.archive.org/web/20250614022714/https://x.ai/legal/faq : *"**Grok.com Data Controls for
Training Grok:** For the Grok.com website, you can go to Settings, Data, and then 'Improve the Model' to
select whether your content is used for model training."* So the opt-out posture is original and
continuous; only the mechanism changed.

**Confidence: high (verified).** Upgraded from `reported`.

**What changes for a user:** a consumer account in, say, the US is opted into model training on
sign-up and must find Data Controls to leave; an account whose country code is in EU27/IS/LI/NO/GB is
opted out on first load without doing anything. Enterprise users cannot see or change the toggle —
their tenant is forced to `excludeFromTraining`.

---

### 3. The X-side training toggle (`x.com/settings/grok_settings`)

Label (verified from X's en table, id `i586f3e0`): *"Allow your public data as well as your
interactions, inputs, and results with Grok and xAI to be used for training and fine-tuning."*
Help text (id `a8d516a4`): *"X may share with xAI your X public data as well as your user
interactions, inputs and results with Grok on X to train and fine-tune Grok and other AI models
developed by xAI…"*

**Click path — `verified` two ways.** From shipped code: Settings → **Privacy and safety** → (second
group, "Data sharing and personalization") → **"Grok & Third-party Collaborators"** →
`/settings/grok_settings`. The row is unconditional (`includeGrokSettings:!0` in
`ondemand.SettingsRevamp...js`); the screen's testID is `xaiDataSharingSettings` and it renders exactly
three switches in this order — training, personalization, memory — plus a destructive "Delete
conversation history" action. X's own help page gives the identical path in prose
(`help.x.com/en/using-x/about-grok`, archived
https://web.archive.org/web/20260902121507/https://help.x.com/en/using-x/about-grok ):
*"Select 'Privacy & Safety' → Scroll to 'Data sharing and personalization' → Select 'Grok &
Third-party Collaborators' → You will see 'Data Sharing' → Select or de-select the option 'Allow your
public data as well as your interactions, inputs, and results with Grok and xAI to be used for training
and fine-tuning.'"* (The literal URL `/settings/grok_settings` is login-walled and has no Wayback
capture, but it is the route string in X's own bundle, so it is verified from code.)

#### 3a. Is it ON by default? — **Resolved: YES. `verified`.**

Upgraded from `reported`. The decisive source is a **regulator document**, the Swiss FDPIC's
conclusion of its investigation into X/Grok, 20 March 2025
(https://www.edoeb.admin.ch/en/conclusion-investigation-x-grok ):

> "TIUC informed the FDPIC about the opt-out option introduced since 16 July 2024. This allows users
> to **reject the default use** of their X contributions for training and fine-tuning Grok in the data
> protection settings. The FDPIC concluded that the company is complying with the requirements of the
> FADP by offering this opt-out option, **which is also offered in the EU**."

A regulator stating that the processing is "the default use" and that the control is an opt-out settles
the polarity. X's own help page corroborates the framing without ever using the words "on by default":
the section is titled **"How do I opt-out of model training?"** and documents only a de-selection
action — in the current wording and in the original 7 Aug 2024 wording
(https://web.archive.org/web/20240807122234/https://help.x.com/en/using-x/about-grok , then reading
*"Allow your posts as well as your interactions, inputs, and results with Grok to be used for training
and fine-tuning"*).

Additionally `corroborated reported` across many independent outlets with hands-on screenshots, and
still true in 2026:
- TechCrunch, 26 Jul 2024 — *"The setting is turned on by default."*
  https://techcrunch.com/2024/07/26/heres-how-to-disable-x-twitter-from-using-your-data-to-train-its-grok-ai/
- The Verge, 26 Jul 2024 — *"X uses your data to train its Grok AI assistant by default."*
  https://www.theverge.com/2024/7/26/24206904/x-grok-ai-train-turn-off
- Social Media Today, 28 Jul 2024 — *"users opted in by default."*
  https://www.socialmediatoday.com/news/x-opt-out-of-sharing-your-data-to-train-grok/722601/
- Tom's Guide, 30 Jul 2024; Variety, 26 Jul 2024; BleepingComputer, 27 Jul 2024; WIRED, Sept 2024.
- **Engadget, 28 Sept 2026** — *"X enrols every account in Grok training by default, covering both your
  public posts and conversations with SpaceXAI's chatbot."*
  https://www.engadget.com/2268598/how-to-stop-ai-companies-training-your-data/
- PCMag, updated 21 Jul 2026 (headline: "X Has a Hidden Setting Turned On by Default"):
  https://www.pcmag.com/explainers/x-twitter-has-hidden-setting-training-elon-musks-ai-how-to-turn-it-off
- PPC Land, 11 Jul 2026, reporting Surfshark research — *"X sets AI training consent to on by default"*,
  3–5 actions to disable: https://ppc.land/meta-drops-instagram-ai-tagging-tool-as-8-of-10-apps-default-users-in/

**String/UI timeline, `verified` from Wayback diffs of `help.x.com/en/using-x/about-grok`:**
- ≤ 13 Nov 2024 — old string *"your **posts** as well as your interactions…"*, settings path "Grok":
  https://web.archive.org/web/20241113070229/https://help.x.com/en/using-x/about-grok
- by 10 Dec 2024 — current string *"your **public data** … with Grok **and xAI**"*, path renamed to
  **"Grok & Third-party Collaborators"**:
  https://web.archive.org/web/20241210020141/https://help.x.com/en/using-x/about-grok
- between 23 and 30 Jan 2025 — the "Grok Personalization" section (item 8) is added:
  absent https://web.archive.org/web/20250123122941/https://help.x.com/en/using-x/about-grok ,
  present https://web.archive.org/web/20250130172040/https://help.x.com/en/using-x/about-grok

**Confidence: high (verified).** Note what the client contributes here: nothing. The value is a Relay
field read straight off the server with no fallback —
```js
let {__id:o, allow_xai_data_sharing:c} = useFragment(v, userPreferences);
let p = !!c;                     // no ?? fallback, no seed value
return <Toggle checked={p} disabled={l} name="allowXaiDataSharingCustomization" .../>
```
(mutation `XaiDataSharingSettingsMutation`, variable `allowXaiDataSharing`). So the default is
established entirely by the external record, not by the bundle.

**What changes for a user:** every X account is enrolled in Grok/xAI training on creation, including
the content of their Grok conversations, and the only exit is a three-levels-deep checkbox.

#### 3b. Does it ship OFF for EU/EEA accounts? — **Resolved: NO, on the best available record.**

**Label: `verified` that what the EU gets is an opt-out rather than an opt-in or a regional default-off;
`corroborated reported` that EU/EEA accounts were and are defaulted in; `unresolved` only on a
first-hand observation of the checkbox on a newly created EU/EEA account today.**

This is the one item where the brief's hypothesis does not survive. The 2024 Irish remedy was a
**backward-looking, dataset-specific** commitment, not a change of default.

**The undertaking itself.** Full text obtained and published by TechCrunch, 4 Sept 2024
(https://techcrunch.com/2024/09/04/irelands-privacy-watchdog-ends-legal-fight-with-x-over-data-use-for-ai-after-it-agrees-to-permanent-limits/ ):

> "Twitter International Unlimited Company undertakes that personal data comprised in EU/EEA publicly
> accessible posts … which is contained in datasets which were used for the purposes of developing,
> training and/or refining … 'Grok' **between May 7, 2024 and August 1, 2024, shall be deleted and not
> processed** … for the aforementioned purposes."

Nothing about future processing, consent, or any setting. Max Schrems in the same piece: *"Basically
Twitter got away without any fine… Twitter continues to offer the product based on unlawfully obtained
data."*

**The DPC's own press releases say nothing about defaults.** 8 Aug 2024
(https://www.dataprotection.ie/en/news-media/press-releases/dpc-welcomes-xs-agreement-suspend-its-processing-personal-data-purpose-training-ai-tool-grok )
— the first-ever use of s.134 Data Protection Act 2018 by any Lead Supervisory Authority — and
4 Sept 2024, striking out the proceedings on the undertaking becoming permanent
(https://www.dataprotection.ie/en/news-media/press-releases/data-protection-commission-welcomes-conclusion-proceedings-relating-xs-ai-tool-grok ).
Neither mentions toggles, settings, defaults, opt-in or opt-out. `verified` negative.

**Nor does any later DPC/EDPB material.** The DPC's **AI Insights Report, Sept 2026**
(https://www.dataprotection.ie/sites/default/files/uploads/2026-09/DPC-AI-Insights-Report-AC.pdf )
frames the X case purely as a mitigations failure, and — crucially — its normative framework for AI
training treats **Article 21 objection / opt-out** as the compliance mechanism, not mandatory opt-in:
*"there may be no effective way for users to exercise their Article 21 rights if not provided the
opportunity to opt out or object prior to the processing beginning"*; *"Objection forms or opt outs
should be easily accessible, easy to use…"* (pp. 52–53). I found **no EDPB opinion, statement or
Art. 66 urgent binding decision specific to X/Grok** — the DPC's 4 Sept 2024 EDPB referral produced
only generic AI-model guidance. `unresolved` on EDPB.

**Positive evidence that EU/EEA accounts were and are defaulted in:**
- **noyb, 12 Aug 2024** (nine GDPR complaints, AT/BE/FR/GR/IE/IT/NL/ES/PL) —
  https://noyb.eu/en/twitters-ai-plans-hit-9-more-gdpr-complaints — *"began unlawfully using the
  personal data of more than 60 million users in the EU/EEA … without their consent"*, and explicitly:
  *"most people found out about **the new default setting** through a viral post … on 26 July 2024 –
  over two months after the AI training had begun."* X relied on legitimate interests, not consent.
- **X's own statement, 8 Aug 2024**, quoted by TechCrunch
  (https://techcrunch.com/2024/08/08/elon-musks-x-agrees-to-pause-eu-data-processing-for-training-grok/ ):
  *"We are pleased that people using X in the EU can continue to use Grok and control how their data is
  used with **a simple privacy setting**."* The EU remedy was framed as the same user-controlled
  setting, not a regional default flip.
- **FDPIC, 20 Mar 2025** — the opt-out against "the default use" *"is also offered in the EU."*
- **X Privacy Policy effective 15 Jan 2026**, archived
  https://web.archive.org/web/20261001000125/https://x.com/en/privacy (official PDF
  https://legal.x.com/content/dam/legal-twitter/site-assets/x-privacy-policy-2026-09-21/en/x-privacy-policy-2026-09-21.pdf ):
  *"**If you do not opt out**, in some instances the recipients of the information may use it for their
  own independent purposes… including, for example, to train their artificial intelligence models."*
  Its only EEA-specific content is controller/DPO/LSA identification (X Internet Unlimited Company,
  Dublin; Irish DPC as LSA) — **no EEA carve-out for AI-training defaults**. `verified`
- **xAI's own FAQ** states the opposite of a default-off rule for the EU: *"in some regions (excluding
  the EU/UK), when you use Grok without logging in, you won't have the option to opt out of model
  training"* — i.e. EU/UK get an opt-out where others do not. `verified` (https://x.ai/legal/faq ;
  direct fetch 403s, reachable via text proxy).
- **help.x.com has never published an EU/EEA variant** of the Grok settings instructions — no "EU",
  "EEA" or "Europe" string appears in the settings sections across Wayback snapshots from Aug 2024
  through Sept 2026. `verified` negative.
- 2026 how-to journalism records no EU exception for X even while carving one out for Meta
  (Engadget, Sept 2026; Surfshark/PPC Land, Jul 2026). `reported`

**Claims to the contrary, flagged and not relied on:** AI-generated SEO pages (e.g. cortexos.app:
*"the Irish DPC … leading to a pause and eventual exclusion for the EU"*) assert an EU exclusion. It is
unsourced and contradicted by the FDPIC (Mar 2025) and by the DPC's April 2025 inquiry into *ongoing*
EU/EEA training. Do not cite it.

**The April 2025 statutory inquiry and whether training resumed.**
- **Opened 11 April 2025** under s.110, into *"the processing of personal data comprised in
  publicly-accessible posts posted on the 'X' social media platform by EU/EEA users, for the purposes
  of training generative artificial intelligence models, in particular the Grok Large Language Models
  (LLMs) … lawfulness and transparency"*
  (https://www.dataprotection.ie/en/news-media/latest-news/data-protection-commission-announces-commencement-inquiry-x-internet-unlimited-company-xiuc ;
  TIUC renamed **X Internet Unlimited Company (XIUC)** from 1 April 2025). Corroborated by Reuters,
  RTÉ, Politico, TechCrunch. `verified`
- **Still open as of Sept 2026, no decision, no fine** — the DPC AI Insights Report (p. 29) lists both
  the Grok-LLM-training inquiry and a second XIUC inquiry into Grok generative functionality affecting
  EU/EEA data subjects "including children" as ongoing. `verified`
- **Did X resume EU training, and under what default?** No company statement exists. The inference —
  that EU/EEA public posts continued or resumed being processed on a legitimate-interests,
  default-on/opt-out basis — follows from the undertaking's narrow scope, the April 2025 inquiry into
  ongoing processing, and the FDPIC's March 2025 finding. Label that inference
  `corroborated reported`; an explicit resumption date or X statement about the EU default is
  **`unresolved`**.

**Other 2025–26 regulatory actions, none of which pin down a default** (`verified`):
- **DPC inquiry, 17 Feb 2026** into XIUC over *"the creation and publication of potentially harmful,
  non-consensual intimate and/or sexualized images … including children, using generative artificial
  intelligence functionality associated with the Grok large language model"*, examining **GDPR Arts. 5,
  6, 25 (data protection by design and by default) and 35 (DPIA)**
  (https://www.dataprotection.ie/en/news-media/press-releases/data-protection-commission-opens-investigation-x-xiuc ).
  This is the only DPC proceeding putting Art. 25 "by default" in scope — but about Grok's image
  generation, **not** the training toggle.
- **European Commission, 26 Jan 2026 — DSA, not GDPR/AI Act**: formal proceedings on whether X assessed
  and mitigated systemic risks from Grok's functionalities, including manipulated sexually explicit
  images, and whether it produced a pre-deployment risk assessment for Grok
  (https://digital-strategy.ec.europa.eu/en/news/commission-investigates-grok-and-xs-recommender-systems-under-digital-services-act ).
  Does not mention training data, GDPR, or default settings.
- **EU AI Act: `unresolved`** — no AI Act action, decision or AI Office measure found concerning X/Grok
  training defaults.
- **Switzerland**: FDPIC closed its preliminary investigation 20 Mar 2025 finding the opt-out model
  FADP-compliant.
- **UK ICO** reportedly opened a Grok investigation 3 Feb 2026 — `reported` only; the ICO URL could not
  be retrieved, so treat as unverified.

**What changes for a user:** an EEA or UK account on **x.com** gets the same default-on training toggle
as a US account — the Irish action deleted a 2024 dataset, it did not flip the switch. That is the
opposite of **grok.com**, where xAI *does* ship the privacy-protective set to the same 31 countries
(see the `dv` set above). Anyone writing guidance should not tell EEA users they are protected by
default on X.

**Verified negative on a client-side EU gate:** I searched X's live 1,390-key switch payload for any
region/jurisdiction gate that could sit in front of this toggle (`\beu\b`, `_eu_`, `europe`, `dsa`,
`gdpr`, `region`, `geo`, `country`, `jurisdic`, `p13n`, `personaliz`). The only hits are DSA reporting
flows, German/Turkish media transparency, Birdwatch country allow-listing,
`responsive_web_personalization_id_sync_enabled:false` and `xchat_enable_eu_report:false` — **nothing
touching xAI training**. And `ondemand.SettingsRevamp...js` does contain an `isEUUser` selector
(`settings_metadata.is_eu || is_eu_country`) but it is wired only to the **Off-X Activity / cookie-use**
screen; the same is true of the other five chunks that reference `is_eu_country` (`bundle.Routes`,
`bundle.Ocf`, `ondemand.SettingsInternals`, `bundle.LoggedOutHome`,
`shared~loader.LoggedOutExtras…`), all of which use it for ads/cookie personalization propagation in
signup flows. The only gating on the three Grok toggles is age
(`grok_settings_age_restriction_enabled: true`, `grok_settings_restriction_age: 18` — under-age
accounts get the switches `disabled`).

---

### 4. `Personalize Grok with your conversation history` (grok.com)

**Resolved default: ON outside EEA/UK (`enableMemory:true`); OFF for EEA/UK and enterprise.
Row is additionally gated on a server feature flag.**

**How established — `verified`, shipped code:**
- `grokjs2/1-jsl8v3kdkhp.js`:
  ```js
  s.ENABLE_MEMORY_TOGGLE && c.user && !g && SettingsToggleRow({
     title: n("settings-data.memory-toggle.title","Personalize Grok with your conversation history"),
     description: n("settings-data.previous-conversations.description",
       "Allow Grok to remember details from your previous conversations. Private chats are never stored."),
     checked: C.enableMemory, onCheckedChange: e => T({enableMemory:e}) })
  ```
- `26x_v88vhivnt.js`: `B.enableMemory = !0`; `M.enableMemory = !1`.

Row visibility also resolved: `ENABLE_MEMORY_TOGGLE` maps to the server flag `enable_memory_toggle`
(constant table in `26x_v88vhivnt.js`), and grok.com's inlined production payload carries
`"enable_memory_toggle":true` — so **the row is rendered**. Companion flags in the same payload:
`enable_memory_summary:false` (the "Memory from your chats" summary viewer is hidden),
`enable_memory_import:true`, `enable_memory_editing:true`, `force_allow_memory_settings:false`.

**Independent corroboration — `corroborated reported`, and it independently confirms the EEA/UK
carve-out:**
- **TechCrunch, 16 Apr 2025** — *"Grok's new memory feature is available in beta on Grok.com and the
  Grok iOS and Android apps, **but not for users in the EU or U.K.** It can be turned off from the Data
  Controls page in the settings menu."* https://techcrunch.com/2025/04/16/xai-adds-a-memory-feature-to-grok/
  (same EU/UK exclusion in The Economic Times:
  https://economictimes.indiatimes.com/tech/artificial-intelligence/grok-gets-a-memory-xai-rolls-out-recall-feature-mirroring-chatgpt/articleshow/120374371.cms )
- **CNET, Joe Hindy, 17 Apr 2025** — *"Despite being in beta, the feature is **enabled by default**, or
  at least it was when we tried it."*
  https://www.cnet.com/tech/services-and-software/grok-now-remembers-what-you-talked-about-and-heres-how-to-make-it-stop/
- DeleteMe, 29 Jun 2026 — screenshot of the row **switched on**, carrying a `beta` pill:
  https://joindeleteme.com/wp-content/uploads/2026/06/personalizegrokwithyourconversationhistory-1024x126.png

That is a clean three-way convergence: the shipped `B`/`M` objects, a tech-press report of the EU/UK
exclusion at launch, and a hands-on report plus screenshot of the default-on state.

**Confidence: high (verified) — stored default from shipped code, row visibility from the live
production flag payload, corroborated by independent reporting including the EEA/UK carve-out.**

**What changes for a user:** outside EEA/UK, Grok accumulates a persistent memory of your chats from
the first conversation. The description's promise — "Private chats are never stored" — is the only
built-in escape hatch, and the incognito path is itself removable by a `disable_incognito` server flag.

---

### 5. `Personalize Grok using 𝕏` (grok.com)

**Resolved default: ON outside EEA/UK (`allowXPersonalization:true`); OFF for EEA/UK and enterprise.
Row only appears if the Grok account is linked to an X account.**

**How established — `verified`, shipped code:** `grokjs2/1-jsl8v3kdkhp.js`
```js
c.user?.xUserId && SettingsToggleRow({
  title: n("settings-data.x-personalization.title","Personalize Grok using 𝕏"),
  checked: C.allowXPersonalization, onCheckedChange: e => T({allowXPersonalization:e}) })
```
plus `B.allowXPersonalization = !0` / `M.allowXPersonalization = !1` in `26x_v88vhivnt.js`.
The declared data scope (i18n `settings-data.x-personalization.permissions`) is: *"𝕏 user profile,
𝕏 account information and location, 𝕏 settings, 𝕏 preferences, posts viewable on your 𝕏 account."*

**Independent corroboration — `reported`:** DeleteMe's screenshot of the row **switched on**
(https://joindeleteme.com/wp-content/uploads/2026/06/grokpersonalizationtoggle-1024x192.png ), and
xAI's **own** mobile Data Controls screenshot on https://x.ai/legal/faq shows "Personalize Grok using
X" ON alongside "Improve the Model"
(https://media.x.ai/cdn-cgi/image/fit=scale-down,onerror=redirect,f=auto/v1/website/app-data-6d629376.webp ) —
a first-party illustration, so `verified` for the state it depicts.

**Confidence: high (verified).**

**What changes for a user:** linking X to Grok outside EEA/UK silently turns on a cross-product data
flow that includes posts from protected accounts the user can see — the row is on from the moment the
link exists, and its visibility is conditional on the link, so an unlinked user never sees it and never
learns it exists.

---

### 6. `Personalize Grok with your device location` (grok.com)

**Resolved default: OFF (`enableBrowserGeoLocation:false`), in all regions — and in production the
row is not rendered at all, because the gating flag `enable_browser_geo_location` is `false`.**

**How established — `verified`, shipped code:**
- `26x_v88vhivnt.js`, the preferences default object `P` (which both `B` and `M` embed):
  `P = { ..., enableBrowserGeoLocation:!1, ... }`
- `grokjs2/1-jsl8v3kdkhp.js`: `s.ENABLE_BROWSER_GEO_LOCATION && c.user && SettingsToggleRow({ ...,
  checked: C.preferences.enableBrowserGeoLocation, onCheckedChange: e => P("enableBrowserGeoLocation",e) })`
- The Zod schema in the same file re-asserts the default via `.catch(e.enableBrowserGeoLocation)`,
  so a malformed stored value also falls back to `false`.

- Row visibility: grok.com's inlined production flag payload carries
  `"enable_browser_geo_location":false`, so the toggle is **absent from Data Controls** right now.
  The sibling `enable_chat_location_request` is also `false`.

**Confidence: high (verified) — stored default from shipped code, row visibility from the live
production flag payload.**

Corroboration status: **`unresolved`, and worth saying so.** I could find **no third-party
walkthrough, screenshot, or article that covers this row at all** — searches on the exact label and
description string return nothing, and everything written about "Grok location" concerns IP geolocation
or OS-level permissions rather than this toggle. That is consistent with the row being flagged off for
essentially everyone. The one adjacent official statement is xAI's privacy policy: *"We obtain your
consent prior to collecting precise location information."* (https://x.ai/legal/privacy-policy )

**What changes for a user:** nothing to fix — this one ships off and is not even exposed. Note that
`enable_chat_location_request` is a separate per-chat prompt rather than a stored preference, and it is
also off, so neither location path is live in the anonymous bucket.

---

### 7. `Allow Grok to remember your conversation history` (X side)

**Resolved default: `unresolved`** (but see the row-visibility finding below, which matters more in
practice). What blocked it: the same structure as item 3a — no client default; the value is a
server-supplied Relay field.
```js
// ondemand.SettingsRevamp.3f7a1da9c7e92895a.js
let i = featureFlagString("grok_settings_memory_visibility","hide");
let {__id:c, allow_grok_memory:d} = useFragment(H, userPreferences);
let g = !!d;
return i === "hide" ? null : <Toggle checked={g} disabled={o || i==="disable"} name="allowXaiMemory" .../>
```
Mutation `XaiMemoryMutation`, variable `allow_grok_memory`. Help text (id `f49b39b8`): *"Allow Grok to
remember details from your previous conversations. You can delete individual conversations to forget the
associated details."*

**But the more important finding, and it is `verified`: the row is not rendered in production.**
The client's own fallback for `grok_settings_memory_visibility` is `"hide"` (the third argument to the
flag read), and X's **live switch payload — inlined in the HTML of `x.com/settings/grok_settings` —
carries `"grok_settings_memory_visibility":{"value":"hide"}`**. The three states are `hide` (row not
rendered at all), `disable` (rendered but read-only), anything else (interactive). So today the X-side
memory toggle **does not appear on the page**, in the anonymous/default bucket.

Also verified from the same payload: `grok_settings_age_restriction_enabled: true` and
`grok_settings_restriction_age: 18`, which is what drives the `disabled` prop on all three Grok
toggles for under-18 accounts.

**Third-party evidence on the stored default — `reported`, single source, and it conflicts with the
production flag above.** PCMag, Jason Cohen, updated 21 Jul 2026, hands-on:
> "I opened Settings and privacy > Privacy and safety > Grok & Third-party Collaborators and found
> **three things enabled by default**: Allow your public data, as well as your interactions, inputs, and
> results with Grok and xAI, to be used for training and fine-tuning. Allow X to personalize your
> experience with Grok. **Allow Grok to remember your conversation history.** I unchecked all three."

https://www.pcmag.com/explainers/x-twitter-has-hidden-setting-training-elon-musks-ai-how-to-turn-it-off
(Yahoo Tech / regional PCMag editions carry the same article and are **not** independent corroboration.)

**Reconciling the two, honestly:** PCMag saw the row in July 2026; the anonymous/default bucket today
returns `grok_settings_memory_visibility: "hide"`. Both can be true — the switch is a per-cohort string
value, so it was presumably not `"hide"` for that account at that time, or has since been set to `hide`
platform-wide. I am not going to collapse this into one claim. The defensible statement is: *the row is
flagged hidden in the bucket I can observe; where it has been visible, one outlet reports it shipped ON.*

X's help centre is silent on it: `help.x.com/en/using-x/grok-memory` exists in Wayback only as a single
403 capture (`20260804095212`) and currently returns 404, and no "remember"/"memory" string appears
anywhere in the Sept 2026 "About Grok" page. `verified` negative.

Weak contrary signal, flagged not relied on: a July 2026 tutorial video is framed as *enabling* the
setting — "How To Allow Grok To Remember Your Conversation History On X.Com / Twitter", with a
"1:07 Turn On Conversation History Memory" chapter and a description saying it shows you where to
*"turn it on"* (https://www.youtube.com/watch?v=nwg47Ns-GGE , 10 Jul 2026). Low-quality channel; the
account may simply have had it off. It is the only thing pointing the other way.

Do not conflate this with grok.com's memory toggle (item 4). CNET's *"enabled by default"* finding and
TechCrunch's EU/UK exclusion both concern the **xAI-side** control, not this X-side one.

**Confidence: high (verified) that the row is hidden in the observable production bucket and on the
field name; the stored value's default is `reported` on one outlet's hands-on, and therefore
`unresolved` as a firm default.**

**What changes for a user:** there is currently **no X-side control over Grok conversation memory** —
the toggle is flagged off, so a user cannot see or change it, and whatever the server has stored stands.
Practically this means "I checked my X Grok settings and memory wasn't listed" is the expected
experience, not evidence that memory is off. The only reachable memory control is the grok.com one
(item 4).

---

### 8. `Allow X to personalize your experience with Grok` (X side)

**Resolved default: `unresolved`.** Same blocker: server-supplied Relay field, no client default.
```js
let {__id:p, allow_xai_personalization:g} = useFragment(Z, userPreferences);
let h = !!g;
return <Toggle checked={h} disabled={d} name="allowXaiPersonalizationCustomization"
        learnMoreLink="https://help.x.com/using-x/about-grok" .../>
```
Mutation `XaiPersonalizationSettingsMutation`, variable `allow_xai_personalization`. Help text
(id `ed141096`) names the flow explicitly: *"X may share with xAI your X data as well as your user
interactions, inputs and results with Grok to personalize your experience with Grok and other AI
models developed by xAI."*

Row is unconditional apart from the age gate (no `*_visibility` flag, unlike item 7).

**Official framing — `verified`:** X documents this control *only* as an opt-out, which is the same
signature as item 3. `help.x.com/en/using-x/about-grok`, archived
https://web.archive.org/web/20260902121507/https://help.x.com/en/using-x/about-grok :
> "**How do I opt-out of Grok personalization?** You have the flexibility to control how your data …
> are used to personalize your Grok experience. Below you can see how you can opt-out by managing your
> privacy setting at X. … You will see 'Grok Personalization' → Select or de-select the option **'Allow
> X to personalize your experience with Grok.'**"

**Ship date — `verified`:** between 23 and 30 January 2025 (absent
https://web.archive.org/web/20250123122941/https://help.x.com/en/using-x/about-grok , present
https://web.archive.org/web/20250130172040/https://help.x.com/en/using-x/about-grok ).

**Third-party evidence on the default — `reported`, single source:** PCMag's 21 Jul 2026 hands-on (quoted
in full under item 7) lists this as one of *"three things enabled by default."*
https://www.pcmag.com/explainers/x-twitter-has-hidden-setting-training-elon-musks-ai-how-to-turn-it-off
No second independent outlet enumerates the shipped positions of all three X-side toggles, so this does
not reach `corroborated reported`.

**Confidence: high (verified) on click path, field name, ship date and the official opt-out framing;
the default is `reported` (one outlet) and therefore not firmed up to `verified`.**

**What changes for a user:** this is the X→xAI personalization pipe, distinct from the training pipe in
item 3, and it sits on the same screen — turning off training does not turn this off.

---

### 9. `Watermark Imagine generations` (grok.com)

**Resolved — but the honest answer is not "default off", and reporting it that way would be wrong.**

Three facts, each separately `verified`, which together mean the toggle does not do what its name
suggests to a reader of the defaults table:

1. **The stored preference defaults to `false`.** `26x_v88vhivnt.js`, preferences object `P`:
   `watermarkImagineGenerations:!1`, with the Zod schema's `.catch(e.watermarkImagineGenerations)`
   re-asserting it. `P` is embedded in both `B` and `M`, so this is region-independent.
2. **The row is hidden unless a remote Imagine config turns it on, and that config's client fallback is
   `false`.** `grokjs2/1-jsl8v3kdkhp.js`:
   `!!s.IMAGINE_CONFIGS.get("enable_watermark_setting", !1) && c.user && !g && SettingsToggleRow({...})`
   — the second argument is the fallback. Checked against production: `enable_watermark_setting` is
   **absent** from the 727-key flag payload grok.com inlines for an unauthenticated request (searched
   the unescaped payload for `watermark` — no key in any form), so `IMAGINE_CONFIGS.get(..., !1)`
   returns `false` and the row does not render. It may be delivered only inside an authenticated
   session or only to Imagine-eligible tiers.
3. **xAI's own documentation says Imagine output is watermarked regardless, with no way to turn it
   off.** `https://docs.x.ai/grok/faq`, section *"Why do my generated images/videos have a 'grok'
   watermark? Can I remove it?"*, verbatim:

   > "Generated images and videos include a Grok watermark to indicate that the content was created
   > with AI. **There is no setting to remove the watermark.** In some jurisdictions, labeling
   > AI-generated content is also legally required. Removing, altering, or obscuring the watermark or
   > other provenance signals is prohibited under our Acceptable Use Policy."

   Corroborated by a third party stating the same: metagrok.io — *"There is no setting to remove it."*
   (https://metagrok.io/how-to/own-grok-outputs-and-commercial-use) — `reported`.

**I cannot reconcile 1–2 with 3, and I am not going to paper over it.** The two readings that fit are
(a) the toggle adds an *additional or more prominent* visible watermark on top of a baseline mark that
is always applied, or (b) it is a gated experiment for a cohort where the baseline mark is absent.
Which one is true is **`unresolved`** — no third-party source documents this toggle at all, and every
"remove Grok watermark" article is about third-party scrubbing tools rather than this setting.

**The defensible line for the audit file, and the one I recommend:** *a visible Grok watermark is
applied to Imagine output by default and xAI's docs say there is no setting to remove it; separately, a
"Watermark Imagine generations" preference exists in the client, defaults to `false`, and its row is
hidden from accounts that do not receive the `enable_watermark_setting` config.* Do **not** write
"watermarking is off by default."

**Confidence: high (verified) on all three underlying facts; `unresolved` on what the toggle actually
changes and on row visibility for authenticated Imagine users.**

**What changes for a user:** nothing they can act on — the control is hidden from most accounts, and
per xAI's docs the watermark is not removable anyway. The audit value here is the contradiction itself:
a shipped preference whose name implies watermarking is opt-in, against documentation saying it is
mandatory.

---

### 10. `Block modifications by Grok` (X, per-post) — click path and default

**Click path resolved — `verified`.** It is **not** in the composer's main menu, not in the post "…"
menu, and not an account-level setting. It lives in the **composer's per-attachment media settings
dialog** — the same modal that holds alt text, crop, and the sensitive-media/content-warning controls.
Analytics section is `sensitive_media`.

Code, from `shared~bundle.ComposeMedia~bundle.TwitterArticles.76a18f777fc2197ca.js`:
```js
ec = m().b7e6d23a;   // "Block modifications by Grok"
eh = m().e98a8136;   // "Prevent Grok from modifying this content"
...
A = ("boolean" == typeof n /*isGrokEditBlocked*/) && !!u /*toggleIsGrokEditBlocked*/;
...
A ? <View role="group">
      <Checkbox checked={n} helpText={eh} label={ec} name="blockGrokEdit"
                onChange={b} type="switch" />
    </View> : null
```
Rendered in the same column as, and immediately after, the `aiGenerated` checkbox ("Generated with AI")
and before the `download` switch ("Allow video to be downloaded"). It only renders when the host passes
a boolean plus a handler, and the host gates that on a feature switch:
```js
let h = featureSwitches.isTrue("responsive_web_grok_media_block_edit_enabled");
if (isVideo) return <VideoMediaEditor {...e} blockGrokEditEnabled={h} … />
return <ImageMediaEditor {...e} blockGrokEditEnabled={h} … />
```
**That switch is `true` in production** (`"responsive_web_grok_media_block_edit_enabled":{"value":true}`
in the inlined payload on `x.com/settings/grok_settings`), so the row is live. The exact tab is
`MediaTab.SensitiveMedia`, rendered by `_renderSensitiveMediaTab()` — i.e. the dialog's
**Sensitive media** tab, alongside Alt text, Crop, and (for video) Subtitles/Trimmer.

**Resolved default: OFF — Grok modification is permitted unless the author opts in to blocking.
Proven twice, once in each of the two editor classes.**

Image path:
```js
_renderSensitiveMediaTab = () => { let {blockGrokEditEnabled:e} = this.props; …
  let s = e ? { isGrokEditBlocked: i[t]?.grokActions?.blockGrokEdit ?? !1,
                toggleIsGrokEditBlocked: this._handleToggleGrokEditBlocked } : null; … }
_handleToggleGrokEditBlocked = () => {
  let e = this.state.mediaMetadata[this.state.currentMediaId]?.grokActions?.blockGrokEdit ?? !1;
  this._updateCurrentMediaMetadata({ grokActions: { blockGrokEdit: !e } }); }
```
Video path — the constructor hard-codes it, and note the contrast with the download switch right next
to it, which *does* get a server-supplied default:
```js
this.state = { isAiGenerated: a?.selfReportedAiGenerated?.selfReportedAiGenerated ?? !1,
               isGrokEditBlocked: !1,                              // hard-coded off
               isAllowedDownloadVideo: e.allowDownloadVideoDefault, // server-supplied default
               … }
```
On publish the value is serialised to the media-metadata API as
`grok_actions: { block_grok_edit: "true" | "false" }`
(`bundle.ComposeMedia.9391d55f0d8e994aa.js`), and is only sent at all if the author touched one of the
media-metadata controls. The viewer-facing counterpart string exists too: *"Images from this post are
not editable by Grok"* (id `f6385f9c`).

**Mitigating context from the same production switch payload, worth recording so the audit does not
overstate the exposure:** X's in-app "edit this image with Grok" entry points are currently *off* —
`responsive_web_grok_tweet_actions_edit_image_enabled: false`,
`responsive_web_grok_tweet_media_edit_image_button_enabled: false`,
`responsive_web_grok_tweet_media_detail_edit_image_button_enabled: false` — while
`responsive_web_grok_link_edit_image_to_grok_com_enabled: true` routes the flow out to grok.com
instead, and `responsive_web_grok_edit_image_attribution_mode` is `"free"`. So the block-switch guards
a capability whose on-X buttons are presently disabled; the grok.com route is where it matters.

**Confidence: high (verified).**

**What changes for a user:** every image and video a user posts is Grok-editable by default, and the
only opt-out is a switch buried one level deep in the composer's media dialog, per attachment, before
posting. There is no account-level "never" and no retroactive control in the shipped client.

**Independent corroboration — `corroborated reported`, and it converges with the bundle exactly.**
X never announced this feature and it is absent from help.x.com, but three outlets found it in the same
place the code puts it, and all describe it as per-image and opt-in:
- **Social Media Today**, Andrew Hutchinson, 8 Mar 2026 — first sighting: *"a simple toggle that enables
  users to stop Grok from reimagining their material"*, located in *"the image/video upload flow in the
  post composer"*, with X having *"not promoted the new option as yet."*
  https://www.socialmediatoday.com/news/x-formerly-twitter-adds-option-to-restrict-grok-image-variations/814140/
- **The Verge**, Jess Weatherbed, 9 Mar 2026 — verified independently, and gives the exact gesture
  path: *"When you upload an image into the X post builder, you can locate it by tapping on the
  **paintbrush symbol** that appears on the bottom right of the thumbnail, and then selecting the
  **flag icon** at the bottom right of the editing taskbar."* Quotes the strings verbatim: *"block
  modifications by Grok"* and *"prevent @Grok from modifying this content."* Also: *"The toggle also
  doesn't appear on older content that's already been uploaded to X."*
  https://www.theverge.com/tech/891352/x-grok-xai-edit-blocker-photo-toggle
- **PCMag**, Jibin Joseph, 10 Mar 2026 — *"Tap the edit button, then select the **flag icon** to adjust
  the image's **content settings**. On this page, you'll see a button to 'Block modifications by Grok.'"*
  and *"X has not made an official announcement about its new button."*
  https://www.pcmag.com/news/x-adds-button-to-block-grok-from-editing-images-but-its-hard-to-find
- SquaredTech, 9 Mar 2026 — same flag-icon path, iOS-exclusive at the time.
  https://www.squaredtech.co/x-grok-edit-blocker-fails

That "flag icon → content settings" is precisely `MediaTab.SensitiveMedia` in the bundle, which is the
independent confirmation of the click path. **Ship date: 8 March 2026** (first sighting), never
officially announced.

**Default OFF, corroborated:** PCMag's July 2026 explainer states it plainly — *"the option is fairly
well hidden and **must be implemented on a case-by-case basis**. To block Grok from being able to edit
your photos, you need to **customize permissions before you post the image to X. You can't do it after
the fact.**"*
https://www.pcmag.com/explainers/x-twitter-has-hidden-setting-training-elon-musks-ai-how-to-turn-it-off

**Efficacy limits, from The Verge's hands-on — worth recording, because the toggle is weaker than its
label:** it blocks only the reply-tag vector. Bypasses that still worked at the time: long-pressing a
protected image on X iOS to open "Edit image with Grok" straight into the Grok app; saving the protected
image, re-uploading it and then tagging Grok (which strips the protection); and pulling the image into
the Grok app directly. Free accounts were already blocked from @Grok image edits after the January 2026
backlash, so the toggle's marginal effect falls mainly on Premium subscribers.

**Platform matrix — `unresolved`, and the sources contradict each other.** The Verge (Mar 2026): iOS
only, *"The Grok blocker didn't appear at any point during the X image upload process on the web in our
testing."* PCMag's July 2026 explainer: *"I was also only able to do this on the web; the option is
available on iOS, but not Android yet."* The most consistent reading is that it expanded from iOS-only
in March to iOS + web by July, with Android still missing — but I cannot verify the current matrix.
(My own evidence is web-only: the component and the enabling switch are both in X's web bundle today.)

**Regulatory backdrop, `verified`:** this shipped during the Grok sexualised-image crisis that produced
the European Commission's DSA proceedings of 26 Jan 2026 and the Irish DPC's 17 Feb 2026 inquiry citing
GDPR Arts. 5, 6, **25 (by design and by default)** and 35 — see item 3b for both citations. A
per-image, opt-in, post-hoc-unavailable control is exactly the kind of design an Art. 25 analysis would
scrutinise.

**Flagged for the audit — a live inconsistency across X's two web stacks.** X is mid-migration to a new
front end (`abs.twimg.com/x-web/x-web/`). Its English table contains the **inverted** label
**"Allow modifications by Grok"**, with no consuming component yet in the shipped x-web chunks (grepped
all 2,078 downloaded x-web assets — the literal appears only in `assets/en-DHR7HtaA.js`). If that
polarity ships as written, the same underlying field will be presented as an allow-switch rather than a
block-switch, and a default-off allow-switch means the opposite of a default-off block-switch. This is
worth a watch-item rather than a finding.

---

### 11. Team / org plane defaults

Panel: grok.com → Settings → (team context) **"Organization Sharing & Retention"**, rendered by
`grokjs2/3gfgjmgykxhkq.js`, backed by `teamSettingsQueryOptions({teamId})` /
`updateTeamSettingsMutationOptions`.

#### 11a. `Product sharing` — "Set the widest audience members can share each resource with."

**Resolved scope ceiling — `verified`:** the ceiling differs by resource type.
```js
eA = [SharingScope.ORGANIZATION, SharingScope.TEAM, SharingScope.NONE];       // projects, skills
eI = [SharingScope.PUBLIC, ...eA];                                            // conversations only
rows = [ {conversationsScope, options: eN(eI, org.conversations)},
         {projectsScope,      options: eN(eA, org.projects)},
         {skillsScope,        options: eN(eA, org.skills)} ]
```
So **Conversations** can be raised to `Public`; **Projects** and **Skills** top out at `Organization` —
there is no public option for them at all. The enum is the protobuf `SharingScope`
(`SHARING_SCOPE_UNSPECIFIED, _NONE, _TEAM, _ORGANIZATION, _PUBLIC` = 0..4, confirmed in
`grokjs/0uf56-pwxogcp.js` and `grokjs/1tx97cquvu2z2.js`), and an org-level policy caps each team via
`eN` (filter `<= ceiling`) and `eC` (`min`), surfaced in the UI as *"Limited by organization policy."*

**Resolved default scope — `verified` from an official xAI source.** `https://docs.x.ai/grok/management`
(reachable as markdown at `https://docs.x.ai/grok/management.md`; `docs.x.ai` is **not** Cloudflare-
blocked, unlike `x.ai/*`) states verbatim:

> "Public links apply to conversations only; projects and skills cap at Organization. **By default,
> conversations and projects can be shared organization-wide, and skills start at Private.**"

So the shipped ceilings are **Conversations = Organization, Projects = Organization, Skills = Private**.
The same page gives the ladder and the semantics: *"A sharing policy sets the widest audience a member
may pick for a given resource; members can always share more narrowly, never more broadly"*, and
*"Tightening a policy applies right away. Members can no longer create shares wider than the new
ceiling, and access to existing shares beyond it is restricted to match."*

Note the divergence from the client's own fallback, which is worth recording because it shows the
client cannot be used alone here:
```js
conversationsScope = (server.sharing?.conversations && != UNSPECIFIED) ? that
                   : server.publicSettings?.allowPublicShare ? PUBLIC : NONE
projectsScope = eM(server.sharing?.projects)   // UNSPECIFIED/absent -> NONE
skillsScope   = eM(server.sharing?.skills)     // UNSPECIFIED/absent -> NONE
```
With nothing stored the client would draw all three as `None`; the server in fact supplies
Organization/Organization/Private. Also flag the legacy bridge in that code: a team with the old
`publicSettings.allowPublicShare` boolean set is promoted straight to ceiling-**`Public`** for
conversations under the new scope model, without anyone re-consenting.

**Confidence: high (verified — official xAI documentation for the defaults and the ceilings; shipped
code for the enum, the per-resource option lists, the org-policy `min()` cap and the legacy bridge).**

#### 11b. `Conversation retention` — "Set how long deleted or stale conversations are retained before being permanently removed."

**Resolved default: `Retain indefinitely` is NOT the client's shipped state. The client's fallback is
`Custom period` at 15 days.**
```js
// 00wwe6evlg5_z.js
MIN_RETENTION_DAYS = 15
clampRetentionDays = e => (!Number.isFinite(e) || e <= 0) ? 15 : Math.max(15, Math.min(1825, e))
retentionModeFromSettings = e => e ? "indefinite" : "custom"     // e = conversationsRetentionPeriodDisabled

// 3gfgjmgykxhkq.js
retentionDays     = server.conversationsRetentionPeriodDays       ?? MIN_RETENTION_DAYS   // 15
retentionDisabled = server.conversationsRetentionPeriodDisabled   ?? !1                  // false
mode              = retentionModeFromSettings(retentionDisabled)                          // "custom"
```
Range is 15–1825 days (max 5 years). The dropdown offers exactly two options, `Retain indefinitely`
and `Custom period`.

**Confidence: high (verified) for the client fallback. The authoritative server-side default for a
newly provisioned team is `unresolved`** — the `??` only fires when the API omits the field, and I
cannot observe an unauthenticated team-settings response. I am deliberately not calling this
"default = 15 days" for the product.

Checked against the official docs and the retention default is **not** documented: the
`https://docs.x.ai/grok/management` "Sharing policy" section documents Product Sharing in detail but
says nothing about Conversation retention, and `docs.x.ai/grok/faq` only offers *"Deleted chats and
files are removed from systems within standard retention windows unless we are required to retain them
longer for legal, compliance, or safety purposes."* Greps over all of `docs.x.ai` (185 pages, full
sitemap) for `conversation retention`, `retention period`, `indefinit`, `15 day`, `1825`, `5 year`
returned nothing. The 30-day figures in the xAI docs are the **API** audit-retention window
(`docs.x.ai/developers/faq/security`: *"all API requests and responses are stored on our servers
(encrypted at rest) for 30 days for auditing purposes… automatically deleted after 30 days"*), which is
a different control — do not conflate it with team conversation retention.

**What changes for a user:** an org admin reading the panel sees "Custom period / 15 days" on a team
that has never been configured, which reads as a retention *limit* rather than retain-forever — the
opposite of the hypothesis in the brief. Treat the shipped server value as unknown until an
authenticated team can be observed.

---

### 12. Connector OAuth scopes

**Resolved: YES — the full scope inventory is now sourced, from xAI's own documentation.**

**How established — `verified`, official xAI source.** `x.ai/*` and `help.x.com/*` 403, but
**`docs.x.ai` does not** (it 308-redirects `/docs/*` to `/*` and serves 200). Every page is available
as markdown by appending `.md`, and `docs.x.ai/sitemap.xml` lists all 185 pages. The connector docs
publish per-connector OAuth scope tables. URLs: `https://docs.x.ai/grok/connectors`,
`.../connectors/gmail-google-calendar`, `.../connectors/google-drive`, `.../connectors/onedrive`,
`.../connectors/outlook`, `.../connectors/microsoft-teams`, `.../connectors/sharepoint`,
`.../connectors/salesforce`, `https://docs.x.ai/grok/connector-management`.

#### Google — Gmail (tiered; `docs.x.ai/grok/connectors/gmail-google-calendar`)
| Scope | Purpose | When requested |
|---|---|---|
| `gmail.readonly` | Search and read emails | Always (base) |
| `gmail.modify` | Drafts, trash, label changes | When write tools are enabled |
| `gmail.send` | Send messages, reply, forward | When send tools are enabled |
| `gmail.labels` | Create and delete labels | When label-management tools are enabled |
| `userinfo.email` | Identify your Google account | Always |

xAI's note: *"gmail.modify is a superset of gmail.readonly. When write tools are enabled, only the
modify scope is requested to avoid duplicate permission prompts."* Read that carefully — once write is
enabled the user sees **one** prompt, for the broader scope, not two.

#### Google — Calendar (tiered; same page)
| Scope | Purpose | When requested |
|---|---|---|
| `calendar.readonly` | Search and read calendar events | Always (base) |
| `calendar.events` | Create, update, and delete events | When write tools are enabled |
| `calendar.freebusy` | Check availability / free-busy | When availability tool is enabled |
| `calendar.calendarlist.readonly` | List accessible calendars | When calendar-list tool is enabled |
| `userinfo.email` | Identify your Google account | Always |

#### Google Drive (`docs.x.ai/grok/connectors/google-drive`)
| Scope | Purpose |
|---|---|
| `drive.metadata.readonly` | View metadata for files in your Drive (titles, dates, folder structure) |
| `drive.readonly` | Read the content of files in your Drive |
| `drive` | Create and modify files in your Drive (write operations, optional) |
| `userinfo.email` | Identify your Google account |

`drive` is the **full-Drive** Google scope, i.e. the broadest one Google offers for Drive. xAI labels it
"(write operations, optional)", so the audit line should be: enabling Drive writes grants Grok
unrestricted read/write over the whole Drive, not a per-file picker grant.

#### Microsoft OneDrive (`docs.x.ai/grok/connectors/onedrive`) — Graph, delegated
| Scope | Purpose |
|---|---|
| `Files.ReadWrite` | Read and write files in the user's OneDrive |
| `User.Read` | Read the signed-in user's profile (used to identify the account) |
| `offline_access` | Maintain access without repeated sign-in prompts |

Note there is no read-only tier here: the base connection is already `Files.ReadWrite`.

#### Microsoft Outlook Mail (`docs.x.ai/grok/connectors/outlook`) — Graph, delegated
| Scope | Purpose |
|---|---|
| `Mail.ReadWrite` | Read, create, update, and delete mail and drafts |
| `Mail.Send` | Send mail on behalf of the user |
| `User.Read` | Read the signed-in user's profile |
| `offline_access` | Maintain access without repeated sign-in prompts |

Again no read-only tier — unlike Gmail, Outlook is connected with send-on-your-behalf from the start.

#### Microsoft Outlook Calendar (same page) — Graph, delegated
| Scope | Purpose |
|---|---|
| `Calendars.ReadWrite` | Read, create, update, and delete calendar events |
| `User.Read` | Read the signed-in user's profile |
| `offline_access` | Maintain access without repeated sign-in prompts |

#### Microsoft Teams (`docs.x.ai/grok/connectors/microsoft-teams`) — Graph, delegated
| Scope | Purpose |
|---|---|
| `Team.ReadBasic.All` | List the teams the user belongs to |
| `Channel.ReadBasic.All` | List channels within those teams |
| `ChannelMessage.Read.All` | Read messages in channels the user has access to |
| `ChannelMessage.Send` | Send messages and replies in channels |
| `ChannelMember.Read.All` | View channel membership |
| `TeamMember.Read.All` | View team membership |
| `Chat.Read` | Read one-on-one and group chat messages |
| `Chat.Create` | Create new one-on-one and group chats |
| `ChatMessage.Send` | Send messages in chats |
| `User.Read` | Read the signed-in user's profile |
| `offline_access` | Maintain access without repeated sign-in prompts |

Eleven scopes including DM read (`Chat.Read`) and send-as-you in both channels and DMs, all granted in
one step. This is the widest consumer-reachable grant in the set.

#### Microsoft SharePoint (`docs.x.ai/grok/connectors/sharepoint`)
Per-user sign-in scopes:
| Scope | Purpose |
|---|---|
| `Sites.Read.All` | Read items in all SharePoint site collections the user can access |
| `Files.Read.All` | Read all files the user can access (required for cross-site document search) |
| `User.Read` | Read the signed-in user's profile |
| `offline_access` | Maintain access without repeated sign-in prompts |

xAI's caveat, verbatim: *"When write capabilities are enabled for your organization, the connector
requests **Files.ReadWrite.All** instead of the read-only scopes above."* Separately, write access
*"uses a separate Microsoft Entra application with its own permissions… This grants the
`Files.ReadWrite.All` scope and is independent of the read-only consent from step 3."*

Plus a **background indexing sync with its own, separate scope set** — this is the part most likely to
be missed in an audit, because it is not the same grant the user approves at sign-in:
- Delegated mode: `Sites.Read.All` (*"Enumerate and read items from every site the account can
  access"*), `Files.Read.All` (*"Download file content for indexing across those sites"*),
  `offline_access`.
- Application mode: `Sites.Selected` (*"Read items only in the sites explicitly granted to the
  application… The sync cannot discover or index any site that has not been selected."*)

The two auth modes, with xAI's own framing:
- **Delegated permissions** *(xAI marks this "recommended")* — `Sites.Read.All`. xAI's mitigation advice
  is organisational, not technical: *"The recommended approach is to create a dedicated user account
  with access limited to specific SharePoint sites, then connect using that account."* Client copy
  (i18n `mcp-connectors.sharepoint.auth-mode.all-sites.*`): *"Grok reads all sites visible to the
  connecting admin"*, *"Quick setup with no additional configuration needed."*
- **Application-level permissions** — `Sites.Selected`. Client copy: *"Least-privilege access with no
  broad permissions"*, *"Requires an admin to configure allowed sites in Azure."*

Mitigation xAI states, and it should be quoted alongside the warning: *"Indexed content is
access-checked against the querying user on every request, so regardless of which sync mode is in use,
team members still only see results they are individually authorized to view in SharePoint."*

Audit line: xAI marks the **tenant-wide read** option as Recommended and the least-privilege option as
the one that "requires an admin to configure." SharePoint is also the one connector where the broad
option is reachable by clicking Continue on the default-selected choice — and it is the only connector
whose own documentation confirms xAI **stores** an index of the content, rather than reading in real
time.

#### Salesforce (`docs.x.ai/grok/connectors/salesforce`)
| Scope | Purpose | When requested |
|---|---|---|
| `mcp_api` | Access the Salesforce REST and SOAP APIs to read and write data | Always |
| `refresh_token` | Maintain access and refresh tokens between sessions | Always |

xAI: *"All actions are further restricted by your Salesforce profile, role, sharing rules, and
field-level security."* This connector is admin-provisioned (client ID/secret entered in the xAI
console) and runs via the Salesforce DX MCP server.

#### Mechanism and defaults, `verified` from shipped code
`grokjs/0kcqgmleanlog.js` plus the dialog in `grokjs2/1bondwvl6xnnr.js`
(`mcp-connectors.scope-consent.*`, *"Grant Permissions / Choose what Grok can do on your behalf"*):
```js
mayRequireScopeConsent = e => eM.has(e)
eM = new Set([ConnectorType.SHAREPOINT, SHAREPOINT_RW, SHAREPOINT_ADMINLESS, ONE_DRIVE,
              OUTLOOK, OUTLOOK_CALENDAR, MICROSOFT_TEAMS, POWER_BI])

seedScopeGroupSelection = (groups, priorSelectedIds) =>
   new Set([ ...groups.filter(g => g.required).map(g => g.id),
             ...(priorSelectedIds ?? []).filter(id => known(id)) ])   // then prune unmet dependencies
expandScopeGroupSelection = (groups, picked) => /* required + picked + transitive dependsOn */
```
The scope groups themselves come from `POST /api/connectors/list-connector-scope-groups`, and the
client's Zod schema for the response names every field (`grokjs/2c4yk92w1hb5e.js`):
```js
{ groups: [{ id, label, description, scopes: string[], required: boolean, dependsOn: string[] }],
  consentMessage, consentVersion, priorSelectedGroupIds }
```
— so the per-group scope strings are served to the client at runtime, just not baked into the bundle.
Four verified consequences:
1. The granular, user-visible scope-consent step exists **only for the Microsoft family** (plus Power
   BI). Google, Slack, Notion and the catalog connectors go straight to the provider's own OAuth screen
   with the server-chosen scope set.
2. **It is switched off in production right now.** The whole feature is gated on
   `grok_web_connector_scope_consent_enabled` (`function l(){ return !0 ===
   useFeatureStore.getState().getFeature("grok_web_connector_scope_consent_enabled") }`), and grok.com's
   inlined production payload carries `"grok_web_connector_scope_consent_enabled":false`. So today
   **every** connector, Microsoft included, goes straight to the provider consent screen with the
   server-chosen scope set — there is no xAI-side permission picker in front of it.
3. When it is on, **optional scope groups default to unselected** — the seed is required-groups-only
   plus anything the user previously picked. Non-required permissions are opt-in, not opt-out. Credit
   where due, but note it is latent, not live.
4. Groups carry `required` and `dependsOn`; picking a dependent group transitively pulls in its
   prerequisites on confirm, so the confirmed grant can exceed what the user visibly ticked.

The previous pass's grep conclusion is confirmed, with the greps named: across all **1,969** grok.com
chunks (`grokjs/` 84 + `grokjs2/` 1,885) I searched for `googleapis.com/auth/`,
`https://www.googleapis.com`, `drive.readonly`, `gmail.readonly`, `calendar.readonly`,
`offline_access`, `channels:history`, `Files.Read`, `Mail.Read`, `Calendars.Read`, `User.Read`,
`openid email profile` — **zero hits for all twelve**. The only literal provider scope strings in the
client are `Sites.Read.All` and `Sites.Selected`, as UI copy in the en i18n table
(`grokjs/376vlecp-jky0.js`). Scopes are minted server-side at `/rest/auth/create-oauth-connector` and
`getAuthUrl`. So the docs, not the bundle, are the source of record — which is why this item needed the
`docs.x.ai` route.

#### Supporting consent / retention copy, `verified`
From the official docs (per connector page, "Privacy and security"):
- Gmail / Google Calendar / Google Drive: *"**We do not train on your data.** SpaceXAI does not use
  your Gmail or Google Calendar data for model training."* and *"**Nothing is stored.** …Grok accesses
  your data in real time when you ask a question, and does not retain it afterward."*
- Outlook / OneDrive / Teams: *"These are delegated permissions. Grok can only access the mailbox of
  the signed-in user"* (resp. own OneDrive; resp. teams/channels/chats already joined).
From the shipped i18n table (`grokjs/376vlecp-jky0.js`):
- `syncing-connector.consent.no-training-*`: *"We never train on your data"* / *"xAI does not train on
  your {{name}} data."*
- Real-time, non-ingesting claims exist for **Gmail, Google Calendar, Outlook, Outlook Calendar and
  Power BI** only. **Google Drive, OneDrive, SharePoint, Slack and Notion carry no such claim**, and
  Drive has a separate `google-drive-sync` connector described as *"track and sync your Google Drive
  files"* — i.e. ingesting. SharePoint's doc confirms an indexing sync outright.
- `mcp-connectors.third-party-warning`: *"Third-party connectors are not built or maintained by xAI.
  Use caution when granting access to external services. Review the permissions before connecting."*

#### Three structural corrections to the brief's framing of this item
1. **The built-in set is seven connectors, and Slack is not one of them.** `docs.x.ai/grok/connectors`
   lists exactly: Gmail & Google Calendar, Google Drive, OneDrive, Outlook Mail & Calendar, Microsoft
   Teams, SharePoint, Salesforce. `verified`. Slack and Notion i18n strings *do* ship in the client
   (`syncing-connector.slack.*`, `syncing-connector.notion.*` in `grokjs/376vlecp-jky0.js`) — I read
   them there — but they are not in the official built-in table, which places them in the **connector
   catalog** instead. One third-party catalog maintainer goes further and says Slack is not available
   at all: *"Slack failed the two-surface test (absent from the picker and from the docs table) and is
   removed"* (`reported`, https://github.com/rdmgator12/awesome-grok-connectors ). Net: treat Slack as
   catalog-or-absent, not as a built-in with unresolved scopes.
2. **Catalog connectors cannot have xAI-defined scopes, by construction.** xAI classifies GitHub,
   Notion, Linear, Box, Canva, Vercel, Stripe, Figma and the rest as third-party-hosted MCP servers
   that xAI surfaces but does not build or maintain (`docs.x.ai/grok/connectors`, plus the
   `third-party-warning` string above). Their OAuth scopes are defined by each provider's own MCP
   endpoint — e.g. GitHub via `api.githubcopilot.com/mcp/x/all`, Notion via `mcp.notion.com/mcp`
   (`reported`, same catalog repo). So "the remaining scopes" is not one unresolved list but N
   provider-side lists. Adjust the audit's framing accordingly.
3. **There is a Google Workspace Marketplace listing, but it is a different product.** It is the
   Docs/Sheets/Slides add-on, not the grok.com Drive/Gmail connector OAuth client. Its declared
   permissions, verbatim from https://workspace.google.com/marketplace/app/grok/660927092109
   (`verified`): *"See, edit, create, and delete all your Google Docs documents · See, edit, create,
   and delete only the specific Google Drive files you use with this app · View and manage spreadsheets
   that this application has been installed in · See, edit, create, and delete all your Google Slides
   presentations · Display and run third-party web content in prompts and sidebars inside Google
   applications · Connect to an external service · See your primary Google Account email address · See
   your personal info, including any personal info you've made publicly available."* The raw
   `googleapis.com/auth/...` URIs behind those phrases are **`unresolved`** — I will not guess the
   mapping, and no Google admin-console app-access-control export for xAI's client was obtainable.
   **Do not file these under the grok.com connector scopes**; they are a separate grant surface.

#### Microsoft Entra enterprise app
`verified` that one exists and may require tenant admin consent — xAI's docs instruct: *"contact your
IT administrator and ask them to grant consent for the xAI Grok application in the Azure AD admin
portal under Enterprise applications."* The app's **client ID / object ID is `unresolved`** — no public
Entra gallery listing or admin-portal screenshot surfaced. SharePoint write access uses a **separate
Entra app registration** with its own consent, per the SharePoint doc quoted above.

**Confidence: high (verified) for every scope table above, for the Microsoft-only scope-consent gate,
for the optional-groups-default-off behaviour in code, and for that dialog being flagged off in
production.** Still `unresolved`: Slack, Notion, GitHub and the rest of the "connector catalog" have no
per-connector doc page and therefore no published scope list — blocked by the catalog being enumerated
only inside an authenticated `grok.com/connectors` session. A follow-up that would close it without
credentials is unavailable to me here: the per-group `scopes[]` array is returned by
`POST /api/connectors/list-connector-scope-groups`, which needs a session.

**What changes for a user:** connecting Outlook, OneDrive or Teams hands Grok write/send authority in a
single click with no read-only option; enabling Drive writes grants the full-Drive `drive` scope; and
SharePoint's recommended mode is tenant-wide read plus a background index that keeps its own grant.
The opt-in permission picker that would soften this exists in the code but is switched off, so right
now the provider's own consent screen is the only place a user sees what they are granting.


---

### Appendix — official-source quotes on retention, sharing and opt-out posture

Everything here is `verified` from an official xAI or X source. These are the quotes worth lifting into
the audit's retention and lineage sections; they also date the controls.

**30-day deletion, stated consistently since at least Nov 2024.**
- `x.ai/legal/faq`, archived 5 Nov 2024 (https://web.archive.org/web/20241105123923/https://x.ai/legal/faq ):
  *"If you delete conversations from your account, they will be removed from our systems **within 30
  days**, unless they have been de-identified and disassociated from your account or we have to retain
  them for safety, security or legal reasons."*
- `x.ai/legal/faq`, archived 14 Jun 2025 (https://web.archive.org/web/20250614022714/https://x.ai/legal/faq ):
  *"When using Private Chat, your conversation history will not be viewable to you and will be deleted
  from xAI systems **within 30 days**."*
- `x.ai/legal/faq`, archived 13 Sept 2026 (https://web.archive.org/web/20260913161312/https://x.ai/legal/faq ):
  *"After you indicate that you want your data deleted, it will take **up to 30 days** to delete from
  SpaceXAI systems."*
- `x.ai/legal/privacy-policy`, effective 24 Aug 2026 (archived
  https://web.archive.org/web/20261002172849/https://x.ai/legal/privacy-policy ): *"when Private Chat
  is turned on, conversations will not appear in your conversation history and your conversations will
  be deleted from SpaceXAI systems **within 30 days** unless it is necessary that they be kept longer
  for legal, compliance, or safety purposes. Further, if you choose to delete any or all of your
  conversations or if you choose to delete your account, we will delete the data **within 30 days**."*
- The grok.com UI says the same thing in-product (i18n `settings-data.deleted-conversations.description`):
  *"View and restore conversations that you have deleted. Deleted conversations are permanently removed
  after 30 days."*
- **Do not conflate with the API window.** `docs.x.ai/developers/faq/security`: *"By default, all API
  requests and responses are stored on our servers (encrypted at rest) for **30 days** for auditing
  purposes in the event of suspected abuse or misuse. SpaceXAI does not train on this data."* Same
  number, different control, and it has a documented off-switch (Zero Data Retention, team-admin
  self-serve, surfaced as an `x-zero-data-retention` response header).
- X-side, same window: `help.x.com/en/using-x/about-grok` (archived
  https://web.archive.org/web/20250509143914/https://help.x.com/en/using-x/about-grok ): *"Deleted
  conversations are removed from our systems **within 30 days**, unless we have to keep them for
  security or legal reasons."*

**The unauthenticated carve-out — an opt-out that does not exist outside the EU/UK.**
`x.ai/legal/faq`, archived 14 Jun 2025: *"If you do not log into your account to access Grok (i.e., you
are unauthenticated), where permissible, we may collect and retain your content on an anonymous basis.
As a result, **in some regions (excluding the EU/UK)**, when you use Grok without logging in, you won't
have the option to opt out of model training."* The consumer terms put it even more bluntly
(`x.ai/legal/terms-of-service`, last updated 11 Sept 2026): *"**Where available, you may access our
Service without logging in; when doing so, where permitted, you grant us full rights to use any data
you provide** to or obtain from our Service for product development and model training purposes."*
Note the direction of the carve-out: EU/UK users get *more* control here, not less.

**The toggle itself, per the consumer terms** (`x.ai/legal/terms-of-service`, 11 Sept 2026):
*"Electing whether your User Content is used for product development or model training. When logged
into our Service, **you can select** whether or not you want us to use your User Content to improve our
products and services and train our models. Private Chat and User Content that you request to be
deleted will be queued for deletion, which may take **up to 30 days**."*

**X's opt-out does not unlearn.** `help.x.com/en/using-x/about-grok` (archived
https://web.archive.org/web/20260507202711/https://help.x.com/en/using-x/about-grok ): *"when you use
an X feature that is powered by Grok (e.g. X recommendations), Grok will learn from your interactions
and **the opt-out does not prevent a deployed model from learning** as a result of its normal use."*
That sentence deserves its own line in the audit — it materially narrows what the item-3 toggle buys.

**Naming note for the audit's front matter:** xAI now brands itself **"SpaceXAI"** on x.ai and in
`docs.x.ai` (same entity, same legal documents), and the X-side corporate entity was renamed from
Twitter International Unlimited Company (TIUC) to **X Internet Unlimited Company (XIUC)** on
1 April 2025. `x.ai/legal/consumer-terms-of-service` has never been archived and 404s today — the
consumer terms live at `x.ai/legal/terms-of-service`.

**Fetching note for anyone reproducing this:** `x.ai/*` and `help.x.com/*` 403 direct automated
fetches, but both render through a text-extraction proxy (`r.jina.ai`), and `web.archive.org` responds
to `curl` with the `id_` raw-content suffix even where the fetch tool is blocked. `docs.x.ai` needs no
workaround at all. `forbes.com`, `pcmag.com`, `theverge.com` and `cnet.com` block the fetch tool but
respond to `curl`.

---

### Status summary

| # | Item | Resolved default | Label |
|---|---|---|---|
| 1 | Allow chat link sharing (grok.com) | **ON**, all regions incl. EEA/UK and enterprise | verified (code, two places) + reported screenshot |
| 2 | Improve the Model (grok.com) | **ON** outside EEA/UK; **OFF** in EEA/UK and enterprise; row hidden for enterprise/gov | verified (code + xAI EU addendum) + corroborated reported |
| 3a | X training toggle `allow_xai_data_sharing` | **ON** | **verified** (Swiss FDPIC regulator doc + X help-page opt-out framing) + corroborated reported |
| 3b | …does it ship OFF for EU/EEA? | **NO** — same default-on toggle; the 2024 Irish remedy was a dataset-specific deletion, not a default change | verified (undertaking text, DPC releases, X privacy policy, xAI FAQ) + corroborated reported; first-hand EEA observation unresolved |
| 4 | Personalize with conversation history (grok.com) | **ON** outside EEA/UK; **OFF** in EEA/UK and enterprise; row rendered | verified (code + prod flag) + corroborated reported (TechCrunch EU/UK exclusion, CNET default-on) |
| 5 | Personalize using 𝕏 (grok.com) | **ON** outside EEA/UK; **OFF** in EEA/UK and enterprise | verified (code + xAI's own screenshot) |
| 6 | Device location (grok.com) | **OFF**; row not rendered (prod flag `false`) | verified (code + prod flag); third-party corroboration unresolved (nobody covers it) |
| 7 | Allow Grok to remember history (X) | **row hidden** in the observable bucket (`grok_settings_memory_visibility:"hide"`); where visible, reported ON | verified (prod flag) / reported (one outlet) — default **unresolved** |
| 8 | Allow X to personalize with Grok (X) | documented only as an opt-out; reported ON | verified (official framing + ship date Jan 2025) / reported (one outlet) — default **unresolved** |
| 9 | Watermark Imagine generations (grok.com) | preference **`false`**, row hidden — **but xAI docs say output is watermarked with no way to remove it**. Contradiction unresolved; do not publish "off by default" | verified (all three facts) / unresolved (what it changes) |
| 10 | Block modifications by Grok (X) | **OFF**, per-image, no retroactive application. Path: composer → image thumbnail **paintbrush** → **flag** icon → **Sensitive media** / content settings. Row live (prod flag `true`). Shipped 8 Mar 2026, never announced | verified (code, both editor paths + prod flag) + corroborated reported (Social Media Today → The Verge → PCMag) |
| 11a | Team Product sharing | **Conversations = Organization, Projects = Organization, Skills = Private**; Public available for conversations only | verified (official xAI docs + code) |
| 11b | Team Conversation retention | `Retain indefinitely` is **not** the client's state; client fallback is Custom / 15 days (range 15–1825) | verified (client fallback); server default **unresolved** |
| 12 | Connector OAuth scopes | **Full tables sourced** for all seven built-ins (Gmail, Google Calendar, Drive, OneDrive, Outlook Mail/Calendar, Teams, SharePoint incl. a second indexing-sync set, Salesforce). xAI's own scope-consent picker is flagged **off** in production | verified (official docs + code); catalog-connector scopes unresolved by construction |

#### Still open, and what would close each
- **Items 7 and 8** — the server-side stored default for `allow_grok_memory` and
  `allow_xai_personalization`. Both rest on a single outlet's July 2026 hands-on. Closing them needs an
  authenticated X session on a brand-new account (read `user_preferences` before touching anything), a
  second independent hands-on walkthrough, or an official X statement. Item 7 additionally needs an
  account in a cohort where `grok_settings_memory_visibility` is not `"hide"`.
- **Item 3b** — a first-hand observation of the checkbox on a newly created EEA/EU account. Proven
  absent from both clients, so it is purely a server-side question. No regulator document states it;
  the DPC's April 2025 inquiry into *ongoing* EU/EEA training is still open with no decision, and the
  EU AI Act record is empty on this point.
- **Item 9** — what the `watermarkImagineGenerations` preference actually changes given that
  `docs.x.ai/grok/faq` says the watermark cannot be removed; and whether
  `enable_watermark_setting` is delivered to authenticated Imagine users.
- **Item 11b** — the shipped server value for `conversationsRetentionPeriodDisabled` /
  `conversationsRetentionPeriodDays` on a newly provisioned team. Not documented anywhere on
  `docs.x.ai` (all 185 pages searched); needs an authenticated team-settings response.
- **Item 12** — per-provider scopes for catalog connectors (GitHub, Notion, Linear, Box, Canva, …),
  which are defined by each third party's own MCP endpoint rather than by xAI; the raw
  `googleapis.com/auth/...` URIs behind the Google Workspace Marketplace add-on's permission phrases;
  and the Microsoft Entra app's client/object ID. The grok.com-side list is served at runtime by
  `POST /api/connectors/list-connector-scope-groups` (`scopes[]` per group), which requires a session.
- **Item 10** — the current platform matrix (The Verge said iOS-only in March 2026, PCMag said web +
  iOS and no Android in July 2026). My own evidence is web-only.
- **Unattributed but suggestive**, flagged rather than used: the DPC AI Insights Report (Sept 2026,
  p. 36) describes an unnamed controller whose *"opt out for processing personal data for AI training
  for a particular chatbot was not available to non-subscribers using mobile devices"*, affecting
  ~7.7 million EEA mobile users, identified Jan 2025 and fixed by Feb 2025, with the controller
  committing not to train on data collected during the gap. It fits X/Grok — Grok was open to all users
  and the opt-out was long web-only — but the report does not name it, so it must stay unattributed.
