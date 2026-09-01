---
name: architecture-design
description: Use when the user asks for a new architecture, architecture plan, domain model, module boundary, system shape, or targeted architecture improvement.
---

# Architecture design

Purpose determines structure. Design from the domain outward. Produce a
concrete shape whose boundaries an implementer can use without
rediscovering ownership, failure, or change.

1. **Classify the job:** new project, existing-codebase redesign, or
   targeted improvement. State the primary decision.
2. **Map the domain:** nouns, verbs, lifecycle states, invariants,
   policies, events, ownership centers, and external shapes. Separate
   domain concepts from DTOs, database records, framework objects, and
   UI state.
3. **Design boundaries:** place them where responsibility, ownership,
   lifecycle, consistency, failure, or independent change actually
   differ. Each module gets one responsibility, a small public
   interface, owned data, dependencies, and failure modes. Make
   dependency direction and cross-boundary contracts explicit. Prefer
   forms native to the existing stack and conventions unless the
   problem requires a different shape.
4. **Plan slices:** the smallest end-to-end behavior. For existing code,
   change carefully: preserve compatibility and move one workflow or
   boundary at a time. Name adapters, deletion points, migration
   steps, and rollback notes when risk requires them. Do not add
   extension points for a future that is not here.
5. **Pressure-test:** hardest workflow, failure path, migration,
   concurrency case, integration outage, and likely next feature. Look
   for shallow wrappers, duplicate invariant owners, cycles, hidden
   shared state, and abstractions that have not earned their keep.
   Operational behavior and failure are part of the design, not
   afterthoughts.

If the goals or constraints are unclear, invoke `brainstorming`. If the
user asks for pressure testing, invoke `grill-me`. Use `hyperplan` for a
separate hostile architecture and delivery verdict.

Return:

```text
Context
Goals
Non-goals
Domain and ownership
Modules and contracts
Dependencies and failures
Vertical slices
Tradeoffs
Verification
Risks
```

State rejected alternatives when the decision is significant. Prefer the
smallest boundary change that removes the current pain. Keep necessary
complexity; remove structure that has no job.
