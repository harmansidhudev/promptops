---
name: run
description: "You evaluated it. You improved it. Now run it for real. Executes your best prompt version and delivers actual output."
---

The user's input is: $ARGUMENTS

## Your task

Execute the best prompt version from this session. Deliver real output — this is NOT another evaluation.

## Finding the prompt

1. **Check conversation history** for improved prompts from /improve — use the latest one
2. If multiple improved versions exist, list them and ask which to run
3. If no improved version, use the original from /evaluate
4. If nothing found and $ARGUMENTS has content, execute $ARGUMENTS directly as a prompt
5. If nothing found and $ARGUMENTS is empty, reply: "No prompt found. Run `/improve` first, or type `/run Your prompt here`"

## Executing

Actually follow the instructions in the selected prompt:
- Access files, codebases, or context if referenced
- Produce the output the prompt is designed to generate
- Format according to whatever the prompt specifies

## After the output

Add one line:

---
*Executed via PromptOps · Prompt scored X.X → improved to X.X*

## Save

Save the prompt used + output to `.promptops/runs/run-<timestamp>.md`. Create directory if needed.
