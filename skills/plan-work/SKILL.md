---
name: plan-work
description: Resolve consequential design choices and save an executable plan without implementing it. Use for planning, grilling an idea, or reviewing architecture and delivery before code.
---

# Work plan

Read [working rules](../mlstack/references/rules.md).

## Understand before specifying

Read the request, current code, prior plan, relevant docs, and available evidence.
Restate the person's goal and concrete successful flow. Keep the product idea
intact as the plan becomes more detailed. A polished spec for a different
product is a failed plan.

Find discoverable facts yourself. Separate them from decisions. For each open
decision that changes behavior, scope, ownership, migration, or rollout, ask a
numbered question with your recommendation and a short before/after example.
Bundle independent questions in one round. Defer dependent questions until their
prerequisites are settled. Use one at a time if the user requests it.

Routine implementation choices do not need a questionnaire. A request to grill
or stress-test warrants deeper questioning; a narrow, settled fix does not.

## Check the proposed path

Trace the main scenario and relevant failures: duplicate requests, ordering,
timeouts, retries, partial writes, cancellation, rollback, and recovery.
For shared services, check both mixed-version directions and deployment order.
State explicit non-goals and any later phase that is documentation only.

Review architecture and delivery separately when the user requests a hostile
review. For each blocker, name the scenario, cause, impact, and smallest required
change. Recommend READY, READY WITH CONDITIONS, or BLOCKED with supporting facts.

## Save the plan

Use the requested path; otherwise use `plan.md` in the current workspace.
Read an existing file before updating it. Preserve accepted decisions and user
edits. A plan should contain:

- Goal, current behavior, intended behavior, and scope.
- Settled decisions and real blockers or missing evidence.
- Ordered [thin slices](../vertical-slices/SKILL.md), dependencies, and acceptance checks.
- For each behavior change, the public test seam and red-to-green check.
- Migration, rollout, recovery, and compatibility steps when relevant.

Keep one canonical plan. Link to existing docs rather than repeating them.
Do not create ADRs, tickets, branches, or additional process files by default.

Stop after saving and reporting the path. Planning approval does not authorize
implementation. Wait for an execute instruction. Later corrections update the
same plan; they do not silently restart or broaden the work.
