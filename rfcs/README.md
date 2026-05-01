# RFCs — Orion OS

This directory holds Request For Comments documents — open architectural
questions that need discussion before becoming decisions.

## What is an RFC

An RFC opens a problem that affects the system layer. It does not solve it
right away. It frames the problem so that real usage produces the data
needed to decide.

A typical RFC moves through three states:

```
🟡 Open       → problem framed, options sketched, decision pending
🟢 Decided    → resolved, links to the resulting decisions/changes
🔴 Withdrawn  → problem dissolved, abandoned, or replaced by another RFC
```

RFCs are never deleted. A withdrawn RFC keeps its trace.

## When to open an RFC

- The question affects the system layer (this repo), not just one instance.
- The answer cannot be decided in a single session — it needs observation.
- The eventual decision will likely modify `DECISIONS.md` or introduce
  new universal rules.

## When NOT to open an RFC

- The question is project-specific (it goes to that project's decisions file).
- The answer is obvious and reversible (just decide, no ceremony needed).
- The RFC would only restate something already in `DECISIONS.md`.

## Index

| ID | Title | Status |
|----|-------|--------|
| [RFC-001](./RFC-001-instance-contract.md) | Instance Contract | 🟡 Open |

---

*RFCs are how Orion OS makes decisions it cannot yet make.*
