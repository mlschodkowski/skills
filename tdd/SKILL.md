---
name: tdd
description: Test-driven development with the red-green-refactor loop for any mainstream language or stack. Use when the user wants test-first development, tracer bullets, integration-style tests, behavior-driven bug fixes, or asks to add or repair functionality in Python, Go, JavaScript/TypeScript, Java, C#, Rust, Ruby, or similar ecosystems. Reach for this skill whenever the user wants to drive implementation from tests instead of coding first.
---

# Test-Driven Development

Use vertical slices. Write one failing test for one observable behavior, make it pass with the smallest reasonable change, then refactor. Repeat.

Test behavior through public interfaces, not implementation details. Prefer integration-style tests that exercise real code paths using the project's normal tools and idioms. A good test survives internal refactors. A bad test breaks because you renamed a helper, mocked your own internals, or asserted how the code works instead of what it does.

Match the project you're in. Use the existing test runner, assertion style, naming conventions, and build workflow whether that means `pytest`, `go test`, `cargo test`, `JUnit`, `RSpec`, `vitest`, or something else.

See [tests.md](tests.md) for examples, [mocking.md](mocking.md) for boundary-mocking guidance, and [interface-design.md](interface-design.md) for interface design.

## Anti-Pattern: Horizontal Slices

Do not write all tests first and all implementation second. That turns RED into "write every test I can think of" and GREEN into "write all the code," which usually produces brittle, speculative tests.

Why this goes wrong:

- You test imagined behavior instead of the next real behavior.
- You lock in shapes and signatures before learning what the code needs.
- Tests stop being sensitive to the user-facing behavior that matters.
- You lose the feedback loop that makes TDD useful.

**Correct approach**: Vertical slices via tracer bullets. One test → one implementation → repeat. Each test responds to what you learned from the previous cycle. Because you just wrote the code, you know exactly what behavior matters and how to verify it.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED→GREEN: test1→impl1
  RED→GREEN: test2→impl2
  RED→GREEN: test3→impl3
  ...
```

## Workflow

### 1. Planning

Before writing code:

- Confirm the public interface you are changing or adding.
- Confirm which behaviors matter most and what order to tackle them in.
- Design interfaces for [testability](interface-design.md).
- Look for chances to create [deep modules](deep-modules.md).
- List behaviors to test, not implementation steps.
- Get user approval on the plan.

Ask: "What should the public interface look like? Which behaviors are most important to test?"

You cannot test everything. Focus on critical paths, risky behavior, and logic the user actually cares about.

### 2. Tracer Bullet

Write one test that proves one thing about the system end to end:

```
RED:   Write test for first behavior → test fails
GREEN: Write minimal code to pass → test passes
```

This is your tracer bullet. It proves the path works and gives you a reliable place to grow from.

Example behaviors:

- `checkout with valid cart returns confirmed order`
- `Parse("42") returns 42 with no error`
- `POST /users creates a retrievable user`

### 3. Incremental Loop

For each remaining behavior:

```
RED:   Write next test → fails
GREEN: Minimal code to pass → passes
```

Rules:

- One test at a time
- Only enough code to pass current test
- Don't anticipate future tests
- Keep tests focused on observable behavior
- Keep the project's test runner, type checker, and formatter happy as you go

### 4. Refactor

After the current test is green, look for [refactor candidates](refactoring.md):

- [ ] Extract duplication
- [ ] Deepen modules (move complexity behind simple interfaces)
- [ ] Apply SOLID principles where natural
- [ ] Consider what new code reveals about existing code
- [ ] Run tests after each refactor step

**Never refactor while RED.** Get to GREEN first.

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
```
