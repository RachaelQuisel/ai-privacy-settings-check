# Microsoft Copilot

> **Last verified:** 2026-10-02 · **second gap-fill pass same day** — see *Second pass* at the end of this file for what closed, what did not, and one correction to the ten-defaults list
> **Four surfaces, kept separate throughout — do not blur them:** **(a) consumer Copilot** (copilot.com / Copilot app, personal Microsoft account) · **(b) Microsoft Copilot (work/school tenant)** — renamed from *Microsoft 365 Copilot* · **(c) Copilot in Windows incl. Recall** · **(d) GitHub Copilot**
>
> **Research-method caveat:** the research pass exhausted its 200-call search budget early, so the back half was done by direct fetch against known and inferred documentation URLs. Every 404 and redirect is disclosed inline. GitHub Copilot findings were verified first-hand from docs.github.com, with the remaining gaps marked `unresolved` rather than filled in.

**Verified 2026-10-02.** Four surfaces kept separate throughout: **(a) consumer Copilot** (copilot.com / Copilot app, personal Microsoft account), **(b) Microsoft Copilot (work/school tenant)** — renamed from *Microsoft 365 Copilot*, **(c) Copilot in Windows incl. Recall**, **(d) GitHub Copilot**.

---

## Framing notes — read before anything below

**The consumer Copilot fork of 2026-08-18.** Microsoft shipped an updated consumer Copilot app on 18 August 2026 and, rather than editing its support pages, **published a second parallel set and left the first in place**. The older set carries the verbatim banner: *"An updated version of the Microsoft Copilot app for web, desktop, and mobile devices is available as of August 18, 2026. **The information in this article applies only to the older version** of the Microsoft Copilot app."* The two sets answer the model-training question **differently, and both are currently correct for their respective versions**: the older app has a **Privacy → Training on conversation activity** toggle that is **on by default**; the newer app's privacy-controls page has **no model-training toggle at all** and states that prompts are not used to train foundation models. Any guidance that does not name a version is ambiguous. Both are documented in full in §1(a).
(https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls ; https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02)

The two parallel page sets, concretely:

| Older app (pre-2026-08-18) | Newer app (2026-08-18+) |
| --- | --- |
| `support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls` | `support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls` |
| `support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot` | `support.microsoft.com/en-us/privacy/microsoft-copilot/activity-history` |
| | `support.microsoft.com/en-us/privacy/microsoft-copilot/overview` |
| | `support.microsoft.com/en-us/privacy/microsoft-copilot/young-people` |
| Has **Privacy → Training on conversation activity** and **Training on voice conversations** | Has **no** training toggle; headings are Memory, Shared experiences, Chat history, Web search, Personalized advertising, Import browser data from Microsoft Edge |
| *"Microsoft uses data from Bing, MSN, Copilot... for AI training"* | *"Prompts, responses, and your file contents when using the Microsoft Copilot app aren't used to train foundation models."* |

**The boundary was renamed.** "Commercial data protection" (CDP) is the **old** name. Microsoft now says **"enterprise data protection" (EDP)**, described verbatim as *"an improvement on top of the previous commercial data protection (CDP) promise."* Anything still citing CDP describes a superseded term. Full treatment in §1(b).

**Product rename in flight.** Every current doc carries: *"Microsoft 365 Copilot is now named **Microsoft Copilot**, and Microsoft 365 Copilot Chat is now named **Microsoft Copilot Chat**."* The app URL moved from `m365.cloud.microsoft` to **`copilot.cloud.microsoft`**.

**URL notes.** `privacy.microsoft.com/en-us/privacystatement` **301-redirects** to `www.microsoft.com/en-us/privacy/privacystatement`. `learn.microsoft.com/en-us/copilot/microsoft-365/microsoft-365-copilot-privacy` resolves to canonical `/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy`. `learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy` now has canonical `/en-us/azure/foundry/responsible-ai/openai/data-privacy` ("Models sold by Azure"). **404s this session:** `support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-faq`; `support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-mobile-app`; both guessed Edge "Copilot Mode" support URLs; `learn.microsoft.com/en-us/windows/client-management/manage-agent-workspace`; `docs.github.com/en/copilot/concepts/privacy`; `docs.github.com/en/copilot/how-tos/manage-your-account/manage-copilot-policies-as-an-individual-subscriber`; `docs.github.com/en/site-policy/github-terms/github-copilot-product-specific-terms`.

**Two live contradictions in Microsoft's own Recall documentation are flagged, not resolved** — see §5(c) (unconfigured retention default) and the `AllowRecallEnablement` entry referenced from §7(c).

---

## 1. Training on your data

### (a) Consumer Copilot

- **Setting:** Training on conversation activity
- **Where:** copilot.com: profile icon → profile name → **Privacy** → **Training on conversation activity**. Windows/macOS app: profile icon → **Settings** → **Privacy**. Mobile: menu → profile icon → **Account** → **Privacy**. No deep-link URL published.
- **Default:** **On** (training occurs unless you opt out) — **on the pre-2026-08-18 app only.** The FAQ states: *"Except for certain categories of users or users who have opted out, Microsoft uses data from Bing, MSN, Copilot, and interactions with ads on Microsoft for AI training."* Excluded categories: Entra ID work/school accounts, Microsoft 365 consumer app users (Word/Excel/PowerPoint/Outlook), unauthenticated users, under-18s, and users in Brazil, China (excl. Hong Kong), Israel, Nigeria, South Korea, Vietnam. **No EEA/UK carve-out is listed.**
- **Exposes:** Your typed Copilot conversations are used to train Microsoft's generative AI models, and are retained 18 months by default.
- **Recommend:** Opt out explicitly on **every** client — and understand the limit: opting out *"will not exclude your conversations from being used for other general product or system improvements nor from use for advertising, digital safety, security, and compliance purposes."*
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot ; https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Training on voice conversations
- **Where:** Same path, under **Privacy** (older app only)
- **Default:** `unresolved` — Microsoft's page documents the toggle and its opt-out effect but never states on/off. Third parties claim it is **off** by default; I could not confirm this in Microsoft documentation.
- **Exposes:** Voice interactions used for model training. Separately verified: *"No user or Copilot audio is stored"*, but *"Text transcripts produced from your Copilot Voice conversations are handled in the same way as conversation history."*
- **Recommend:** Set to off explicitly rather than assuming.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls ; https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-voice-with-microsoft-copilot — checked 2026-10-02
- **Confidence:** `unresolved` (default) / `verified` (control, path, scope)

- **Setting:** *(no setting — the new app's stated position)*
- **Where:** n/a — applies to the app version released 2026-08-18 and later
- **Default:** No training. Verbatim: *"Prompts, responses, and your file contents when using the Microsoft Copilot app aren't used to train foundation models."* And on feedback: Microsoft *"does not use this feedback to train the foundation models used by Copilot."* I confirmed the new app's privacy-controls page lists **no model-training toggle at all** — its only headings are Memory, Shared experiences, Chat history, Web search, Personalized advertising, Import browser data from Microsoft Edge.
- **Exposes:** Nothing for training; conversations are still retained and still used for safety, abuse prevention and (separately) advertising.
- **Recommend:** Confirm which app version you are on. If the Privacy section with training toggles is absent, you are on the new app and training is off by policy, not by toggle.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/activity-history ; https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(human review — no opt-out exists)*
- **Where:** n/a
- **Default:** On, and not optional. Verbatim: *"Some Copilot conversations are subject to both automated and human review for product improvement and digital safety purposes"* and *"Limited human review is required as part of the investigation process when a violation of the Code of Conduct is suspected. To ensure that our services are safe and secure for everyone, an opt-out of human review is not available."*
- **Exposes:** A sample of your conversations can be read by people at Microsoft regardless of every other setting on this page.
- **Recommend:** Treat consumer Copilot as a non-confidential channel. There is no configuration that changes this.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(Copilot Vision / image content — stated exclusion)*
- **Where:** n/a
- **Default:** Excluded from training. Verbatim: *"User inputs, images, audio, and shared page content aren't used to train models or personalize your experience."*
- **Exposes:** Nothing for training. Images are deleted *"within 30 days after the conversation ends"*; Vision session data retained *"up to 47 hours"*.
- **Recommend:** No action — but note the asymmetry: Vision content is training-exempt while ordinary chat on the older app is not.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-vision-with-microsoft-copilot ; https://support.microsoft.com/en-us/microsoft-copilot/transparency-note-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(Copilot in Microsoft 365 consumer apps — stated exclusion)*
- **Where:** n/a
- **Default:** No training. Verbatim: *"Prompts, responses, and your file contents when using Copilot in Microsoft 365 apps aren't used to train foundation models."*
- **Exposes:** Nothing for training.
- **Recommend:** Prefer Copilot inside Word/Excel/Outlook over the standalone consumer chat app if you're on the older app version and care about training.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/privacy/copilot-in-microsoft-365-apps-for-home-your-data-and-privacy — checked 2026-10-02
- **Confidence:** `verified`

### (b) Microsoft Copilot (work/school tenant) — the enterprise data protection boundary, precisely

**What EDP is.** *"Enterprise data protection (EDP) refers to controls and commitments, under the Data Protection Addendum (DPA) and Product Terms, that apply to customer data for users of Microsoft Copilot and Microsoft Copilot Chat"* — with the footnote *"The specific controls will vary depending on a customer's Microsoft subscription plans."* **It is a contractual construct, not a network perimeter.** Microsoft acts as **data processor**.

**What it covers.** Prompts and responses: *"The user's prompts and Copilot's responses are stored within Microsoft 365 and never leave the service boundary for both Microsoft Copilot and Microsoft Copilot Chat without customer direction."* Plus encryption at rest and in transit, tenant isolation, GDPR, EU Data Boundary, ISO/IEC 27018, your sensitivity labels, your retention policies, audit, and the Customer Copyright Commitment. On training: *"Prompts, responses, and data accessed through Microsoft Graph aren't used to train foundation LLMs, including those used by Microsoft Copilot."* Microsoft Copilot has also **opted out of Azure OpenAI abuse monitoring**: *"While abuse monitoring, which includes human review of content, is available in Azure OpenAI, Microsoft Copilot services have opted out of it."*

**The four documented exits from the boundary — this is the widely-misread part:**

1. **Web/Bing grounding leaves it.** *"The Bing search service operates separately from Microsoft 365 and has different data-handling practices... Microsoft acts as an **independent data controller**."* And explicitly: *"The Microsoft Products and Services Data Protection Addendum (DPA) **doesn't apply** to the use of generated web search queries in Microsoft Copilot, Microsoft Copilot Chat, or the Bing search service. Also, **HIPAA compliance and the EU Data Boundary don't apply** to generated search queries."* Mitigations that *do* hold: the query is a few words (not the full prompt), user and tenant identifiers are stripped, and Product Terms commit that queries *"aren't used to improve Bing"*, *"aren't used to train generative AI foundation models"*, *"aren't shared with advertisers"*, and *"aren't used to create advertising profiles or to track user behavior."* But the query **can be informed by the content of a referenced Microsoft 365 document** — specifically *"When a user enters a prompt into Copilot inside a Microsoft 365 application"* or *"When the user explicitly references a specific document in their prompt."*
2. **Third-party agents, connectors and plugins leave it.** *"Data processed by non-Microsoft services isn't subject to Microsoft agreements."* And *"When you're using agents in Microsoft Copilot, check the privacy statement and terms of use of the agents to determine how they'll handle your organization's data."*
3. **"Anthropic models with Data Retention" leave it.** *"data is stored by Anthropic and **not subject to your Microsoft Customer Agreement** including commitments in the Product Terms and DPA... Anthropic acts as an independent processor."*
4. **Consumer-account sign-in bypasses it.** EDP applies *"when users sign in with a Microsoft Entra account."* The same client accepts personal Microsoft accounts; the only hard control is **Tenant Restrictions v2**.

**Also note:** ordinary Anthropic models (as a Microsoft subprocessor, inside the DPA) are *"currently excluded from the EU Data Boundary, and when applicable, in-country processing commitments."*

**What EDP does *not* mean.** It does not mean nothing leaves Microsoft 365 — web queries do, by default. It does not mean no human ever reads your content — Purview-authorised admins, eDiscovery, and Copilot diagnostics-log submissions all reach it. It does not extend to anything an agent or connector hands to a third party. And it is not a function of the app you are in: it is a function of **which account you signed in with**.

*(Evidence for this whole subsection: https://learn.microsoft.com/en-us/microsoft-365/copilot/enterprise-data-protection ; https://learn.microsoft.com/en-us/microsoft-365/copilot/manage-public-web-access ; https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy ; https://learn.microsoft.com/en-us/microsoft-365/copilot/connect-to-ai-subprocessor ; https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — all checked 2026-10-02; `verified`)*

**Copilot Chat (free/PAYG) vs licensed Copilot.** Both get EDP — the difference is grounding, not protection. Copilot Chat is grounded in web data and is not grounded in organizational content as part of the chat experience; the licensed product adds Microsoft Graph grounding. Chat can still reach org data via pasted or uploaded content, open-file context in app agents, Copilot Chat in Outlook, PAYG agents, and Edge page context (see `EdgeEntraCopilotPageContext` in §8c). `verified`

- **Setting:** Allow web search in Copilot
- **Where:** Cloud Policy service for Microsoft 365 — https://config.office.com/ → **Customization** → **Policy Management**. Values: *Enabled in Microsoft Copilot and Microsoft Copilot Chat* / *Disabled in Microsoft Copilot and Microsoft Copilot Chat* / *Disabled in Microsoft Copilot Work mode; Enabled in Microsoft Copilot Web mode and Microsoft Copilot Chat*.
- **Default:** **On when unconfigured.** *"If the IT admin doesn't configure the Allow web search in Copilot policy, web search will be available to users in both Microsoft Copilot and Microsoft Copilot Chat, unless the IT admin has set the Allow the use of additional optional connected experiences in Office policy to Disabled."* GCC/DoD exception: *"Web search is available, but is turned off by default."*
- **Exposes:** Copilot-generated queries — potentially shaped by the content of a tenant document — go to Bing outside the DPA, outside HIPAA, outside the EU Data Boundary.
- **Recommend:** At minimum *Disabled in Work mode*; fully disabled for regulated workloads. Work mode is where prompts are grounded in tenant files, so that is where query leakage carries real content. Note the side effect: choosing *Disabled in Work mode* also disables web search in **Researcher** and **Cowork**.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/manage-public-web-access — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Web search *(user-side; also rendered as the **Web content** toggle)*
- **Where:** Microsoft Copilot app → **Settings** → **Personalization** → expand **Advanced** → **Web search**. Researcher also exposes a **Web search** toggle in its input box; Analyst and Cowork do not.
- **Default:** **On.** *"If the IT admin enables web search, the Web content toggle is turned on by default."* Dimmed and off if the admin disables web search.
- **Exposes:** Same Bing egress path, at user discretion; preference persists across sessions and devices.
- **Recommend:** Off for anyone handling regulated material — but treat as advisory, since any user can flip it back.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/manage-public-web-access — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** AI providers operating as Microsoft subprocessors
- **Where:** Microsoft 365 admin center → **Copilot** → **Settings** → **View all** → **AI providers operating as Microsoft subprocessors** → select **Anthropic** → *"Choose who can access Anthropic models for Copilot and generative AI experiences."* To disable: **Copilot** → **Settings** → **User access** page → same setting → **Disable Anthropic as a Microsoft subprocessor**. Requires **AI Administrator** or Global Administrator.
- **Default:** Region-split. *"Microsoft enables Anthropic models on by default for most customers in commercial cloud (excluding EU/EFTA and UK)."* / *"Customers within the EU Data Boundary and customers in the UK have Anthropic models disabled by default"* — *"the default is set to **No users**."* Unavailable in GCC federal, GCC High, DoD and other sovereign clouds.
- **Exposes:** Prompts and responses route to Anthropic as a Microsoft subprocessor under the DPA and Product Terms — but **outside the EU Data Boundary** and outside in-country processing commitments.
- **Recommend:** Leave off if you carry EU/UK residency obligations; if on, scope it to a named security group so residency-sensitive teams are excluded. If you previously opted in under Anthropic's separate terms in EU/EFTA/UK, *"you need to opt in again. The toggle is set to **Off** by default."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/connect-to-ai-subprocessor — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Anthropic models with Data Retention
- **Where:** Same admin page; requires explicitly accepting Anthropic's Commercial Terms of Service and Data Protection Addendum, then selecting all or specific users/groups.
- **Default:** **Off everywhere.** *"off by default for all scenarios, including in regions when different Anthropic models are on by default... No users will have access to these models until the tenant admin explicitly opts in to enable use of Anthropic models with Data Retention."*
- **Exposes:** Prompts and responses stored **by Anthropic**, outside your Microsoft agreement — *"Anthropic (not Microsoft) stores most inputs and outputs for up to 30 days before deleting them."* Policy-flagged content may be retained *"for up to two years"* and trust-and-safety classification scores *"for up to seven years."* *"Anthropic doesn't use retained data for model training without your express permission."*
- **Recommend:** Leave off. This is the clearest single-toggle exit from EDP that exists. Note the contrast: certain **Fable-class** models are available *with* Anthropic as subprocessor under the DPA where *"Anthropic doesn't retain customer content (including prompts and responses)"* — eligibility is account-team dependent.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/connect-to-ai-subprocessor — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Turn on optional connected experiences *(admin policy: **Allow the use of additional optional connected experiences in Office**)*
- **Where:** User: **File → Account → Account Privacy → Manage Settings**. Mac: app menu (Word/Excel) → **Preferences → Privacy**. Admin: Cloud Policy / Group Policy / Mac-iOS-Android preferences.
- **Default:** **Available (on).** *"If you don't configure this policy setting, these optional connected experiences are available to your users."*
- **Exposes:** Bing-backed and third-party-backed Office features licensed to the **user**, not your tenant: *"these optional cloud-backed services aren't covered by your organization's license with Microsoft. Instead, they're licensed directly to you."* Includes Copilot **Scheduled prompts**, which *"relies on Microsoft Power Automate."*
- **Recommend:** Don't use this as a Copilot web-search control — disabling it *"restricts Microsoft Copilot Chat, Microsoft Copilot, and multiple experiences across Microsoft 365."* Use `Allow web search in Copilot` instead. Note the explicit decoupling: *"The privacy setting for optional connected experiences available to users in Microsoft 365 apps... has no effect on the availability of web search."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365-apps/privacy/optional-connected-experiences ; https://learn.microsoft.com/en-us/microsoft-365-apps/privacy/overview-privacy-controls ; https://learn.microsoft.com/en-us/microsoft-365/copilot/manage-public-web-access — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Experiences that analyze your content
- **Where:** Same Account Privacy dialog; admin via Cloud Policy / Group Policy
- **Default:** **Available (on).** *"If you don't configure these policy settings, all these connected experiences will be available to your users."*
- **Exposes:** At default, content analysis is permitted in Office apps. Turning it off removes Copilot entirely from **Excel, OneNote, Outlook, PowerPoint, Word** on Windows, Mac, iOS and Android. Microsoft adds: *"Your personal data collected from the use of connected experiences in Microsoft 365 isn't used to train large language models (LLMs), including those used by Microsoft Copilot."*
- **Recommend:** Not a useful Copilot privacy lever — it's an all-or-nothing kill switch for five apps. Control Copilot via licensing and Copilot-specific settings.
- **Risk:** Low (as a privacy lever)
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy ; https://learn.microsoft.com/en-us/microsoft-365-apps/privacy/overview-privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Optional diagnostic data *(levels: **Required** / **Optional** / **Neither**)*
- **Where:** File → Account → Account Privacy → Manage Settings; admin via Cloud Policy policy setting
- **Default:** **Optional.** *"Optional diagnostic data will be sent to Microsoft unless you change the setting."* Users signed in with a work or school account *"won't be able to change the diagnostic data level"* themselves.
- **Exposes:** Optional-level data *"may also be used in aggregate to train and improve experiences powered by machine learning, such as recommended actions, text predictions, and contextual help."*
- **Recommend:** Set to **Required** by policy. It is the one Office privacy control that is on by default *and* feeds machine-learning improvement. Note *"Even if you choose Neither, required service data will be sent from the user's device to Microsoft."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365-apps/privacy/overview-privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot diagnostics logs
- **Where:** M365 admin center → **Copilot** → **Settings** → **Other settings** → **Copilot diagnostics logs**
- **Default:** `unresolved`
- **Exposes:** When an admin submits logs on a user's behalf, the submission includes prompts, generated responses, relevant content samples and log files — and *"it temporarily overrides any user level feedback policy."*
- **Recommend:** Enable only for a live support case; it overrides the user's own feedback choice.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified` (behavior) / `unresolved` (default)

### (c) Copilot in Windows / Recall

- **Setting:** Send optional diagnostic data
- **Where:** Settings → Privacy & security → **Diagnostics & feedback** — `ms-settings:privacy-feedback`. Policy: Computer Configuration → Administrative Templates → Windows Components → Data Collection and Preview Builds → **Allow diagnostic data**; CSP `System/AllowTelemetry`.
- **Default:** **Required (Basic)** — *"This is the default setting for Windows 10, version 1903 and later."* Levels: Diagnostic data off (0, Enterprise/Education/Server only), Required (1), Enhanced (2, legacy), Optional/Full (3).
- **Exposes:** At **Optional**, Microsoft receives *"App activity, such as which programs are launched on a device"*, browsing history and search terms from Microsoft browsers, diagnostic logs, and full crash dumps that *"may unintentionally contain personal data, such as portions of memory from a document and a web page."* Recall and Click to Do both emit diagnostic data per this setting.
- **Recommend:** Keep at **Required**, never Optional. On Enterprise/Education, consider **Diagnostic data off** plus *Limit dump collection* and *Limit diagnostic log collection*.
- **Risk:** High at Optional, Medium at Required
- **Evidence:** https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Tailored experiences
- **Where:** Settings → Privacy & security → Diagnostics & feedback
- **Default:** `unresolved`
- **Exposes:** Microsoft uses your diagnostic data *"to provide more relevant tips and recommendations"* — profiling off telemetry. *"Crash data is never used for Tailored experiences."*
- **Recommend:** Off.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/privacy/configure-windows-diagnostic-data-in-your-organization — checked 2026-10-02
- **Confidence:** `verified` (exists, behavior) / `unresolved` (default)

- **Setting:** Recall feedback (the **…** → Feedback icon inside Recall)
- **Where:** In Recall: **…** → Feedback
- **Default:** N/A (user action)
- **Exposes:** The single documented path by which Recall content reaches Microsoft: *"Filing feedback will send data from Recall to Microsoft, including any screenshots that a user attaches to the feedback."*
- **Recommend:** Never attach a snapshot to feedback. One click defeats the entire local-only architecture.
- **Risk:** High (if used)
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Recall snapshot processing location *(no toggle — stated architecture)*
- **Where:** n/a
- **Default:** Entirely local. *"No internet or cloud connections are required or used to save and analyze snapshots. Snapshots aren't sent to Microsoft. Recall AI processing occurs locally, and snapshots are securely stored on the local device only... Microsoft can't access or view the snapshots."*
- **Exposes:** Nothing to Microsoft at default. Minor exception: *"Occasionally, Recall will get artifacts from the internet from the snapshot URL top-level domain"* (favicons, site metadata).
- **Recommend:** No action; this is the one genuinely reassuring claim in the Recall stack. The risk is local compromise, not cloud egress.
- **Risk:** Low
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

### (d) GitHub Copilot

- **Setting:** Allow GitHub to use my data for AI model training
- **Where:** https://github.com/settings/copilot — select the dropdown and choose **Disabled** to opt out
- **Default:** **Enabled.** Opt-in by default **starting 2026-04-24**, for **Copilot Free, Copilot Pro, Copilot Pro+, and Copilot Max**. Data covered: *"inputs, outputs, code snippets, and associated context."* Business/Enterprise are excluded: *"GitHub does not use Copilot Business or Copilot Enterprise customer data to train AI models."*
- **Exposes:** Your prompts, Copilot's outputs, and **snippets of your code plus surrounding context** are used to train GitHub's AI models — on every individual plan including the paid ones.
- **Recommend:** Set to **Disabled** immediately on every personal account. This is the highest-impact default change on any Copilot surface in the last 12 months, and it reversed the previous posture for paid individual plans.
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Suggestions matching public code
- **Where:** Individual: https://github.com/settings/copilot (dropdown: **Allow** / **Block**). Enterprise/org: the **Privacy** section of the Copilot policy page.
- **Default:** **Allowed** for Copilot Business users (*"set to Allowed by default for Copilot Business users"*). The default for individual (Free/Pro/Pro+/Max) accounts is **`unresolved`** — neither the policy page nor the code-referencing concept page states it.
- **Exposes:** With "Allow", Copilot may emit suggestions that match public code verbatim, with the licence implications that carries; with "Block", GitHub checks suggestions *"against public code on GitHub"* and filters matches.
- **Recommend:** **Block** — the IP-contamination risk of an unattributed verbatim match outweighs the lost suggestions. Note code referencing (seeing *which* repo matched) only works when matching is **allowed**, so Block and referencing are mutually exclusive. Applies to accepted inline suggestions in JetBrains/VS Code/Visual Studio and to Copilot Chat responses on all platforms.
- **Risk:** Medium
- **Evidence:** https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-enterprise-policies ; https://docs.github.com/en/copilot/concepts/completions/code-referencing — checked 2026-10-02
- **Confidence:** `verified` (Business default) / `unresolved` (individual default)

- **Setting:** *(retention periods for prompts and suggestions)*
- **Where:** n/a
- **Default:** **`unresolved`.** I could not find any current GitHub documentation stating a retention period for Copilot prompts or suggestions for Individual vs Business/Enterprise. The GitHub general privacy statement (effective **2026-04-27**) mentions Copilot exactly once, only as *"the features you use (such as pull requests, Codespaces, or GitHub Copilot)"*, with no Copilot-specific retention disclosure. `docs.github.com/en/copilot/concepts/privacy` and `docs.github.com/en/site-policy/github-terms/github-copilot-product-specific-terms` both **404**. Widely-cited figures (e.g. "28 days for Individual") could not be confirmed.
- **Exposes:** Unknown duration of prompt/suggestion retention.
- **Recommend:** Do not assert a GitHub Copilot retention period in policy documents. Ask GitHub directly, or rely on the Business/Enterprise DPA rather than a published number.
- **Risk:** Medium
- **Evidence:** https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement — checked 2026-10-02
- **Confidence:** `unresolved`

---

## 2. Memory, history & personalization

### (a) Consumer Copilot

- **Setting:** Saved memories
- **Where:** Copilot → **Settings** → **Personalization** → **Saved memories**. Manage/delete: **Manage** → **Delete all memories**, or the trash icon per memory. *(New app, 2026-08-18+)*
- **Default:** **Enabled (on).** *"Copilot can offer you tailored experiences by remembering key details and preferences from your conversations."*
- **Exposes:** Copilot builds a persistent profile of *"your name, interests, and goals"* and other details inferred from your chats, and applies it across future conversations.
- **Recommend:** Off if you use Copilot for client or confidential work — persistent memory means content from one engagement can surface in another. Turning it off does **not** delete existing memories; use **Delete all memories** as a separate step.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Personalization and memory *(older app)*
- **Where:** copilot.com / Windows / macOS: profile icon → profile name → **Memory** → **Personalization and memory**. Mobile: menu → profile icon → **Memory**. Edge sidebar: sidebar menu (…) → **Settings** → **Memory**.
- **Default:** **On where available.** *"If personalization is available to you, it will be on by default. Personalization is not currently available for users in Brazil, China (excluding Hong Kong), Israel, Nigeria, South Korea, and Vietnam."*
- **Exposes:** Memory plus cross-conversation personalization. *"If you turn off personalization and memory, Copilot will forget its memories of your conversations"* but *"You can still view your past conversations."* Important gotcha: *"The personalization setting in Copilot does not control whether you receive personalized ads."*
- **Recommend:** Off, and handle ads separately at the privacy dashboard.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls ; https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** One shared experience
- **Where:** Copilot → **Settings** → **Personalization** → **One shared experience** *(new app)*
- **Default:** **Enabled.** *"Your experiences with those products can be used to give you a more relevant and personalized experience"* — scope is **Bing, Edge, MSN and Copilot**.
- **Exposes:** A cross-product profile join: what you do in Bing, Edge and MSN shapes Copilot, and vice versa.
- **Recommend:** Off. This is the broadest cross-service data pull in the consumer Copilot settings surface and it buys you little.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Microsoft usage data *(older app — the predecessor of "One shared experience")*
- **Where:** profile icon → profile name → **Memory** → **Microsoft usage data**
- **Default:** Enabled (the page describes behavior *"if 'Microsoft usage data' is enabled"*; it does not state the out-of-box value explicitly).
- **Exposes:** *"Copilot uses data from Bing, MSN, Edge and other Microsoft product you've used to personalize your experience."*
- **Recommend:** Off.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls — checked 2026-10-02
- **Confidence:** `verified` (control, path) / `unresolved` (stated default)

- **Setting:** Allow ads personalization
- **Where:** Copilot → **Settings** → **Personalization** → **Allow ads personalization**. Also at https://account.microsoft.com/privacy/ad-settings/ (toggle **See ads that interest you**).
- **Default:** **Enabled for users 18+.** *"Personalized ads might use your chat history, saved memories, and other Microsoft data."* *"Copilot doesn't show personalized advertising to users under the age of 18"* regardless of settings.
- **Exposes:** Your Copilot chat history and saved memories feed ad targeting across Microsoft. Remember the training opt-out explicitly does **not** cover advertising use.
- **Recommend:** Off — and turn off **See ads that interest you** on the privacy dashboard too, because the two are separate controls.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls ; https://www.microsoft.com/en-us/privacy/privacy-support-requests — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Import browser data *(**Bring over your browsing data from Microsoft Edge**)*
- **Where:** Copilot → **Settings** → **Web browsing** → **Import browser data** → **Bring over your browsing data from Microsoft Edge**. **US-based Microsoft accounts only.**
- **Default:** `unresolved` — Microsoft documents the toggle and its scope but not its out-of-box state. Separately verified for Copilot on Windows: *"Every time you launch the Copilot app on Windows, it can import cookies stored in Microsoft Edge to make your experience more personalized and helpful."*
- **Exposes:** *"cookies, history, payment info, passwords, and autofill data"* imported into Copilot.
- **Recommend:** Verify this is off. The import list includes **passwords and payment info** — this is the single widest data scope of any consumer Copilot toggle.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls ; https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified` — default confirmed **OFF** in the second pass. **Closed in the second pass** — see *Second pass — gap-fill, 2026-10-02* at the end of this file.

- **Setting:** Browsing data sync / autofill in Copilot for Windows
- **Where:** Copilot app → **Profile** → **Settings** → **Browsing settings** → **Web data and security** → **Privacy**
- **Default:** `unresolved`
- **Exposes:** *"When you are signed in, Copilot provides an option to sync all your history, favorites, passwords and other browser data between Copilot apps and with Microsoft Edge."* And Copilot on Windows can store payment cards: *"When you check out on a shopping site, you can choose 'Save' to store your card for faster checkout next time."*
- **Recommend:** Do not sync passwords into Copilot, and do not save cards there. The Copilot app is now a browser with a credential store attached to an AI agent.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified` (behavior, path) / `unresolved` (defaults)

- **Setting:** Recent files shown in Copilot on Windows
- **Where:** In Copilot, right-click a recent file → **Hide**
- **Default:** Shown. *"Copilot shows files you've recently opened on your device by referencing Recent Items in Windows."*
- **Exposes:** Your recently-opened filenames are surfaced in the Copilot UI — shoulder-surfable, and a hint surface for file-grounded prompts.
- **Recommend:** Hide anything client-identifying; consider turning off Windows **Activity history** (`ms-settings:privacy-activityhistory`) as the upstream control.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Visibility of Microsoft 365 Copilot conversations within Copilot
- **Where:** Copilot settings (exact path not given on the page)
- **Default:** Visible. *"Yes. You can manage or turn off the visibility of Microsoft 365 Copilot conversations at any time in your Copilot settings."*
- **Exposes:** Conversations from Copilot in Microsoft 365 consumer apps appear inside the consumer Copilot chat list.
- **Recommend:** Turn off if you share a device, so work-adjacent conversations don't surface in the general chat history.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified` (control, default) / `unresolved` (exact click path)

### (b) Microsoft Copilot (tenant)

- **Setting:** Enhanced personalization
- **Where:** **No admin-center UI.** Microsoft Graph only — the `enhancedPersonalizationSetting` resource type. *"To configure the control programmatically via Microsoft Graph, a tenant administrator can write a script."*
- **Default:** **On.** *"By default, Enhanced personalization is turned on"* / *"No action is required to turn on Copilot memory; you only need to turn off Copilot memory for end-users or the tenant if desired."* Microsoft labels the whole feature as preview: *"Copilot personalization and memory are in preview and subject to change."*
- **Exposes:** A persistent per-user profile — saved memories, inferences from chat history, custom instructions — built from *"Copilot Chat conversations"*, *"emails, Team chats, and meeting transcripts"*, usage signals and profile information, stored in a hidden folder in the user's Exchange mailbox.
- **Recommend:** Turn off via Graph unless you have deliberately reviewed and accepted it. It is on by default, invisible in the admin portal, and — see the next item — outside your retention and audit regime.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/copilot-personalization-memory — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(Copilot memory governance — a documented absence, not a setting)*
- **Where:** n/a
- **Default:** *"Retention policies and retention labels configured in Purview by organization admins **don't apply** to Copilot memory... **There are no admin controls to enforce retention rules specifically for Copilot memory.**"* Memories persist *"until the end-user explicitly deletes the saved memory."* *"Memory and personalization actions **don't generate audit log entries** in Purview."* *"No, admins can't restrict what type of information is added to Copilot memory."*
- **Exposes:** An indefinitely-retained, un-audited, retention-exempt inferred profile of each employee derived from their work content.
- **Recommend:** This is the strongest argument for turning Enhanced personalization off tenant-wide. If you keep it, record the gap in your DPIA and records of processing — your retention schedule does not reach it. Memory *is* discoverable in eDiscovery (item class `IPM.Contact`, folder `CopilotMemory`), but *"Custom instructions aren't accessible"* to admins.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/copilot-personalization-memory — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Saved memories / Custom instructions / Chat history *(user controls)*
- **Where:** Copilot Chat → **… Settings and more** → **Chat settings** → **Personalization** → **Saved memories** tile → **Manage saved memories**. Also a **Chat history & work insights** toggle on work/school accounts.
- **Default:** **On.** *"Saving memories is **On** by default."* With Enhanced personalization off tenant-wide, users *"see the user-level controls for Custom instructions, Saved memories, and Chat history in Settings > Personalization as turned off. They can't turn on these settings."*
- **Exposes:** Toggling off **stops application but does not delete**: *"Copilot is stopped from applying saved memories to the chat, but doesn't remove saved memories."* Chat-history details are the exception — deleted after 30 days when disabled. Deleting a chat does not delete memories derived from it; deleting every chat where a fact appeared removes it from Chat History details *"within seven days."*
- **Recommend:** Tell users to use **Delete all memories**, not just the toggle. Also point them at **Start a new temporary chat**, which *"won't access or store any personalized information"* — though *"admins can access temporary chats in Purview just like they can with regular chats."*
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-365-copilot/manage-copilot-memory-in-microsoft-365-copilot ; https://learn.microsoft.com/en-us/microsoft-365/copilot/copilot-personalization-memory — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot Frontier
- **Where:** M365 admin center → **Copilot** → **Settings** → **View all** → **Copilot Frontier**. Options: *No access* / *All groups of users* / *Specific user groups*.
- **Default:** **No access.** *"No access: No users can access Frontier features. This option is the default."*
- **Exposes:** Nothing at default. If enabled, users get experimental features and agents whose governance posture is by definition unsettled.
- **Recommend:** Keep at **No access**, or scope to a small pilot group with its own data-handling rules.
- **Risk:** Medium (if enabled)
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Recommendations for Microsoft Copilot licensing
- **Where:** M365 admin center → **Copilot** → **Settings** → **Data access** → **Recommendations for Microsoft Copilot licensing**
- **Default:** **Enabled.** *"By default, this setting is enabled."*
- **Exposes:** *"Microsoft provides licensing recommendations based on Microsoft 365 apps activity"* — per-user activity profiling surfaced to administrators as candidate lists.
- **Recommend:** Disable where works-council or employee-monitoring constraints apply. It is individual-level activity analysis, on by default, presented to admins.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified`

### (c) Copilot in Windows / Recall

- **Setting:** Recall shows a customized experience using your snapshots
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Advanced settings**
- **Default:** **On.** Turning it off reduces the Recall home page to a bare search bar.
- **Exposes:** A curated "here's what you were doing" homepage generated from your snapshot index — content on screen without you searching for it.
- **Recommend:** Off if Recall is on. Pure exposure surface, no functional loss.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Recall additional activity details from App Actions providers *(policy: `DisableRecallDataProviders`)*
- **Where:** Policy only — `./User/Vendor/MSFT/Policy/Config/WindowsAI/DisableRecallDataProviders`; GP path `Windows Components > Windows AI`. Providers themselves listed at **Settings → Apps → Actions**. **Enterprise/Education only; Windows Insider Preview.**
- **Default:** **Enabled** (`0` = providers enabled). *"By default, additional activity details from available providers are displayed in Recall."*
- **Exposes:** Third-party and Microsoft App Actions providers inject app-held metadata into your Recall timeline — Microsoft's own example is *"meeting attendees for meeting Recall snapshots."* App data joins your screen archive.
- **Recommend:** Set to `1` on managed ENT/EDU devices. On consumer SKUs prune providers at Settings → Apps → Actions; no consumer-specific Recall toggle for this was verifiable.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified` (policy, default) / `unresolved` (consumer-side control)

- **Setting:** Activity history
- **Where:** Settings → Privacy & security → Activity history — `ms-settings:privacy-activityhistory`
- **Default:** `unresolved`
- **Exposes:** Local and synced record of app and document activity — the upstream source for Copilot's "recent files" list and adjacent to App Actions data that Recall ingests.
- **Recommend:** Off.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified` (URI exists) / `unresolved` (default)

- **Setting:** Inking & typing personalization
- **Where:** Settings → Privacy & security → Inking & typing personalization — `ms-settings:privacy-speechtyping`
- **Default:** `unresolved`
- **Exposes:** Builds a personal dictionary from what you type and ink.
- **Recommend:** Off.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified` (URI) / `unresolved` (default)

### (d) GitHub Copilot

- **Setting:** Store local sessions in the Cloud
- **Where:** Enterprise/organization Copilot policy pages (Business/Enterprise only). Options include **View from cloud**.
- **Default:** Effectively off. *"the applicable 'Store local sessions in the Cloud' policy must be set to at least 'View from cloud' for session data to be synced. If the policy is disabled or unconfigured, sessions are stored locally only."*
- **Exposes:** When enabled, local Copilot CLI / Copilot app session data (prompts, context, responses) syncs to GitHub.com. *"Synced session data is tied to your personal account and is accessible only to you by default."* Deletion: *"For Copilot CLI, deleting a local session that has been synced to your account prompts you to choose whether to also delete the synced copy. For the GitHub Copilot app, deleting a local session also deletes its synced copy immediately."* No retention period is published. Separately: *"When you query previous interactions or use `/chronicle`, Copilot may send relevant session data, such as prompts, context, and responses, to the AI model."*
- **Recommend:** Leave unconfigured unless you specifically need cross-device session continuity — it moves local prompt history into GitHub's cloud with no documented retention limit.
- **Risk:** Medium
- **Evidence:** https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/session-data — checked 2026-10-02
- **Confidence:** `verified` (behavior, default) / `unresolved` (retention)

---

## 3. Connectors & OAuth scopes

### (a) Consumer Copilot

- **Setting:** Connectors
- **Where:** Mobile: **Profile** → **Connectors** → **Connect** next to the service. Desktop: the **Open** icon (**+**) → **Use connectors**. Available on Copilot.com and Copilot Mobile (iOS/Android), and in the Copilot app on Windows.
- **Default:** Not stated on Microsoft's page; Microsoft's Windows announcement describes connectors as *"Opt-in per service"*, so the effective default is **not connected**.
- **Exposes:** Connectable services are **Microsoft OneDrive, Microsoft Outlook.com (email, calendar, contacts), Google Drive, Google Gmail, Google Calendar, Google Contacts**. Once connected, Copilot can search across all of them in natural language. Microsoft commits: *"Microsoft do not use data from connected services to train Copilot. Your connected data is not used to personalize your experience without your permission."* But *"Copilot responses that include your data will remain in your conversation history unless you delete the conversation"* — meaning connector-sourced content is copied into retained chat history.
- **Recommend:** Connect nothing you wouldn't paste into the chat box. **The specific OAuth scopes requested are not published in any Microsoft document I could find** — review them on the Google/Microsoft consent screen itself, not in Copilot's UI, which does not enumerate them. Microsoft's page also does not document a disconnect path or where to revoke at the identity provider.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/connecting-microsoft-copilot-to-other-services ; https://blogs.windows.com/windowsexperience/2025/10/16/making-every-windows-11-pc-an-ai-pc/ — checked 2026-10-02
- **Confidence:** `verified` (service list, training/retention statements, click paths) / `unresolved` (per-connector defaults, OAuth scopes, documented revocation path)

- **Setting:** File Search and File Read
- **Where:** Copilot app → **Account** → **Settings** → **File Search and File Read**
- **Default:** `unresolved` — Microsoft states only *"You can adjust permissions for what Copilot file search can access by going to Account > Settings > File Search and File Read."*
- **Exposes:** Copilot reading local files for grounding. Whether file contents are uploaded for cloud inference is not stated. Related verified capability: *"Copilot can reference files in your connected online storage providers like OneDrive and Google Drive, with your permission."*
- **Recommend:** Turn both off unless actively needed, and re-verify after each Copilot app update.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/windows/welcome-to-copilot-on-windows-675708af-8c16-4675-afeb-85a5a476ccb0 — checked 2026-10-02
- **Confidence:** `verified` (control, path) / `unresolved` (default, data flow)

### (b) Microsoft Copilot (tenant)

- **Setting:** User access *(agents and plugins)*
- **Where:** M365 admin center → **Agents** → **Settings** → **User access**. Options: *All users* / *No users* / *Specific users or groups*. ("Plugins include tools, MCP servers, connectors, skills, and other AI artifacts.")
- **Default:** **All users.** *"All users - This option is the default. It means that all users in the organization can access agents and plugins, subject to the existing app policies and user assignments."*
- **Exposes:** Every user in the tenant can use agents and plugins — including MCP servers and non-Microsoft connectors whose data handling sits outside your Microsoft agreements. Microsoft's own warning on that page: *"Data processed by non-Microsoft services isn't subject to Microsoft agreements. Review the terms provided by non-Microsoft agent and plugin publishers."*
- **Recommend:** Scope to *Specific users or groups*. This is the highest-leverage agent control because it gates the whole class rather than individual agents.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Agent and plugin access *(**Allow agents and plugins built by Microsoft** / **…by your organization** / **…by external publishers**)*
- **Where:** M365 admin center → **Agents** → **Settings** → **Agent and plugin access**
- **Default:** `unresolved` per option. Related verified facts: agent management *"is enabled by default in all Microsoft Copilot licensed tenants"*, and store agents require approval — *"before users can access these agents, each agent must undergo a streamlined process of submission and approval"*; *"Members of your organization can only access the agents that you have allowed."*
- **Exposes:** With external publishers allowed, users can install third-party agents that process tenant data outside Microsoft's agreements.
- **Recommend:** Turn off **external publishers** until you have a named review process. Quirk to expect: *"Users see agents and plugins built by Microsoft even if you disable the setting, but they can't install those agents and plugins."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — checked 2026-10-02
- **Confidence:** `verified` (options, effects) / `unresolved` (defaults)

- **Setting:** Advanced package uploads
- **Where:** M365 admin center → **Copilot** → **Settings** → **All settings** → **Advanced package uploads**. Options: *All users* / *No users* / *Specific users or groups*.
- **Default:** `unresolved`
- **Exposes:** An "advanced" package is *"a package that uses either a Declarative Agent with actions or an MCP server"* — user-side-loaded code that can call arbitrary endpoints. Basic (instructions-only) packages are always allowed.
- **Recommend:** *No users*, or a small named developer group. Side-loaded MCP servers are the least-governed data path in the tenant surface.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified` (options) / `unresolved` (default)

- **Setting:** Copilot connectors — admin-configured (synced) / self-serve (synced) / federated (MCP)
- **Where:** M365 admin center → **Settings** → **Search & intelligence** → **Data sources**; federated connectors appear in the connections list as **Ready**. Admins manage federated connectors via **Copilot connectors** → **Your connections**.
- **Default:** No connection crawls until an admin configures one. Microsoft-provided default federated connectors *"appear as Ready in your connections list."*
- **Exposes:** **Synced** connectors index external system content **into Microsoft Graph** inside your tenant, where it becomes groundable: *"It automatically includes indexed connector content when generating responses—no extra setup required."* Source ACLs are honored (*"Search and Copilot only show items to users who have access in the source system"*) — but ACL fidelity is only as good as the connector. **Self-serve** connectors *"Connect using the user's own identity, credentials, and consent — not admin credentials"*, and on disconnect *"the indexed content is removed and synchronization stops."* **Federated** connectors do *"No indexing… data remains in the source system"*, querying live via MCP over OAuth 2.0.
- **Recommend:** Prefer federated for sensitive sources — nothing lands in your index. Audit source-side ACL fidelity before enabling any synced connector; a connector ingesting with coarse or stale ACLs turns a quiet external repository into tenant-wide Copilot grounding. **Re-review federated connectors now:** *"Write actions will be available starting early October 2026"*, which flips them from read-only to mutating.
- **Risk:** High (synced) / Medium (self-serve, federated)
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/overview — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Microsoft Graph connectors / agents as Copilot extensibility
- **Where:** M365 admin center → **Integrated apps**
- **Default:** Admin-gated. *"Admins have full control to select which agents are allowed in their organization. A user can only access the agents that their admin allows and that the user installed or is assigned. Microsoft Copilot only uses agents that are turned on by the user."*
- **Exposes:** *"Data from Graph connectors can be returned in Microsoft Copilot responses if the user has permission to access that information."* In **Integrated apps**, *"admins can view the permissions and data access required by an agent as well as the agent's terms of use and privacy statement."*
- **Recommend:** Make the Integrated apps permission review a documented gate, not a formality — it is the one place the agent's requested data access and its own privacy statement are both visible before approval.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** User consent settings *(Entra ID)*
- **Where:** https://entra.microsoft.com → **Identity** → **Applications** → **Enterprise applications** → **Consent and permissions** → **User consent settings**. Built-in policies: `microsoft-user-default-low` ("Allow user consent for apps from verified publishers, for selected permissions"), `microsoft-user-default-legacy` ("Allow user consent for apps"), or disabled.
- **Default:** *"By default, all users are allowed to consent to applications for permissions that don't require administrator consent. For example, by default, a user can consent to allow an app to access their mailbox but can't consent to allow an app unfettered access to read and write to all files in your organization."* Which specific built-in policy new tenants receive is **`unresolved`**.
- **Exposes:** Any user can grant a third-party app delegated access to their own mailbox and similar scopes — which an agent or plugin can then ride.
- **Recommend:** Microsoft's own guidance: *"we recommend that you allow user consent only for applications that have been published by a verified publisher"* (`microsoft-user-default-low`), paired with deliberate permission classification and the **admin consent workflow** enabled so tightening consent doesn't just generate shadow workarounds.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-user-consent — checked 2026-10-02
- **Confidence:** `verified` (behavior) / `unresolved` (which built-in policy is the new-tenant default)

### (c) Copilot in Windows

- **Setting:** Reduce protections for agent connectors *(also rendered "Enable more agent connectors by reducing protections")*
- **Where:** **Settings → System → Advanced → AI components → Reduce protections for agent connectors**
- **Default:** **Off.** Microsoft's verbatim warning: *"This setting enables MCP servers to run with more access and privileges, and may expose your device to additional security threats."*
- **Exposes:** With it **off**, MCP servers reached through the Windows On-device Agent Registry run contained in a separate Windows session under a separate agent account, with **no** access to your files, settings, registry, credentials, or the apps and windows you are using. Turning it **on** lets unpackaged MCP servers and `.mcpb` bundles run **in your user session** — i.e. with your identity.
- **Recommend:** Leave **Off** permanently. Microsoft describes it as being *"for testing purposes"*; flipping it collapses the single most meaningful boundary in the Windows agentic stack.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/ai/mcp/servers/mcp-containment — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(File access consent for MCP host apps — a runtime prompt, not a named toggle)*
- **Where:** Consent dialog shown when an MCP server requests a known-folder capability
- **Default:** Not granted until you accept a prompt.
- **Exposes:** The sharpest trap in the design, documented plainly: *"Permissions to user files are granted for the host and not per server. When the user grants access to their user files, any MCP server used in that session will have access to the user's files."* One "yes" to one server grants every server under that host.
- **Recommend:** Decline unless you know every MCP server that host loads. Assume a grant is host-wide and session-wide, never per-tool.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/ai/mcp/servers/mcp-containment — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Enable or Disable Agent Connectors — `ConfigureAgentConnectors`
- **Where:** CSP `./Device/Vendor/MSFT/Policy/Config/WindowsAI/ConfigureAgentConnectors`. **Enterprise/Education/IoT only (not Pro); Windows Insider Preview.** GP path shown as the unrendered `WindowsAI > AT > WindowsComponents > WindowsAI`.
- **Default:** **`0` = "User in control."** Other values: `1` Force Enable, `2` Force Disable.
- **Exposes:** At default, each individual user decides whether MCP agent connectors operate on a managed device.
- **Recommend:** Set `2` (Force Disable) until you have an agent inventory and a cross-prompt-injection threat model.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Agent connector allow-list — `AgentConnectorAccessPolicy`
- **Where:** CSP Device only. Enterprise/Education/IoT; Insider Preview. JSON string per the schema at `https://go.microsoft.com/fwlink/?LinkId=2363700` (not fetched).
- **Default:** None published.
- **Exposes:** Governs which MCP server/host connections are permitted — the chokepoint for which agents reach which tools.
- **Recommend:** If you allow agents at all, run an explicit allow-list here rather than leaving users in control.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified` (policy exists, scope) / `unresolved` (schema contents)

### (d) GitHub Copilot

- **Setting:** MCP servers in Copilot
- **Where:** Enterprise: the **MCP** page under AI controls. Organization: https://github.com/organizations/ORG/settings/copilot/policies
- **Default:** **Disabled.** *"The policy is disabled by default."* Scope limit, verbatim: *"The MCP policy **only** applies to users who have a Copilot Business or Copilot Enterprise subscription from an organization or enterprise that configures the policy"*, and *"Copilot Free, Copilot Pro, Copilot Pro+, or Copilot Max **do not** have their MCP access governed by this policy."* Also *"This policy does not control access and permissions for the GitHub MCP server in third-party host applications."*
- **Exposes:** At default, nothing for Business/Enterprise. For individual plans there is **no org-level MCP gate at all** — personal-plan users can wire up arbitrary MCP servers unconstrained by enterprise policy. And note the interaction with §8(d): **"Default policy for new features" names the MCP policy as in scope**, and unconfigured GA features are slated to be **enabled on 2026-10-22**.
- **Recommend:** Leave disabled, and **explicitly** disable it rather than leaving it unconfigured, so the 22 October default-enablement doesn't flip it. For individual-plan developers on company machines, the control has to be device-level, not GitHub-level.
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp/extend-copilot-chat-with-mcp ; https://docs.github.com/en/copilot/concepts/enterprise/default-availability — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Partner agents *(Anthropic Claude, OpenAI Codex)*
- **Where:** https://github.com/settings/copilot/coding_agent — toggles under **Partner agents**
- **Default:** Appears disabled until the user enables each one; GitHub does not state the default explicitly, so `unresolved`. *"You can choose whether to allow the following coding agents to be enabled"*, and *"Installed agent apps also appear under 'Partner agents' and are enabled in the same way."*
- **Exposes:** *"Coding agents have access to the same repositories that Copilot cloud agent has been enabled in"* — and cloud agent defaults to **all repositories** (see §7(d)). So enabling a partner agent grants a third-party agent that same repo scope.
- **Recommend:** Narrow **Repository access** to *Only selected repositories* **before** enabling any partner agent, not after.
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies — checked 2026-10-02
- **Confidence:** `verified` (scope inheritance, location) / `unresolved` (default)

- **Setting:** Copilot access to Bing
- **Where:** https://github.com/settings/copilot
- **Default:** **Disabled.** *"This setting is disabled by default."*
- **Exposes:** When enabled, Copilot Chat *"use[s] Bing to search the internet"* — prompt-derived queries leave GitHub for Microsoft's search service.
- **Recommend:** Leave disabled unless you need current-technology lookups; it is one of the few GitHub Copilot settings that ships private.
- **Risk:** Low at default, Medium when enabled
- **Evidence:** https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies — checked 2026-10-02
- **Confidence:** `verified`

---

## 4. Sharing & publication defaults

### (a) Consumer Copilot

- **Setting:** Share chat / Share response
- **Where:** Conversation: **Share** (near the top of the conversation) → **Share chat** → **Copy link**. Single response: **More options (…)** → **Share response** → **Copy link**.
- **Default:** Sharing is **on**; a created link is accessible to anyone who has it, subject to sign-in. For personal Microsoft accounts: *"Anyone you share the link with can open it by signing in with their Microsoft account."* (Work/school accounts: *"Anyone in your organization who has the link can open it by signing in."*)
- **Exposes:** The full conversation or response as a snapshot, to any holder of the URL who signs in with any Microsoft account. Treat it as effectively public. Mitigation Microsoft does state: *"Sharing a Copilot conversation or response doesn't give anyone access to referenced Microsoft 365 content."*
- **Recommend:** Never paste confidential content into a chat you intend to share, and audit links at **Settings → Data controls → Shared links** — you can *"Review links you created"*, *"Copy a sharing link again"*, or *"Stop sharing an existing link"*, after which *"the link stops working and people can no longer access the shared conversation or response."*
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-365-copilot/share-conversations-responses-in-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot Pages *(consumer)*
- **Where:** Copilot → Pages. Requires a **Microsoft 365 Personal, Family, Premium or Pro** subscription.
- **Default:** `unresolved` — Microsoft's FAQ does not state the sharing scope of a newly created Page. What is verified: *"A Copilot Page is saved as a .page file in a new user-owned SharePoint Embedded container."*
- **Exposes:** Unconfirmed. Do not assume private-by-default and do not assume link-shared-by-default.
- **Recommend:** Create a Page as a test user and inspect the resulting permissions before writing any guidance about it.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-365-copilot/frequently-asked-questions-about-microsoft-365-copilot-pages — checked 2026-10-02
- **Confidence:** `unresolved`

### (b) Microsoft Copilot (tenant)

- **Setting:** Allow users to share Copilot responses
- **Where:** M365 admin center → **Copilot** → **Settings** → **Copilot sharing** → select or clear **Allow users to share Copilot responses** → **Save**. Roles: **AI Reader** to view, **AI Admin** to edit.
- **Default:** **On.** *"Copilot sharing is turned on by default."*
- **Exposes:** Any user can mint a link to a full Copilot session or a single response. Scope note: *"This setting also controls whether users can share content with lower-sensitivity labels, such as General or Public, or no sensitivity label."* Recipients get a snapshot and *"Copilot creates a separate copy in the recipient's chat history"* if they continue it — so turning sharing off later does not unwind existing copies: *"Existing recipient copies aren't affected."*
- **Recommend:** Turn off unless you have a reason not to; otherwise rely on Purview, which *"records Copilot sharing activity, including sharing events, link access, and blocked sharing attempts."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-copilot-manage-content-sharing — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Create and view Copilot Pages and Copilot Notebooks
- **Where:** Cloud Policy — https://config.office.com/ → **Customization** → **Policy Management**. Values *Enabled* / *Disabled* / *Not configured*.
- **Default:** **Enabled.** Microsoft's own at-a-glance table reads *"Copilot Pages and Copilot Notebooks creation | Cloud Policy: Create and view Copilot Pages and Copilot Notebooks | **Enabled**"*, and *"Not configured: Copilot Pages and Copilot Notebooks creation and integration are available to the users."*
- **Exposes:** Pages (`.page` files) and Notebooks live in *"the same user-owned SharePoint Embedded container used by Loop My workspace"*, count against your SharePoint quota, and in SharePoint admin center, PowerShell and Purview audit appear **only under the application name `Loop`** — *"there's no separate Copilot Pages or Copilot Notebooks application filter."* The **default sharing audience of a new Page is not documented** (`unresolved`).
- **Recommend:** Keep enabled only if you accept that your audit trail cannot distinguish Copilot Pages from Loop. Disabling does not delete: *"Existing Copilot Pages and Notebooks aren't deleted."* Your real blast-radius control is Loop components — without them *"Copilot Pages are only interactive within the Microsoft Copilot app and supported chat experiences."* Policy-change latency: up to 90 minutes if policies already existed, up to 24 hours if none did.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/loop/cpcn-admin-configuration — checked 2026-10-02
- **Confidence:** `verified` (policy default, storage, audit) / `unresolved` (new-Page sharing scope)

- **Setting:** Enable code previews for AI-generated content in Microsoft Copilot Chat and Copilot Pages
- **Where:** Cloud Policy — config.office.com → Customization → Policy Management
- **Default:** **Enabled.** *"Not configured: Users can view and interact with AI-generated code previews in Copilot Chat and Copilot Pages, including building lightweight apps."*
- **Exposes:** Copilot executes model-generated code previews inside Chat and Pages, including building lightweight apps.
- **Recommend:** Disable unless you have a specific need — it is model-authored code running in a user-facing surface, on by default.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/loop/cpcn-admin-configuration — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Sharing *(agents)*
- **Where:** M365 admin center → **Agents** → **Settings** → **Sharing**. Options *All users* / *No users* / *Specific users*.
- **Default:** `unresolved`
- **Exposes:** Who can broadcast a custom agent tenant-wide. Two limits: *"Sharing control only applies to agents built with **Microsoft Copilot Agent Builder**"*, and *"No users"* is not absolute — *"Disable sharing at the org level, but users can still share directly with specific individuals."*
- **Recommend:** *Specific users*, and note the gap: Copilot Studio-built agents have their own sharing path that this does not govern.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — checked 2026-10-02
- **Confidence:** `verified` (options, scope limit) / `unresolved` (default)

- **Setting:** Agent feedback sharing
- **Where:** M365 admin center → **Agents** → **Settings** → **Agent feedback sharing**. Options *No agents* / *All agents* / *Selected agents*.
- **Default:** `unresolved`
- **Exposes:** Developers — including external publishers — receive *"thumbs-up or thumbs-down ratings and comments"* from your users. *"This setting doesn't affect whether people can rate agents or what data an agent can access."*
- **Recommend:** *No agents*, or *Selected agents* limited to internally built ones. Free-text feedback from users is a classic accidental-disclosure channel to third parties.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — checked 2026-10-02
- **Confidence:** `verified` (options) / `unresolved` (default)

### (c) Copilot in Windows / Recall

- **Setting:** Export past snapshots
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Advanced settings** → **Export snapshots** → **Export past snapshots** → **Export**. Scopes: last 7 days, last 30 days, or all snapshots. Windows Hello required to start.
- **Default:** Available to unmanaged **EEA** users only. On managed devices **denied** — `AllowRecallExport` **Default Value `0`** = *"Deny export of Recall and snapshots information."*
- **Exposes:** Hands a third-party app or website your snapshots plus *"Snapshot details, including information related to each snapshot such as the time and date it was saved along with associated information from opened apps"* — encrypted, together with your **Recall export code**, which is the decryption key. There is a documented developer API to **decrypt exported snapshots**. Exports outlive a Recall reset.
- **Recommend:** Do not export. The export code is shown once during Recall setup — *"The Recall export code is displayed to users during Recall setup even if this policy is set to disabled or not configured"* — and handing it over hands over the archive permanently.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/topic/680bd134-4aaa-4bf5-8548-a8e2911c8069 ; https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Export snapshots from now on
- **Where:** Same path under **Export snapshots**
- **Default:** Off; EEA only; denied by default on managed devices.
- **Exposes:** A **continuous** stream of every future snapshot to a third party until you turn it off or reset Recall. *"Users will be reminded every 30 days that continuous export is enabled."*
- **Recommend:** Never enable. A 30-day reminder cadence is not an adequate guardrail on a continuous screen-archive export.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/topic/680bd134-4aaa-4bf5-8548-a8e2911c8069 ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

### (d) GitHub Copilot

- **Setting:** *(Copilot cloud agent session visibility)*
- **Where:** The **"All sessions"** view on the **Agents** tab of a repository
- **Default:** **Shared.** Verbatim: *"Copilot cloud agent sessions are shared by default. They appear in the 'All sessions' view on the 'Agents' tab of your repository, visible to anyone with access to the repository."*
- **Exposes:** Your prompts to the cloud agent, its reasoning and its actions are readable by every collaborator on the repository — including, on a public repository, everyone.
- **Recommend:** Assume anything you say to the cloud agent is published to the repo's audience. Do not paste credentials, customer names, or unreleased plans into an agent prompt. I found no documented toggle to make cloud agent sessions private — mark that `unresolved`.
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/session-data — checked 2026-10-02
- **Confidence:** `verified` (default) / `unresolved` (whether it can be changed)

---

## 5. Retention & deletion

### (a) Consumer Copilot

- **Setting:** *(conversation activity retention — no toggle)*
- **Where:** n/a
- **Default:** **18 months.** *"By default, we store conversation activity for 18 months"* / *"Copilot retains the last 18 months of interactions in your conversation history."* There is **no documented option to turn conversation history off** — the support page does not mention one.
- **Exposes:** 18 months of prompts and responses held against your Microsoft account, usable for ads personalization (unless disabled) and — on the older app — training (unless opted out).
- **Recommend:** Delete on a schedule; there is no "don't record" switch to rely on.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot ; https://support.microsoft.com/en-us/topic/conversation-history-in-microsoft-copilot-9a07325a-0366-4c2d-82cb-dab61be8287c — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Delete all activity history
- **Where:** **https://account.microsoft.com/privacy** → **Privacy** → **Empower your productivity** → **Copilot** → **Your Copilot app activity history** → choose **Copilot apps** or **Copilot in Microsoft 365 apps** → **Delete all activity history** → confirm **Clear**. (**Export all activity history** is on the same page.) Applies only when signed in with a Microsoft account.
- **Default:** Nothing deleted until you act.
- **Exposes:** Removes the stored record of typed prompts and AI responses. Retention after deletion is not stated.
- **Recommend:** Use this rather than per-chat deletion; the dashboard is the only place that clears the whole account-level record, and it also offers an export for a data-portability request.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/topic/manage-your-microsoft-copilot-activity-history-in-the-privacy-dashboard-2acfee74-d7c4-406d-b3fb-5f73da9272fc ; https://www.microsoft.com/en-us/privacy/privacy-support-requests — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Delete individual conversations
- **Where:** copilot.com: conversation → **…More** → **Delete**. Windows/macOS: right-click → **Delete**. Mobile: three dots → **Delete**. **Apple ID sign-in:** **Account → Privacy → Clear my history**.
- **Default:** Nothing deleted until you act.
- **Exposes:** Per-conversation removal only.
- **Recommend:** Note the Apple-ID path differs from the Microsoft-account path — a user who tidied one may not have touched the other.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/topic/conversation-history-in-microsoft-copilot-9a07325a-0366-4c2d-82cb-dab61be8287c — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Delete all memories
- **Where:** Copilot → **Settings** → **Personalization** → **Manage** → **Delete all memories** (or the trash icon per memory)
- **Default:** Memories persist until deleted; turning the toggle off does not delete them.
- **Exposes:** Saved memories survive history deletion and vice versa — they are two separate stores.
- **Recommend:** Do both. Deleting chats does not clear memories derived from them.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(Vision and image retention — no toggle)*
- **Where:** n/a
- **Default:** *"Session data may be temporarily retained for up to **47 hours** to support user-submitted feedback and is automatically deleted afterward if no feedback is submitted."* Images: *"All images are deleted within **30 days** after the conversation ends."* Screenshots taken by **Browse with Copilot** in Edge *"are retained for up to **30 days**."* Conversation transcripts persist in chat history regardless.
- **Exposes:** Short-lived raw media, long-lived transcripts.
- **Recommend:** Delete the conversation if you shared something sensitive — the transcript is the durable artifact, not the image.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-vision-with-microsoft-copilot ; https://support.microsoft.com/en-us/microsoft-copilot/transparency-note-for-microsoft-copilot ; https://support.microsoft.com/en-us/topic/copilot-actions-in-edge-5ed5e17e-42df-40a3-984a-20420eba86e2 — checked 2026-10-02
- **Confidence:** `verified`

### (b) Microsoft Copilot (tenant)

- **Setting:** Retention policy locations — **Microsoft Copilot experiences** / **Enterprise AI apps** / **Other AI apps**
- **Where:** Microsoft Purview portal → Data Lifecycle Management → Retention policies. Locations now include Microsoft 365 Copilot, Security Copilot, Copilot in Fabric, Copilot Studio; Entra-registered AI apps, ChatGPT Enterprise, Microsoft Foundry; and under "Other AI apps" — ChatGPT, Google Gemini, **Microsoft Copilot (consumer version)**, DeepSeek.
- **Default:** **No policy unless you create one, and absent one the data persists:** *"In most scenarios, these messages aren't removed."* Migration trap: *"Previously, messages from Microsoft 365 Copilot and Microsoft 365 Copilot Chat were automatically included in the retention policy location named Teams chats and Copilot interactions... Retention policies for Microsoft 365 Copilot and Microsoft 365 Copilot Chat are now separate from Teams chats."*
- **Exposes:** Prompts and responses accumulate indefinitely in a hidden Exchange mailbox folder, discoverable by eDiscovery, with no default expiry. "Other AI apps" require *"a collection policy with the setting to capture content"* to be in scope at all.
- **Recommend:** Create an explicit delete-after-N-days policy for **Microsoft Copilot experiences**. If you had a policy on the old combined location, verify your Copilot coverage did not silently lapse.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/purview/retention-policies-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(storage mechanics and real deletion latency — not configurable)*
- **Where:** n/a
- **Default:** *"Data from generative AI messages is stored in a hidden folder in the mailbox of the user who runs the AI app. This hidden folder isn't designed to be directly accessible to users or administrators."* The mailbox has `RecipientTypeDetails` of **UserMailbox**. Expired items move to **SubstrateHolds**, stay *"at least 1 day"*, then a timer job (*"typically takes 1-7 days to run"*) purges them. Microsoft's worked example: *"a delete action after 1 day could take 16 days before the message is permanently deleted so that it's no longer returned in eDiscovery searches."*
- **Exposes:** Two traps. *"Messages visible in your AI apps are not an accurate reflection of whether they are retained or permanently deleted for compliance requirements."* And *"permanent deletion from the SubstrateHolds folder is always suspended if the mailbox is affected by another retention policy for the same location, Litigation Hold, delay hold, or if an eDiscovery hold is applied to the mailbox for legal or investigative reasons."*
- **Recommend:** Never answer a deletion or DSR question from the Copilot UI. Verify with eDiscovery, and check for Litigation Hold — a hold silently defeats your Copilot deletion policy.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/purview/retention-policies-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Delete your Microsoft Copilot activity history *(user-initiated)*
- **Where:** **https://myaccount.microsoft.com/** (My Account portal)
- **Default:** History retained. *"this stored data provides users with Copilot activity history."*
- **Exposes:** Prompts, responses and *"citations to any information used to ground Copilot's response"*, stored under M365 contractual commitments, *"encrypted while it's stored and isn't used to train foundation LLMs."*
- **Recommend:** Tell users this exists — and tell them it triggers the Purview deletion pipeline above, not an instant purge.
- **Risk:** Low
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(admin read paths for Copilot interaction data)*
- **Where:** Purview **Content search** / eDiscovery; **Microsoft Teams Export APIs** for Teams chats with Copilot
- **Default:** Available to compliance admins. *"To view and manage this stored data, admins can use Content search or Microsoft Purview."*
- **Exposes:** Copilot prompts and responses are readable by appropriately-privileged admins — part of EDP, not an exception to it. *"Until messages are permanently deleted from the SubstrateHolds folder, they remain searchable by eDiscovery tools."*
- **Recommend:** Include Copilot interaction content in your privileged-access inventory and tell users it is discoverable.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy ; https://learn.microsoft.com/en-us/purview/retention-policies-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(departed users)*
- **Where:** n/a
- **Default:** *"If a user leaves your organization and their Microsoft 365 account is deleted, their Copilot and other AI app messages that are subject to retention are stored in an inactive mailbox. The messages remain subject to any retention policy that was placed on the user before their mailbox was made inactive, and the contents are available to an eDiscovery search."*
- **Exposes:** Ex-employees' Copilot prompt history survives account deletion and stays discoverable.
- **Recommend:** Apply the Copilot retention policy **before** offboarding; post-hoc application won't reach an already-inactive mailbox.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/purview/retention-policies-copilot — checked 2026-10-02
- **Confidence:** `verified`

### (c) Copilot in Windows / Recall

- **Setting:** Set maximum storage for snapshots used by Recall
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Storage**. Policy: `SetMaximumStorageSpaceForRecallSnapshots`; GP **Windows Components → Windows AI → Set maximum storage for snapshots used by Recall**. **Policy is Enterprise and Education only.**
- **Default:** **`0` = OS decides by disk size** — *"25 GB is allocated when the device storage capacity is 256 GB. 75 GB is allocated when the device storage capacity is 512 GB. 150 GB is allocated when the device storage capacity is 1 TB or higher."* Selectable: 10/25/50/75/100/150 GB. Oldest snapshots are evicted first.
- **Exposes:** On a 1 TB laptop, 150 GB of screen history — months of everything you looked at.
- **Recommend:** Set to the minimum (10 GB) wherever Recall is permitted. A smaller cap means a shorter effective exposure window if the device is lost or compromised.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Set maximum duration for storing snapshots used by Recall
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Storage**. Policy: `SetMaximumStorageDurationForRecallSnapshots`. **Enterprise and Education only.** Values: 30 / 60 / 90 / 180 days (and 0 = OS decides).
- **Default:** **CONTRADICTION FLAGGED, NOT RESOLVED — Microsoft's own documentation conflicts, and this one matters.** The CSP page states *"When this policy isn't configured, the maximum storage duration is 90 days unless the current user specifies a different value"* with **Default Value: 90**. The `manage-recall` page states the opposite: *"If the policy isn't configured, snapshots aren't deleted until the maximum storage allocation is reached, and then the oldest snapshots are deleted first."* I am not resolving this from Microsoft's docs.
- **Exposes:** On the second reading, snapshots persist until the disk cap evicts them — potentially a year or more of screen history on a large drive.
- **Recommend:** Set **30 days** explicitly. Do not inherit a default that Microsoft documents two different ways. *"If both maximum storage duration and maximum storage space are set for Recall, then snapshots are deleted when the first maximum is reached."* (`manage-recall` additionally prints the wrong friendly name for this policy in its Computer Configuration row — the CSP page has the correct one.)
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `unresolved` (out-of-box default) / `verified` (options and policy values)

- **Setting:** Delete snapshots
- **Where:** Settings → Privacy & security → **Recall & snapshots**. Scopes: past hour, 24 hours, 7 days, 30 days, or **Delete all**. Per-app/site: in a search result, **…** → **Delete all**.
- **Default:** N/A (action)
- **Exposes:** Nothing.
- **Recommend:** Delete-all before any device handoff, repair, resale, or border crossing. Deletion does not stop future capture — pair it with adding the app to **Apps to filter**.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15 ; https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Reset Recall
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Advanced settings** → **Reset Recall**
- **Default:** N/A (action)
- **Exposes:** Deletes all snapshots and resets Recall settings. In the EEA a reset **issues a new export code** — but snapshots already exported, and anything shared with a third party, survive the reset.
- **Recommend:** Use for a clean slate, understanding it does not reach exported copies.
- **Risk:** Low
- **Evidence:** https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c ; https://support.microsoft.com/en-us/topic/680bd134-4aaa-4bf5-8548-a8e2911c8069 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(snapshot deletion triggered by policy change)*
- **Where:** `AllowRecallEnablement` set to disabled, or `DisableAIDataAnalysis` set to enabled
- **Default:** N/A
- **Exposes:** Both policies delete existing snapshots when applied: *"If snapshots were previously saved on the device, they'll be deleted when this policy is disabled"* / *"...when this policy is enabled."* Removing Recall requires a device restart.
- **Recommend:** This is your fleet-wide remediation lever if Recall was enabled before you had a policy in place.
- **Risk:** Low (it's a control)
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Clear Browsing data *(Copilot for Windows)*
- **Where:** Copilot app → **Profile** → **Settings** → **Browsing settings** → **Web data and security** → **Clear Browsing data** → choose time range and data types
- **Default:** Nothing cleared until you act.
- **Exposes:** Copilot on Windows keeps browser-style data — cookies imported from Edge, history, saved cards.
- **Recommend:** Clear after any shopping or authenticated browsing done inside Copilot.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

### (d) GitHub Copilot

- **Setting:** Delete synced sessions
- **Where:** GitHub.com (sessions view); Copilot CLI and the GitHub Copilot app prompt on local deletion
- **Default:** Synced sessions retained on GitHub.com with **no published retention period** (`unresolved`).
- **Exposes:** Prompt/response history held server-side indefinitely as far as the docs state.
- **Recommend:** Delete synced sessions deliberately, or don't enable cloud session storage at all (see §2(d)).
- **Risk:** Medium
- **Evidence:** https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/session-data — checked 2026-10-02
- **Confidence:** `verified` (deletion path) / `unresolved` (retention)

---

## 6. Voice, audio & camera

### (a) Consumer Copilot

- **Setting:** Share screen *(Copilot Vision)*
- **Where:** Windows app: start a **Voice** session → **Share screen** → pick screen or app (*"You can share up to two apps at a time"*) → end with **Stop** in the floating toolbar. Edge: **Share screen**, end with **X** in the toolbar at the bottom of the Copilot window. Mobile: start a Voice session → **Share screen** (device camera or screen), end with **X**. Requires **Microsoft 365 Personal, Family, or Premium**.
- **Default:** **Off, per session.** *"Vision is off by default"* and requires explicit activation each time, with a privacy notice on first use: *"The first time a user uploads an image to Copilot Vision, they will be provided with information on how their image is processed."*
- **Exposes:** The pixels of whatever you share go to Microsoft's cloud for analysis. Commitments: not used for training or personalization; session data retained up to 47 hours; *"Screenshots and camera images shared with Vision aren't stored after your session ends"*; *"text transcripts of your interactions may be saved so you can revisit them later and to help monitor for abuse."*
- **Recommend:** Share a single **window**, never the whole screen, and never with a password manager, mail client, or client data visible. Stop the session explicitly rather than minimizing.
- **Risk:** High when active, Low at default
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-vision-with-microsoft-copilot ; https://support.microsoft.com/en-us/microsoft-copilot/transparency-note-for-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot Voice *(microphone)*
- **Where:** Press the **microphone icon** in the composer; mute by clicking the microphone icon, which *"will disable the microphone and stop Copilot from listening"*; end with **X**. Voice selection: copilot.com → profile icon → profile name → **Voice**; Windows/macOS → profile icon → **Settings** → next to **Voice**; mobile → menu → profile icon → **Voice Settings**.
- **Default:** Not listening until invoked. *"you may need to grant microphone access to Copilot on your browser or device."*
- **Exposes:** *"Voice data is used to provide the Copilot Voice service"*; *"Text transcripts produced from your Copilot Voice conversations are handled in the same way as conversation history."* Whether raw audio is stored, and for how long, is **not stated** on the consumer Voice page.
- **Recommend:** Revoke microphone permission at the OS level if you don't use Voice — *"you can turn off Copilot access to your microphone in your platform settings"*, which is a harder guarantee than the in-app control. Set **Training on voice conversations** to off (§1(a)).
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-voice-with-microsoft-copilot — checked 2026-10-02
- **Confidence:** `verified` (controls, paths) / `unresolved` (audio retention)

- **Setting:** Listen for "Hey Copilot"
- **Where:** Copilot app → **Settings** (the **…** menu) → **General** → **Listen for "Hey Copilot"**
- **Default:** **Off.** *"Starting a voice chat by saying 'Hey Copilot' is turned off by default."*
- **Exposes:** Continuous local listening for the wake phrase. Microsoft: *"'Hey Copilot' only listens for you to say, 'Hey Copilot.' It doesn't listen to any other words or noises"*, and new chats can't start while the screen is locked or another app is playing audio. Microsoft concedes *"Language and accent variations may cause accidental activation."*
- **Recommend:** Leave **Off**. An always-listening mic with an admitted false-positive rate is a poor trade for a shortcut Win+C already gives you.
- **Risk:** Medium
- **Evidence:** https://support.microsoft.com/en-us/topic/a0bf9f39-6dab-47ae-9054-2d919753293e ; https://learn.microsoft.com/en-us/windows/client-management/manage-windows-copilot — checked 2026-10-02
- **Confidence:** `verified`

### (b) Microsoft Copilot (tenant)

- **Setting:** Copilot *(Teams **meeting** policy)*
- **Where:** Teams admin center → **Meetings** → **Meeting policies** → *Recording & transcription* → **Copilot**. PowerShell: `Set-CsTeamsMeetingPolicy -Copilot <value>`. Values: *On* (`Enabled`) / *On with saved transcript required* (`EnabledWithTranscript`) / *On with transcript saved by default* (`EnabledWithTranscriptDefaultOn`) / *Off* (`Disabled`).
- **Default:** **On with saved transcript required** (`EnabledWithTranscript`). Verbatim: *"**This is the default value.** When organizers with this policy create meetings and events, Copilot's default value in their meeting options is **During and after the meeting**. This option is enforced; **organizers can't change this value**."*
- **Exposes:** Out of the box, every organizer is **forced** into *During and after the meeting*, which requires a saved transcript — so meeting content is transcribed and persisted, and the organizer cannot opt out per meeting. This is the most consequential default in the tenant surface.
- **Recommend:** Change to `Enabled` (organizer defaults to *Only during the meeting*, which uses *"temporary speech-to-text audio processing data that isn't saved after the meeting"*, and can still escalate), or `EnabledWithTranscriptDefaultOn` if you want transcripts by default with organizer discretion. Reserve `Disabled` for privileged cohorts.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoftteams/copilot-teams-transcription — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot *(Teams **calling** policy)*
- **Where:** Teams admin center → **Voice** → **Calling policies** → **Copilot**. PowerShell: `Set-CsTeamsCallingPolicy -Copilot`. Values *On* (`Enabled`) / *On with saved transcript required* / *Off*.
- **Default:** **On** (`Enabled`). *"On | Enabled | **This is the default value**. Call participants can use Copilot with or without transcription during calls."*
- **Exposes:** Copilot is on by default in 1:1 and PSTN calls. Scope split: *"Teams calling policies control Copilot in one-to-one and group calls. Teams meeting policies control Copilot in scheduled meetings and Meet now."*
- **Recommend:** `Enabled` with call transcription off gives in-call assistance with nothing persisted; `Disabled` where call content is privileged. Copilot is unavailable in end-to-end encrypted calls and meetings regardless.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoftteams/copilot-teams-calling-transcription — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Transcription *(`-AllowTranscription`)*
- **Where:** Teams admin center → Meetings → Meeting policies → *Recording & Transcription*; `Set-CsTeamsMeetingPolicy -AllowTranscription`
- **Default:** `unresolved`
- **Exposes:** Gates whether Copilot can run after a meeting. Critical residual even when off: *"Depending on your organization's Microsoft Purview retention policies, Copilot prompts and responses during meetings might be retained for compliance purposes, even if recording and transcription are turned off. This applies only to the Commercial cloud."*
- **Recommend:** Do not equate "transcription off" with "nothing kept" — Copilot prompt/response pairs can still be retained.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoftteams/copilot-teams-transcription — checked 2026-10-02
- **Confidence:** `verified` (interaction) / `unresolved` (default)

- **Setting:** Screen and camera sharing *(Vision in Microsoft Copilot)*
- **Where:** M365 admin center → **Copilot** → **Settings** → **Copilot actions** → **Screen and camera sharing**
- **Default:** **On.** *"Vision in Microsoft Copilot is on by default, so no action is required to enable it. If you want to disable vision for users, you can do so in the Microsoft 365 admin center by turning off Screen and camera sharing."*
- **Exposes:** *"users can share their desktop screen or mobile camera and ask Copilot questions about what they're seeing."* At default, any licensed user can stream a screen containing third-party or regulated data, or a phone camera, to Copilot. For M365 Copilot specifically, *"audio and video data are temporarily stored for you to provide feedback to Microsoft and is deleted after 48 hours."*
- **Recommend:** Turn off unless you have a named use case. Screen-sharing to an AI bypasses every document-level control you have built, because it captures rendered pixels rather than permissioned files. *"Disabling vision in Microsoft Copilot doesn't affect voice availability."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** `EnrollVoice` / `EnrollFace` / `PassiveVoiceEnrollment` *(plus `VoiceIsolation`)*
- **Where:** **PowerShell only** — `Set-CsTeamsAIPolicy` / `New-CsTeamsAIPolicy` / `Grant-CsTeamsAIPolicy`. *"This policy is accessible exclusively via Microsoft PowerShell and replaces the previous EnrollUserOverride setting in CsTeamsMeetingPolicy."* Teams admin center can **view** enrollment status and **delete** enrolled data, but not change the default.
- **Default:** **All three enabled.** *"The new policy includes three distinct settings which are enabled by default"* / *"By default, voice and face enrollment is enabled for all users in the organization."* With a gate: *"**Users will still need to opt in** after the feature is available to begin enrolling their voice and face profile."*
- **Exposes:** Biometric voice and face profiles stored *"in the Office 365 trusted compliance store"*, used for speaker attribution and Copilot accuracy. `PassiveVoiceEnrollment` ("Express enrollment") builds a voice profile *"based on the user's in-meeting speech"* continuously. Retention: removed on unenroll; within 90 days of account deletion; auto-removed after one year unused. Microsoft commits *"Microsoft doesn't use the voice and face profiles of users to train any models."* Admins **cannot** export it — *"data export is managed directly by end users."* Not available in GCCH/DoD.
- **Recommend:** Under BIPA or GDPR Art. 9, disable `PassiveVoiceEnrollment` at minimum — passive capture is hard to square with explicit biometric consent even with a user opt-in gate.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoftteams/rooms/voice-and-face-recognition — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot custom dictionary
- **Where:** M365 admin center → **Copilot** → **Settings** → **Other settings** → **Copilot custom dictionary**
- **Default:** No dictionary until you upload one.
- **Exposes:** You upload org vocabulary — *"your organization's proper nouns, technical jargon"* — to improve Teams transcription. The dictionary itself can be sensitive (codenames, unreleased products).
- **Recommend:** Review contents before upload; don't load unannounced project names.
- **Risk:** Low
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page — checked 2026-10-02
- **Confidence:** `verified` (existence) / `unresolved` (default)

- **Setting:** Copilot voice chat at work *(no admin toggle exists)*
- **Where:** n/a
- **Default:** Available; **no feature-specific admin control.** Verbatim: *"There is no feature-specific toggle for admins to disable voice chat today, though web grounding can be disabled if optional connected experiences are turned off."*
- **Exposes:** Voice chat grounded in Microsoft Graph and the web. Commitments: *"Text transcripts from voice chats are stored and managed like regular Copilot conversations, so your existing retention, eDiscovery, and audit policies apply to the transcript content. **No user or Copilot audio is stored.**"* Launch paths: short-press Copilot key / Win+C → **Start a new voice chat**; long-press opens the voice controller; **"Hey Copilot"** wake word (opt-in, via Frontier).
- **Recommend:** Record this as a governance gap rather than looking for a switch. Do not disable optional connected experiences just to reach it — *"turning off optional connected experiences will disable web grounding for not only voice, but other Copilot experiences (including text Copilot) as well."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-windows-copilot — checked 2026-10-02
- **Confidence:** `verified`

### (c) Copilot in Windows

- **Setting:** Microphone / Camera app permissions
- **Where:** Settings → Privacy & security → **Microphone** (`ms-settings:privacy-microphone`) and **Camera** (`ms-settings:privacy-webcam`)
- **Default:** `unresolved`
- **Exposes:** The OS-level substrate under every voice and Vision feature. Revoking the Copilot app's microphone access here kills "Hey Copilot" and Voice regardless of in-app toggles.
- **Recommend:** Revoke microphone for the Copilot app if you don't use Voice — OS permissions outrank in-app ones.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified` (URIs) / `unresolved` (defaults)

- **Setting:** Voice activation
- **Where:** Settings → Privacy & security → **Voice activation** — `ms-settings:privacy-voiceactivation`
- **Default:** `unresolved`
- **Exposes:** The OS-level gate for which apps may use wake-word activation, and whether they may do so when the device is locked.
- **Recommend:** Audit after touching any wake-word feature; it is the system-level backstop for "Hey Copilot."
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified` (URI) / `unresolved` (default)

- **Setting:** Online speech recognition
- **Where:** Settings → Privacy & security → **Speech** — `ms-settings:privacy-speech`
- **Default:** `unresolved`
- **Exposes:** When on, voice input goes to Microsoft's cloud speech service rather than being handled on-device.
- **Recommend:** Off unless you need cloud dictation — Copilot+ PCs ship on-device Speech Recognition on the NPU, so cloud is often unnecessary.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings ; https://learn.microsoft.com/en-us/windows/ai/apis/ — checked 2026-10-02
- **Confidence:** `verified` (URI, on-device alternative) / `unresolved` (default)

- **Setting:** *(Recall audio and video — stated exclusion)*
- **Where:** n/a
- **Default:** Not captured. *"Recall doesn't record audio or save continuous video. It also doesn't save game video when Game Mode is active on platforms that support it."*
- **Exposes:** Nothing audio/video; Recall is still-image snapshots plus OCR.
- **Recommend:** No action — but don't let this reassurance obscure that still snapshots of a video call still capture whatever was on screen.
- **Risk:** Low
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

### (d) GitHub Copilot

**None identified.** No voice, audio or camera permission surface is documented for GitHub Copilot.

---

## 7. Agentic / computer-use permissions

### (c) Copilot in Windows — Recall snapshot capture and the exclusion lists

- **Setting:** Save snapshots
- **Where:** Settings → **Privacy & security** → **Recall & snapshots** → **Save snapshots**. **No documented `ms-settings:` deep link exists** — Microsoft's `ms-settings:` URI reference (updated 2026-09-30) contains no entry for Recall & snapshots, Click to Do, AI components, Agent tools, or Text and image generation. Any guide citing `ms-settings:privacy-recall` is citing an undocumented string.
- **Default:** **Off — opt-in, per user.** Verbatim: *"By default, saving snapshots for Recall aren't enabled. You need to opt in to saving snapshots."* On **unmanaged** Copilot+ PCs the Recall component is present but capture is off until the user opts in: *"For unmanaged Copilot+ PC devices, Recall is available by default but a user has to opt in to save snapshots."* On **commercially managed** devices Recall is removed/disabled by default and *"IT administrators can't, on their own, enable saving snapshots on behalf of their users. The choice to enable saving snapshots requires individual user opt-in consent."* Per-user on multi-user devices: *"If multiple people sign in on a device with different accounts, each person needs to make the decision."* Recall has **never** shipped on-by-default in any SKU per the sources read. Enabling requires >=50 GB free; *"Saving snapshots automatically pauses once the device has less than 25 GB of storage space."*
- **Exposes:** At default, nothing — no snapshots exist. Once on, Windows captures snapshots periodically *"while content on the screen is different from the previous snapshot"*, OCRs them locally, and stores them encrypted on the local disk. Pausing is tactical only: the tray **Pause until tomorrow** auto-resumes at 12:00 AM.
- **Recommend:** Leave **Off**. If you will never use it, remove the component entirely: Control Panel → Programs → **Turn Windows features on or off** → uncheck **Recall** (`ms-settings:optionalfeatures`), or `Disable-WindowsOptionalFeature -Online -FeatureName "Recall" -Remove`. Removal matters because any app can call the **`ms-recall` protocol URI**, which *"opens [Recall] and takes a snapshot of the screen."*
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall ; https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** *(Recall encryption and Windows Hello gating — architecture, not a toggle)*
- **Where:** n/a
- **Default:** Encrypted and biometric-gated, always. Verbatim: *"Recall requires users to confirm their identity with Windows Hello before it launches and before accessing snapshots. **At least one biometric sign-in option must be enabled** for Windows Hello, either facial recognition or a fingerprint, to launch and use Recall... Recall takes advantage of just in time decryption protected by **Hello Enhanced Sign-in Security (ESS)**. **Snapshots and any associated information in the vector database are always encrypted.** Encryption keys are protected via **Trusted Platform Module (TPM)**, which is tied to the user's Windows Hello ESS identity, and can be used by operations within a secure environment called a **Virtualization-based Security Enclave (VBS Enclave)**. This means that other users can't access these keys and thus can't decrypt this information."* Also required: *"Users need to enable Device Encryption or BitLocker"* — and *"Device Encryption or BitLocker are enabled by default on Windows 11."* Hardware floor: a **Copilot+ PC** meeting the **Secured-core** standard, **40 TOPS NPU**, **16 GB RAM**, 8 logical processors, 256 GB storage. Isolation: *"Recall doesn't share snapshots with other users that are signed into Windows on the same device and IT admins can't access or view the snapshots on end-user devices. Microsoft can't access or view the snapshots."*
- **Exposes:** The protections are real and layered. The residual risk is **local, authenticated** compromise — malware running as you, after you have authenticated — and anything that can read the screen, since Recall *"uses general Windows screenshot APIs."* Microsoft states this plainly: *"It's a general security risk to allow screenshots of content that you want to prevent from being exfiltrated."* A PIN alone is insufficient to open Recall.
- **Recommend:** Do not describe Recall as "an unencrypted plaintext database" — that was the 2024 preview, not the shipped design. Do describe it as a locally-stored, Hello-ESS-gated archive whose threat model is device compromise and physical or coerced access.
- **Risk:** Medium (architecture) — High (consequence if the device is compromised)
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall ; https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Apps to filter
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Apps to filter** → **Add app**. Also from inside Recall: **…** → **Settings**. The consumer privacy page renders the control group as **"Add apps and websites."** Policy: `SetDenyAppListForRecall` (semicolon-separated AUMIDs or executable names, e.g. `code.exe;Microsoft.WindowsNotepad_8wekyb3d8bbwe!App;ms-teams.exe`).
- **Default:** **Empty**, with these built-in exceptions: remote desktop sessions from **Remote Desktop Connection (mstsc.exe)**, **VMConnect.exe**, **Azure Virtual Desktop (MSI)** and **RAIL** are filtered; **DRM content** is never stored; **Game Mode** video is not saved; and *"Recall doesn't record audio or save continuous video."*
- **Exposes:** Any app not on this list — password managers, Signal, banking apps, EHR software, your terminal — has its window contents OCR'd into the local index. Caveat on the RDP exceptions: *"Clients will be saved by Recall unless the client implements screen capture protection."*
- **Recommend:** If Recall is on, add every credential manager, messaging client, terminal, and anything touching health, financial or client data. **SKU gap to know:** the policy version is **Enterprise and Education only** — Pro and Home admins cannot centrally seed this list, and consumers must add apps by hand. Policy changes require a device restart.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall ; https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://support.microsoft.com/en-us/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15 — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Websites to filter
- **Where:** Settings → Privacy & security → **Recall & snapshots** → **Websites to filter** → **Add website**. Policy: `SetDenyUriListForRecall` (semicolon-separated URIs including scheme, e.g. `https://www.Contoso.com;https://www.WoodgroveBank.com`).
- **Default:** **Empty**, with these built-in exceptions: private/incognito browsing is filtered by default in supported browsers, and browser-local pages (`edge://`, `chrome://`) are filtered by default. Site-specific filtering works in **Microsoft Edge, Firefox, Opera, Google Chrome**; *"For Chromium-based browsers not listed, filters private browsing activity only, doesn't filter specific websites."* *"You'll need to use a supported browser for filtering websites."*
- **Exposes:** Microsoft names the leak paths explicitly: *"websites are filtered when they are in the foreground or are in the currently opened tab of a supported browser. Parts of filtered websites can still appear in snapshots such as embedded content, the browser's history, or an opened tab that isn't in the foreground."* And *"Filtering doesn't prevent browsers, internet service providers (ISPs), websites, organizations, or others from knowing that the website was accessed and building a history."* Matching is inclusive: adding `https://www.WoodgroveBank.com` also filters `https://Account.WoodgroveBank.com` and `.../Account`. Policy changes require a device restart.
- **Recommend:** Use a supported browser if you rely on this; add banking, health, webmail, HR and customer-portal domains. Do not treat it as a redaction guarantee — background tabs and embeds still land in snapshots. Policy version is **Enterprise/Education only**.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall ; https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Sensitive information filtering *(the consumer page renders it as **Sensitive information filter**)*
- **Where:** Settings → Privacy & security → **Recall & snapshots**
- **Default:** **On.** Verbatim: *"the **Sensitive information filtering** setting is enabled by default to help ensure your data's confidentiality."* The consumer page agrees: *"Sensitive information filtering setting, which is enabled by default, helps filter out snapshots when potentially sensitive information is detected—for example, passwords, credit cards, and more."* The exact string in the shipping Settings UI is `unresolved` — Microsoft's own pages use two spellings, and the 2024 architecture blog called it "sensitive content filtering."
- **Exposes:** When on, a snapshot is **not saved at all** if the on-device **Microsoft Classification Engine (MCE)** — *"the same technology leveraged by Microsoft Purview for detecting and labeling sensitive information"*, running on the NPU — detects a sensitive type. The published type list is large (credit cards, IBAN, SWIFT, "General Password", Azure connection strings and storage keys, plus national ID / driver's licence / tax numbers for many countries). Microsoft is blunt that this is a **storage** filter, not a processing filter: *"the sensitive information remains on the device at all times, regardless of whether the Sensitive information filtering setting is enabled or disabled."*
- **Recommend:** Leave **On**, but do not rely on it. It is pattern-matching: it will miss free-text secrets, handwritten notes, screenshots of secrets, and anything outside the published type list. The failure mode is silent.
- **Risk:** High (because the protection is partial and feels total)
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-recall ; https://learn.microsoft.com/en-us/windows/client-management/recall-sensitive-information-filtering ; https://support.microsoft.com/en-us/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15 — checked 2026-10-02
- **Confidence:** `verified` (default, mechanism, limits) / `unresolved` (exact UI string)

- **Setting:** Click to Do
- **Where:** Settings → Privacy & security → **Click to Do**. Launched by **Windows+Q** or **Windows+click**. Policy `DisableClickToDo` (Computer and User Configuration → Windows Components → Windows AI).
- **Default:** **On.** *"By default, Click to Do is enabled for users"* (policy default `0` = enabled).
- **Exposes:** On activation it screenshots the screen and analyzes it locally — *"Screenshot analysis is always performed locally on their device"* — and *"Click to Do ends when they exit it, and it can't take screenshots while closed."* Nothing leaves the device **until you pick an action**: "Search the web" sends the selection to Bing via Edge, "Visual search with Bing" sends the image to Bing, and app transfers drop a temp file in `C:\Users\{username}\AppData\Local\Temp`. Diagnostic data is collected regardless. Click to Do also runs **on top of Recall snapshots**.
- **Recommend:** Turn **Off** unless you use it — it's a standing screen-capture-and-analyze primitive bound to an easily-mistyped hotkey. Note the carve-out: *"The policy to manage Click to Do doesn't affect Click to Do in Recall."*
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/manage-click-to-do ; https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Experimental agentic features *(Copilot Actions on Windows)*
- **Where:** **Settings → System → AI components → Agent tools → Experimental agentic features** per Microsoft's Windows security book; Microsoft's consumer support page gives the shorter **Settings → System → AI Components → Experimental agentic features**. The two Microsoft pages disagree on whether "Agent tools" is an intermediate node. No documented deep link.
- **Default:** **Off.** *"Copilot Actions is disabled by default."* Enabling requires an **administrative** account and is **device-wide**: *"once enabled, it's enabled for all users on the device."* Currently Windows Insider / Copilot Labs preview.
- **Exposes:** Once on, Windows provisions separate standard **agent accounts**, creates an **agent workspace** (an isolated parallel desktop session), and grants agents read/write access to six known folders — **Documents, Downloads, Desktop, Music, Pictures, Videos** — plus anything readable by all accounts on the system. An agent then clicks, types and scrolls on your behalf using vision and reasoning.
- **Recommend:** Leave **Off**. Microsoft names cross-prompt injection as a live, unsolved risk class: *"malicious content embedded in UI elements or documents can override agent instructions, leading to unintended actions like data exfiltration or malware installation."* And the grant is device-wide for every profile, not just yours.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/security/book/operating-system-agentic-security ; https://support.microsoft.com/en-us/windows/ai/ai-features/experimental-agentic-features — checked 2026-10-02
- **Confidence:** `verified` (default, admin requirement, device scope, folder list) / `unresolved` (which click path ships)

- **Setting:** Files — **Allow Always** / **Ask every time** / **Never allow** *(per agent)*
- **Where:** Settings → System → AI Components → **Agents** → *[select agent]* → **Files**. Documented from build 26100.7344 and later.
- **Default:** `unresolved` — Microsoft's support page describes the six known folders as *"Granted by Default (when toggle enabled)"*, implying a permissive effective default, but does not state the per-agent control's own default.
- **Exposes:** At **Allow Always**, an agent reads and writes Documents/Downloads/Desktop/Pictures/Music/Videos whenever it decides it needs to, with no prompt.
- **Recommend:** If you run agents at all, set **Ask every time** per agent — the only setting that keeps a human in the loop on file access. **Never allow** for any agent you have not deliberately scoped.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/windows/ai/ai-features/experimental-agentic-features — checked 2026-10-02
- **Confidence:** `verified` (options, location) / `unresolved` (default)

- **Setting:** Agent consent duration — `AgentConsentDuration`
- **Where:** CSP `./Device/Vendor/MSFT/Policy/Config/WindowsAI/AgentConsentDuration`. Enterprise/Education/IoT; Insider Preview.
- **Default:** **720 hours (30 days).** *"This policy setting allows you to configure the duration (in hours) for which agent consent decisions remain valid before re-prompting the user. The default value is 720 hours (30 days). The minimum value is 1 hour and the maximum value is 8760 hours (1 year)."*
- **Exposes:** How long a user's "yes" to an agent stays valid. Thirty days is a long time for consent granted to a system Microsoft itself describes as vulnerable to prompt injection.
- **Recommend:** Shorten substantially — 24 hours or less — so consent is a recurring decision rather than a one-time one.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Settings agentic search experience — `DisableSettingsAgent`
- **Where:** GP Computer Configuration → Administrative Templates → Windows Components → Windows AI → **Disable Settings agentic search experience**. Enterprise/Education/IoT; Insider Preview. No consumer toggle verified.
- **Default:** **`0` = enabled.** *"Settings agentic experience enhances search results within the Settings app by enabling natural language. When activated, it utilizes an AI model to provide intelligent Settings search suggestions."*
- **Exposes:** Natural-language queries typed into Settings search are handled by an AI model. Whether those prompts leave the device is **not stated** in the CSP doc.
- **Recommend:** Set `1` on managed fleets until Microsoft documents where the prompts are processed.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai — checked 2026-10-02
- **Confidence:** `verified` (policy, default) / `unresolved` (data flow)

- **Setting:** Allow Recall to be enabled — `AllowRecallEnablement` *(cross-referenced here; full admin-plane entry in §8(c))*
- **Where:** GP **Windows Components → Windows AI → Allow Recall to be enabled**. CSP Device only. Pro/Enterprise/Education/IoT. Windows 11 24H2 + KB5055627 (10.0.26100.3915) and later.
- **Default:** **CONTRADICTION FLAGGED, NOT RESOLVED.** The CSP page lists **Default Value `1`** ("Recall is available") while the *same page's prose* says *"By default, Recall is disabled for managed commercial devices... If this policy isn't configured, end users will have the Recall component in a disabled state"*, and `manage-recall` says *"By default, Recall is disabled and removed on managed devices."*
- **Exposes:** Setting `0` removes the Recall bits and deletes existing snapshots (requires restart). To let users opt in at all, an admin must configure **both** this **and** `DisableAIDataAnalysis`.
- **Recommend:** Set explicitly to `0` on any managed fleet handling regulated data. Do not rely on the unconfigured state given the contradiction.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-windowsai ; https://learn.microsoft.com/en-us/windows/client-management/manage-recall — checked 2026-10-02
- **Confidence:** `verified` (mechanics) / `unresolved` (unconfigured default)

### (a) Consumer Copilot — agentic features

- **Setting:** Browse with Copilot *(Copilot Actions in Edge)*
- **Where:** In the Copilot text box, select **Browse with Copilot**, then enter your request. *"The tab where Copilot is working shows a cursor icon in the tab menu."*
- **Default:** For the consumer experience, the support page gives **no disable instructions** — only that Edge's enhanced security settings let you *"control site-level access."* Under enterprise policy `AllowBrowsingWithCopilot`: *"If you don't configure this policy, browsing with Copilot is **off by default**, and users can turn it on"*, it is *"available only to users with an active Microsoft 365 Copilot subscription"*, and it only works on domains in `BrowsingWithCopilotAllowList` — *"If no domains are configured in the allow list, browsing with Copilot is effectively disabled."*
- **Exposes:** *"Copilot captures screenshots of the webpage it's using solely to browse and act on your behalf"*, retained **up to 30 days**. Crucially: *"Copilot can access cookies, which means if you're already signed into a site that Copilot has access to, it will also be signed in automatically."* Limits that do hold: *"it does not have unrestricted access to all your data"*, *"it cannot access autofill data, saved passwords, or wallet information"*, and *"Any information you enter directly into a webpage... is not saved by Copilot, but it may be saved in Edge."* Copilot *"will ask for your attention and supervision for certain actions, such as buying an item, booking a reservation, sending an email, or deleting a calendar event."*
- **Recommend:** Treat cookie inheritance as the headline risk — the agent browses as your logged-in self. Sign out of sensitive sites before using it, or use a separate profile. On managed devices, configure a narrow allow-list rather than leaving it unconfigured.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/topic/copilot-actions-in-edge-5ed5e17e-42df-40a3-984a-20420eba86e2 ; https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies/allowbrowsingwithcopilot — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Copilot Tasks *(scheduled and one-shot autonomous tasks)*
- **Where:** The **Tasks** view in Copilot. Stop a running task with the **interrupt message** button; *"You can pause, turn off, or delete scheduled tasks"*, *"delete any Tasks stored memory"*, and *"unlink individual Connectors at any time."*
- **Default:** No tasks exist until you create one. Regular tasks *"run once and begin as soon as you submit your request"*; scheduled tasks *"run at a specific time or on a recurring schedule."*
- **Exposes:** *"Copilot may browse the web, navigate and interact with websites, generate or edit files, or use connected services you've authorized."* Data touched: screenshots of browser interactions (retained briefly, not used for training), **cookies (optional, encrypted, retained up to 30 days)**, task-specific memory for preferences and dates, and connectors to *"email or cloud storage"*. Stated limit: it *"does not store sensitive information such as passwords, credit card numbers, bank account details, or government ID numbers."* Approval is requested before *"Monetary transactions"*, *"Submitting personal information to external websites"*, *"Actions involving other people"*, and *"Account-altering actions"*.
- **Recommend:** Don't grant Tasks a connector you wouldn't grant a contractor. Delete Tasks stored memory and unlink connectors when a task is finished — the cookie retention window keeps your authenticated state for up to 30 days.
- **Risk:** High
- **Evidence:** https://support.microsoft.com/en-us/microsoft-copilot/using-copilot-tasks — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Scheduled prompts
- **Where:** Copilot; documented by Microsoft as an **optional connected experience**
- **Default:** Available where optional connected experiences are available (on by default in Office — §1(b)).
- **Exposes:** *"You can schedule Copilot prompts to run automatically at set times and frequencies. This experience relies on Microsoft Power Automate"* — so a recurring prompt runs through a separate Microsoft service with its own terms.
- **Recommend:** Know that a scheduled prompt is a Power Automate flow, not just a Copilot setting, when you inventory automation.
- **Risk:** Medium
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365-apps/privacy/optional-connected-experiences — checked 2026-10-02
- **Confidence:** `verified`

### (b) Microsoft Copilot (tenant) — agents and computer use

- **Setting:** Agents *(Data access)*
- **Where:** M365 admin center → **Copilot** → **Settings** → **Data access** → **Agents**; then **Manage all agents** → **Agents** → **All agents** (Agent Registry)
- **Default:** **Enabled.** *"The capability is enabled by default in all Microsoft Copilot licensed tenants."* Gated by approval for store agents; *"Microsoft Copilot only uses agents that are turned on by the user."*
- **Exposes:** When an agent is invoked, *"Microsoft Copilot generates a search query to send to the agent on the user's behalf. The query is based on the user's prompt, Copilot activity history, and data the user has access to in Microsoft 365."* So agents receive derived content from tenant data **and from memory**. Agent types in scope: *Published by your organization*, *Shared by creator*, *Microsoft agents*, *External partner agents*, and *Frontier agents* (including **App Builder** and **Workflows**).
- **Recommend:** Require review of *"the permissions and data access required by an agent as well as the agent's terms of use and privacy statement"* (visible in **Integrated apps**) before approving any agent. Know the exemption: *"Researcher and Analyst are part of the core Copilot chat experience and will not fall under any agent-related settings"* — they stay inside the M365 commercial boundary but are outside agent governance.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps ; https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-privacy — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Agent management rules
- **Where:** M365 admin center → **Agents** → **Settings** → **Agent management rules** → **Add rule**. Actions: *Install Microsoft agents*, *Reassign ownerless agents created with Agent Builder to manager*, *Block ownerless agents without usage*, *Apply template*, *Reject agent publish requests older than N days*.
- **Default:** No rules until you create them.
- **Exposes:** Nothing directly, but it addresses a real exposure: *"Agents become ownerless when their original creator leaves the organization. Administrators must currently identify and transfer ownership manually, which can result in lifecycle governance gaps."*
- **Recommend:** Create the ownerless-agent rules early — an ownerless agent holding standing data access is durable unmanaged privilege. Note *"The **Apply template** action is a one-time bulk operation. It isn't a scheduled rule"*, and the reassign rule *"only supports agents created by using Microsoft Copilot Agent Builder."*
- **Risk:** Low (the absence of rules is the risk)
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Credentials to use *(Copilot Studio computer use)*
- **Where:** Copilot Studio → agent → **Tools** → **Add tool** → **New tool** → **Computer use** → configuration page. Requires generative orchestration. Models available: OpenAI Computer-Using Agent (GA), Anthropic Claude Sonnet 4.5 (GA), Sonnet 4.6 (Experimental), Opus 4.6 (Premium, Experimental).
- **Default:** **Maker-provided credentials.** Verbatim: *"**Maker-provided credentials** (default): Use the maker's credentials. This option is suitable for autonomous agents."* With Microsoft's own warning: *"If you share an agent with this setting, **anyone using it can act with the original author's access** on the configured machine."*
- **Exposes:** A shared computer-use agent is a privilege-escalation primitive by default — every user of it operates as the maker on the target machine, driving a real mouse and keyboard across websites and desktop apps.
- **Recommend:** Use **End user credentials** for anything conversational or shared. Reserve maker credentials for genuinely autonomous agents on dedicated, least-privileged machines — Microsoft's own hardening list: *"Use dedicated machines for computer use"*, *"Limit permissions to the user account"*, *"Limit web access to an allow list"*, *"Limit specific desktop apps."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Access control *(computer use — allow list of websites and desktop apps)*
- **Where:** Copilot Studio → computer use tool configuration → **Access control**
- **Default:** **Unrestricted.** *"By default, computer use can operate on any website or application."*
- **Exposes:** At default the agent can act on anything reachable from that machine. And the control is weaker than it looks: *"Access control only prevents the model from taking actions on websites or applications that aren't in the allow list. **It doesn't stop the model from opening them.**"* Microsoft's example: with only microsoft.com and Edge allowed, *"the model can still use the Microsoft Edge search bar to open Bing."*
- **Recommend:** Always define an allow list, and back it with Intune Edge policy and Windows application control — Microsoft's own recommendation, precisely because the in-product list doesn't prevent navigation.
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use — checked 2026-10-02
- **Confidence:** `verified`

- **Setting:** Stored credentials *(computer use)* and Enforce HTTPS
- **Where:** Copilot Studio → computer use tool configuration → **Stored credentials** → *Internal storage* or *Azure Key Vault*; and the **Enforce HTTPS** toggle
- **Default:** Internal storage requires no preconfiguration — *"Power Platform encrypts and stores secrets internally."* **Enforce HTTPS** default is `unresolved` (described as something you *"Turn on"*).
- **Exposes:** Usernames and passwords for third-party websites and desktop apps, held so the agent can sign in autonomously, keyed by login domain (wildcards supported) or desktop app process name.
- **Recommend:** Use the **Azure Key Vault** option for anything beyond a demo — it gives rotation, access policy and audit that internal storage does not surface. Turn on **Enforce HTTPS**: *"When this setting is turned on, computer use doesn't interact with HTTP sites, helping protect against potential data exposure."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use — checked 2026-10-02
- **Confidence:** `verified` (mechanism, options) / `unresolved` (Enforce HTTPS default)

- **Setting:** Human supervision *(computer use)*
- **Where:** Copilot Studio → computer use tool configuration → **Human supervision** (email reviewer via Outlook + response time limit)
- **Default:** `unresolved`
- **Exposes:** The escalation path when *"the computer-use agent detects potentially harmful instructions that could alter model behavior"* — i.e. prompt injection against an agent holding a keyboard. Microsoft flags the design trap: *"If you choose a reviewer other than the person running the computer-use agent, they likely don't see the activity because they didn't initiate the run. Therefore, they can't properly verify or act on the request."*
- **Recommend:** Set the reviewer to the initiating user, not a generic security mailbox, or the supervision is theatre. On expiry *"the request expires, and the computer-use run stops if no response is received."*
- **Risk:** High
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use — checked 2026-10-02
- **Confidence:** `verified` (behavior) / `unresolved` (default)

### (d) GitHub Copilot — coding agent

- **Setting:** Repository access *(Copilot cloud agent)*
- **Where:** https://github.com/settings/copilot/coding_agent → **Repository access** dropdown → **No repositories** / **All repositories** / **Only selected repositories**
- **Default:** **All repositories.** *"Copilot cloud agent is enabled in all repositories by default."* Admin gate on Business/Enterprise: *"an administrator must enable the relevant policy before you can use the agent"*, and *"you can block Copilot cloud agent for all users in your enterprise's repositories."*
- **Exposes:** An autonomous agent with read/write reach across every repository your account can touch, running in *"its own ephemeral development environment, powered by GitHub Actions, where it can explore your code, make changes, execute automated tests and linters."* Its sessions are **shared by default** (§4(d)), and partner agents inherit this same repository scope (§3(d)). Whether it can trigger arbitrary workflows, and what repository secrets it can read, are **not documented** (`unresolved`).
- **Recommend:** Set to **Only selected repositories**. This single dropdown is the difference between "an agent can touch one project" and "an agent can touch everything I have access to."
- **Risk:** High
- **Evidence:** https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies ; https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent ; https://docs.github.com/en/copilot/concepts/enterprise/policies — checked 2026-10-02
- **Confidence:** `verified` (default, scope) / `unresolved` (secrets access, workflow triggering)

- **Setting:** Internet access *(the Copilot agent firewall)*
- **Where:** Organization: **Settings → Copilot → Internet access**. Repository: **Settings → Copilot → Internet access**.
- **Default:** **Firewall on, with a recommended allowlist enabled.** *"By default, Copilot's access to the internet is limited by a firewall."* The recommended allowlist covers *"Common operating system package repositories (for example, Debian, Ubuntu, Red Hat)"*, *"Common container registries (for example, Docker Hub, Azure Container Registry, AWS Elastic Container Registry)"*, *"Packages registries used by popular programming languages"*, *"Common certificate authorities (to allow SSL certificates to be validated)"*, and *"Hosts used to download web browsers for the Playwright MCP server."*
- **Exposes:** At default, the agent can reach every host on that allowlist — which includes package registries, a well-known exfiltration channel for an agent that has been prompt-injected.
- **Recommend:** Keep the firewall on and **narrow** the allowlist to the registries your build actually needs. Watch the PR for blocked-request warnings: *"If Copilot tries to make a request which is blocked by the firewall, a warning is added to the pull request body (for new pull requests) or to a comment (for existing pull requests). The warning shows the blocked address and the command that tried to make the request"* — those warnings are a signal worth reading, not noise.
- **Risk:** Medium
- **Evidence:** https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-the-firewall — checked 2026-10-02
- **Confidence:** `verified`

---

## Continued in two further files

This vendor baseline is split across three files to stay well inside the directory's per-file size
limit. Read them in order:

1. **`copilot.md`** (this file) — framing notes and categories 1–7.
2. **[`copilot-admin-api-mobile.md`](copilot-admin-api-mobile.md)** — category 8 (admin / workspace
   plane, incl. the Edge policies and the Windows locked-vs-defaulted analysis), category 9 (API /
   developer plane), category 10 (mobile & OS permissions), **the ten defaults most likely to surprise
   you**, and **Volatile**.
3. **[`copilot-second-pass.md`](copilot-second-pass.md)** — the 2026-10-02 gap-fill: what closed, what
   did not, the method constraint that bounds every `unresolved` label, and one correction to the
   ten-defaults list.

