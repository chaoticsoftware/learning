# AI Learning — Sina
# Repository: https://github.com/chaoticsoftware/learning

## What This Is
A structured, self-paced AI mastery curriculum for a veteran software engineer.
12 modules covering the full AI practitioner stack — taught interactively with Claude,
tracked in git, resumable on any device.

---

## Table of Contents
1. [Quick Start on a New Device](#quick-start-on-a-new-device)
2. [Git Usage in This Learning Program](#git-usage-in-this-learning-program)
3. [Client Device Setup](#client-device-setup)
4. [File Structure](#file-structure)
5. [Module List](#module-list)
6. [How Sessions Work](#how-sessions-work)

---

## Quick Start on a New Device

```bash
git clone https://github.com/chaoticsoftware/learning.git
cd learning
git checkout u/sinah/init
cat PROGRESS.md           # see where you left off
```

Then open Claude Code and say:

```
Resume my AI learning. Read PROGRESS.md and pick up where we left off.
```

That's it. Everything Claude needs is in the repo.

---

## Git Usage in This Learning Program

### Why git here
Git is the persistence layer for this learning experience. It tracks:
- What you've learned (topic notes in `topics/`)
- How far you've progressed (`PROGRESS.md`)
- Working code from exercises (`exercises/`)
- Evolution of the curriculum and facilitation approach (`LEARNING_PLAN.md`, `MASTER_PROMPT.md`)

Every session ends with a commit + push so that any device can resume with `git pull`.

### Branching strategy
- **`u/sinah/init`** is the single working branch — all learning happens here
- No feature branches needed for notes and exercises
- If experimenting with exercise code you might want to throw away, branch off: `git checkout -b experiment/module-5-agent-loop`, then merge or discard

### Commit message conventions

| Prefix | Use for | Example |
|--------|---------|---------|
| `learn(module-N):` | New teaching content added to `topics/` | `learn(module-2): prompt engineering with CoT diagrams` |
| `progress(module-N):` | Session update to `PROGRESS.md` | `progress(module-2): completed few-shot and structured output sections` |
| `exercise(module-N):` | Code added or updated in `exercises/` | `exercise(module-4): tool use loop with calculator and web search` |
| `drill(module-Na):` | Drill-down sub-topic file added | `drill(module-1a): attention mechanism deep dive` |
| `meta:` | Infrastructure changes — README, MASTER_PROMPT, LEARNING_PLAN, .gitignore | `meta: add client setup guide to README` |

### Session sync workflow

```
Start of session (any device)       End of session
──────────────────────────────       ──────────────────────────────
git pull                             git add -A
                                     git commit -m "progress(N): ..."
                                     git push
```

Claude Code handles the end-of-session commit automatically.
If using another AI tool, do it manually.

### What lives in git / what doesn't

| Committed | Not committed (in .gitignore) |
|-----------|-------------------------------|
| All `.md` teaching notes | `.env` files, API keys |
| All exercise source code | `node_modules/`, `.venv/` |
| `PROGRESS.md` updates | Large model weight files (`.bin`, `.gguf`, etc.) |
| `MASTER_PROMPT.md` versions | IDE workspace files (`.idea/`, `.vscode/`) |

---

## Client Device Setup

### Core requirements

| Tool | Purpose | Install |
|------|---------|---------|
| **git** | Version control | Comes with most systems; [git-scm.com](https://git-scm.com) |
| **Claude Code** | Primary AI facilitator (CLI) | `npm install -g @anthropic-ai/claude-code` |
| **Node.js 18+** | Required by Claude Code and JS exercises | [nodejs.org](https://nodejs.org) (use LTS) |
| **Python 3.11+** | Required for most AI library exercises | [python.org](https://python.org) or `pyenv` |

### IDE — VSCode (recommended)

VSCode is a solid choice for this curriculum. Install it and add these extensions:

| Extension | Why |
|-----------|-----|
| **Markdown Preview Enhanced** | Renders Mermaid diagrams in topic files — essential |
| **Python** (Microsoft) | Linting, IntelliSense for exercise code |
| **Pylance** | Fast Python type checking |
| **GitLens** | Richer git history, blame, and diff views |
| **GitHub Copilot** | You already use this; keep it available for comparison exercises |
| **REST Client** | Test API calls directly from `.http` files (useful in Module 3) |
| **Jupyter** | Run `.ipynb` notebooks for ML exercises (Module 10) |
| **Thunder Client** | Lightweight API client inside VSCode |

**VSCode settings worth enabling:**
```json
{
  "editor.wordWrap": "on",
  "markdown.preview.breaks": true,
  "files.autoSave": "onFocusChange"
}
```

### Alternative IDEs

| IDE | Strengths | When to prefer |
|-----|----------|----------------|
| **Cursor** | VSCode fork with deep AI integration; entire codebase is AI-context-aware | If you want AI-assisted coding as a first-class feature in the IDE itself |
| **Zed** | Extremely fast, built-in AI (Claude), multiplayer editing | If you value raw performance and minimalism |
| **JetBrains (PyCharm / IDEA)** | Best-in-class Python/Java refactoring and debugging | If exercises become large Python projects |

**Cursor** is worth trying specifically in the context of this curriculum — it's a live demonstration of AI-native development (Module 12 territory). Many AI practitioners use it daily.

### Python environment setup

```bash
# Install uv — the fastest Python package manager (recommended over pip/conda)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Create a virtual environment for exercises
cd ~/learning
uv venv
source .venv/bin/activate        # macOS/Linux
.venv\Scripts\activate           # Windows

# Core packages for early modules (add more as curriculum progresses)
uv pip install anthropic openai python-dotenv httpx
```

### Node/JS setup (for MCP and JS exercises)

```bash
# Install fnm (fast Node version manager — preferred over nvm)
curl -fsSL https://fnm.vercel.app/install | bash
fnm install 22
fnm use 22

# Verify
node --version   # should show v22.x
```

### API keys you'll need

Create a `.env` file in the repo root (it's gitignored):

```bash
# .env — never commit this file
ANTHROPIC_API_KEY=sk-ant-...       # from console.anthropic.com — needed from Module 3
OPENAI_API_KEY=sk-...              # optional; useful for cross-model comparison exercises
```

Access it in Python:
```python
from dotenv import load_dotenv
import os
load_dotenv()
api_key = os.getenv("ANTHROPIC_API_KEY")
```

### Markdown rendering for Mermaid diagrams

Teaching notes use Mermaid diagrams extensively. To render them:

| Method | How |
|--------|-----|
| **VSCode + Markdown Preview Enhanced** | Right-click `.md` file → "Open Preview" |
| **GitHub** | Renders Mermaid natively in `.md` files in the repo |
| **Obsidian** | Install the Mermaid plugin; good for note-taking alongside sessions |
| **`npx @mermaid-js/mermaid-cli`** | Export diagrams to SVG/PNG from terminal |

GitHub rendering is zero-setup — just browse `topics/` in the repo UI.

### Windows-specific notes

- Use **WSL2** (Windows Subsystem for Linux) for the best CLI experience — all shell commands in exercises assume a Unix shell
- Install **Windows Terminal** for a better terminal experience
- Claude Code runs natively on Windows but WSL2 is smoother for Python/Node tooling
- Git credential manager is included with Git for Windows

### macOS-specific notes

```bash
# Install Homebrew first if not present
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew install git node python@3.12
```

### Linux-specific notes

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install -y git python3 python3-pip python3-venv

# Node via fnm (preferred over apt's outdated version)
curl -fsSL https://fnm.vercel.app/install | bash
```

---

## File Structure

```
learning/
├── .gitignore
├── README.md                    ← you are here
├── LEARNING_PLAN.md             ← full 12-module curriculum
├── MASTER_PROMPT.md             ← reproduce this on any AI tool
├── PROGRESS.md                  ← session log and per-module status
├── topics/                      ← teaching material, one file per module
│   ├── 01-llm-foundations.md
│   └── ... (created as modules complete)
└── exercises/                   ← hands-on code, one dir per module
    ├── module-01/
    └── ...
```

---

## Module List

| # | Module | Status |
|---|--------|--------|
| 1 | LLM Foundations | In progress |
| 2 | Prompt Engineering | Not started |
| 3 | AI APIs & SDKs | Not started |
| 4 | Tool Use & Function Calling | Not started |
| 5 | AI Agents | Not started |
| 6 | Model Context Protocol (MCP) | Not started |
| 7 | RAG & Knowledge Systems | Not started |
| 8 | Multi-Agent Systems | Not started |
| 9 | Evals & Testing | Not started |
| 10 | Fine-tuning & Customization | Not started |
| 11 | Production AI Systems | Not started |
| 12 | Frontier Topics | Not started |

See `PROGRESS.md` for detailed per-module status and session log.

---

## How Sessions Work

1. `git pull` to sync
2. Tell Claude Code: `"Resume my AI learning. Read PROGRESS.md and pick up where we left off."`
3. Work through the module — Claude teaches, you ask questions, we build things
4. Notes land in `topics/`, code in `exercises/`
5. Claude commits and pushes at session end

If using a different AI tool, use `MASTER_PROMPT.md` and paste in `PROGRESS.md` content manually.
