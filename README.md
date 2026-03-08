# PromptOps

**Evaluate, improve, and run your prompts — all in one session.**

## Commands

All commands accept inline input — type the command followed by your prompt text.

| Command | Usage |
|---|---|
| `/evaluate` | `/evaluate You are a code reviewer. Find bugs.` |
| `/improve` | `/improve You are a code reviewer. Find bugs.` |
| `/regression` | Auto-compares after `/improve`, or paste two versions |
| `/compare` | `/compare You are a code reviewer. Find bugs.` |
| `/run` | Executes the best version from this session |

## The Loop

```
evaluate → improve → regression → run
```

Score it. Improve it. Verify nothing broke. Run it.

## What Each Command Does

**`/evaluate`** — Honest 1-5 score across 5 dimensions (structure, specificity, output control, error prevention, testability). Top 3 issues with copy-paste fixes.

**`/improve`** — Rewrites your prompt with schemas, guardrails, and no filler. Shows before/after score and what changed.

**`/regression`** — Side-by-side comparison of old vs new. Flags what improved (✅), what's risky (⚠️), and what regressed (🔴). Includes fixes for any regressions.

**`/compare`** — Benchmarks across Claude Opus/Sonnet/Haiku + GPT-4o. Shows per-run cost, daily cost, monthly cost with clear token assumptions. Gives a concrete routing rule.

**`/run`** — Executes the improved prompt for real and delivers actual output.

## Saved Outputs

Every command saves results to `.promptops/` in your project:

```
.promptops/
├── evals/
├── improved/
├── regressions/
├── comparisons/
└── runs/
```

## Skills (Auto-Invoked)

- **prompt-quality-check** — One-line fix while you edit prompts. Silent when solid.
- **golden-dataset-builder** — Saves approved outputs as test cases over time.

## Installation

**Mac app:** Plugins → Add plugin → Upload plugin → select this folder

**Terminal:** `claude --plugin-dir /path/to/promptops`

## Author

**Harman Sidhu** — [harmansidhudev.com](https://harmansidhudev.com)
