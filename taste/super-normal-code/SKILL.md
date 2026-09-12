---
name: super-normal-code
description: Apply clear, ordinary code style when designing, implementing, refactoring, reviewing, or simplifying code.
---

# Super Normal Code

Build the smallest clear change that solves the current problem and fits the
codebase. Prefer reuse and ordinary language or platform features over new
structure. Do not chase brevity when it hides behavior or safety.

## Decide before adding

Stop at the first option that works well enough:

1. Remove features, layers, configuration, and future structure the task does
   not need.
2. Reuse existing helpers, types, patterns, names, and boundaries.
3. Prefer the standard library, platform features, then already-installed
   dependencies. Do not add a package for a few clear lines.
4. Use direct control flow and explicit results.
5. Add only the smallest new structure that earns its cost now.

An abstraction is justified by a real domain rule, owned state or invariants,
variation, side effect, boundary, multiple consumers, or a useful test seam.
An imagined future is not enough. Apply the same test to mocks and test
helpers.

## Keep the path clear

- Use one term per concept and one job per block.
- Prefer plain functions for stateless work; use an object when it owns state,
  invariants, lifecycle, or a real application boundary.
- Use a facade only to hide a real subsystem.
- Prefer early returns and flat control flow. More than three levels of
  indentation is a smell, not an automatic failure; flatten only when the
  result is clearer and fits local style.
- Prefer short functions, few locals, one statement per line, and explicit
  failure paths. A long flat table or switch can be clearer than premature
  helpers.
- Comment intent, invariants, and non-obvious constraints, not the code line
  by line.
- Keep validation, authorization, observability, retries, transactions,
  compatibility, security boundaries, and domain invariants when they protect
  real behavior.

## Deliberate shortcuts

When a simple choice has a known ceiling, mark it with:

    // limit: what breaks or gets slow; upgrade when measurable trigger

Do not mark ordinary simple code. Use shortcut-debt to list these markers.

## Change and verify

Read the relevant callers, tests, data shapes, side effects, errors,
ownership, and external contracts before editing. For a bug, fix the shared
owner when possible instead of adding sibling guards.

Check observable behavior, boundary inputs, failures, and regressions. New
non-trivial logic should leave one small runnable check; trivial one-liners
need none. Widen checks for shared code or important boundaries.

Before finishing, ask whether a clearer ordinary approach would work, whether
each abstraction pays for itself, and whether needed safeguards remain.
Report the solution first and mention meaningful omissions or limits briefly.
