# NurKit — Feature

Full NurKit flow scoped to one feature. Pass the feature name as argument.

## Steps

1. Read `.nurkit/prompts/feature.md` completely
2. Read the latest blueprint and `.nurkit/STACK.md` to understand existing project
3. Run the full flow scoped to this feature:
   - Clarify (scoped)
   - Plan → save to `.nurkit/blueprints/BLUEPRINT-[feature-name].md`
   - Analyze
   - Gaps → save to `.nurkit/gaps/GAPS-[date]-[feature-name].md`
   - Checklist → save to `.nurkit/checklists/CHECKLIST-[feature-name].md`
   - Build
4. Never touch the main BLUEPRINT or main CHECKLIST files
5. Update CHANGELOG.md, STACK.md, ENV.md as normal during build

⚡ MODEL HINT: Use your best model for planning steps, any model for build steps.
