---
name: prompt-complexity-check
description: "Catches prompts that are too complex for a single pass. Fires after /improve produces output. Suggests splitting into phases when token count, objective count, or context domains make single-pass execution unreliable. Silent when the prompt is fine."
---

After `/improve` produces an improved prompt, silently analyze it for complexity. Check:

1. **Token count** — estimated >1500 tokens
2. **Objective count** — 3+ distinct task objectives (e.g., "score X, then generate Y, then compare Z")
3. **Context domains** — requires holding >2 separate knowledge areas simultaneously
4. **Cost at scale** — per-run cost would exceed $0.02 on Sonnet at default pricing

If ANY of these are true, suggest splitting. Use exactly this format:

⚡ **This prompt might work better in phases.** ~X tokens, N objectives — splitting could improve accuracy and cut costs by ~X%. Want me to break it into phases? (y/n)

If the user says yes:
1. Split the prompt into sequential phases following these rules:
   - Each phase gets exactly one objective
   - Target 300-800 tokens per phase
   - Split at natural task transitions — never mid-reasoning or mid-list
   - Each phase after the first must reference prior phase outputs explicitly
   - Shared context (definitions, constraints, tone) goes in a reusable preamble included with every phase
2. Present each phase in a numbered code block so the user can copy them
3. Show the estimated token savings and per-phase cost breakdown
4. Save the phased version to `.promptops/improved/improved-phased-<timestamp>.md`

If the user says no: move on. Don't mention it again this session.

Rules: one line to suggest, silence means the prompt is fine, never auto-split, never block the /improve output, don't fire on prompts that are already under 1500 tokens with fewer than 3 objectives.
