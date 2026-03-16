# NurKit
> AI-powered project orchestration for serious vibe coding.
> Works with Claude Code, OpenCode, or any AI tool.

---

## What is NurKit?

NurKit is a structured system that makes AI-assisted development reliable, organized, and consistent across sessions. It solves the core problems of vibe coding:

- **Context loss** between sessions — CONTEXT.md saves state, every time
- **Planning gaps** — clarify + analyze + gaps audit catches everything before a line of code is written
- **Model cost waste** — use powerful models for thinking, cheaper models for execution
- **Vibe coding chaos** — every file has a header, every task gets a commit, nothing is silently forgotten

---

## Install

### On any machine (Windows Git Bash or Mac Terminal)

```bash
git clone https://github.com/[your-username]/nurkit.git
```

That's it. NurKit lives on your machine. No npm, no global install needed.

---

## Start a New Project

```bash
mkdir my-new-project
cd my-new-project

# Copy NurKit into the project
cp /path/to/nurkit/kit .
cp -r /path/to/nurkit/.kit .
cp /path/to/nurkit/CLAUDE.md .
cp /path/to/nurkit/.gitignore .

# Make the script executable
chmod +x kit

# Initialize
./kit init
```

---

## The Workflow

```
./kit clarify       ← Document your idea fully (use your best model)
./kit plan          ← Full architecture blueprint (use your best model)
./kit analyze       ← Catch what the plan missed from clarify
./kit gaps          ← Completeness audit — empty states, validation, security, etc.
./kit checklist     ← Generate phased tasks (cheaper model is fine)
./kit build         ← Execute phase by phase (cheaper for backend, UI model for frontend)
./kit deploy        ← Staging first, then production
```

### Starting with an existing idea document

```bash
./kit clarify --input my-idea.md
```

---

## All Commands

| Command | What it does | Model |
|---|---|---|
| `./kit init` | Scaffold NurKit into a project | — |
| `./kit clarify` | Deep questioning to document your idea | Best |
| `./kit clarify --input file.md` | Clarify from an existing document | Best |
| `./kit plan` | Full blueprint from clarify output | Best |
| `./kit analyze` | Find what the plan missed from clarify | Best |
| `./kit gaps` | Master completeness audit | Best |
| `./kit checklist` | Generate phased task list | Cheaper |
| `./kit build` | Execute current phase, auto-commit | Cheaper / UI model |
| `./kit feature "name"` | Full flow scoped to one feature | Best → Cheaper |
| `./kit review` | Compare code vs blueprint | Best |
| `./kit status` | Progress dashboard | Any |
| `./kit commit` | Meaningful commit + changelog | Any |
| `./kit sync` | Save session state before closing | Any |
| `./kit deploy --prod` | Deploy to production | — |

---

## Slash Commands

### Claude Code
Commands are in `.claude/commands/`. Type `/` inside Claude Code to use them.
No model switching needed — just use the commands in order.

### OpenCode
Commands are in `.opencode/commands/`. Type `/` inside OpenCode to use them.
Models are pinned per command automatically — planning commands use Opus, build commands use Sonnet.

### Usage
/clarify          — document your idea
/plan             — write the blueprint
/analyze          — verify plan vs clarify
/gaps             — completeness audit
/checklist        — generate tasks
/build            — execute current phase
/feature auth     — scoped feature flow
/review           — drift analysis
/sync             — save session before closing
/status           — progress dashboard
/commit           — meaningful commit + changelog
/deploy           — deploy to staging
/deploy --prod    — deploy to production

---

## Model Strategy

NurKit tells you when to switch models. Look for `⚡ MODEL HINT` in command output.

- **Planning commands** (clarify, plan, analyze, gaps, review) → Use your most capable model
- **Backend build phases** → Strong reasoning model
- **Frontend build phases** → UI-focused model (the checklist will tell you)
- **Routine commands** (checklist, sync, commit, status) → Cheapest model is fine

---

## Working with Claude Code

NurKit includes `CLAUDE.md` in the project root. Claude Code reads this automatically at every session start. It contains the full agent laws, session rituals, and reading order. Claude Code will always know:

- Where we are in the project
- What files to read
- What rules to follow
- What to do before and after every session

---

## The .kit/ Folder

```
.kit/
├── AGENT.md              ← Agent laws and session rituals
├── STANDARDS.md          ← Code quality principles (reference)
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

Every command uses a prompt file in `.kit/prompts/`. If a command isn't producing the results you want, open the relevant prompt file and improve it. No code changes needed.

---

## Saving a Session

When your context window gets long or you're switching models, run:

```bash
./kit sync
```

This saves the complete session state to `CONTEXT.md`. Next session, the agent reads it first and knows exactly where to continue.

---

## On Windows

Use **Git Bash** (included with Git for Windows). Open Git Bash, navigate to your project, and run `./kit` commands exactly as shown. Everything works identically to Mac.

---

## License

MIT — use it, fork it, improve it.
