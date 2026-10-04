# Claude (Anthropic)

> **Last verified:** 2026-10-02
> **Surfaces covered:** claude.ai · Desktop · mobile · Claude Code · Claude in Chrome · Cowork · Anthropic Console/API
> **Domain note:** `privacy.anthropic.com` 301-redirects to `privacy.claude.com`; `support.anthropic.com` → `support.claude.com`. Claude Code docs at `code.claude.com/docs`, API docs at `platform.claude.com/docs`. Old links still resolve via redirect.

## 1. Training on your data

### The 2025 consumer policy change — what is actually true

The most misreported item on this list. Verified facts, in Anthropic's own words:

- *"We are also extending data retention to five years, if you allow us to use your data for model training."*
- *"If you do not choose to provide your data for model training, you'll continue with our existing 30-day data retention period."*
- *"This updated retention length will only apply to new or resumed chats and coding sessions."*
- *"If you delete a conversation with Claude it will not be used for future model training."*
- Selection deadline was **October 8, 2025** — not September 28, which several outlets printed.
- Scope: Claude Free, Pro, and Max, *"including when they use Claude Code from accounts associated with those plans."* Explicitly excluded: *"Claude for Work, Claude for Government, Claude for Education, or API use, including via third parties such as Amazon Bedrock and Google Cloud's Vertex AI."*
- Evidence: https://www.anthropic.com/news/updates-to-our-consumer-terms — checked 2026-10-02 — `verified`

---

- **Setting:** `Help improve our AI models`
  *(Live UI label, confirmed by direct observation. Earlier third-party walkthroughs rendered it "Help improve Claude" — that is wrong. The in-product description reads: "Allow the use of your chats and coding sessions to train and improve Anthropic AI models.")*
- **Where:** Settings → Privacy → toggle. https://claude.ai/settings/data-privacy-controls
- **Default:** **`unresolved` for the out-of-box state.** Anthropic's help article does not state a default. Three pieces of evidence point to effectively-on: (a) the Privacy Policy reads *"We may use your Inputs and Outputs to train and improve Anthropic AI models, **unless you opt out** through your account settings"* — opt-out framing, `verified`; (b) the Aug-2025 news post says new users *"select their preference during signup"* without naming a default, `verified`; (c) third-party reporting states the toggle arrives **pre-set to On** inside the "Updates to Consumer Terms and Policies" modal, beside a prominent "Accept" button — `reported`. Team, Enterprise, API, Gov, Education: off / not applicable (`verified`).
- **Exposes:** Left on, every new or resumed chat and Claude Code session from a Free/Pro/Max account becomes eligible training data, held de-identified in training pipelines up to five years.
- **Recommend:** **Off.** Highest-leverage toggle on claude.ai — drops retention from 5 years to 30 days and removes your work from training corpora.
- **Risk:** High
- **Evidence:** https://privacy.claude.com/en/articles/12109829-how-do-i-change-my-model-improvement-privacy-settings ; https://www.anthropic.com/legal/privacy ; https://www.anthropic.com/news/updates-to-our-consumer-terms — checked 2026-10-02
- **Confidence:** `verified` — setting, path, exact label and description string all confirmed by direct observation (live read of a consumer Max account, 2026-10-02), matching the help-center label. `unresolved` remains on the **new-account default**; `reported` remains on the pre-checked modal. Note the observed account had it **on**, which is consistent with but does not prove the default.

- **Setting:** Thumbs up / thumbs down on a Claude response
- **Where:** Hover a Claude message → thumbs icons (all surfaces)
- **Default:** Available to all consumer users; not disableable by a consumer
- **Exposes:** Submitting feedback hands Anthropic the associated conversation, which *"may be used to train our AI models as permitted under applicable laws"*, retained **5 years** — **even if model improvement is off.**
- **Recommend:** Don't rate responses in a sensitive conversation. No consumer off switch exists.
- **Risk:** Medium
- **Evidence:** https://privacy.claude.com/en/articles/10023580-is-my-data-used-for-model-training ; https://privacy.claude.com/en/articles/10023548-how-long-do-you-store-my-data — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(no setting)* Safety-classifier flagging
- **Where:** Not user-controllable
- **Default:** Always on, every plan and tier including ZDR
- **Exposes:** *"Even if you opt-out, we will use Inputs and Outputs for model improvement when: (i) your conversations are flagged for safety review…"* Flagged inputs/outputs kept **up to 2 years**; trust-and-safety classification scores **up to 7 years**.
- **Recommend:** Treat as unavoidable. Factor into what you paste into any Claude surface, ZDR API traffic included.
- **Risk:** Medium
- **Evidence:** https://www.anthropic.com/legal/privacy ; https://privacy.claude.com/en/articles/10023548-how-long-do-you-store-my-data ; https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Rate chats *(admin)*
- **Where:** Organization settings → Data and privacy
- **Default:** `unresolved` — article names the control and who can change it, not its default
- **Exposes:** While on, any member's thumbs-up/down ships the conversation to Anthropic as training-eligible feedback, bypassing the org's no-training posture.
- **Recommend:** Off for any org handling client or regulated data. Main leak path out of commercial no-training terms.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/10504844-manage-user-feedback-settings-on-team-and-enterprise-plans ; https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training — checked 2026-10-02
- **Confidence:** `verified` (label, path, Owner-locked); `unresolved` (default)

- **Setting:** Development Partner Program → "Join"
- **Where:** Console → Settings → Privacy controls → Development Partner Program. https://platform.claude.com/settings/privacy
- **Default:** **Opted out.** Orgs must explicitly enroll. Prepaid-billing commercial accounts only; ZDR orgs ineligible.
- **Exposes:** Sends Claude Code sessions to Anthropic for training, stored up to **two years**, and that retention survives leaving the program.
- **Recommend:** Leave unjoined absent a deliberate reason and no client-confidentiality exposure.
- **Risk:** High *(if joined)*
- **Evidence:** https://support.claude.com/en/articles/11174108-about-the-development-partner-program ; https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Trusted Tester Program
- **Where:** Invitation-based; no standing settings path found
- **Default:** Not enrolled
- **Exposes:** Named by Anthropic as an explicit training opt-in that overrides the model-improvement setting.
- **Recommend:** Decline for accounts carrying client work.
- **Risk:** Medium
- **Evidence:** https://privacy.claude.com/en/articles/10023580-is-my-data-used-for-model-training — checked 2026-10-02
- **Confidence:** `verified` that it exists and is a training opt-in; `unresolved` on any UI path

- **Setting:** `/feedback` (and `/bug`, `/share`, Claude-drafted feedback) in Claude Code
- **Where:** Claude Code CLI. Opt out: `DISABLE_FEEDBACK_COMMAND=1`
- **Default:** **On** connecting directly to the Claude API. **Off** on Amazon Bedrock, Google Cloud Agent Platform, Microsoft Foundry, Claude Platform on AWS.
- **Exposes:** Sends conversation history **including code** to Anthropic (stored in Google Cloud Storage), optionally filing a GitHub issue in a **public** repo. Retained **5 years**. The dialog offers to widen scope to other sessions from the same project over 24 hours or 7 days.
- **Recommend:** `DISABLE_FEEDBACK_COMMAND=1` on any machine with client code; at minimum never widen past "current session only".
- **Risk:** High
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** "How is Claude doing this session?" survey → *"Can Anthropic look at your session transcript to help us improve Claude Code?"*
- **Where:** Claude Code CLI. Opt out: `CLAUDE_CODE_DISABLE_FEEDBACK_SURVEY=1`; also suppressed by `DISABLE_TELEMETRY`, `DO_NOT_TRACK`, `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`. Rate-limit via `feedbackSurveyRate`.
- **Default:** **On for every provider**, including Bedrock/Vertex/Foundry where other telemetry is off. The rating alone stores no transcript. Answering **Yes** uploads your conversation transcript, subagent transcripts, and the raw on-disk session log. API access values and token patterns are redacted, but *"Source code, file contents, and other conversation content are uploaded as-is."* Shared transcripts retained **up to 6 months**. Not used for training.
- **Exposes:** One mis-click on "Yes" ships a full session transcript with source code to Anthropic.
- **Recommend:** `CLAUDE_CODE_DISABLE_FEEDBACK_SURVEY=1`, or answer "Don't ask again".
- **Risk:** High
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

## 2. Memory, history & personalization

- **Setting:** Search and reference chats
- **Where:** Settings → Memory. https://claude.ai/new#settings/customize-memory ; legacy: https://claude.ai/settings/capabilities
- **Default:** **Enabled by default**, paid plans only (Pro, Max, Team, Enterprise) on web, Desktop, Mobile
- **Exposes:** Any new chat can silently pull content from your entire prior history into context, including chats you'd forgotten.
- **Recommend:** Off if one account holds unrelated clients or mixes personal and work — cross-contamination is the real risk here, not exfiltration.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Generate memory from chats *(legacy label: "Generate memory from chat history")*
- **Where:** Settings → Memory (legacy: Settings → Capabilities)
- **Default:** **On by default** for Free, Pro, Max. **Off by default per Team/Enterprise member**, and unavailable until an Owner enables memory org-wide.
- **Exposes:** Claude writes persistent memory entries from your chats and reuses them in later conversations and tasks, including Projects (each project keeps a separate memory space).
- **Recommend:** Keep on only if you want personalization; pause or disable for accounts touching multiple clients. Review entries periodically — memory is included in data exports.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Include sensitive topics in memory
- **Where:** Settings → Memory
- **Default:** **Off.** By default Claude does not save topics *"some people consider sensitive, such as health information."*
- **Exposes:** On, health and similar subject matter becomes a durable memory entry on your account.
- **Recommend:** Leave off. One of the few genuinely privacy-protective defaults on the platform.
- **Risk:** High *(if enabled)*
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Memory *(per-chat)*
- **Where:** New chat → "+" menu → toggle **Memory** off, **before sending the first message**
- **Default:** Follows the account setting. **Cannot be changed after the first message sends.**
- **Exposes:** On, that chat both reads memory and contributes new entries.
- **Recommend:** Off for any one-off chat about a client you don't want blended into general context.
- **Risk:** Low
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Incognito chat *(ghost icon)*
- **Where:** New chat outside a project → ghost icon, upper right. Active state: black border, "Incognito chat" label upper left; close with "x".
- **Default:** Off — opt-in per chat. **All plans.**
- **Exposes:** Nothing extra. Incognito chats are *"not saved to your chat history or to Claude's memory"*, *"not used for training"* even with model improvement on, and excluded from chat search and monthly recaps. **They are not ephemeral:** *"retained for either 30 days (default), or longer in accordance with your organization's custom data retention setting."*
- **Recommend:** Use as the default mode for anything sensitive. Note that in the new Claude experience incognito falls back to the previous chat experience — no file creation or code execution.
- **Risk:** Low
- **Evidence:** https://support.claude.com/en/articles/12260368-use-incognito-chats — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Monthly recap
- **Where:** No dedicated toggle. Suppress by turning off **Generate memory from chat history**.
- **Default:** *"available by default for eligible accounts where memory is on."* Free, Pro, Max on web and Desktop only — not Team, Enterprise, or mobile.
- **Exposes:** Builds a personal summary across recent chats, including content Claude wrote from connected services (not the raw emails or files).
- **Recommend:** Harmless on a single-purpose account; disable via memory if you share a screen or device.
- **Risk:** Low
- **Evidence:** https://support.claude.com/en/articles/15672559-see-your-monthly-recap — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Memory import / export
- **Where:** Settings → Memory
- **Default:** Manual action
- **Exposes:** Nothing by itself; the export is a plaintext record of everything Claude has inferred about you, so treat the file as sensitive.
- **Recommend:** Export once and read it — fastest audit of what Claude actually retains about you.
- **Risk:** Low
- **Evidence:** https://support.claude.com/en/articles/12123587-import-and-export-your-memory-from-claude — checked 2026-10-02
- **Confidence:** `reported` — article title and existence confirmed in search results; page body not fetched.

- **Setting:** Memory — organization capability *(admin)*
- **Where:** Organization settings → Capabilities
- **Default:** Off per Team/Enterprise member until the Owner enables it org-wide
- **Exposes:** Nothing until enabled. Admins **cannot** view or edit members' memories; org-level changes are audit-logged.
- **Recommend:** Leave off absent a named use case. **Admin-lockable:** members cannot enable memory if the org capability is off.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context — checked 2026-10-02
- **Confidence:** `verified`

## 3. Connectors & OAuth scopes

- **Setting:** Connectors *(per-connector enable)*
- **Where:** Customize → Connectors, or "+" in chat → Connectors → **Manage connectors**
- **Default:** **Off** — *"connectors are off until you explicitly enable them per conversation."* Web connectors on all plans including Free; custom connectors limited to **one** on Free, unlimited on paid.
- **Exposes:** An enabled connector lets Claude read — and with write tools, modify — data in Gmail, Drive, Microsoft 365, Slack, Notion and similar. **The connector's OAuth grant is the ceiling, not your prompt.**
- **Recommend:** Enable per conversation, not permanently. Disconnect anything not actively in use.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Tool permissions — **Always allow** / **Needs approval** / **Blocked**
- **Where:** Customize → Connectors → select connector → **Tool permissions**
- **Default:** `unresolved` — per-tool default not stated. Team/Enterprise Owners can set centrally.
- **Exposes:** "Always allow" on a write tool lets Claude send mail, modify files or post messages with no confirmation, bounded only by your own permissions in the source system.
- **Recommend:** Every **write** tool to "Needs approval" or "Blocked"; reads on approval for anything containing client data.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities — checked 2026-10-02
- **Confidence:** `verified` (labels, path); `unresolved` (defaults)

- **Setting:** OAuth scope review at connect time
- **Where:** The third-party consent screen when connecting a connector or custom remote-MCP server
- **Default:** Whatever the server requests
- **Exposes:** Anthropic's own guidance: *"review what permissions the MCP server is requesting… limit these scopes when possible and deny access if requested permissions seem unnecessary."* A broad grant persists until revoked.
- **Recommend:** Read the scope list every time; revoke at both ends — Customize → Connectors **and** the provider's own security settings.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp — checked 2026-10-02
- **Confidence:** `reported` — guidance paraphrased from search extraction, not fetched verbatim.

- **Setting:** Microsoft 365 connector — Entra admin consent and per-scope revocation
- **Where:** Organization settings → Connectors (Owner enable) **plus** Microsoft Entra Global Administrator consent
- **Default:** Not connected. Personal accounts (`@outlook.com`) cannot be used; requires an Entra tenant.
- **Exposes:** Delegated permissions scoped to what each user can already see. Admins can revoke individual scopes — dropping `Sites.Read.All` kills SharePoint, dropping `Mail.Read` kills Outlook mail. Documents stay in-tenant and are *"retrieved only during active queries and not cached."* Refresh tokens expire after **90 days** inactive; access tokens **60–90 minutes**. Conditional Access MFA and group rules work; **location/network restrictions do not**, because requests originate from Anthropic's range `160.79.104.0/21`.
- **Recommend:** Grant only the scopes a named workflow needs; add Anthropic's IP range to Conditional Access expectations rather than assuming network rules hold.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/12684923-microsoft-365-connector-security-guide — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Organization settings → Connectors / Browse connectors / Featured connectors *(admin)*
- **Where:** Organization settings → Connectors → Browse connectors
- **Default:** Owners must explicitly enable connectors before members can use them. Featured connectors listed with one switch each.
- **Exposes:** Nothing until enabled. Turning one off removes it for every member *"from the member's next turn."*
- **Recommend:** Allowlist only reviewed connectors. **Admin-lockable:** a member cannot re-enable a disabled connector.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Restrict verified domain connectors *(admin)*
- **Where:** Organization settings → Organization and access
- **Default:** `unresolved`
- **Exposes:** Unrestricted, members may connect services authenticated outside your verified domains.
- **Recommend:** Restrict.
- **Risk:** Medium
- **Evidence:** https://platformsecurity.com/blog/how-to-secure-your-claude-enterprise-tenant — checked 2026-10-02
- **Confidence:** `reported` — third-party settings inventory only; no Anthropic article found naming this control.

- **Setting:** Claude Code MCP controls — `managed-mcp.json`, `managedMcpServers`, `allowedMcpServers`, `deniedMcpServers`, `allowManagedMcpServersOnly`, `allowAllClaudeAiMcps`, `allowClaudeInChromeWithManagedMcp`, `disableClaudeAiConnectors`
- **Where:** macOS `/Library/Application Support/ClaudeCode/managed-mcp.json` · Linux/WSL `/etc/claude-code/managed-mcp.json` · Windows `C:\Program Files\ClaudeCode\managed-mcp.json`, plus managed settings sources (server-managed settings, MDM plist, HKLM registry, `managed-settings.json`)
- **Default:** **Wide open.** *"By default, anyone running Claude Code can connect any MCP server they choose."* `allowedMcpServers` unset = all allowed; `deniedMcpServers` unset = none blocked. Anthropic reviews Directory connectors against listing criteria but *"doesn't security-audit or manage any MCP server."*
- **Exposes:** An unaudited MCP server runs with your local tool permissions and sees whatever Claude passes it.
- **Recommend:** Solo — audit each server before `claude mcp add`, and prefer `serverUrl`/`serverCommand` matching: Anthropic explicitly warns `serverName` *"is not a security control."* Orgs — deploy `managed-mcp.json` with `allowManagedMcpServersOnly: true`.
- **Risk:** High
- **Evidence:** https://code.claude.com/docs/en/managed-mcp — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Share chats using connectors *(admin)*
- **Where:** Organization settings → Data and privacy
- **Default:** `unresolved`
- **Exposes:** Allows a shared chat to carry connector-sourced content — PII, financials — to whoever holds the share link.
- **Recommend:** Off, even where plain chat sharing stays on.
- **Risk:** High
- **Evidence:** https://platformsecurity.com/blog/how-to-secure-your-claude-enterprise-tenant — checked 2026-10-02
- **Confidence:** `reported` — named in a third-party inventory, corroborated by search snippets; no Anthropic article fetched naming it.

## 4. Sharing & publication defaults

- **Setting:** Visibility dropdown — **Public** / **Private** *(chat sharing)*
- **Where:** Open a chat → **Share** → visibility dropdown
- **Default:** *"chats are always private by default."* Free/Pro/Max: Public means *"anyone with the link can view the chat snapshot."* Team/Enterprise: *"can only share chats with other members of the same organization, not publicly."*
- **Exposes:** A public share link exposes a snapshot of the whole conversation to anyone with the URL — no account needed.
- **Recommend:** Audit existing links periodically and set stale ones back to Private. A shared link is a standing exposure, not a one-time send.
- **Risk:** High
- **Evidence:** https://privacy.claude.com/en/articles/10593882-share-and-unshare-chats — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** People with access *(share a chat by email)*
- **Where:** Chat → **Share** → addresses under **People with access** → **Send**
- **Default:** Nobody. All plans; Team/Enterprise restrict invites to organization-domain addresses.
- **Exposes:** A snapshot up to the moment of sharing, including artifacts and your name. Recipients cannot continue the chat, copy it, or download files; attached files aren't visible except within an org. The link works only for the exact address entered. Team/Enterprise admins see sharing activity in audit logs.
- **Recommend:** Prefer email invites over public links — scoped, revocable, logged.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/16762496-share-a-chat-with-specific-people — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Artifact visibility — **Only you** (Pro/Max) / **Only people invited** (Team/Enterprise) / **Anyone with the link** / **Anyone at [organization]**; access levels **Can view** / **Commenter** / **Can edit**
- **Where:** Open an artifact → share controls
- **Default:** *"Artifacts start private to you. Nothing is shared until you share it."* Team/Enterprise artifacts stay inside the org by default. Public publishing is a Free/Pro/Max path; org sharing is the Team/Enterprise path. Group sharing is Enterprise-only; invite-by-email is beta on Pro and up.
- **Exposes:** "Anyone with the link" turns a working document into an unauthenticated public page.
- **Recommend:** Default-private is correct — widen deliberately, and prefer "Anyone at [org]" over link sharing inside a company.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/9547008-publish-and-share-artifacts — checked 2026-10-02
- **Confidence:** `verified` on labels, defaults, plan matrix; `unresolved` on whether published artifacts are search-indexed — the article does not say.

- **Setting:** Share projects, with sub-setting **Public projects** *(admin)*
- **Where:** Organization settings → Data and privacy. Enterprise per-role: Organization settings → Roles → role → **Capabilities**
- **Default:** **Both on by default.** Team gets org-level toggles; Enterprise adds per-role control. Changing requires Primary Owner, Owner, or a custom role with **Privacy: Can manage**.
- **Exposes:** On by default, a member can expose a project — including its knowledge files — org-wide or beyond.
- **Recommend:** Turn **Public projects** off; keep **Share projects** on only if teams genuinely collaborate in projects. **Admin-lockable:** members then see *"Project sharing is turned off by your administrator."*
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/9927533-control-project-sharing-for-your-organization — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Shared chats → **Manage**
- **Where:** Settings → Privacy → Shared chats → Manage
- **Default:** Lists whatever you've shared
- **Exposes:** Nothing new; it is the audit surface for links already created.
- **Recommend:** Review quarterly. Old share links are the most commonly forgotten exposure on claude.ai.
- **Risk:** Medium
- **Evidence:** panel confirmed by direct observation (live read of a consumer Max account, 2026-10-02) at Settings → Privacy → Your data → **Shared chats → Manage**; columns are Name, Date shared, Location, Unshare, and each row carries the sharing scope beneath its title. — checked 2026-10-02
- **Confidence:** `verified` for the panel, its path and its columns. Still **no Anthropic help article names it** — the documentation gap is real even though the feature is not.

- **Setting:** `Shared artifacts` → **Manage** · `Uploaded files` → **Manage** · `Your feedback` → **Manage** · `Memory preferences` → **Manage**
- **Where:** Settings → Privacy → **Your data**, alongside Export data and Shared chats
- **Default:** Each lists whatever exists; these are management surfaces, not toggles.
- **Exposes:** Nothing new — but they matter because **each is a separate store with its own lifecycle.** Deleting a conversation does not clear an uploaded file, revoke a shared artifact, or withdraw submitted feedback (feedback is training-eligible and 5-year-retained per §1).
- **Recommend:** Audit all four alongside Shared chats. Most people have never opened three of them.
- **Risk:** Medium
- **Evidence:** confirmed by direct observation (live read of a consumer Max account, 2026-10-02) — checked 2026-10-02
- **Confidence:** `verified` for existence, labels and path; `unresolved` for what each panel's contents look like when populated, which was not inspected.

- **Setting:** *(settings sections absent from this file)* `Design systems` · `Reflect` · `Time and focus`
- **Where:** Settings navigation, between Memory and Claude Code
- **Default:** **`unresolved` — these three sections exist in the live settings navigation and are not documented anywhere in this file.** They were observed but not opened.
- **Exposes:** Unknown. `Reflect` and `Time and focus` in particular sound like they could carry activity-derived data.
- **Recommend:** **Open them before relying on this file as a complete inventory of Claude's settings surface.** Their absence here is a known gap, not an assertion that they are empty.
- **Risk:** Cannot rate
- **Evidence:** observed in the settings navigation (live read of a consumer Max account, 2026-10-02) — checked 2026-10-02
- **Confidence:** `unresolved`

## 5. Retention & deletion

- **Setting:** Delete conversation
- **Where:** Chat list → conversation → delete
- **Default:** Manual. Deleted chats are *"Removed from your chat history immediately"* and *"Deleted from our back-end storage systems within 30 days."* Also: *"If you delete a conversation with Claude it will not be used for future model training."*
- **Exposes:** Until deleted, chats stay in history and — with model improvement on — in training pipelines.
- **Recommend:** Delete anything sensitive promptly. Deletion is the one action that reliably pulls a conversation out of future training.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/10023548-how-long-do-you-store-my-data ; https://www.anthropic.com/news/updates-to-our-consumer-terms — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(derived)* Consumer retention window
- **Where:** Governed by the model-improvement toggle at https://claude.ai/settings/data-privacy-controls
- **Default:** Training **on** → *"we may retain your data in a de-identified format for up to 5 years"* in training pipelines. Training **off** → *"you'll continue with our existing 30-day data retention period."* **Caveat:** the current Privacy Center retention article (updated 2026-07-01) has a "Standard Retention Timeframe" heading with **no duration text under it**, and states only that turning the setting off means Anthropic *"will not use your previous or new chats or coding sessions for future model training"* — it does not restate the 30-day figure. The 30 days is verified from the Aug-2025 news post and the Claude Code data-usage page, not the current retention article. Chats you keep stay visible in history indefinitely, so "30 days" plainly describes backend/training-pipeline retention, not your chat list.
- **Exposes:** At default, five years of conversations in training infrastructure.
- **Recommend:** Turn model improvement off, and don't treat the 30-day figure as a deletion guarantee — delete explicitly.
- **Risk:** High
- **Evidence:** https://www.anthropic.com/news/updates-to-our-consumer-terms ; https://privacy.claude.com/en/articles/10023548-how-long-do-you-store-my-data ; https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified` for the 5-year and 30-day figures as published; `unresolved` on exactly which store the 30 days applies to — Anthropic's two documents don't line up.

- **Setting:** Export data
- **Where:** Settings → Privacy → **Export data**
- **Default:** Manual. Includes *"Conversation data and the user data for your account"*; download link emailed, **expires 24 hours** after delivery, and you must stay signed in. Free/Pro/Max via web or Desktop only — **not mobile**. Team/Enterprise members must ask their Primary Owner.
- **Exposes:** The export file is your entire history in plaintext — the most sensitive artifact you own.
- **Recommend:** Export before deleting an account or leaving a plan; store encrypted.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/9450526-export-your-claude-data — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Delete Account
- **Where:** Initials/name lower left → Settings → **Account** → **Delete Account**
- **Default:** Manual. Cancel Pro/Max and *"wait until the end of your current subscription period"* first; multiple accounts on one email must be specified individually.
- **Exposes:** You lose access to saved chats. **Post-deletion backend retention is not stated** — the article defers to the retention article, which gives no account-deletion figure.
- **Recommend:** Export first, then delete. Don't assume deletion purges flagged content — the 2-year/7-year flagged windows are stated to survive.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/10023660-deleting-claude-accounts — checked 2026-10-02
- **Confidence:** `verified` on the path; `unresolved` on post-deletion retention

- **Setting:** Custom data retention / **Chat retention** *(admin)*
- **Where:** Organization settings → Data and privacy. https://claude.ai/admin-settings/data-privacy-controls
- **Default:** **Enterprise only.** *"Data is retained indefinitely unless a custom retention period is set."* Minimum settable period **30 days** (*"each month is counted as 30 days"*). Primary Owner or Owner only.
- **Exposes:** At default, every chat and project in the org is kept indefinitely and is exportable by the Primary Owner.
- **Recommend:** Set a finite period. It applies **retroactively** — *"any data that falls outside the new period is scheduled for permanent deletion as soon as you save."* Carve-outs: covers chats and projects only, **not** Claude Design, Claude Tag, Claude Managed Agents, or Claude Code on the web.
- **Risk:** High
- **Evidence:** https://privacy.claude.com/en/articles/10440198-configure-custom-data-retention-controls-for-enterprise-plans ; https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(derived)* Commercial / API standard retention
- **Where:** No toggle; contractual
- **Default:** Anthropic *"automatically delete[s] inputs and outputs on our backend within 30 days of receipt or generation"* for API, Console, Team and Enterprise. Flagged chats: **2 years** for inputs/outputs, **7 years** for classification scores.
- **Exposes:** 30 days of prompts and completions at rest under AES-256 disk encryption.
- **Recommend:** Pursue ZDR if you process client-confidential prompts at volume.
- **Risk:** Medium
- **Evidence:** https://privacy.claude.com/en/articles/7996866-how-long-do-you-store-my-organization-s-data — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Claude Code local session transcripts / `cleanupPeriodDays`
- **Where:** `~/.claude/projects/` on disk; period set via `cleanupPeriodDays`
- **Default:** *"Claude Code clients store session transcripts locally in plaintext under `~/.claude/projects/` for 30 days by default."* Transcripts from sessions started or last continued in Claude Desktop or Cowork are **exempt from that limit by default**.
- **Exposes:** Plaintext copies of every session — including sensitive values you pasted — on your disk, and in Cowork's case indefinitely. Cowork local history is *"not subject to Anthropic's standard data retention policies, and admins cannot centrally manage or delete it."*
- **Recommend:** Lower `cleanupPeriodDays`, ensure FileVault/BitLocker, clear `~/.claude/projects/` after sensitive engagements.
- **Risk:** High
- **Evidence:** https://code.claude.com/docs/en/data-usage ; https://support.claude.com/en/articles/13455879-use-claude-cowork-on-team-and-enterprise-plans — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Export logs *(audit logs, admin)*
- **Where:** Organization settings → Data and Privacy → **Export logs**
- **Default:** **Enterprise only.** Aggregates *"all audit logs for the organization within the past 180 days"*; link live 24 hours. Owners and Primary Owners only. Orgs using customer-managed encryption keys must use the Compliance API instead.
- **Exposes:** Timestamps, actor, event type, **IP addresses**, device details. Chat and project **titles and content are excluded** (identifiers only) — though *"chat inputs/outputs will be exportable by Primary Owners via data exports."*
- **Recommend:** Members should know an Owner can export a 180-day activity trail including IPs, and separately can export chat content.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/9970975-access-audit-logs — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(derived)* Compliance API / Activity Feed retention
- **Where:** https://platform.claude.com/docs/en/manage-claude/compliance-api
- **Default:** **Activity Feed: 6 years.** **Local session transcripts** (Cowork, Claude Code on users' machines): **6 years by default**, or the org's custom retention period when a finite one is set. **Remote session transcripts** (Cowork in the cloud): **6 years** unless a user deletes sooner. ZDR local sessions are not captured. Under HIPAA readiness, only Cowork and Claude Code local sessions are captured, retained **30 days**.
- **Exposes:** A six-year, organization-readable archive of local agent sessions — materially longer than the 30-day figure most people associate with Claude.
- **Recommend:** Set a finite org retention period. The 6-year local-session default is the biggest sleeper retention number in the product.
- **Risk:** High
- **Evidence:** https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified`

## 6. Voice, audio & camera

- **Setting:** Voice mode *(sound-wave icon)*
- **Where:** Mobile: icon beside the microphone in the input field. Web/Desktop: sound-wave symbol lower right. Voice selection: Settings → General → **Voice settings**; language at Settings → General → Voice → **Language**.
- **Default:** Beta, **all plans**. Opt-in per use.
- **Exposes:** *"Textual transcripts of your audio conversations are saved in your chat history just like text conversations."* Audio itself is not retained. Transcripts then inherit your training/retention settings.
- **Recommend:** Fine to use — but the transcript is an ordinary chat, subject to the 5-year training window if model improvement is on.
- **Risk:** Low
- **Evidence:** https://support.claude.com/en/articles/11101966-use-voice-mode — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Dictation *(mobile microphone)*
- **Where:** Microphone icon in the mobile input field; OS mic permission at Settings → Claude
- **Default:** Opt-in per use
- **Exposes:** *"After converting your speech input to text, we delete your audio recording but the text of your chat will be retained in accordance with our retention periods."* Voice recordings are not used for training; *"If you have allowed us to use your chats or coding sessions to improve Claude, the transcribed text may be used in accordance with your privacy settings."*
- **Recommend:** Safe for audio, but treat the transcript as text you typed. The article names no third-party speech provider — if that matters, it is unresolved.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/10067979-what-personal-data-is-collected-when-using-dictation-on-the-claude-mobile-apps — checked 2026-10-02
- **Confidence:** `verified` on handling; `unresolved` on subprocessors

- **Setting:** *(derived)* Computer use — screenshot capture
- **Where:** Cowork / computer use; enabling toggle in §7
- **Default:** When computer use runs: *"computer use will process and collect screenshots from the computer's display that Claude uses to interpret and interact with the interface, along with the user's Inputs and Outputs."* Screenshots go to Anthropic's backend; *"Anthropic will automatically delete all screenshots from our backend within 30 days, unless the customer and Anthropic have agreed to different terms."*
- **Exposes:** Images of whatever was on screen — other apps, open tabs, notifications — uploaded and held 30 days.
- **Recommend:** Close unrelated windows and sign-in detail managers before any computer-use session. The most under-appreciated exposure in the agentic surface.
- **Risk:** High
- **Evidence:** https://privacy.claude.com/en/articles/10030352-what-personal-data-will-be-processed-by-computer-use — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Camera / Photos access *(mobile)*
- **Where:** iOS Settings → Claude
- **Default:** `unresolved` as a Claude-documented setting. The App Store privacy label lists **User Content (photos or videos)** among data linked to you but does not list camera or microphone as requested permissions; iOS gates both behind a system prompt regardless.
- **Exposes:** Images you attach become ordinary chat content under your retention and training settings.
- **Recommend:** Grant photo access as "Selected Photos", not full library.
- **Risk:** Medium
- **Evidence:** https://apps.apple.com/us/app/claude-by-anthropic/id6473753684 — checked 2026-10-02
- **Confidence:** `reported` — App Store label read via search extraction; no Anthropic article enumerating camera/photo permissions was fetched.

## 7. Agentic / computer-use permissions

- **Setting:** Permission mode — **Manually approve** / **Automatically approve** / **Skip all approvals**
- **Where:** Claude in Chrome → dropdown on the chat input
- **Default:** **"Automatically approve" is the default in the Cowork side panel** — Claude screens its own actions and pauses only when something needs approval. The classic side panel instead shows a plan up front with **Approve plan** / **Make changes**. The preference persists across sessions.
- **Exposes:** In Auto, Claude acts on live logged-in pages without per-action confirmation; in Skip, with no checks at all.
- **Recommend:** **Manual.** The default is convenience-first, and this is a browser holding your authenticated sessions.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide ; https://support.claude.com/en/articles/12902428-use-claude-in-chrome-safely ; https://support.claude.com/en/articles/12012173-get-started-with-claude-in-chrome — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** **Always allow actions on this site** / **Allow all for this website** / **Allow this time only** / **Deny**
- **Where:** The per-action approval prompt in the side panel
- **Default:** No site pre-approved; you grant per site
- **Exposes:** "Always allow" gives Claude standing permission to act on that domain without asking. Even then, Claude *"still asks for your explicit approval before downloading a file, entering potentially sensitive information into a page, or granting authorizations."* Hard-blocked regardless: purchases and financial transactions, creating accounts, handling credit-card or ID data, downloads from untrusted sources, permanent deletions, investment advice, executing trades, modifying system files, and following instructions found in email or web content. Adult and known-pirated sites blocked; financial sites require permission.
- **Recommend:** Use "Allow this time only". Anthropic's own guidance: avoid banking, healthcare and legal sites, and note *"the risk is not zero"* — internal testing puts prompt-injection attack success *"less than 0.08%"*, which is not zero.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide ; https://support.claude.com/en/articles/12902428-use-claude-in-chrome-safely — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Permissions page *(approved sites, revoke, permission history)*
- **Where:** Claude extension icon → three dots → **Extension settings** → Permissions
- **Default:** Empty until you grant
- **Exposes:** Nothing; it is the review surface.
- **Recommend:** Review and revoke monthly — site grants accumulate silently.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Enable computer use *(Cowork desktop)*
- **Where:** Settings → General (under Desktop app) → **Enable computer use**. macOS 15+ defaults to background access; **Full control** mode is in the same menu.
- **Default:** **Pro and Max only** — *"Team and Enterprise plans don't have access to computer use at this time."* Claude *"asks for your permission before accessing each application"* and you *"must approve before Claude can interact with that app."* Access order: connectors → browser → screen interaction. *"Some apps are off-limits by default,"* specifically *"investment and trading platforms, cryptocurrency."* You can also *"Prevent Claude from accessing certain apps by adding them to a blocklist."*
- **Exposes:** Screen-level access to approved apps, with screenshots uploaded and kept 30 days (§6).
- **Recommend:** Off unless actively needed; stay on background access rather than Full control; blocklist sign-in detail managers, banking and messaging apps.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork — checked 2026-10-02
- **Confidence:** `verified` on availability, defaults, path; `unresolved` on exact wording of the per-app permission prompt

- **Setting:** 1Password integration *(Claude in Chrome)*
- **Where:** Organization settings → Claude in Chrome
- **Default:** **Off.** Allows sign-in detail filling for sign-in tasks on macOS.
- **Exposes:** On, an agent can retrieve and type sign-in details from your sign-in detail manager.
- **Recommend:** Keep off. **Admin-lockable:** members cannot override.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/13065128-claude-in-chrome-admin-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** WebFetch domain safety check / `skipWebFetchPreflight`
- **Where:** Claude Code settings file
- **Default:** **On for every provider**, and *not* disabled by `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`. *"Only the hostname is sent, not the full URL, path, or page contents."* Passing hostnames cached 5 minutes.
- **Exposes:** Every hostname Claude Code fetches is sent to `api.anthropic.com` — a log of which domains you browse via the tool.
- **Recommend:** Leave on. Disabling removes the blocklist check; if you must, pair with `WebFetch` permission rules.
- **Risk:** Low
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Bypass permissions mode / Auto permissions mode *(Claude Code, admin)*
- **Where:** Organization settings → Claude Code
- **Default:** `unresolved`
- **Exposes:** Bypass mode lets Claude Code run commands without approval.
- **Recommend:** Disable bypass mode org-wide.
- **Risk:** High
- **Evidence:** https://platformsecurity.com/blog/how-to-secure-your-claude-enterprise-tenant — checked 2026-10-02
- **Confidence:** `reported` — third-party inventory; not corroborated against an Anthropic page.

## 8. Admin / workspace plane (Team, Enterprise)

- **Setting:** Enable for your team *(Claude in Chrome)*
- **Where:** Organization settings → Claude in Chrome
- **Default:** **Team: enabled by default. Enterprise: disabled by default** — but documented to turn **on September 10, 2026 unless already disabled**. Members cannot override.
- **Exposes:** Browser-agent access to members' authenticated sessions.
- **Recommend:** **That date has passed.** Enterprise admins who never touched this are now enabled — check immediately. **Admin-lockable:** yes.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/13065128-claude-in-chrome-admin-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Allowlist / Blocklist *(Claude in Chrome)*
- **Where:** Organization settings → Claude in Chrome
- **Default:** Neither configured. Allowlist restricts Claude to specified domains only; Blocklist blocks sites regardless of allowlist. Members cannot override either.
- **Exposes:** Unset, members can grant Claude access to any non-category-blocked site.
- **Recommend:** Run an allowlist. **Admin-lockable:** yes.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/13065128-claude-in-chrome-admin-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Cowork side panel *(Enterprise)*
- **Where:** Organization settings → Claude in Chrome (requires Cowork enabled in Organization settings → Cowork)
- **Default:** **Disabled.** Members cannot override.
- **Exposes:** Promotes the browser side panel into a full Cowork session, which defaults to "Automatically approve".
- **Recommend:** Leave disabled until you've reviewed the Auto-approve posture.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/13065128-claude-in-chrome-admin-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Enable for your organization *(Cowork)*
- **Where:** Organization settings → Cowork
- **Default:** **On by default for both Team and Enterprise.** No member-level override; Enterprise can scope with groups and custom roles.
- **Exposes:** Cowork agent sessions org-wide. Local sessions store conversation history on users' machines, outside Anthropic's retention policy and outside admin reach — *"admins cannot centrally manage or delete it."* Cloud sessions save to the member's Claude account.
- **Recommend:** Disable, or scope to named groups, until you've accounted for ungoverned local transcripts.
- **Risk:** High
- **Evidence:** https://support.claude.com/en/articles/13455879-use-claude-cowork-on-team-and-enterprise-plans — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Organization settings → Data and privacy *(group)*: **Chat retention**, **Location metadata**, **Rate chats**, **Share chats**, **Share chats using connectors**, **Public projects**, **Share projects**, **Export logs**
- **Where:** https://claude.ai/admin-settings/data-privacy-controls
- **Default:** Verified individually above where documented: Share projects **on**, Public projects **on**, Chat retention **indefinite** (Enterprise). **Location metadata** and **Rate chats** defaults `unresolved`.
- **Exposes:** This one page governs retention, sharing reach, and the feedback-to-training path for the whole org.
- **Recommend:** Treat as the org's privacy control panel and review after every Anthropic release — third-party guidance observes that *"new settings frequently ship enabled by default."*
- **Risk:** High
- **Evidence:** https://privacy.claude.com/en/articles/10440198-configure-custom-data-retention-controls-for-enterprise-plans ; https://support.claude.com/en/articles/9927533-control-project-sharing-for-your-organization ; https://support.claude.com/en/articles/10504844-manage-user-feedback-settings-on-team-and-enterprise-plans — checked 2026-10-02
- **Confidence:** mixed — see each item

- **Setting:** Organization settings → Capabilities *(Memory, Web search, Ask Org, Interactive content, Artifact connectors, Inline visualizations)*
- **Where:** Organization settings → Capabilities; Enterprise per-role at Organization settings → Roles → role → Capabilities
- **Default:** **Memory: off per member until the Owner enables it** (`verified`). Other capability defaults `unresolved` — only a third-party inventory enumerates them.
- **Exposes:** Each capability widens what Claude can read or render for members.
- **Recommend:** Enable deliberately, per role on Enterprise. **Admin-lockable:** yes for memory; presumed for the rest.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context ; https://platformsecurity.com/blog/how-to-secure-your-claude-enterprise-tenant — checked 2026-10-02
- **Confidence:** `verified` (Memory); `reported` (the rest)

- **Setting:** Role-based permissions — **Privacy: Can manage**
- **Where:** Organization settings → Roles → role → Capabilities
- **Default:** Enterprise only. Primary Owners and Owners hold it inherently; custom roles need Privacy set to "Can manage" to change sharing and privacy settings.
- **Exposes:** Anyone holding it can change org retention and sharing posture.
- **Recommend:** Grant to as few people as possible; review in audit logs.
- **Risk:** Medium
- **Evidence:** https://support.claude.com/en/articles/9927533-control-project-sharing-for-your-organization ; https://support.claude.com/en/articles/13930458-set-up-role-based-permissions-on-enterprise-plans — checked 2026-10-02
- **Confidence:** `verified` for the Privacy permission gate; `reported` for the broader RBAC article

- **Setting:** Compliance API
- **Where:** https://platform.claude.com/docs/en/manage-claude/compliance-api
- **Default:** Claude Enterprise and Claude Console customers. Covers the Activity Feed; for Enterprise also the directory of users/roles/groups across linked orgs, effective settings per org, **the underlying chats, files and projects** in claude.ai orgs, and Cowork, Claude Code, Claude Science, Claude for Microsoft 365 and Claude in Chrome sessions.
- **Exposes:** Programmatic read access to member conversation content and agent session transcripts — far broader than the CSV audit-log export.
- **Recommend:** Members on Enterprise should assume chat content is retrievable by their organization. Admins: scope and log Compliance API sign-in details like any SIEM integration.
- **Risk:** High
- **Evidence:** https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified` on scope and retention; the Compliance API page itself not fetched directly

## 9. API / developer plane

- **Setting:** *(default posture)* No training on commercial data
- **Where:** Contractual, no toggle
- **Default:** *"we will not use your inputs or outputs from our commercial products (e.g. Claude for Work, Anthropic API, Claude Gov, etc.) to train our models."* Exceptions: you *"explicitly report feedback or bugs"* or *"otherwise choose to allow us to use your data."*
- **Exposes:** Nothing by default. Practical leak paths are the **Rate chats** toggle (§1) and the Development Partner Program (§1).
- **Recommend:** Close both leak paths rather than relying on the headline promise.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Zero data retention (ZDR)
- **Where:** Sales/account-team gated. Verify at **Settings → Privacy Controls → Data retention period**.
- **Default:** **Not enabled.** Standard is 30-day retention. Covers *"eligible Anthropic APIs, Anthropic products that use your Commercial organization [API access value] (including Claude Code accessed via the API), and Claude Code for Enterprise plans."* Explicitly **not** in the standard Enterprise plan — *"it is enabled on a per-organization basis by your account team after confirming eligibility."* Consumer plans don't qualify.
- **Exposes:** Without it, prompts and responses sit at rest 30 days. **With it, these still persist:** *"User Safety classifier results in order to enforce our Usage Policy"*; flagged inputs/outputs **up to 2 years**; Covered Models' mandatory retention. Stateful features are not ZDR-eligible — code execution and programmatic tool calling retain container data **up to 30 days**, and using one *"is a choice to step outside your ZDR arrangement for that specific data."* Web search and web fetch are ZDR-eligible, but their **dynamic filtering** is not.
- **Recommend:** Pursue ZDR, then audit which API features you actually call — a single `code_execution` call silently exits the arrangement.
- **Risk:** High *(without it)*
- **Evidence:** https://privacy.claude.com/en/articles/8956058-i-have-a-zero-data-retention-agreement-with-anthropic-what-products-does-it-apply-to ; https://platform.claude.com/docs/en/manage-claude/api-and-data-retention ; https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Workspace **Privacy controls** → 30-day data retention
- **Where:** Console → Settings → Workspaces → select workspace → **Privacy controls**. https://platform.claude.com/settings/workspaces
- **Default:** Off for ZDR organizations; *"Workspaces without an override continue to follow the organization default."*
- **Exposes:** Enabling carves a 30-day-retention hole in an otherwise-ZDR org so that workspace can call Covered Models.
- **Recommend:** Use a dedicated workspace for Covered Models rather than relaxing the org default.
- **Risk:** Medium
- **Evidence:** https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** HIPAA compliance card
- **Where:** Console → **Settings → Data retention** (https://platform.claude.com/settings/privacy), visible to admins with the HIPAA management permission
- **Default:** Not enabled. Self-serve via Anthropic's standard BAA; negotiated BAAs via sales.
- **Exposes:** Once accepted, *"the configuration is permanent and cannot be disabled by an administrator."* Enforced org-wide; non-eligible features return HTTP 400. Does **not** cover Claude Code, Claude Platform on AWS, or Microsoft Foundry, nor PHI processing through the Console UI. Do not put PHI in JSON schema definitions — compiled grammars are cached separately and *"do not receive the same PHI protections."*
- **Recommend:** Use a separate organization for HIPAA workloads. It cannot be undone.
- **Risk:** High
- **Evidence:** https://platform.claude.com/docs/en/manage-claude/api-and-data-retention — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Data retention practices for Covered Models
- **Where:** Policy, not a toggle
- **Default:** Conversation content is *"not retained by default; the exception is Covered Models, which require 30-day retention."*
- **Exposes:** Using a Covered Model forces 30-day retention even in an otherwise-ZDR org.
- **Recommend:** Check model eligibility before routing sensitive traffic.
- **Risk:** Medium
- **Evidence:** https://platform.claude.com/docs/en/manage-claude/api-and-data-retention ; https://privacy.claude.com/en/articles/15425996-data-retention-practices-for-covered-models — checked 2026-10-02
- **Confidence:** `verified` on the 30-day requirement; the Covered Models article not fetched

- **Setting:** `DISABLE_TELEMETRY`
- **Where:** Environment variable, or `settings.json`
- **Default:** **Metrics on** connecting to the Claude API; **off** on Bedrock, Google Cloud Agent Platform, Microsoft Foundry, Claude Platform on AWS.
- **Exposes:** *"latency, reliability, and usage patterns, sent to Anthropic and to third-party logging infrastructure over TLS. Metrics never include your code, prompts, or file paths."*
- **Recommend:** Set `=1` for no third-party operational telemetry — but note the cost: it *"also disables feature-flag evaluation, which can make Remote Control unavailable,"* and Claude Code then falls back to built-in defaults for gated behavior. Any non-empty value counts as set, including `0` and `false`.
- **Risk:** Low
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `DISABLE_ERROR_REPORTING`
- **Where:** Environment variable, or `settings.json`
- **Default:** **On only when all of:** you sign in with a **Pro or Max** subscription, run **v2.1.198 or later**, connect directly to the Claude API, and your org has no ZDR or HIPAA agreement. Off on all third-party providers.
- **Exposes:** Error messages and stack traces from Claude Code internals to a third-party error-tracking service. *"Claude Code redacts known patterns of [sensitive values], file paths, email addresses, and other personal information before anything leaves your machine"* — known patterns, so not a guarantee.
- **Recommend:** Set `=1` on machines with client code; it does not break feature flags the way `DISABLE_TELEMETRY` does.
- **Risk:** Medium
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`
- **Where:** Environment variable, or `settings.json`
- **Default:** Unset. Setting it disables all non-essential traffic at once — autoupdater, bug command, error reporting, telemetry — and suppresses the session-quality survey. Does **not** affect the WebFetch safety check or official-marketplace auto-install (`CLAUDE_CODE_DISABLE_OFFICIAL_MARKETPLACE_AUTOINSTALL`).
- **Exposes:** Left unset, metrics/error/feedback channels run per the entries above.
- **Recommend:** The blunt instrument — effective, but it disables the autoupdater too, so patch manually. On a signed-in Claude apps gateway session, analytics, error reporting and survey ratings are already disabled by the gateway sign-in detail with no way to re-enable.
- **Risk:** Low
- **Evidence:** https://code.claude.com/docs/en/data-usage — checked 2026-10-02
- **Confidence:** `verified`

## 10. Mobile & OS app permissions

- **Setting:** Calendar / Location / Reminders / Health *(iOS app integrations)*
- **Where:** Requested contextually in-app with **Allow once**, **Always allow**, **Don't allow**. Manage at iOS **Settings → Claude**; Health at **Settings → Health → Data Access & Devices → Claude**.
- **Default:** Not granted — Claude *"requests permissions contextually rather than upfront."* Messages and email need no permission because they route through the device share sheet. **Health data is *"not saved to memory by default."***
- **Exposes:** Granting lets Claude read calendar events, reminders, coarse location and Health records to answer requests; Anthropic says Claude *"only accesses the data necessary for each specific request."* **Not documented:** which of that data is transmitted to Anthropic's servers versus handled on-device — treat it as transmitted.
- **Recommend:** **Allow once** rather than **Always allow**, especially for Health. Leave "Include sensitive topics in memory" off (§2) so health context isn't persisted.
- **Risk:** High *(Health)* / Medium *(Calendar, Reminders, Location)*
- **Evidence:** https://support.claude.com/en/articles/11869619-use-claude-with-ios-apps — checked 2026-10-02
- **Confidence:** `verified` on permissions, labels, paths; `unresolved` on server-side data flow

- **Setting:** *(App Store privacy label)* Data linked to you
- **Where:** https://apps.apple.com/us/app/claude-by-anthropic/id6473753684
- **Default:** As declared by Anthropic PBC: coarse **Location**; **Contact Info** (email, name, phone); **User Content** (photos or videos); **Identifiers** (user ID, device ID); **Usage Data**; **Diagnostics**. Apple notes labels are developer-declared and unverified.
- **Exposes:** Device and user identifiers tied to usage, independent of your in-app privacy toggles.
- **Recommend:** Assume mobile usage is identity-linked; use web with incognito for anything you want loosely coupled to your identity.
- **Risk:** Medium
- **Evidence:** https://apps.apple.com/us/app/claude-by-anthropic/id6473753684 — checked 2026-10-02
- **Confidence:** `reported` — read via search extraction, not a direct fetch

- **Setting:** Location metadata
- **Where:** Settings → Privacy (consumer); Organization settings → Data and privacy (admin). https://claude.ai/settings/data-privacy-controls
- **Default:** `unresolved` for consumers — Anthropic's article points at the dashboard without naming the toggle or its default. **The label is confirmed as "Location metadata" by direct observation (live read of a consumer Max account, 2026-10-02), under Settings → Privacy → Preferences**, with the description "Allow Claude to use coarse location metadata (city/region) to improve product experiences." The observed account had it **on**; whether that is the shipped default is still unconfirmed.
- **Exposes:** Anthropic uses *"IP address to determine coarse-grained location (city/region level)"* for optional features like web search, and separately *"IP address and other signals to infer coarse-grained location (country/region level)"* for security and anti-abuse — the second is **mandatory and "cannot be toggled off."** Mobile and extension location access is managed at the device level.
- **Recommend:** Turn the optional product-enhancement use off; accept that the security-purpose inference remains.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/11186740-does-claude-use-my-location ; https://joindeleteme.com/ai-privacy-settings/claude-privacy-settings-guide/ — checked 2026-10-02
- **Confidence:** `verified` on behavior; `reported` on the label; `unresolved` on default

- **Setting:** Your privacy choices *(cookies)*
- **Where:** claude.ai → **Learn More** → **Your privacy choices**; anthropic.com footer → **Privacy Choices**; or a browser-level global privacy control signal
- **Default:** Three categories: **Necessary** (*"cannot be refused"*), **Analytics**, **Marketing**. Marketing cookies support *"Targeted Marketing"* through Google, Facebook, Reddit, TikTok and Twitter/X. **Regional defaults `unresolved`** — the article gives no GDPR/CCPA-specific configuration.
- **Exposes:** At default, your claude.ai visits feed conversion tracking on five ad platforms.
- **Recommend:** Reject Analytics and Marketing, and enable a browser-level global privacy control so the signal persists across devices.
- **Risk:** Medium
- **Evidence:** https://privacy.claude.com/en/articles/10023541-what-cookies-does-anthropic-use — checked 2026-10-02
- **Confidence:** `verified` on categories and controls; `unresolved` on defaults by region

- **Setting:** *(capability gaps worth knowing)*
- **Default:** **Data export is not available on mobile** (web or Desktop only). **Monthly recap is not available on mobile.** Memory and incognito are available on mobile.
- **Recommend:** Do privacy housekeeping — export, share-link audit, account deletion — from the web app.
- **Risk:** Low
- **Evidence:** https://privacy.claude.com/en/articles/9450526-export-your-claude-data ; https://support.claude.com/en/articles/15672559-see-your-monthly-recap — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Android app permissions
- **Where:** Google Play data-safety section / Android app info
- **Default:** **`unresolved`.** The Android permission set and Play data-safety declarations were not verified in this pass. Do not assume parity with iOS.
- **Recommend:** Check Android Settings → Apps → Claude → Permissions directly.
- **Risk:** Unknown
- **Evidence:** none — `unresolved`
- **Confidence:** `unresolved`

## Volatile

Re-check these first.

1. **"Help improve our AI models" default.** The label is now settled by direct observation and matches the help-center string. What remains open is the **new-account default** — the Aug-2025 change is under 14 months old, the Privacy Policy was last updated **2026-09-10**, and the help article still declines to state one. Expect wording and consent flow to keep shifting under GDPR pressure — EU legal analysis has called the pre-selected toggle potentially unlawful.
2. **Consumer retention documentation.** The retention article (updated **2026-07-01**) has an empty "Standard Retention Timeframe" section and no longer restates the 30-day opt-out window the Aug-2025 post promised. Either the policy changed or the doc regressed. Re-verify before relying on "30 days".
3. **Claude in Chrome on Enterprise.** Documented to flip from disabled to **enabled on September 10, 2026 unless already disabled** — that date has passed, so Enterprise admins who never touched it are now enabled. Highest-urgency admin item here.
4. **Cowork.** Recent, already **on by default for Team and Enterprise**, with local transcripts outside admin control and a 6-year Compliance API default for local sessions. Admin surface is new and expanding.
5. **Memory.** Moved from **Settings → Capabilities** to **Settings → Memory** with a new deep link; both paths still live. "Include sensitive topics in memory" and per-chat memory are recent additions. The monthly-recap article still references the legacy path.
6. **Domain migration.** `privacy.anthropic.com` → `privacy.claude.com`, `support.anthropic.com` → `support.claude.com`, recent enough that Anthropic's own Claude Code docs still link to the old host. Expect stale links in third-party guides.
7. **Claude Code MCP policy.** `allowedMcpServers` behavior for `managed-mcp.json` servers **changed at v2.1.259** — managed servers an allowlist previously suppressed now load with no prompt or notice. `allowClaudeInChromeWithManagedMcp` requires v2.1.282+. Versioning fast.
8. **Error reporting in Claude Code.** Became default-on for Pro/Max sign-ins at **v2.1.198** — a default that got *more* permissive.
9. **Beta surfaces:** share-a-chat-by-email, artifact invite-by-email, inference hooks, Groups/RBAC.
10. **Anthropic Interviewer.** The Privacy Center now carries five articles about it, one covering *"sessions completed after September 29, 2026"* — three days before this check. An actively changing consumer data-collection product, not audited here.
11. **Admin defaults generally.** Third-party guidance observes *"new settings frequently ship enabled by default"* and recommends monthly review — consistent with what was found: Share projects on, Public projects on, Cowork on, Chrome auto-on for Enterprise.

### Unresolved, collected

New-account default for the training toggle · default for **Rate chats** · default for **Location metadata** (label now verified) · the contents and purpose of the **Design systems**, **Reflect** and **Time and focus** settings sections · per-tool connector permission defaults · cookie defaults by region · whether published artifacts are search-indexed · post-account-deletion backend retention · Android permission set · defaults for Claude Code **Bypass/Auto permissions mode** and **Restrict verified domain connectors** · which Organization → Capabilities toggles beyond Memory are on out of the box · the dictation speech-to-text subprocessor · exact wording of Cowork's per-app permission prompt.
