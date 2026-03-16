# NURKIT-CHANGELOG.md
> This file tracks changes to NurKit itself — not your project.
> Your project's changelog lives in .nurkit/CHANGELOG.md

---

## v1.4.0 — Renamed .kit/ to .nurkit/, Added Antigravity Support

### Changed
- Renamed `.kit/` folder to `.nurkit/` across entire project
- All internal references updated from `.kit/` to `.nurkit/`

### Added
- `.agents/rules/nurkit-always.md` — always-on rules for Antigravity
- `.agents/rules/nurkit-standards.md` — glob-activated code standards
- `.agents/rules/nurkit-types.md` — model-decision type ownership rules
- `.agents/workflows/` — 12 workflow files for Antigravity slash commands
- Antigravity users can now use /clarify, /plan, /analyze, /gaps,
  /checklist, /build, /feature, /review, /sync, /status, /commit, /deploy

## v1.3.0 — Removed Automatic Model Pinning

### Changed
- Removed all model: pins from .opencode/commands/ files
- Model strategy is now identical for Claude Code and OpenCode
- Both tools use ⚡ MODEL HINT comments only — user always chooses the model
- README model strategy section updated to reflect this

### Reason
Not all users have access to specific models or API subscriptions.
NurKit should work with any model the user has available.

## v1.2.0 — Removed Shell Script, Simplified Setup

### Removed
- `kit` bash script — no longer needed
- All `./kit` command references
- `chmod +x` setup requirement
- Terminal-switching workflow

### Changed
- README completely rewritten — new project and existing project setup
- Setup is now pure copy-paste, no script execution
- Usage is now entirely through slash commands inside the AI tool

### How to upgrade from v1.1.0
- Delete the `kit` file from your project root
- No other changes needed — all .kit/ files and commands stay the same

## v1.1.0 — Slash Commands

### Added
- `.claude/commands/` — 12 slash commands for Claude Code
- `.opencode/commands/` — 12 slash commands for OpenCode with models pinned per command
- Planning commands (clarify, plan, analyze, gaps, review) pinned to Opus in OpenCode
- Build commands (checklist, build, feature, sync, status, commit, deploy) pinned to Sonnet in OpenCode
- README updated with slash command usage section

## v1.0.0 — Initial Release

### Commands
- `./kit init` — scaffold NurKit into any project
- `./kit clarify` — deep questioning with --input file support
- `./kit plan` — full blueprint generation
- `./kit analyze` — drift detection between vision and blueprint
- `./kit gaps` — master completeness audit with dated output files
- `./kit checklist` — phased task generation with type labels
- `./kit build` — phase-aware execution with auto-commit
- `./kit feature` — scoped single-feature full flow
- `./kit review` — drift analysis between code and blueprint
- `./kit status` — progress dashboard
- `./kit commit` — meaningful commit with changelog update
- `./kit sync` — session state save before closing
- `./kit deploy` — VPS deployment with staging-first enforcement

### Files
- AGENT.md — session laws and rituals (short, read every session)
- STANDARDS.md — code quality principles (reference on demand)
- GAPS-TEMPLATE.md — master completeness checklist (10 sections)
- CHECKLIST-TEMPLATE.md — phased task list shape
- STACK.md — stack lock with agent rules
- ASSUMPTIONS.md — surfaced assumptions log
- KNOWN-ISSUES.md — open and resolved issues tracker
- DECISIONS.md — architectural decision log
- DEFINITION-OF-DONE.md — what done means at every level
- ENV.md — environment variable documentation
- DEPLOY.md — VPS setup, deploy process, and history
- CONTEXT.md — session state with appended history
- CLAUDE.md — Claude Code compatible agent rules
- All 12 prompt files in .nurkit/prompts/

### Key Design Decisions
- Tool-agnostic: works with Claude Code, OpenCode, or any AI tool
- Principle-based: no library names in agent rules
- Folder structure: gaps/, blueprints/, checklists/ for versioned history
- CLI: tries AI CLI first, falls back to manual paste
- Model hints: user-facing, not agent instructions
- CLAUDE.md: copy of AGENT.md for Claude Code native reading
