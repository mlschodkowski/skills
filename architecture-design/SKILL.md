---
name: architecture-design
description: Use when the user asks for a new architecture, architecture plan, domain model, module boundary, system shape, or targeted architecture improvement.
---

# Architecture Design

Design from the domain outward. Produce a concrete shape that a future implementer can use without rediscovering the boundaries.

1. **Classify the job:** new project, existing-codebase redesign, or targeted improvement. State the primary decision.
2. **Map the domain:** name nouns, verbs, lifecycle states, invariants, policies, events, ownership centers, and external shapes. Separate domain concepts from DTOs, database records, framework objects, and UI state.
3. **Design boundaries:** give each module one responsibility, a small public interface, owned data, dependencies, and failure modes. Make dependency direction and cross-boundary contracts explicit.
4. **Plan slices:** choose the smallest end-to-end behavior. For existing code, preserve compatibility and move one workflow or boundary at a time. Name adapters, deletion points, migration steps, and rollback notes when risk requires them.
5. **Pressure-test:** check the hardest workflow, failure path, migration, concurrency case, integration outage, and likely next feature. Identify shallow wrappers, duplicate invariant owners, cycles, and hidden shared state.

If the goals or constraints are unclear, invoke `brainstorming`. If the user asks for pressure testing, invoke `grill-me`. Use `hyperplan` for a separate hostile architecture and delivery verdict.

Return:

```text
CONTEXT:
GOALS:
NON_GOALS:
DOMAIN_AND_OWNERSHIP:
MODULES_AND_CONTRACTS:
DEPENDENCIES_AND_FAILURES:
VERTICAL_SLICES:
TRADEOFFS:
VERIFICATION:
RISKS:
```

State rejected alternatives when the decision is significant. Prefer the smallest boundary change that removes the current pain.
