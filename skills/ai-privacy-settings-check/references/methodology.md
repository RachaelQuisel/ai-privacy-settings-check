# Methodology — rating findings and spotting dark patterns

> **Last verified:** 2026-10-02

## Evidence labels

Every finding carries one. They are not interchangeable and must never be blurred.

| Label | Means |
|---|---|
| `verified` | This specific account's setting was directly observed in a live read, on a stated date |
| `documented` | The vendor documents this default; this account was not read |
| `reported` | Only a third party claims it — journalism, community thread, vendor marketing |
| `unresolved` | Could not be determined. Say what blocked it |
| `contested` | Credible sources disagree. Give both readings |

Two more fields are required on every finding, because of dark pattern 6 below:

- `verified_on` — the date the toggle state was observed
- `recheck_after` — `verified_on` + 30 days, or the next app update, whichever comes sooner

And one discipline field:

- `policy_vs_practice` — whether the rating rests on what the vendor's policy *permits*, or on documented behavior. A finding whose severity derives only from permissive policy language must say so, and **must not** be escalated by overrides 1–5 below, which require a documented exposure path.

## Severity rubric

Designed to be computed, not argued. Five dimensions, each scored 0–3 from an explicit list. Sum, band, then apply overrides and caps. Range 0–15.

### S — Data sensitivity reachable *through this setting*

| S | Test |
|---|---|
| 0 | Telemetry, crash logs, feature-usage counters only |
| 1 | Behavioral/metadata: timestamps, prompt counts, device/locale, derived interests |
| 2 | Conversation content, uploaded files, or connected-document content |
| 3 | Special-category or regulated content: health, sexual, biometric, political/religious, children's data, sign-in details/sensitive values, or client-confidential material under a professional duty |

### X — Third-party exposure the setting permits

| X | Test |
|---|---|
| 0 | Stays on device, or inside the vendor with no human access |
| 1 | Vendor personnel or contracted processors may read it (human review) |
| 2 | Named third parties, subprocessors, or ad-selection systems |
| 3 | Open internet: publicly resolvable URL, search-indexable, or reachable by an arbitrary attacker |

### R — Recoverability after the fact

| R | Test |
|---|---|
| 0 | Flipping the setting ends the exposure; nothing persists |
| 1 | Reversible via a deletion request, with lag |
| 2 | Partially irreversible: copies retained on a separate clock, already human-reviewed, or already re-shared |
| 3 | Irreversible: incorporated into model weights, publicly indexed/cached/archived, or already exfiltrated |

### P — Scope of people affected

| P | Test |
|---|---|
| 0 | Account holder only |
| 1 | The account holder's named counterparties (people in the thread) |
| 2 | An entire workspace, tenant, or org |
| 3 | Non-users who never consented: meeting participants, email senders, people merely mentioned, minors |

### A — Activation / attack surface

| A | Test |
|---|---|
| 0 | Off by default; requires a deliberate per-use action |
| 1 | On by default, but exposure requires a user action |
| 2 | On by default and passive — exposure occurs with no further action |
| 3 | On by default, passive, **and** the lethal trifecta is complete: private-data access + untrusted-content exposure + an outbound channel |

### Banding

`TOTAL = S + X + R + P + A`

| Band | Rule |
|---|---|
| **High** | TOTAL ≥ 9, **or** any override fires |
| **Medium** | TOTAL 5–8 |
| **Low** | TOTAL ≤ 4 |

### Overrides — escalate to High regardless of total

1. **X = 3 and S ≥ 2** — conversation content reachable from the open internet. *The top realized-harm category: Grok share, ChatGPT discoverable chats, Meta AI Discover.*
2. **A = 3 and S ≥ 2** — trifecta complete over real content. *EchoLeak, AgentFlayer, Claudy Day.*
3. **R = 3 and S = 3** — special-category data in an irreversible sink.
4. **P = 3 and S ≥ 2** — content captured about people who never consented. *Otter.ai, Siri. Carries statutory wiretap / all-party-consent exposure, not only privacy exposure.*
5. **S = 3 and X ≥ 2** — regulated or sign-in detail data reaching third parties or ad systems.

### Caps — never rate above Medium

- **C1.** The data provably never leaves the device **and** no outbound channel exists (X = 0, A ≤ 2). Local-model and on-device findings land here. Caveat: local frontends often reintroduce cloud dependencies — update checks, embedding APIs, plugin systems. If any does, X ≠ 0 and the cap does not apply.
- **C2.** S = 0 (pure telemetry) — cap at **Low** absent an override.

### Worked examples

| Finding | S | X | R | P | A | Total | Band | Driver |
|---|---|---|---|---|---|---|---|---|
| A share link exists for a chat containing health details, and it resolves logged-out | 3 | 3 | 3 | 1 | 1 | **11** | High | Overrides 1, 3 |
| Consumer training toggle left on; general work conversations | 2 | 1 | 3 | 0 | 2 | **8** | Medium | No override fires. Irreversible but not third-party-exposed. **This is the honest rating — and the one most listicles get wrong in the High direction.** |
| Drive connector enabled while the assistant summarizes externally-supplied documents; Drive holds client files | 3 | 3 | 3 | 2 | 3 | **14** | High | Overrides 1, 2, 3, 5 |
| Ad personalization on, memory on, no sensitive content stored | 1 | 2 | 1 | 0 | 2 | **6** | Medium | Rises to High if memory holds S=3 material (override 5) |
| AI notetaker auto-joins meetings with external participants | 2 | 1 | 2 | 3 | 2 | **10** | High | Override 4 |
| Crash-telemetry sharing on | 0 | 2 | 1 | 0 | 2 | **5** | Low | Cap C2 |

## The dark-pattern catalog

Each entry: the pattern, a cited example, and the detection heuristic to apply.

### 1. Opt-out, not opt-in

Privacy-degrading processing starts on; the burden of refusal falls on the user.

**Example.** Slack analyzed messages, content and files to build ML models by default, with no opt-in, under terms applicable since at least Sept 2023 — [TechCrunch](https://techcrunch.com/2024/05/17/slack-under-attack-over-sneaky-ai-training-policy/), `reported`. Stanford's Jennifer King told the House Energy & Commerce Oversight Subcommittee: *"Users should not be automatically opted in to having their data used in model training"* — [written testimony](https://hai.stanford.edu/assets/files/testimony-safeguarding-data-privacy-and-well-being-for-ai-chatbot-users.pdf), `verified`.

**Heuristic.** Create a brand-new account on a clean device and record every privacy toggle's state *before touching anything*. Any privacy-degrading toggle reading "on" at t=0 is an opt-out finding. **Do not infer defaults from a long-lived account** — you cannot distinguish the default from the owner's past clicks.

### 2. Retroactive policy change with a short objection window

Data collected under promise A is relicensed for use B by amendment, with a deadline that converts inaction into consent.

**Regulator position.** FTC: *"It may be unfair or deceptive for a company to adopt more permissive data practices — for example, to start sharing consumers' data with third parties or using that data for AI training — and to only inform consumers of this change through a surreptitious, retroactive amendment to its terms of service or privacy policy"* — [FTC, 2024-02-13](https://www.ftc.gov/policy/advocacy-research/tech-at-ftc/2024/02/ai-other-companies-quietly-changing-your-terms-service-could-be-unfair-or-deceptive), `verified`.

**Practice.** Anthropic set a hard date of 2025-10-08 by which existing Free/Pro/Max users had to accept updated terms and make a training selection to keep using Claude — [Anthropic](https://www.anthropic.com/news/updates-to-our-consumer-terms), `verified`.

**Heuristic.** Diff the privacy policy and terms against the Internet Archive at 6-month intervals. Flag any clause whose effective date precedes the amendment date, and any consent flow whose only path to continued service is a button. Record whether refusal was offered as a coequal option or as an exit.

### 3. Bundled consent

One action grants several unrelated permissions, or a permission is granted at a level the affected person does not control.

**Examples.** Slack's opt-out was exercisable only by the workspace owner, via email — individual members could not opt themselves out ([The Register](https://www.theregister.com/2024/05/20/slack_ts_and_cs_update/), `reported`). Gemini's Android access to Phone/Messages/WhatsApp took effect *"whether your Gemini Apps Activity is on or off"* — the toggle a user would reach for does not govern the capability ([Malwarebytes](https://www.malwarebytes.com/blog/news/2025/07/no-thanks-google-lets-its-gemini-ai-access-your-apps-including-messages), `reported`).

**Heuristic.** For each privacy-relevant behavior, name the *one* control that governs it, then test it. If flipping that control does not change the behavior, or no per-user control exists, it is bundled. Count permissions granted per click; more than one is a finding.

### 4. "History off" ≠ "not retained"

A control named for visibility is read by users as a control over storage.

**Vendor's own words.** Google: with Keep Activity off, chats are *"retained with your account for 72 hours"*; human-reviewed chats are *"retained for up to three years"* and survive deletion of your activity — [Google](https://support.google.com/gemini/answer/13594961), `verified`. EFF states temporary and private modes *"do not mean the company doesn't store that data at all"* and that users should *"not think of it as private"* — [EFF Surveillance Self-Defense](https://ssd.eff.org/module/privacy-considerations-with-ai-tools), `verified`.

**Heuristic.** For each history / temporary / incognito control, locate the vendor's stated retention number for data covered by it. **If the vendor publishes no number, that absence is itself the finding.** Never accept the UI label as the retention policy.

### 5. Human-review clauses buried in sub-pages

The fact that employees or contractors read conversations lives in a help-center sub-page, not in the chat UI or the main policy.

**Example.** Google, in the Gemini Apps Privacy Hub rather than in the product: *"A subset of chats are reviewed by human reviewers (including Google's trained service providers)… Please don't enter confidential information that you wouldn't want a reviewer to see"* — [Google](https://support.google.com/gemini/answer/13594961), `verified`. Why it matters: Apple's USD 95 million Siri settlement concerned recordings shared with human reviewers.

**Heuristic.** Search the vendor's full documentation for `human review`, `reviewer`, `annotator`, `trained service providers`, `rater`. Then ask whether it is disclosed anywhere in the surface where a user actually types. **The distance in clicks between the input box and the disclosure is the measurable finding.**

### 6. Settings that silently re-enable after an update

A privacy setting reverts without user action, usually attributed to a migration or backend change.

**Status: `contested` and unreproduced.** A 487-point thread, *"Tell HN: OpenAI keeps re-enabling the 'allow training' setting"*, has the OP's dated notes and multiple corroborating commenters including one on Claude Code — but also commenters whose toggles stayed off indefinitely, and plausible benign explanations (migration bug, UI confusion) — [Hacker News](https://news.ycombinator.com/item?id=49643556), `contested`. **Do not state this as fact in either direction.**

**Heuristic.** This is the one pattern a single inspection cannot detect. Snapshot each toggle with a date stamp and re-verify after every app update and at a fixed cadence. An audit that checks once and declares a setting correct is making a claim it has not earned. *"Verified on date X"* is the only defensible phrasing — which is why `verified_on` and `recheck_after` are required fields.

### 7. Sharing features whose output is search-indexable

A "share" affordance users read as "send to one person" actually publishes to the open web — sometimes with no checkbox at all.

**Examples.** Grok's share generated a URL also exposed to Google, Bing and DuckDuckGo with no indication to the user (~370,000 conversations). ChatGPT's opt-in "Make this chat discoverable" checkbox still surfaced ~4,500 conversations. Meta AI had a Discover feed. All `reported` — see [evidence-base.md](evidence-base.md).

**Heuristic.** Generate a share link in a logged-out private window and confirm it loads. Run `site:<vendor-share-domain>` against Google and Bing. Check for `noindex` headers and `robots.txt` on the share path. Then **enumerate the account's existing share links** — exposure is cumulative and historical, not current-state.

### 8. Opt-out via a channel the product does not contain

The refusal mechanism lives outside the product: an email address, a web form, a separate privacy portal.

**Examples.** Slack's opt-out required emailing a specific address with a mandated subject line. OpenAI maintains both an in-app toggle and a separate privacy-portal request, which community commenters flagged as unnecessary complexity and which led some to conclude the in-app toggle alone is insufficient — [The Register](https://www.theregister.com/2024/05/20/slack_ts_and_cs_update/), [HN](https://news.ycombinator.com/item?id=49643556), `reported`.

**Heuristic.** Count the surfaces required to fully opt out. More than one is a finding, and each must be verified independently — **an auditor who flips the in-app toggle and stops has produced a false negative.**
