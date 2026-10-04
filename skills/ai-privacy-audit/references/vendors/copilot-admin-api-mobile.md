# Microsoft Copilot — admin, API and mobile planes

> **Last verified:** 2026-10-02 · Continues [copilot.md](copilot.md), which carries the header, the framing notes on the 2026-08-18 consumer fork, and categories 1–7.
> **Four surfaces kept separate throughout:** (a) consumer Copilot · (b) Microsoft Copilot work/school tenant · (c) Copilot in Windows incl. Recall · (d) GitHub Copilot

## 8. Admin / workspace plane

### Microsoft Edge policies

- **Setting:** `EdgeEntraCopilotPageContext`, `CopilotPageContext`, `CopilotCoworkToolActionsEnabled`, `AllowBrowsingWithCopilot`, `EdgeCopilotEnabled`
- **Where:** Microsoft Edge policy, per profile. `AllowBrowsingWithCopilot` is also recommendable (user-overridable) via the "Microsoft Edge - Default Settings" GP path.
- **Default:** `EdgeCopilotEnabled` — *"If you don't configure this policy, eligible users can use Copilot in Microsoft Edge and can turn off Copilot in the settings page."* Other verified policy names whose defaults were **not** individually checked: `CopilotCDPPageContext` (**marked obsolete**), `Microsoft365CopilotChatIconEnabled`, `CopilotAddressBarSuggestionsEnabled`, `CopilotNewTabPageEnabled`, `BrowsingWithCopilotAllowList`, `BrowsingWithCopilotBlockList`, `M365LinksAutoOpenCopilotEnabled`.
- **Exposes:** **`EdgeEntraCopilotPageContext` is the one to watch:** with it on, intranet page content, browsing history and video transcripts flow into Copilot in the side pane — **including for users without a Copilot licence**, since it covers *"Microsoft Copilot with enterprise data protection (EDP)"* as well as Business Chat. Partial mitigation: *"Copilot can't access page content on pages protected by data loss prevention (DLP) policies, even if this policy is enabled."*
- **Recommend:** **Disable `EdgeEntraCopilotPageContext` if you are relying on "Copilot Chat can't see org data" — it can, via the browser.** Non-EU tenants should not assume the EU default applies to them. All of these are `Can be mandatory: Yes` and `Per Profile: Yes`.
- **Risk:** High *(page context)* / Medium *(others)*
- **Evidence:** https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies ; .../edgeentracopilotpagecontext ; .../copilotpagecontext ; .../copilotcoworktoolactionsenabled ; .../edgecopilotenabled — checked 2026-10-02
- **Confidence:** `verified` (the five fetched individually) / `unresolved` (defaults for the remaining policy names)

### Windows: locked vs merely defaulted

- **Genuinely locked:** `AllowRecallEnablement` = `0` (bits removed; *"individual users can't enable Recall on their own"*) · `DisableAIDataAnalysis` = `1` (capture blocked, existing snapshots deleted) · `ConfigureAgentConnectors` = `1`/`2` (Force Enable / Force Disable) · `CopilotCoworkToolActionsEnabled` enabled or disabled (*"users can't change this setting on the Settings page"*) · `AllowBrowsingWithCopilot` enabled or disabled · AppLocker block on `MICROSOFT.COPILOT`.
- **Merely a default:** `ConfigureAgentConnectors` = `0` ("User in control") · **the Recall app and website filter lists** (*"Users will be able to add additional applications to exclude from snapshots using Recall settings"* — admins seed, users extend, and **cannot be prevented from extending**) · `SetMaximumStorageSpaceForRecallSnapshots` / `SetMaximumStorageDurationForRecallSnapshots` when unconfigured (*"unless the current user specifies a different value"*) · `SetCopilotHardwareKey` (*"Users can change the key assignment in Settings"*) · `EdgeEntraCopilotPageContext` / `CopilotPageContext` unconfigured.
- **The critical asymmetry:** an admin can **prevent** Recall entirely, but can **never enable capture** on a user's behalf — *"The choice to enable saving snapshots requires individual user opt-in consent."* Conversely, **there is no policy that forces a user's Recall filter lists to stay as the admin set them.**
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

### (d) GitHub Copilot — admin plane

- **Setting:** `Default policy for new features` *(and `Default availability for released models`)*
- **Where:** Enterprise → AI controls → Copilot → **Features & clients**. The same mechanism covers the **Copilot code review** policy on the Agents page and the **MCP servers in Copilot** policy on the MCP page.
- **Default:** **Enabled.** Verbatim: *"This policy is enabled by default. If you don't take action, unconfigured features will be enabled on October 22."* The models policy is already active; the features policy *"will start applying to new and existing GA features from October 22, 2026."*
- **Exposes:** ⚠️ **The single most urgent item in this file.** Twenty days from this check, any Copilot feature your enterprise or organization has left *unconfigured* — **including MCP server support and Copilot code review** — flips on automatically. **"We never turned that on" will stop being true without anyone acting.**
- **Recommend:** Before 2026-10-22, either *"disable the default policies in your enterprise or organization's settings"*, or *"explicitly disable individual features and models so that they are not eligible for automatic enablement."* **Explicit-disable is the safer pattern: it survives future default-policy changes.**
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/concepts/enterprise/default-availability — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Content exclusion
- **Where:** Repository Settings → Copilot → Content exclusion · Organization Settings → Copilot → Content exclusion · Enterprise → AI controls → Copilot → Content exclusion. YAML forms: `- "/PATH"`, or `"*": ["/PATH"]` / `REPOSITORY-REFERENCE:`.
- **Default:** **No exclusions configured** at any level.
- **Exposes:** When set, *"Inline suggestions will not be available in the affected files."* **Three documented leaks:** *"It's possible that Copilot may use semantic information from an excluded file if the information is provided by the IDE indirectly. Examples of such content include type information and hover-over definitions for symbols."* Exclusions *"currently do not apply to symbolic links or remote filesystem repositories."* And chat/agent coverage is partial — supported in Visual Studio, **VS Code Chat (not Edit or Agent modes)**, JetBrains, github.com, GitHub Mobile, the Copilot app and the CLI; **not supported** for chat/agent in Xcode or Eclipse. Propagation takes *"up to 30 minutes."*
- **Recommend:** Exclude sensitive values directories, customer-data fixtures and vendored third-party code — **but do not treat it as a boundary: type information still leaks, and VS Code Agent mode ignores it entirely, which is exactly where an agent has the most reach.**
- **Risk:** High *(because the gaps are in the highest-capability modes)*
- **Evidence:** https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/content-exclusion — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Suggestions matching public code *(enterprise/org enforcement)*
- **Where:** The **Privacy** section of the enterprise or organization Copilot policy page
- **Default:** **Allowed** for Copilot Business users — *"set to Allowed by default for Copilot Business users."*
- **Recommend:** Set to **Block** at enterprise level so it is not left to each developer. Whether an enterprise setting hard-locks organizations out of changing it is **`unresolved`**.
- **Risk:** Medium
- **Confidence:** `verified` (default for Business) / `unresolved` (lock semantics)

- **Setting:** *(organization and enterprise policy pages generally)*
- **Default:** Varies per policy. **GitHub does not publish a consolidated policy-by-policy default table** — the enterprise and organization how-to pages both describe the mechanism without enumerating defaults or lock behaviour.
- **Recommend:** **Export your current policy state before 22 October so you have a baseline to compare against.** Do not assume "unconfigured" means "off" after that date.
- **Risk:** Medium
- **Confidence:** `verified` (paths, mechanism) / `unresolved` (per-policy defaults, lock semantics)

- **Setting:** *(Copilot audit log and metrics)*
- **Where:** **Not located.** The documented path 404s.
- **Default:** **`unresolved`** — which Copilot events are recorded in the GitHub audit log, their retention period, and the click path to view them could not be confirmed.
- **Recommend:** **Do not promise GitHub Copilot audit coverage in a control narrative without confirming it in the enterprise UI directly.** Note that where blocked-firewall events occur, the record is a **PR comment**, not an audit log entry.
- **Risk:** Medium
- **Confidence:** `unresolved`

## 9. API / developer plane

### (b) Microsoft 365 Copilot — extensibility and APIs

- **Setting:** Copilot APIs (export / retrieval)
- **Default:** Governed by the Agents settings in §3b plus **Advanced package uploads**. Admin consent is required for anything touching the export or retrieval APIs.
- **Recommend:** Treat admin consent on these as a privacy event — the retrieval and export APIs reach Copilot interaction content.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/copilot-apis-overview — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Declarative agents, skills, MCP servers, custom engine agents
- **Default:** Governed by the Agents settings in §3b plus **Advanced package uploads**.
- **Exposes:** A critical governance statement: *"Using an API doesn't by itself select a package or distribution route. **Each part of a combined solution retains its own identity, authentication, deployment, distribution, and governance requirements.**"* A declarative agent *"can call an external API or remote MCP server through a supported action"* — **so a tenant-approved agent can be a hop to an unreviewed endpoint.**
- **Recommend:** **Review the *actions* of an approved agent, not just the agent.** Approval of the wrapper is not approval of what it calls.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/overview — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Custom Copilot connectors *(Graph connectors API)*
- **Default:** None exist until built. *"Building a custom connector requires a developer to define a schema, register the connection in Microsoft Entra ID, and write code to pull and push data."*
- **Exposes:** **The developer defines the ACL attached to each ingested item** — so Copilot's permission fidelity for that content is only as good as the connector author's code.
- **Recommend:** Treat custom connector ACL mapping as a security review item. Microsoft's own advice: *"Custom connectors offer flexibility but require maintenance. Use prebuilt connectors when possible."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/overview — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Teams Export APIs
- **Exposes:** *"For Microsoft Teams chats with Copilot, admins can also use Microsoft Teams Export APIs to view the stored data"* — **an additional programmatic read path to Copilot interaction content, alongside eDiscovery.**
- **Recommend:** Include in your privileged-access inventory.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy — checked 2026-10-02
- **Confidence:** `verified`

### (c) Copilot in Windows — developer plane

- **Setting:** `ms-recall` protocol URI
- **Default:** Available whenever the Recall component is installed.
- **Exposes:** *"If you're a developer and want to launch Recall, you can call the `ms-recall` protocol URI. When you call this URI, Recall opens and takes a snapshot of the screen."* **Any installed app can trigger a snapshot by protocol launch.**
- **Recommend:** **The strongest argument for removing the Recall optional component rather than merely toggling Save snapshots off.**
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `SetWindowDisplayAffinity` / `WDA_EXCLUDEFROMCAPTURE`
- **Where:** Win32 API (`winuser.h`)
- **Default:** Not set — windows are capturable by default.
- **Exposes:** The developer-side opt-out: *"By setting the flag `WDA_EXCLUDEFROMCAPTURE`, the window content won't show up in Recall or any other screenshot application."*
- **Recommend:** **If you ship a Windows app handling sensitive values or client data, set this.** It is the only mechanism that protects your users regardless of **their** Recall settings — and the one thing a consultant building client tooling can actually control.
- **Risk:** Low as a control; High if omitted from a sensitive app
- **Confidence:** `verified`

- **Setting:** `UserActivity.ContentInfo` labels / Recall DLP provider API / exported-snapshot decryption API
- **Exposes:** Apps can push sensitivity-label metadata to Recall; third parties can build DLP providers; and **there is a documented path for an app or website to decrypt exported Recall snapshots** given the user's export code.
- **Recommend:** Label-aware apps should supply ContentInfo. **The decryption API is precisely why the export code must never leave the user's hands.**
- **Risk:** Medium
- **Confidence:** `verified` (referenced from the parent doc; the individual API pages were not fetched)

- **Setting:** On-device model install / removal
- **Where:** **Settings → System → AI components** — remove or reinstall Phi Silica, Image Generation, Speech Recognition models
- **Default:** On Copilot+ PCs, Phi Silica and Speech Recognition are preinstalled on the NPU; **Image Generation is not preinstalled**. On GPU/CPU devices Phi Silica downloads on demand — *"several GB … in the background through Windows Update"*, with Microsoft telling developers to *"show a consent dialog before triggering the download."*
- **Exposes:** Multi-gigabyte background downloads triggerable by any app calling the API, and the presence of local generative models that apps can invoke.
- **Recommend:** Remove models you don't use; audit this page after installing AI-adjacent apps.
- **Risk:** Low
- **Evidence:** https://learn.microsoft.com/en-us/windows/ai/apis/ — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Semantic Search *(Windows AI Foundry)*
- **Default:** Private preview; **no user-facing control documented.**
- **Exposes:** A semantic index over local content, exposed to apps. Privacy controls are `unresolved`.
- **Recommend:** **Watch this. A general semantic index over local files is a Recall-class privacy surface without Recall's published controls.**
- **Risk:** Medium (`unresolved`)
- **Confidence:** `unresolved`

### (d) GitHub Copilot — developer plane

- **Setting:** *(what context is sent for completions, and its retention)*
- **Default:** `unresolved`. The code-suggestions concept page *"does not address data transmission, retention policies, or the scope of context sent during completions."* `docs.github.com/en/copilot/concepts/privacy` **404s**.
- **Exposes:** Unknown scope of surrounding-file context transmitted per completion. Content exclusion partially bounds it (§8d) but leaks type information.
- **Recommend:** **Do not make claims about GitHub Copilot completion context scope in a client-facing document.** Rely on content exclusion plus the Business/Enterprise DPA, and say the published detail is thin.
- **Risk:** Medium
- **Confidence:** `unresolved`

## 10. Mobile & OS app permissions

### (a) Consumer Copilot

- **Setting:** Copilot mobile privacy settings
- **Where:** Copilot mobile → menu → profile icon → **Account → Privacy** (training); menu → profile icon → **Memory**; **Profile → Connectors**; **Voice Settings** via menu → profile icon.
- **Default:** Same as desktop per setting — **but the paths differ, and Microsoft does not state that preferences sync across clients.**
- **Exposes:** A user who set training and memory preferences on the web may never have touched mobile.
- **Recommend:** **Set training, memory and ads opt-outs on every client separately, then verify each. Treat non-sync as the assumption.**
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls — checked 2026-10-02
- **Confidence:** `verified` (paths) / `unresolved` (whether settings sync)

- **Setting:** Share screen *(mobile camera / screen, Copilot Vision)*
- **Where:** Copilot mobile → start a **Voice** session → **Share screen** → end with **X**. OS camera permission required.
- **Default:** **Off**, per session, with a privacy notice on first use.
- **Exposes:** A live camera feed or phone screen to Microsoft's cloud for analysis, under the same 47-hour session retention and no-training commitments as desktop Vision.
- **Recommend:** **Revoke camera permission for Copilot at the OS level if you don't use mobile Vision** — a harder guarantee than the in-app control.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** *(full OS permission list for the Copilot mobile app)*
- **Default:** **`unresolved`.** **No Microsoft documentation enumerating the Copilot mobile app's OS permission requests or their defaults could be found.** The App Store and Play Store listings could not be read (the App Store ID 404'd; the Play listing returned only a title; the mobile-app support page 404s). What **is** verified: microphone is required for Voice and *"you can turn off Copilot access to your microphone in your platform settings"*; camera is required for mobile Vision; and the Microsoft privacy statement says Copilot *"will use your prompts, **location**, language, and related settings."*
- **Recommend:** **Audit the permission list on a real device rather than from documentation.** Deny location unless you use location-dependent prompts, and deny microphone and camera unless you use Voice and Vision. **Do not cite a permission matrix you have not seen on-device.**
- **Risk:** Medium
- **Confidence:** `unresolved`

- **Setting:** Microsoft Family Safety controls over Copilot *(under-18 accounts)*
- **Default:** Not configured. Baseline for under-18s: *"For young people, Copilot doesn't personalize results based on your conversation history, and it doesn't show you personalized ads"* — though *"You may see ads while using Copilot, but these ads are based on what you're asking about in your chat."*
- **Exposes:** Parents can *"Block access to the Copilot app or Copilot via browser"*, set time limits, and *"Choose which features are available… such as image generation, voice mode, group chat, or AI companions."* No exact UI paths are published (`unresolved`).
- **Recommend:** Use the **feature-level** controls rather than a blanket block — **group chat** and **AI companions** are the two newest and least-documented surfaces.
- **Risk:** Medium
- **Confidence:** `verified` (capabilities, baseline) / `unresolved` (click paths)

### (b) Microsoft 365 Copilot (tenant)

- **Setting:** Tenant Restrictions v2
- **Where:** Microsoft Entra — https://learn.microsoft.com/en-us/entra/external-id/tenant-restrictions-v2
- **Default:** Not configured.
- **Exposes:** ⚠️ **This is *the* control for the consumer-account bypass of EDP.** *"Users can sign in to the Microsoft Copilot app with a work or school account or a personal Microsoft account."* Microsoft's pointer is explicit: *"To manage whether users can sign in with personal accounts, see Tenant Restrictions v2."* Visual cues (different background colour, a "Work" label, a green shield) are **advisory only.**
- **Recommend:** **Configure it on managed devices.** Without it, the easiest way for a user to leave your data-protection boundary is to switch accounts inside the same app.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/copilot/manage — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Intune App Protection policies (APP / MAM)
- **Default:** Not configured.
- **Exposes:** Microsoft's Copilot-specific rationale: *"APP can prevent the inadvertent or intentional copying of Copilot-generated content to apps on a device that aren't included in the list of permitted apps."*
- **Recommend:** Deploy for mobile. **The only documented control over Copilot *output* leaving the managed app boundary on a device.**
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/security/zero-trust/copilots/zero-trust-microsoft-365-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Search *(Microsoft Search)* and Item insights
- **Where:** M365 admin center → **Settings → Search & intelligence**
- **Default:** **On.** *"By default, Microsoft Search is allowed and turned on. You can also enable Item insights and show recommended files. Users can turn off Item insights, but we recommend that it stays on."*
- **Exposes:** Item insights drives file recommendations and **the suggested-prompts-with-files behaviour that lets even unlicensed Copilot Chat users pull org files into a prompt.**
- **Recommend:** If you are trying to keep Copilot Chat web-only, **Item insights is a side channel worth reviewing** — and note it is user-overridable, so it is a default rather than a lock.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Pin Copilot Chat
- **Where:** M365 admin center → Copilot → Settings → User access → Pin Copilot Chat
- **Default:** In-app: **pinned.** *"Microsoft Copilot Chat is pinned by default for most users who are eligible for Copilot Chat."* Taskbar pinning: **off** — *"This setting is off by default."*
- **Exposes:** Discoverability only — **and the scope has eroded twice:** it *"no longer governs the Microsoft Copilot app"* (EEA/Switzerland from 2025-07-25; everywhere else from **2026-01-28**), and *"Chat remains available in the app navigation."*
- **Recommend:** **Do not use pinning as an access control** — it never blocked access and has been progressively decoupled. Pair any block with the **Custom link for blocked Microsoft Copilot app** setting, because unexplained blocks push people to personal accounts, **which is the one path with no EDP at all.**
- **Risk:** Low
- **Confidence:** `verified`

### (c) Copilot in Windows

- **Setting:** Copilot key and **Win+C** shortcut *(`Customize Copilot key on keyboard`)*
- **Where:** Settings → Personalization → Text input → Customize Copilot key on keyboard. **Deep link: `ms-settings:personalization-textinput-copilot-hardwarekey`** — the only AI-adjacent documented `ms-settings:` URI. Policy: `SetCopilotHardwareKey`.
- **Default:** **Configured.** The app settings table reads *"Copilot Key and Windows + C shortcut | ✅ Configured by default."* Short-press opens a lightweight prompt box; **long-press opens the voice controller.**
- **Exposes:** A dedicated hardware key that opens a cloud assistant, and **on long-press a live microphone session.**
- **Recommend:** **Remap to Search or a Custom app for any cohort where Copilot is restricted** — otherwise the hardware keeps inviting the behaviour your policy forbids.
- **Risk:** Medium
- **Confidence:** `verified`

- **Setting:** Uninstall the Microsoft Copilot app
- **Where:** Settings → Apps → Installed Apps → ⋯ → Uninstall. PowerShell: `Get-AppxPackage -Name "Microsoft.Copilot" | Remove-AppxPackage`.
- **Default:** Installed. *"The Microsoft Copilot app is automatically enabled after you install the Windows updates listed above if you haven't previously enabled a group policy to prevent the installation of Copilot."*
- **Exposes:** The consumer Copilot app on a work device. Note it *"doesn't support Microsoft Entra authentication and users trying to sign in… will be redirected"* — **so on a managed PC the consumer app is only useful with a personal account, which is exactly the EDP bypass.**
- **Recommend:** **Uninstall it on managed devices and block reinstall with AppLocker.** A consumer Copilot app on a work machine is a boundary hole with a shortcut key attached.
- **Risk:** High
- **Confidence:** `verified`

- **Setting:** `Ask Copilot` *(taskbar item)*
- **Where:** Settings → Personalization → Taskbar → Taskbar items → Ask Copilot. Taskbar page: `ms-settings:taskbar`.
- **Default:** `unresolved` — Microsoft's announcement calls the experience *"opt-in"* and says it *"does not grant Copilot access to your content"*, but **no Microsoft support page documents the toggle itself or its shipped state**; the click path comes from third-party guides.
- **Exposes:** One-click entry to Copilot Vision and Voice from the taskbar. **Hiding the button does not disable Copilot — Win+C still launches it.**
- **Recommend:** Toggle off to remove the mis-click surface, then remap the key or uninstall the app if you want it actually gone.
- **Risk:** Medium
- **Confidence:** `verified` for the toggle's existence and location (a Microsoft accessibility page documents it); **`unresolved` for its shipped state**, which Microsoft still does not publish. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.

- **Setting:** `Text and image generation` *(app permission)*
- **Where:** Settings → Privacy & security → Text and image generation. No documented `ms-settings:` URI.
- **Default:** `unresolved` — no Microsoft page documenting this page's default or exact toggle labels was found.
- **Exposes:** Which installed apps may invoke Windows' local generative models on your behalf. **Worth knowing: the viral claim that this setting "secretly runs AI and slows your PC" was tested and debunked** — it is a visibility and permission page, not a background workload.
- **Recommend:** Open it and audit the recent-activity list; deny any app you did not expect. **Do not disable it on performance grounds — that rationale is false.**
- **Risk:** Medium
- **Confidence:** `reported` for the page itself, which remains third-party-only. **The *absence* is a verified negative:** the page is missing from all three of Microsoft's canonical enumerations, including the current `ms-settings:` URI reference. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.

- **Setting:** Windows app permission pages underlying every AI feature
- **Where:** Documented deep links: `ms-settings:privacy-microphone`, `privacy-webcam`, `privacy-documents`, `privacy-pictures`, `privacy-downloadsfolder`, `privacy-broadfilesystemaccess`, **`privacy-graphicscaptureprogrammatic`**, **`privacy-graphicscapturewithoutborder`**, `search-permissions`
- **Default:** `unresolved` per page.
- **Exposes:** The OS-level gates under everything above — notably **the two Graphics capture pages (programmatic screen-capture permission)** and **broad file system access**, both directly relevant to agentic file and screen access.
- **Recommend:** Audit Documents / Pictures / Downloads / broad file system and **both Graphics capture pages** after enabling anything agentic. **OS permissions outrank in-app toggles, and they are where you can actually see which apps asked.**
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified` (URIs) / `unresolved` (defaults)

### (d) GitHub Copilot

- **Setting:** *(GitHub Mobile Copilot permissions)*
- **Default:** `unresolved` — no GitHub documentation of a distinct permission or privacy surface for Copilot in GitHub Mobile beyond the account-level settings. Content exclusion **is** documented as supported on GitHub Mobile for chat.
- **Recommend:** Manage GitHub Copilot privacy at https://github.com/settings/copilot — it governs mobile too. Verify on-device if you need a permission inventory.
- **Risk:** Low
- **Confidence:** `unresolved`

## The ten defaults most likely to surprise you

1. **GitHub Copilot now trains on individual-plan code by default** — "Allow GitHub to use my data for AI model training" has been **opt-in by default since 2026-04-24** for Free, Pro, Pro+ and Max, covering *"inputs, outputs, code snippets, and associated context."* Business and Enterprise are exempt.
2. **GitHub's "Default policy for new features" turns on unconfigured features on 2026-10-22** — twenty days after this check — and **the policy enabling that behaviour is itself enabled by default.** MCP server support and Copilot code review are named in scope.
3. **Teams meeting Copilot defaults to `EnabledWithTranscript`, and organizers cannot override it** — transcripts are saved, enforced, out of the box.
4. **Copilot memory (Enhanced personalization) is on by default**, has **no admin-center UI** (Graph only), generates **no Purview audit records**, and is **immune to your retention policies.**
5. **Vision — screen and mobile camera sharing — is on by default in the tenant**, bypassing every file-level permission you configured, because it captures rendered pixels.
6. **`User access` defaults to All users** — verbatim: *"**All users** - This option is the default."* Out of the box every licensed user can reach agents and plugins, including external-publisher agents and MCP servers. ⚠️ **Correction to an earlier reading of this file:** "All users" is the default of **`User access`**, *not* of the adjacent **`Agent and plugin access`** setting — they are two different controls on the same Agents → Settings page, and the latter (three per-publisher allow switches) has **no documented default at all**. Do not cite one as the other.
7. **Web search is on by default and it leaves the DPA, HIPAA and the EU Data Boundary.** The green shield in the UI does not communicate this.
8. **Copilot Studio computer use defaults to maker sign-in details and an unrestricted allow-list** — *"anyone using it can act with the original author's access"* on *"any website or application."*
9. **GitHub Copilot cloud agent is enabled in all repositories by default**, and its sessions are **shared by default** to anyone with repo access.
10. **The Azure OpenAI abuse-monitoring opt-out is not available to self-serve customers** — only *"customers and partners managed by a Microsoft account team or under an eligible program."*

## Volatile

### Changed in the last 12 months

- **Consumer Copilot forked on 2026-08-18.** Microsoft shipped a new app and published a **second, parallel set of support pages** rather than editing the first. The old set documents **Privacy → Training on conversation activity / Training on voice conversations** with training **on by default**; the new set has **no training toggle at all** and states *"Prompts, responses, and your file contents when using the Microsoft Copilot app aren't used to train foundation models."* **Both are live and both are correct for their version.** Any guidance that doesn't name a version is now ambiguous.
- **"Commercial data protection" was superseded by "enterprise data protection."** EDP is *"an improvement on top of the previous commercial data protection (CDP) promise."* **Documents still saying CDP are describing a retired term.**
- **Product rename in flight:** Microsoft 365 Copilot → **Microsoft Copilot**; M365 Copilot Chat → **Microsoft Copilot Chat**; app URL `m365.cloud.microsoft` → **`copilot.cloud.microsoft`**. Doc labels and shipping UI labels are out of sync — **and network allow-lists need updating.**
- **GitHub: individual-plan training flipped on 2026-04-24.** GitHub's general privacy statement is effective 2026-04-27 and contains **no Copilot-specific retention disclosure at all.**
- **GitHub: the 2026-10-22 default-enablement date is imminent** — the single most actionable item in this file.
- **Anthropic became a Microsoft subprocessor**, on by default in commercial cloud excluding EU/EFTA/UK, and **excluded from the EU Data Boundary.** A separate **"Anthropic models with Data Retention"** opt-in **exits the Microsoft DPA entirely.** Audit records now carry `ModelProvider` / `ModelName`.
- **Purview retention location split:** Copilot moved out of *"Teams chats and Copilot interactions"* into *"Microsoft Copilot experiences."* **Legacy policies may no longer cover Copilot — verify yours.**
- **Restricted SharePoint Search is retiring** — new enablement blocked from 2026-07-31. Migrate to Restricted Content Discovery.
- **Pin Copilot Chat was decoupled from the Copilot app** — EEA/Switzerland 2025-07-25, rest of world 2026-01-28. Any policy resting on pinning is weaker than when it was written.
- **`TurnOffWindowsCopilot` is formally deprecated**; Microsoft now routes admins to AppLocker. Any runbook citing it is stale.
- **Recall shipped to retail** but `manage-recall` still labels it **"Recall (preview)"**. **Recall DLP integration is new**, with Purview as the only provider plus a public provider API. **EEA snapshot export** is new, with a decryption API for third parties.
- **Azure OpenAI docs were restructured** and the **abuse-monitoring retention period was removed from the documentation.** The commonly-cited "30 days" is **no longer stated anywhere** — treat it as unverified.
- **Copilot personalization and memory are explicitly labelled preview:** *"in preview and subject to change."*

### Likely to move next

- **Phi Silica is being retired.** *"Phi Silica is being replaced by Aion Instruct… begins rolling out to Windows Insider Preview devices in November 2026 and to retail devices in January 2027, at which point Phi Silica will be removed."* **Every on-device text feature sits on this model**, so its privacy and moderation characteristics will change.
- **Windows AI APIs are leaving Copilot+ exclusivity** — Phi Silica now runs on NVIDIA RTX 30+ and AMD RX 9060+ GPUs; Speech Recognition and Video Super Resolution run on CPU. **"My PC can't do that, it has no NPU" is becoming false.**
- **Federated Copilot connectors become writable:** *"Write actions will be available starting early October 2026"* — **days away.** They flip from read-only to mutating external systems.
- **Agentic Windows is entirely Insider-preview and churning:** `AgentConnectorAccessPolicy`, `ConfigureAgentConnectors`, `AgentConsentDuration`, `DisableRecallDataProviders`, `DisableSettingsAgent`, `AllowRecallExport`, `OnDeviceRegistryLoggingLevel` and `DisableClickToDo` are all *"subject to change"*, and several still show a raw unrendered GP path — **the ADMX friendly names are not final.**
- **Windows Semantic Search is in private preview with no published user controls** — the most likely next Recall-scale privacy story.
- **Microsoft Agent 365** is positioned as the emerging *"control plane for AI agents… regardless of where these agents are built or acquired"*; agent governance will likely migrate there.
- **Purview DSPM is mid-reorganization** — now split into *Data Security Posture Management* and *DSPM for AI (**classic**)*.
- **Security Copilot is slated for inclusion in Microsoft 365 E5** — *"In the coming months"* — which widens the AI governance surface for E5 tenants automatically.
- **Microsoft still publishes no `ms-settings:` deep links** for Recall & snapshots, Click to Do, AI components, Agent tools, or Text and image generation.

### Two live contradictions in Microsoft's own documentation

1. **Recall's unconfigured retention default.** The WindowsAI CSP page says `SetMaximumStorageDurationForRecallSnapshots` has **Default Value 90** and *"When this policy isn't configured, the maximum storage duration is 90 days."* `manage-recall` and the consumer storage page say the opposite: snapshots *"aren't deleted until the maximum storage allocation is reached."* **Set it explicitly to 30 days rather than inheriting either.**
2. **`AllowRecallEnablement`'s unconfigured default.** The CSP table lists **Default Value `1`** ("Recall is available"); the prose on the same page says *"If this policy isn't configured, end users will have the Recall component in a disabled state."* **Set it explicitly to `0`.**

3. **`-AllowTranscription`'s documented default.** The Teams admin article says Transcription *"is **On** by default for new policies."* The `Set-CsTeamsMeetingPolicy` cmdlet reference for the same parameter lists **`Default value: None`** and states no policy default. (The cmdlet page's value is PlatyPS boilerplate for "no value implied if omitted," but as written the two Microsoft pages do not agree.) **Reported, not adjudicated** — assume transcripts are being produced unless you set the Global meeting policy to `$false`, and note `-TranscriptionForWebinar` and `-TranscriptionForTownhall` default *Enabled* separately.

Also worth flagging: `manage-recall` prints the **wrong friendly name** for the storage-duration policy in its Computer Configuration row; the CSP page has the correct one.

### Research-method caveat carried forward

The research pass **exhausted its 200-call WebSearch budget early**, so the back half was done by direct fetch against known and inferred documentation URLs. Every 404 and redirect is disclosed inline. The GitHub Copilot findings were verified first-hand from docs.github.com, with gaps — per-policy default table, retention periods, individual-account "Suggestions matching public code" default — **honestly marked `unresolved` rather than filled in.**

---

