---
name: bug-reproduction
description: Turn a bug report into a minimal executable reproduction with a clear failing result. Use for repro-only requests, intermittent failures, or an unverified bug report; diagnosis and fixes are separate work.
---

# Reproduce a bug

Read [stack rules](../mlstack/references/rules.md).

1. Record expected behavior, observed behavior, trigger, version, environment,
   and available evidence. Inspect the real call path and existing test tools.
   Ask for only the missing facts that prevent a useful attempt.
2. Build the cheapest executable check that reaches the reported symptom.
   Prefer an existing test, then a CLI or HTTP check, then browser automation,
   captured-event replay, or a small harness. Use synthetic data and local
   environments. Keep credentials out of commands and artifacts.
3. Run the check and record its exact command and failure. A dependency error
   or unrelated crash does not reproduce the report. For timing bugs, measure
   failure counts over a stated number of trials and record time or seed data.
4. Remove one input, step, or dependency at a time. Re-run after each removal.
   Keep the smallest case that still shows the exact symptom. Check that an
   unaffected input or known-good revision behaves differently when available.
5. Report the runnable command, setup, expected and actual result, trial count,
   and retained fixture or evidence path. State which environment you verified.

A reproduction-only request ends here. Leave production code unchanged.
When a fix is also requested, continue with
[bug-diagnosis](../bug-diagnosis/SKILL.md) using this same check.

If the bug does not reproduce, list attempts and results. Separate a source-based
hypothesis from observed behavior. Name the exact missing input, access, or
environment needed next; do not invent a successful reproduction.
