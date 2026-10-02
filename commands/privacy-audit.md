---
description: Audit privacy and permission settings across AI assistant accounts and flag over-permissive defaults
argument-hint: "[products, or 'all'] [--baseline-only]"
---

Run the `llm-privacy-audit` skill.

Products in scope: $ARGUMENTS

If no products were named, ask which to audit and offer the default roster: ChatGPT, Claude, Gemini, Grok, Microsoft Copilot, Meta AI.

If `--baseline-only` is present, skip the live read entirely and produce the documented-baseline audit, noting in Limits that no account state was observed.
