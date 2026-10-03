# Meta AI (and Muse)

> **Last verified:** 2026-10-02
> **Surfaces covered:** Meta AI assistant (standalone app, Vibes, and in-app on WhatsApp / Instagram / Messenger / Facebook) · **Muse**, Meta's personal AI agent (launched 2026-09-08 — a separate product, *not* a Meta AI rebrand) · Meta AI on Ray-Ban/Oakley AI glasses · Accounts Center · Meta Business Agent · Meta Model API (formerly Llama API)

## Three framing facts that govern everything below

1. **There is no global default for Meta AI.** The US/rest-of-world build and the EU/UK build differ on training objection rights, voice-recording storage, and ad use of AI chats. Every default below is stated per-region or marked `unresolved`.
2. **Human review of Meta AI conversations cannot be turned off anywhere, in any region.** The single most important finding here, and it has no setting attached to it.
3. **Muse has materially better privacy controls than Meta AI does** — a real training opt-out, an ads carve-out, per-connector scoping. Do not generalize Meta AI's weakness onto Muse, or Muse's controls onto Meta AI.

**Verification method note.** Meta's Privacy Center pages (`facebook.com/privacy/genai`, `/privacy/guide/generative-ai/`) are login-gated or render as boilerplate to automated fetch and **returned no control labels**. `faq.whatsapp.com` returns title-only to automated fetch; a direct curl returns WhatsApp's error page. All WhatsApp items are therefore sourced from WhatsApp's blog, `engineering.fb.com`, or fact-checks quoting the FAQ — never from the FAQ itself. The Meta AI memory article resolves to the help-center index rather than the article, so Meta AI's cross-chat memory controls are the weakest-evidenced part of this file.

## 1. Training on your data

The core regional story: **EU/UK/Switzerland/Brazil/Japan/South Korea have a GDPR-style right to object. The US and most of the rest of the world have no training opt-out for Meta AI at all.** Separately, since **2025-12-16**, AI chat content feeds ad targeting with **no opt-out anywhere it applies**.

- **Setting:** "Right to object" *(forms: "I want to object to the use of my information for Meta AI"; "…from third parties for Meta AI"; "I have a different objection…"; plus a separate form for "Your messages with AIs on WhatsApp")*
- **Where:** Facebook/Instagram → Settings & Privacy → Privacy Center → Privacy Topics → **AI at Meta** → bottom of page → "Right to object". Post-deadline form: `https://www.facebook.com/help/contact/6359191084165019`. Third-party-data form: `https://www.facebook.com/help/contact/510058597920541`. **No Privacy Center deep link could be verified** — do not publish those paths as confirmed.
- **Default:** **No objection filed; your public posts are used for AI training.** The form exists only in EU, UK, Switzerland, Brazil, Japan, South Korea. **US/rest-of-world: no opt-out available** — not an oversight to work around, the designed state.
- **Exposes:** Your public Facebook/Instagram posts, captions, comments and public profile information enter Meta's generative-AI training corpus. Private messages between you and other people are excluded by Meta's definition; content *other people* posted that you appear in is not yours to object to.
- **Recommend:** File immediately if you are in a covered region, and file separately for **every** account you hold — objections are per-account and apply to **future** use only. Already-trained data cannot be withdrawn.
- **Risk:** High
- **Evidence:** https://www.facebook.com/legal/eu-ai-terms/ ; https://proton.me/blog/turn-off-meta-ai-facebook — checked 2026-10-02
- **Confidence:** `reported` for exact form labels and the covered-region list; `verified` that EU-specific AI Terms exist as a separate instrument; `unresolved` for every Privacy Center URL

- **Setting:** *(No setting exists)* — use of Meta AI conversations for content and ad personalization
- **Where:** No dedicated control. Meta directs users to Ads Preferences, feed controls, Privacy Center and Accounts Center — **none of which switch this off.**
- **Default:** **On, effective 2025-12-16. No opt-out available.** Notifications began 2025-10-07. Meta's announcement says only that it is rolling out "in most regions" and **never names the exclusions**; third-party reporting consistently names EU, UK and South Korea as excluded at launch. Conversations before 2025-12-16 are excluded.
- **Exposes:** Your voice and text exchanges with Meta AI become ad- and content-targeting signal across Facebook, Instagram and Messenger — and across WhatsApp **only if** you have added your WhatsApp account to the same Accounts Center.
- **Recommend:** The only lever is behavioral — do not discuss anything commercially revealing with Meta AI. The one real control: **keep WhatsApp out of your Accounts Center**, the switch that pulls WhatsApp AI chats into the ad graph.
- **Risk:** High
- **Evidence:** https://about.fb.com/news/2025/10/improving-your-recommendations-apps-ai-meta/ — checked 2026-10-02
- **Confidence:** `verified` for the effective date, absence of opt-out, sensitive-topic carve-out and the Accounts Center mechanic. **`reported` for the EU/UK/South Korea exclusion** — Meta never officially named the excluded regions, which means Meta never officially committed to excluding them.

Meta's committed carve-out, verbatim: *"When people have conversations with Meta AI about topics such as their religious views, sexual orientation, political views, health, racial or ethnic origin, philosophical beliefs, or trade union membership, as always, we don't use those topics to show them ads."*

- **Setting:** Human review of AI interactions — *(no setting exists)*
- **Where:** Nowhere. Governed by the Meta AI Terms of Service.
- **Default:** **On, all regions, no opt-out available.** Both the global and EU terms (effective **2026-05-13**) carry identical language: *"In some cases, Meta will review your interactions with AIs, including the content of your conversations with or messages to AIs, and this review can be automated or manual (human)."*
- **Exposes:** Any conversation with Meta AI on any surface may be read by a Meta employee or contractor.
- **Recommend:** Treat every Meta AI conversation as reviewable by a stranger. **There is nothing to toggle. This is the finding, not a gap in the research.**
- **Risk:** High
- **Evidence:** https://www.facebook.com/legal/ai-terms ; https://www.facebook.com/legal/eu-ai-terms/ — checked 2026-10-02
- **Confidence:** `verified`

Context worth carrying: Swedish press reported in 2026 that workers at a Kenya-based subcontractor reviewed Ray-Ban Meta customer footage including intimate content, and the BBC found Meta's claimed face-blurring during review unreliable. A US class action (Bartone v. Meta / Canu, Clarkson Law Firm, March 2026) targets the marketing line *"designed for privacy, controlled by you."* `reported`.

- **Setting:** "Help improve our AI models" **(Muse only)**
- **Where:** Muse → Settings → **Data controls** → toggle off → confirm via "Turn off to confirm"
- **Default:** **On.** Meta states this explicitly. Changes **also apply to previous interactions** — a genuinely retroactive opt-out, which is unusual. US/Canada only, because Muse is US/Canada only.
- **Exposes:** Your Muse conversations and tool-call trajectories are used to develop Meta's AI models; Meta says it strips names, email addresses, phone numbers and SSNs and disassociates interactions from your account first.
- **Recommend:** **Off, at setup.** It is retroactive, costs nothing functionally, and is the only real training opt-out Meta offers a US consumer.
- **Risk:** Medium (High if left on)
- **Evidence:** https://www.meta.com/help/artificial-intelligence/2225571704857152/ ; https://research.meta.ai/blog/security-and-safety-for-ai-agents-our-approach-with-muse — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Store visual data from AI experiences" **(AI glasses)**
- **Where:** Meta AI app → your glasses' settings → Meta AI → scroll → **Store visual data from AI experiences**. Glasses must be out of the case and connected; **repeat per pair**.
- **Default:** **On (opt-out model)** — `reported`. Meta's own article does not state the default. No regional carve-out documented.
- **Exposes:** Images and video from AI experiences — "live AI and other multimodal AI features" — are stored and used to improve Meta AI, and Meta says the process "may be automated or manual (human)." Excluded: media captured with the capture LED on, voice interactions, and content shared to Messenger/Instagram.
- **Recommend:** **Off.** With it off, Meta states visual data *"will not be stored after completing your request"* and *"will not be available for human review."* Highest-value single flip on the device.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/ai-glasses/1381548946634724/ ; https://www.engadget.com/2269454/how-to-stop-meta-training-its-ai-models-on-your-smart-glasses-visual-data/ — checked 2026-10-02
- **Confidence:** `verified` for the setting and behavior; `reported` for the default

- **Setting:** "Allow people to reuse your content on Instagram and with AI features at Meta"
- **Where:** Instagram → Profile → Menu → **Sharing and reuse**
- **Default:** **On.** Rolled out starting in the US; wording varies by app version. **The worst live default found anywhere in this file.**
- **Exposes:** Strangers can reference your public Instagram account by @-mention inside a Meta AI image prompt and generate imagery using your likeness. The specific generation feature was pulled after backlash in July 2026 — **the permission grant remained.**
- **Recommend:** **Off.** A standing, open-ended grant over "AI features at Meta" whose future scope you cannot see. Meta kept the grant after killing the feature it was built for.
- **Risk:** High
- **Evidence:** https://www.malwarebytes.com/blog/ai/2026/07/turn-off-this-meta-setting-before-someone-generates-ai-images-of-you ; removal confirmed https://techcrunch.com/2026/07/10/meta-removes-controversial-ai-feature-on-instagram-after-backlash/ — checked 2026-10-02
- **Confidence:** `reported` for label/path/default; `verified` that the feature was withdrawn

- **Setting:** "Activity from other businesses" *(renamed from "Activity information from ad partners")*
- **Where:** Accounts Center → Ad preferences. https://www.facebook.com/help/1455040619735222/
- **Default:** **On.** Took effect in the US and a number of other countries in July 2026, more to follow. Meta discontinued the separate "Your activity off Meta technologies" setting entirely.
- **Exposes:** Data businesses share with Meta about your off-Meta activity now personalizes not only ads but, in Meta's words, *"the content you see in your Feed and AI responses"* — this control now reaches into what Meta AI says to you.
- **Recommend:** **Off.** The one setting that visibly expanded its blast radius into AI output in the last year, while Meta removed the narrower control beside it.
- **Risk:** Medium
- **Evidence:** https://about.fb.com/news/2026/06/better-personalization-and-changes-to-controls-for-your-activity-from-other-businesses/ — checked 2026-10-02
- **Confidence:** `verified` for the rename, discontinuation and AI-responses expansion; `unresolved` for the toggle's out-of-box state

- **Setting:** Camera roll media and AI training
- **Default:** **Not used for training.** Meta, verbatim: *"We don't use photos and videos from your camera roll to improve AI at Meta unless you choose to publish or share them in interactions with any AI at Meta feature, such as Meta AI."*
- **Exposes:** Nothing for training at default — but see §10, because the photos are still uploaded.
- **Recommend:** Do not paste camera-roll images into Meta AI; that is the act that converts them into training data.
- **Risk:** Low *(for training specifically)*
- **Evidence:** https://about.fb.com/news/2026/04/now-rolling-out-facebooks-opt-in-camera-roll-suggestions-in-the-eu-and-uk/ — checked 2026-10-02
- **Confidence:** `verified`

## 2. Memory, history & personalization

**The weakest-documented category.** Meta's memory help article does not resolve, and the Meta AI app's own "Manage your information" screen contains **no memory control at all** — verified directly.

- **Setting:** Meta AI cross-chat memory ("memories") — exact toggle label **unresolved**
- **Where:** Per Meta's help copy, managed "from anywhere you're chatting with it" — **not** from a central settings screen. Verified: Meta AI app → Menu → Settings → Data & privacy → **Manage your information** offers only three options (export your information, remove all public vibes, delete all chats and media) and **no memory management**.
- **Default:** **On, with cross-account merging when accounts share an Accounts Center.** Meta: saving or deleting a memory in one place "saves or deletes them everywhere"; removing an account from the Accounts Center means Meta will "stop combining new memories after you remove an account." Personalized responses launched US and Canada only. **Whether memory can be disabled wholesale is `unresolved`** — no off switch found, and no official statement that one exists.
- **Exposes:** A detail volunteered to Meta AI in an Instagram DM persists and resurfaces when you chat with Meta AI in WhatsApp, if both accounts sit in one Accounts Center.
- **Recommend:** Do not add WhatsApp to your Accounts Center; audit and delete memories from within a chat periodically. **Do not promise anyone they will find a memory off switch** — verify in-app.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1771195753735844/ (verified absence) — checked 2026-10-02
- **Confidence:** `verified` that no memory control exists in "Manage your information"; `reported` for cross-account behavior; `unresolved` for label, default, and whether an off switch exists

- **Setting:** "Memory" **(Muse)** — backed by an editable `Memory.md` file
- **Where:** Muse → Assistant icon → **Identity** → **Memory**. Directly editable as a file.
- **Default:** **On.** `unresolved` whether it can be disabled outright as opposed to edited and cleared. You can also tell Muse to "forget" specific things.
- **Exposes:** Muse retains learned facts across sessions, including information drawn from connected services. Meta warns that after you delete something, *"Muse may still remember information it learned from what you deleted."*
- **Recommend:** Read `Memory.md` after any substantial task — the rare case where an AI's memory is a plain-text file you can audit line by line. Prune aggressively.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/artificial-intelligence/2225571704857152/ — checked 2026-10-02
- **Confidence:** `verified` for path and file; `unresolved` for a disable toggle

- **Setting:** Accounts Center account linking
- **Where:** Accounts Center → add/remove accounts
- **Default:** Depends on account history. Meta: *"if you've added your Facebook and Instagram accounts to the same Accounts Center, Meta AI can draw from both."*
- **Exposes:** Cross-app profile and engagement history shapes Meta AI's answers — **and** it is the mechanism that pulls WhatsApp AI chats into ad targeting post-Dec 2025.
- **Recommend:** **Keep WhatsApp unlinked.** The highest-leverage control a Meta AI user actually has, and the only one that meaningfully constrains the Dec 2025 ads change.
- **Risk:** Medium
- **Evidence:** https://about.fb.com/news/2025/10/improving-your-recommendations-apps-ai-meta/ — checked 2026-10-02
- **Confidence:** `verified`

**Notable absence, verified.** Meta's official Accounts Center inventories of cross-account settings list birthday, ad preferences, ad topics, payment info, password/security, contacts upload and off-Meta activity — and **mention no AI control of any kind.** The Accounts Center is where Meta says memory syncs, but it is not where Meta lets you manage it.

## 3. Connectors & OAuth scopes

Almost all of this is **Muse**, and it is the best-designed permission surface Meta ships. Meta AI proper has no connector platform; the glasses have a narrow one.

- **Setting:** "Connectors"
- **Where:** Muse → Settings → **Connectors** → Connect next to a service → Continue to authorize. Or say "Connect my Gmail".
- **Default:** **Nothing connected, except** Facebook, Instagram and Threads, which **auto-connect** if those accounts share the same Accounts Center. Everything else is explicit opt-in, one at a time. US/Canada only.
- **Exposes:** At default, three Meta services. Each connector grants a cloud-resident agent standing access to that service's data — email, calendar, health, files, shopping, payments.
- **Recommend:** Connect the minimum, and **remove the three auto-connected Meta connectors** if you did not ask for them — they are the only ones you never consented to individually.
- **Risk:** High *(scope, not design)*
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1687253048996149/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Read vs. write scope per connector — "Read only" / "Read and interact"
- **Where:** Muse → Settings → **Permissions** → Manage permissions → Connectors; also per-service during setup
- **Default:** `unresolved` per connector. Meta's framing: *"For things like email, people choose what Muse can do, whether it reads their mail or can also send on their behalf"* and *"Muse will not take many important actions, like sending an email, without your approval."*
- **Exposes:** At read-write, Muse can send mail, post and transact as you without a human in the loop for anything not classed "important."
- **Recommend:** **Read-only on email, calendar and files.** The word "many" in "will not take many important actions" is doing a lot of work — do not rely on the approval gate to catch everything.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1687253048996149/ ; https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/ — checked 2026-10-02
- **Confidence:** `verified` for the model; `unresolved` for per-connector defaults

- **Setting:** Global approval mode — "Ask for some actions" / "Always ask"
- **Where:** Muse → Settings → **Permissions**. Per-action choices at prompt time: Allow once / Allow for this task / Allow for this site / Always allow / Deny.
- **Default:** **"Ask for some actions"** (asks before writes and important reads) — `reported`; Meta's help text describes the behavior without naming the default.
- **Exposes:** At default, routine reads and some writes proceed unprompted.
- **Recommend:** **"Always ask."** Accept the friction; this is an agent holding your credentials and a payment method.
- **Risk:** High
- **Evidence:** behavior corroborated at https://www.meta.com/help/artificial-intelligence/1687253048996149/ — checked 2026-10-02
- **Confidence:** `reported` for option labels and default; `verified` that a configurable approval setting exists

- **Setting:** Custom connectors
- **Where:** Muse → Settings → Connectors → Muse walks you through it, "which can involve retrieving API information". Credentials go to the Secure Credentials Store.
- **Default:** None configured.
- **Exposes:** Whatever the third-party API exposes. Meta states plainly: **"Meta doesn't review custom connectors."**
- **Recommend:** Avoid. An unreviewed connector is an unaudited data path out of an agent that holds your mail and money.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1687253048996149/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "File System Access" **(Muse on Mac)** — per-app: Off / Read only / Read and interact
- **Where:** Muse → Settings → **File System Access**. Underlying macOS grants: **Full Disk Access**, **Automation**, **Notifications**. Also revocable at macOS System Settings → Privacy & Security.
- **Default:** Configured during setup per app; `unresolved` which state is pre-selected.
- **Exposes:** With Full Disk Access the agent can find, read and update files anywhere on the machine; with Automation it can drive local apps. Meta notes interactions *"may include screenshots of your screen."*
- **Recommend:** **Off for everything not actively needed, and never "Read and interact" on a messaging app.** Full Disk Access to a cloud-backed agent is the single broadest grant in this entire file.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1126304576638594/ — checked 2026-10-02
- **Confidence:** `verified` for labels and macOS grants; `unresolved` for the default selection

- **Setting:** "Connected apps" *(AI glasses music services)* and the Muse Spotify connector
- **Where:** Glasses — Meta AI app → Connected apps → Spotify, or Glasses → Device settings → Apps → Amazon Music. Muse — Settings → Connectors → Spotify (announced 2026-09-23).
- **Default:** Not connected.
- **Exposes:** Glasses: playback control and library access. Muse Spotify: playback, library writes, playlist creation, Personal Podcast generation, and calendar-triggered scheduled playback — a write grant on your music account tied to your calendar.
- **Recommend:** Low-stakes relative to everything else here. Read-only if offered.
- **Risk:** Low–Medium
- **Evidence:** https://www.meta.com/help/ai-glasses/1378872149701658/ ; https://newsroom.spotify.com/2026-09-23/spotify-meta-muse-agent/ — checked 2026-10-02
- **Confidence:** `verified` that the connectors exist; `unresolved` for OAuth scopes granted

## 4. Sharing & publication defaults

### The 2025 Discover incident, and what is true now

Meta AI launched 2025-04-29 with a public **"Discover"** feed. Meta's launch post claimed "nothing is shared to your feed unless you choose to post it" — technically true, but the share flow did not make the audience legible. On 2025-06-12 TechCrunch published *"The Meta AI app is a privacy disaster,"* whose central finding was: *"Meta does not indicate to users what their privacy settings are as they post, or where they are even posting to."* Users who signed in via a **public Instagram account** had their AI prompts become public. Security researcher Rachel Tobac surfaced home addresses and court details and called it *"a UX failure that weaponizes convenience."* Reported content included tax-evasion questions, medical and legal matters, and character-reference letters naming real people in full. Meta added a warning interstitial above "Post to feed" — `reported`; that text is no longer in Meta's live help pages.

**Current state, verified 2026-10-02: the word "Discover" appears nowhere in Meta's live help documentation.** The public feed is now officially "the Meta AI and Vibes feed"; shared items are "public vibes" on a "public Meta AI or Vibes profile." Vibes launched 2025-09-25, reached Europe 2025-11-06, and has been tested as a standalone app since Feb 2026. The feed is now media-centric rather than prompt-centric. **Meta never published a deprecation notice for Discover**, and one Feb 2026 third-party article still referenced a "Discover Feed" — so the honest statement is *the name is gone from official documentation and the feed is now Vibes-centric*, not *Meta removed Discover*. `unresolved` whether a distinct text-prompt tab survives in any build or region. **No FTC or DPA action specific to the Discover feed was located**; the one FTC complaint found (EPIC-led, reportedly 36 groups) targets the AI-chat-to-ads practice instead.

- **Setting:** "Post" *(to the Meta AI and Vibes feed)*
- **Where:** Meta AI app → tap your generated image/video in the thread → **Post**. For chats: Share → preview interstitial → Post to feed.
- **Default:** **Not shared.** Nothing is public until you tap Post — verified in Meta's current help text. No regional difference in the mechanism; Vibes availability differs by region.
- **Exposes:** At default, nothing — but one tap publishes to a feed any Meta AI/Vibes user can browse, attached to your public profile, with no expiry.
- **Recommend:** Never use it on anything derived from a real conversation. The default is correct; the 2025 failure was the preview screen, and preview screens change without notice.
- **Risk:** High *(consequence)* / Low *(default)*
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1337455336906126/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Share a link" / "Delete link"
- **Where:** Meta AI app → open conversation → More (⋯, top right) → **Share a link** → Copy link. To revoke: Menu (top left) → select the conversation under Chats → Menu (top right) → **Delete link**.
- **Default:** No link exists until you create one.
- **Exposes:** A **non-expiring, freely re-shareable public URL** snapshotting the conversation. Meta states it outright: *"The link doesn't expire and people can share the link,"* and warns *"Be mindful when sharing a link to a conversation if you've discussed personal information or circumstances with Meta AI."*
- **Recommend:** Treat every link as permanent publication; delete the **link**, not just the chat, when done. This is the 2025 failure mode in a new wrapper — unbounded lifetime, no access control, no revocation reminder.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1382777929673771/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Remove all public vibes"
- **Where:** Meta AI app → Menu → Settings → Data & privacy → Manage your information → **Remove all public vibes** → Remove all
- **Default:** N/A — one-time action.
- **Exposes:** Nothing; remediation. **Note the catch:** Meta says the media stays in your Media section and you can "choose to repost them later" — this removes from the feed, it does not delete.
- **Recommend:** Run once if you used the app in 2025, then follow with "Delete all chats and media."
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/artificial-intelligence/2457110494637611/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Make all your prompts visible to only you" / "Suggesting your prompts on other apps"
- **Default:** N/A / `unresolved`
- **Recommend:** Use if present in your build — but **neither label appears in Meta's live help docs any more**; that menu now shows only export / remove all public vibes / delete all chats and media. They appear superseded by "Remove all public vibes," likely removed with the text-prompt feed. **Do not promise anyone they will find them.**
- **Risk:** Medium
- **Evidence:** 2025-era secondary reporting only — checked 2026-10-02
- **Confidence:** `unresolved`

- **Setting:** "@Meta AI" in WhatsApp group chats
- **Where:** Type `@Meta AI` in any group thread.
- **Default:** **Available in groups by default.** Per WhatsApp's stated position, Meta AI receives and responds **only** to messages that directly address it — a DM to Meta AI or an `@Meta AI` mention. It does **not** read all messages in a private or group chat; other messages remain end-to-end encrypted.
- **Exposes:** The specific @-mentioning message leaves E2EE and goes to Meta. **The real group risk is social, not cryptographic:** any single member can pull a slice of the thread out of encryption, and the others get no veto.
- **Recommend:** For any group where confidentiality matters, enable Advanced Chat Privacy and have an admin lock it.
- **Risk:** Medium
- **Evidence:** WhatsApp's position as quoted at https://english.factcrescendo.com/2026/09/30/meta-ai-reading-whatsapp-private-chats-advanced-chat-privacy-fact-check/ — checked 2026-10-02
- **Confidence:** `reported`. Attribute as "per WhatsApp's help centre as quoted by," never "per the FAQ" — the FAQ is not machine-readable.

- **Setting:** "Advanced Chat Privacy"
- **Where:** Open the chat or group → tap the contact or group name at the top → scroll to **Advanced Chat Privacy** → toggle on. **Per-chat, not global.** In groups, Group info → Group permissions → Edit group settings controls whether all members or **admins only** can change it.
- **Default:** **Off.** Must be enabled chat by chat.
- **Exposes:** At default, any participant can export the chat, auto-download its media, and pull its content into AI features.
- **Recommend:** **On** for every client, legal, medical or financial group, and restrict the setting to admins. Per WhatsApp's announcement it blocks three things: exporting chats, auto-downloading media to the recipient's phone, and *"using messages for AI features."* **Get the nuance right:** it does not stop Meta AI from "reading" your chats, because Meta AI does not read them by default — it stops **participants** from feeding that chat into AI features. A Sept 2026 fact-check specifically debunked the inflated version of this claim.
- **Risk:** Medium (Low once enabled)
- **Evidence:** https://blog.whatsapp.com/introducing-advanced-chat-privacy ; corroborated at https://engineering.fb.com/2025/04/29/security/whatsapp-private-processing-ai-tools/ — checked 2026-10-02
- **Confidence:** `verified` for the three blocked behaviors and the enable path; `reported` for the admin-restriction path

- **Setting:** Prompt sharing with generated media
- **Default:** Meta's AI Disclosures (effective **2025-11-19**) state that when you share generated media with others, *"your prompt may also be shared with those users."*
- **Exposes:** The text you typed travels with the image — including anything personal you used to steer it.
- **Recommend:** Assume your prompt is part of the artifact. Write prompts you would be willing to publish.
- **Risk:** Medium
- **Evidence:** https://www.facebook.com/legal/meta-AI-disclosures/ — checked 2026-10-02
- **Confidence:** `verified`

## 5. Retention & deletion

The governing caveat, from the Meta AI Terms of Service (effective **2026-05-13**), applies to everything in this section: *"deleting individual messages, entire threads, or even your account may not delete our copy of your personal information."* And: *"When information is shared with AIs, the AIs will sometimes retain and use that information. Do not share information that you don't want the AIs to use and retain."*

- **Setting:** "Delete all chats and media" **(Meta AI app)**
- **Where:** Meta AI app → Menu → Settings → Data & privacy → Manage your information → **Delete all chats and media**
- **Default:** N/A — one-time action. History is retained until you act.
- **Recommend:** Run it if you have 2025-era history, paired with "Remove all public vibes." Understand that it governs your copy, not necessarily Meta's.
- **Risk:** Low
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1771195753735844/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Reset" **(Muse)**
- **Where:** Muse → Settings → Data Controls → **Reset** → confirm. Per-conversation: Chats tab → select chat → three-dot menu → Delete. Per-message: tap and hold → Delete.
- **Default:** N/A. Meta warns *"Resetting Muse cannot be undone"*; it removes all chat history, files and active tasks.
- **Exposes:** Nothing; remediation. **But:** *"After you delete something from Muse, Muse may still remember information it learned from what you deleted."*
- **Recommend:** Use Reset when decommissioning; for routine hygiene prune `Memory.md` directly, because deleting chats does not reliably remove what was learned from them.
- **Risk:** Low
- **Evidence:** https://www.meta.com/help/artificial-intelligence/2225571704857152/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Voice activity log" **(AI glasses)**
- **Where:** Meta AI app → Glasses (top right) → Device settings → tap your glasses → scroll → **Glasses privacy** → **Voice activity log**
- **Default:** Populated. **In the US this is the only control over voice data that remains** (see §6).
- **Exposes:** The inventory of what Meta already holds — stored transcripts, audio recordings and related data, processed "using machine learning and trained reviewers."
- **Recommend:** Delete everything, on a recurring schedule. Export via Download Your Information first if you want a copy.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/ai-glasses/1129552064459382/ — checked 2026-10-02
- **Confidence:** `verified`

### Verified retention periods

From https://www.meta.com/legal/ai-glasses/voice-controls-privacy-notice/ , effective 2025-07-22:

| Data | Retention |
|---|---|
| Intentional voice interactions (recordings + transcripts) | **Up to one year** |
| Misfires ("false wakes" / misactivations) | **Deleted within 90 days** |
| Voice recordings where storage is off (EU/UK; Ray-Ban Stories all regions) | **Deleted immediately** after processing |
| Cloud media (glasses photos/videos) | **30 days**, then auto-deleted |
| Camera-roll uploads after you turn cloud processing off | Meta "will begin to remove" them "after 30 days" |
| Download-your-information export | Up to **30 days** to produce; **4 days** to download |

- **Setting:** `/reset-ai` **(WhatsApp)**
- **Default:** N/A — a command, not a setting.
- **Recommend:** **Cannot responsibly recommend — existence could not be verified.** `faq.whatsapp.com` is unreadable to automated fetch; WABetaInfo returned nothing; search budget exhausted before a corroborating source was reached. **Do not publish `/reset-ai` as a verified control.**
- **Risk:** Cannot rate
- **Evidence:** none — checked 2026-10-02
- **Confidence:** `unresolved`

- **Setting:** "Export your information"
- **Where:** Meta AI app → Menu → Settings → Data & privacy → Manage your information → Download your information → **Export your information** → Create export → select profile → Next → choose destination → Start export
- **Default:** N/A. Covers "Meta AI app, Meta.ai website, Vibes app, Meta AI glasses." HTML or JSON; custom date ranges. **Excludes content you already deleted.**
- **Recommend:** Export **before** any bulk deletion — the export excludes deleted content, so the order matters.
- **Risk:** Low
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1314808549771571 — checked 2026-10-02
- **Confidence:** `verified`

## 6. Voice, audio & camera

### The 2025 change, verified

On **2025-04-29** Meta emailed Ray-Ban Meta owners with two simultaneous changes. First, **the voice-recording-storage opt-out was deleted** — Meta's notice, as quoted by PetaPixel: *"The option to disable voice recordings storage is no longer available."* Second, **"Meta AI with camera" was switched on by default.** The same day Meta renamed Meta View to the Meta AI app and "automatically migrat[ed] your existing media and device settings," so anyone who had previously set voice storage off was migrated into the new regime. The EU was not covered — **and that regional split is still live today**, confirmed by reading the three regional notices side by side.

- **Setting:** Voice recording and transcript storage **(AI glasses)**
- **Where:** **US/rest-of-world: there is no setting.** Review and delete only, via Voice activity log (§5). **UK/EU:** a voice-storage setting exists but **no help article naming its label or path could be located** — `unresolved`.
- **Default:** **Region-split, both sides verified.** **US/rest-of-world:** *"Text transcripts and audio recordings of your voice interactions are stored by default to help improve Meta's products"* for Ray-Ban Meta and Oakley Meta — **no opt-out available.** **UK and Ireland/EU:** *"You can choose to store your voice recordings… You can turn voice storage off in settings at any time,"* plus *"Even with voice recording storage off, you can still use the Meta AI service."* **Ray-Ban Stories (2021 gen-1):** opt-out preserved in **all** regions — the toggle was removed only for the current products.
- **Exposes:** In the US, every "Hey Meta" utterance plus whatever background audio rides along is uploaded, transcribed, retained up to one year, and made available to Meta's trained human reviewers.
- **Recommend:** **US:** turn off "Hey Meta" — the only way to stop the inflow — then purge the Voice activity log on a schedule. **UK/EU:** set voice storage off.
- **Risk:** High
- **Evidence:** https://www.meta.com/legal/ai-glasses/voice-controls-privacy-notice/ ; https://www.meta.com/gb/legal/ai-glasses/voice-controls-privacy-notice/ ; https://www.meta.com/ie/legal/ai-glasses/voice-controls-privacy-notice/ ; https://petapixel.com/2025/05/01/meta-updates-smart-glasses-policy-to-expand-ai-data-collection/ — checked 2026-10-02
- **Confidence:** `verified` for defaults and the regional split; `unresolved` for the EU/UK toggle's UI label

**Human review of voice, verified.** Meta uses *"trained reviewers"* to assess recordings across "speech patterns, phrases, local dialects, and accents," via "controlled and monitored systems," and **changes the pitch of recordings when they are reviewed.** There is **no opt-out from review itself** in any region.

- **Setting:** "Hey Meta" *(inside "Hey Meta" preferences)*
- **Where:** Meta AI app → Glasses → Device settings → your glasses → Meta AI → **"Hey Meta" preferences** → toggle beside **Hey Meta**
- **Default:** **On** — `reported`. The *path* is verified on meta.com; the toggle's own label and default are not documented by Meta.
- **Exposes:** Keeps the mics listening for the wake word; every triggered interaction ships audio and a transcript to Meta, where (US) it is stored up to a year and is human-reviewable — and it is what keeps "Meta AI with camera" live, since there is no separate camera-AI toggle.
- **Recommend:** **Off.** The one switch that collapses the whole voice-plus-camera-AI path. You can still summon Meta AI by tap-and-hold on the touchpad.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/ai-glasses/899314785056676/ (path) — checked 2026-10-02
- **Confidence:** path `verified`; label and default `reported`

- **Setting:** Respond without "Hey Meta"
- **Where:** Meta AI app → Glasses → Device settings → your glasses → Meta AI → "Hey Meta" preferences → toggle beside **Respond without "Hey Meta"**
- **Default:** **On by default** — Meta states this explicitly. No documented regional variation.
- **Exposes:** After any request *"your microphone will stay on after each request you make and will turn off automatically if you don't make an additional request after a little while"* — so anything you or anyone nearby says in that trailing window can be captured and uploaded as a follow-up turn.
- **Recommend:** **Off.** An open-mic window you did not ask for; say the wake word each time instead.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/ai-glasses/899314785056676/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Cloud media" *(the autocapture article calls the same control "Cloud media processing" — label inconsistency inside Meta's own docs)*
- **Where:** Meta AI app → Glasses → Device settings → your glasses → swipe down → **Glasses privacy** → toggle beside **Cloud media**
- **Default:** **On** — `reported`; Meta's article states no default. `unresolved` officially.
- **Exposes:** Photos and videos leave the glasses for Meta's servers and are *"temporarily stored in the cloud for 30 days before being automatically deleted"* — triggered by something as ordinary as "Hey Meta, send a photo."
- **Recommend:** **Off.** Keeps captures on device and phone. Cost: voice-driven sharing and autocapture stop working.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/ai-glasses/734190441863923/ — checked 2026-10-02
- **Confidence:** setting and 30-day retention `verified`; default `reported`

- **Setting:** "Share additional data" *(Meta's help article never names the toggle)*
- **Where:** Meta AI app → Glasses → Device settings → your glasses → scroll → **Glasses privacy**
- **Default:** **On** — `reported`. Meta says only that you "can choose to share Additional Data from your devices during initial setup" and "can change this choice at any time in settings." Officially `unresolved`.
- **Exposes:** "Information about how you use your AI Glasses and Wrist Devices" — telemetry and usage, governed by the Supplemental Meta Platforms Technologies Privacy Policy (effective 2026-06-29). Meta is explicit that it "does not include the photos and videos captured by your glasses."
- **Recommend:** **Off.** Pure product-analytics donation; nothing you use breaks.
- **Risk:** Low–Medium
- **Evidence:** https://www.meta.com/help/ai-glasses/483508126732797/ — checked 2026-10-02
- **Confidence:** label and default `reported`; the definition of "Additional Data" `verified`

- **Setting:** Live AI — **no persistent toggle exists**
- **Where:** Voice-initiated: "Hey Meta, start live AI" / "Stop live AI" / "Pause live AI" (single tap to pause, tap-and-hold to end). Transcripts at Meta AI app → hamburger → Chats. Its stored output is governed by "Store visual data from AI experiences."
- **Default:** Off until invoked. "currently available in English and will be rolling out over time in the US and Canada."
- **Exposes:** Meta states plainly: *"Your glasses camera and microphone are continuously active during the session."* With visual-data storage on, that continuous stream is retained and human-reviewable.
- **Recommend:** Avoid. If used, turn off visual-data storage first and **end** sessions rather than pausing. **Whether the capture LED stays lit during live AI is not documented** — `unresolved`, and the question most worth answering before using this.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/ai-glasses/894093646030348/ — checked 2026-10-02
- **Confidence:** `verified`, except LED behavior

- **Setting:** Autocapture
- **Where:** "Hey Meta, start autocapture"; optional auto-start via Glasses settings → App connections → Garmin. Requires Cloud media processing enabled.
- **Default:** **Not enabled by default** — must be started manually or wired to Garmin.
- **Exposes:** Records clips hands-free and, per Meta, *"Meta AI captures a continuous series of low-resolution images (similar to Live AI)"* for context, with cloud processing.
- **Recommend:** Leave off and do not connect Garmin auto-start — a continuous-capture mode that can begin without a deliberate per-session command.
- **Risk:** Medium–High
- **Evidence:** https://www.meta.com/help/ai-glasses/1824727564872648/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Capture LED — **no opt-out available**
- **Where:** Hardware. Not in settings.
- **Default:** Always active, cannot be disabled. "Whenever content is being captured for your gallery, this white light blinks." Tamper detection added: if the LED is covered or damaged, "the camera automatically disables itself."
- **Exposes:** A bystander protection, not a user setting. **Important limit:** Meta's visual-data article explicitly *excludes* LED-on captures from "visual data" — implying AI reads of the camera are a separate, differently-signalled path.
- **Recommend:** Nothing to change. Know that **the LED does not reliably signal AI camera use.**
- **Risk:** Low *(wearer)* / High *(bystanders)*
- **Evidence:** https://www.meta.com/ai-glasses/privacy/ ; https://about.fb.com/news/2026/07/metas-ai-glasses-your-questions-answered/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "Ready to talk" **(Meta AI app voice mode)**
- **Where:** Meta AI app → Menu → Settings → under Meta AI settings
- **Default:** **Off.** Meta: *"If you prefer to have voice on by default, there's a control in your settings to toggle the Ready to talk feature on."* The rare Meta voice default that is already the private one.
- **Exposes:** At default, nothing — the mic is not hot. Enabled, the app opens listening, so whatever is audible at launch is captured and sent to Meta.
- **Recommend:** Leave off.
- **Risk:** Low at default / High if enabled
- **Evidence:** https://about.fb.com/news/2025/04/introducing-meta-ai-app-new-way-access-ai-assistant/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Face and voice enrollment for Meta AI media features
- **Where:** Deletion path: Meta AI settings on Instagram, WhatsApp, Messenger or the Meta AI app — "deleting the photos of yourself and the voice recording."
- **Default:** Not enrolled; opt-in by providing media. Meta AI Disclosures effective 2025-11-19.
- **Exposes:** Images, videos and voice recordings you provide, plus your prompt instruction, used to evaluate AI performance and meet compliance obligations. **Note the terms include an express waiver of claims under Illinois BIPA and the Texas Capture or Use of Biometric Identifier Act** — a biometric-rights waiver attached to a consumer feature.
- **Recommend:** Do not enroll. If you have, delete the enrolled photos and voice recording. Meta's own fallback: "You can always choose not to use these features."
- **Risk:** High
- **Evidence:** https://www.facebook.com/legal/meta-AI-disclosures/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Facial recognition on glasses
- **Where:** **No user-facing facial-recognition setting found** in any Meta help or legal page read.
- **Default:** `unresolved` — asserting nothing either way.
- **Exposes:** Adjacent verified concern: the BBC reported Meta's claimed face-blurring during human review "did not consistently work," so face data reaches reviewers regardless.
- **Recommend:** No action available. If Meta ships such a setting it will land under Glasses privacy and will be the highest-risk toggle on the device.
- **Risk:** Cannot rate
- **Confidence:** `unresolved`

- **Setting:** Media auto-import from glasses
- **Default:** **Conflicting sources.** Meta's help article describes user-initiated import; **EFF states footage "imports automatically by default into the Meta AI mobile app."** These could not be reconciled.
- **Recommend:** Check on-device whether an auto-import toggle exists in your build, and clear the app cache after imports.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/ai-glasses/1427588664906909/ vs https://www.eff.org/deeplinks/2026/03/think-twice-buying-or-using-metas-ray-bans — checked 2026-10-02
- **Confidence:** `unresolved`

**Also noted:** **Muse Charm**, a pocket-sized device with real-time voice, announced at Connect 2026-09-24. No privacy settings documented. `unresolved`.

## 7. Agentic / computer-use permissions

**Not "none identified" — the opposite.** Meta shipped a full computer-use agent three weeks before this check. **Muse** launched **2026-09-08** for US adults on iOS, Android and web, expanded to **US and Canada** 2026-09-29, powered by Muse Spark. Free tier plus Power (USD 20/mo) and Maximum (USD 100/mo). It opens browsers, fills forms, sends email, books travel, negotiates, checks out via "Link built by Stripe", **has its own email address**, and **keeps working after you close the app.**

Architecture, verified from Meta's research blog: a **Muse Secure VM** running the agent in a `systemd-nspawn` runtime cell where "root inside the runtime cell is mapped to an unprivileged host user so runtime cell root is not host root." Outside sit `hatch-safety` (independent inspection models), `privsep` workers, `hatch-authd` (credentials), and **Sentinel** — "the sole permission authority for approval to perform actions with connectors to third-party services and for all egress over the network," deciding allow / denied / ask and evaluating "the hostname, the resolved and final destination IP address, the port, protocol, HTTP method, path." Credentials use **just-in-time insertion** with the agent seeing only **surrogate** tokens. Prompt-injection defenses include model-level training, labeling external data as "untrusted input," and "an ensemble of multiple prompt injection detection classifiers."

- **Setting:** "Web access default setting"
- **Where:** Muse → Settings → Permissions → **Web access default setting**
- **Default:** `unresolved` — Meta documents the setting's existence and that Muse "asks you to confirm before it takes certain important actions in the browser, like making a purchase," but does not state the shipped default.
- **Exposes:** A cloud-resident browser holding your logged-in sessions, navigating and transacting on your behalf while you are not watching.
- **Recommend:** Most restrictive option available, and use the in-chat controls actively: "Open browser in the chat" to watch, "Take control of the browser" to pause Muse, "Stop the task" to kill it.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/2124746764949121/ — checked 2026-10-02
- **Confidence:** setting and controls `verified`; default `unresolved`

- **Setting:** Pre-action confirmation and audit trail
- **Where:** Inline approval prompts. Per-action options: Allow once / Allow for this task / Allow for this site / Always allow / Deny.
- **Default:** **On for "important actions."** Meta: *"Muse checks with the person before sensitive actions like sending an email or making a purchase"* and *"Muse shows people a complete audit trail of everything it has done and plans to do."* For small business: *"nothing publishes, sends, or spends without your approval."*
- **Exposes:** Actions **not** classed important proceed without asking — and Meta's own phrasing is that Muse "will not take **many** important actions" without approval, which is not the same as all.
- **Recommend:** **Never use "Always allow."** Read the audit trail after every multi-step task. Do not treat the confirmation gate as complete coverage.
- **Risk:** High
- **Evidence:** https://about.fb.com/news/2026/09/introducing-muse-personal-ai-agent/ ; https://www.meta.com/help/artificial-intelligence/1047255454427887/ — checked 2026-10-02
- **Confidence:** `verified` for every quoted commitment; `unresolved` for how the gate behaves in practice

- **Setting:** macOS **Full Disk Access**, **Automation**, **Notifications** *(for Muse local-app control)*
- **Where:** Granted at setup; managed at Muse → Settings → File System Access, and at macOS System Settings → Privacy & Security
- **Default:** Per-app choice at setup (Off / Read only / Read and interact); `unresolved` which is pre-selected.
- **Exposes:** Full Disk Access lets the agent "find, read or update files"; Automation lets it "perform actions on apps that store information locally"; interactions "may include screenshots of your screen."
- **Recommend:** **Deny Full Disk Access.** The broadest single grant in this file — a cloud-backed agent with read-write reach over your whole filesystem and the ability to drive your local apps.
- **Risk:** High
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1126304576638594/ — checked 2026-10-02
- **Confidence:** labels and grants `verified`; default selection `unresolved`

- **Setting:** Muse data access by Meta personnel — **no opt-out available today**
- **Where:** No setting. **Muse Confidential VM** is promised "later this year" (2026), "intended to cryptographically and verifiably prevent Meta from accessing data in your VM," currently with "a small group of trusted testers."
- **Default:** Meta, verbatim: it *"restricts access to your data by Meta personnel through operational policies. It does not prevent Meta from accessing data when necessary to support, secure or operate the service."*
- **Exposes:** Everything in your VM — connected-service data, credentials-adjacent context, conversations — is reachable by Meta under its own operational policy.
- **Recommend:** Do not put anything in Muse you would not hand to Meta staff. **Today the protection is a policy, not a mechanism.**
- **Risk:** High
- **Evidence:** https://research.meta.ai/blog/security-and-safety-for-ai-agents-our-approach-with-muse — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Muse and ad systems — a real carve-out
- **Default:** *"Muse doesn't share your conversations or the data in your virtual machine with Meta ad systems."* **Caveat Meta itself states:** indirect activity (browsing, purchases) may still influence ad targeting.
- **Exposes:** Less than you would expect — a genuine exception to the Dec 2025 ads change, worth stating plainly in any client-facing summary.
- **Recommend:** Note it, but do not over-read it: the VM contents are walled off; the downstream consequences of what Muse does on your behalf are not.
- **Risk:** Low *(for the carve-out itself)*
- **Evidence:** https://www.meta.com/help/artificial-intelligence/1047255454427887/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "AI phone calls" from Muse — opt-out for non-users
- **Default:** Non-users can receive AI phone calls placed by other people's Muse agents.
- **Exposes:** You can be called by someone else's agent without having any Meta AI relationship.
- **Recommend:** Submit the opt-out form if this matters. Worth flagging — a Meta AI surface that touches people who never consented to anything.
- **Risk:** Medium
- **Evidence:** https://www.meta.com/help/artificial-intelligence/4532990443643263/ — checked 2026-10-02
- **Confidence:** `verified` that the opt-out exists; `unresolved` for the form URL

**Pre-launch, `reported` only:** "Hatch" (cross-app chat summaries into a morning email, auto birthday messages, trend-based post generation), "Open Claw" (executes commands "with no further input"), and an Instagram agentic shopping tool that would "handle the purchase process on their behalf." No launch dates, no published permission model.

## 8. Admin / workspace plane

Thin, and asymmetric: Meta has built agentic tooling **for** businesses with enterprise controls, and essentially nothing for the consumer on the other side of it.

- **Setting:** Meta Business Agent
- **Where:** Businesses activate it from Meta's business surfaces; runs on WhatsApp, Messenger and Instagram. The Platform connects "hundreds of systems like Shopify, Zendesk, and Shopee."
- **Default:** Not active until a business turns it on. Announced 2026-06-03; 1M+ businesses already using it; free, with paid tiers coming.
- **Exposes:** **The finding is the asymmetry.** The agent autonomously answers, recommends from a catalog, books appointments, qualifies leads and closes sales, deciding for itself "when a team member steps in." Meta's announcement names **enterprise-grade controls for the business** and **no consumer-side controls at all** — and does not say what customer data the agent accesses. As a consumer messaging a business on WhatsApp you may be negotiating with an autonomous agent, with **no disclosure toggle and no opt-out available** on your side.
- **Recommend:** As a business admin: define rules explicitly, set human-handoff thresholds conservatively. As a consumer: assume any business chat may be agent-operated.
- **Risk:** Medium
- **Evidence:** https://about.fb.com/news/2026/06/meta-business-agent/ — checked 2026-10-02
- **Confidence:** `verified` that the product exists and what it does; `unresolved` on consumer data exposure and specific admin setting labels

- **Setting:** "Group permissions" → "Edit group settings" **(WhatsApp admin lock on Advanced Chat Privacy)**
- **Where:** WhatsApp → Group info → Group permissions → **Edit group settings** → restrict to admins
- **Default:** `unresolved` whether all members or admins only can change group settings out of the box.
- **Exposes:** If any member can toggle Advanced Chat Privacy off, one person can re-open the whole group to AI feature use and chat export.
- **Recommend:** Restrict to admins on any group handling client, legal, medical or financial matters — then enable Advanced Chat Privacy. **The only genuine admin-plane AI control found for WhatsApp.**
- **Risk:** Medium
- **Evidence:** https://blog.whatsapp.com/introducing-advanced-chat-privacy — checked 2026-10-02
- **Confidence:** `reported`

- **Setting:** Muse for small business connectors
- **Where:** Muse → Settings → Connectors. Launched 2026-09-29, US and Canada.
- **Default:** Nothing connected. Connectors include Asana, Box, Canva, Dropbox, Figma, Granola, HighLevel, Intuit QuickBooks, Klaviyo, Lovable, Notion, Shopify, Slack, Stripe, Zoom, plus Facebook and Instagram business accounts, plus custom connectors.
- **Exposes:** Connected, Muse reaches Instagram professional-account analytics, Facebook Pages, Meta ad accounts, email, calendar, sales data, campaign performance, financial records and customer information — a small business's entire operational data estate, in one agent, in a Meta-operated VM.
- **Recommend:** **Do not connect QuickBooks, Stripe or a CRM holding customer PII.** The consolidation risk is the point: each connector is individually reasonable and the aggregate is a single point of failure over the whole business.
- **Risk:** High
- **Evidence:** https://about.fb.com/news/2026/09/introducing-muse-small-business/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** WhatsApp Business App / Cloud API admin control over Meta AI
- **Default:** **`unresolved`.** Could not verify whether a WhatsApp Business admin can disable Meta AI in business conversations, whether customer messages to a business are used for AI, or whether any MDM/enterprise control exists.
- **Recommend:** Treat as an open question for any client with a WhatsApp Business deployment — **do not assume either direction.**
- **Risk:** Cannot rate
- **Confidence:** `unresolved`

Also unverified in this plane: Meta Business Suite org-level AI toggles, Page-level opt-out of AI training, Facebook-Group-admin control over `@Meta AI`. None identified — and their absence could not be confirmed either.

## 9. API / developer plane

**The Llama API was renamed.** `llama.developer.meta.com/docs/` now 302-redirects to `dev.meta.ai/docs/`, serving the **Meta Model API** — Muse Spark, Muse Image, Muse Voice Transcribe, SAM 3.1, Muse Glimmer. This is the clearest and best data-handling posture anywhere in Meta's AI estate, because it is explicit and tier-based.

- **Setting:** Model tier selection — Standard vs. Contributor
- **Where:** Choose the model ID in your API call. Standard: `muse-spark-1.3`, `muse-spark-1.2`, `muse-spark-1.1`. Contributor: `muse-spark-1.3-contributor`, `muse-spark-1.2-contributor`. https://dev.meta.ai/docs/models
- **Default:** **Standard tier — "your data is never used for training."** There is no separate toggle; **the tier is the control.** The Contributor tier offers *"heavily discounted token pricing in exchange for permission to use your prompts and completions to train future Meta models"* — opt-in by explicitly choosing a `-contributor` model ID.
- **Exposes:** On Standard, nothing for training. On Contributor, every prompt and completion becomes Meta training data in exchange for a discount.
- **Recommend:** **Standard tier, always, for anything touching customer or client data.** Pin exact model IDs in config and review them in code review — the only thing separating "never trained on" from "trained on" is an eleven-character suffix, which is a dangerously easy mistake to make or to inherit from copied sample code.
- **Risk:** Low on Standard / High if a `-contributor` ID reaches production
- **Evidence:** https://dev.meta.ai/docs/models ; https://dev.meta.ai/docs/pricing-rate-limits — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Retention and zero-retention for the Meta Model API
- **Where:** Not found. `/docs/overview`, `/docs/models`, `/docs/pricing-rate-limits` and the docs index were read; **no retention period, no zero-retention option and no link to API-specific terms appear anywhere.** `dev.meta.ai/docs/legal/` returned an identity-confirmation screen, not a policy.
- **Default:** **`unresolved`** — "never used for training" is not the same claim as "not retained," and Meta does not make the second claim.
- **Recommend:** **Do not assume zero retention.** For regulated data, get a written commitment from Meta rather than relying on the docs.
- **Risk:** Medium
- **Confidence:** `unresolved`

- **Setting:** `permissions.default_profile` **(Muse Code CLI)**
- **Where:** Settings key `permissions.default_profile`; launch flag `--approval-mode`. https://dev.meta.ai/docs/muse-code/permissions
- **Default:** **`Auto-review`** — an automated reviewer handles approval requests, falling back to the user if unavailable. Approval-mode default is `on-request`. Sandbox network default is `proxy-only` (per-destination approval).
- **Exposes:** At default, **an automated model — not you — approves the agent's actions.** Profiles: "Ask me", "Auto-review", "Unrestricted" (equivalent to `--yolo`), "Read-only".
- **Recommend:** Set **"Ask me"** for any repo that matters, and keep the sandbox on. The documented escape hatches — `--yolo` (disables approval *and* sandbox), `--disable-approval`, `--disable-sandbox`, `--approval-judge off` — should be treated as prohibited in any shared or CI configuration.
- **Risk:** High at `Unrestricted` / Medium at the `Auto-review` default
- **Evidence:** https://dev.meta.ai/docs/muse-code/permissions — checked 2026-10-02
- **Confidence:** `verified`

The sandbox is OS-level: write access only to workspace and temp, `.git` / `.muse` / `.agents` read-only, enforced via Seatbelt (macOS), bubblewrap (Linux), Windows sandbox. **No telemetry or data-usage statement appears in the Muse Code docs** — `unresolved`. `dev.meta.ai/docs/computer-use` exists as a documented capability. **Meta AI Studio data handling: not verified** — `unresolved`.

## 10. Mobile & OS app permissions

- **Setting:** "Get creative ideas made for you by allowing camera roll cloud processing"
- **Where:** Facebook app → Menu → Settings & privacy → Settings → **Camera roll sharing suggestions** → toggle. Also via Create → Story → Settings → Camera roll settings. iPhone article: https://www.facebook.com/help/iphone-app/1243459406996869/
- **Default:** **Opt-in; off until you accept the prompt.** Meta: users "must opt in to use this feature, and you can turn it off at any time." Began testing in US and Canada (June 2025); extended to EU and UK **2026-04-16**; extended **2026-08-31** to Bolivia, Colombia, the Dominican Republic, El Salvador, Honduras, Nicaragua, Paraguay and Uruguay. **Not default-on anywhere verifiable.**
- **Exposes:** Meta automatically uploads "recent photos and videos from your camera roll on a regular basis" plus "older photos and videos based on special themes" like birthdays and holidays — **unpublished photos you never shared** — and derives metadata including recency, favorites, photo type, content analysis (food, animals, people), location and image quality. Meta commits that the media is **not used for ads targeting** and **not used to improve AI at Meta** unless you publish or share it into an AI feature. If you turn it off, "Meta will begin to remove your already uploaded photos and videos from our cloud after 30 days."
- **Recommend:** **Off.** The 30-day deletion lag and the ongoing-upload design mean the cost of leaving it on is a standing copy of your private camera roll in Meta's cloud; the benefit is collage suggestions.
- **Risk:** High
- **Evidence:** https://www.facebook.com/help/iphone-app/1243459406996869/ ; https://about.fb.com/news/2026/04/now-rolling-out-facebooks-opt-in-camera-roll-suggestions-in-the-eu-and-uk/ ; https://techcrunch.com/2025/06/27/facebook-is-asking-to-use-meta-ai-on-photos-in-your-camera-roll-you-havent-yet-shared/ — checked 2026-10-02
- **Confidence:** `verified` for label, path, upload behavior, 30-day removal, opt-in status and regional rollout

- **Setting:** "Photo suggestions while browsing" *(second toggle under Camera roll sharing suggestions)*
- **Default:** `unresolved` — the help article documents the cloud-processing toggle's path but not either toggle's out-of-box state.
- **Exposes:** Surfaces camera-roll photos as share prompts while you browse; `unresolved` whether this alone triggers cloud upload or is purely on-device.
- **Recommend:** Off, alongside cloud processing — and verify in-app, since the relationship between the two toggles is not documented.
- **Risk:** Medium
- **Confidence:** `reported` for existence; `unresolved` for default and behavior

- **Setting:** "Show Meta AI Button" **(WhatsApp)**
- **Where:** WhatsApp → Settings → Chats → **Show Meta AI Button**
- **Default:** On, described as "rolling out in phases" as of Sept 2026.
- **Exposes:** Cosmetic only — hides the entry point; does not change what Meta AI receives when @-mentioned.
- **Recommend:** Turn off for noise reduction, but **do not treat it as a privacy control.** **Lowest-confidence item in this file:** not found in any official WhatsApp source. Verify in-app before telling anyone it exists.
- **Risk:** Low
- **Confidence:** `reported`

- **Setting:** Meta AI in Facebook / Instagram / Messenger — **mute only, no off switch**
- **Where:** Facebook: Search → tap Meta AI → **i** → Mute. Instagram: paper-airplane icon → Meta AI thread → **i** → Mute messages. Messenger: **i** → Mute → Until I change it (plus archive, or it reappears).
- **Default:** Meta AI present and integrated into search and DMs. **No opt-out available** for the integration itself — verified across two independent guides: "You cannot fully turn Meta AI off on Facebook, Instagram, WhatsApp, or Messenger."
- **Exposes:** The assistant stays embedded in search and messaging surfaces; muting suppresses the thread, not the integration.
- **Recommend:** Mute for noise. Accept that there is no removal path. **The standalone Meta AI app is fully removable — uninstall it.**
- **Risk:** Medium
- **Evidence:** https://proton.me/blog/turn-off-meta-ai-facebook — checked 2026-10-02
- **Confidence:** `reported`

- **Setting:** Location for Meta AI
- **Default:** `unresolved`. Meta AI's terms state it uses your "interests, location and profile" to personalize, and the help center links to the location privacy guide — but **no in-app Meta-AI-specific location toggle or its default could be verified**, because Privacy Center pages do not render to automated fetch.
- **Recommend:** Set **approximate** location at the OS level for the Meta AI app and for Facebook/Instagram — the OS control is verifiable and effective where the in-app one is not.
- **Risk:** Medium
- **Confidence:** `unresolved`

- **Setting:** OS-level permissions for Meta AI apps — Camera, Microphone, Photos (full vs. limited), Location (precise vs. approximate), Contacts, Local Network, Bluetooth, Notifications, iOS App Tracking Transparency
- **Where:** iOS Settings → *app* → permissions; Android Settings → Apps → *app* → Permissions
- **Default:** **`unresolved`** — Meta's per-permission requests were not verified, and no permission manifest is guessed at here.
- **Recommend:** Grant **Photos: limited/selected** rather than full library, **Location: approximate**, and deny **Contacts** and **Local Network** — safe general-purpose hardening independent of what Meta requests, and Photos-limited is the direct mitigation for the camera-roll upload path above. On iOS, deny tracking.
- **Risk:** Medium
- **Confidence:** `unresolved`

- **Setting:** Private Processing **(WhatsApp)**
- **Where:** No user-facing toggle name found. Announced 2025-04-29.
- **Default:** **Optional** — Meta states that "Using Meta AI through WhatsApp, including features that use Private Processing, must be optional." First use cases: message summarization and writing suggestions.
- **Exposes:** When active, less than otherwise: *"When you interact with AI chats that use Private Processing technology, Meta cannot read or access the messages you have shared,"* and search queries made through it "are not connected to your account." EU/UK availability **not stated** — `unresolved`.
- **Recommend:** Prefer Private Processing features over ordinary Meta AI where you have the choice; use Advanced Chat Privacy to block AI feature use in a chat entirely. **Note the limit:** this is a confidentiality guarantee for *summarization and writing suggestions*, not for Meta AI conversations generally — those remain human-reviewable per §1.
- **Risk:** Low *where it applies*
- **Evidence:** https://engineering.fb.com/2025/04/29/security/whatsapp-private-processing-ai-tools/ — checked 2026-10-02
- **Confidence:** `verified` for mechanism and optionality; `unresolved` for regional availability and any UI label

## Volatile

### Changed in the last 12 months — confirmed

1. **AI chats became ad-targeting input on 2025-12-16, with no opt-out.** The largest single shift in this file. Notifications began 2025-10-07. Triggered an EPIC-led FTC complaint reportedly signed by 36 groups.
2. **"Discover" vanished from Meta's vocabulary.** The public feed is now "Meta AI and Vibes," media-centric rather than prompt-centric, with no deprecation notice ever published. Two 2025-era remediation labels — "Make all your prompts visible to only you" and "Suggesting your prompts on other apps" — are no longer in official docs and may be gone.
3. **Muse launched 2026-09-08** (US), expanded to US + Canada 2026-09-29 — Meta's first true computer-use agent. Spotify connector 2026-09-23; Muse Charm announced 2026-09-24.
4. **Meta Business Agent launched 2026-06-03**, already on 1M+ businesses.
5. **The Llama API became the Meta Model API** — new Standard/Contributor tier split governing training rights.
6. **"Activity information from ad partners" → "Activity from other businesses"** (July 2026, US first), **"Your activity off Meta technologies" discontinued entirely**, and the surviving control now also shapes "AI responses" — scope expansion dressed as consolidation.
7. **"Store visual data from AI experiences"** appeared on AI glasses around Sept 2026 — brand new, apparently default-on, and did not exist when the April 2025 coverage most people cite was written.
8. **Camera roll cloud processing** went from a US/Canada test (June 2025) to EU/UK (2026-04-16) to eight more countries (2026-08-31) — **still opt-in at every step, which is worth crediting.**
9. **The Instagram AI-likeness episode (July 2026):** feature shipped, backlash, withdrawn in roughly two days — but **"Allow people to reuse your content…" remains ON by default. The grant outlived the feature.**
10. Meta AI Terms of Service re-issued effective 2026-05-13; Supplemental Meta Platforms Technologies Privacy Policy effective 2026-06-29; Meta AI Disclosures effective 2025-11-19.
11. **Capture-LED tamper detection** added by software update — glasses now self-disable the camera if the LED is blocked.

### Most likely to move next

1. **The EU/UK/South Korea exclusion from AI-chat ad targeting.** Meta **never officially named the excluded regions**. An unnamed exclusion is an uncommitted one. Highest-probability silent reversal on this list, and the first thing to re-check.
2. **The US voice-storage opt-out may return.** The EU/UK builds already ship the toggle, so the engineering exists; the March 2026 Clarkson class action targets exactly the "designed for privacy, controlled by you" framing.
3. **Muse's legal surface is incomplete.** The May 2026 AI Terms contain no mention of agentic action, public feeds, Vibes or Discover — and Muse shipped four months later. Expect a revision; re-check quarterly.
4. **Muse Confidential VM** — promised "later this year" (2026). Until it ships, "Meta cannot access your VM" is a policy, not a mechanism. The biggest pending change to Muse's risk profile.
5. **The 1Password connector for Muse** ("coming soon"). The moment a scoped per-service grant becomes blanket credential access, and the moment Muse's permission model changes character.
6. **Human review disclosure or an opt-out,** given the Kenya-subcontractor reporting and the unreliable face-blurring finding.
7. **Muse beyond the US/Canada**, and onto AI glasses and Muse Charm — which will force the first EU-facing agentic privacy terms Meta has had to write.
8. **Hatch, Open Claw, and Instagram agentic shopping** — all pre-launch, no published permission model.
9. **Meta AI's memory controls.** The help article does not resolve, and the app's "Manage your information" screen has no memory option. Something is mid-change here.
10. **Glasses settings entry point and label drift.** Meta's own articles already call one control both "Cloud media" and "Cloud media processing."
11. **"Show Meta AI Button"** in WhatsApp — "rolling out in phases," unverified in any official source.
12. **The "Sharing and reuse" permission.** Meta killed the feature and kept the grant. It will be spent on something.

### What could not be verified

Stated plainly so nothing here gets over-read:

- **`/reset-ai` in WhatsApp** — no source verified. Do not publish it as a control.
- **Meta AI memory toggle label, default, and whether an off switch exists** — help article resolves to the help-center index.
- **Any Privacy Center deep link**, including the Right-to-Object path — all pages returned boilerplate or login walls.
- **Per-app OS permission manifest** for Meta AI apps.
- **WhatsApp Business / Cloud API admin controls over Meta AI**, Meta Business Suite org-level AI toggles, Page-level training opt-out, Facebook Group admin control of `@Meta AI`.
- **Meta Model API retention and zero-retention** — "never used for training" is documented; "not retained" is not claimed.
- **Meta AI Studio data handling.**
- **Facial recognition on glasses** — no setting found; nothing asserted either way.
- **Glasses media auto-import** — Meta's help docs and EFF directly contradict each other.
- **Whether the capture LED is lit during Live AI sessions.**
- **Defaults for:** Cloud media, Share additional data, "Hey Meta", Store visual data, Web access default setting, Muse global approval mode, Muse per-connector read/write, File System Access, "Photo suggestions while browsing", and "Activity from other businesses".
- **Blocked sources:** reddit.com, faq.whatsapp.com (title-only / error page), CNBC, Forbes, EPIC (403), CNN's Muse hands-on (451), Oakley FAQ (403). The 404 Media Discover piece exists as a headline via mirror only; **no Business Insider URL was found at all.**
- **No regulatory action specific to the Discover feed** was located.
