---
name: code-review
description: Use when the user asks for an evidence-first review of a code change, diff, branch, PR, or implementation against its contract, failure paths, tests, and maintainability.
disable-model-invocation: true
---

# Code Review

Review changed behavior, not every line you can find. Do not edit files unless the user asks.

1. Set the boundary. Identify the requested change, fixed point, diff, affected entry points, callers, data, external boundaries, and tests. If the target is ambiguous, ask one concise question.
2. Reconstruct the contract from the task, public interfaces, existing behavior, callers, persisted data, and tests. Mark facts, inferences, and missing evidence.
3. Trace the changed path through normal, failure, boundary, lifecycle, concurrency, and test or observability paths. Check ownership, validation, retries, time, ordering, idempotency, partial failure, compatibility, and rollback where relevant.
4. Review tests for observable behavior and missing regression coverage. Do not demand tests for unchanged or unreachable behavior.
5. Review readability and abstractions only when they hide ownership, policy, control flow, failure, or a concrete maintenance risk. Do not report taste as a defect.
6. Report only actionable findings. Each finding needs a priority, exact location, evidence, concrete impact, and smallest useful change. If the contract is missing, state the decision needed instead of inventing a fix.
7. Run only proportionate checks needed to confirm a finding. Use `$simple-language` when the report needs clearer wording for its reader. Never claim a test or command ran unless it did.

Use this output:

```text
VERDICT: READY | NEEDS_CHANGES | NEEDS_DECISION
FINDINGS:
  - [P1] <title>
    LOCATION: <path:line or symbol>
    EVIDENCE: <observed code, contract, or test>
    IMPACT: <concrete failure or risk>
    ACTION: <smallest useful change or decision>
TESTS_AND_CHECKS: <commands/results, or not run>
LIMITS: <unreviewed areas and missing evidence>
```

Priority means: P0 is an immediate severe break, security issue, data loss, or outage; P1 is likely incorrect behavior or regression; P2 is a concrete maintainability, coverage, or operability risk. Do not report preference as a defect.

Use `READY` only when no material finding remains. Use `NEEDS_DECISION` when missing contract evidence prevents a safe verdict. This skill is user-invoked; it complements the existing fixed-point standards/spec `review` skill and final-polish `taste-review` skill.
