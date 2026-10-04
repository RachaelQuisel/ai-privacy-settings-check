# Open questions — what this audit does not know

> **Generated:** 2026-10-02 · **201 of 566 documented settings** carry a `reported` or `unresolved` component.


This file exists because an audit that only lists what it found is an audit you cannot calibrate.
Every entry below is a setting whose **default state, click path, or effect could not be established
from a primary source** on the check date. The setting itself is real and documented in its vendor
file — what is missing is the confidence to state a default as fact.

**Read it three ways.**

- **As an auditor:** these are the items where you must look at the live account rather than cite the
  baseline. A `reported` default is a hypothesis; an `unresolved` one is not even that.
- **As a maintainer:** this is the work queue.
- **As a reader deciding whether to trust the rest:** a vendor with a high open ratio is not a worse
  vendor, it is a worse-*documented* one. Meta AI sits high because Meta's Privacy Center is
  login-gated, not because its settings are more dangerous.

**Why the ratio is this high.** Most vendors do not publish default states. They document that a
setting exists and how to change it, and leave the shipped value to be discovered. That is itself a
finding — see dark pattern 1 in [methodology.md](methodology.md).

**What an item here does and does not mean.** It means the answer was absent from the sources that
were reachable. It does **not** mean the answer is unknowable. The Copilot second pass ran with no
search budget, so its `unresolved` labels mean *"absent from Microsoft's own documentation"* — narrower
than "nobody knows."

**Three things close an item, and research is the slowest.** A **live read** settles labels, paths and
current state. **Shipped client code** settles defaults when the docs won't — Grok's second pass
resolved ten of twelve that way, including the discovery that its consumer defaults are **regional**,
not global. And a **verified negative** — proving a setting is absent from a vendor's own canonical
documentation — is worth as much as a positive.


## Open items by vendor

| Vendor file | Settings documented | Open (`reported` or `unresolved`) |
|---|---:|---:|
| Microsoft Copilot | 118 | 40 |
| Google Gemini | 101 | 35 |
| Meta AI (and Muse) | 61 | 35 |
| ChatGPT (OpenAI) | 120 | 31 |
| Claude (Anthropic) | 73 | 24 |
| Grok (xAI) | 63 | 23 |
| Microsoft Copilot (admin, API, mobile) | 30 | 13 |
| **Total** | **566** | **201** |

## Microsoft Copilot

`vendors/copilot.md` — 40 open of 118 documented.

**Unresolved — no sourced default, path, or effect:**

- Training on voice conversations
- Copilot diagnostics logs
- Tailored experiences
- Suggestions matching public code
- (retention periods for prompts and suggestions)
- Microsoft usage data (older app — the predecessor of "One shared experience")
- Browsing data sync / autofill in Copilot for Windows
- Visibility of Microsoft 365 Copilot conversations within Copilot
- Recall additional activity details from App Actions providers (policy: DisableRecallD…
- Activity history
- Inking & typing personalization
- Store local sessions in the Cloud
- Connectors
- File Search and File Read
- Agent and plugin access (Allow agents and plugins built by Microsoft / …by your organ…
- Advanced package uploads
- User consent settings (Entra ID)
- Agent connector allow-list — AgentConnectorAccessPolicy
- Partner agents (Anthropic Claude, OpenAI Codex)
- Copilot Pages (consumer)
- Create and view Copilot Pages and Copilot Notebooks
- Sharing (agents)
- Agent feedback sharing
- (Copilot cloud agent session visibility)
- Set maximum duration for storing snapshots used by Recall
- Delete synced sessions
- Copilot Voice (microphone)
- Transcription (-AllowTranscription)
- Copilot custom dictionary
- Microphone / Camera app permissions
- Voice activation
- Online speech recognition
- Sensitive information filtering (the consumer page renders it as Sensitive informatio…
- Experimental agentic features (Copilot Actions on Windows)
- Files — Allow Always / Ask every time / Never allow (per agent)
- Settings agentic search experience — DisableSettingsAgent
- Allow Recall to be enabled — AllowRecallEnablement (cross-referenced here; full admin…
- Stored sign-in details (computer use) and Enforce HTTPS
- Human supervision (computer use)
- Repository access (Copilot cloud agent)


## Google Gemini

`vendors/gemini.md` — 35 open of 101 documented.

**Unresolved — no sourced default, path, or effect:**

- Instructions for Gemini (rendered as "Saved info" in some locales)
- Web & App Activity — and its sub-checkbox Include Chrome history and activity from si…
- Personal Intelligence in AI Mode (draws on Search Services History)
- Connected Apps (formerly Gemini Extensions, then Apps)
- Google Photos — Gemini features in Photos and query donation
- Gem sharing — roles Viewer / Editor
- Canvas web app public links — the worst default in this category
- Sharing AI Overviews / AI Mode responses from Search
- AI Mode history deletion
- Talk to Gemini hands-free → Hey Google (and legacy Hey Google & Voice Match)
- Gemini in Meet — Automatic note-taking (user-facing: "Take notes for me") ⚠️
- Gemini Spark / Turn off Gemini Spark
- Let Gemini browse for you (Chrome auto browse)
- Screen automation in Android apps — no dedicated toggle found
- Deep Research
- Skills (replacing Gems) — Skills Manager
- Computer Use via the Gemini API — safetydecision, disabledsafetypolicies, enablepromp…
- Feature access (Gemini side panel per Workspace service)
- CSE, IRM, and Drive trust rules as Gemini exclusions
- Gemini for Workspace log events / Gemini Notebook log events / Gemini reports
- Free-tier retention period
- Paid Services data-use clause
- Prompt logging for abuse monitoring (standard Google models) — materially changed; fl…
- Gemini Code Assist individual/free tier — retired
- Gemini on lock screen → Use Gemini without unlocking and Make calls and send messages…
- Screen context → use text from screen / use screenshot
- Android runtime permissions — Microphone, Camera, Location, Contacts, Notifications,…
- Display over other apps / Accessibility service
- iOS Gemini app permissions and lock-screen surfaces

**Reported only — a third party claims it, no primary source:**

- Improve Google services with your audio and Gemini Live videos & screenshares
- Memory (web toggle also labelled "Your past chats with Gemini")
- Device assistance, Phone, Messages, WhatsApp (Android) — the Keep-Activity bypass
- Uploaded files in a shared conversation — no setting; always included
- Jules (coding agent) data use
- Digital assistant app (device) / Digital assistants from Google → Gemini

## Meta AI (and Muse)

`vendors/meta-ai.md` — 35 open of 61 documented.

**Unresolved — no sourced default, path, or effect:**

- "Right to object" (forms: "I want to object to the use of my information for Meta AI"…
- "Activity from other businesses" (renamed from "Activity information from ad partners")
- Meta AI cross-chat memory ("memories") — exact toggle label unresolved
- "Memory" (Muse) — backed by an editable Memory.md file
- Read vs. write scope per connector — "Read only" / "Read and interact"
- "File System Access" (Muse on Mac) — per-app: Off / Read only / Read and interact
- "Connected apps" (AI glasses music services) and the Muse Spotify connector
- "Make all your prompts visible to only you" / "Suggesting your prompts on other apps"
- /reset-ai (WhatsApp)
- Voice recording and transcript storage (AI glasses)
- Facial recognition on glasses
- Media auto-import from glasses
- "Web access default setting"
- Pre-action confirmation and audit trail
- macOS Full Disk Access, Automation, Notifications (for Muse local-app control)
- "AI phone calls" from Muse — opt-out for non-users
- Meta Business Agent
- WhatsApp Business App / Cloud API admin control over Meta AI
- Retention and zero-retention for the Meta Model API
- "Photo suggestions while browsing" (second toggle under Camera roll sharing suggestions)
- Location for Meta AI
- OS-level permissions for Meta AI apps — Camera, Microphone, Photos (full vs. limited)…
- Private Processing (WhatsApp)

**Reported only — a third party claims it, no primary source:**

- (No setting exists) — use of Meta AI conversations for content and ad personalization
- "Store visual data from AI experiences" (AI glasses)
- "Allow people to reuse your content on Instagram and with AI features at Meta"
- Global approval mode — "Ask for some actions" / "Always ask"
- "@Meta AI" in WhatsApp group chats
- "Advanced Chat Privacy"
- "Hey Meta" (inside "Hey Meta" preferences)
- "Cloud media" (the autocapture article calls the same control "Cloud media processing…
- "Share additional data" (Meta's help article never names the toggle)
- "Group permissions" → "Edit group settings" (WhatsApp admin lock on Advanced Chat Pri…
- "Show Meta AI Button" (WhatsApp)
- Meta AI in Facebook / Instagram / Messenger — mute only, no off switch

## ChatGPT (OpenAI)

`vendors/chatgpt.md` — 31 open of 120 documented.

**Unresolved — no sourced default, path, or effect:**

- Thumbs up / thumbs down (training carve-out, no toggle)
- Include environments (Codex)
- Enable memory ("Let ChatGPT personalize your experience based on your chats, files, a…
- Reference chat history
- Reference record history ("Let ChatGPT reference all previous recording transcripts a…
- Reference my writing style ("Let ChatGPT use your chats, Library files, and connected…
- Reference photo / Full-body reference photo
- Library search / Connector search / Suggested prompts / Fast answers / Web search
- Computer History
- Share chats and scheduled tasks (workspace permission)
- GPT sharing level — Invite-only / Workspace link / Your workspace / Anyone with the l…
- Codex workspace share links
- NYT litigation preservation order — lifted
- Workspace data-retention policy
- Voice mode — Live / Advanced / Standard
- Background conversations / Start with Voice / Start automatically in CarPlay
- ChatGPT Voice (master enable)
- Codex Cloud internet access — Package managers / Custom domains only / All unrestricted
- Codex Cloud repository access / Connect GitHub
- Data Retention — Zero Data Retention / Modified Abuse Monitoring
- Agent tracing
- Enterprise Key Management (EKM / BYOK)
- iOS "Allow Tracking" / App Tracking Transparency
- Android OS runtime permission manifest
- Enable Work with Apps (macOS desktop)
- ChatGPT extension setup (Apple Intelligence) — with or without an account
- Visual Intelligence → ChatGPT
- Notification channels
- Work network access / Reset ChatGPT Work

**Reported only — a third party claims it, no primary source:**

- Include your audio recordings / Include your video recordings
- Audit logging (API Platform)

## Claude (Anthropic)

`vendors/claude.md` — 24 open of 73 documented.

**Unresolved — no sourced default, path, or effect:**

- Help improve our AI models
- Rate chats (admin)
- Trusted Tester Program
- Tool permissions — Always allow / Needs approval / Blocked
- Artifact visibility — Only you (Pro/Max) / Only people invited (Team/Enterprise) / An…
- Shared artifacts → Manage · Uploaded files → Manage · Your feedback → Manage · Memory…
- (settings sections absent from this file) Design systems · Reflect · Time and focus
- (derived) Consumer retention window
- Delete Account
- Dictation (mobile microphone)
- Enable computer use (Cowork desktop)
- Calendar / Location / Reminders / Health (iOS app integrations)
- Location metadata
- Your privacy choices (cookies)
- Android app permissions

**Reported only — a third party claims it, no primary source:**

- Memory import / export
- OAuth scope review at connect time
- Restrict verified domain connectors (admin)
- Share chats using connectors (admin)
- Camera / Photos access (mobile)
- Bypass permissions mode / Auto permissions mode (Claude Code, admin)
- Organization settings → Capabilities (Memory, Web search, Ask Org, Interactive conten…
- Role-based permissions — Privacy: Can manage
- (App Store privacy label) Data linked to you

## Grok (xAI)

`vendors/grok.md` — 23 open of 63 documented.

**Unresolved — no sourced default, path, or effect:**

- Personalize Grok with your conversation history ("Allow Grok to remember details from…
- Personalize Grok using 𝕏 ("Allow your 𝕏 data to be used for personalizing and enhanci…
- Personalize Grok with your device location ("Allow Grok to include your browser locat…
- Allow Grok to remember your conversation history (X side)
- Allow X to personalize your experience with Grok (X side)
- Granular OAuth scope strings
- Watermark Imagine generations / Share to X
- Block modifications by Grok ("Prevent Grok from modifying this content"; related: "Im…
- Cookie Settings → Manage
- Call transcript / Voice Chat history
- Custom Voice / voice cloning ("Voice cloning is available on the Grok mobile app")
- Camera / live vision in voice mode
- Grok Bot account/data plane
- Product sharing — scopes Private / Team / Organization / Public, per resource (Conver…
- Conversation retention → Custom period / Retain indefinitely
- Team settings surface — Overview, Usage, Analytics, Connectors, Marketplaces, Advanced
- Grok Bot org controls
- Grok Build CLI — /privacy, /settings
- OS runtime permission grants — Microphone, Camera, Photos, Location, Notifications, C…
- Allow NSFW Content (I'm 18+)

**Reported only — a third party claims it, no primary source:**

- Allow your public data as well as your interactions, inputs, and results with Grok an…
- Protect your posts
- Connected apps (X side, reverse direction)

## Microsoft Copilot (admin, API, mobile)

`vendors/copilot-admin-api-mobile.md` — 13 open of 30 documented.

**Unresolved — no sourced default, path, or effect:**

- EdgeEntraCopilotPageContext, CopilotPageContext, CopilotCoworkToolActionsEnabled, All…
- Suggestions matching public code (enterprise/org enforcement)
- (organization and enterprise policy pages generally)
- (Copilot audit log and metrics)
- Semantic Search (Windows AI Foundry)
- (what context is sent for completions, and its retention)
- Copilot mobile privacy settings
- (full OS permission list for the Copilot mobile app)
- Microsoft Family Safety controls over Copilot (under-18 accounts)
- Ask Copilot (taskbar item)
- Windows app permission pages underlying every AI feature
- (GitHub Mobile Copilot permissions)

**Reported only — a third party claims it, no primary source:**

- Text and image generation (app permission)

## How to close one

1. Read the entry's `Evidence` and `Confidence` lines — they name what was already tried.
2. Prefer, in order: **a live read** · **shipped client code** (name the file and key) · vendor
   documentation · an archived snapshot · two or more independent third parties agreeing, which is
   *corroborated reported*, never `verified`.
3. Update `Default`, `Evidence` and `Confidence`, and bump the file's `Last verified` date.
4. Regenerate this file so the counts stay true.

**A live read settles a label or a path. It does not settle a default** — an observed account is one
data point shaped by its owner's history.

**Check whether the default is regional before writing it as one value.** Grok's consumer toggles are
ON outside the EEA/UK and OFF inside it.

**Do not close an item by inference.** The value of this list is that everything on it is genuinely
unknown, and everything off it is genuinely sourced.

