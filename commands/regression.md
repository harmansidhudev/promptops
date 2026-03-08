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
4. **If $ARGUMENTS is empty** — check `.promptops/improved/` for the latest improved file and `.promptops/evals/` for the latest eval file. Use those as Version B and Version A respectively.
5. **If still nothing found** — reply: "Paste both versions:\n\n**Version A:** old prompt\n\n**Version B:** new prompt"

## Golden dataset validation

After scoring both versions, check if `.promptops/datasets/captured.json` exists and contains test cases.

If test cases exist:
1. Run **both** prompt versions against each test case input
2. Compare each output to the golden (expected) output
3. Use semantic similarity — outputs don't need to be identical, but must convey the same meaning and include the same key information
4. Add a **Test Results** section to the report (see format below)

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

### 🧪 Golden Dataset Results

*(Only show this section if `.promptops/datasets/captured.json` exists with test cases.)*

| # | Input (first 60 chars) | Version A | Version B | Winner |
|---|---|---|---|---|
| 1 | "Summarize this art..." | ✅ Match | ✅ Match | Tie |
| 2 | "Extract the names..." | ✅ Match | ⚠️ Partial | A |
| 3 | "Classify this feed..." | ❌ Miss | ✅ Match | B |

**Version A:** X/N passed · **Version B:** X/N passed

*(If no test cases exist, show: "💡 No golden dataset found. Approve outputs during `/run` to build test cases automatically.")*

**Verdict:** One sentence overall assessment — now informed by both scoring AND empirical test results.

> Run `/run` to execute the winning version. Run `/test` to see full test details.

## Verdict logic

- **✅ Safe** — no regressions in scores AND no test case regressions
- **⚠️ Review** — minor regressions but overall better, or test results are mixed
- **🔴 Risky** — important constraints lost, overall score dropped, or test cases that passed on A now fail on B

## After responding

Save to `.promptops/regressions/regression-<timestamp>.md`. Create directory if needed.
