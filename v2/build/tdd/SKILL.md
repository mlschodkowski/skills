---
name: tdd
description: Use when the user asks for test-driven development, test-first implementation, or public behavior contracts.
disable-model-invocation: true
---

# Test-driven development

Define the public contract, then run a strict red-green-refactor loop.
Interfaces communicate what callers can assume; tests lock that down
through observable behavior.

## Contract

Before implementation, record:

- public entry points, signatures, types, and boundaries
- user-observable behaviors and failure results
- external dependencies that require injection
- the thinnest vertical behavior to implement first

For injectable boundaries and return-result shapes, see
[interface-design.md](interface-design.md).

Test public behavior. Do not mock internal collaborators. Mock only
external APIs, time, randomness, or direct filesystem access when the
boundary requires it — boundaries should match real ownership and
side effects. See [mocking.md](mocking.md) when the mock boundary is
unclear. See [tests.md](tests.md) when a test is drifting toward
implementation.

## Loop

1. **Red.** Write one small test for one observable behavior. Run it.
   Confirm it fails for the missing behavior, not for a test error.
2. **Green.** Write the smallest implementation that passes. Do not add
   speculative options, abstractions, or unrelated cleanup. Abstractions
   earn existence later, when a stable concept or repeated behavior
   appears.
3. **Refactor.** Keep the test green. Remove duplication, improve names,
   flatten control flow, and keep only structure with a current job.
   Prefer forms native to the codebase. See [refactoring.md](refactoring.md)
   if duplication, feature envy, primitive obsession, or a shallow
   module appears.
4. Repeat for the next behavior.

Code before a failing test means the test has not proved its value.
Delete the implementation and start from the test unless the user
explicitly approved an exception.

Before reporting completion, confirm every behavior has a test, every
test failed for the expected reason, the full suite passes, and output
has no unexplained warnings.
