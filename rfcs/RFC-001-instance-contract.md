# RFC-001 — Instance Contract

> **Status:** 🟡 Open
> **Author:** Mario Vidal + Orion
> **Opened:** May 1, 2026 (Session 33, immediately after v2.0.0)
> **Target version:** v2.x (no specific minor yet)

---

## Summary

How does an Orion OS instance (private repo holding `projects/`, `logs/`, etc.)
relate to the Orion OS system layer (this public repo)? What is the contract
between them — versioning, updates, source of truth?

This RFC exists because v2.0.0 split the system layer into a public repo
without yet defining how instances depend on it. The split itself is correct.
The relationship is not yet designed.

---

## Context

Until v1.5.0 there was a single private repo where everything lived together:
agents, skills, workflows, decisions, projects, logs. There was no contract
to define because everything was one thing.

v2.0.0 created `Mjosuex85/orion-os` (this repo) as the public system layer.
Instances now live separately as private repos. The first such instance is
`Mjosuex85/orion`, used by Mario for projects like GameOn and NutriApp.

This raises three concrete questions:

1. **New instance bootstrap.**
   When someone creates a new instance for a new project, how does Orion
   know which version of the system layer to use, and how does it maintain
   coherence between universal decisions (in this repo) and project-specific
   decisions (in the instance)?

2. **System-layer-only updates.**
   When working inside an instance on a real project, only project-related
   files change. Does Orion still know how to work the same way in any
   v2.0.0-compliant instance? What guarantees this?

3. **System layer evolution.**
   When this repo gets updated (a new universal decision, a renamed workflow,
   a deprecated skill), what happens to instances that already exist? Today
   the answer is: nothing. They don't find out.

---

## The core architectural question

> **Is an instance a *fork* of the system layer, or a *consumer* of it?**

The two ends of the spectrum:

### Fork model
The instance contains its own copy of the system layer (agents, skills,
workflows, templates, universal decisions). When the public repo evolves,
the instance must merge or cherry-pick those changes itself. The instance
is fully autonomous — it works even if the public repo disappears.

- ✅ Resilient: each instance functions in isolation.
- ❌ Updates are manual, recurring work for every instance owner.
- ❌ Instances drift over time. Two instances of "v2.0.0" may not match.
- ❌ Hard to scale to v3.0.0 (every web user would have a fork to maintain).

### Consumer model
The instance contains only the instance layer (`projects/`, `logs/`, personal
context). At session start, Orion reads the system layer directly from the
public repo, like a runtime dependency.

- ✅ All instances always have the latest system.
- ❌ Instance is no longer self-contained. Public repo changes can break
  every instance simultaneously.
- ❌ No way to pin an instance to an older system version.
- ❌ Offline use becomes harder.

### Hybrid model (preliminary intuition, not yet decided)
The instance declares an explicit version of the system layer, e.g.

```
# orion-os.manifest.yml (in instance repo root)
orion_os_version: 2.0.0
```

At session start, Orion:
1. Reads the manifest.
2. Reads the system layer at the matching tag of this public repo.
3. Notifies the founder if a newer system version exists.
4. The founder decides when to upgrade — through a documented upgrade flow.

This is how mature frameworks handle the same problem (Angular, Rust, Python).
It is the model most aligned with **D89 (reversible by default)**: the founder
controls the upgrade pace, instances stay stable, and a future v3.0.0 web
product can use the exact same mechanism (the web app reads `orion_os_version`
from the user's config and serves the right system layer).

---

## Failure modes the contract must prevent

These are the silent breakages observed or anticipated in v2.0.0 today:

1. **Silent drift.** A decision made inside a single instance that should have
   been universal never gets promoted. Future instances lack it.
2. **Skill contamination.** A skill in the public repo accidentally containing
   project-specific references propagates to every future instance.
3. **Untracked instance version.** No instance currently declares which
   system version it targets. Two "v2.0.0 instances" may diverge without
   anyone noticing.
4. **Update blindness.** When the public system layer evolves, existing
   instances don't learn about it.
5. **Promotion ambiguity.** No formal protocol decides what stays in
   `projects/<n>-decisions.md` vs. what moves to universal `DECISIONS.md`
   and then to the public repo.

---

## What this RFC does NOT decide

- The actual sync mechanism between instances and the public repo.
  (That is RFC-XXX, future. This RFC is upstream of it.)
- The exact format of the manifest file.
- The upgrade protocol's UX.
- Whether instances should also pin individual skills/workflows separately.

---

## Options to consider in resolution

When this RFC moves to discussion, the resolution must answer at minimum:

1. Fork vs Consumer vs Hybrid — which model?
2. How does an instance declare its system version?
3. What is the bootstrap flow for a brand-new instance?
4. What is the upgrade flow for an existing instance when the public layer evolves?
5. What is the promotion protocol for a decision that starts local and proves universal?
6. How does Orion verify, at session start, that an instance is coherent
   with its declared system version?

---

## Constraints any resolution must satisfy

- **D89 — Reversible by default.** The chosen model must not block v3.0.0.
- **D94 — System and instance never mix.** Any mechanism preserves this.
- **D90 — Scaffold via GitHub API/MCP, never terminal.** The mechanism
  must work in a future web context where the user has no terminal.
- **Realistic for Mario today.** Whatever is decided, Mario must be able to
  operate it without ceremony. If it requires three new commands and a
  Python script, it is the wrong design.

---

## Process

This RFC stays open through v2.x while real migrations happen
(`agents/` first, then `templates/`, then `workflows/`, etc.). Each
migration is a data point about how the system and instance actually
interact. Premature resolution would close the RFC before the data
arrives.

The RFC is expected to resolve **before v3.0.0 begins** — because v3.0.0
cannot be designed without an answer.

---

## Related

- v2.0.0 release notes (this repo, MIGRATION.md)
- D89, D94, D95 (this repo, DECISIONS.md)
- ROADMAP.md → Open Question #7

---

*RFC-001 — opened the day v2.0.0 shipped, intentionally.*
