# Orion OS — Roadmap & Vision

> Where Orion OS is, where it's going, and the principles guiding evolution.

---

## What is Orion OS

Orion OS is a framework for orchestrating AI agent teams that build real software.
Not a chatbot. A working methodology: roles, rules, memory, decisions, workflows.

Today it runs on Claude + GitHub MCP + markdown files.
Tomorrow it will be a web product anyone can use without technical knowledge.

**The two layers:**
```
System layer   → workflows, skills, templates, decisions (this repo)
Instance layer → projects, logs, personal decisions (your private fork)
```

---

## Current state — v2.0.0

### What works
- Smart session init: agents load the right context + skills per project
- Session commands: project init, project switch, session close
- Multi-project isolation in a single instance
- Multi-framework skills (Angular, React, etc.)
- Monorepo + polyrepo support in project-init
- Scaffold via GitHub MCP — reversible toward web UI
- Universal decisions framework (D1-D93) governing every project

### What doesn't work yet
- No automatic session start — requires manual bootstrap trigger
- No persistent memory between sessions — markdown is loaded each time
- No web interface — requires technical knowledge (git, Claude, MCP)
- System ↔ instance sync is manual

---

## Roadmap

### v2.x — System layer maturation
```
Goal: migrate, generalize, and stabilize the system layer in this public repo
What changes:
  - Agents, skills, workflows, templates migrated incrementally from private instances
  - Each migration is reviewed and generalized — no bulk dumps
  - /examples populated with real anonymized projects
  - Sync mechanism between private instances and this repo defined and tested
```

### v3.0.0 — Orion OS web interface
```
Goal: anyone can use Orion OS without technical knowledge
Core flow:
  1. User goes to the web app
  2. GitHub OAuth → connects their account
  3. Onboarding wizard:
     - Project name
     - Topology (monorepo/polyrepo)
     - Frontend / Backend / DB / Auth / Deploy choices
  4. Orion creates repo + files + first issue automatically
  5. User gets a chat with Orion — context loaded, no bootstrap needed
  6. "Setup" button → automated git clone + install script

Tech stack (proposed, not decided):
  - Frontend: React or Angular
  - Backend: Node (NestJS or serverless)
  - LLM: Anthropic API
  - GitHub integration: OAuth + GitHub API (replaces MCP)
  - Session memory: DB-backed (replaces markdown bootstrap)
```

---

## Core principles

### D89 — Every decision must be reversible
When two options exist, always choose the one that doesn't block the web product.
If a decision is irreversible, document and justify it explicitly.

### D90 — Scaffold via GitHub API/MCP, never terminal
Orion pushes files to repos. Users clone and install.
This maps 1:1 to the future web UI "Setup" button.
If a workflow only works with terminal access, it is not a valid Orion OS workflow.

### The lab principle
Real projects are the primary lab for testing Orion OS.
Every decision made in a real project either improves Orion OS or validates
v3.0.0 assumptions. The framework grows from use, not from speculation.

---

## Open questions

1. **Persistent memory without markdown bootstrap?**
   DB-backed state, vector memory, hybrid?

2. **Minimum viable v3.0.0?**
   Just wizard + repo creation, or also full chat interface?

3. **Sync mechanism between this repo and private instances?**
   Cherry-pick, GitHub Action, subtree? Deferred until usage shows the pattern.

4. **What does a "skill" look like in the web product?**
   Marketplace, user-defined, auto-detected from stack?

5. **Onboarding for non-technical founders?**
   How short can the path from signup to first commit be?

---

*Orion OS v2.0.0 — public repo born from the system layer of a working private instance.*
