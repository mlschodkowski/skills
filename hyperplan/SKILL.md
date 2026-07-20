---
name: hyperplan
description: Tear apart a plan before implementation by running 2 hostile subagents from orthogonal angles. Use when the user wants to stress-test a plan, spec, or design before writing code, or says "hyperplan".
---

Find the plan's real weaknesses.

Apply the [plain writing standard](../references/plain-writing.md) to the critique. Be direct without exaggeration.

If there is no plan yet, stop.

## RUNING
Run **2 hostile subagents in parallel**:

1. **Architecture attacker** — attack assumptions, design, coupling, edge cases, failure modes, and rollback.
2. **Delivery attacker** — attack sequencing, scope, testing, rollout, observability, and hidden work.

The two subagents must come at the plan from different angles. They should be sharp, skeptical, and focused on finding real weaknesses.

## RESULTS
Then synthesize the results into:

- **Verdict:** blocked, risky, or ready
- **Architecture attack**
- **Delivery attack**
- **Required plan changes**
- **Safe next move**

Do not write implementation code until this critique is done.
