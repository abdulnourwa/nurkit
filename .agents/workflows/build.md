---
name: build
description: Execute the current phase of the checklist
---
# NurKit — Build

Execute the current phase of the checklist. One task at a time.

## Steps

1. Read `.nurkit/prompts/build.md` completely
2. Read `.nurkit/CONTEXT.md`, `.nurkit/STACK.md`, latest blueprint, latest checklist
3. Print the SESSION START block and wait for user confirmation
4. Find the first uncompleted task in the current phase
5. If phase type changed from previous phase, print the ⚡ MODEL HINT
6. Execute the task following all rules in `.nurkit/STANDARDS.md`
7. After the task, print the TASK COMPLETE block — every field filled
8. Update `.nurkit/CHANGELOG.md`, check off the task, git commit
9. State the next task and wait — do not auto-continue
10. When phase complete: notify user and wait for confirmation before next phase
