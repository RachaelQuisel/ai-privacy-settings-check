# Google Gemini

> **Last verified:** 2026-10-02
> **Surfaces covered:** Gemini app (web/Android/iOS) · Gemini Apps Activity · AI Overviews & AI Mode in Search · Gemini in Workspace · Gemini in Chrome · Gemini Spark · Gemini Notebook · Google AI Studio / Gemini Developer API · Vertex AI (now "Gemini Enterprise Agent Platform") · Gemini CLI & Code Assist

## Orientation — three structural facts

1. **There are at least three separate activity buckets**: `Keep Activity` (Gemini Apps), `Web & App Activity` (Search, AI Overviews, AI Mode), and `Search Services History`. Hardening one does nothing for the others.
2. **Turning off `Keep Activity` is not a kill switch.** Four retention paths survive it (§5), and on Android four connectors bypass it entirely (§3).
3. **Consumer Gemini and Workspace Gemini are materially different products** on human review, training, and link sharing. Never generalize one onto the other.

## 1. Training on your data (incl. human review)

- **Setting:** `Keep Activity`
- **Where:** gemini.google.com → Menu → Settings & help → Activity; or mobile app → Menu → profile picture → Gemini Apps Activity. https://myactivity.google.com/product/gemini
- **Default:** **ON** for consumer accounts. Verbatim: *"If you're aged 18 or over, Keep activity is on by default."* Workspace: also ON by default but **admin-controlled** — *"Keep Activity is on by default and can only be turned off by your account's Workspace administrator."*
- **Exposes:** Every prompt, response, uploaded file, image, video, screen share, Gemini Live transcript, plus "info from websites you visit with Gemini, product usage, and location info" is saved and used "to provide, develop, and improve its services (including training generative AI models)."
- **Recommend:** **OFF** for consumer accounts — the only consumer control that stops model training. **Set auto-delete to 3 months first**, since turning it off is not retroactive.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13278892 ; https://support.google.com/gemini/answer/13594961 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Human review of conversations — **no setting exists; there is no opt-out**
- **Where:** Documented only in the Gemini Apps Privacy Hub, under "Who has access to my chats…"
- **Default:** Active whenever `Keep Activity` is ON. Verbatim: *"A subset of chats are reviewed by human reviewers (including Google's trained service providers) to help improve Google services."* Chats are *"disconnected from your account before being sent to service providers"* — **account-level de-identification only, not content redaction.** Workspace is different: *"Your chats and uploaded files in Gemini Apps won't be reviewed by human reviewers or otherwise used to improve generative AI models."*
- **Exposes:** A sample of your conversations — including attached files and screenshots — is read and annotated by Google staff and third-party contractors, and survives your own deletion by up to three years (§5).
- **Recommend:** Assume anything typed into consumer Gemini at default may be read by a human contractor. Use a Workspace account for client work. Google's own warning: *"Please don't enter confidential information that you wouldn't want a reviewer to see."*
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961 ; https://support.google.com/gemini/answer/14620100 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Uploaded files and photos sampled for training *(governed by `Keep Activity`; no separate toggle)*
- **Default:** **ON** via Keep Activity, applying to uploads submitted from **2025-09-02** onward. Verbatim: *"a sample of your future uploads will be used to help improve Google services for everyone."*
- **Exposes:** A sample of the documents, images and photos you upload leaves the inference path and enters Google's service-improvement corpus.
- **Recommend:** Turn `Keep Activity` off, or use Temporary Chat, before uploading anything you did not author or do not own.
- **Risk:** High
- **Evidence:** https://blog.google/products/gemini/temporary-chats-privacy-controls/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Feedback submission (thumbs up/down) — **no toggle; it is a consent action**
- **Where:** Thumbs icons beneath any Gemini response
- **Default:** Submitting feedback collects *"your feedback, context that can help us better understand your feedback, including the last 24 hours of your chats, and any content included in those chats,"* which is *"reviewed by specially trained teams"* and retained **up to 3 years**.
- **Exposes:** One thumbs-down sends your **last 24 hours of conversation** into the human-review and 3-year-retention path — **even if `Keep Activity` is off and even in a Temporary Chat**, because the privacy notice carves out *"unless you choose to send Google feedback."*
- **Recommend:** Never submit feedback from a session containing client or personal data. **The single most under-advertised data path in the product.**
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Improve Google services with your audio and Gemini Live videos & screenshares`
- **Where:** https://myactivity.google.com/product/gemini → checkbox beneath `Keep Activity` → Turn on
- **Default:** **OFF** (opt-in). Verbatim: *"Your Gemini Live audio, video and screenshares are not used to improve Google services by default."* Requires `Keep Activity` ON to enable.
- **Exposes:** At default, nothing. **But the transcript carve-out is the trap:** *"if Keep Activity is on, transcripts of your Live chats are used to improve Google services, including AI models."* The raw media is spared; the words are not.
- **Recommend:** Leave off — and understand it does not keep Gemini Live out of training. Only `Keep Activity` off or Temporary Chat does that.
- **Risk:** High if enabled; Medium at default *(because of the transcript gap)*
- **Evidence:** https://support.google.com/gemini/answer/13594961#audio_live — checked 2026-10-02
- **Confidence:** `verified` (default, behavior); `reported` (exact toggle string — Google renders it as a question heading; third-party sources render it variously)

- **Setting:** Imported memory/chats from other AI platforms — **no separate toggle**
- **Default:** Imported data is treated as your own activity. Verbatim: *"Data (memory and chats) that you import from other AI platforms is saved in your Activity. This data is used consistently with your Gemini Apps activity, including to improve our services (including training generative AI models)."*
- **Exposes:** Importing a ChatGPT or Claude history into Gemini puts that entire backlog into Google's training corpus.
- **Recommend:** Do not import histories from other assistants unless you are content for all of it to train Google's models.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Ads use of Gemini chats — **no setting; a stated commitment**
- **Default:** Not used. Verbatim: *"Your Gemini Apps chats are not being used to show you ads. If this changes, we will clearly communicate it to you."* **Exception:** Google Shopping cart activity from Gemini *"is saved to your Google Wallet"* and used per Wallet settings *"including for personalization and ads."*
- **Recommend:** Treat the chat commitment as reliable; avoid Gemini's shopping-cart and Google Pay flows if you don't want that signal in your ads profile.
- **Risk:** Low (chats) / Medium (shopping)
- **Evidence:** https://support.google.com/gemini/answer/13594961 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Signed-out use of Gemini
- **Default:** Verbatim: *"Your data is not associated with your Google account. The Gemini Apps Privacy Notice does not apply."* Processing falls under the general Google Privacy Policy instead.
- **Exposes:** Not tied to your account — but **also not covered by the Gemini-specific retention and review commitments**, so handling is *less* specified, not more protective.
- **Recommend:** Reasonable for one-off sensitive queries, but do not assume zero retention.
- **Risk:** Medium
- **Confidence:** `verified`

## 2. Memory, history & personalization

- **Setting:** `Personal Intelligence` *(replaced the earlier "Personal context")*
- **Where:** Mobile: Menu → profile picture → Personal Intelligence. Web: Menu → Settings & help → Personal Intelligence. https://gemini.google.com/personalization-settings
- **Default:** **ON.** Verbatim: *"If you start a new chat, Personal Intelligence is on by default."* Requires 18+, a personal Google Account, and `Keep Activity` ON.
- **Exposes:** Gemini draws on your chat history plus whatever Connected Apps are attached to shape every response.
- **Recommend:** Off unless you specifically want cross-session personalization; it is the umbrella that makes Memory and Connected Apps act on each other.
- **Risk:** Medium
- **Evidence:** https://support.google.com/gemini/answer/16598406 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Memory` *(web toggle also labelled "Your past chats with Gemini")*
- **Where:** Menu → profile picture → Personal Intelligence → Memory
- **Default:** **ON.** Google's launch announcement states *"This setting is on by default"* for past-chats personalization. The current help page does **not** restate the default. Requires `Keep Activity` ON.
- **Exposes:** Gemini mines prior conversations for "key details and preferences" and carries them forward, so a detail disclosed once resurfaces in unrelated later chats.
- **Recommend:** Off. **Turning it off does not erase what was already learned** — you must also delete the underlying chats at https://myactivity.google.com/product/gemini
- **Risk:** Medium
- **Evidence:** https://blog.google/products/gemini/temporary-chats-privacy-controls/ ; https://support.google.com/gemini/answer/16598469 — checked 2026-10-02
- **Confidence:** `verified` (launch default, dependency); `reported` (that it is still ON after the Personal Intelligence rebrand — the current page is silent)

- **Setting:** `Instructions for Gemini` *(rendered as "Saved info" in some locales)*
- **Where:** https://gemini.google.com/saved-info
- **Default:** **`unresolved`** — Google states only that *"This data remains saved until you choose to delete it."*
- **Exposes:** Standing instructions and facts persist indefinitely across all chats and are used to complete scheduled actions.
- **Recommend:** Audit this page directly; anything here is permanent until manually removed and is **not** covered by the 18-month auto-delete clock.
- **Risk:** Medium
- **Confidence:** `verified` (label, URL, persistence) / `unresolved` (default)

- **Setting:** `Temporary Chat`
- **Where:** New-chat control (dashed chat-bubble icon, top right)
- **Default:** Off — opt-in per conversation.
- **Exposes:** Verbatim: *"Temporary Chats won't appear in your recent chats or Gemini Apps Activity, and they won't be used to personalize your Gemini experience or train Google's AI models. They are kept for up to 72 hours."*
- **Recommend:** **Make this the default habit for anything client-confidential.** The strongest consumer privacy lever available — but the 72-hour floor and the feedback carve-out still apply.
- **Risk:** Low
- **Evidence:** https://blog.google/products/gemini/temporary-chats-privacy-controls/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Web & App Activity` — and its sub-checkbox `Include Chrome history and activity from sites, apps, and devices that use Google services`
- **Where:** https://myactivity.google.com/activitycontrols ; Google Account → Data & privacy → History settings
- **Default:** **`unresolved` for both.** No Google page states a default. Widely reported as ON with 18-month auto-delete for new accounts, but **this could not be verified in official docs — do not assert it.**
- **Exposes:** **A completely separate bucket from Gemini.** Search, AI Overviews and AI Mode queries land here, not in Gemini Apps Activity. Google states the only way to stop Search queries feeding generative-AI models is: *"you can turn off Web & App Activity in My Activity."* The sub-checkbox widens the corpus to Chrome browsing history and cross-device activity.
- **Recommend:** **Harden this independently of Gemini.** Turning off `Keep Activity` does nothing here. Uncheck the Chrome-history sub-option even if you keep the parent on.
- **Risk:** High
- **Evidence:** https://support.google.com/websearch/answer/54068 ; https://support.google.com/websearch/answer/14901683 — checked 2026-10-02
- **Confidence:** `verified` (labels, path, the Gemini/Search split, Google's stated opt-out mechanism) / `unresolved` (defaults)

- **Setting:** `Personal Intelligence` in AI Mode *(draws on `Search Services History`)*
- **Default:** **`unresolved`.** Requires 18+ in the US. Verbatim: *"Personal Intelligence in AI Mode references previous searches and activity saved in your Search Services History…"*
- **Exposes:** Your Search history becomes a personalization corpus for AI Mode answers. Note `Search Services History` is a **third distinct label**, with no locatable settings page.
- **Recommend:** Turn off Web & App Activity, which starves it — there is no documented direct off switch.
- **Risk:** Medium
- **Evidence:** https://support.google.com/websearch/answer/16011537 — checked 2026-10-02
- **Confidence:** `verified` (quote, dependencies) / `unresolved` (own default and settings path)

- **Setting:** Location collection by Gemini Apps — **no off switch for coarse location**
- **Where:** Precise location: Android Settings → Location → App location permissions → Google app + `Use precise location`; iOS Settings → Google
- **Default:** Verbatim: *"Location data is always collected if you use Gemini Apps so that they can provide you with a response that is relevant to your query."* Coarsened before storage: *"A general area is larger than 3 sq kilometers, and has at least 1000 users."*
- **Exposes:** Every Gemini query carries a general-area location signal you cannot disable. **And there is a documented bypass:** *"Gemini may receive your precise location data from another Google service, like Android Auto, to fulfill your request even if the precise location settings above are off."*
- **Recommend:** Deny precise location at the OS level and set access to "while using the app" — but accept that coarse location is unavoidable and precise location can leak via sibling Google services.
- **Risk:** Medium
- **Evidence:** https://support.google.com/gemini/answer/13594961#location — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Scheduled actions`
- **Where:** Gemini app → Settings & help → Scheduled actions
- **Default:** None active until created; max 10 concurrent. Requires `Keep Activity` ON.
- **Exposes:** Gemini runs queries while you are absent, and **pins the location**: it "will use the location where you created the action for all future responses."
- **Recommend:** Avoid — using it **forces `Keep Activity` on**, which re-enables training and human review for everything else too.
- **Risk:** Medium
- **Evidence:** https://support.google.com/gemini/answer/16316416 — checked 2026-10-02
- **Confidence:** `verified`

## 3. Connectors & OAuth scopes

- **Setting:** `Connected Apps` *(formerly Gemini Extensions, then Apps)*
- **Where:** Menu → profile picture → Personal Intelligence → Connected Apps. https://gemini.google.com/apps
- **Default:** For the Google-app group, **opt-in** — setup presents `Connect all` / `Choose apps` / `Don't connect`, and prior Workspace/Photos connections were **reset**: *"If you've previously connected the Google Workspace app or the Google Photos app, your settings have been reset with the launch of Personal Intelligence with Connected Apps."* Per-toggle defaults are **not stated**.
- **Exposes:** Per Google: *"saved data from Search services and YouTube, emails, files, events, photos, videos, info about your contacts (such as phone numbers, addresses, and birthdays), info from Google Wallet (like payment methods… and financial account info linked with services such as Plaid), and location info."*
- **Recommend:** `Don't connect`, then add individually only what you actively need. **Gmail and Drive are the two that convert Gemini from a chat tool into a corpus reader.**
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/16836988 ; https://support.google.com/gemini/answer/13695044 — checked 2026-10-02
- **Confidence:** `verified` (labels, opt-in card, reset, data scope) / `unresolved` (per-toggle default states)

Group labels, verbatim: `Google Workspace` (Gmail, Calendar, Drive, Docs, Sheets, Slides, Keep, Tasks, Chat, Meet) · `Google Search services` (Search incl. AI Mode and Discover, Maps, Shopping, Flights, Hotels, Translate, News) · `Contacts` (US/English only, **requires AI Ultra**) · `Google Wallet` · `Google Photos` · `YouTube`.

- **Setting:** `Device assistance`, `Phone`, `Messages`, `WhatsApp` (Android) — **the Keep-Activity bypass**
- **Where:** https://gemini.google.com/apps → disconnect each individually
- **Default:** Connected on Android. `Device assistance` (renamed from Utilities) is *"Designed to work automatically with Gemini on Android, even if Keep Activity is off."* Verbatim: *"When Keep Activity is off, Connected Apps won't be available on gemini.google.com, iOS devices, or smart watches. On Android devices, only the Device assistance, Phone, Messages, and WhatsApp apps will be available if the setting is off."* Effective **2025-07-07**, announced by email: Gemini would use these *"whether your Gemini Apps Activity is on or off."*
- **Exposes:** On Android, turning off `Keep Activity` does **not** stop Gemini from reading and acting on your calls, SMS and WhatsApp content — and those conversations still sit in your Google Account for 72 hours.
- **Recommend:** Disconnect all four explicitly. **This is the most important single correction to the common belief that `Keep Activity` off is a kill switch.** iOS is not affected — the carve-out is Android-only.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13695044 ; https://support.google.com/gemini/answer/15235441 — checked 2026-10-02
- **Confidence:** `verified` (current policy text) / `reported` (that they ship connected-by-default rather than requiring a first-run grant)

- **Setting:** Third-party Connected Apps, including custom **MCP servers**
- **Where:** https://gemini.google.com/apps ; roster at https://support.google.com/gemini/table/17434654
- **Default:** Not connected until you authorize.
- **Exposes:** Google explicitly disclaims responsibility: *"Before connecting a custom third-party Model Context Protocol (MCP) server… make sure you trust that third-party and understand the supported actions. **Google does not control, monitor, or secure these servers.**"* And: *"Choosing to connect them may expose your data, passwords, devices, and accounts to unauthorized access."* Third parties *"process your data according to their own privacy policies"* — **Google's no-ads and review commitments do not travel with it.**
- **Recommend:** Treat every third-party connector and MCP server as a full data egress outside all of Google's commitments. Connect none you would not sign a DPA with.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961#connected_apps — checked 2026-10-02
- **Confidence:** `verified`

Current third-party roster (abridged): Adobe, Canva, Picsart, Squarespace, Webflow, Wix, Experian, Peloton, Zocdoc, Apartments.com, Angi, Thumbtack, iHeartRadio, Pandora, Spotify, Samsung Gallery, YouTube Music, Airtable, Dropbox, GitHub, Google Ads, Google Business Profile, Google Classroom, Granola, Linear, Monday.com, Otter.ai, PandaDoc, Wispr AI, Zoho suite, Bandsintown, Fever, GetYourGuide, SeatGeek, Ticketmaster, Viator, plus OEM note/calendar apps. *(Google Maps and YouTube were removed as standalone apps 2025-10-18 and folded into the always-on public-data path.)*

- **Setting:** Google Photos — `Gemini features in Photos` and query donation
- **Where:** Google Photos → Settings → Preferences → Gemini features in Photos
- **Default:** **`unresolved`** for the feature toggle. Query review appears **on** by default — the page says users *"may turn off query review in settings."*
- **Exposes:** Your Ask Photos queries are reviewed. Google's counter-commitment: *"We don't train any generative AI models outside of Google Photos with your personal data in Google Photos."*
- **Recommend:** Turn off query donation. **The Photos commitment is narrower than it reads — it only excludes training *outside* Google Photos.**
- **Risk:** Medium
- **Evidence:** https://support.google.com/photos/answer/15344015 — checked 2026-10-02
- **Confidence:** `verified` (quotes, scope) / `unresolved` (defaults)

## 4. Sharing & publication defaults

- **Setting:** `Share conversation` *(reads "Share conversation and Gem instructions" when a Gem was used)*
- **Where:** Beneath any Gemini response → Share. Link format `g.co/gemini/share/<id>` (verified 302 → `gemini.google.com/share`)
- **Default:** Consumer: available, but **no link exists until you create one**. Workspace: public-link sharing is **OFF by default** (§8).
- **Exposes:** **The entire conversation, not the one response.** Verbatim: *"If you create a public link to share a chat, you share the entire conversation"*; *"Anyone with the link can read the chat, even if you didn't share the link with them directly."* Recipients can **reshare** and **continue the chat**. Includes *"AI-generated artifacts from the conversation, including Canvas documents, images, and videos."* Your name and account are not included.
- **Recommend:** Treat every share link as permanently public and resharable. Screenshot instead where possible.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13743730 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Search-engine indexing of shared chats — **no setting; implementation behavior**
- **Default:** **Shared Gemini chats are correctly `noindex`'d.** Verified by direct HTTP inspection, not reporting: `gemini.google.com/robots.txt` contains only `Disallow: /app/` and `Disallow: /chat/` — **`/share/` is deliberately crawlable** — and a `/share/` page serves `<meta name="robots" content="noindex, nofollow">`. **Crawl-allowed + noindex is the correct combination, and is precisely what ChatGPT (Aug 2025) and Claude got wrong.** Gemini had the inverse misconfiguration in Feb 2024 (`Disallow: /share/` blocked Googlebot from ever seeing the noindex, so URLs got indexed from external links); fixed ~2026-02-27.
- **Exposes:** Search engines will not surface shared chats. **But** noindex does not stop a recipient resharing, screenshotting, or archive/scraper services, and Google's help page makes **no documented commitment** about indexing — implementation-only, could change without notice.
- **Recommend:** Rely on it for search engines; **do not rely on it as a confidentiality control.**
- **Risk:** Low *(indexing specifically)* / High *(the underlying anyone-with-URL exposure)*
- **Evidence:** raw `curl` of `gemini.google.com/robots.txt` and `/share/0000000000`, executed 2026-10-02 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Your public links` / `Delete public link`
- **Where:** Gemini → Settings and Help → Your public links. https://gemini.google.com/sharing (verified HTTP 200)
- **Default:** Empty until you create a link.
- **Exposes:** Lists every live public link. Deletion shows visitors *"a message that the chat no longer exists"* — but does **not** remove third-party copies, and does **not** delete the chat from the activity of anyone who continued it.
- **Recommend:** Audit quarterly and purge. **Deletion is forward-looking only.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Uploaded files in a shared conversation — **no setting; always included**
- **Default:** Included and **downloadable**. Verbatim: *"If you upload an image to a chat and then share the chat, the image is available and downloadable from the shared chat."*
- **Exposes:** Sharing a conversation hands over the source files, not just the text about them.
- **Recommend:** Never share a conversation containing an uploaded client file.
- **Risk:** High
- **Confidence:** `verified` for images; `reported` for PDFs/docs/video — Google names only images; assume the same but it is unstated

- **Setting:** Gem sharing — roles `Viewer` / `Editor`
- **Where:** gemini.google.com → Gems manager (https://gemini.google.com/gems/view) → Gem → Share. **Web only.**
- **Default:** **`Private: Only people with access can open the Gem`.** Can be widened to `Anyone with the link`, `Your organization`, or `Public`.
- **Exposes:** Verbatim: ***"Any Gem instructions and files that you have uploaded to the Gem can be viewed by any user with access to the Gem."*** Google's warning: *"If you have uploaded files to a Gem, don't share the Gem with anyone who you don't want to view the files."* Editors can reshare, edit, and **delete** the Gem. Shared Gems *"are stored and shared in Google Drive, so the sharing settings for Drive also apply."*
- **Recommend:** **Never put proprietary prompt IP or client files in a Gem you intend to share.** Share as Viewer only.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/16504957 — checked 2026-10-02
- **Confidence:** `verified` (default Private; instructions + files exposed) / `unresolved` (a third-party source claims Viewers specifically cannot see knowledge attachments, contradicting Google's text — trust Google, but worth a UI test)

- **Setting:** Canvas web app public links — **the worst default in this category**
- **Where:** Shared through Share → Share conversation; managed at https://gemini.google.com/sharing
- **Default:** No link until created — but once created, verbatim: ***"Anyone with the public link can also view and edit data saved with the app."*** And: *"When you interact with user-generated Canvas apps, anyone with the public link can see any data you share."*
- **Exposes:** A published Canvas app is **not a static page — it has a shared, writable data store.** Anyone with the URL can read *and modify* whatever anyone else entered. A Canvas app used as a form, tracker or intake tool is effectively a public read-write database. *"You cannot delete shared data once provided to app creators."* Canvas content is **not** used to train Google's models.
- **Recommend:** **Never collect real data in a shared Canvas app.** Demo surface only.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961#canvas_data — checked 2026-10-02
- **Confidence:** `verified` (the exposure) / `unresolved` (publish-flow UI labels, and whether published Canvas apps sit on a `noindex`'d path — probing `/canvas`, `/apps/*`, `/share/canvas/*` found no robots meta, so those are not the real paths)

- **Setting:** Sharing AI Overviews / AI Mode responses from Search
- **Where:** Beneath any AI response → Share. Management: AI Mode history → menu → Manage public links (desktop)
- **Default:** No link until created. Requires history and personalized recommendations enabled to share at all.
- **Exposes:** Verbatim: ***"all of your questions and responses within the same thread will be shared"*** — the whole multi-turn thread, not the single answer you clicked Share on. Clicking a shared AI Overview link *"will take you to AI Mode to continue the conversation."* Deletion: *"the shared content will be deleted within minutes."*
- **Recommend:** Assume the full thread leaks; share a screenshot instead. **The whole-thread behavior is not evident from the UI.**
- **Risk:** High
- **Evidence:** https://support.google.com/websearch/answer/16517651 — checked 2026-10-02
- **Confidence:** `verified` (thread-wide exposure, deletion timing) / `unresolved` (indexing status — the noindex finding covers `gemini.google.com/share/` only)

## 5. Retention & deletion

**The core correction — turning off `Keep Activity` does NOT stop all retention.** Four distinct paths survive it.

- **Setting:** The 72-hour floor — **no setting; unavoidable**
- **Default:** Verbatim: *"Temporary chats and chats you have when Keep Activity is off are retained with your account for 72 hours and used to: respond to you, using the last 24 hours of your chat as context, and protect Google, our users, and the public."* And: *"This activity won't appear in your Gemini Apps Activity."*
- **Exposes:** With `Keep Activity` off, your chats still sit in your Google Account for 72 hours in a store **you cannot see, audit, or delete.** **Nothing in Gemini is zero-retention.**
- **Recommend:** Accept the floor; it is the irreducible minimum. There is no Gemini configuration that achieves zero retention.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Human review during the 72-hour window — **no setting; no opt-out**
- **Default:** Verbatim: ***"Even if your Keep Activity setting is off or you use temporary chats, Google still uses your chats to respond to you and help protect Google, our users, and the public, including with help from human reviewers."***
- **Exposes:** Human reviewers retain a path to your chats **even with `Keep Activity` off and even in Temporary Chats** — scoped to safety/abuse rather than quality improvement, but the same human-access channel. This is narrower than the broad quality-review path, which Google's 2025 statement said stops when activity is off: *"With Gemini Apps Activity turned off, their Gemini chats are not being reviewed or used to improve our AI models."* **Both statements are accurate at their respective scopes** — model-improvement review stops; protection review does not.
- **Recommend:** Do not treat `Keep Activity` off as "no human will ever see this." Treat it as **"no human will see this *to improve the model*."**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** The 3-year human-review retention — **no setting; survives your deletion**
- **Default:** Verbatim: ***"Chats reviewed by human reviewers (and related data like your language, device type, location info, or feedback) are not deleted when you delete your activity. Instead, they are retained for up to three years."*** Feedback data: *"retained for up to 3 years."*
- **Exposes:** Once a conversation enters human review, deleting your activity does nothing to it. It persists up to three years, de-identified at the account level but **not content-redacted** — so names, client details and uploaded file contents inside the chat body remain.
- **Recommend:** **This is the retention path that cannot be undone.** The only mitigations are prevention: `Keep Activity` off, Temporary Chats, never submitting feedback, or a Workspace account where human review does not apply.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Auto-delete` period for Gemini Apps Activity
- **Where:** https://myactivity.google.com/product/gemini → auto-delete control
- **Default:** **18 months.** Verbatim: *"By default, your Gemini Apps activity older than 18 months is auto-deleted."* Options: 3 months / 18 months / 36 months / Don't auto-delete. Workspace: admin-set, same windows, default 18 months; *"If your administrator turns on Gemini history retention, you won't be able to change your activity settings."*
- **Recommend:** Set to **3 months** (the floor) *before* turning `Keep Activity` off — turning it off is not retroactive and leaves the backlog on the old clock.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Extended retention for legal/security purposes — **no setting**
- **Default:** Verbatim: *"We retain some data for longer when necessary for legitimate business or legal purposes…"* Also: *"We keep some data until you delete your Google Account, such as information about how often you use Gemini Apps."*
- **Exposes:** An unbounded override on every window above. Usage metadata persists until account deletion.
- **Recommend:** Treat all stated retention windows as ceilings on the *normal* path, not guarantees.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `AI Mode history` deletion
- **Where:** AI Mode → AI Mode history → More → Delete / Delete all. In My Activity it appears under **Search**: https://myactivity.google.com/product/search
- **Default:** Retained per Web & App Activity, **not** Gemini's clock. Deletion is eventually consistent: *"they may still appear in My Activity for some time, but these items will be auto-deleted in less than 24 hours."*
- **Exposes:** AI Mode conversations are Search history. Not subject to Gemini's 18-month default or 3-year human-review path, and **not deleted by any Gemini control.**
- **Recommend:** Purge both buckets separately.
- **Risk:** Medium
- **Confidence:** `verified` (label, URL, 24h lag) / `unresolved` (whether a distinct "AI Mode" heading exists in My Activity)

- **Setting:** Workspace retention *(for contrast)*
- **Where:** Admin console → Generative AI → Gemini for Workspace → Conversation history & deletion
- **Default:** Per Google's Workspace Privacy Hub: Gemini in Workspace **90 days to indefinite, admin-determined**; Gemini app **up to 36 months** (default 18); Gemini Notebook **not retained after session ends**; Gemini app with history off, up to 72 hours. Admin options: 90 days / 540 days / 1080 days / Don't automatically delete / Let users choose, plus `Allow users to delete conversations`.
- **Recommend:** Set 90 days rather than turning history off — turning it off also severs Gemini's access to Workspace apps.
- **Risk:** Medium
- **Evidence:** https://knowledge.workspace.google.com/admin/gemini/manage-gemini-in-workspace-conversation-history-settings — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Export / Takeout
- **Where:** https://takeout.google.com
- **Recommend:** Export before purging.
- **Risk:** Low
- **Confidence:** `verified`

## 6. Voice, audio & camera

- **Setting:** Gemini Live retention *(governed by `Keep Activity`; no Live-specific control)*
- **Where:** Gemini app → Live. Related: `Gemini's Voice`, `Interrupt Live responses`, `Caption preferences`
- **Default:** With `Keep Activity` ON (the default), Live media is retained. Verbatim: *"the transcripts, audio, files, images, & YouTube videos, and any video or screenshares you choose to share with Live are saved in Gemini Apps Activity."* With it off: *"stored in your Google Account for up to 72 hours."*
- **Exposes:** At default, your voice recordings, Live camera video and screen-share video are stored in your Google Account for up to 18 months, and **the transcripts feed model training.** A single Live screen share of a client dashboard puts that video in your account for 18 months.
- **Recommend:** Turn `Keep Activity` off or use Temporary Chat before any Live session involving a screen share, a document, or another person's voice.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/13594961#live_data ; https://support.google.com/gemini/answer/15274899 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Gemini Live camera and screen-share auto-off behavior
- **Default:** Camera auto-**off** when Live is held, when you leave the app, or when the screen locks, and does **not** auto-resume from lock. Screen sharing auto-stops on hold or screen lock and must be manually restarted.
- **Recommend:** Rely on the auto-off as a backstop, not a control — there is no "don't retain this video" switch.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Include voice and audio activity` *(Google Assistant legacy)*
- **Where:** Google Account → Data & privacy → History settings → Web & App Activity → checkbox. https://myactivity.google.com/activitycontrols
- **Default:** **OFF.** Verbatim: *"This voice and audio activity setting is off unless you choose to turn it on."* Safety Center concurs: *"By default, your audio recordings are not saved on Google servers."*
- **Exposes:** At default, Assistant voice interactions are logged as text in Web & App Activity but audio is not stored. If enabled: *"trained reviewers (which include third parties) can analyze the audio to annotate the recording."*
- **Recommend:** Verify unchecked, purge existing audio — then **stop treating it as the audio control.** It is scoped to Assistant only, Assistant began shutting down 2026-09-04, and unchecking it does **nothing** for Gemini. The page still resolves but never mentions Gemini; its last inline update notice is dated 2022-06-06.
- **Risk:** Low at default; **Medium as a false sense of security**
- **Evidence:** https://support.google.com/accounts/answer/6030020 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Talk to Gemini hands-free` → `Hey Google` *(and legacy `Hey Google & Voice Match`)*
- **Where:** Gemini app → Menu → profile picture → Settings → Talk to Gemini hands-free → Hey Google. Voice Match: Google Home app → Settings → Google Assistant → Voice Match
- **Default:** **`unresolved` for both.** Google's pages are phrased as "turn on" instructions and state no default. On Pixel, Google says "Hey Google" works but also tells users to *"check if 'Hey Google' & Voice Match are turned on"*, implying it may arrive enabled via Assistant migration. **Do not assert a default — check the device.**
- **Exposes:** An always-listening local hotword detector; on trigger, audio goes to Google. Voice Match builds a **biometric voice model**: *"This voice model is created on Google's servers and then stored only on the devices where you've turned on Voice Match,"* and Google *"may also temporarily process a model of your voice from your audio saved on Google servers."* **Google documents no way to delete the voice model** — only removing Voice Match per home or per device.
- **Recommend:** Turn `Hey Google` off and use the mic button; remove Voice Match; unbind Settings → System → Gestures → Press & hold power button. **There is no "Hey Gemini" hotword** — Gemini reuses the legacy wake phrase and routes through Voice Match enrollment.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/14554984 ; https://support.google.com/assistant/answer/9071681 — checked 2026-10-02
- **Confidence:** `verified` (labels, paths, voice-model handling) / `unresolved` (defaults)

- **Setting:** Agentic Calling (`Call for me`)
- **Where:** Gemini mobile app → ask Gemini to call a business → tap `Call for me`. Records land in Phone by Google history.
- **Default:** Requires an explicit tap plus acceptance of three agreements. **Your microphone is muted by default** during the call. US numbers only; eligible Pixel devices.
- **Exposes:** **Calls are recorded.** Verbatim: *"Gemini starts every call by disclosing that it's an AI assistant from Google calling on a recorded line on your behalf, stating your name."* Before dialing it shows what it plans to share — *"name, email, phone number, or other relevant details"* — and requires approval; it will not disclose card numbers or passwords. **Transcripts are stored on Google servers; audio recordings are not retained server-side.** Local copies of both remain on-device in Phone by Google. *"Google does not use these recordings or transcripts to train AI models."*
- **Recommend:** Treat as a recorded call: two-party-consent jurisdictions, client confidentiality, and the fact that **a recording of a third party who never consented now exists on your device.** Purge from Phone history after use.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/18336420 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Avatar recordings
- **Default:** Deleted automatically after **3 years** of non-use.
- **Recommend:** Delete manually rather than waiting out the window.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Gemini in Meet — `Automatic note-taking` *(user-facing: "Take notes for me")* ⚠️
- **Where:** Admin console → Apps → Google Workspace → Google Meet → Gemini settings. User side: Meet → gear → Meeting Records
- **Default:** **A transition is in flight and the date has passed.** The steady-state feature page says Off (admin enablement required). The change notice says: **"On or after September 21, 2026"**, Automatic note-taking becomes *"on by default for meetings with 3 or more guests (including the host)"* for **Business Standard / Business Plus**, prerequisite being that Gemini note-taking and smart features are on. **Today is 2026-10-02 — assume any Business Standard/Plus tenant that did not opt out is auto-note-taking right now.**
- **Exposes:** Every meeting with 3+ attendees is transcribed and summarized into a Google Doc *"emailed to the organizer and the person who started the note-taking,"* attached to the Calendar event (so visible to anyone with event access), following Meet/Drive retention and Vault-discoverable.
- **Recommend:** **Check your tenant today** and set `Automatic note-taking` to Off unless you have an affirmative consent story.
- **Risk:** High
- **Evidence:** https://knowledge.workspace.google.com/admin/meet/upcoming-changes-to-automatic-note-taking — checked 2026-10-02
- **Confidence:** `verified` (defaults, recipients) / `unresolved` (whether any in-meeting participant consent prompt exists — neither page documents one; and whether transcription is a separate admin toggle)

## 7. Agentic / computer-use permissions

**Project Mariner no longer exists.** Shut down ~2026-05-04 and folded into Gemini Spark, Chrome auto browse, and AI Mode. "Mariner" and "Agent Mode" are stale names. `reported` — corroborated across trade press; no official Google source fetched.

- **Setting:** `Gemini Spark` / `Turn off Gemini Spark`
- **Where:** Gemini → Menu → Settings & help → Gemini Spark Settings. https://gemini.google.com/gemini-spark
- **Default:** Gated. Requires **18+**, a **personal** Google Account (explicitly not work/school), **Google AI Pro or Ultra**, and **`Keep Activity` ON**. Unavailable in the EEA, Nigeria, Switzerland, UK. Per-user default once subscribed: **`unresolved`**.
- **Exposes:** A cloud-resident agent that **runs when your device is off.** It reaches Connected Apps (Gmail, Calendar, Drive, Docs, Sheets, Slides, Keep, Tasks, Contacts, Photos, YouTube), your Memory and instructions, **your local Chrome and saved logins**, a **remote browser holding cookie-based auth**, and a **remote computer that executes code.** Verbatim: *"Gemini has access to all the same sites that you do, including sites you're signed into."* And: *"Gemini can share information from your chat and other available sources… with websites while using the local or remote browser. This could include your name, contact info, files, preferences, and info you might find sensitive."*
- **Recommend:** Leave off. If used, connect nothing from Gmail/Drive, and purge remote browser and remote-computer data after every task.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/16596215 ; https://support.google.com/gemini/answer/17094507 — checked 2026-10-02
- **Confidence:** `verified` (gating, permissions, logged-in-session access, kill switch) / `unresolved` (per-user default once subscribed)

- **Setting:** Spark confirmation gates
- **Default:** Confirmation required before *"Sending communications, modifying your data, making purchases, and submitting web forms"* and before *"Signing in to websites using Sign in with Google."* `Take control` mode requires you to personally enter passwords or payment details. Per-task Stop; 15 concurrent task cap.
- **Exposes:** **One documented gap:** *"Gemini can perform bulk actions on private tasks in Google Tasks without your confirmation."* Screenshots taken during automation *"are reviewed by trained reviewers and used to improve Google services if Keep Activity is on."*
- **Recommend:** The gates are reasonable, but note the Tasks carve-out and that Spark's screenshots enter human review. **Since Spark requires `Keep Activity` ON, you cannot run the agent and opt out of training/review — that coupling is the structural problem.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Spark data deletion — `Delete remote browser data`, `Delete remote code execution data`, `Turn off Gemini Spark`
- **Default:** Data accumulates until purged. Remote browser cookies and auth data are *"saved for future sessions"*; `.md` files and code persist on the remote computer.
- **Exposes:** Turning Spark off deletes remote browser and remote-computer data but **not** your Chrome browsing data, and **tasks, threads and files Spark created or modified remain.** Schedules are paused, not deleted.
- **Recommend:** Purge both stores explicitly rather than relying on the off switch.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Let Gemini browse for you` *(Chrome auto browse)*
- **Where:** Chrome → Settings → AI innovations → Gemini in Chrome → Permissions. `chrome://settings/ai/gemini`
- **Default:** Gated — US only, 18+, AI Pro or Ultra, personal account, Safe Browsing on, latest Chrome, English. Per-user default once eligible: **`unresolved`**.
- **Exposes:** Multi-step tasks across arbitrary sites; with permission it uses Google Password Manager to sign in (Google states it does not share your passwords with Gemini or with sites). Presents a plan for review, then requests confirmation for sending communications, modifying data, submitting forms, scheduling events, and finalizing financial transactions. Visited sites appear in Chrome history with a distinguishing icon.
- **Recommend:** Keep off; separately revoke the Password Manager auto-sign-in permission.
- **Risk:** High
- **Evidence:** https://support.google.com/chrome/answer/16821166 — checked 2026-10-02
- **Confidence:** `verified` (controls, gates) / `unresolved` (default once eligible)

- **Setting:** `Screen automation` in Android apps — **no dedicated toggle found**
- **Default:** **`unresolved`** — no on/off control documented.
- **Exposes:** Verbatim: *"Gemini can help with tasks, like placing orders or booking rides, using screen automation on certain apps on your device."* It captures **screenshots that may contain visible information**, which *"are reviewed by trained reviewers and used to improve Google services if Keep Activity is on."* Google cautions against entering login or payment details and against using it for emergencies.
- **Recommend:** Do not use for anything involving credentials or payment. Turn `Keep Activity` off to keep the screenshots out of human review.
- **Risk:** High
- **Confidence:** `verified` (behavior, human review) / `unresolved` (whether a toggle exists)

- **Setting:** `Deep Research`
- **Default:** **Google Search is on as a source by default.** Gmail, Drive, Chat, files and notebooks are **opt-in** and *"only available if the Google Workspace app is connected."* Retention inherits Gemini Apps Activity: *"You can only find past research reports if your Keep Activity setting is on."*
- **Recommend:** Do not connect Gmail/Drive as sources for client work; export to Docs and delete the chat.
- **Risk:** Medium (High if Gmail/Drive connected)
- **Evidence:** https://support.google.com/gemini/answer/15719111 — checked 2026-10-02
- **Confidence:** `verified` (sources, retention dependency) / `unresolved` (whether plan approval is a hard gate or advisory)

- **Setting:** `Skills` *(replacing Gems)* — Skills Manager
- **Where:** https://gemini.google.com/agent/skills. Invoked inline with `/` (and soon `@`)
- **Default:** Migration is automatic — *"automatically transition your Gems to skills for you when Gems go away."* Rollout: **November 2026** personal accounts, March 2027 Workspace business/enterprise/nonprofit, June 2027 education.
- **Exposes:** **Skills auto-apply when Gemini judges them relevant** and are composable, so a skill's instructions and knowledge files can enter a conversation the user did not deliberately scope to it. Sharing semantics are promised but not yet documented.
- **Recommend:** Audit what migrates in November and **remove knowledge files from any skill you would not want auto-invoked.**
- **Risk:** Medium
- **Evidence:** https://support.google.com/gemini/answer/18560919 — checked 2026-10-02
- **Confidence:** `verified` (timeline, migration, URL) / `unresolved` (skill sharing defaults)

- **Setting:** `Computer Use` via the Gemini API — `safety_decision`, `disabled_safety_policies`, `enable_prompt_injection_detection`
- **Where:** https://ai.google.dev/gemini-api/docs/computer-use. Recommended model `gemini-3.8-flash`
- **Default:** **Preview.** Verbatim: *"As a Preview capability, Computer Use may contain errors and security vulnerabilities."* The model returns `safety_decision`; when it equals `require_confirmation` the docs instruct the developer to *"prompt the end user."*
- **Exposes:** **The confirmation gate is advisory** — it is the developer's responsibility to surface it, so a careless integration auto-approves everything. Google documents **no server-side retention policy** specific to Computer Use.
- **Recommend:** Never set `disabled_safety_policies`; always honor `require_confirmation`; enable `enable_prompt_injection_detection`; use a paid API tier (§9).
- **Risk:** High
- **Confidence:** `verified` (controls) / `unresolved` (retention)

- **Setting:** Jules (coding agent) data use
- **Default:** Private repos are not used for training and *"no data is sent"*; **public repo data may be used for training.** The repo is cloned into an isolated GCP VM destroyed after the task.
- **Recommend:** Private repos only if training matters to you.
- **Risk:** Medium (public) / Low (private)
- **Evidence:** https://jules.google/docs/faq/ — checked 2026-10-02
- **Confidence:** `reported` — reached via search summary, not a direct fetch; re-verify before relying on it

- **Setting:** `Google Agentspace` → **renamed `Gemini Enterprise`**
- **Default:** `cloud.google.com/agentspace` returns **301 → `cloud.google.com/gemini-enterprise`**. Use the Workspace admin plane, not the Cloud console, to govern it now (§8).
- **Confidence:** `verified`

## 8. Admin / workspace plane

**Structural note.** The entire Workspace admin help corpus moved: every `support.google.com/a/answer/*` URL tested returns **301 → `knowledge.workspace.google.com/...`**. Gemini controls are no longer under *Apps > Additional Google services* or *Apps > Google Workspace* — there is now a **top-level left-nav section called `Generative AI`**. The one exception is Meet note-taking, still under *Apps > Google Workspace > Google Meet*. Also **404:** `workspace.google.com/learn-more/security/security-whitepaper/` — live equivalents are `workspace.google.com/security/ai-privacy` and the Privacy Hub.

- **Setting:** `Gemini app` service status — `On for everyone` / `Off for everyone`, plus `Allow all users to access the Gemini app, regardless of license`
- **Where:** Admin console → Generative AI → Gemini app
- **Default:** **ON by default** for new Business, Enterprise and Frontline customers; **OFF by default for Primary and Secondary (K12)**, ON for Higher Education. The current admin page does not restate this, so for an existing tenant treat as **`unverified` until checked in-console.**
- **Exposes:** Every licensed user gets a consumer-shaped assistant wired to corporate identity with 18-month history.
- **Recommend:** Leave on but pair with a 90-day retention floor; **uncheck "regardless of license"** so unlicensed users don't fall under looser additional-service terms.
- **Risk:** Medium
- **Evidence:** https://knowledge.workspace.google.com/admin/gemini/turn-the-gemini-app-on-or-off — checked 2026-10-02
- **Confidence:** `verified` (new tenants) / `unverified` (existing tenants)

- **Setting:** `Workspace apps` / `Other Google apps` / `Classroom app` *(Gemini app corpus access)*
- **Where:** Admin console → Generative AI → Gemini app → Apps
- **Default:** **ON.** Verbatim: *"By default, the Gemini app can connect to Workspace apps"* — Gmail, Drive, Docs, Calendar, Keep, Tasks. `Other Google apps` covers Maps, YouTube, Hotels, Flights.
- **Exposes:** Out of the box the standalone Gemini app can read a user's mail, files, calendar, notes and tasks.
- **Recommend:** **Highest-leverage admin toggle.** Turn `Other Google apps` off (no business case); make `Workspace apps` a conscious per-OU decision.
- **Risk:** High
- **Evidence:** https://knowledge.workspace.google.com/admin/gemini/turn-google-apps-in-gemini-on-or-off — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Enable Gemini conversation history` / `Conversation history & deletion` / `Allow users to delete conversations`
- **Default:** **ON**, 18 months, 3-month minimum.
- **Recommend:** Set the **90-day** floor rather than turning history off — Google states *"You must turn on Gemini conversation history to use Workspace apps in Gemini,"* so off also severs corpus access.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Feature access` *(Gemini side panel per Workspace service)*
- **Where:** Admin console → Generative AI → Gemini for Workspace → Feature access → Edit per service
- **Default:** **ON.** Verbatim: *"The default setting for Gemini features in Workspace services is on."*
- **Exposes:** The side panel retrieves the user's reachable Gmail/Drive/Docs content on each grounded prompt, scoped to that user's existing ACLs — so **Gemini inherits your oversharing.** **Critical gotcha, verbatim:** *"Even if Gemini is off for a specific app, users can still access its data when using Gemini in other apps."* **Per-app off switches are not data-isolation boundaries.**
- **Recommend:** Contain at the data layer instead — DLP→IRM rules, Drive trust rules, CSE on the sensitive corpus. **Audit shared-drive permissions *before* enabling.**
- **Risk:** High
- **Evidence:** https://knowledge.workspace.google.com/admin/gemini/manage-access-to-gemini-features-in-workspace-services — checked 2026-10-02
- **Confidence:** `verified` (default, the cross-app gotcha) / `unresolved` (the page's edition list omits Business editions — likely a doc error)

- **Setting:** `Smart features in Gmail, Chat, and Meet` / `Smart features in Google Workspace` / `Smart features in other Google products`
- **Where:** Admin: Admin console → Account → Account settings → Smart features for Google Workspace (super-admin). User: Gmail → Settings → General; Drive → Settings → Privacy; Chat → Settings → Data Privacy
- **Default:** **Region-dependent, verified.** *"If your domain is based in the European Economic Area, Japan, Switzerland, or the UK, Workspace smart features and controls are turned off by default. For all other regions… turned on by default."* Admins may choose `Don't set a default experience—Your users choose`, and *"users can override the default."*
- **Exposes:** **This is the master gate for Gemini in Workspace** — users must turn smart features on to access it. Outside EEA/JP/CH/UK, Gemini-in-Workspace is live by default.
- **Recommend:** Adopt the EEA posture everywhere; **turn `Smart features in other Google products` off org-wide regardless of region** — it is the only one that moves signal *outside* Workspace.
- **Risk:** High (#3) / Medium (#1, #2)
- **Evidence:** https://knowledge.workspace.google.com/admin/security/manage-google-workspace-smart-features-for-your-users — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Allow users to access any third-party apps` *(API controls)*
- **Where:** Admin console → Security → Access and data control → API controls → Settings. Per-app: Trusted / Limited / Specific Google data / Blocked. Also `Trust internal apps`
- **Default:** **`Allow users to access any third-party apps` is marked "(default)" on Google's own current page.** ⚠️ This contradicts widely circulated third-party claims that unconfigured apps are blocked by default.
- **Exposes:** Any end user can OAuth-grant an arbitrary external app against corporate Drive and Gmail with **no admin review** — including AI tools that will then train on it under *their* terms, entirely outside Google's no-training commitment.
- **Recommend:** Switch to `Don't allow users to access any third-party apps` and allowlist deliberately. **This is the exact bypass around every other Gemini control above.**
- **Risk:** High
- **Evidence:** https://knowledge.workspace.google.com/admin/apps/control-which-apps-access-google-workspace-data — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `Allow conversation sharing via link` / `Allow conversation sharing via Drive`
- **Where:** Admin console → Generative AI → Gemini app → Sharing → Conversation sharing
- **Default:** Verbatim: *"Using public links to share conversations is turned off by default"* and *"Using Drive to share conversations is turned on by default."*
- **Exposes:** At default, Workspace users cannot mint public Gemini URLs at all. **This is the main reason Workspace is materially safer than consumer Gemini for sharing.**
- **Recommend:** Leave link sharing off.
- **Risk:** Low at default; High if an admin enables link sharing
- **Confidence:** `verified`

- **Setting:** `Allow users to share Gems`
- **Default:** **`unverified`** — not stated on the page.
- **Exposes:** *"Shared Gems are stored and shared in Google Drive, so the sharing settings for Drive also apply to Gems"* — if Drive external sharing is permitted, Gems and their embedded instructions and attached context can leave the organization. Turning it off is **not retroactive**: *"previously shared Gems will still be accessible and shareable from within Drive."* And **Gems are not Vault-covered.**
- **Recommend:** Audit existing Gems in Drive before relying on this toggle.
- **Risk:** Medium
- **Confidence:** `verified` (behavior, non-retroactivity) / `unverified` (default)

- **Setting:** `Gemini Beta features` *(renamed from "Alpha"; URL slug still says `alpha`)*
- **Default:** **OFF.** Verbatim: *"Gemini Beta is turned off by default. Only an administrator can turn it on."*
- **Exposes:** All-or-nothing: *"When you enable access to these features, you enable access to all available Gemini Beta features. You can't control access to individual features."* Current inventory includes Gmail Live, AI Inbox, Docs Live, Keep Live, Fill with Gemini, Meet co-presenter suggestions, **in-person meeting notes** (physical-room audio capture), and Workspace Studio flows.
- **Recommend:** Leave off in production. If piloting, scope to one OU of informed volunteers — **every future beta lands silently on that OU.**
- **Risk:** High if enabled broadly; Low at default
- **Confidence:** `verified`

- **Setting:** `Enable features that may process data across multiple regions` *(Data regions → Advanced settings)*
- **Default:** **ON** — *"This option is turned on by default."*
- **Exposes:** At default, a subset of Gemini features processes data outside your declared region. Turning it off costs image generation, AI voiceover in Vids, video/audio/slide generation, **personalization, Gems, Deep Research, and conversation mode.**
- **Recommend:** If you have a regional commitment, turn it off **and** disable Gemini Notebook — otherwise the commitment is incomplete.
- **Risk:** High for regulated tenants; Low otherwise
- **Confidence:** `verified`

- **Setting:** `Gemini Notebook` service status *(formerly NotebookLM, renamed 2026-07-16)*
- **Default:** **`unverified`** — not stated on the current page. Historically (`reported`): OFF for K12, ON for Higher Education, core service for Business/Enterprise.
- **Exposes:** **The one Gemini surface that escapes both data regions and Vault.** Verbatim: *"Your organization's data region settings don't apply to data processed and cached by Gemini Notebook"*; and it is **absent from Vault's supported services list** — no retention, hold, or eDiscovery coverage. Training carve-out: *"not used to train Gemini Notebook unless you provide feedback."*
- **Recommend:** **If you have a data-region commitment or an eDiscovery obligation, turn it off.**
- **Risk:** High for regulated/regionalized tenants; Medium otherwise
- **Evidence:** https://knowledge.workspace.google.com/vault/getting-started/supported-services-and-data-types — checked 2026-10-02
- **Confidence:** `verified` (data-region exemption, training carve-out, Vault gap) / `unverified` (default, and the Privacy Hub's "not retained after session ends" claim, which conflicts with documented caching)

- **Setting:** `Gemini Enterprise` service and `Allow Gemini Enterprise to access Google Workspace data`
- **Where:** Admin console → Generative AI → Gemini Enterprise. Controls `Gemini Enterprise agents in the side panel`, `Gemini Enterprise assistant`, `Gemini CLI`
- **Default:** **`unverified`** — requires purchased licenses. As of **2026-04-17** these controls **migrated out of the Google Cloud console into the Workspace Admin console**; existing configurations were inherited.
- **Exposes:** Where licensed and enabled, agents can **take actions** (not just read) in Gmail, Drive and Calendar on the user's behalf. Corroborating signal: the Gemini audit log schema now includes `Agent info` and `By an agent`. Data commitment: *"Your data—including prompts, outputs, and training—isn't used to train Google generative AI models."*
- **Recommend:** Keep Workspace-data access off until agent-action audit review is in place; set external chat sharing to org-domains-only; **build an alerting rule on `By an agent` events.**
- **Risk:** High
- **Confidence:** `verified` (controls, migration) / `unverified` (defaults)

- **Setting:** CSE, IRM, and Drive trust rules as Gemini exclusions
- **Default:** CSE is opt-in. **CSE content is confirmed excluded from Gemini:** *"Client-side encryption (CSE) can restrict Gemini's access to sensitive data, because no Google system or Google employee have the technical means to access CSE content."* Also: *"When IRM is applied (e.g., preventing download, printing, or copying), Gemini does not retrieve those protected files."*
- **Exposes:** A mitigation, not an exposure — but CSE also blinds phishing/malware scanning and DLP. **You trade detection for confidentiality.**
- **Recommend:** CSE for the genuinely sensitive corpus; **DLP→IRM as the practical default** — IRM is the only control that excludes files from Gemini retrieval *without* blinding security scanning.
- **Risk:** Low *(it is a control)*
- **Confidence:** `verified` (the exclusion) / `unresolved` (path, default)

- **Setting:** `Gemini for Workspace log events` / `Gemini Notebook log events` / `Gemini reports`
- **Where:** Admin console → Reporting → Audit and investigation. Dashboards: Generative AI → Gemini reports → Org-level / User-level usage
- **Default:** Requires the Audit & Investigation privilege; default view last 7 days; export capped at 100,000 rows. Gemini Notebook log events are **new as of August 2026**. Attributes include `Agent info`, `By an agent`, `Feature Source`.
- **Exposes:** Logs are a control — but **`User-level usage` is a per-employee AI-activity profile** (High/Medium/Low/Zero, active days, days at limit, usage by app). In works-council or co-determination jurisdictions that dashboard is itself a consultable monitoring tool.
- **Recommend:** Alert on `By an agent` events; restrict `Gemini reports` via admin-role scoping; export to your SIEM rather than relying on the row cap.
- **Risk:** Low *(as a control)* / Medium *(the user-level dashboard as monitoring)*
- **Confidence:** `verified` (sources, attributes) / `unresolved` (log retention period)

- **Setting:** Vault coverage of Gemini content
- **Default:** **Partial coverage only.** Covered: *"Vault can retain, hold, search, and export prompts entered by users and responses generated by Gemini app"* (retention rules and holds GA June 2026), and *"notes taken by Gemini"* in Meet. **Not covered, verified exclusions:** *"Any media files or Gems that users attach to Gemini app prompts, or any media files generated by Gemini app"*; **`Google Workspace with Gemini data`** — i.e. "Help me write," side-panel prompts, all in-app Gemini activity; and **Gemini Notebook**, absent from the supported-services list entirely.
- **Exposes:** The standalone Gemini app is discoverable. **Gemini embedded in Workspace apps, Gems, attached/generated media, and Gemini Notebook are an eDiscovery blind spot.** Any legal hold scoped as "we hold everything in Vault" is overstated for AI content.
- **Recommend:** Document the gap in your retention schedule and legal-hold procedures. The only lever today is disabling the uncovered surfaces.
- **Risk:** High for litigation-exposed or regulated organizations
- **Confidence:** `verified`

- **Setting:** `New features` → `Rapid release` / `Scheduled release`
- **Default:** **`unverified`** — the authoritative page does not state a default. Commonly reported as Scheduled; Scheduled is "at least one week after" Rapid.
- **Exposes:** On Rapid Release, default-on Gemini changes (such as the Meet note-taking flip) reach your users first with less notice.
- **Recommend:** Scheduled for production; a throwaway domain on Rapid for advance warning of default changes.
- **Risk:** Medium
- **Confidence:** `verified` (path, labels) / `unverified` (default)

- **Setting:** Workspace training commitment — **contractual, not a toggle**
- **Default:** No training. Verbatim: *"Workspace does not use customer data for training models without customer's prior permission or instruction"*; *"Your content is not human reviewed or otherwise used for Generative AI model training **outside your domain** without permission."*
- **Exposes:** **Read the qualifiers.** Every sentence is scoped by "outside your domain" and "without permission," which leaves room for in-domain improvement and for anything a user "permits" — notably the feedback/thumbs channel and the separate admin setting `Let users participate in surveys and user experience studies`. The Gemini Notebook page is more candid: *"not used to train Gemini Notebook unless you provide feedback."*
- **Recommend:** Rely on the commitment, but turn off surveys/UX studies and brief users that **thumbs-up/down is a consent channel.**
- **Risk:** Low (cross-domain training) / Medium (feedback channel)
- **Confidence:** `verified`

## 9. API / developer plane

**Two surfaces that differ sharply. Do not conflate them.** Google Cloud docs migrated from `cloud.google.com/...` to **`docs.cloud.google.com/...`** (301), and Vertex AI generative AI is now documented as **"Gemini Enterprise Agent Platform"**.

### 9a. Google AI Studio / Gemini Developer API — the tier IS the privacy setting

- **Setting:** Billing Tier (Free → Paid)
- **Where:** Google AI Studio → API keys → *Billing Tier* column → Set up billing. https://aistudio.google.com/apikey
- **Default:** **Free Tier.** Verbatim: *"New accounts begin on the Free Tier."*
- **Exposes:** On Free Tier, verbatim: *"When you use Unpaid Services, including, for example, Google AI Studio and the unpaid quota on Gemini API, Google uses the content you submit to the Services and any generated responses to provide, improve, and develop Google products and services and machine learning technologies."* Every prompt, system instruction, cached content, uploaded file and response flows into product and model development.
- **Recommend:** Link a billing account to the specific project before putting anything real through it. **Paid tier is the only documented way to stop product-improvement use. There is no opt-out toggle on the free tier.**
- **Risk:** High
- **Evidence:** https://ai.google.dev/gemini-api/terms (effective 2026-03-23) — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Human review on the free tier — **no opt-out**
- **Default:** Active on Free Tier. Verbatim: *"To help with quality and improve our products, human reviewers may read, annotate, and process your API input and output… This includes disconnecting this data from your Google Account, API key, and Cloud project before reviewers see or annotate it. Do not submit sensitive, confidential, or personal information to the Unpaid Services."*
- **Exposes:** De-identification is **account-level only** — it does not redact content.
- **Recommend:** Never send client data, source code or PII through a free-tier key.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Free-tier retention period
- **Default:** **`unresolved`.** There is **no day or month count anywhere** in the Unpaid Services section. The only numeric figures are feature-specific: Grounding with Google Search 3 days, Grounding with Google Maps 30 days, displayed Grounded Results up to 90 days. **Do not repeat the commonly cited "55 days"** — it could not be verified in any current Google source.
- **Recommend:** Treat free-tier submissions as permanent.
- **Risk:** High
- **Confidence:** `unresolved` (the absence of a published figure is verified; the figure itself is not published)

- **Setting:** Paid Services data-use clause
- **Default:** No product-improvement use. Verbatim: *"Google doesn't use your prompts (including associated system instructions, cached content, and files such as images, videos, or documents) or responses to improve our products… For Paid Services, Google logs prompts and responses for a limited period of time, solely for detecting and preventing violations of the Prohibited Use Policy… This data may be stored transiently or cached in any country in which Google or its agents maintain facilities."*
- **Exposes:** **"A limited period of time" is not quantified and there is no opt-out. No data-residency guarantee even when paid** — "any country." No human-review statement appears for Paid Services, so human access during a PUP investigation is neither promised nor excluded.
- **Recommend:** Use Vertex / Gemini Enterprise Agent Platform instead if residency matters — **the single biggest reason to prefer it.**
- **Risk:** Medium (Medium-High for residency)
- **Confidence:** `verified` (the clause) / `unresolved` (retention figure, human-review question)

- **Setting:** What makes AI Studio "Paid" — **project-scoped, and this changed**
- **Default:** Current verbatim: *"Your access to Google AI Studio is a 'Paid Service' even when it is offered free of charge, as long as the account you are using to access Google AI Studio has access to a Cloud Project with an associated and active Cloud Billing account or is a Workspace enterprise account. Your access to Gemini API is a 'Paid Service' only when accessing the API through a Cloud Project associated with an active billing account."* The Sept 2025 version read *"When you activate a Cloud Billing account, all use of Gemini API and Google AI Studio is a 'Paid Service.'"*
- **Exposes:** **A trap.** A developer with billing on one project gets Paid protection in the AI Studio **UI**, but an API key minted in a **different, non-billed project is still Unpaid** and gets trained on.
- **Recommend:** **Audit each API key's project individually, not the account.**
- **Risk:** High
- **Evidence:** https://ai.google.dev/gemini-api/terms ; https://web.archive.org/web/20251005134032/https://ai.google.dev/gemini-api/terms — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** EEA / Switzerland / UK carve-out
- **Default:** Verbatim: *"If you're in the European Economic Area, Switzerland, or the United Kingdom, the terms under 'How Google uses Your Data' in 'Paid Services' apply to all Services, including Google AI Studio and unpaid quota in the Gemini API, even though they are offered free of charge."*
- **Recommend:** If you are in scope you already have the protection; verify your account region.
- **Risk:** Low for those users
- **Confidence:** `verified`

- **Setting:** Implicit context caching (Gemini Developer API)
- **Default:** **ON.** Verbatim: *"Implicit caching is enabled by default for all Gemini 2.5 and newer models… There is nothing you need to do in order to enable this."*
- **Exposes:** Prompt prefixes retained server-side to serve cache hits. **No documented way to disable it on the Developer API** — unlike Vertex, which exposes a project-level kill switch.
- **Recommend:** If you need caching off, use Vertex / Agent Platform.
- **Risk:** Medium on free tier *(cached content is explicitly inside the free-tier license grant)* / Low on paid
- **Confidence:** `verified`

- **Setting:** Model tuning content
- **Default:** Verbatim: *"Google only uses content that you import or upload to our model tuning feature for that express purpose… When you delete a tuned model, the related tuning content is also deleted."*
- **Recommend:** Delete tuned models you no longer use.
- **Risk:** Low
- **Confidence:** `verified`

### 9b. Vertex AI / Gemini Enterprise Agent Platform — no training by default, but several default-on retention paths

- **Setting:** "Training Restriction" — Service Specific Terms § 18 *(formerly § 17)*
- **Default:** No training. Verbatim: *"Google will not use Customer Data to train or fine-tune any AI/ML models without Customer's prior permission or instruction."* Docs add: *"This applies to all managed models on Gemini Enterprise Agent Platform, including GA and pre-GA models."*
- **Exposes:** Nothing to model training at default. **But note it is a "without prior permission or instruction" restriction, not an absolute one** — enabling request-response logging or `store=true` *is* an instruction.
- **Recommend:** Rely on it, but audit anything you enable that constitutes an "instruction."
- **Risk:** Low
- **Evidence:** https://cloud.google.com/terms/service-terms (last modified 2026-09-30) — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Interactions API `store` parameter — **the sharpest default-on trap in this section**
- **Default:** **`true`.** Verbatim: *"If you do not specify a value for store, it defaults to true for all models. To achieve zero data retention, explicitly set store = false in your API requests."*
- **Exposes:** Prompts, responses and conversation state persisted server-side by default for anyone who omits the flag.
- **Recommend:** **Set `store: false` explicitly on every Interactions API call** unless you specifically want server-side conversation state.
- **Risk:** High
- **Evidence:** https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Prompt logging for abuse monitoring *(standard Google models)* — **materially changed; flag this**
- **Default:** **ON** for anyone on the public GCP Terms of Service. Verbatim: *"Only customers whose use of Google Cloud is governed by the Google Cloud Platform Terms of Service. This means that customers with a Google Cloud Master Agreement are exempt from prompt logging for this abuse monitoring by default."*
- **Exposes:** When classifiers flag you, prompts are logged and *"stored securely for up to 90 days in the same region or multi-region selected by the customer"*, and *"Authorized Google employees may assess the flagged prompts and may reach out to the customer for clarification."* Verbatim caveat: *"Prompt logs for the purposes of abuse monitoring are not encrypted by Customer-managed encryption keys (CMEK)."* It does confirm: *"This data won't be used to train or fine-tune any AI/ML models."*
- **Recommend:** For true zero data retention, get onto a Google Cloud Master Agreement via an account team — **the self-serve opt-out is gone.** The May 2025 version said **30 days**, said *"Customers also have the option to request an opt-out from abuse logging,"* scoped in-scope customers to those *"who don't have an invoiced (offline) Cloud Billing account,"* and linked a form. Today: **90 days**, the invoiced-billing escape hatch removed, the opt-out sentence removed, and the form resolves to **`/closedform`**.
- **Risk:** Medium-High
- **Evidence:** https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring ; https://web.archive.org/web/20250521191346/https://cloud.google.com/vertex-ai/generative-ai/docs/learn/abuse-monitoring — checked 2026-10-02
- **Confidence:** `verified`. **Documentation contradiction to flag:** the ZDR page still says *"you can request an exception for abuse monitoring. See Abuse monitoring"* — but the page it points to contains no exception mechanism and no form link. **The documented exemption path is broken** — `unresolved`.

- **Setting:** Advanced AI Safety Addendum consent *(Advanced AI models)*
- **Where:** Cloud console → Model Garden → consent prompt. Requires `aiplatform.consents.update` (in `aiplatform.admin`)
- **Default:** Not consented; required **once per project**.
- **Exposes:** Once consented, verbatim: *"All prompts and responses will be logged and securely stored for up to 30 days for the sole purpose of monitoring for abuse"* — in-region, **not CMEK-encrypted**, and *"It may not be possible to opt-out of prompt-response logging when using some Advanced AI features."* For certain third-party models *"you must enable sharing this data with Anthropic for abuse monitoring."*
- **Recommend:** Pre-empt accidental consent: **restrict `aiplatform.consents.update` via IAM and disable Advanced AI models in Model Garden** — Google documents exactly these two controls.
- **Risk:** High if ZDR matters *(unconditional 100% prompt+response logging, possibly non-waivable, plus third-party sharing)*
- **Confidence:** `verified`

- **Setting:** Request-response logging
- **Default:** **OFF.** Verbatim: *"This feature is disabled by default… To achieve zero data retention, do not enable this feature."*
- **Exposes:** Nothing at default. Enabled, it writes request/response samples into your own BigQuery and *"can share request-response logs for specific Advanced AI models with certain MaaS Partners."*
- **Recommend:** Leave off. If enabled for eval, treat that BigQuery dataset as prompt-sensitive.
- **Risk:** Low at default; Medium once enabled
- **Confidence:** `verified`

- **Setting:** In-memory data caching *(project-level)*
- **Default:** **ON.** Verbatim: *"…is stored only in-memory (not at-rest), is isolated at the project level, and has a 24-hour TTL… does not violate zero data retention. This feature can be disabled at the project level."*
- **Recommend:** Leave on unless a specific regulator requires otherwise — Google states it does not violate ZDR, and disabling costs latency.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** Data residency / ML processing location + `gcp.restrictEndpointUsage`
- **Default:** The plain **global** endpoint `https://aiplatform.googleapis.com` gives **no residency guarantee.** Verbatim: *"Global endpoints route and process data anywhere globally… they don't provide regional isolation or data residency guarantees."* Caveat: *"The European Union multi-region (eu) endpoint strictly covers data residency within EU member states. Geographies outside the European Union political boundary, including the United Kingdom and Switzerland, are excluded."*
- **Recommend:** **Never use the global endpoint for regulated data;** pin a jurisdictional endpoint and enforce org-wide with the **`gcp.restrictEndpointUsage`** organization policy constraint.
- **Risk:** High if left on the global endpoint
- **Confidence:** `verified`

- **Setting:** CMEK
- **Default:** **Google default encryption** at rest; CMEK is opt-in.
- **Recommend:** Enable CMEK for key control, rotation and audit — **but know the gap:** abuse-monitoring prompt logs (standard *and* Advanced AI) are explicitly **not** CMEK-encrypted.
- **Risk:** Medium *(control gap, not exposure)*
- **Confidence:** `verified`

- **Setting:** VPC Service Controls perimeter
- **Default:** **No perimeter.** Verbatim: *"By default, these public APIs are reachable from the internet; however, IAM permissions are required for use."* And: *"Private Service Connect… and Private Google Access… don't eliminate public internet accessibility for Agent Platform APIs."*
- **Exposes:** Without a perimeter, a leaked credential is usable from anywhere on the internet; training data, models, inference requests and batch results can egress.
- **Recommend:** Put Agent Platform inside a VPC-SC perimeter. Abuse-monitoring logs are stated to adhere to VPC-SC.
- **Risk:** High without it
- **Confidence:** `verified`

- **Setting:** Grounding features with no off switch
- **Default:** **Grounding with Google Search** — queries derived from end-user prompts plus contextual info stored **up to 3 days**; verbatim: *"There is no way to disable the storage of this information if you use Grounding with Google Search. If you require zero data retention, we recommend using Web Grounding for Enterprise."* **Grounding with Google Maps** — prompts, contextual info and generated output stored **30 days**; *"There is no way to disable the storage of this information."*
- **Recommend:** Use **Web Grounding for Enterprise** instead; avoid Maps grounding for sensitive prompts.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Agent-product retention (CodeMender, Deep Research agent, Sandbox, Live API session resumption)
- **Default:** CodeMender session data including source snippets and diffs encrypted **up to 7 days**. Deep Research agent prompts and session data **7 days**, and it *"cannot be disabled when using the Deep Research agent."* Sandbox snapshots persist for the Sandbox TTL — *"To achieve zero-data-retention, don't use the Sandbox API."* Gemini Live API session resumption is **OFF by default** — *"disabled by default. It must be enabled by the user every time they call the API"*; enabled, it caches *"text, video, and audio prompt data and model outputs, for up to 24 hours."*
- **Recommend:** Don't enable Live session resumption; avoid Sandbox and the Deep Research agent if you need ZDR.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Trusted Tester Program vs. Pre-GA / Preview — **two distinct caveats, don't conflate**
- **Default:** **Trusted Tester** is opt-in: *"lets you optionally share data, but the data is used for product improvements, not for training Gemini models."* **Pre-GA/Preview** carries the Pre-GA Offerings Terms — "as is," limited support — but the Training Restriction **does** cover pre-GA.
- **Recommend:** Don't join Trusted Tester with production data. Read each preview feature's retention statement individually.
- **Risk:** Medium (Trusted Tester) / Low (Preview, re: training)
- **Confidence:** `verified`

### 9c. Gemini Code Assist and Gemini CLI

- **Setting:** Gemini Code Assist individual/free tier — **retired**
- **Default:** Gone. Verbatim: *"Starting June 18, 2026, Gemini Code Assist IDE extensions stopped serving requests for the Gemini Code Assist for individuals, Google AI Pro, and Google AI Ultra tiers. This also applies to usage of Gemini CLI. As part of the deprecation, you can no longer use the Login with Google option."* Migration path is the Antigravity family.
- **Recommend:** The old individuals-tier opt-out toggle no longer exists; do not look for it.
- **Evidence:** https://developers.google.com/gemini-code-assist/docs/deprecations/code-assist-individuals — checked 2026-10-02
- **Confidence:** `verified` (the retirement). **The exact UI label of the old opt-out toggle is `unresolved`** — no surviving official page documents it. Do not state a label.

- **Setting:** Gemini Code Assist Standard & Enterprise data use; `Code customization`
- **Default:** **No training.** Verbatim: *"Gemini doesn't use your prompts or its responses as data to train its models."* Also: *"The Gemini for Google Cloud API doesn't have access to any of the other APIs or resources in your project."* `Code customization` is off until configured: *"When you use code customization, we securely access and store your private code."*
- **Recommend:** Enable code customization deliberately — **it is the one feature that stores your source.** Harden with a VPC-SC perimeter, group-based IAM, SSO + 2SV.
- **Risk:** Low (base) / Medium (code customization)
- **Confidence:** `verified`

- **Setting:** `privacy.usageStatisticsEnabled` *(Gemini CLI)*
- **Where:** `~/.gemini/settings.json` or project `.gemini/settings.json`, under `privacy`
- **Default:** **`true`.** Verbatim: *"Default: `true` — Requires restart: Yes"*
- **Exposes:** Tool names called plus success/failure/duration, model used plus request duration, and session configuration (enabled tools, approval mode). Documented as **not** collected: PII, prompt/response content, file content, tool arguments, tool return data.
- **Recommend:** Set `{"privacy": {"usageStatisticsEnabled": false}}` and restart — **the collected tool-call graph is still a fingerprint of your workflow.**
- **Risk:** Low-Medium
- **Evidence:** https://github.com/google-gemini/gemini-cli/blob/main/docs/reference/configuration.md — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `telemetry.enabled` / `telemetry.logPrompts` *(distinct from usage statistics)*
- **Default:** `telemetry.enabled` = **`false`**; `telemetry.traces` = **`false`**; **`telemetry.logPrompts` = `true`**.
- **Exposes:** Nothing at default. **But the moment you enable telemetry for debugging, prompts are included** — the `prompt` field is only *"excluded if `telemetry.logPrompts` is `false`"* — landing in your local outfile or your GCP project.
- **Recommend:** If you ever enable telemetry, **set `logPrompts: false` in the same edit.**
- **Risk:** Low at default; Medium once telemetry is on
- **Confidence:** `verified`

- **Setting:** Which terms govern Gemini CLI now
- **Default:** With Google-account login removed, the live paths are a **Gemini Developer API key** (→ Gemini API ToS, Unpaid or Paid per the key's project billing) or a **Vertex AI key** (→ GCP Platform ToS).
- **Exposes:** **A Gemini CLI user on a free Developer API key is squarely under Unpaid Services** — prompts and responses used for product improvement and subject to human review. **The highest-value fix for anyone pointing Gemini CLI at client code.**
- **Recommend:** Link billing to the specific key's project, or use a Vertex key.
- **Risk:** High
- **Confidence:** `verified`. Note `docs/resources/tos-privacy.md` on the CLI's `main` branch is **stale** — it still documents the retired Google-account login path, contradicting the deprecation page.

## 10. Mobile & OS app permissions

- **Setting:** `Digital assistant app` *(device)* / `Digital assistants from Google` → `Gemini`
- **Where:** Settings → Apps → Default apps → Digital assistant app (name varies by device; the app listed must be the **Google app**). Alternate: Google app → Profile picture → Settings → Google Assistant → Digital assistants from Google → Gemini
- **Default:** On **Pixel 9 and later**, *"Gemini comes as the default assistant on your device"* out of box — `verified`. On other Android devices the out-of-box default varies by OEM and Android version, and since **2026-09-04** Assistant is being force-migrated to Gemini — `reported`.
- **Exposes:** Gemini inherits every Assistant entry point — "Hey Google" hotword, power-button hold, headphones, watch, Android Auto, and the overlay. Google's own list of what it collects: *"call and message logs, contacts…, installed apps…, language preferences, screen content…, and other app info like page context and URL."*
- **Recommend:** Set `Digital assistant app` to **None** — not to another Google surface, since Gemini is reachable through all of them. Then unbind Settings → System → Gestures → Press & hold power button. **Gotcha, verbatim:** *"Deleting the Gemini mobile app doesn't automatically remove Gemini as your device's default digital assistant."*
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/14554984 ; https://support.google.com/pixelphone/answer/15283615 — checked 2026-10-02
- **Confidence:** `verified` (paths, labels, uninstall gotcha) / `reported` (non-Pixel out-of-box default, Assistant shutdown date)

- **Setting:** `Gemini on lock screen` → `Use Gemini without unlocking` and `Make calls and send messages without unlocking`
- **Where:** Gemini app → Menu → profile picture → Settings → Gemini on lock screen
- **Default:** **`unresolved`.** Google's dedicated lock-screen page, the Device assistance page, the manage/delete page, and three independent how-to writeups were all checked — **none states a default.** All are phrased as "turn on" instructions, weak circumstantial evidence for off-by-default, but Google never says so. **Check the device; do not assume.**
- **Exposes:** If enabled, anyone holding the locked phone can have Gemini answer questions, **make calls, read and reply to messages from notifications**, control smart-home devices, set alarms, play media, and toggle flashlight/volume — **without the PIN.** Personal-content reads still prompt: *"if your requests include personal content, like when you read your calendar, Gemini will ask you to unlock your phone first."*
- **Recommend:** Turn **both** off. `Make calls and send messages without unlocking` **converts physical possession of the phone into send-as-you authority.**
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/14576209 — checked 2026-10-02
- **Confidence:** `verified` (labels, path, capability list) / `unresolved` (default). A reported Android 16 lock-screen auth-bypass allowing SMS/WhatsApp sends without a PIN could not be verified — the source returned HTTP 403; patch status unknown.

- **Setting:** `Screen context` → `use text from screen` / `use screenshot`
- **Where:** Gemini app → Menu → profile picture → Settings → Screen context
- **Default:** **`unresolved`.** Google's page says only *"Make sure 'use text from screen' and 'use screenshot' are on"* — phrasing that implies they may already be on but states no default.
- **Exposes:** Whatever is on screen when you summon Gemini — including another app's content — is sent to Google as text and/or a screenshot, and lands in Gemini Apps Activity if `Keep Activity` is on. **The quietest high-volume data path in the product.**
- **Recommend:** Both off unless actively needed.
- **Risk:** High
- **Confidence:** `verified` (labels, path) / `unresolved` (default)

- **Setting:** Android runtime permissions — Microphone, Camera, Location, Contacts, Notifications, Phone, Files/Photos
- **Where:** Settings → Apps → [Google app, and Gemini if present] → Permissions. Location also at Settings → Location → App location permissions → Google app with a separate `Use precise location`. Notification read/reply at Settings → Apps → Special app access → Notification read, reply & control → Google
- **Default:** Android 6+ runtime permissions are **not granted until a first-use prompt.** Notification read/reply and "Display over other apps" are **special app access** grants requiring an explicit trip to settings.
- **Exposes:** See the collection list above. **Microphone stays open up to 5 minutes** per voice prompt.
- **Recommend:** Deny Camera and Contacts; set Location to "Allow only while using the app" with `Use precise location` off; leave notification read/reply off. **Important caveat:** permissions are largely shared with the **Google app**, not scoped to Gemini — revoking the mic for the Google app also kills it for Search. Google has since shipped a separately-deletable Gemini app entry, so on 2026 builds you may see both carrying overlapping grants — **check both.**
- **Risk:** High (microphone, notification access) / Medium (location, contacts, camera)
- **Confidence:** `verified` (permissions, paths, 5-minute mic window) / `reported` (the Google-app-hosting model is verified for 2025; how cleanly 2026 builds separate the two is `unresolved`)

- **Setting:** `Display over other apps` / Accessibility service
- **Default:** **`unresolved` — and it could not be confirmed that Gemini requests it at all.** The Gemini overlay behaves like a draw-over-apps surface and Google documents that it reads *"page context and URL… when you use Gemini overlay,"* but **no Google page lists `Display over other apps` or an Accessibility grant as a Gemini requirement.** Do not report it as a Gemini permission without checking the device.
- **Risk:** `unresolved`
- **Confidence:** `unresolved`

- **Setting:** iOS Gemini app permissions and lock-screen surfaces
- **Where:** iOS Settings → [Gemini] / [Google]. Google routes location through the Google app: *"When you use Gemini, it uses the location permissions you choose for the Google app."* Requires **iOS 17+**.
- **Default:** iOS requires per-permission consent prompts; location default is whatever the **Google app** holds.
- **Exposes:** **iOS is materially safer than Android on three counts, all verified:** (1) **Gemini cannot be the system assistant** — Siri is not replaceable, and there is no iOS equivalent of `Digital assistant app`. (2) **No Siri or Shortcuts integration is documented** — the iOS get-started page, iOS widget page, iOS Connected Apps page, and a help-center search for "Siri" were all checked; zero Google documentation exists. (3) **No Phone/Messages/WhatsApp carve-out** — *"When Keep Activity is off, Connected Apps won't be available on gemini.google.com, iOS devices, or smart watches,"* so **on iOS `Keep Activity` off genuinely does sever connector access.** **The exposure instead is lock-screen surfaces:** home-screen widget, **lock-screen widget**, **lock-screen control (iOS 18+)**, and **Control Center control (iOS 18+)** — with widget actions that open straight into Gemini Live, the microphone, or the camera.
- **Recommend:** Deny Camera and Photos; Location `Never` or `While Using the App` with precise location off; **do not add Gemini as a lock-screen widget or control** — the iOS analogue of the Android lock-screen risk.
- **Risk:** Medium overall; Medium-High for lock-screen widgets/controls
- **Confidence:** `verified`. A widely-reported Apple–Google arrangement to have Gemini models power a rebuilt Siri is a **different thing** from Gemini-app Shortcuts and could not be verified from a primary source — `unresolved`.

- **Setting:** `Gemini in Chrome` and `Share current tab by default`
- **Where:** Desktop: Chrome → Settings → AI innovations → Gemini in Chrome. `chrome://settings/ai/gemini`. Android: Chrome → Ask Gemini; per-chat `Stop sharing`. Other labels on the same page: `Precise location`, `Microphone`, `Let Gemini browse for you`, `Media understanding`
- **Default:** **Your current tab is shared by default.** Verbatim (Android): *"By default, your current page is shared with Gemini in Chrome."* Desktop: *"When you start a new chat, your current tab is shared with Gemini by default."* `Media understanding` is noted as **on by default**. Requires 18+ (13+ for basic use), signed into Chrome, English, Android 12+ and 4GB+ RAM; **unavailable in Incognito.** Workspace accounts require admin enablement.
- **Exposes:** Verbatim: *"Gemini collects and processes page content and the URL from your current tab and any other tabs you've shared with it. If you use Gemini in Chrome to find pages you visited in Chrome, the relevant URLs from your history will also be collected."* You can share up to **10 open tabs**. And critically: *"Information from websites you visit with the Gemini in Chrome feature is stored in Gemini Apps Activity if your Keep Activity setting is on. **Page content will be logged to your Google Account temporarily and will not appear in your Gemini Apps Activity.**"* — **page bodies are logged to your account in a place you cannot see or audit.**
- **Recommend:** Turn `Share current tab by default` **off**; never invoke Gemini in Chrome on authenticated pages (banking, health, HR, client portals); leave `Let Gemini browse for you` off.
- **Risk:** High
- **Evidence:** https://support.google.com/gemini/answer/16283624 — checked 2026-10-02
- **Confidence:** `verified`

## Volatile

### Already moved — recent enough that most guides are wrong

| Change | When | Why it matters |
|---|---|---|
| `Gemini Apps Activity` renamed **`Keep Activity`**; scope widened to cover uploads | Aug 2025 (uploads from 2025-09-02) | Nearly every third-party guide still uses the old label |
| **`Temporary Chat`** shipped (72h, no training, no personalization) | Aug 2025 | The best consumer privacy lever, new enough to be unknown |
| Gemini drives **Phone, Messages, WhatsApp, Utilities regardless of activity setting**; `Utilities` → `Device assistance` | 2025-07-07 | Breaks the near-universal belief that `Keep Activity` off is a kill switch |
| `Personal context` → **`Personal Intelligence`**; `Gemini Extensions` → `Apps` → **`Connected Apps`**; prior Workspace/Photos connections **reset** | 2025–2026 | Three renames in ~18 months; defaults were reset, so prior audits are stale |
| **Project Mariner shut down**, folded into Spark / Chrome auto browse / AI Mode | ~2026-05-04 (`reported`) | "Mariner" and "Agent Mode" are dead names |
| **Gemini Spark** launched — remote browser + remote computer, requires `Keep Activity` ON | 2026 | New high-risk agentic surface with forced activity logging |
| **`Google Agentspace` → `Gemini Enterprise`** (verified 301) | 2026 | Breaks bookmarks and docs |
| **NotebookLM → `Gemini Notebook`** | 2026-07-16 | The data-region and Vault gaps came with it |
| **Gemini Enterprise admin controls migrated Cloud console → Workspace Admin console**; new top-level `Generative AI` nav | 2026-04-17 | Every documented Gemini admin click path older than April 2026 is wrong |
| **Entire Workspace admin help corpus moved**: `support.google.com/a/*` → `knowledge.workspace.google.com` | ~2026-10-01 | Any tooling pinned to `support.google.com/a/` will break |
| **Vertex abuse-logging 30 → 90 days**; self-serve opt-out removed; form now `/closedform`; invoiced-billing exemption removed | since May 2025 | A 3× retention increase plus loss of the documented opt-out |
| **Vertex AI generative AI → "Gemini Enterprise Agent Platform"**; Cloud docs → `docs.cloud.google.com` | 2026 | The old data-governance page no longer exists |
| **Gemini API ToS rewritten**; Paid status became **project-scoped for API keys** while AI Studio follows the account | effective 2026-03-23 | Creates the key-in-unbilled-project trap |
| **Code Assist individuals / AI Pro / AI Ultra tiers retired**, incl. that login path for Gemini CLI | 2026-06-18 | The old free-tier opt-out toggle no longer exists |
| **Vault retention rules + litigation holds for the Gemini app** GA | June 2026 | Previously search/export only |
| **Data regions support for the Gemini app** GA | 2026-06-29 | Enterprise Plus, Education Plus/Standard, Frontline Plus only |
| **Workspace admin control for Gemini conversation sharing** (link sharing OFF by default) | ~Mar 2026 | The main reason Workspace is safer than consumer |
| **`Gemini Alpha features` → `Gemini Beta features`** (slug still `alpha`) | within window | Label/slug mismatch will confuse searches |
| **Gemini Notebook log events** added to Audit and investigation | Aug 2026 | New audit source |
| **Google Assistant shutdown began** | 2026-09-04 (`reported`) | Makes `Include voice and audio activity` vestigial |
| **Gemini in Chrome shipped to Chrome on Android**, incl. auto browse | June–Aug 2026 | New mobile exposure surface |
| **Agentic Calling (`Call for me`)** | 2026 | Creates third-party call recordings in your Google account |
| **Gem sharing** shipped | Sep 2025 | Instructions *and* knowledge files exposed to recipients |
| Gemini **removed Maps and YouTube as standalone apps** | 2025-10-18 | Folded into the always-on public-data path |

### Live right now — check today

⚠️ **Meet `Automatic note-taking` flipped ON by default on or after 2026-09-21** for Business Standard/Plus, meetings with 3+ guests. **That date has passed.** Any tenant that did not explicitly opt out should be assumed to be auto-note-taking now, and Google documents **no in-meeting participant consent prompt.** The single most urgent item in this file.

### Likely to move next

- **Gems → `skills` migration: November 2026 for personal accounts** (next month), March 2027 Workspace business, June 2027 education. Migration is automatic, skills **auto-apply without explicit invocation**, sharing semantics undocumented. Expect every Gem-sharing recommendation above to need rewriting.
- **Gemini Spark** is new, subscription-gated, excluded from EEA/UK/Switzerland/Nigeria — expect availability, defaults, and the `Keep Activity` coupling to change.
- **`Search Services History`** is a third activity label with no locatable settings page. Expect consolidation or a new control.
- **`Include voice and audio activity`** page is stale (last inline update 2022) and its product is sunsetting.
- The **Vertex ZDR ↔ abuse-monitoring documentation contradiction** is an unresolved doc bug.
- **AI Overviews / AI Mode** remain officially un-disableable; the `udm=14` and `-AI` workarounds are undocumented and could break at any time.

### Honest gaps — do not publish these as fact

1. **Defaults not verified:** `Gemini on lock screen` (both toggles); `Screen context` sub-options; `Hey Google` / Voice Match; `Saved info`; per-toggle Connected Apps states; Web & App Activity and its Chrome-history sub-checkbox; Search personalization; AI Mode `Personal Intelligence`; Gemini Spark and Chrome auto-browse once eligible; Workspace `Gemini Notebook`, `Gemini Enterprise`, `Allow users to share Gems`, `Allow users to delete conversations`, and release track.
2. **Gemini API free-tier retention period is genuinely unpublished.** Do not cite "55 days" or any other figure.
3. **Canvas publish flow:** exact UI labels and the URL path for published Canvas apps were not identified, so the `noindex` question is untested. **Given the documented read-write data exposure, this is the most important remaining gap.**
4. **Gem `Viewer` vs knowledge files:** Google's text says all users with access see uploaded files; a third-party source claims Viewers cannot. Needs a UI test.
5. **`Display over other apps` / Accessibility** — could not confirm Gemini requests either.
6. **Meet AI note-taking participant consent mechanism**, and whether transcription is a separate admin toggle.
7. **CSE** admin click path and default; **Gemini audit log retention period**; the Workspace `Workspace Intelligence` and temporary-chats admin controls (named in the live nav, pages not reachable at inferred slugs).
8. **Jules** — reached via search summary only; re-fetch directly.
9. **Project Mariner shutdown** and the 2026-09-04 Assistant shutdown date — trade press only.
10. **AI Mode share links** — indexing status unverified; the noindex finding covers `gemini.google.com/share/` only.
11. **Export to Docs / Draft in Gmail** — exact UI labels and an explicit "private by default" statement not obtained.

### URL status log

- **404:** `workspace.google.com/learn-more/security/security-whitepaper/` · `cloud.google.com/vertex-ai/generative-ai/docs/learn/data-governance` · `.../learn/request-response-logging` · `developers.google.com/gemini-code-assist/resources/data-governance` · two `knowledge.workspace.google.com` Gemini admin slugs named in the live nav (settings exist, slugs need in-console discovery)
- **301/302:** all `support.google.com/a/answer/*` → `knowledge.workspace.google.com` · all `cloud.google.com/vertex-ai/generative-ai/docs/*` → `docs.cloud.google.com/gemini-enterprise-agent-platform/*` · `cloud.google.com/agentspace` → `cloud.google.com/gemini-enterprise` · `g.co/gemini/share` → `gemini.google.com/share`
- **Closed/dead:** the Vertex abuse-logging opt-out form → `/closedform`
- **Live, verified 200:** `gemini.google.com/sharing` · `gemini.google.com/robots.txt` · all `support.google.com/gemini/*` pages cited
- **Note:** `gemini.google/policy-guidelines/` resolves but contains **only content policy** — no privacy, retention, audio or settings content. The real page is https://support.google.com/gemini/answer/13594961 (last updated **2026-09-24**).
