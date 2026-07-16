---
name: simplify-codebase
description: Simplify code and tests for emergency readability without changing behavior, weakening reuse, or damaging architecture. Use when the user asks to simplify/refactor code, apply clean code, make code or tests on-call friendly, remove boilerplate or test noise, reduce implementation-coupled tests, or improve behavior-focused coverage.
---

# Simplify Codebase

Make the requested code boring enough that an on-call engineer can trace, change, and trust it. Boring means obvious control flow, simple data, local names, and boundaries that earn their cost.

This is not deletion for its own sake. Preserve behavior and the architecture that carries real responsibility.

## The earned rule

Prefer plain functions, simple data objects, concrete dependencies, and visible state.

Keep or introduce an object, interface, factory, strategy, configuration knob, dependency, retry, or test case only when it earns its cost through a current responsibility or boundary:

- ownership, lifecycle, state, or a business invariant;
- a stable public or compatibility boundary;
- multiple real implementations or policies that vary now;
- an external dependency, side effect, or necessary test seam;
- an existing codebase pattern that makes the surrounding code clearer.

Do not add an abstraction for imagined reuse, scale, flexibility, or a future mode.

## Workflow

1. Find the contract.
   - Read the public entrypoints, callers, tests, logs, docs, and data shapes touched by the change.
   - Name the behavior, side effects, errors, observability, and compatibility concerns that must not change.
   - Completion: every in-scope external behavior is listed or intentionally ruled out.

2. Mark unearned complexity.
   - Identify deep nesting, hidden mutation, unclear ownership, boolean mazes, temporal coupling, broad helpers, duplicated branches, and layers that merely rename work.
   - Use the earned rule to separate accidental complexity from essential domain or architecture complexity.
   - Completion: each target has a concrete reading, debugging, or change cost.

3. Simplify in small slices.
   - Prefer straight-line code, guard clauses, named intermediate values, table-driven decisions, and small single-purpose functions.
   - Keep data close to its owner. Inline a helper that hides more than it explains; extract one when its name removes real mental state.
   - Prefer direct calls and concrete dependencies. Keep SOLID-style objects and seams when they express a real current boundary or fit the codebase.
   - Completion: each slice preserves behavior, is reviewable alone, and is tested or inspected before the next slice.

4. Preserve the load-bearing path.
   - Keep stable public APIs unless the user requested a change.
   - Keep domain types, module boundaries, dependency injection, error semantics, observability, and reuse that earn their cost.
   - Do not simplify by removing validation, useful error paths, logging, metrics, authorization, transactions, required retries, or compatibility behavior.
   - Completion: every removed abstraction is unused, duplicated, or unearned; every kept boundary has a clear job.

5. Verify from the outside.
   - Run focused tests first, then broader tests when the blast radius is shared.
   - Inspect output, logs, generated payloads, migrations, or CLI text when they are part of the contract.
   - Completion: verification covers the contract from step 1, or the final response states the exact gap.

## Boring Code Rules

- Keep nesting shallow with guard clauses or clear dispatch.
- Make state and ownership visible. Avoid hidden mutation, global reads, and callback-driven control flow unless the boundary earns them.
- Use names that reveal intent, domain language, and side effects.
- Prefer local reasoning. A reader should not need to open several files to understand an ordinary branch.
- Reduce concepts before reducing lines. Obvious ownership is better than compressed code that hides policy.
- Keep failures distinct and operational. Error paths, logs, and metrics are part of the code's contract.
- Prefer language and standard-library idioms over custom machinery. In Go/C-like code, favor small functions, explicit ownership, clear error handling, simple structs, and table-driven cases.

## Tests and Coverage

- Keep tests for public behavior, business rules, failures, compatibility, and real regressions.
- Remove or rewrite tests that only prove mock calls or private implementation steps without a useful outcome.
- Keep focused tests for real boundaries such as parsing, rendering, retries, permissions, deterministic time, serialization, or external integrations.
- Add a case only for a distinct branch, boundary, invariant, failure mode, data shape, permission, or regression. Do not repeat the same path for a coverage percentage.
- When deleting a test, state what still covers the behavior or why the old assertion had no behavioral value.

## Review Gate

Before finishing, check:

- Can a tired engineer find the main path in under a minute?
- Are state changes and failure paths explicit?
- Does every remaining abstraction earn its cost?
- Did the code retain real ownership, reuse, and architecture boundaries?
- Do tests prove behavior and cover distinct paths?
- Did verification prove the contract stayed the same?

Continue simplifying if an answer is no, or state the remaining risk clearly.
