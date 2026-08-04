---
name: simplify-codebase
description: Use when code or tests are difficult to read, debug, maintain, or trust; when an on-call engineer needs a simpler path; or when a user asks to simplify, refactor, remove boilerplate, or make implementation-focused tests prove behavior.
---

# Simplify Codebase

Make code and tests easy to understand at 3 AM. Reduce cognitive load without changing behavior or removing load-bearing boundaries.

## Workflow

1. **Map the contract.** Read the requested entrypoints, callers, tests, logs, docs, and data shapes. List behavior, side effects, errors, observability, compatibility rules, and required verification.
2. **Find accidental complexity.** Look for unclear names, deep nesting, hidden mutation, unclear ownership, boolean mazes, duplicated branches, broad helpers, long chains, and abstractions that only rename or forward work.
3. **Simplify in small slices.** Use guard clauses, clear control flow, local data, direct calls, and small functions. Prefer one clear responsibility per function, method, and code block. Do not split code only to make units smaller.
4. **Verify externally.** Run focused tests first, then broader tests when shared code is affected. Inspect contract output such as logs, payloads, migrations, or CLI text.

## Rules

- Use simple, precise, obvious names. Rename unclear local and private symbols. Keep public, serialized, database, and external contract names unless requested.
- Prefer direct code over a helper that only renames or forwards one operation. Extract a method only when it owns a meaningful responsibility. Treat `x.foo.bar.z.x` as a possible ownership problem; use a meaningful method, data shape, or boundary adapter instead of a wrapper that only hides the chain.
- Prefer one clear responsibility per function, method, and code block. Do not split code only to make units smaller. Add a short comment only for a reason, constraint, or risk that the code cannot show. Do not shorten code unless it also reduces cognitive load.
- Keep an abstraction only when it owns a real rule, lifecycle, state, public or compatibility boundary, current variation, side effect, or test seam. Remove it when it only supplies a name or imagined reuse.
- Preserve validation, useful errors, logging, metrics, authorization, transactions, retries, domain logic, error semantics, and compatibility behavior. Keep the work within scope; expand it only for correctness or verification.
- If two valid designs differ in behavior, ownership, or a public boundary, ask the user. Otherwise choose the smallest clear change and state the assumption.

## Tests

- Keep tests for public behavior, business rules, failures, compatibility, boundaries, and regressions. Use obvious names, short setup, real inputs, and behavior-focused assertions.
- Remove tests that only prove mock calls or private implementation steps. Keep mocks for real external boundaries or side effects.
- Add a test only for a distinct branch, boundary, invariant, failure mode, data shape, permission, or regression. When removing one, state what still covers the behavior.

## Mandatory 3AM Review

Before finishing, ask:

- Can an on-call engineer who wakes at 3 AM find the main path and failure path quickly?
- Are names simple and obvious? Does each function, method, and code block do one clear job well?
- Can an unneeded helper become direct code without losing a real boundary?
- Are ownership, state changes, failures, observability, and long-chain boundaries easy to find?
- Do tests show behavior, and did the change preserve the public contract and domain logic?

Continue simplifying when the answer is no, or state the remaining risk.

## Final report

Report the main simplifications, removed or kept abstractions, verification performed, and remaining risk. State clearly when behavior was not verified.
