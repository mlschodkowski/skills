---
name: code-review
description: Use when the user asks for a review of changed code—such as a working-tree diff, commit, range, branch, or PR—to check behavior, risks, tests, and maintainability.
disable-model-invocation: true
---

# Code Review

Review the change as a behavior change, not as a line-counting exercise. Do not edit files unless the user asks.

## Choose the review path

First identify the review target and its base:

- working-tree or staged changes: compare with `HEAD`;
- one commit: compare it with its parent;
- a commit range, branch, or PR: use the requested base and head, or the merge-base when that is the stated comparison.

Say which base and head you used. If the target or base is unclear, ask one short question.

The order is: resolve the boundary, do a quick scan, recommend a path, and then start the full review only after the user chooses when they have not already chosen one. State it in one sentence, for example:

`Review path: STANDARD (the change crosses a public boundary and changes control flow, so I will trace normal, failure, lifecycle, and test paths).`

- `SHALLOW`: a small, local, low-risk change. Check the contract, affected callers, normal and obvious failure paths, and useful tests.
- `STANDARD`: the normal path. Also trace control flow, data and state changes, external boundaries, lifecycle, observability, and compatibility where relevant.
- `DEEP`: a high-risk, unclear, or wide change. Add adversarial cases for retries, timeouts, duplicates, ordering, partial failure, recovery, migration, irreversible effects, and release or rollback confidence where relevant.

Use the chosen path. Do not silently expand a shallow review. If evidence shows that the chosen path cannot answer a safety question, explain why and ask whether to widen it.

## Review the behavior

Build a small before-and-after model of the change:

1. What starts the path, and what can it return or change?
2. Which entry points, callers, data, state, side effects, external systems, and operators are affected?
3. Which branches were added, removed, or changed?
4. Which facts come from code, tests, or the stated contract? Which are inferences or missing evidence?

Trace the important paths. Check normal behavior, expected failures, boundary inputs, lifecycle and cleanup, concurrency, ownership, validation, retries, time, ordering, idempotency, partial failure, compatibility, rollback, and observability when they matter to this change. Follow the path far enough to find the real owner of each decision and side effect.

Review tests for observable behavior and useful regression coverage. Do not demand tests for unchanged or unreachable behavior. A focused check is better than a large test request that does not prove the risk.

## Check good code and good taste

Treat good taste as a maintenance question, not as a personal style vote. Ask whether a developer could understand the main path, failure path, and owner quickly during an incident or a late-night fix.

- Prefer precise names and direct control flow. Look for hidden rules in nesting, forwarding, duplication, or comments.
- Keep policy, lifecycle, state, side effects, external boundaries, compatibility rules, and test seams owned in clear places.
- Question wrappers and abstractions that only forward once, hide a decision, or prepare for reuse that the current code does not need. Keep an abstraction when it makes a real boundary or responsibility clearer.
- Check that errors, logs, and metrics add useful context without leaking sensitive data. Check that tests expose failures instead of hiding them.
- Prefer the smallest change that solves the current problem. Do not turn unrelated old code into a finding unless the change makes it harder to understand or trust.

Report a readability or abstraction issue only when it has a concrete effect on correctness, debugging, change safety, or maintenance. Do not report preference as a defect.

## Report findings

Report only issues that could matter. For each finding, give a priority, exact location, evidence, concrete impact, and the smallest useful action. If the contract is missing, name the decision that is needed instead of inventing a fix.

The report does not need a fixed shape. It is usually useful to include the selected path, a short description of the semantic change, findings, checks that were run, and limits or missing evidence. Use a verdict such as `READY`, `NEEDS_CHANGES`, or `NEEDS_DECISION` when it helps the reader.

Priority means: `P0` is an immediate severe break, security issue, data loss, or outage; `P1` is likely incorrect behavior or a regression; `P2` is a concrete maintainability, coverage, or operability risk. Use `READY` only when no material finding remains. Use `NEEDS_DECISION` when missing contract evidence prevents a safe verdict.

Run only proportionate checks needed to confirm findings. Never claim that a command or test ran unless it did. Keep the language simple and explain technical terms when the reader may not know them.
