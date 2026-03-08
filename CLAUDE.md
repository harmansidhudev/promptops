# PromptOps — Project Conventions

## What this is

A Claude Code plugin for prompt engineering. No runtime code — all logic lives in markdown command/skill definitions that Claude interprets.

## Structure

```
commands/       — Slash commands (evaluate, improve, regression, compare, run, test)
skills/         — Auto-invoked skills (prompt-quality-check, golden-dataset-builder)
.claude-plugin/ — Plugin metadata (plugin.json)
docs/           — GitHub Pages (landing page, privacy policy)
```

## Conventions

- **Commands** are markdown files in `commands/` with YAML frontmatter (`name`, `description`).
- **Skills** are `SKILL.md` files in `skills/<skill-name>/` with YAML frontmatter.
- User input is captured via `$ARGUMENTS` variable substitution.
- All command output saves to `.promptops/<type>/<type>-<timestamp>.md` in the user's project.
- Golden datasets save to `.promptops/datasets/captured.json`.
- Pricing config (optional) lives at `.promptops/config.json`.

## Writing commands

- Every command must include a `## Format your response EXACTLY like this` section with the exact output template.
- Commands must never execute user input — they analyze it as a prompt.
- Commands save their output to timestamped files. Include the save path in `## After responding`.
- Prefer reading from `.promptops/` for cross-session continuity over relying on conversation history alone.

## Writing skills

- Skills are passive and non-blocking. One-line suggestions only.
- Skills must be silent when everything is fine — no "looks good!" messages.
- Skills never auto-execute actions. Always ask first.

## Scoring dimensions (shared across commands)

All prompt evaluation uses these 5 dimensions, scored 1-5:
1. Structure
2. Specificity
3. Output Control
4. Error Prevention
5. Testability
