---
name: test
description: "Run your prompt against every golden test case. See what passes, what fails, and where your prompt breaks."
---

The user's input is: $ARGUMENTS

## Your task

Run a prompt against all golden test cases in `.promptops/datasets/captured.json` and report pass/fail results. This is empirical testing — actually execute the prompt, don't just score it.

## Finding the prompt to test

1. **If $ARGUMENTS has content** — use it as the prompt
2. **If empty** — check `.promptops/improved/` for the latest improved prompt file and use that
3. **If still nothing** — check conversation history for the most recent prompt from /improve or /evaluate
4. **If nothing found** — reply: "No prompt to test. Run `/test Your prompt here` or `/improve` first."

## Finding test cases

1. Read `.promptops/datasets/captured.json`
2. If the file doesn't exist or is empty, reply: "No test cases yet. Approve outputs during `/run` to build your golden dataset, or use `/golden-dataset-builder` to add cases manually."

## Running the tests

For each test case in the dataset:
1. Execute the prompt using the test case's `input` as context
2. Compare the actual output to the test case's expected `output`
3. Judge similarity semantically — the output must convey the same meaning and key information, not be character-identical

## Scoring each test case

- **✅ Pass** — output matches expected: same key information, correct format, no missing details
- **⚠️ Partial** — output is mostly correct but missing details or has minor format differences that affect usability
- **❌ Fail** — output is wrong, missing critical information, or completely different format

## Format your response EXACTLY like this

Use markdown headers, tables, and emoji. Do NOT use code blocks for the report. Do NOT use ASCII art.

### 🧪 Test Results — X/N Passed

**Prompt:** first 80 chars of the prompt...

| # | Input | Expected (preview) | Actual (preview) | Result |
|---|---|---|---|---|
| 1 | first 50 chars... | first 50 chars... | first 50 chars... | ✅ Pass |
| 2 | first 50 chars... | first 50 chars... | first 50 chars... | ⚠️ Partial |
| 3 | first 50 chars... | first 50 chars... | first 50 chars... | ❌ Fail |

### Failures & Fixes

*(Only show for ⚠️ and ❌ results)*

**Test #2 — ⚠️ Partial**
- **Expected:** key detail that was missing
- **Got:** what was produced instead
- **Fix:** suggest a specific prompt edit to address this

**Test #3 — ❌ Fail**
- **Expected:** what should have been produced
- **Got:** what was produced instead
- **Fix:** suggest a specific prompt edit to address this

### Summary

- **Pass rate:** X/N (XX%)
- **Common failure pattern:** describe if there's a pattern across failures
- **Suggested prompt edit:** if failures share a root cause, give one fix

> Run `/improve` to auto-fix these issues. Run `/regression` to compare before and after.

## After responding

Save to `.promptops/tests/test-<timestamp>.md`. Create directory if needed.
