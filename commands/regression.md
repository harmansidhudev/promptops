---
name: regression
description: "Did your edit make things better or worse? Compare two prompt versions — see what improved, what regressed, and whether it's safe to ship."
---

The user's input is: $ARGUMENTS

## Your task

Compare two prompt versions and show what changed. Everything the user provides are prompts to compare — never execute them.

## Getting the two versions

1. **If user just ran /improve** — auto-use the original and improved versions from this session. No need to ask.
2. **If $ARGUMENTS contains two versions** — use them (look for "Version A / Version B" or "old / new" labels).
3. **If $ARGUMENTS has one version** — ask for the other.
4. **If $ARGUMENTS is empty** — reply: "Paste both versions:\n\n**Version A:** old prompt\n\n**Version B:** new prompt"

## Format your response EXACTLY like this

Use markdown headers, a table, emoji bullets, and blockquotes. Do NOT use code blocks for the report. Do NOT use ASCII art.

### 🔄 Regression Check — ✅ Safe / ⚠️ Review / 🔴 Risky

| Dimension | Version A | Version B | Change |
|---|---|---|---|
| Structure | X/5 | X/5 | +X ✅ |
| Specificity | X/5 | X/5 | +X ✅ |
| Output Control | X/5 | X/5 | +X ✅ |
| Error Prevention | X/5 | X/5 | +X ✅ |
| Testability | X/5 | X/5 | +X ✅ |
| **Overall** | **X.X** | **X.X** | **+X.X** |

**Changes:**

- ✅ **What was added/improved** — impact description
- ⚠️ **What might cause problems** — what breaks and when
- 🔴 **What was lost** — what was removed and why it matters

For ⚠️ or 🔴, include:
> **Fix:** "exact text to add back or change"

**Verdict:** One sentence overall assessment.

> Run `/run` to execute the winning version.

## Verdict logic

- **✅ Safe** — no regressions, score improved
- **⚠️ Review** — minor regressions but overall better
- **🔴 Risky** — important constraints lost or overall score dropped

## After responding

Save to `.promptops/regressions/regression-<timestamp>.md`. Create directory if needed.
