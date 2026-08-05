---
name: abstraction-audit
description: Use when a coding task, diff, or design creates, changes, or proposes abstractions and their responsibility, cost, or current need must be decided.
---

# Abstraction Audit

Audit every abstraction in scope. Do not audit unrelated existing code merely because you encountered it.

Treat types, objects, interfaces, factories, layers, policy objects, configuration, dependencies, retries, state, and test seams as abstractions when they hide a boundary, policy, or meaningful behavior. Ignore ordinary local helpers that only make direct code readable.

For each abstraction:

1. Read the task, diff, entrypoints, callers, tests, data shapes, and existing boundaries needed to establish its contract.
2. State its current responsibility and the boundary it protects.
3. State its cost: indirection, state, coupling, configuration, dependency, or test burden.
4. Decide `keep`, `simplify`, `defer`, or `remove`. A future possibility is not a current need; name the concrete trigger if deferring.

Apply the same test to fixtures, mocks, builders, and test seams. Keep them only when they clarify a real boundary or repeated current setup.

Return one short row per item:

| Abstraction | Responsibility and need now | Cost | Decision |
| --- | --- | --- | --- |
| `Name` | What it owns or protects; why it is needed now | Extra complexity | Keep, simplify, defer, or remove; next action |

Use evidence from the code and state uncertainty instead of guessing.
