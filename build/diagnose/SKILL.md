---
name: diagnose
description: Disciplined diagnosis loop for hard bugs and performance regressions. Reproduce → minimise → hypothesise → instrument → fix → regression-test. Use when user says "diagnose this" / "debug this", reports a bug, says something is broken/throwing/failing, or describes a performance regression.
---

# Diagnose

Hard bugs. Get a pass/fail loop first. Do not guess from reading code.

When exploring, use the project's domain glossary for the modules you
touch, and check ADRs in that area.

## Feedback loop

This is the work. A fast, deterministic, agent-runnable pass/fail signal
makes bisection, hypothesis-testing, and instrumentation possible. Without
one, staring at code will not save you.

Spend most of the effort here. Try, roughly in this order:

1. Failing test at a seam that reaches the bug (unit, integration, e2e).
2. Curl or HTTP script against a running dev server.
3. CLI with a fixture, diffing stdout against a known-good snapshot.
4. Headless browser script (Playwright / Puppeteer) asserting on
   DOM, console, or network.
5. Replay a captured trace (request, payload, event log) through the
   path in isolation.
6. Throwaway harness: a minimal subset of the system that hits the
   path with one call.
7. Property or fuzz loop when the bug is "sometimes wrong."
8. Bisection harness (`git bisect run`) when the bug appeared between
   two known states.
9. Differential loop: same input through old vs new (or two configs).
10. HITL bash script last. If a human must click, drive them with
    `scripts/hitl-loop.template.sh` so the loop is still structured.

Once you have a loop, make it faster, sharper, and more deterministic.
Pin time, seed RNG, isolate filesystem, freeze network. A 30-second
flaky loop is barely better than none. A 2-second deterministic loop
is enough.

For non-deterministic bugs, raise the reproduction rate until it is
debuggable. Loop the trigger, add stress, narrow timing windows. 50%
is workable; 1% is not.

If you cannot build a loop, stop. List what you tried. Ask for access
to the environment that reproduces it, a captured artifact (HAR, log
dump, core dump, screen recording with timestamps), or permission to
add temporary production instrumentation. Do not hypothesise without
a loop.

## Reproduce

Run the loop. Confirm it is the user's symptom, not a nearby failure.
Capture the exact error, wrong output, or timing so later steps can
check the fix against it. For flakes, confirm the rate is high enough
to debug against.

## Hypotheses

Write 3–5 ranked, falsifiable hypotheses before testing any of them:

> If X is the cause, then changing Y will make the bug disappear, or
> changing Z will make it worse.

If you cannot state the prediction, it is not a hypothesis yet. Show
the ranked list when the user may already have ruled some out; do not
wait on a reply.

## Instrument

Each probe maps to a prediction. Change one variable at a time.

Prefer a debugger or REPL if the environment supports it. Otherwise a
few logs at the boundaries that distinguish hypotheses. Never "log
everything and grep."

Tag every debug log with a unique prefix, e.g. `[DEBUG-a4f2]`, so
cleanup is one grep.

For performance regressions, logs are usually wrong. Establish a
baseline (timing harness, profiler, query plan), then bisect. Measure
first.

## Fix

If there is a seam that exercises the real bug pattern as it occurs at
the call site, turn the minimised repro into a failing test there, apply
the fix, watch it pass, then re-run the original (un-minimised) loop.

A shallow seam (one caller when the bug needs several, a unit test that
cannot replay the chain) gives false confidence. If no correct seam
exists, that is the finding: the architecture is preventing the bug from
being locked down. Note it. Fix anyway if you can, and say what would
make the next one lockable.

## Cleanup

Before calling it done:

- Original loop no longer reproduces the bug.
- Regression test passes, or the missing seam is written down.
- All `[DEBUG-...]` instrumentation removed.
- Throwaway harnesses deleted or moved to a clearly marked debug
  location.
- The winning hypothesis is in the commit or PR message.

Ask what would have prevented this bug. If the answer is architectural
(no test seam, tangled callers, hidden coupling), recommend that change
after the fix is in, not before.
