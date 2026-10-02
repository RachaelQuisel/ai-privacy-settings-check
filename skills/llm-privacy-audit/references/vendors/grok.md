# Grok (xAI / SpaceXAI)

> **Last verified:** 2026-10-02
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
- **Default:** **ON.** Officially unstated. xAI's Consumer FAQ says only "You control whether your data is used for training Grok" and never names the default; @grok's own public instructions and all contemporaneous reporting describe it as on-by-default (opt-out).
- **Exposes:** Every prompt, uploaded file, image, document and voice input you send, plus Grok's responses, is retained against your account and used by SpaceXAI to train and fine-tune its models, with a limited number of authorized personnel able to read conversations.
- **Recommend:** **OFF.** The only account-level switch that stops your chat content entering the training corpus. Turning it off is forward-only and does not retract anything already ingested.
- **Risk:** High
- **Evidence:** label/path verified live at `cdn.grok.com/_next/static/chunks/376vlecp-jky0.js` (key `settings-data.improve-model.title`); FAQ at `web.archive.org/web/20260928235916/https://x.ai/legal/faq` — checked 2026-10-02
- **Confidence:** label/path `verified`; default `reported`

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
- **Default:** **ON for existing accounts** — enabled retroactively in July 2024 without prior consent. X has never published the default in its own help text. Treat as on-by-default and verify in your own account.
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

**Live connector inventory** (verified from grok.com's own string table): Gmail, Google Calendar, Google Drive, Google Drive (sync), OneDrive, Outlook, Outlook Calendar, SharePoint, SharePoint Direct, Slack, Notion, Power BI, X Ads. Live flags show Google Drive/Gmail/Calendar/OneDrive **enabled**, GitHub and Notion **disabled** for consumer web at time of check.

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
- **Default:** **Not found.** No OAuth scope identifiers appear in any grok.com client bundle — all 84 chunks were grepped for `googleapis.com/auth/*` and Microsoft Graph scope names with **zero hits**; scopes are requested server-side. No xAI doc enumerates them.
- **Recommend:** Read the provider's own consent screen; it is the authoritative scope list.
- **Confidence:** `unresolved` — the requested scopes for every connector could not be confirmed

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
- **Default:** **Unresolved.** The feature is live (`show_auto_share_settings: true`, `enable_temp_always_request_share_link: true`) but the shipped state could not be determined, and **no xAI doc mentions this setting at all.** ⚠️ **This is the one to check first in your own account** — a default-on "share using only your chat link" materially lowers the bar to exposure.
- **Exposes:** If on, a chat becomes viewable from its link without the explicit per-conversation share step.
- **Recommend:** OFF. Keep sharing an explicit, per-conversation act.
- **Risk:** High
- **Confidence:** label `verified`; default `unresolved`

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
- **Recommend:** Env vars or a secret manager, never shared between teammates, rotate regularly.
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
