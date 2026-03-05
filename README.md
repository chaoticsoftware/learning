# AI Learning — Sina
# Repository: https://github.com/chaoticsoftware/learning

## What This Is
A structured, self-paced AI mastery curriculum for a veteran software engineer.
12 modules covering the full AI practitioner stack — taught interactively with Claude,
tracked in git, resumable on any device.

---

## Quick Start on a New Device

```bash
git clone https://github.com/chaoticsoftware/learning.git
cd learning
git checkout u/sinah/init      # or whatever the active branch is
cat PROGRESS.md                # see where you left off
```

Then open Claude Code (or any capable AI tool) and paste:

```
Resume my AI learning. Read PROGRESS.md and pick up where we left off.
```

That's it. Everything Claude needs is in the repo.

---

## Syncing Progress Between Devices

**At the end of every session** (Claude does this, but you can also do it manually):

```bash
git add -A
git commit -m "progress(module-N): <one line describing what was covered>"
git push
```

**At the start of a session on a different device:**

```bash
git pull
```

---

## Commit Message Conventions

| Prefix | When to use | Example |
|--------|------------|---------|
| `learn(module-N):` | New module teaching content added | `learn(module-1): LLM foundations with Mermaid diagrams` |
| `progress(module-N):` | Session progress — concepts covered, exercises done | `progress(module-2): covered CoT and few-shot prompting` |
| `exercise(module-N):` | Exercise code added or updated | `exercise(module-4): tool use loop with calculator` |
| `drill(module-Na):` | Drill-down sub-topic added | `drill(module-1a): attention mechanism deep dive` |
| `meta:` | Changes to LEARNING_PLAN, MASTER_PROMPT, README, PROGRESS structure | `meta: add git workflow to MASTER_PROMPT v1.2.0` |

---

## Branch Strategy

- **`u/sinah/init`** — main working branch; all learning happens here
- No need for feature branches unless experimenting with exercise code you might want to discard
- Push to remote after every session so progress is always recoverable from any device

---

## File Structure

```
learning/
├── .gitignore
├── README.md                    ← you are here; cross-device guide
├── LEARNING_PLAN.md             ← full 12-module curriculum
├── MASTER_PROMPT.md             ← how to reproduce this on any AI tool
├── PROGRESS.md                  ← session log and per-module status
├── topics/                      ← teaching material, one file per module
│   ├── 01-llm-foundations.md
│   ├── 02-prompt-engineering.md
│   └── ... (created as modules complete)
└── exercises/                   ← hands-on code, one dir per module
    ├── module-01/
    ├── module-02/
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

1. Pull latest: `git pull`
2. Tell Claude: `"Resume my AI learning. Read PROGRESS.md and pick up where we left off."`
3. Work through the module — Claude teaches, you ask questions, we build things
4. Notes land in `topics/`, code in `exercises/`
5. At session end Claude updates `PROGRESS.md` and commits + pushes

If using a different AI tool (not Claude Code), use the master prompt from `MASTER_PROMPT.md`
and paste in the current `PROGRESS.md` content manually.
