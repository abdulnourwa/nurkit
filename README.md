<div align="center">

![NurKit Banner](file:///C:/Users/MiQDAD/.gemini/antigravity/brain/ebad8e14-ce2e-45d8-a374-a22f4dc3f12a/nurkit_banner_1773653843385.png)

# NurKit
### AI-Powered Project Orchestration for Professional Vibe Coding

[![Version](https://img.shields.io/badge/version-1.6.0-blue.svg?style=flat-square)](https://github.com/abdulnourwa/nurkit/blob/main/NURKIT-CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)](https://github.com/abdulnourwa/nurkit/blob/main/LICENSE)
[![Maintenance](https://img.shields.io/badge/maintained-yes-brightgreen.svg?style=flat-square)](#)
[![Stack](https://img.shields.io/badge/stack-Any-orange.svg?style=flat-square)](#)

</div>

---

## ⚡ What is NurKit?

**NurKit** is a battle-hardened orchestration layer designed to transform "vibe coding" into a structured, professional engineering workflow. It bridges the gap between raw AI capabilities and consistent, production-grade development.

### Why NurKit?
- 🧠 **Zero Context Loss**: `CONTEXT.md` meticulously tracks session state, so your AI always knows where you left off.
- 🎯 **Rigorous Planning**: Native `/clarify`, `/plan`, and `/gaps` workflows ensure deep architectural alignment before a single line of code is written.
- 🏦 **Standardized Output**: Enforced file headers, modular structure, and automated changelogs keep your codebase clean and navigable.
- 🛠️ **Tool Agnostic**: One system for **Claude Code**, **OpenCode**, **Codex**, and **Antigravity**. Same rules, same brain.

---

## 🚀 Quick Start

### 1. Installation
Clone NurKit once to your local machine:
```bash
git clone https://github.com/abdulnourwa/nurkit.git ~/nurkit
```

### 2. Scaffold a Project
Initialize any directory (new or existing) with the NurKit core:
```bash
# Enter your project
cd my-cool-project

# Inject NurKit (select based on your tools)
cp -r ~/nurkit/.nurkit .
cp -r ~/nurkit/.agents .    # For Antigravity
cp -r ~/nurkit/.claude .    # For Claude Code
cp -r ~/nurkit/.opencode .  # For OpenCode
cp ~/nurkit/AGENTS.md .     # For OpenCode / Codex
cp ~/nurkit/opencode.json . # For OpenCode
cp ~/nurkit/CLAUDE.md .     # For Claude Code
```

### 3. Initialize Workflow
Open your AI tool of choice in the project root and start the cycle:
```bash
/clarify
```

---

## 📂 The Repository Brain
NurKit organizes your project's technical memory into a unified `.nurkit/` directory.

| File | Purpose |
| :--- | :--- |
| `AGENT.md` | Core laws, session rituals, and development standards. |
| `CONTEXT.md` | Persistent session state and chronological history. |
| `STACK.md` | Strict technology lock to prevent dependency drift. |
| `STANDARDS.md` | Comprehensive architectural and code quality rules. |
| `BLUEPRINTS/` | Versioned technical designs and implementation plans. |
| `CHECKLISTS/` | Granular, phased task lists derived from blueprints. |

---

## 🛠️ Unified Commands
NurKit provides a cross-tool command set that works identically across all supported AI interfaces.

```mermaid
graph TD
    A[/clarify] --> B[/plan]
    B --> C[/analyze]
    C --> D[/gaps]
    D --> E[/checklist]
    E --> F[/build]
    F --> G[/review]
    G --> H[/commit]
    H --> I[/deploy]
```

### Command Reference
| Command | Primary Action | Ideal Model |
| :--- | :--- | :--- |
| `/clarify` | Deep-dive requirement gathering. | Reasoning (Opus/Sonnet) |
| `/plan` | Generate a comprehensive architectural blueprint. | Reasoning (Opus/Sonnet) |
| `/gaps` | Audit the plan for edge cases and security. | Reasoning (Opus/Sonnet) |
| `/checklist`| Break the blueprint into executable phases. | Balanced (Sonnet) |
| `/build` | Execute a phase and auto-commit changes. | Balanced (Sonnet) |
| `/sync` | Force-save current state to the context ledger. | Fast (Haiku/Flash) |

---

## 🔌 Tool Integration

### 🧊 OpenCode & Codex
- Auto-reads `AGENTS.md` (or `AGENTS.override.md`) at session start.
- `opencode.json` ensures core context is always loaded.
- Type `/` to access full command suite.

### 🐦 Claude Code
- Natively reads `CLAUDE.md`.
- Slash commands are integrated via the `.claude/commands` directory.

### 🛰️ Antigravity
- Uses `.agents/rules` for always-on session intelligence.
- Workflows are executable via the standard command palette.

---

## 📖 Best Practices
1. **Always `/sync`**: Before closing a session, use `/sync` to ensure the next model knows exactly where to resume.
2. **Respect the Header**: NurKit requires specific headers for every file. Never skip them.
3. **Planning First**: Resist the urge to code before `/plan` and `/gaps` are complete.

---

## 📄 License
Distributed under the **MIT License**. See `LICENSE` for more information.

<div align="center">
  <sub>Built with ❤️ by the NurKit Community</sub>
</div>
