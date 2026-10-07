# Testing and verification

## Test-first

Every change starts with a test that is red:

- Bug fix: write a test that reproduces the bug. See it fail. Then make it pass.
- New behaviour: write tests for it, including invalid input. See them fail. Then implement.
- Refactor: run the tests before and after. Both runs are green.

A new test file is part of the task. If the repo has no test runner, ask before you add one.

## Plan

For multi-step tasks, state the plan with one check per step:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
```

## Verify

- Run the narrowest check that can catch the failure. Widen it for shared or important boundaries.
- Inspect the final diff before you report.
- If the same approach fails twice, stop and re-plan from the evidence.
