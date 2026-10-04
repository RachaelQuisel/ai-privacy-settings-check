# Microsoft Copilot — second pass, gap-fill 2026-10-02

> Continues [copilot.md](copilot.md) and [copilot-admin-api-mobile.md](copilot-admin-api-mobile.md).
> Read the **Method constraint** below before weighing any `unresolved` label in any of the three files.

The first pass left a list of `unresolved` items. This section records what a targeted second pass
resolved, what it could not, and one correction to a claim made above.

## Method constraint — read this before weighing any `unresolved` below

Both gap-fill passes ran with **zero WebSearch budget** (200/200 consumed). Three search substitutes
were tried and failed: DuckDuckGo served CAPTCHAs, Mojeek returned 403, and Bing's RSS mode silently
ignored quoted phrases and `site:` operators. What worked, and is worth reusing:

- Direct fetch of known primary URLs.
- **`support.microsoft.com/en-us/search?query=…`** — real ranked results; the single most useful
  channel for consumer Copilot and Windows docs.
- **`learn.microsoft.com/api/search?search=…&locale=en-us&$top=N`** — works, but fuzzy; does not
  honour exact phrases and does not index `support.microsoft.com`.

**Consequence: no third-party corroboration was possible.** Every `unresolved` in this section means
*"absent from Microsoft's or GitHub's own documentation, via the channels above"* — **not** "absent
from the internet." That is a narrower and more useful claim than it looks, but do not over-read it.

## What closed

**Verified:** `Import browser data` (off) · per-agent **Files** permission (off, and the whole agentic
feature is off by default and admin-only to enable) · **Recall is opt-in and off at retail**, with a
consent prompt at first launch, nothing captured if ignored, and a second Windows Hello gate · the
**Azure abuse-monitoring retention figure is genuinely no longer published** — the change-log entry
showing it was dropped in the June 2023 relocation was found, so it was removed rather than moved ·
**enterprise-policy lock semantics** · **GitHub Copilot retention is confirmed not disclosed** in its
documentation · a live URL for **Copilot audit-log coverage**, replacing the dead one.

**Verified negatives** — worth as much as a positive here: the `Text and image generation` permission
page is **absent from all three of Microsoft's canonical enumerations**, including the current
`ms-settings:` URI reference. The page is real and third-party-documented; Microsoft does not list it.

**Partial:** a Microsoft source for the **`Ask Copilot` taskbar toggle** does exist (an accessibility
page), so its *existence* upgrades `reported` → `verified` — **its shipped state remains undocumented.**

**Still open, and the priority order for a pass with real search budget:** `File Search and File Read`
default · Copilot Pages default link scope · the shipped state of the `Ask Copilot` toggle · the
per-app toggle half of the Graphics-capture pages · an explicit sentence for the voice-training
default. On that last one the default was **not** firmed up: Microsoft documents voice training with
opt-out framing, which implies on-by-default, but never states it — so it stays `reported` with the
inference flagged as inference.

## Corrections to carry forward

1. **`User access` vs `Agent and plugin access`** — corrected in the ten-defaults list above.
2. **Azure pages renamed and recanonicalized** to `/azure/foundry/…` under **"Microsoft Foundry"** /
   "Foundry Models sold by Azure". Older `/azure/ai-services/openai/…` citations are stale.
3. **A policy-layer default of `0` means "no admin override" — it is not the user-facing toggle's
   shipped position.** The two were kept separate rather than collapsed; collapsing them would have
   manufactured a default that does not exist.
4. **Canonical drift on learn.microsoft.com:** pages requested under `/en-us/copilot/microsoft-365/*`
   are served with canonical `/en-us/microsoft-365/copilot/*`. Cite the canonical form.

## Consumer Copilot, Windows and Azure

All items checked **2026-10-02**.

#### 1. `Training on voice conversations` — default

**Resolved default:** Not explicitly stated by Microsoft. Microsoft documents it as an
**opt-out** control, which implies **on by default**, but never says so in words.

The privacy-controls page names both siblings in the same breath, for all three surfaces, and
then applies a single opt-out sentence to both:

> "In Copilot for Windows or macOS: Select your profile icon, then select **Settings** >
> **Privacy** > **Training on conversation activity** and **Training on voice conversations**."
> […] "Opting out will exclude your future conversation activities from being used for training
> these AI models."

The Privacy FAQ frames training the same way, again without isolating voice:

> "Except for certain categories of users or users who have opted out, Microsoft uses data from
> Bing, MSN, Copilot, and interactions with ads on Microsoft for AI training."

Checked and found **silent** on the voice default: the Transparency Note, and the Microsoft
privacy statement (which only offers the generic "we may use your data to develop, train, and
fine-tune our AI models, including large language models (LLMs)").

**Evidence:**
- https://support.microsoft.com/en-us/microsoft-copilot/microsoft-copilot-privacy-controls — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- https://support.microsoft.com/en-us/privacy/microsoft-copilot/transparency-note — silent; checked 2026-10-02
- https://www.microsoft.com/en-us/privacy/privacystatement — silent; checked 2026-10-02

**Confidence:** `reported` — the opt-out framing is from a Microsoft primary source, but the
default state is inferred, not read. Do not promote to `verified` without an explicit sentence.

**What changes for a user:** Voice chats with Copilot are almost certainly feeding model training
until the user goes and switches it off, and it is a *separate* switch from the text-conversation
one — turning off conversation-activity training does not cover voice.

---

#### 2. `Import browser data` — default

**Resolved default:** **OFF.** The toggle appears as "Bring over your browsing data from
Microsoft Edge" and is off until the user turns it on.

A related, distinct mechanism on the same product is also opt-in — Edge **cookie** import at app
launch: "Every time you launch the Copilot app on Windows, it can import cookies stored in
Microsoft Edge to make your experience more personalized and helpful. **This works only when you
choose to allow it**."

**Evidence:**
- https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02

**Confidence:** `verified`

**What changes for a user:** Copilot does not pull Edge history/sign-in details/form data until the user
opts in — this is one of the few consumer Copilot switches that ships closed.

---

#### 3. `File Search and File Read` — default

**Resolved default:** `unresolved`.

Microsoft documents the setting's **existence and location** but states no default:

> "You can adjust permissions for what Copilot file search can access by going to
> **Account > Settings > File Search and File Read** and toggling the setting."

**What blocked it:** No Microsoft page states the shipped state. Tried: Getting started with
Copilot on Windows (names the setting, no default); both privacy-controls pages; the Privacy FAQ;
the screen-reader Copilot-settings page; and four `support.microsoft.com` searches including the
exact phrase `"File Search and File Read"` (3 results, all checked). With no WebSearch budget,
third-party screenshots/guides that might show the shipped position were unreachable.

Adjacent but **not** the same toggle — do not conflate: the Privacy FAQ says "Copilot shows files
you've recently opened on your device by referencing Recent Items in Windows," which indicates
recent-file *surfacing* is active, but says nothing about the File Search and File Read permission.

**Evidence:**
- https://support.microsoft.com/en-us/microsoft-copilot/getting-started-with-copilot-on-windows — checked 2026-10-02
- https://support.microsoft.com/en-us/search?query=%22File+Search+and+File+Read%22+Copilot — checked 2026-10-02

**Confidence:** `unresolved`

**What changes for a user:** Unknown whether Copilot can read local files out of the box; the
control exists at Account → Settings → File Search and File Read and should be checked manually.

---

#### 4. Copilot for Windows browsing-sync — default

**Resolved default:** **Off / opt-in** for the documented import paths; the broader
"sync everything" default is not stated.

Two separable things, and Microsoft is only explicit about the first two:

1. **Edge browser-data import toggle** — off by default (see item 2). `verified`
2. **Edge cookie import at launch** — "works only when you choose to allow it". `verified`
3. **Full browser-data sync** — "When you are signed in, Copilot provides an option to sync all
   your history, favorites, [sign-in details] and other browser data…" Described as an *option*; **no
   default state given.** `unresolved`

Getting started with Copilot on Windows mentions "you can sync [sign-in details] and form data so it's
easier to work within Copilot" and qualifies it "if you choose to enable it" — opt-in phrasing,
but still not an explicit default. "Browse with Copilot" documents what Copilot accesses
(screenshots, cookies, open tabs, site permissions) and states **no** defaults at all.

**Evidence:**
- https://support.microsoft.com/en-us/microsoft-copilot/privacy-faq-for-microsoft-copilot — checked 2026-10-02
- https://support.microsoft.com/en-us/privacy/microsoft-copilot/privacy-controls — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-copilot/getting-started-with-copilot-on-windows — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-copilot/browse-with-copilot — no defaults; checked 2026-10-02

**Confidence:** `reported` — opt-in framing is Microsoft-sourced and consistent across three
pages, but the full-sync default is never stated outright.

**What changes for a user:** Browser data does not flow into Copilot on Windows unless the user
accepts it, but the acceptance is solicited at app launch, so it is easy to grant by reflex.

---

#### 5. Copilot Pages — default sharing scope

**Resolved default:** `unresolved`. Microsoft documents **storage ownership** but never the
default audience.

The strongest fact available:

> "A Copilot Page is saved as a `.page` file in a new **user-owned** SharePoint Embedded container."

"User-owned container" implies creator-private until a link is handed out, and the sharing docs
only describe **Copy link** (shares the page in Loop) and **Copy component** (embeds it in
Microsoft 365 apps). But Microsoft never states the default link scope — specifically **not**
whether the generated link defaults to "People in <org> with the link" versus "Specific people",
which is the thing that actually matters.

**What blocked it:** Six Copilot Pages support articles all silent on default visibility
(how-it-works, share-a-page, FAQ, get-started, collaborate, identify-authors), plus two
`support.microsoft.com` searches and one Learn search that surfaced no admin-side doc. The Learn
search for the SharePoint Embedded container permissions model returned nothing relevant.

**Evidence:**
- https://support.microsoft.com/en-us/microsoft-365-copilot/frequently-asked-questions-about-microsoft-365-copilot-pages — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-365-copilot/share-a-microsoft-365-copilot-page — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-365-copilot/how-microsoft-365-copilot-pages-works — checked 2026-10-02

**Confidence:** `unresolved`

**What changes for a user:** A new Page is most likely private until shared, but the blast radius
of the share link — org-wide versus named people — is undocumented, so treat a shared Page as
potentially org-visible until verified in the UI.

---

#### 6. `Ask Copilot` taskbar toggle — Microsoft source?

**Resolved:** **A Microsoft source does exist** — upgrade the toggle's *existence* from
`reported` to `verified`. Its **shipped state remains undocumented.**

Microsoft's accessibility documentation names the control and places it in Taskbar settings:
an **"Ask Copilot" toggle button** under Taskbar settings. The same page also documents
"Customise Copilot key on keyboard" (options: Search, Microsoft Copilot, Custom, Copilot).
Neither carries a default.

Corroborating context from Getting started with Copilot on Windows: on new Windows 11 PCs the
Copilot app is "pinned to the taskbar or on the Start menu" — but that page does **not** mention
an "Ask Copilot" toggle at all, so it cannot settle the default.

**Evidence:**
- https://support.microsoft.com/en-us/accessibility/windows/copilot/use-a-screen-reader-to-manage-copilot-settings-in-windows — checked 2026-10-02
- https://support.microsoft.com/en-us/microsoft-copilot/getting-started-with-copilot-on-windows — checked 2026-10-02

**Confidence:** `verified` for the toggle's existence and location; `unresolved` for its default.

**What changes for a user:** The taskbar "Ask Copilot" entry point is a real, Microsoft-documented
switch the user can turn off in Taskbar settings — it is no longer a third-party-only claim.

---

#### 7. `Text and image generation` app-permission page — Microsoft source?

**Resolved:** **No Microsoft source exists** for this as a Windows app-permission page. This is a
positive finding, not merely a failed search — the page is absent from all three of Microsoft's
own canonical enumerations:

1. The authoritative `ms-settings:` URI reference (page `ms.date` **2026-09-26**, i.e. current)
   lists the complete **Privacy** table — ~40 entries from `privacy-accountinfo` through
   `privacy-voiceactivation`. There is **no** "Text and image generation" entry and **no**
   corresponding `ms-settings:` URI.
2. The support.microsoft.com **App permissions** article enumerates **32** permission categories
   (Account Info, App diagnostics, Bluetooth, Calendar, … File system, … Webcam, WiFi). "Text and
   image generation" is **not** among them.
3. "Change privacy settings in Windows" and "Exploring Windows Settings" never name it.

A `support.microsoft.com` search for the exact phrase `"Text and image generation"` returns only
four results, **all** about in-app image generation (Paint Image Creator, Copilot image
generation, Copilot in Word) — none about a Settings permission page. A Learn search for the
generative-AI app-permission concept returned nothing relevant.

**Evidence:**
- https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — full Privacy URI table, no such page; checked 2026-10-02
- https://support.microsoft.com/en-us/windows/apps/app-permissions — 32 categories, no such page; checked 2026-10-02
- https://support.microsoft.com/en-us/search?query=%22Text+and+image+generation%22 — checked 2026-10-02

**Confidence:** `reported` — the page itself stays third-party-only. The *absence* from
Microsoft's canonical lists is `verified`.

**What changes for a user:** Toggle labels and defaults for this page cannot be cited to
Microsoft; if it exists on a given build it is undocumented, so anything written about it must be
attributed to third-party observation.

---

#### 8. Per-agent `Files` permission default (Windows agent settings)

**Resolved default:** **OFF / prompt-gated by default**, and the whole feature is off by default
on top of that.

- Location: **Settings > System > AI Components > Agents** → select the agent → **Files** section.
- Scope: six known folders — **Documents, Downloads, Desktop, Videos, Pictures, Music**.
- Options: **"Allow Always"** · **"Ask every time"** · **"Never allow"**.
- Default: access is not pre-granted — "Windows will prompt you for permission to share files in
  these folders."
- Feature gate above it: **"The experimental agentic features setting is off by default."** And:
  "This setting can only be enabled by an administrative user of the device and once enabled,
  it's enabled for all users on the device including other administrators and standard users."

**Evidence:**
- https://support.microsoft.com/en-us/windows/ai/ai-features/experimental-agentic-features — checked 2026-10-02

**Confidence:** `verified`

**What changes for a user:** Agents reach personal folders only after an admin turns the feature
on *and* the user answers a prompt — but note the admin's switch flips it on for **every** account
on the device, including standard users.

---

#### 9. Defaults for three Windows app-permission pages

Settings page names are `verified` from the current `ms-settings:` URI reference:

| URI | Settings page |
|---|---|
| `ms-settings:privacy-graphicscaptureprogrammatic` | **Graphics** |
| `ms-settings:privacy-graphicscapturewithoutborder` | **Graphics** (same page) |
| `ms-settings:privacy-broadfilesystemaccess` | **File system** |

**(a) `privacy-broadfilesystemaccess` — Resolved default: OFF.** Explicit and dated:

> "In the April 2018 update, the default for the permission is On. **In the October 2018 update,
> the default is Off.**"

So: on by default in Windows 10 1803 only, off by default from 1809 onward. Same page notes the
permission is a *restricted* capability, that toggling it while an app runs forcibly terminates
the app, and that Store submissions declaring it need extra justification. The consumer-facing
"Windows file system access and privacy" article describes the master toggle but — notably —
**does not state the default**; only the developer doc does.

**(b) `privacy-graphicscaptureprogrammatic` — Resolved default: "user in control" at the policy
layer; the user-facing toggle default is `unresolved`.**

Policy CSP `LetAppsAccessGraphicsCaptureProgrammatic`: **Default Value `0`**, where
`0` = User in control, `1` = Force allow, `2` = Force deny. Description: "specifies whether
Windows apps can take screenshots of various windows or displays."

**(c) `privacy-graphicscapturewithoutborder` — same.** Policy CSP
`LetAppsAccessGraphicsCaptureWithoutBorder`: **Default Value `0`** (User in control).
Description: "specifies whether Windows apps can turn off the screenshot border."

Important distinction, and the reason (b) and (c) are not fully resolved: `0 / user in control`
is the **policy** default — it means no administrator override is applied — which is *not* the
same as the shipped position of the per-app toggle the user sees on the Graphics page. No
Microsoft page states that toggle's default. Policy CSP Privacy contains **no** broad-file-system
policy, so there is no policy-layer answer for (a) — the developer doc above is the only source.

Related current context worth carrying: Insider build 26340.9233 (21 Aug 2026) moved camera,
microphone and location to **per-desktop-app** permissions, where "Apps that haven't yet accessed
a resource prompt for permission the first time access is requested" — the same prompt-on-first-use
pattern, though that build note does not extend it to Graphics.

**Evidence:**
- https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings — page names; checked 2026-10-02
- https://learn.microsoft.com/en-us/windows/uwp/files/file-access-permissions — **redirect/canonical** to `/windows/apps/develop/files/file-access-permissions`; source of the April/October 2018 default statement; checked 2026-10-02
- https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-privacy — both graphics policy defaults; checked 2026-10-02
- https://support.microsoft.com/en-us/windows/privacy/windows-file-system-access-and-privacy — no default stated; checked 2026-10-02

**Confidence:** `verified` for the three page names and for the File system default (OFF since
1809); `verified` for both graphics **policy** defaults; `unresolved` for the graphics per-app
**toggle** defaults.

**What changes for a user:** Apps cannot read the whole file system without an explicit grant on
modern Windows; for programmatic screen capture, Windows ships with no admin override, leaving the
decision to the user — but what that per-app switch reads as out of the box is undocumented.

---

#### 10. Is Recall opt-in or on at retail today?

**Resolved:** **Opt-in. Off at retail.** The user gets a consent prompt, and ignoring it leaves
Recall inert.

Direct from support.microsoft.com:

> "By default, saving snapshots for Recall aren't enabled. **You need to opt in to saving
> snapshots.**"

> "The first time you open Recall, you'll be asked if you want to allow snapshots to be saved."

> "Recall requires you to confirm your identity before it launches and before you can access your
> snapshots, so you'll also need to **enroll into Windows Hello** if you haven't already enrolled."

**Shipped retail behaviour on a current Copilot+ PC:**
- Snapshot saving is **off** out of the box.
- Consent is solicited at **first launch of Recall**, not during OOBE setup.
- **If the user ignores the prompt, nothing is captured** — no snapshots are saved, and the search
  and timeline surfaces stay empty. There is no silent-on path and no grace-period capture.
- Two gates, not one: the opt-in **and** Windows Hello enrollment. A user who declines Hello
  cannot reach snapshots even having opted in.

Per instructions, the two previously flagged documentation contradictions — CSP versus
`manage-recall` on `AllowRecallEnablement`, and on retention duration — were **not** investigated
and **stay flagged**. Nothing here bears on either.

**Evidence:**
- https://support.microsoft.com/en-us/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c — checked 2026-10-02

**Confidence:** `verified`

**What changes for a user:** A retail Copilot+ PC records nothing by default; Recall only starts
capturing after a deliberate opt-in plus biometric enrollment, so inaction is the safe state.

---

#### 11. Azure OpenAI / Azure AI Foundry abuse-monitoring retention period

**Resolved: the figure is no longer published.** Confirmed by reading both current canonical
pages end to end. **No retention duration appears anywhere** — not "30 days", not any other
number, on either page.

What the docs say *instead* of a duration — storage is described structurally and by access
control, never temporally:

- Human-review storage exists and is partitioned: "The abuse monitoring data store where prompts
  and completions are stored for human review is **logically separated by customer resource**…
  A separate data store is located in each geography…"
- Automated review stores nothing: "prompts and completions that undergo such review are **not
  stored** by the abuse monitoring system or used to train the AI model or other systems."
- Access is gated by SAWs and Just-In-Time manager approval; for EEA deployments, reviewers are
  EEA-located.
- Customers approved for **modified abuse monitoring** skip storage and human review entirely.
- Verification that logging is off is via the `ContentLogging` capability reading `false` in the
  Azure portal JSON view or `az cognitiveservices account show`.

Why the commonly-cited "30 days" has no current home: the data-privacy change log records, under
**23 June 2023**, "removed information about abuse monitoring which is now available at Azure
OpenAI Service abuse monitoring" — the content was relocated to the abuse-monitoring page, and
**that destination page carries no retention figure either**. The figure was dropped in the move,
not relocated. Neither page's later change-log entries (18 Nov 2024, 17 Dec 2024, 3 Oct 2025)
reintroduce one.

Collateral finding worth noting for any doc that cites these pages: the service has been
**renamed**. Both pages now canonicalize to `/azure/foundry/...` (fetched via the older
`/azure/ai-foundry/...` paths, which still serve content), the product is "**Microsoft Foundry**",
and the subject is "**Foundry Models sold by Azure**" rather than "Azure OpenAI Service". Page
dates: data-privacy `ms.date` 2026-05-18, abuse-monitoring `ms.date` 2026-05-13.

**Evidence:**
- https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy — **canonical now** `/azure/foundry/responsible-ai/openai/data-privacy`; checked 2026-10-02
- https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring — **canonical now** `/azure/foundry/openai/concepts/abuse-monitoring`; checked 2026-10-02

**Confidence:** `verified` — verified as a negative: the absence was read directly off both
current primary sources, including the change-log entry that explains the removal.

**What changes for a user:** No one can state how long Azure retains flagged prompts and
completions for human review; "30 days" should be struck from any current writeup, and the honest
line is that Microsoft documents the storage's isolation and access controls but not its lifetime.

---

#### Carry-forward for the next pass

Retry with real WebSearch budget, in priority order:

1. **Item 3** (`File Search and File Read` default) — highest value, cleanest question.
2. **Item 5** (Copilot Pages default link scope: org-wide vs specific people).
3. **Item 6** (shipped state of the now-confirmed `Ask Copilot` taskbar toggle).
4. **Item 9(b)(c)** (per-app toggle default on the Graphics page, as distinct from policy `0`).
5. **Item 1** (an explicit sentence for the voice-training default, to promote `reported` → `verified`).

Items **2, 8, 10, 11** are closed and `verified`. Item **7** is closed as a documented negative.

## Tenant plane and GitHub Copilot

Scope: only the 15 items left `unresolved` by the prior pass. All evidence `checked 2026-10-02`.
Search budget note: the WebSearch budget for this session was already exhausted (200/200) before work
began, so every page below was reached by direct URL on learn.microsoft.com / docs.github.com. Where a
default is marked `unresolved`, it means I read the authoritative page and the default is not stated —
not that I ran out of attempts.

Label key: **verified** = read on learn.microsoft.com or docs.github.com. **reported** = third-party or
inferred from primary wording without an explicit statement.

---

#### Microsoft 365 / Copilot tenant admin plane

##### 1. Self-service purchases (Copilot licences)
- **Resolved default:** **Enabled (allowed)**. Verbatim: "By default, all new products are set to allow
  users to make a self-service purchase." Microsoft Copilot is an in-scope product — `ProductId`
  **CFQ7TTC0MM8R**. Admin-center equivalent (Copilot > Settings > User access > *Microsoft Copilot
  self-service purchases*) offers **Allow** / **Allow trials only** / **Do not allow**.
- **Lockable?** Yes, but **per product only** — there is no single tenant kill switch. Verbatim:
  "Self-service purchases and trials can't be completely turned off at the tenant level with a single
  command. The **AllowSelfServicePurchase** policy is managed on a per-product basis. You can only turn
  off self-services purchases and trials for the entire tenant by turning off each product
  individually." Requires Global or Billing Administrator (Global Reader for read-only). Changing it is
  not retroactive: "Changing the value ... only impacts trials or purchases made for the specified
  product from that point forward."
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/commerce/subscriptions/allowselfservicepurchase-powershell
  (ms.date 2025-05-02, updated 2026-08-18) · https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page
  (updated 2026-09-28) · checked 2026-10-02.
  Oddity worth knowing: the PowerShell page ships `ROBOTS: NOINDEX, NOFOLLOW`, so it will not surface in
  search engines — reachable only by direct link.
- **Confidence:** High (verified).
- **For an admin:** Users can buy Copilot on your tenant today unless you explicitly set the Copilot
  product to `Disabled` (or `OnlyTrialsWithoutPaymentMethod`); doing it once per product is the only way
  to get tenant-wide coverage, and new products Microsoft adds later arrive allowed again.

##### 2. Agent and plugin access vs. "User access" default — **PRIOR FINDING NEEDS CORRECTING**
- **Resolved default:** The "All users is the default" claim is **true of the `User access` setting, not
  of `Agent and plugin access`** — they are two different settings on the same M365 admin center page
  (Agents > Settings).
  - **User access** — verbatim: "**All users** - This option is the default. It means that all users in
    the organization can access agents and plugins, subject to the existing app policies and user
    assignments." Other options: **No users**, **Specific users or groups**.
  - **Agent and plugin access** — three independent allow switches, **no default stated anywhere on the
    page**: "Allow agents and plugins built by Microsoft", "Allow agents and plugins built by your
    organization", "Allow agents and plugins built by external publishers". Its default is `unresolved`;
    the only adjacent default statement is on the agent-management article: "The capability is enabled by
    default in all Microsoft Copilot licensed tenants."
- **Lockable?** Yes — both are tenant settings set by an admin; users cannot override. One leak documented
  for Agent and plugin access: "Users see agents and plugins built by Microsoft even if you disable the
  setting, but they can't install those agents and plugins." Plugins explicitly include "tools, MCP
  servers, connectors, skills, and other AI artifacts."
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings (ms.date
  2026-09-03, updated 2026-09-30) · https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps
  (ms.date 2026-05-18) · checked 2026-10-02.
- **Confidence:** High for `User access` = All users (verified verbatim). `Agent and plugin access`
  default = unresolved.
- **For an admin:** Out of the box every licensed user can reach agents and plugins — including
  external-publisher agents and MCP servers — so the gate is one setting (`User access`) away from wide
  open, and the per-publisher gate (`Agent and plugin access`) has no documented shipped state to rely on.

##### 3. Sharing (tenant-level Copilot/agent sharing)
- **Resolved default:** `unresolved`. The page enumerates the options but never names a default:
  "**All users** - All users can share their agents with others in your tenant." / "**No users** -
  Disable sharing at the org level, but users can still share directly with specific individuals." /
  "**Specific users** - Restrict broad sharing permissions to designated groups." Also scoped: "Sharing
  control only applies to agents built with **Microsoft Copilot Agent Builder**."
- **Lockable?** **Only partially — and the doc says so.** Even at `No users`, "users can still share
  directly with specific individuals." So this setting cannot be used as a hard sharing block.
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings · checked
  2026-10-02.
- **Confidence:** High that the options and the `No users` carve-out are as quoted; default unresolved.
- **For an admin:** Treat this as a broad-distribution control, not a DLP control; person-to-person agent
  sharing survives the strictest setting, and anything not built in Copilot Agent Builder is out of scope
  entirely.

##### 4. Agent feedback sharing
- **Resolved default:** `unresolved`. Options only: **No agents** ("Developers don't receive feedback for
  any agents"), **All agents** ("Developers receive feedback for all agents"), **Selected agents**
  ("Developers receive feedback only for agents you select"). No shipped state documented.
- **Lockable?** Yes — tenant admin sets it at Agents > Settings > Agent feedback sharing; it is not a
  user-facing preference. Scope caveat, verbatim: "This setting doesn't affect whether people can rate
  agents or what data an agent can access."
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/admin/manage/agent-settings · checked
  2026-10-02.
- **Confidence:** High on options/lockability; default unresolved.
- **For an admin:** The question "do third-party agent developers currently see our users' thumbs-down
  comments?" cannot be answered from docs — you have to open the blade and read the tenant's current
  value.

##### 5. Advanced package uploads
- **Resolved default:** `unresolved`. Options only: **All users**, **No users**, **Specific users or
  groups**. Definition, verbatim: "An advanced agent is a package that uses either a Declarative Agent
  with actions or an MCP server. All other packages are considered basic... Basic package uploads remain
  allowed and aren't impacted. This setting only applies to user-uploaded packages by members of your
  organization and doesn't relate to Microsoft or third-party built agents."
- **Lockable?** Yes — admin-set, scoped to users/Entra ID groups. Note that the *basic* upload path
  (declarative agents, instructions only) is **not** governed by it at all.
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page
  (section "Advanced package uploads") · checked 2026-10-02.
  Minor doc inconsistency: this page puts the setting under the **Copilot actions** heading but gives the
  click path as **Copilot > Settings > All settings > Advanced package uploads**, while the agent-settings
  article routes all agent settings through **Agents > Settings**. Same setting, two documented paths.
- **Confidence:** High on semantics; default unresolved.
- **For an admin:** This is the MCP-server-sideloading control. Even locked down, users can still upload
  instruction-only declarative agents.

##### 6. Copilot diagnostics logs
- **Resolved default:** **Not a default-bearing toggle.** The documented feature is an admin *action*, not
  an on/off state: "If users encounter an issue and can't send Copilot feedback logs to Microsoft, you can
  submit feedback logs on their behalf. The data includes prompts and generated responses, relevant
  content samples, and log files." No shipped on/off state is documented, so any claim of a default here
  would be invented.
- **Lockable?** Not applicable as a user-override question — and note the inverse: using it **overrides
  the user's own policy**. Verbatim: "When you use this scenario to send feedback logs, it temporarily
  overrides any user level feedback policy." Path: Copilot > Settings > Other settings > Copilot
  diagnostics logs.
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page ·
  checked 2026-10-02.
- **Confidence:** High (verified) that it is an admin-initiated submission with a documented user-policy
  override; "default state" is the wrong frame for it.
- **For an admin:** This is a privacy-relevant admin capability — an admin can ship a user's prompts,
  Copilot responses and content samples to Microsoft even where the user's feedback policy says no.

##### 7. `-AllowTranscription` (Teams PowerShell) — **DOC CONTRADICTION, FLAGGED**
- **Resolved default:** **On / `$true` for new policies**, per the admin article: "Toggle
  **Transcription** **On** or **Off**. This setting is **On** by default for new policies."
- **Contradiction to report:** the cmdlet reference for the same parameter lists `Default value: None`
  in its parameter-properties table and gives no policy default — only "Set this to TRUE to allow. Set
  this to FALSE to prohibit." (This is PlatyPS boilerplate for "no value implied if omitted", but as
  written the two Microsoft pages do not agree on a documented default; I am reporting both rather than
  picking.) Adjacent, unambiguous values from the admin article: `-TranscriptionForWebinar` default
  *Enabled*; `-TranscriptionForTownhall` default *Enabled*; live captions default
  `DisabledUserOverride` ("**This value is the default setting.**").
- **Lockable?** Yes. It is a per-user *and* per-organizer policy; `Set-CsTeamsMeetingPolicy -Identity
  Global -AllowTranscription $false` applies to everyone without a custom policy and users cannot override
  it. Coupling worth noting: "When organizers turn off Microsoft Copilot in Teams meetings and events,
  recording and transcription are also turned off." Both the organizer and the person starting the
  transcript need it on.
- **Evidence:** https://learn.microsoft.com/en-us/microsoftteams/meeting-transcription-captions (ms.date
  2026-07-06) · https://learn.microsoft.com/en-us/powershell/module/microsoftteams/set-csteamsmeetingpolicy
  (ms.date 2025-07-13) · checked 2026-10-02.
- **Confidence:** High on the admin-center default (On for new policies); the cmdlet page's silence is the
  flagged inconsistency.
- **For an admin:** Assume transcripts are being produced unless you set the Global meeting policy to
  `$false` — and remember webinars and town halls have their own separately-defaulted-On parameters.

##### 8. Preview models
- **Resolved default:** **No single tenant-wide default exists; it is per-model, and "disabled by
  default" applies only to named subsets.** Verbatim: "Some preview models are disabled by default,
  including: Models with data retention by the provider [and] Certain models hosted and operated by
  Microsoft to preserve customer choice around available models." Hard defaults that *are* documented:
  - Anthropic models **with Data Retention**: "off by default for all scenarios, including in regions when
    different Anthropic models are on by default... No users will have access to these models until the
    tenant admin explicitly opts in."
  - Copilot Frontier (experimental/preview features and agents): "By default, no users have access to
    Frontier features"; "**No access**: No users can access Frontier features. This option is the
    default."
  - Standard (non-retention) Anthropic models: "Microsoft enables Anthropic models on by default for most
    customers in commercial cloud (excluding EU/EFTA and UK)"; EU/EFTA/UK default is **No users**.
- **Lockable?** Yes. Admins "Enable or disable preview models", "Restrict access to specific users or
  groups"; provider-level assignments are "applied at the provider level and enforced across Microsoft
  Copilot and Copilot Studio experiences." Requires AI Administrator or Global Administrator.
- **Evidence:** https://learn.microsoft.com/en-us/microsoft-365/copilot/manage-preview-ai-models (ms.date
  2026-09-01) · https://learn.microsoft.com/en-us/microsoft-365/copilot/connect-to-ai-subprocessor
  (ms.date 2026-09-18) · https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-page ·
  checked 2026-10-02.
- **Confidence:** High for the named cases; "the tenant default for preview models" as a single value is
  **unresolved by design** — Microsoft documents it per model class.
- **For an admin:** Do not audit this as one switch. Check three places: Frontier (off), AI providers
  operating as Microsoft subprocessors (Anthropic on by default outside EU/EFTA/UK), and the separate
  opt-in for Anthropic models with Data Retention (off, and takes you outside the Microsoft DPA —
  Anthropic stores most inputs/outputs up to 30 days, up to 2 years for flagged content).

##### 9. PPAC external-LLM setting
- **Resolved default:** Setting name is **"Enable External models"** (environment-level) with a matching
  **"External Models"** environment-group rule. **Default state is not stated on the PPAC page** →
  `unresolved` at the PPAC layer. What *is* documented is the gating chain: the M365 admin center must
  allow the provider first — "You must allow Anthropic access in the Microsoft 365 admin center, allow
  Mistral access in the Microsoft 365 admin center, and/or allow xAI access in Microsoft 365 admin
  center. If enabled there, you can access these settings in the Power Platform admin center." And: "If
  the external model toggle is visible but you can't select it, your organization's admin didn't enable
  access to that model family in the Microsoft 365 admin center." Providers covered: Anthropic, Mistral,
  xAI. Since 2026-01-07 Anthropic is a Microsoft subprocessor, so Product Terms + DPA apply to its use in
  Copilot Studio / Power Platform.
- **Lockable?** Yes, two ways: per environment (Settings > Product > Features) and, for managed
  environments in an environment group, the **External Models** rule — which must be published
  ("Publish rules") and then governs the environments in the group. The upstream M365 provider switch is
  the harder lock: turn the provider off there and the PPAC toggle is visible but unselectable.
- **Evidence:** https://learn.microsoft.com/en-us/power-platform/admin/allow-llm-generative-responses
  (ms.date 2026-05-28) · https://learn.microsoft.com/en-us/microsoft-365/copilot/connect-to-ai-subprocessor ·
  checked 2026-10-02.
- **Confidence:** High on name, scope and lock mechanics; **default unresolved** (the page describes how
  to "check or uncheck" without saying which ships checked). Inherited-default inference only: because
  Anthropic is on by default in commercial cloud outside EU/EFTA/UK, the provider gate upstream is open
  there — that is `reported`, not verified, for the PPAC toggle itself.
- **For an admin:** Exclusions matter more than the default here: Anthropic in Copilot Studio is outside
  EU Data Boundary commitments, xAI is US-tenant only, no FedRAMP for Anthropic or xAI in Copilot Studio,
  and PCI DSS is not applicable.

---

#### GitHub Copilot

##### 10. Individual-account "Suggestions matching public code" default
- **Resolved default:** `unresolved`. The individual-subscriber policy page describes the choice and both
  behaviours but never names a shipped value: "Your personal settings for GitHub Copilot include an option
  to either allow or block code suggestions that match publicly available code"; block mode checks "about
  150 characters against public code on GitHub." No "by default" sentence attaches to this setting.
- **What I tried:** (a) https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies —
  read in full, asked for every sentence containing "default"; only hits were the cloud-agent and
  web-search defaults (below). (b) The legacy path
  https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-policies-as-an-individual-subscriber
  — resolves (same-host redirect to the current page, no 404) and carries the same text, no default.
  (c) https://docs.github.com/en/copilot/reference/supported-surfaces-for-policies — lists the policy by
  name; "The document does not explicitly state default values for any of these policies."
- **Lockable?** Not applicable for a personal account (the user *is* the admin). For contrast, the only
  documented default for this setting anywhere is the Business one, which remains confirmed: "**Suggestions
  matching public code** is set to **Allowed** by default for Copilot Business users."
- **Evidence:** the three URLs above · checked 2026-10-02.
- **Confidence:** High that the individual default is **not disclosed** in GitHub's docs. Do not firm it
  up from the Business value.
- **For an admin:** For BYO-licence/Copilot Pro users you cannot cite a documented default — you have to
  have each user read their own setting, or push the Business/Enterprise policy instead.
- Useful adjacent individual defaults found on the same page (verified, verbatim): "Copilot cloud agent is
  enabled in all repositories by default, but you can block it from being used in repositories owned by
  your own personal account by changing your account settings"; and for web search in Copilot Chat, "This
  setting is disabled by default."

##### 11. Partner-agent default (third-party coding agents)
- **Resolved default:** **Off / opt-in — but `reported`, not verified**, because GitHub never writes
  "disabled by default." The wording is consistently permission-granting and action-required, at all three
  scopes:
  - Personal: "You can choose whether to allow the following coding agents to be enabled in your personal
    account: Anthropic Claude, OpenAI Codex... Installed agent apps also appear under 'Partner agents' and
    are enabled in the same way... under 'Partner agents', click the toggle to enable the third-party
    agent you want to use."
  - Organization: "You can choose whether to allow the following coding agents to be enabled in your
    organization: Anthropic Claude, OpenAI Codex" + the same toggle step under Settings > Copilot > Cloud
    agent.
  - Enterprise-owned orgs: "If the app is installed in an organization owned by an enterprise, an
    administrator must also enable the 'agent apps' Copilot policy before the agent features become
    available."
  Blast radius, verbatim: "Coding agents have access to the same repositories that Copilot cloud agent has
  been enabled in" — and cloud agent itself *is* enabled in all repositories by default.
- **Lockable?** Yes. Enterprise sets the `agent apps` policy; an org cannot override an enterprise-set
  policy (see item 15).
- **Caveat that could flip this:** GitHub's new **"Default policy for new features"** is itself enabled by
  default and "will start applying to new and existing GA features from October 22, 2026... If you don't
  take action, unconfigured features will be enabled on October 22." So an *unconfigured* partner-agent
  policy on Business/Enterprise may become enabled on that date without admin action. It "does **not**
  apply to features in preview."
- **Evidence:** https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies ·
  https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-organization/manage-policies ·
  https://docs.github.com/en/copilot/concepts/agents/agent-apps ·
  https://docs.github.com/en/copilot/concepts/enterprise/default-availability · checked 2026-10-02.
- **Confidence:** Medium (`reported`). Direction is unambiguous (a toggle you click to enable); the literal
  default sentence does not exist in the docs.
- **For an admin:** Decide the `agent apps` policy explicitly before 2026-10-22 rather than leaving it
  unconfigured, because unconfigured GA features are scheduled to flip on.

##### 12. GitHub Copilot retention periods — **CONFIRMED NOT DISCLOSED IN DOCS**
- **Resolved default:** `unresolved`, and the prior pass's conclusion is **confirmed and widened**: there
  is no Copilot-specific retention disclosure (no durations, no per-plan table) anywhere I could reach on
  docs.github.com.
- **What I tried, all checked 2026-10-02:**
  - https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/session-data —
    closest thing to a retention page. Gives storage *locations and lifetimes-by-location*, not periods:
    local sessions in `~/.copilot/session-state/` "until manually deleted"; "Synced session data is tied to
    your personal account and is accessible only to you by default"; "The environment is destroyed when
    the session ends, but the session log remains available on GitHub.com." No duration, no plan split.
  - https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement — no
    Copilot-specific retention statement; only the general "We'll retain your Personal Data as long as your
    account is active and as needed to fulfill contractual obligations, comply with legal requirements,
    resolve disputes, and enforce agreements."
  - https://docs.github.com/en/copilot/responsible-use/chat-in-github — no retention statement.
  - **404:** https://docs.github.com/en/site-policy/privacy-policies/github-copilot-privacy-statement
  - **404:** https://docs.github.com/en/site-policy/github-terms/github-copilot-product-specific-terms
  - https://copilot.github.trust.page/faq — returned only the "github.com Trust Center" shell (client-side
    rendered); no policy text retrievable via fetch. This is the one place likely to hold the numbers, and
    it is not a docs.github.com source, so anything from it would be `reported` at best.
- **Lockable?** N/A.
- **Confidence:** High that the disclosure is absent from the documentation set; the trust-center content
  remains unread (JS-only page), so "nowhere at all" is not provable.
- **For an admin:** You cannot answer a client's "how long does GitHub keep our prompts?" from GitHub's
  documentation. Route it to the Copilot Trust Center / your GitHub account team and get it in writing;
  treat any retention number circulating from blogs as unverified.

##### 13. Copilot audit-log coverage — live URL found (prior URL dead)
- **Resolved default (coverage, path, retention):**
  - Events covered, verbatim: "Changes to your Copilot plan, such as changes to settings and policies or a
    user losing or receiving a license", plus agent activity performed on GitHub's website.
  - Explicitly **not** covered, verbatim: the audit log "does **not** include client session data, such as
    the prompts a user sends to Copilot locally."
  - **Retention: "The audit log retains events for the last 180 days."**
  - Click path: navigate to your enterprise → settings (gear) icon → **Audit log**.
  - Event-schema reference for agent events:
    https://docs.github.com/en/copilot/reference/enterprise-administrators/agentic-audit-log-events
- **Live URL:** https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/review-audit-logs
  ("Check for changes to settings or licenses").
- **404s observed while locating it (all checked 2026-10-02):**
  https://docs.github.com/en/copilot/how-tos/administer/manage-for-enterprise/manage-policies ·
  https://docs.github.com/en/copilot/how-tos/administer/enterprises/manage-policies ·
  https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies **resolves** (live).
  Pattern: the `how-tos/administer/...` segment is dead; the live segment is
  `how-tos/administer-copilot/manage-for-enterprise/...`.
- **Lockable?** N/A (observability, not a policy).
- **Confidence:** High (verified).
- **For an admin:** The audit log answers "who changed Copilot policy / who holds a licence", on a rolling
  180-day window — it will never answer "what did someone paste into Copilot", so prompt-level forensics
  needs a different control.

##### 14. Cloud-agent sensitive values access
- **Resolved default:** **Deny by construction.** Only the **Agents**-type sensitive values and variables are
  visible to the Copilot cloud agent; verbatim: "Copilot cloud agent does not have access to GitHub
  Actions, Codespaces, or Dependabot [sensitive values] and variables." Agents-type values are "exposed to the agent
  as environment variables in its development environment." MCP servers read only values "prefixed with
  `COPILOT_MCP_`, which are only available to MCP servers." Migration note (the one way an org can have
  inherited exposure it did not re-consent to): "If you previously configured [sensitive values] or variables in the
  `copilot` environment in a repository's GitHub Actions settings, those [sensitive values] and variables have been
  automatically migrated to the new repository-level **Agents** type."
- **Lockable?** Effectively yes — nothing is readable unless someone explicitly creates it as an Agents
  sensitive value/variable; there is no blanket allow to turn off.
- **Evidence:** https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/configure-secrets-and-variables
  · checked 2026-10-02.
- **Confidence:** High (verified).
- **For an admin:** Audit the **Agents** sensitive value scope per repo (and anything auto-migrated out of the old
  `copilot` Actions environment) — that list *is* the agent's sign-in detail surface; your Actions and
  Dependabot sensitive values are out of reach.

##### 15. Enterprise-policy lock semantics — **RESOLVED**
- **Resolved default:** An organization **cannot** override a policy the enterprise has set. Verbatim from
  the org-side page: "If your enterprise owner has selected a specific policy... you cannot override that
  setting at the organization level." Enterprise owners choose between enforcing and delegating: "Enterprise
  owners can define a policy for the whole enterprise, or delegate the decision to individual organization
  owners" — the delegation value is **"Let organizations decide"**, and only then does the org setting
  apply: "At the organization level, it applies to features that an enterprise owner has set to **Let
  organizations decide**, but that an organization owner has not explicitly configured."
- **Combination rules (the part "enforcement options" never spelled out):** within one enterprise, where a
  user gets Copilot from several organizations, "the least restrictive policy usually applies"; across
  enterprises, "the most restrictive policy across enterprises almost always applies."
- **Lockable?** Yes — that is precisely the semantics: enterprise-set = locked downward; `Let organizations
  decide` = delegated.
- **Evidence:** https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-organization/manage-policies ·
  https://docs.github.com/en/copilot/concepts/enterprise/policies ·
  https://docs.github.com/en/copilot/concepts/enterprise/default-availability ·
  https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-enterprise-policies ·
  checked 2026-10-02.
- **Confidence:** High (verified) for the lock and the delegation value. Note the hedges in GitHub's own
  wording — "usually applies", "almost always applies" — so multi-org/multi-enterprise users are not
  deterministic from docs alone.
- **For an admin:** Set Copilot policy at the enterprise and it is a true lock for every org beneath it;
  leave it at "Let organizations decide" and each org sets its own — and for users who hold licences from
  several of your orgs, expect the *loosest* of those to win.

---

#### Cross-cutting flags

1. **Prior finding corrected (item 2):** "All users" is the documented default of **User access**, not of
   **Agent and plugin access**. The latter has no documented default.
2. **Microsoft self-contradiction (item 7):** `meeting-transcription-captions` says Transcription is "On by
   default for new policies"; the `Set-CsTeamsMeetingPolicy` reference for the same parameter says
   `Default value: None`. Reported, not adjudicated.
3. **Microsoft internal path inconsistency (item 5):** Advanced package uploads is documented under
   *Copilot actions* with a *Copilot > Settings > All settings* path, while every other agent setting is
   documented at *Agents > Settings*.
4. **Four M365/Copilot agent settings ship with no documented default** (items 3, 4, 5, plus the
   Agent-and-plugin-access half of item 2). For a privacy audit these must be read from the tenant, not
   asserted from docs.
5. **Dated change to watch (item 11):** GitHub's "Default policy for new features" is enabled by default
   and starts applying to new *and existing* GA features on **2026-10-22**; unconfigured features flip on.
6. **404s / redirects observed, all 2026-10-02:**
   - 404 `learn.microsoft.com/en-us/microsoft-365-copilot/microsoft-365-copilot-admin-settings`
   - 404 `learn.microsoft.com/en-us/copilot/microsoft-365/microsoft-365-copilot-admin-settings`
   - 404 `docs.github.com/en/copilot/how-tos/administer/manage-for-enterprise/manage-policies`
   - 404 `docs.github.com/en/copilot/how-tos/administer/enterprises/manage-policies`
   - 404 `docs.github.com/en/site-policy/privacy-policies/github-copilot-privacy-statement`
   - 404 `docs.github.com/en/site-policy/github-terms/github-copilot-product-specific-terms`
   - Redirect (same-host, content served): legacy
     `docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-policies-as-an-individual-subscriber`
     → current individual policy page.
   - Canonical drift on learn.microsoft.com: pages requested under `/en-us/copilot/microsoft-365/*` are
     served with canonical `/en-us/microsoft-365/copilot/*` (e.g. `microsoft-365-copilot-page`,
     `connect-to-ai-subprocessor`, `manage-preview-ai-models`). Cite the canonical form.
   - `copilot.github.trust.page/faq` returns a JS shell only — not fetchable as text.
