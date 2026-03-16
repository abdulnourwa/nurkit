# NurKit — /kit analyze prompt
> Context: {{CONTEXT}}
> Vision: {{VISION}}
> Blueprint: {{BLUEPRINT}}

---

You are doing a critical backward-looking review. Compare the blueprint against the vision and find everything that was lost, forgotten, contradicted, or left vague during planning.

You are not adding new ideas. You are making sure what was discussed in clarify actually made it into the blueprint.

Do not rewrite the blueprint from scratch. Find specific gaps and fix specific sections.

## Your Process

### Step 1 — Cross-Reference Every Item

**Roles & Workflows**
- Is every role from VISION.md fully represented in the blueprint?
- Does every role's workflow appear in the blueprint's feature specifications?
- Are there workflows in the vision with no corresponding API endpoint or screen?

**Features**
- Is every feature from VISION.md present in the blueprint?
- Are features in VISION.md priority order respected in the phases?
- Are any non-features accidentally included in the blueprint?

**Business Rules**
- Is every business rule enforced somewhere in the blueprint?
- Which rules have no corresponding validation or logic defined?

**Scale & Security**
- Are scale expectations reflected in the database and API design?
- Are all security requirements addressed?

**Integrations**
- Is every integration from the vision present in the blueprint?

**Open Questions**
- Are any open questions from the vision silently assumed instead of resolved?

### Step 2 — Check Internal Consistency

- Does the folder structure match the API design?
- Do the screens listed match the features specified?
- Are there endpoints with no screen that calls them?
- Are there screens with no endpoint that feeds them?
- Does the type ownership map cover all types mentioned in feature specs?
- Does the auth approach match the role/permission requirements?

### Step 3 — Update the Blueprint

For every gap or contradiction found:
1. State clearly what was missing or wrong
2. Update the relevant section
3. Only fix what is wrong — do not rewrite correct sections

### Step 4 — Report

```
## Analysis Complete

### Items recovered from vision missing from blueprint:
- [item]: added to [section]

### Contradictions fixed:
- [contradiction]: resolved by [change]

### Type ownership gaps:
- [type]: added to [location]

### Items still unclear (need user input):
- [item]: [question]

### Blueprint updated: [filename]
```

When complete: "Analysis complete. Blueprint updated. Run ./kit gaps"
