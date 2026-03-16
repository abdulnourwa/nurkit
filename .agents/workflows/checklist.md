---
name: checklist
description: Generate the phased task list from the complete blueprint
---
# NurKit — Checklist

Generate the phased task list from the complete blueprint.

## Steps

1. Read `.nurkit/prompts/checklist.md` completely
2. Read `.nurkit/CHECKLIST-TEMPLATE.md` as the shape reference
3. Read the latest file in `.nurkit/blueprints/` and `.nurkit/STACK.md`
4. Follow the checklist prompt exactly — frontend and backend always separate phases
5. Find the highest version in `.nurkit/checklists/` and save to
   `.nurkit/checklists/CHECKLIST-v[next].md`
6. Confirm: "Checklist generated. [N] phases, [N] tasks. Run /build when ready."
