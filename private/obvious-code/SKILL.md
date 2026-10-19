---
name: obvious-code
description: Use when code or tests are difficult to read, debug, review, maintain, or trust because names, control flow, ownership, side effects, or abstractions force the reader to infer behavior.
disable-model-invocation: true
---

# Obvious Code

Make behavior, ownership, and dependencies easy to follow, review, and change.

## Process

1. Map the relevant callers, data shapes, state owners, side effects, errors,
   tests, and compatibility contracts before editing.
2. Identify the main behavior and the rules that must remain true.
   Arrange the code so the reader can follow inputs, decisions, effects,
   and results.
3. Fit the existing codebase. Use stable domain terms and consistent patterns
   for comparable operations. Keep differences visible when behavior differs.
4. Choose the smallest structure that expresses the real boundaries.
   Use functions for direct stateless flows. Use an object or service for
   owned state, invariants, lifecycle, or a cohesive application boundary.
   Use a facade when it hides a real subsystem boundary.
5. Keep related decisions and data together. Give each block one coherent
   purpose. Separate responsibilities where ownership, effects, or reasons
   for change differ.
6. Remove indirection, wrappers, options, and abstractions that add no useful
   boundary or understanding. Keep abstractions that protect rules, isolate
   effects, support real variation, or provide a useful test seam.
7. Check the result through the main path and relevant failure paths.
   Verify behavior and output with checks appropriate to the change.

## Clarity rules

Use clear names, direct control flow, explicit conditions and results,
and one term per concept. Rename unclear local or private symbols within
scope. Preserve external names and behavior unless the task changes them.

Use formatting to reveal structure. Keep related statements together and
separate distinct stages. Follow the formatter and local conventions.

Prefer a little repetition when it keeps independent rules clear.
Extract shared code when it represents one rule that should change together.

Preserve validation, authorization, observability, retries, transactions,
domain logic, errors, and compatibility. Reduction is complete only while
the required behavior remains clear and intact.

Test observable behavior, boundaries, invariants, and failures.
Broaden checks when shared code or compatibility is affected.

Ask when unresolved behavior, ownership, or boundary choices would change
the result. State routine assumptions and make the smallest clear change.

Read [examples.md](references/examples.md) when an example would clarify
the choice.

Use `tdd` and `simple-language` when their triggers match or the user invokes
them.
