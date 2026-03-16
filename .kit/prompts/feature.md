# NurKit — /kit feature prompt
> Context: {{CONTEXT}}
> Blueprint (existing): {{BLUEPRINT}}
> Stack: {{STACK}}

---

You are running the full NurKit flow scoped to one feature. The main project files are not touched.

## Scope Rules
- Feature blueprint: `blueprints/BLUEPRINT-[feature-name].md`
- Feature checklist: `checklists/CHECKLIST-[feature-name].md`
- Gaps output: `gaps/GAPS-[date]-[feature-name].md`
- Main BLUEPRINT.md and main CHECKLIST.md are NOT modified
- CHANGELOG.md, STACK.md, ENV.md, DECISIONS.md are still updated (project-wide)

## Integration Awareness
Before planning, read the existing blueprint to understand:
- What already exists — do not re-create it
- What stack is in use — do not introduce new stack without flagging
- What patterns are established — follow them
- What types already exist in shared/types/ and feature types files

## Flow

### Step 1 — Feature Clarification
Ask:
1. What does this feature do? (one clear sentence)
2. Who uses it and what is their workflow?
3. What existing parts of the app does it connect to?
4. What are the acceptance criteria?
5. Edge cases or constraints specific to this feature?

### Step 2 — Feature Blueprint
Cover:
- Purpose and all roles involved
- New files needed (with purposes, following feature folder structure)
- Existing files that need modification (what changes)
- New types — check shared/types/ and existing feature types first
- New API endpoints
- New UI screens and their states
- Database changes if any
- New environment variables if any

### Step 3 — Feature Analyze
Did anything from clarification get lost in the blueprint?

### Step 4 — Feature Gaps
Run gaps scoped to this feature — UI states, edge cases, integration points, permissions.

### Step 5 — Feature Checklist
Generate scoped checklist following the same phase rules as full project checklists.

### Step 6 — Build
Follow standard build process using the feature checklist and the TASK COMPLETE block.

When complete: "Feature [name] complete. All tasks done. CHANGELOG updated."
