# Report template

Adapt the contents to what was actually audited. Keep the section order — readers learn it. Omit a section only when it would be empty, and say why.

---

> **Sensitive — handle as confidential.** This report describes the current security posture of the named accounts. Share it only with the account owner and anyone they explicitly designate. Do not paste it into a group chat, shared channel, ticket, or AI assistant.

# AI privacy audit — [subject] — [YYYY-MM-DD]

## Scope

- **Products audited:** [list, with plan tier for each]
- **Region:** [affects which defaults and rights apply]
- **Read method:** live read / documented baseline / both — per product
- **Audit date:** [YYYY-MM-DD]
- **Baseline last verified:** [date per vendor file; flag anything over 90 days old]
- **Not covered:** [products declined, categories out of scope, accounts not accessible]

## Summary

Three to five sentences. What is the overall exposure, what is the single most important thing to change, and is this account better or worse configured than the out-of-box default. No findings here — just the shape of the situation.

## Findings

Ranked by severity, highest first. Across products, not grouped by product — the owner wants to know what to fix first, not to read six vendor sections.

### [N]. [Setting] — [Product] — **[High/Medium/Low]** · *[verified/documented/reported/unresolved]*

- **Observed:** what state it is in, and how that was determined
- **Exposes:** what data flows where, concretely, while it stays this way
- **Recommend:** the target state
- **Fix:** the exact click path or URL
- **Evidence:** citation URL, plus the date checked
- **If unresolved:** what blocked the read and what the owner should check manually

## Already configured well

Short list. Settings that are at a privacy-protective state, whether by the owner's choice or because the vendor's default is sound. This section is not padding — it stops the owner from "fixing" something twice and tells them which vendors treated them decently.

## Manual annex — mobile and OS permissions

Cannot be read from a desktop. A checklist for the owner to walk on each device, with the per-OS path for each item.

## Limits

What would change these recommendations. Be specific:

- Baseline entries older than 90 days, named
- Products or categories that could not be read, and why
- Settings whose documented default is contested between credible sources
- Anything where vendor policy permits a practice that is not documented to occur — state which one you have evidence for

## Re-check

When to run this again, and what triggers an early re-run: a vendor policy change notice, a plan upgrade, a new connector grant, a new device, or a team member joining a workspace.
