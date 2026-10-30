---
name: explain-code
description: Explain how a code path, subsystem, or architecture works, including runtime flow, ownership, and where a change belongs. Use for code walkthroughs, ownership questions, and domain or module design.
---

# How it works

Read [stack rules](../mlstack/references/rules.md).

1. Identify the question and entry point. Read the relevant domain terms and
   architecture decisions when present. Start with a narrow interpretation
   and state it when scope is unclear.
2. Follow real calls through data, state ownership, effects, errors, and
   recovery. Check configuration and tests that affect runtime behavior.
3. Explain the subsystem's job, main concepts, runtime sequence, and ownership.
   Cite paths and symbols. Use a small diagram only when it makes the flow clearer.
4. Name important constraints and gotchas. Distinguish source facts from runtime
   assumptions and unobserved behavior. For placement questions, recommend the
   existing boundary that owns the rule and state what would change the choice.

Keep the explanation at the level needed to make a change safely. A walkthrough
does not authorize edits, new architecture documents, or a refactor.

## When the model needs work

Name entities, states, transitions, invariants, and the owner of each effect.
Check concrete valid, invalid, repeated, and partially failed scenarios. Prefer
a data structure that represents the real rules over flags that must stay in
sync. Keep a direct conditional when a new abstraction buys no real guarantee.

Read [module-design.md](references/module-design.md) when choosing an interface
or test seam, and [module-dependencies.md](references/module-dependencies.md) when
external dependencies affect that choice. A deep module hides real complexity
behind a small interface; it does not need a large wrapper hierarchy.

For an alternative design, compare two materially different interfaces in the
current agent. State invariants, a caller example, hidden effects, test surface,
and tradeoffs. Recommend one. No model roster or delegation is required.

A design discussion does not authorize a refactor, glossary rewrite, or ADR.
When implementation is requested, use [clean-code](../clean-code/SKILL.md)
and [tdd](../tdd/SKILL.md) within the agreed scope.
