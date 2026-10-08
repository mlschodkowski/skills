---
name: tdd
description: Use when the user asks for test-driven development, test-first implementation, public behavior contracts, or a vertical tracer slice.
disable-model-invocation: true
---

# Test-Driven Development

Use TDD in two phases: define the public contract, then execute a strict RED-GREEN-REFACTOR loop.

## Contract

Before implementation, record:

- public entry points, signatures, types, and boundaries;
- user-observable behaviors and failure results;
- external dependencies that require injection;
- the thinnest vertical behavior to implement first.

Test public behavior. Do not mock internal collaborators. Mock only external APIs, time, randomness, or direct filesystem access when the boundary requires it.

## Loop

1. **RED:** Write one small test for one observable behavior. Run it and confirm it fails for the missing behavior, not for a test error.
2. **GREEN:** Write the smallest implementation that passes. Do not add speculative options, abstractions, or unrelated cleanup.
3. **REFACTOR:** Keep the test green. Remove duplication, improve names, flatten control flow, and keep only abstractions with a current responsibility.
4. Repeat for the next behavior.

Code before a failing test means the test has not proved its value. Delete the implementation and start from the test unless the user explicitly approved an exception.

Before reporting completion, confirm every behavior has a test, every test failed for the expected reason, the full suite passes, and output has no unexplained warnings.
