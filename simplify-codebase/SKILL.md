---
name: simplify-codebase
description: Simplify code for emergency readability without changing behavior, weakening reuse, or damaging architecture. Use when the user asks to simplify, reduce complexity, flatten control flow, remove boilerplate, make code on-call friendly, clean up a codebase, or review/refactor code specifically for clarity under pressure.
---

# Simplify Codebase

## Aim

Make the code boring enough that an on-call engineer woken up at night can trace it, change it, and trust it. Boring means obvious control flow, local names, few moving parts, and preserved boundaries.

This is not minimalism by deletion. Keep the abstractions, reuse, tests, and architecture that carry real weight.

## Workflow

1. Find the contract.
   - Read the public entrypoints, tests, callers, logs, docs, and data shapes touched by the change.
   - Name the behavior that must not change before editing.
   - Completion: every externally visible behavior, side effect, and compatibility concern in scope is listed or intentionally ruled out.

2. Mark complexity.
   - Identify code that forces stack-building in the reader's head: deep nesting, hidden mutation, unclear ownership, boolean mazes, temporal coupling, leaky abstractions, broad helpers, premature configuration, and duplicated branches.
   - Separate accidental complexity from essential domain or architecture complexity.
   - Completion: each simplification target has a concrete reason tied to reading, debugging, or change risk.

3. Simplify in small slices.
   - Prefer straight-line code, guard clauses, table-driven decisions, named intermediate values, small functions, and single-purpose helpers.
   - Keep data close to the code that owns it.
   - Collapse indirection that only renames work.
   - Inline helpers when the call hides more than it explains.
   - Extract helpers when the name removes a real chunk of mental state.
   - Completion: each slice is behavior-preserving, reviewable alone, and can be tested or inspected before the next slice.

4. Preserve the load-bearing shape.
   - Keep stable public APIs unless the user asked to change them.
   - Keep domain types, module boundaries, dependency injection, error semantics, observability, and reusable seams that are used by real callers or tests.
   - Do not flatten a design into procedural code when the abstraction expresses ownership, lifecycle, policy, or a business invariant.
   - Completion: every removed abstraction is proven unused, duplicated, or harmful; every kept abstraction has a clear job.

5. Verify from the outside.
   - Run focused tests first, then broader tests when the blast radius is shared.
   - Inspect output, logs, generated payloads, migrations, or CLI text when those are part of the contract.
   - Completion: verification covers the public behavior named in step 1, or the final answer states the exact gap.

## Boring Code Rules

- Keep nesting shallow. Aim for at most two levels inside a function. Use early returns, extracted decisions, or `match`/switch-style dispatch when branches grow.
- Make state visible. Prefer explicit values over hidden mutation, global reads, or control hidden in callbacks.
- Make names do work. A good name should let the reader skip opening a helper. If it cannot, the helper may be the wrong shape.
- Prefer local reasoning. A reader should not need to inspect five files to understand one branch.
- Reduce concepts before reducing lines. Shorter code that hides policy is worse than longer code with obvious ownership.
- Keep error paths first-class. Do not merge distinct failures into vague fallbacks just to reduce branches.
- Keep logs and metrics operational. Simplification must not remove the breadcrumbs needed during an incident.
- Use standard library and language idioms before custom frameworks. In Go and C-like code, prefer small functions, explicit ownership, clear error handling, and table-driven cases over clever generic machinery.

## Good Deletions

Delete code when it is:

- dead, unreachable, or only defending against impossible states already ruled out by types or earlier validation;
- a pass-through wrapper with no policy, ownership, retry, logging, transaction, authorization, or compatibility role;
- duplicated branch logic that can become one named decision;
- configuration or extension machinery with no real variation;
- comments that restate code instead of preserving a non-obvious business rule.

## Bad Deletions

Do not delete code just because it is verbose when it:

- encodes a domain invariant;
- isolates a dependency, side effect, or failure boundary;
- preserves backward compatibility;
- makes testing deterministic;
- carries observability needed for production support;
- matches a local architecture pattern used elsewhere.

## Review Gate

Before finishing, answer these questions in your own head and reflect any failures in the final response:

- Can a tired engineer find the main path in under a minute?
- Can they tell which state changes before and after the call?
- Are failures explicit and distinguishable?
- Did reuse improve or stay intact?
- Did the architecture get clearer rather than flatter for its own sake?
- Did tests or inspection prove behavior stayed the same?

If any answer is no, continue simplifying or state the remaining risk clearly.
