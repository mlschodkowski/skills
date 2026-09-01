---
name: autonoma-code
description: >
  Use when designing, implementing, refactoring, reviewing, or simplifying
  code, tests, or software architecture. Prefer form that follows from
  purpose, context, real boundaries, and use. Keep accidental complexity
  low; keep necessary complexity. Favor explicit mechanisms, legible
  relationships, and change through stable boundaries.
---

# Autonoma Code

Taste for code. Shared principles:
[autonoma-principles.md](../autonoma-principles.md). This skill is the
code application.

Build the change whose structure can be explained by real requirements,
relationships, constraints, and use — not by fashion, abstraction for its
own sake, or taste performance.

Complexity is acceptable when the problem requires it. Prefer the
smallest mechanism that still satisfies correctness, operability, and
localized change.

## Decision ladder

Stop at the first step that works well enough.

1. **Does this need to exist?**
   Drop features, layers, config, and speculative structure with no job.
   Do not remove structure merely because it looks complex if it
   corresponds to a real responsibility.

2. **Is the form already native to this context?**
   Reuse helpers, types, patterns, names, and boundaries when they fit.
   Follow local conventions unless there is a concrete reason not to.

3. **Does the language, stdlib, platform, or an installed dependency already do it?**
   Prefer in order: standard library → platform feature → already-installed
   dependency. Do not add a package for a few clear lines.

4. **Can an explicit ordinary mechanism solve it?**
   Prefer plain functions, direct control flow, and explicit results over
   frameworks or indirection that add no capability.

5. **Only then add structure.**
   Smallest change that improves the system now. Abstraction when a
   stable concept, repeated behavior, or meaningful boundary justifies it.

## Clear code

Match the codebase's boundaries, names, and style.

- Purpose determines structure: one term per concept; one job per block.
- Make relationships legible: ownership, dependency direction, and data
  flow should be readable from names, types, and layout.
- Rename unclear local or private symbols. Keep public names and behavior.
- Prefer plain functions for stateless work.
- Use an object or service when it owns state, invariants, lifecycle, or
  a real application boundary.
- Use a facade only to hide a real subsystem.
- Do not add classes, interfaces, factories, wrappers, or config only to
  group functions or prepare for a future that is not here.
- Do not make impossible or unrelated state combinations representable.
- Prefer at most **3 levels** of control-flow indent in a function (the
  body counts as level 1). Flatten when a clearer shape is easy. Do not
  "fix" depth by packing logic into one dense line.
- Prefer short functions that do one job. A longer function is fine when
  the body is flat and repetitive. Split when the logic is deep or hard
  to hold in mind.
- Prefer few locals. Prefer one statement per line.
- Comment intent, invariants, and non-obvious constraints — not a
  line-by-line how.
- When several failure paths need the same teardown, share one cleanup
  path.
- Name functions so success and failure are obvious.
- Prefer helpers that do not secretly exit the caller's control flow.
- Prefer quiet success. Log or measure failures and real state changes.

## Abstraction and boundaries

Judge only abstractions touched by this task.

Add abstraction when it stands for something real: a domain rule, a real
boundary, owned state or invariants, real variation, a side effect, a
concept with more than one real consumer, a real test seam.

Boundaries should follow ownership, responsibility, lifecycle,
consistency, security, deployment, or independent change — not diagram
aesthetics.

Preserve information until there is a reason to hide it. Hide details
consumers should not depend on; keep contracts, state transitions, and
important failure modes observable.

For each abstraction in scope: keep, simplify, defer, or remove. If you
defer, name the concrete trigger. Apply the same test to test helpers
and mocks.

### Deliberate shortcuts

Sometimes the simple approach is right now, but it has a known limit.
Mark that limit and the condition that should force a better design:

```text
// limit: <what breaks or gets slow>; upgrade when <measurable trigger>
```

Without a trigger, "we'll fix it later" is forgotten. Do not mark
ordinary simple code. To list markers later, use `$shortcut-debt`.

## Change discipline

Change existing things carefully. Read enough of the surrounding system
before editing: responsibilities, consumers, dependencies, invariants,
and observable behavior.

Prefer localized corrections when the problem is localized. Broader
redesign when the structure itself prevents the required behavior.

For bugs, fix the shared owner of the mistake when you can. Before
adding a guard at one call site, check the other callers.

Design for change through stable boundaries, not universal extensibility.
An extension point for an imaginary future is accidental complexity now.

Keep complexity that protects real behavior: validation at trust
boundaries, authorization, observability, retries and transactions where
required, domain rules, error handling, compatibility, security.

Treat operational behavior as part of the design: startup, shutdown,
config, failure, recovery, migration. Design for failure deliberately —
do not let failure semantics emerge by accident.

## Verification

Check behavior and output, not private structure.

Cover the boundaries, failures, and regressions this change can break.
Widen checks when you touch shared code or important boundaries.

New non-trivial logic (branch, loop, parser, money, auth) should leave
one small runnable check that fails if that logic breaks. Prefer the
repo's test style. Trivial one-liners need none.

Looking simpler is not success. The result must be correct, legible,
operable, and safe to change.

## Before you finish

- Does every significant structural element have a job?
- Does this fit the native form of the codebase?
- Do boundaries and relationships correspond to reality?
- Did abstractions earn their existence?
- Are contracts and failure modes explicit enough?
- Did you remove accidental complexity without removing necessary
  completeness?
- Would a specialist call this ordinary and correct for the problem?

Lead with the solution. At most three short lines on what you left out
or simplified, and why.

Do not pull in other skills unless their own triggers match or the user
asks.
