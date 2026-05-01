# Orion OS

> A framework for orchestrating AI agent teams that build real software.

Orion OS is not a chatbot. It is a working methodology: roles, rules, memory,
decisions, and workflows for using AI agents as a real engineering team.

It runs today on top of Claude + GitHub MCP + markdown files.
It is evolving toward a web product anyone can use without technical knowledge.

---

## Core idea

You don't manage AI by giving it tasks.
You manage AI by giving it **context, rules, and a place to write things down**.

Orion OS provides the structure:

- **Roles** — Architect, Tech Leads, QA. Each agent has a defined scope.
- **Decisions** — every architectural choice is logged and reversible.
- **Workflows** — repeatable procedures for common operations.
- **Skills** — framework-specific patterns loaded on demand.
- **Memory** — markdown files the agents read at the start of every session.

---

## Two layers

```
System layer   → workflows, skills, templates, decisions (this repo)
Instance layer → projects, logs, personal decisions (your private fork)
```

This repo is the **system layer**. To use Orion OS you create your own private
instance — a fork or new repo where your projects, logs, and personal context live.

---

## Status

Current version: **v2.0.0** — system layer extracted, public repo born.

Roadmap:
- **v2.x** — refine the system layer based on real usage
- **v3.0.0** — web interface, anyone uses Orion OS without setup

See [ROADMAP.md](./ROADMAP.md) for details.

---

## How to use it (today, technical)

> v2.0.0 is for technical users comfortable with markdown, git, and Claude.
> v3.0.0 will remove this requirement.

1. Create your own private repo as an Orion OS instance
2. Copy the structure from this repo into yours
3. Connect Claude (claude.ai or Desktop) to your repo via GitHub MCP
4. Tell Claude: *"despierta Orion"* — it reads ORION.md and starts working

A complete getting-started guide is being migrated from the private instance
in v2.x. Until then, this README is the entry point.

---

## Decisions framework

Every technical decision in Orion OS follows **D89 — reversible by default**.

When two options exist, always choose the one that doesn't close doors for
the future. If a decision is irreversible, document it explicitly and justify it.

See [DECISIONS.md](./DECISIONS.md) for the full set of universal decisions
that govern every project built with Orion OS.

---

## Repository structure

```
agents/      → role definitions (architect, tech leads, QA)
skills/      → framework patterns (angular, react, etc.)
workflows/   → repeatable procedures
templates/   → reusable file templates
examples/    → real anonymized projects showing Orion OS in use
DECISIONS.md → universal decisions
ROADMAP.md   → vision and direction
MIGRATION.md → how this repo came to be
```

Most subdirectories are being populated incrementally from the private
instance during v2.x. Each migration is a deliberate, reviewed step —
not a bulk dump.

---

## Why public?

Orion OS started as one founder's private system to coordinate AI agents
across multiple software projects. It worked. The next step is making it
work for anyone.

This repo is the system in its current form — extracted, generalized,
and opened. It is incomplete on purpose: each piece is migrated only
after it has proven useful in real projects.

---

## License

MIT. See [LICENSE](./LICENSE).
