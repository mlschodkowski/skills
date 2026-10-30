# Testing and verification

Use the repository's existing runner and fixtures. Match the check to the change.

## Test-first

- Bug fix: add or extend a regression test. Confirm it fails for the reported
  cause, then make it pass.
- New behavior: cover meaningful success and failure paths before claiming done.
  Use [tdd](../skills/mlstack/skills/tdd/SKILL.md) for one behavior per red–green–refactor cycle.
- Refactor: run affected tests before and after. Both runs must pass.
- Documentation or formatting: check syntax, links, builds, or rendering as
  applicable. Do not add tests that only mirror the edited text.

A new test file can be part of the requested change. Ask before adding a new test
runner or testing dependency.

## Reusable project checks

Use [create-verification-skill](../skills/mlstack/skills/create-verification-skill/SKILL.md)
when a project needs a reusable way to launch the app, exercise user behavior,
and capture evidence. Reuse existing harnesses. Run the generated instructions
once before calling them usable. The same skill routes maintenance requests to
its supporting maintenance workflow.

For risk outside the diff, use [blast-radius](../skills/mlstack/skills/blast-radius/SKILL.md).
Name the critical safety assumption and run the smallest check that could
refute it. Separate confirmed risks from risks with missing evidence.

For lifecycle or protocol rules, use [statechart](../skills/mlstack/skills/statechart/SKILL.md).
Check a bounded TLA+ model, inspect rule failures, and replay bug paths against
the real implementation. A passing model does not prove the implementation.
The bundled launcher needs a TypeScript-capable runtime and TLC with Java 11 or
later. It can provision TLC and Java through mise, or use `TLA2TOOLS` and `JAVA`.

## Multi-step work

Name one useful check per step. If the user asks for a plan, save it and stop
before implementation.

## Verify

- Run the narrowest check that can catch the failure. Widen it for shared or
  release-critical boundaries.
- Inspect the final artifact and diff. Verify required side effects and tracker
  status when the request includes them.
- Preserve evidence when cleaning up processes and scratch state.
- Report exact commands, observed results, and unverified behavior. Distinguish
  local tests, mocks, DEV checks, and production evidence.
- If the same approach fails twice, reassess it from the observed evidence.
