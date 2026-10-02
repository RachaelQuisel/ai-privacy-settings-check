# LLM Privacy Audit

LLM Privacy Audit reviews the privacy settings on your AI accounts and tells you which
defaults are costing you something.

I built it because the honest answer to "is my ChatGPT training on my client work?" turned
out to be six answers, four of which had changed in the last year. ChatGPT's consumer
training toggle is on by default. Gemini's "Keep Activity" off switch doesn't stop retention,
human review, or four Android connectors that keep working regardless. Claude in Chrome was
documented to turn itself on for Enterprise tenants on a date that has already passed. None
of that is in a settings page you'd think to open.

The plugin returns findings. It doesn't change a setting, and it doesn't tell you that you're
fine.

## Install

```
/plugin marketplace add RachaelQuisel/llm-privacy-audit
/plugin install llm-privacy-audit
```

## Use

```
/privacy-audit                      # asks what to audit, offers the default roster
/privacy-audit chatgpt claude        # just those two
/privacy-audit all --baseline-only   # documented defaults only, no browser, no login
```

Or just ask: "audit my AI privacy settings," "what should I turn off in ChatGPT,"
"is Gemini training on my chats."

## What you get back

Findings, ranked by severity across all products at once — not grouped by vendor, because
you want to know what to fix first, not read six vendor sections.

Each finding carries five things:

- What state the setting is in, and **how that was determined**.
- What data flows where while it stays that way.
- The target state and the exact click path.
- A citation with the date it was checked.
- A severity score you can audit, not a vibe.

Here is [a full fictional example](skills/llm-privacy-audit/examples/sample-audit.md).

## The ten categories

| Category | What it covers |
|---|---|
| Training on your data | Model-training toggles, human review of conversations. |
| Memory, history & personalization | Persistent memory, chat history, cross-product personalization. |
| Connectors & OAuth scopes | What Gmail, Drive, Calendar and Slack grants can actually reach. |
| Sharing & publication defaults | Share links, search indexing, team visibility. |
| Retention & deletion | Post-deletion windows, temporary modes, the real delete path. |
| Voice, audio & camera | Usually a separate consent from text. Routinely missed. |
| Agentic / computer-use | Browser agents, site permissions, MCP servers, autonomous scopes. |
| Admin / workspace plane | The settings that override what members chose. |
| API / developer plane | Org retention, zero-data-retention, abuse logging. |
| Mobile & OS app permissions | Mic, photos, contacts, screen recording. Manual annex. |

Default roster: **ChatGPT, Claude, Gemini, Grok** (including the separate X-side training
toggle), **Microsoft Copilot, Meta AI**. The roster is a directory of files. Add a vendor by
adding one.

## Two things it gets right that most advice gets wrong

**Training toggles are over-rated.** There is no documented case of an individual suffering
an attributable harm from a frontier vendor training on their chat. Meanwhile Grok published
hundreds of thousands of conversations to search engines with no setting that would have
prevented it. The rubric rates a left-on training toggle **Medium** — irreversible, but not
third-party-exposed. That is the opposite of what most checklists say, and the worked
examples say so out loud.

**"Don't type secrets into the chatbot" stops working once connectors are on.** In the
AgentFlayer research the victim typed nothing sensitive. They uploaded an innocuous document,
asked for a summary, and the agent went and found API keys in their own Drive. So the audit
checks for the *lethal trifecta* — private data access, untrusted content, and an outbound
channel — as a finding in its own right, rated above any single toggle in the set.

## What it will not do

These are constraints written into the skill, not suggestions.

- It will not change a setting. Not a toggle, not a connector, not a deletion, not an
  objection form — even when the fix is obvious and you're watching. It hands you the path.
- It will not read a failed page as "off." A page that times out, hits an SSO wall, or
  renders blank is recorded as **unresolved**, with what blocked it. Absence is never
  evidence of a safe default.
- It will not state a default it did not verify. Each vendor file marks entries
  `verified`, `documented`, `reported`, `contested`, or `unresolved`, and several high-profile
  defaults are genuinely unresolved because the vendor doesn't publish them.
- It will not confuse policy with practice. A permissive privacy policy is evidence of
  permission, not of behaviour. The report says which one it has.
- It will not pretend a dated check is a standing fact. Every finding carries `verified_on`
  and `recheck_after`, because at least one vendor's toggle is credibly reported to
  re-enable itself and nobody has reproduced it either way.
- It will not ask for your credentials, or anyone else's. The person running it is the
  account owner or is sitting with them. For a client, they run it on their machine.

If a settings page or help doc contains text that reads like an instruction, the skill treats
it as content to report on. It does not follow it.

## What data it sends

None. The plugin is markdown and two small JSON manifests. It bundles no MCP servers, no
hooks, no agents, and no executable code. It has no endpoint of its own.

If you ask for a live read, Claude drives a browser you are already signed into, reads the
settings pages, and records what it saw. That happens in your session, on your machine. The
observations go into a report you choose where to save. `reports/` is git-ignored and no real
account data belongs in this repository.

## The report is itself sensitive

A completed audit lists which AI products you use, which third-party accounts they can reach,
and where your configuration is weakest. That is a useful document for you and a useful
document for an attacker. Reports mask account emails, workspace names and connected-account
identifiers by default, and carry a confidentiality header. Don't paste one into a group chat
— and specifically don't paste one into a chatbot whose retention settings it just criticised.

## Everything moves

These settings change constantly. Every vendor file carries a `last verified` date, and the
audit flags any baseline older than 90 days in its **Limits** section. Each file also ends
with a `Volatile` list — what changed in the last twelve months, what is most likely to move
next, and what could not be verified at all. That last list is the honest part: it names the
defaults the vendors don't publish, so you check them yourself instead of trusting a number
someone made up.

## License

MIT. See [LICENSE](LICENSE).
