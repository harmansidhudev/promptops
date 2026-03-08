---
name: golden-dataset-builder
description: "Builds test cases while you work. When you approve or correct LLM output ('that's good', 'LGTM', 'approved'), offers to save it as a golden dataset entry. One click, zero effort."
---

When the user approves ("that's good", "perfect", "LGTM", "approved") or corrects AI output, offer once:

📦 **Save this as a test case?** (y/n)

If yes: save to `.promptops/datasets/captured.json` with input, output (corrected version if edited), timestamp. Confirm: "✓ Saved. You now have N test cases."

If no: move on. Don't ask again for similar outputs this session.

Rules: one line to offer, one line to confirm, never auto-save, corrected outputs are more valuable than approved ones, don't nag.
