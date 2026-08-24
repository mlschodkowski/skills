---
name: super-normal-code
description: >
  Use when designing, implementing, refactoring, reviewing, or simplifying
  code, tests, or software architecture. Prefer clear, ordinary solutions that
  fit the codebase. Avoid extra abstraction and invention unless the current
  task needs them. Keep correctness, contracts, behavior, and real system
  boundaries.
---

# Super Normal Code

Taste for code. Shared principles:
[super-normal-principles.md](../super-normal-principles.md). This skill
is the code application.

Build the smallest clear change that solves the current problem and fits
this codebase. Prefer reuse and ordinary language features over new
structure. Do not chase the shortest possible code when that hurts
clarity or safety.

## Decision ladder

Stop at the first step that works well enough.

1. **Does this need to exist?**
   Drop features, layers, config, and "for later" structure the task does
   not need. Unfamiliar is not the same as unnecessary.

2. **Is it already in this codebase?**
   Reuse helpers, types, patterns, names, and boundaries when they fit.

3. **Does the language, stdlib, platform, or an installed dependency already do it?**
   Prefer in order: standard library → platform feature → already-installed
   dependency. Do not add a package for a few clear lines.

4. **Can clearer code solve it without new structure?**
   Prefer plain names, direct control flow, and explicit results.

5. **Only then add structure.**
   Smallest change that improves the system now. No new dependency,
   config, or layer unless this task needs it.

Change an existing convention when it is unclear, brittle, or adds
needless complexity. Keep it when it is working and understood.

## Clear code

Match the codebase's boundaries, names, and style.

- One term per concept. One job per block.
- Rename unclear local or private symbols. Keep public names and behavior.
- Prefer plain functions for stateless work.
- Use an object or service when it owns state, invariants, lifecycle, or
  a real application boundary.
- Use a facade only to hide a real subsystem.
- Do not add classes, interfaces, factories, wrappers, or config only to
  group functions or prepare for a future that is not here.
- Do not make impossible or unrelated state combinations representable.
- A slightly longer clear version beats a clever one-liner that hides
  meaning.
- Prefer at most **3 levels** of control-flow indent in a function (the
  body counts as level 1). Deeper nesting is a smell, not an automatic
  reject. Flatten when a clearer shape is easy (early return, guard,
  inverted condition, small named helper). Do not "fix" depth by packing
  logic into one dense line. Nested callbacks or block-bodied lambdas
  count toward the depth. Keep deeper nesting when the flatter form would
  be worse or fight local style.
- Prefer short functions that do one job. A longer function is fine when
  the body is flat and repetitive (a big switch or table). Split when the
  logic is deep or hard to hold in mind.
- Prefer few locals. A long list of locals usually means the function is
  doing too much.
- Prefer one statement per line. Do not hide control flow in commas,
  stacked assignments, or dense boolean piles.
- Comment what and why: intent, invariants, non-obvious constraints. Not
  a line-by-line how. If the body needs a tour, simplify the body.
- When several failure paths need the same teardown, share one cleanup
  path instead of copying it.
- Name functions so success and failure are obvious (predicate vs
  find/get that may miss).
- Prefer helpers that do not secretly exit the caller's control flow.
- Prefer quiet success. Log or measure failures and real state changes.

## Abstraction

Judge only abstractions touched by this task. A small local helper that
makes the path readable is fine.

Add abstraction when it stands for something real: a domain rule, a real
boundary, owned state or invariants, real variation, a side effect, a
concept with more than one real consumer, a real test seam.

For each abstraction in scope: keep, simplify, defer, or remove. A
future maybe is not a current need. If you defer, name the concrete
trigger. Apply the same test to test helpers and mocks.

### Deliberate shortcuts

Sometimes the simple approach is right now, but it has a known limit
(for example a global lock, an O(n²) scan, or a naive heuristic). Mark
that limit and the condition that should force a better design:

```text
// limit: <what breaks or gets slow>; upgrade when <measurable trigger>
```

Example:

```text
// limit: one global lock; upgrade when lock wait shows up in profiles
```

Without a trigger, "we'll fix it later" is forgotten. The marker is a
ticket in the code. Do not mark ordinary simple code. To list markers
later, use `$shortcut-debt`.

## Change discipline

Read enough of the surrounding system before editing. Shrink the fix
after you understand the path, not by skipping the reading.

Check callers, tests, data shapes, side effects, errors, compatibility,
ownership, and external contracts when they matter.

For bugs, fix the shared owner of the mistake when you can. Before
adding a guard at one call site, check the other callers of the same
function.

Keep complexity that protects real behavior: validation at trust
boundaries, authorization, observability, retries and transactions where
required, domain rules and invariants, error handling, compatibility,
security boundaries.

Remove complexity that does not earn its cost. If ownership or behavior
is unclear, ask.

## Verification

Check behavior and output, not private structure.

Cover the boundaries, failures, and regressions this change can break.
Widen checks when you touch shared code or important boundaries.

New non-trivial logic (branch, loop, parser, money, auth) should leave
one small runnable check that fails if that logic breaks. Prefer the
repo's test style. Trivial one-liners need none. Do not add test
framework ceremony for a local proof.

Looking simpler is not success. The result must be correct, readable,
and safe to change.

## Before you finish

- Would a clearer ordinary approach work?
- Does this fit the existing codebase?
- Does every abstraction pay for itself?
- Is the behavior obvious from the code?
- Did you remove noise without removing needed safeguards?
- Will this still be easy to change in a few months?

Lead with the solution. At most three short lines on what you left out
or simplified, and why.

Do not pull in other skills unless their own triggers match or the user
asks.
