# NurKit
> AI-powered project orchestration for serious vibe coding.
> Works with Claude Code and OpenCode. No bash scripts. No setup headaches.

---

## What is NurKit?

NurKit is a structured system that makes AI-assisted development reliable,
organized, and consistent across sessions. It solves the core problems of
vibe coding:

- **Context loss** between sessions — CONTEXT.md saves state every time
- **Planning gaps** — clarify + analyze + gaps audit catches everything
  before a line of code is written
- **Model cost waste** — planning commands use Opus, build commands use
  Sonnet — automatic in OpenCode, hinted in Claude Code
- **Vibe coding chaos** — every file has a header, every task gets a
  commit, nothing is silently forgotten

---

## Install Once

```bash
# Clone NurKit to your machine — do this once ever
git clone https://github.com/[your-username]/nurkit.git ~/nurkit
```

---

## New Project

```bash
mkdir my-app && cd my-app
git init

# Copy NurKit into your project
cp -r ~/nurkit/.kit .
cp -r ~/nurkit/.claude .        # if you use Claude Code
cp -r ~/nurkit/.opencode .      # if you use OpenCode
cp ~/nurkit/CLAUDE.md .         # if you use Claude Code

# Commit
git add .
git commit -m "init: add NurKit"
```

Open Claude Code or OpenCode in this folder and type `/clarify` to begin.

---

## Existing Project

```bash
cd your-existing-project

# Copy .kit — safe, this folder won't exist yet
cp -r ~/nurkit/.kit .

# Claude Code commands
# If .claude/ does not exist:
cp -r ~/nurkit/.claude .
# If .claude/commands/ already exists with other commands:
cp ~/nurkit/.claude/commands/*.md .claude/commands/

# OpenCode commands
# If .opencode/ does not exist:
cp -r ~/nurkit/.opencode .
# If .opencode/commands/ already exists with other commands:
cp ~/nurkit/.opencode/commands/*.md .opencode/commands/

# CLAUDE.md
# If CLAUDE.md does not exist:
cp ~/nurkit/CLAUDE.md .
# If CLAUDE.md already exists — open it and paste this at the bottom:
# ---
# ## NurKit Rules
# [paste content of ~/nurkit/CLAUDE.md here]

# .gitignore — never overwrite, only append these 3 lines if not present:
echo "" >> .gitignore
echo "# NurKit" >> .gitignore
echo ".kit/ENV.md" >> .gitignore
echo ".kit/CONTEXT.md" >> .gitignore
echo ".kit/AGENT-ERRORS.md" >> .gitignore

# Commit
git add .
git commit -m "chore: add NurKit"
```

Open Claude Code or OpenCode and type `/clarify` to begin.

---

## The Workflow

Same for both new and existing projects. Same for both tools.

```
/clarify      →    /plan      →    /analyze
    ↓
/gaps         →    /checklist →    /build
    ↓
/deploy
```

---

## All Commands

| Command | What it does | Model |
|---|---|---|
| `/clarify` | Deep questioning to document your idea | Best |
| `/clarify my-idea.md` | Clarify from an existing document | Best |
| `/plan` | Full blueprint from clarify output | Best |
| `/analyze` | Find what the plan missed from clarify | Best |
| `/gaps` | Master completeness audit | Best |
| `/checklist` | Generate phased task list | Cheaper |
| `/build` | Execute current phase, auto-commit | Cheaper |
| `/feature auth-system` | Full flow scoped to one feature | Best → Cheaper |
| `/review` | Compare code vs blueprint | Best |
| `/status` | Progress dashboard | Any |
| `/commit` | Meaningful commit + changelog update | Any |
| `/sync` | Save session state before closing | Any |
| `/deploy` | Deploy to staging | — |
| `/deploy --prod` | Deploy to production | — |

---

## Model Strategy

NurKit does not switch models automatically. You always choose your model.
Commands show a `⚡ MODEL HINT` when a different model would serve you better.

- Planning work (clarify, plan, analyze, gaps, review) → use your best model
- Build work (checklist, build, feature) → a strong reasoning model is fine
- Routine work (sync, status, commit, deploy) → any model works

This applies to both Claude Code and OpenCode.
Switch models in your tool's model selector whenever you see a hint.

---

## How Each Tool Uses NurKit

### Claude Code
- Reads `CLAUDE.md` automatically at every session start
- Agent knows all rules, rituals, and file locations without you explaining
- Commands live in `.claude/commands/`
- Type `/` to see all available commands

### OpenCode
- Commands live in `.opencode/commands/`
- Models pinned per command — planning always Opus, build always Sonnet
- Type `/` to see all available commands

### Both tools
- Read the same `.kit/` files — same brain, same memory, same prompts
- The tool is just the interface — NurKit works identically in both

---

## Saving a Session

When your context window gets long or you are switching models:

```
/sync
```

This saves complete session state to `.kit/CONTEXT.md`.
Next session the agent reads it and knows exactly where to continue.

---

## The .kit/ Folder

```
.kit/
├── AGENT.md              ← Agent laws and session rituals
├── STANDARDS.md          ← Code quality, folder rules, type rules
├── CONTEXT.md            ← Current session state + history
├── STACK.md              ← Tech stack lock
├── ASSUMPTIONS.md        ← Surfaced assumptions log
├── KNOWN-ISSUES.md       ← Open and resolved issues
├── DECISIONS.md          ← Architectural decision log
├── DEFINITION-OF-DONE.md ← What done means at every level
├── ENV.md                ← Environment variable docs (gitignored)
├── DEPLOY.md             ← VPS setup and deploy history
├── CHANGELOG.md          ← Auto-updated change log
├── GAPS-TEMPLATE.md      ← Master completeness checklist
├── CHECKLIST-TEMPLATE.md ← Phased task list shape
├── prompts/              ← One prompt file per command
├── blueprints/           ← Versioned architecture blueprints
├── gaps/                 ← Dated gaps audit outputs
├── checklists/           ← Versioned task checklists
└── vision/               ← Vision documents
```

---

## Tuning NurKit

Every command uses a prompt file in `.kit/prompts/`.
If a command is not producing the results you want,
open the relevant prompt file and improve it.
No other changes needed — the command picks it up immediately.

---

## On Windows

Use **Git Bash** (included with Git for Windows).
All commands work identically to Mac.

---

## License

MIT — use it, fork it, improve it.
