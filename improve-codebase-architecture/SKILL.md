---
name: improve-codebase-architecture
description: Use when auditing a codebase for architectural friction and proposing deepening opportunities with a visual report.
disable-model-invocation: true
---

# Improve Codebase Architecture

Find real architectural friction and propose deepening opportunities: changes
that put more behavior behind a smaller, cleaner, testable interface. This is
a report workflow; do not implement the refactor during discovery.

Use the vocabulary from [codebase-design](../codebase-design/SKILL.md):
module, interface, depth, seam, adapter, leverage, locality, deletion test,
and interface as test surface. Read the project's CONTEXT.md and nearby ADRs
only when they exist and are relevant to the area under review.

## Discovery

- Follow a direction named by the user. Without one, inspect recent history
  first and let recurring hot spots set the scope.
- Read only the code, tests, contracts, and documentation needed to establish
  the friction and its owner.
- Look for shallow modules, leaked seams, scattered decisions, test surfaces
  that hide real behavior, and unnecessary bouncing between files.
- Apply the deletion test: deleting a suspected wrapper should concentrate
  complexity, not merely move it.
- Use a sub-agent only when a separate bounded read materially improves
  coverage; it is not a required step.

## Report

Read [HTML-REPORT.md](HTML-REPORT.md) when writing the report. Save a
self-contained HTML report in the OS temporary directory, using a fresh
architecture-review timestamped filename. Open it when the environment
supports that action and report its absolute path.

For each candidate, show the involved files, current friction, proposed
deepening, locality and leverage benefits, test impact, recommendation strength,
and a small before/after visual. Use Mermaid only for graph-shaped relationships
and simpler HTML or SVG for other comparisons. End with one top recommendation.
Use the project's domain language and mark any real ADR conflict.

Do not propose interfaces or edit code in the initial report. Finish by asking:
Which of these would you like to explore?

## Follow-up

When the user selects a candidate, continue as a separate decision and design
step. Use available domain-modeling and codebase-design guidance when the
decision actually changes the domain model or module seam. Update CONTEXT.md or
record an ADR only when the workflow reaches a real decision or the user asks;
do not invent a separate questioning workflow.
