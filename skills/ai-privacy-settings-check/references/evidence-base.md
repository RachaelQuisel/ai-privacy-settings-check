# Evidence base — why the severity ratings are what they are

> **Last verified:** 2026-10-02. All URLs checked that date.

This file is what separates an audit from a listicle. It ranks categories by **realized** harm — documented incidents with identifiable victims — rather than by how much attention each gets, and it records the widely-repeated advice that does not hold up.

**Access caveat carried from research:** OpenAI's help pages, `openai.com/enterprise-privacy`, `searchengineland.com`, and `news.stanford.edu` returned HTTP 403 to automated fetch. Claims sourced only from search metadata rather than a read page are marked **[not directly read]** and downgraded to `reported` regardless of publisher authority.

## Risk model

Ranked by realized harm. Note throughout that **frequency of harm and irreversibility diverge sharply** — conflating them is the main way audit severity goes wrong.

### 1. Sharing & publication defaults — highest realized harm

The only category where hundreds of thousands of real, named-sensitive conversations are documented to have reached the open internet.

- xAI's Grok share button published conversations to search engines without telling users: **~370,000 conversations indexed**, including a user's name, personal details, at least one password, and uploaded files. `reported` — [Forbes](https://www.forbes.com/sites/iainmartin/2025/08/20/elon-musks-xai-published-hundreds-of-thousands-of-grok-chatbot-conversations/) **[not directly read]**, [Vice](https://www.vice.com/en/article/grok-chats-showing-up-google-search/) **[not directly read]**
- ChatGPT's "Make this chat discoverable" checkbox put shared chats into Google: **~4,500** found by `site:chatgpt.com/share` dorking, including mental-health and addiction disclosures. OpenAI disabled it 2025-07-31 and called it a "short-lived experiment." `reported` — [Bitdefender](https://www.bitdefender.com/en-us/blog/hotforsecurity/your-shared-chatgpt-chats-may-be-publicly-searchable-heres-how-to-delete-them), [MLQ](https://mlq.ai/news/chatgpt-removes-public-indexing-as-google-exposed-nearly-4500-shared-conversations/)
- Meta AI's Discover feed surfaced users' medical, legal and relationship prompts publicly. Meta's remediation was a pop-up warning — an admission the prior flow did not convey publication. `reported` — [eWeek](https://www.eweek.com/news/meta-ai-chats-public-sensitive-data-privacy/), [WinBuzzer](https://winbuzzer.com/2025/06/13/metas-ai-app-discover-feed-publicly-exposes-private-chats-without-users-knowing-xcxwbn/)

**Irreversibility: maximum.** Search caches, Archive.org and screenshots survive the vendor's fix.

### 2. Connectors & OAuth scopes — second-highest realized harm, largest blast radius

- **Salesloft Drift**: OAuth tokens stolen; UNC6395 queried and exported records from **700+ organizations** over ten days in Aug 2025, hunting AWS keys, passwords and Snowflake tokens. Victims included Cloudflare, Google, Palo Alto Networks, Proofpoint, Zscaler. `reported` — [Anomali](https://www.anomali.com/blog/salesloft-drift-breach-recap), [AppOmni](https://appomni.com/blog/drift-breach-salesforce-unc6395-saas-prevention/)
- **AgentFlayer**: uploading one poisoned document to ChatGPT caused it to search the victim's connected Google Drive for API keys and exfiltrate them via image-render URLs routed through Azure Blob storage, defeating OpenAI's `url_safe` check. Zenity: *"Any resource connected to ChatGPT can be targeted."* `verified` (primary researcher writeup, read directly) — [Zenity Labs, 2025-08-06](https://labs.zenity.io/post/agentflayer-chatgpt-connectors-0click-attack-5b41)

The distinguishing feature: **a connector converts "don't type secrets into the chatbot" from sound advice into irrelevant advice**, because the model fetches the secrets on your behalf.

### 3. Retention & deletion — high realized harm, and the category users most misjudge

- **DeepSeek** left two ClickHouse instances publicly queryable with no auth, exposing **1M+ log lines including plaintext user chat history and backend API keys**. Found by Wiz "within minutes." `reported` — [BleepingComputer](https://www.bleepingcomputer.com/news/security/deepseek-exposes-database-with-over-1-million-chat-records/), [The Hacker News](https://thehackernews.com/2025/01/deepseek-ai-database-exposed-over-1.html)
- **Legal hold beats the delete button.** A 2025-05-13 preservation order in *NYT v. OpenAI* required retaining output logs *"regardless of user deletion requests or privacy regulation requirements,"* affirmed on appeal 2025-06-26. `reported` — [The Cyber Express](https://thecyberexpress.com/openai-court-order-nyt-copyright-dispute/). Later reporting indicates the order was narrowed or lifted and that a separate production of ~20M de-identified conversations was ordered; **the post-June-2025 timeline is `contested` across sources and was not resolved** — [Yahoo/AP](https://www.yahoo.com/news/articles/judge-lifts-order-requiring-openai-151518813.html) **[not directly read]**
- Google documents that human-reviewed Gemini chats are **retained up to three years and survive your deletion of activity**, because they are disconnected from your account before review. `verified` (read directly) — [Gemini Apps Privacy Hub](https://support.google.com/gemini/answer/13594961)

### 4. Agentic & computer-use — rapidly rising; realized harm mostly in research, not yet confirmed victim counts

- **EchoLeak** (CVE-2025-32711, CVSS 9.3): zero-click indirect prompt injection in Microsoft 365 Copilot — one crafted email, no user interaction, organizational data exfiltrated. Patched June 2025; Microsoft reported no in-the-wild exploitation. `reported` — [HackTheBox](https://www.hackthebox.com/blog/cve-2025-32711-echoleak-copilot-vulnerability), [arXiv 2509.10540](https://arxiv.org/abs/2509.10540)
- **"Claudy Day"** (Oasis Security, March 2026): invisible HTML in a URL parameter pre-filled the claude.ai chat box, instructing Claude to search conversation history, write it to a file, and upload it via the Files API with an attacker-controlled key — against a **default, out-of-the-box session**. `reported` — [Oasis Security](https://www.oasis.security/blog/claude-ai-prompt-injection-data-exfiltration-vulnerability)
- Further 2025–26 classes: PromptJacking (RCE via Claude connectors), Claude pirate (Files API exfiltration), agent session smuggling. `reported` — [The Hacker News](https://thehackernews.com/2025/11/researchers-find-chatgpt.html), [PromptArmor](https://www.promptarmor.com/resources/claude-cowork-exfiltrates-files)

**The governing framework is practitioner-originated and now near-universal: the lethal trifecta** — private data access + exposure to untrusted content + an outbound channel. Operative advice: don't combine all three, and don't trust guardrail products claiming to let you. `verified` (primary, read directly) — [simonwillison.net, 2025-06-16](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/). SalesBleed/Agentforce is reported as the first real-world execution of the full pattern against an enterprise CRM agent — [Forkast](https://forkast.news/salesforce-agentforce-got-zero-clicked-through-its-own-web-form-and-the-attack-vector-is-in-every-agent-that-combines-these-three-things).

This framework is why dimension **A = 3** exists in the rubric.

### 5. Admin / workspace plane — moderate incident count, but a scope multiplier on everything above

One admin decision binds every employee, and the opt-out is often not self-service. Slack's global model opt-out required a workspace owner to **email a specific address with a mandated subject line**. `reported` — [TechCrunch](https://techcrunch.com/2024/05/17/slack-under-attack-over-sneaky-ai-training-policy/), [The Register](https://www.theregister.com/2024/05/20/slack_ts_and_cs_update/). The Drift breach is also fundamentally an admin-plane failure: a stale third-party OAuth grant nobody owned.

**Gap.** Microsoft 365 Copilot "oversharing via inherited SharePoint permissions" could not be verified against a primary Microsoft source. Widely asserted in vendor marketing; treat as **unverified** until confirmed against Microsoft Learn.

### 6. Voice / audio / camera — low frequency, but the only category with a large settled payout

- Apple agreed to **$95M** to settle claims that unintended Siri activations were recorded and extracts shared with human reviewers; class period 2014-09-17 to 2024-12-31. `reported` — [Courthouse News](https://www.courthousenews.com/judge-approves-95-million-apple-settlement-over-siri-privacy-case/)
- **Otter.ai** faces consolidated class actions (N.D. Cal., Aug–Sep 2025) alleging its notetaker recorded Zoom/Meet/Teams participants **who were not Otter accountholders** and used those recordings to train speech models, under ECPA and California law. `reported` — [NPR](https://www.npr.org/2025/08/15/g-s1-83087/otter-ai-transcription-class-action-lawsuit), [National Law Review](https://natlawreview.com/article/ai-notetaking-tools-under-fire-lessons-otterai-class-action-complaint)

This is the category that most reliably harms **non-users** — which is why it scores high on the rubric's P dimension even with few incidents.

### 7. Memory & history — few standalone incidents, but 2026 changed the stakes

Memory was a convenience feature with diffuse risk until it became an ad-targeting input. ChatGPT ads began 2026-02-09 for logged-in US Free/Go users, expanding to UK, Mexico, Brazil, Japan and South Korea by 2026-08-11, with memory feeding ad selection for users who have both settings on. `reported` — [OpenAI Help](https://help.openai.com/en/articles/20001047-ads-in-chatgpt) **[403, not directly read]**, [The Keyword](https://www.thekeyword.co/news/chatgpt-ads-personalization-memory)

**Whether ad personalization ships on by default is `contested`** — secondary coverage says OpenAI "enabled ad personalization as a default," but the primary page could not be read. **Auditors must check this toggle's live state rather than cite it.** OpenAI's stated position — chats, memories, email, precise location, IP and sensitive categories are not shared with advertisers, targeting happens internally — is a `verified` *policy claim* and is **not** evidence of what the pipeline does.

### 8. Training on your data — most-discussed, least-documented individual harm; near-maximal irreversibility

Where attention and realized harm diverge most, and an honest audit should say so. **No documented case was found** of an individual suffering a concrete, attributable harm from a frontier vendor training on their chat. What *is* documented:

- The EDPB holds that models trained on personal data **may themselves contain personal data** (memorization) and are not anonymous by nature; anonymity is a case-by-case assessment. `verified` — [EDPB Guidelines 02/2026 and 03/2026, adopted 2026-07-08](https://www.edpb.europa.eu/news/edpb-sheds-light-on-anonymisation-and-web-scraping-for-generative-ai-and-adopts-final-version_en) (read directly; consultation closed 2026-10-30)
- Regulatory harm is real: Garante fined OpenAI **€15M** for training without an adequate legal basis and for transparency failures. `verified as a fine issued` — [Portolano Cavallo](https://portolano.it/en/newsletter/portolano-cavallo-inform-digital-ip/chatgpt-italian-data-protection-authority-issued-15-million-euro-fine-prescribed-awareness-campaign). **But** one source reports the Court of Rome annulled it on 2026-03-18 on one-stop-shop jurisdictional grounds — `contested`, single source, [gdprfine.com](https://gdprfine.com/cases/openai-15-million-garante-2024)
- Irreversibility is the strongest argument for acting. ICO: people *"are unlikely to be able to revoke their consent if removing their data requires model re-training, which is currently an extremely cost and time intensive process."* `verified` (read directly) — [ICO](https://ico.org.uk/about-the-ico/what-we-do/our-work-on-artificial-intelligence/response-to-the-consultation-series-on-generative-ai/the-lawful-basis-for-web-scraping-to-train-generative-ai-models/)

**So: High on irreversibility, Low on observed frequency.** Both are true, and a rubric that sees only one produces bad findings. This is why the worked example rates a left-on training toggle **Medium**, not High.

### 9. Mobile & OS app permissions — low documented frontier-vendor harm; high documented harm in the long tail

- Google expanded Gemini's Android access to Phone, Messages, WhatsApp and Utilities from 2025-07-07 **regardless of whether Gemini Apps Activity is on or off**, with 72-hour retention even when off. `reported` for the change — [Malwarebytes](https://www.malwarebytes.com/blog/news/2025/07/no-thanks-google-lets-its-gemini-ai-access-your-apps-including-messages); the 72-hour figure is `verified` against [Google's own hub](https://support.google.com/gemini/answer/13594961)
- **Microsoft Recall** shipped intended-on, stored screenshots in an unencrypted database, and was reversed to opt-in after researcher and activist backlash; concerns persisted into 2025–26. `reported` — [The Record](https://therecord.media/microsoft-reverses-course-recall-opt-in), [GeekWire 2026](https://www.geekwire.com/2026/one-year-after-its-rocky-launch-microsofts-windows-recall-still-raises-security-red-flags/)
- Mozilla found **24,354 trackers in one minute** of use in the Romantic AI app, with data going to Facebook and ad networks; 10 of 11 romantic chatbots failed Mozilla's Minimum Security Standards. `verified` (Mozilla primary) — [Mozilla Foundation](https://www.mozillafoundation.org/en/blog/creepyexe-mozilla-urges-public-to-swipe-left-on-romantic-ai-chatbots-due-to-major-privacy-red-flags/). **Scope caveat: companion apps, not ChatGPT/Claude/Gemini.** See overstated advice #6.

### 10. API / developer plane — lowest realized consumer harm, most favorable defaults

Anthropic's consumer training change explicitly does **not** apply to Claude for Work, Government, Education, or API use via third parties. `verified` (read directly) — [Anthropic](https://www.anthropic.com/news/updates-to-our-consumer-terms).

**Gap:** `openai.com/enterprise-privacy` returned 403, so OpenAI's API default-no-training and zero-data-retention terms are **not asserted here**. Verify directly before putting them in a report. The residual API risk is credential hygiene, which DeepSeek demonstrated — the leaked logs contained backend API keys.

## Incident ledger

Each row: what happened, label, and **the specific control that would have prevented or limited it.**

| Date | Incident | Label | Preventing / limiting control |
|---|---|---|---|
| 2019→2025-01 | Apple Siri unintended activations recorded, extracts shared with human reviewers; **$95M settlement** | `reported` | "Improve Siri & Dictation" off; wake-word disabled; on-device-only processing |
| 2023-09→2024-05 | Slack analyzed messages/content/files for ML by default; opt-out required an org-owner email | `reported` | Workspace-level global model opt-out submitted, **with receipt retained as evidence** |
| 2024-06 | Microsoft Recall shipped intended-on with unencrypted screenshot DB; reversed to opt-in | `reported` | Recall off at OS level; group-policy disable in managed estates |
| 2024-09-18→20 | LinkedIn began training gen-AI on member data and enabled the setting globally **before** updating its terms; paused for UK/EEA/CH after ICO engagement | `reported` | "Data for Generative AI Improvement" off — note the window where no control existed in-region |
| 2024-02 | Mozilla: 10/11 romantic chatbots failed Minimum Security Standards; **24,354 trackers in 60 seconds** in Romantic AI; half blocked data deletion | `verified` | OS-level tracking/ad-ID denial; uninstall. These apps largely lacked usable controls — which *is* the finding |
| 2024-12-20 | Garante fined OpenAI **€15M** (legal basis + transparency), plus a mandated public-awareness campaign | `verified` (fine issued); annulment `contested` | N/A — regulator action. Cite for *legal-basis* severity, not user remediation |
| 2025-01-29 | DeepSeek left ClickHouse publicly queryable: **1M+ log lines, plaintext chat history, backend API keys** | `reported` | No user setting prevents this. Limiting: short retention tier, no history, vendor-risk exclusion |
| 2025-01-30 | Garante ordered DeepSeek blocked in Italy | `reported` | Vendor allow-listing at the org level |
| 2025-03-19 | noyb GDPR complaint over ChatGPT fabricating that a named man murdered his children, mixed with true personal details; no rectification offered | `reported` | **No setting fixes this.** Shows settings-only remediation has a hard ceiling |
| 2025-04→06 | Meta AI Discover feed published users' medical, legal and personal prompts; fix was a warning pop-up | `reported` | Never use the share/post affordance; audit and delete existing posts |
| 2025-05-13 | *NYT v. OpenAI* preservation order: retain output logs *"regardless of user deletion requests or privacy regulation requirements"* | `reported`; later timeline `contested` | **No consumer setting defeats a legal hold.** Limiting: contractual ZDR tiers, or not sending the data |
| 2025-06-11 | EchoLeak (CVE-2025-32711, CVSS 9.3): zero-click exfiltration in M365 Copilot via a single email | `reported` | Copilot scoped away from untrusted inbound content; outbound render/link egress blocked — break the trifecta |
| 2025-07-07 | Gemini gained Android Phone/Messages/WhatsApp access **irrespective of Gemini Apps Activity**; 72h retention even when off | `reported` / `verified` (72h) | Per-app Gemini connection toggles off; assistant disabled at OS level. **The Activity toggle is the wrong control here** |
| 2025-07-31 | ChatGPT shared-chat discoverability put ~4,500 conversations into Google | `reported` | "Make this chat discoverable" unchecked; periodic audit and revocation of **all existing** share links |
| 2025-08-06 | AgentFlayer: one poisoned doc → ChatGPT searched connected Drive for API keys → exfiltrated via Azure-Blob image URLs. Also reproduced against Copilot Studio, Cursor+Jira MCP, Salesforce Einstein, Gemini | `verified` (primary) | Drive connector disconnected; no connectors enabled while summarizing untrusted documents |
| 2025-08-09→17 | Salesloft Drift OAuth tokens stolen (UNC6395); records exported from **700+ organizations** | `reported` | Third-party OAuth grant inventory, least-privilege scopes, mandatory token rotation, removal of unused integrations |
| 2025-08-15→09 | Four class actions allege Otter recorded Zoom/Meet/Teams participants **who were not Otter users** and trained speech models on it | `reported` | Auto-join off; recording consent from all parties; training opt-out on the transcription vendor |
| 2025-08-20 | xAI Grok share URLs exposed to search engines with no user indication: **~370,000 conversations**, incl. names and at least one password | `reported` | **No setting existed.** Only control: never use share. Proves "there's a checkbox" is not a safety guarantee |
| 2025-08-18 | Texas AG issued CIDs to Meta and Character.AI over chatbots posing as mental-health providers while logging and exploiting interactions | `verified` (AG release) | Not a settings issue — cite for severity escalation on minors' and health data |
| 2025-05-19 | Garante fined Luka Inc. (Replika) **€5M** — no legal basis, no age verification | `reported` | Vendor exclusion; minors' access controls |
| 2025-10-08 | Anthropic deadline: Free/Pro/Max users had to accept new terms and choose training on/off; opting in extends retention 30 days → **5 years** | `verified` (primary) | "Help improve Claude" off before the deadline; re-verify after, per dark pattern 6 |
| 2025-11-18 | Jennifer King (Stanford) testified to House E&C: users should not be auto-enrolled; chatbots "can memorize training data"; platforms with existing profiles may fuse chat behavior into ad targeting | `verified` | Framing source for opt-in-by-default findings |
| 2026-02-09→08-11 | ChatGPT ads launched (US Free/Go), expanded to UK/MX/BR/JP/KR; memory can feed ad selection where both settings are on | `reported`; default-on `contested` | Ad personalization off; memory off or scoped; delete ad-related data |
| 2026-03 | "Claudy Day": invisible HTML in a chat-prefill URL → Claude searched conversation history → wrote to file → uploaded via Files API with attacker key, from a **default session** | `reported` | Conversation-history/search-past-chats off; file upload/egress restricted; don't open prefilled chat links |
| 2026-07-08 | EDPB adopted Guidelines **02/2026** (anonymisation) and **03/2026** (web scraping for gen-AI) — first comprehensive GDPR framework for scraping to train gen-AI | `verified` (primary) | Not a setting — the live standard against which vendor legal-basis claims should be assessed |

## Consensus recommendations

Settings nearly every credible source agrees you should change, with the dissent noted.

1. **Turn off model training / "improve the model" on every consumer tier.** EFF: *"Opt out of training whenever you can."* `verified` — [EFF](https://ssd.eff.org/module/privacy-considerations-with-ai-tools). *Dissent:* EFF itself cautions this is partial — "Don't Use This to Train AI" does not equal "Cannot Access Data," since retention, history, breach exposure and government requests persist. Nobody credible argues against doing it; several argue against overvaluing it.

2. **Never use share/publish features for anything sensitive — and audit links you already created.** Unanimous across the Grok, ChatGPT and Meta AI incidents. The only recommendation found with **zero dissent** and the strongest realized-harm backing. *Note:* remediation is not flipping a toggle, it is enumerating and revoking existing links, because exposure is historical.

3. **Treat "history off" / temporary / incognito as a reduction, never as non-retention.** Vendor-confirmed: Gemini 72 hours with Keep Activity off; ChatGPT and Claude 30 days for temporary chats; Google human-reviewed chats up to 3 years surviving deletion. `verified`. *Dissent:* EFF still recommends temporary chats on the grounds companies *"may use [them] less for training"* — use as a supplement, not a substitute.

4. **Do not grant connectors/OAuth scopes you do not need, and never assemble the lethal trifecta.** `verified` (primary) — [simonwillison.net](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/). *Dissent:* none on the principle. Real disagreement on whether *any* mitigation permits the combination — Willison says guardrail products are unreliable; vendors say defenses are improving. Treat vendor claims as `contested`.

5. **Turn off ad personalization wherever ads exist.** `verified` — EFF. Now load-bearing because of ChatGPT ads + memory integration. *Dissent:* OpenAI maintains advertisers never receive chats, memories, email, precise location, IP or sensitive categories. That is a policy commitment, not a documented practice; **both facts belong in a report.**

6. **Turn off or tightly scope memory / persistent personalization.** Consensus here is **weaker** than 1–5 and should be reported as such. The case strengthened in 2026 when memory became an ad-targeting input and Claudy Day showed conversation history is itself an exfiltration target. *Dissent:* EFF does not list memory-off among its core recommendations, and the utility cost is real. **Rate memory findings on what the memory contains, not on the existence of the feature.**

7. **Decline AI meeting recorders by default; obtain all-party consent before any.** Driven by Otter.ai and Siri — both turn on people who never agreed to anything. *Dissent:* none on the consent requirement; the open legal question is whether platform-level notice suffices.

8. **At the org level: set the workspace opt-out, inventory third-party OAuth grants, remove stale integrations.** Drift hit 700+ organizations through an integration most were not actively managing. *Dissent:* none.

9. **For genuinely sensitive work, move to a tier with contractual no-training and short retention.** `verified` — Anthropic's commercial tiers are excluded from the consumer change. *Dissent — important:* this addresses training and retention and does **nothing** about exfiltration. EchoLeak, AgentFlayer and Drift all landed on enterprise deployments. **"Upgrade to enterprise" is not a privacy answer, it is a training answer.**

10. **Use guest / accountless modes and minimize what you type.** EFF's first recommendation, alongside unique passwords, 2FA, and redacting personal information from uploaded files. *Dissent:* insufficient once connectors are live.

**Structural caveat every audit should carry.** US users have fewer rights than EU users on the identical product because there is no comprehensive US federal privacy law. `reported` — [IAPP](https://iapp.org/news/a/new-study-maps-the-privacy-gap-in-consumer-ai-and-proposes-a-fix). A settings-only audit cannot close that gap and should not imply it has.

## Things commonly recommended that are wrong or overstated

1. **"Turn off training and you're private."** — **Overstated.** EFF is blunt: "Don't Use This to Train AI" ≠ "Cannot Access Data." Even with training off, companies retain data for history and other purposes and remain exposed to breaches and government requests. Retention, human review and legal holds are *separate controls*; Google's human-reviewed chats persist up to three years past deletion. `verified`

2. **"Temporary / incognito chat means nothing is stored."** — **False.** Gemini 72 hours with Keep Activity off; ChatGPT and Claude 30 days. `verified`

3. **"Delete your chats and the data is gone."** — **False in at least two documented ways.** A preservation order required OpenAI to retain output logs regardless of deletion requests; Google states human-reviewed chats survive deletion for up to three years. `reported` / `verified`

4. **"Exercise your GDPR right to erasure and your data comes out of the model."** — **Overstated to the point of misleading.** ICO: revocation is unlikely where removal requires re-training. A paper titled, pointedly, *Machine Unlearning Doesn't Do What You Think* warns against treating unlearning as a reliable privacy remedy — `verified` (primary), [arXiv 2412.06966](https://arxiv.org/pdf/2412.06966). The strong form ("the right to be forgotten is dead") is `contested`. **What is actually true:** erasure requests reliably affect stored conversations; their effect on model weights is unproven and must never be asserted in a finding.

5. **"They sell your conversations to advertisers."** — **Not substantiated for the frontier vendors.** No documented instance of OpenAI, Anthropic or Google selling conversation content to third parties. **What is true, and different:** (a) ad targeting now happens *internally* using conversation and memory signals (ChatGPT, 2026); (b) King's testimony warns platforms with existing behavioral profiles may fuse chat signals into targeting — a prospective risk, not a documented practice; (c) third-party ad-tech data flows **are** documented — in companion apps, not frontier chatbots. Keep the policy/practice line visible.

6. **"Mozilla found 24,354 trackers in AI chatbots."** — **A category error, and a common one.** That finding is specific to the **Romantic AI** companion app, not ChatGPT, Claude or Gemini. `verified` — [Mozilla](https://www.mozillafoundation.org/en/blog/creepyexe-mozilla-urges-public-to-swipe-left-on-romantic-ai-chatbots-due-to-major-privacy-red-flags/). **Citing it against a frontier vendor is the fastest way to discredit an audit.**

7. **"Don't put sensitive information in prompts and you're covered."** — **Obsolete once connectors are enabled.** In AgentFlayer the victim typed nothing sensitive; they uploaded an innocuous document, asked for a summary, and the agent found API keys in their own Drive. `verified` (primary). Input hygiene is necessary and no longer sufficient.

8. **"Enterprise / Teams / Business tier means your data is safe."** — **Half right, and the wrong half is the dangerous one.** Correct on training. Wrong on exposure: EchoLeak hit M365 Copilot, AgentFlayer hit Copilot Studio and Salesforce Einstein, Drift exfiltrated from 700+ enterprise Salesforce orgs. Enterprise tiers buy contractual terms, not an absence of exfiltration paths.

9. **"Prompt injection is fixable with better system prompts or a guardrail product."** — **False per practitioner consensus.** Willison states guardrail products claiming to prevent trifecta attacks are unreliable, and that neither current design patterns nor emerging mitigations protect end users assembling their own tools. `verified` (primary). The only dependable individual-level control is capability separation.

10. **"Run a local model and you're fully private."** — **Directionally the strongest control available, routinely overstated.** Reported misconceptions: local frontends quietly reintroduce cloud dependencies (update checks, embedding APIs, plugin systems, optional analytics); "no internet = no risk" ignores malicious model files and plugins; "open source = safe" still requires code verification. `reported` only — community-sourced; **do not present as verified.**

11. **"A VPN or a burner email makes your chats private."** — **Wrong target.** The data at issue is the *content* you type while authenticated, which no network-layer control touches. EFF's actual version is **accountless/guest mode**, which removes account-linkage, not content. *The VPN critique is reasoning, not a cited claim — present it as such.*

12. **"The toggle you set stays set."** — **Unproven in both directions, which is why an audit must re-verify.** `contested`, unreproduced. **Do not state as fact either way.** The defensible output is a dated verification plus a re-check interval.

13. **"The €15M Garante fine proves OpenAI's training was unlawful."** — **Cite with care.** The fine was issued (`verified`), but one source reports annulment on jurisdictional grounds 2026-03-18 (`contested`, single source). Use it as evidence that regulators scrutinize legal basis, not as a settled holding.

## Claims that could not be substantiated — stated plainly

- **No documented case** of a frontier vendor's training opt-out being proven ineffective. The community reports concern the toggle's *persistence*, not its efficacy.
- **"At least two of six frontier developers do not allow opting out of model training at all"** — appears in summaries of Stanford/HAI work; the primary page returned 403, so the wording could not be confirmed and the two vendors are not named. The related framing — "every major provider now trains on consumer chat data by default" — is `reported` and should be scoped to **consumer tiers only**.
- **Whether ChatGPT ad personalization defaults to on.** `contested`; verify live.
- **Microsoft 365 Copilot permission-inheritance oversharing.** Widely asserted, not verified against a Microsoft primary source.
- **NIST AI 600-1** (Generative AI Profile) is cited via a secondary source; no canonical URL was confirmed. [AI RMF 1.0 / NIST AI 100-1](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf) is confirmed and names "privacy-enhanced" as a trustworthiness characteristic.
