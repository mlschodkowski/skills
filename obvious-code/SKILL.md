---
name: obvious-code
description: Use when code or tests are difficult to read, debug, review, maintain, or trust because names, control flow, ownership, side effects, or abstractions force the reader to infer behavior.
---

# Obvious Code

Obvious code is readable code: make behavior easy to follow, review, and safely
change.

Occam's razor is usually good approach.

Fit the existing codebase first. Match its boundaries and conventions. Choose
the simplest local structure: use procedural functions for direct stateless
flows; use an object or service for owned state, invariants, lifecycle, or a
cohesive application boundary. Use a facade only when it hides a real subsystem
boundary. Do not add classes or facades only to group functions or imitate a
paradigm.

Use clear names, one term per concept, direct control flow, explicit conditions
and results, and one responsibility per block.
Rename unclear local/private symbols; preserve external names and behavior.

Before editing, map callers, tests, data shapes, side effects, errors,
compatibility, and contracts. Keep abstractions for rules, boundaries,
variations, side effects, or test seams. Preserve validation,
authorization, observability, retries, transactions, domain logic, errors, and
compatibility.

Verify behavior and output; broaden checks for shared code. Test behavior,
boundaries, invariants, failures, permissions, and regressions, not private
steps.

Do not introduce abstractions that don't make sense. For example don't create classes with multiple
members which combination does not make sense. There should be no code having
an impossible or improper state.

Ask when behavior, ownership, or boundaries differ; choose the smallest clear
change.

Examples: [examples.md](references/examples.md).

Use `tdd`, `abstraction-audit`, and `simple-language` only when their own
triggers match or the user invokes them. Do not force a chain of skills.
