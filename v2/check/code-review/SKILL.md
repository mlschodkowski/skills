---
name: code-review
description: Use when the user asks for a review of changed code—such as a working-tree diff, commit, range, branch, or PR—to check behavior, risks, tests, and maintainability. For complexity-only delete lists, use over-engineering-review instead.
disable-model-invocation: true
---

# Code review

Review the change as a behavior change. Do not edit files unless the
user asks.

If they want only a "what can we delete" pass, use
`$over-engineering-review` (diff) or `$over-engineering-audit` (whole
repo). Do not mix that cut-list format into this review.

## Path

Identify the target and its base:

- working-tree or staged: `HEAD`
- one commit: its parent
- range, branch, or PR: the requested ends, or the merge-base when that
  is the comparison

Say which base and head you used. If unclear, ask once.

Recommend a path, then start the full review only after the user chooses
when they have not already chosen one. One sentence, for example:

`Review path: STANDARD (the change crosses a public boundary and changes
control flow, so I will trace normal, failure, lifecycle, and test
paths).`

- `SHALLOW`: small, local, low-risk. Contract, affected callers, normal
  and obvious failure paths, useful tests.
- `STANDARD`: also trace control flow, data and state, external
  boundaries, lifecycle, observability, and compatibility where
  relevant.
- `DEEP`: high-risk, unclear, or wide. Add adversarial cases for
  retries, timeouts, duplicates, ordering, partial failure, recovery,
  migration, irreversible effects, and release or rollback confidence
  where relevant.

Do not silently expand a shallow review. If the chosen path cannot
answer a safety question, say why and ask whether to widen it.

## Behavior

Build a small before-and-after of the change:

1. What starts the path, and what can it return or change?
2. Which entry points, callers, data, state, side effects, external
   systems, and operators are affected?
3. Which branches were added, removed, or changed?
4. Which facts come from code, tests, or the stated contract? Which are
   inferences or missing evidence?

If the behavior change is hard to see in prose, show one small
before-and-after of the path. For control flow, an execution tree: function
calls as nodes, and a control node only when omitting it would hide a
branch, loop, failure, side effect, or early exit. Mark added and removed
nodes with `+` and `-`. Keep unchanged context small. Preserve exact
identifiers and error names. Do not invent unverified calls. Do not make
a diagram the review.

Trace the paths that matter for this change: normal behavior, expected
failures, boundary inputs, lifecycle, concurrency, ownership,
validation, retries, time, ordering, idempotency, partial failure,
compatibility, rollback, observability. Follow far enough to find the
real owner of each decision and side effect.

Change existing things carefully: name current responsibilities,
consumers, dependencies, and invariants before judging the diff. Prefer
localized fixes when the problem is localized; flag a broader redesign
only when the structure itself blocks correct behavior.

Review tests for observable behavior and useful regression coverage. Do
not demand tests for unchanged or unreachable behavior.

If the change has a spec, issue, or PRD, check the diff against it.
Keep those findings separate from behavior findings so a clean wrong
implementation cannot hide. If the repo documents coding standards in
prose (`AGENTS.md`, ADRs, and similar), cite violations of those
documents. Skip anything a formatter or linter already owns. Do not
invent a spec or a style guide.

## Readability and structure

Report structure issues only when they hurt correctness, debugging,
safe change, or day-to-day maintenance. A pure delete list belongs in
`$over-engineering-review`.

Distinguish accidental complexity (structure with no job) from complexity
the problem requires. Keep necessary completeness — validation at trust
boundaries, failure behavior, operability, compatibility — even when it
makes the change look less tidy.

Check that ownership, dependency direction, and data flow are legible
from names, types, and layout; the happy path, failure path, and owner
are easy to find; boundaries follow real responsibility, lifecycle, or
change lines rather than diagram taste; abstractions in the diff earned
their existence; wrappers that only forward once or hide a decision are
called out; errors, logs, and metrics help operators without leaking
secrets; tests would fail if the bug returned; the change is no larger
than the problem.

## Report

Report only issues that could matter. For each finding: priority, exact
location, evidence, concrete impact, and the smallest useful action. If
the contract is missing, name the decision that is needed instead of
inventing a fix.

The report does not need a fixed shape. It is usually useful to include
the selected path, a short description of the semantic change, findings,
checks that were run, and limits or missing evidence. Use `READY`,
`NEEDS_CHANGES`, or `NEEDS_DECISION` when it helps.

`P0`: immediate severe break, security issue, data loss, or outage.
`P1`: likely incorrect behavior or a regression.
`P2`: a concrete maintainability, coverage, or operability risk.

Use `READY` only when no material finding remains. Use `NEEDS_DECISION`
when missing contract evidence prevents a safe verdict.

Run only the checks needed to confirm findings. Never claim that a
command or test ran unless it did.
