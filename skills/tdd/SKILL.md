---
name: tdd
description: Implement features or bug fixes with TDD through public behavior with one vertical red-green-refactor cycle at a time. Use for TDD, regression tests, or test-first requests.
---

# TDD

Read [stack rules](../mlstack/references/rules.md).

## Define the contract

Read the relevant callers, tests, domain terms, and decisions. Identify the
public entry point, observable behavior, failure result, and external effects.
Use the existing test seam when it reaches the behavior. State this choice;
ask only when a different contract would change the result.

Test through the interface used by callers. Read [tests.md](tests.md) when
choosing assertions and [mocking.md](mocking.md) when isolating dependencies.
Keep real internal collaborators. Replace external APIs, time, randomness, or
filesystem boundaries only where control is necessary.

## One vertical cycle

1. **RED:** Write one small test for one observable behavior. Run it. Confirm
   that the expected missing or broken behavior causes the failure. Correct
   import errors, broken fixtures, or irrelevant failures before continuing.
2. **GREEN:** Write the smallest complete implementation that passes. Run the
   test again. Update callers required by the contract; keep unrelated behavior
   unchanged.
3. **REFACTOR:** While green, improve names, control flow, and duplication only
   within scope. Run affected tests after the refactor.
4. Repeat for the next behavior. Each cycle crosses the necessary layers;
   do not write all tests and then all implementation.

Expected values come from the contract or an independently worked example.
Assertions must detect wrong behavior rather than repeat the implementation.

For a bug, the test must catch the reported trigger. Re-run the original
reproduction after the fix. For a refactor, establish a green baseline first.

Use the smallest check that still catches the real failure. If the failure needs
concurrency, multiple callers, or a real database transaction, keep that scenario.
Use local substitutes for unavailable external services and state their limits.
When a focused test becomes unexpectedly slow, diagnose the runner or fixture;
do not keep rerunning a stuck suite or remove its assertions to make it green.

## Missing test infrastructure

Inspect existing runners and fixtures before adding infrastructure. If a real
test cannot run, use the closest executable reproduction and state the gap.
Ask before adding a new test dependency. Explicit TDD work without a running
red phase remains incomplete; do not label a static review as a passing test.

Preserve existing edits. If implementation already exists, seek failing-before
evidence in a disposable copy or record that the red phase was not observed.

## Done

Run the final focused tests and the checks required by the repository. Report
the red failure, green result, final commands, and any skipped validation.
