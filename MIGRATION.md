# MIGRATION.md — How Orion OS v2.0.0 came to be

> This document explains the origin of this repo, its relationship with
> private Orion OS instances, and how the migration from a single private
> repo into a system/instance split was performed.

---

## Origin

Orion OS was developed as one founder's private system over ~32 working sessions
between late 2025 and April 2026. It started as a single private repo that
mixed two layers:

- **System layer** — agents, skills, workflows, templates, universal decisions.
  Reusable across any project, by any user.
- **Instance layer** — specific projects, session logs, personal decisions,
  metrics. Tied to one founder and their products.

By v1.5.0 the system was mature enough that the next reversible step was to
extract the system layer into a public repo. This repo is that extraction.

---

## What lives where

```
This repo (Mjosuex85/orion-os, public)
└── System layer
    ├── agents/      role definitions
    ├── skills/      framework patterns
    ├── workflows/   repeatable procedures
    ├── templates/   reusable file templates
    ├── examples/    anonymized real projects
    └── DECISIONS.md universal decisions

Private instances (e.g. Mjosuex85/orion, private)
└── Instance layer
    ├── projects/    real project state
    ├── logs/        session logs, post-mortems, agent feedback
    ├── metrics/     per-instance metrics
    └── projects/<n>-decisions.md  project-specific decisions
```

---

## How v2.0.0 was created

Per **D89 (reversible by default)** and the v2.0.0 session decisions:

- **Repo strategy:** new repo from scratch, no shared git history with the private
  instance. Reason: the private repo's history contains commits with project names,
  half-finished decisions, and learning sessions. The public repo is a product,
  not a diary. The private repo keeps full history.

- **Genericization:** hybrid. System code is generic ("the founder", "the project").
  `/examples/` contains real projects in anonymized form, so users see what a
  working Orion OS instance actually looks like — not just empty templates.

- **Sync mechanism:** **deferred**. Until we observe the real pattern of changes
  (does DECISIONS.md change more often than skills? do workflows mutate together?)
  we don't pick an automation. The first 2-3 migrations from private to public
  are manual cherry-picks, on purpose. The data tells us what to automate.

---

## Migration plan

v2.0.0 ships as a skeleton: README, LICENSE, ROADMAP, DECISIONS, MIGRATION,
and empty subdirectories.

The actual content (agents, skills, workflows, templates, examples) is being
migrated incrementally during v2.x — file by file, generalized and reviewed.

This is intentional:
- Every migrated file is read carefully and stripped of instance-specific details.
- Every migration is a small experiment that informs the eventual sync mechanism.
- No bulk dumps. Quality over speed.

---

## Creating your own instance

There is no automated path yet (that's v3.0.0). For technical users:

1. Create a private repo for your instance (e.g. `your-name/orion`).
2. Copy this repo's structure into it as a starting point.
3. Add your own `projects/`, `logs/`, `metrics/` directories.
4. Write your `ORION.md` — this is your Orion's memory of you, your team, your work.
5. Connect Claude (claude.ai or Desktop) to your instance via GitHub MCP.
6. Start a session: *"despierta Orion"*.

A proper getting-started guide is part of v2.x migration work.

---

*Orion OS v2.0.0 — born from a working private instance.*
