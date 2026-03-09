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

**`/improve`** — Rewrites your prompt with schemas, guardrails, and no filler. Shows before/after score and what changed. If the result is complex (1500+ tokens, 3+ objectives), suggests splitting into phases.

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
- **prompt-complexity-check** — Detects when an improved prompt is too complex for a single pass. Suggests splitting into sequential phases to improve accuracy and reduce cost. Fires after `/improve`, silent when the prompt is fine.

## Installation

**Claude Code (recommended):**
```
/plugin install promptops@harmansidhudev/promptops
```

**Mac app:** Plugins → Add plugin → Upload plugin → select this folder

**Terminal:** `claude --plugin-dir /path/to/promptops`

### Install Scopes

| | Session | Project | Global |
|---|---|---|---|
| **How** | `claude --plugin-dir /path/to/promptops` | `/plugin install promptops --scope project` | `/plugin install promptops` |
| **Persists** | Only while session is open | Committed to repo (`.claude/plugins`) | Stored in `~/.claude/plugins` |
| **Available where** | That one session | That repo only | Every project |
| **Shared with team** | No | Yes — checked into git | No — local to your machine |
| **Auto-loads** | No — must pass flag each time | Yes — every time you open the repo | Yes — always |
| **Live-updates from source** | Yes — reads files directly | No — reinstall to update | No — reinstall to update |
| **Best for** | Dev/testing the plugin | Team workflows on a shared repo | Personal tooling you want everywhere |

> **Tip:** Use `--plugin-dir` during development for live changes. Once the plugin is published on the Claude marketplace, install it directly with `/plugin install` for automatic updates.

## Author

**Harman Sidhu** — [harmansidhudev.com](https://harmansidhudev.com)
