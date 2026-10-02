# LLM Privacy Audit

A Claude Code plugin that reviews the privacy and permission settings on your AI assistant accounts and flags the defaults that expose more than you intended.

Most AI products ship permissive. Training on your conversations is frequently opt-out rather than opt-in, memory is on by default, connector grants are broader than the feature that requested them, and "turn off chat history" routinely does not mean "do not retain." This plugin inventories those settings, tells you which ones are costing you something, and gives you the exact path to each fix.

It is **read-only**. It reports and recommends. It never changes a setting on your behalf.

## What it covers

Ten categories per product:

1. Training on your data
2. Memory, history & personalization
3. Connectors & OAuth scopes
4. Sharing & publication defaults
5. Retention & deletion
6. Voice, audio & camera
7. Agentic / computer-use permissions
8. Admin / workspace plane
9. API / developer plane
10. Mobile & OS app permissions

Default product roster: **ChatGPT, Claude, Gemini, Grok** (including the separate X-side training toggle), **Microsoft Copilot, Meta AI**. The roster is a directory of files — add a vendor by adding one.

## How it works

Two layers, kept deliberately separate:

- **Documented baseline** — a dated, cited reference per vendor: every setting, its location, its out-of-box default, what it exposes, and the recommended state. No login required.
- **Live read** — optionally drives your own logged-in browser to each settings page and records what your account is *actually* set to.

Every finding is labeled with its confidence: `verified` (your account was read), `documented` (the vendor's default, your account was not read), `reported` (a third party claims it), or `unresolved` (could not be determined, and why). A failed read is reported as a failed read — never as the default, and never as "off."

## Install

```sh
/plugin marketplace add RachaelQuisel/llm-privacy-audit
/plugin install llm-privacy-audit
```

## Use

```
/privacy-audit                      # asks what to audit, offers the default roster
/privacy-audit chatgpt claude        # just those two
/privacy-audit all --baseline-only   # documented defaults only, no browser, no login
```

## Privacy of the audit itself

A completed audit lists which AI products you use, which third-party accounts they can reach, and where your configuration is weakest. Reports are masked by default, carry a confidentiality header, and are written locally. `reports/` is git-ignored and no real account data belongs in this repository.

## Running it for someone else

The person running the audit must be the account owner or be sitting with them. The plugin never asks for, accepts, or uses someone else's credentials. For a client engagement, either they run it on their machine, or they drive their browser while you read and record.

## Maintenance

These settings move. Each vendor file carries a `last verified` date, and the audit flags any baseline older than 90 days in its **Limits** section. Each vendor file also ends with a `Volatile` list — the settings most likely to have changed since, and the first place a maintainer should look.

## License

MIT © Rachael Quisel
