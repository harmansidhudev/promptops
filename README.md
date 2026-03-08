# PromptOps

**Evaluate, improve, test, and run your prompts — all in one session.**

## Commands

All commands accept inline input — type the command followed by your prompt text.

| Command | Usage |
|---|---|
| `/evaluate` | `/evaluate You are a code reviewer. Find bugs.` |
| `/improve` | `/improve You are a code reviewer. Find bugs.` |
| `/regression` | Auto-compares after `/improve`, or paste two versions |
| `/test` | Runs prompt against your golden dataset |
| `/compare` | `/compare You are a code reviewer. Find bugs.` |
| `/run` | Executes the best version from this session |

## The Loop

```
evaluate → improve → regression → test → run
```

Score it. Improve it. Verify nothing broke. Test against real cases. Run it.

## What Each Command Does

**`/evaluate`** — Honest 1-5 score across 5 dimensions (structure, specificity, output control, error prevention, testability). Top 3 issues with copy-paste fixes. Shows previous score if one exists.

**`/improve`** — Rewrites your prompt with schemas, guardrails, and no filler. Shows before/after score and what changed.

**`/regression`** — Side-by-side comparison of old vs new. Flags what improved (✅), what's risky (⚠️), and what regressed (🔴). Runs both versions against your golden dataset for empirical validation.

**`/test`** — Runs your prompt against every golden test case. Shows pass/fail results, failure patterns, and suggested fixes.

**`/compare`** — Benchmarks across Claude Opus/Sonnet/Haiku + GPT-4o. Shows per-run cost, daily cost, monthly cost with clear token assumptions. Supports custom pricing via config.

**`/run`** — Executes the improved prompt for real and delivers actual output. Works across sessions — finds your latest improved prompt from disk.

## Saved Outputs

Every command saves results to `.promptops/` in your project:

```
.promptops/
├── evals/
├── improved/
├── regressions/
├── tests/
├── comparisons/
├── datasets/        ← golden test cases
├── runs/
└── config.json      ← optional custom pricing
```

## Custom Pricing

Copy `config.example.json` to `.promptops/config.json` and update rates. The `/compare` command reads from this file, falling back to built-in defaults if it doesn't exist.

## Skills (Auto-Invoked)

- **prompt-quality-check** — One-line fix while you edit prompts. Silent when solid.
- **golden-dataset-builder** — Saves approved outputs as test cases over time.

## Installation

**Claude Code (recommended):**
```
/plugin install promptops@harmansidhudev/promptops
```

**Mac app:** Plugins → Add plugin → Upload plugin → select this folder

**Terminal:** `claude --plugin-dir /path/to/promptops`

## Author

**Harman Sidhu** — [harmansidhudev.com](https://harmansidhudev.com)
