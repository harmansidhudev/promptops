---
name: prompt-quality-check
description: "Spots weak prompts while you write them. Fires when editing system prompts, CLAUDE.md, agent definitions, skill files, or anything with template variables and LLM instructions. One-line fix — only when it matters. Silent when solid."
---

When the user is writing/editing a prompt (system prompt, CLAUDE.md, agent, skill, or file with {{variables}} or "You are a..." patterns), check for:

1. Missing output format
2. No "Do NOT" guardrails
3. Vague instructions
4. No edge case handling

If you find something, give ONE suggestion:

💡 **Prompt tip:** Add an output schema — `"Respond in JSON: {field: type}"`

Rules: one line max, include the actual fix text, silence means approval, don't repeat, don't interrupt mid-thought.
