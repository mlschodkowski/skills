---
name: bug-diagnosis
description: Diagnose broken behavior, errors, intermittent bugs, and performance regressions with a runnable feedback loop. Fix the root cause when requested; keep diagnosis-only work read-only apart from reproduction artifacts.
---

# Diagnose bugs

Read [stack rules](../mlstack/references/rules.md).

## Establish the signal

Use [bug-reproduction](../bug-reproduction/SKILL.md) unless a check already
reproduces the report. Reuse that check. Read enough code to build it, but keep
untested theories separate from evidence. Make the signal faster and more
deterministic when that helps distinguish causes.

If local reproduction is blocked, continue useful source inspection. Report
provisional causes with the exact missing evidence. Ask for the smallest
artifact or access that would distinguish them. Do not claim a verified fix.

## Distinguish causes

For an incident, align request IDs, logs, metrics, deployment times, and source
versions into one timeline. Compare before and after the suspected change.
Trace startup, workers, pools, transactions, cancellation, and cleanup when the
failure reaches them. Compute totals across processes and replicas instead of
reading one per-process limit as the system limit. Keep a source hypothesis
separate from a cause demonstrated by runtime evidence.

For support cases, cross-check the proposed cause with another available source.
If impact scope is requested, query the same symptom and distinguish exact from
partial matches by environment. Give the smallest safe manual remedy and its
preconditions, but run a production write only on an explicit instruction.

1. Inspect relevant callers, ownership, side effects, configuration, tests,
   recent changes, and external contracts. Check domain docs and ADRs if present.
2. Rank plausible causes. For each, state a prediction and the check that would
   disprove it. Use several hypotheses when the cause is uncertain; a direct
   failure trace does not need an invented list.
3. Test one variable at a time with a debugger, targeted probe, or short-lived
   instrumentation. Record the observation and update the ranking. Tag temporary
   logs so they can be found and removed.
4. For performance, measure a baseline before changing code. Compare the same
   workload, environment, and metric after each candidate change. Distinguish
   timing noise from a repeatable effect.

## Fix within scope

A diagnosis-only request ends with the supported cause and proposed fix.
For a requested fix, use [tdd](../tdd/SKILL.md). Put the regression check
at a seam that reaches the real caller sequence. Change the shared cause once;
trace all affected callers rather than patching each symptom separately.

Re-run the minimal test and the original scenario. Check related failure paths.
Remove temporary instrumentation and unused reproduction scaffolding that this
task created. Keep a useful regression fixture when it provides lasting value.

Report the cause, evidence that distinguishes it from other hypotheses,
changed behavior, unchanged contracts, exact checks, and remaining gaps.

Explain the result as: what failed, when it could happen, how the old path
behaved, and what the proposed or applied fix changes. Include downsides and
what still needs a dev or production check. Use
[simple-language](../simple-language/SKILL.md) when the mechanism needs a simple example.
