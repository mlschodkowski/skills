---
name: hyperplan
description: Use when a plan, design, specification, or rollout needs a hostile architecture and delivery review before implementation, or when coupling, state ownership, failure recovery, sequencing, or hidden work is unclear.
---

# Hyperplan: Stress-Test a Plan

Find blockers before code. Run two independent attacks, then make one decision from the evidence:

1. Architecture attack: test boundaries, ownership, state, and failure recovery.
2. Delivery attack: test slices, scope, tests, rollout, operations, and hidden work.
3. Synthesis: state what must change before implementation and define the next safe move.

Apply `ste` to the report. Keep code, commands, paths, API names, status names, and error text exact.

## Gate

- If there is no concrete plan, specification, or design, stop and ask for it.
- Do not write implementation code until the synthesis is complete.
- Review the proposed solution. Do not invent a different product scope.

## The Two Attacks

Run both attacks in parallel with subagents when the environment supports it. If it does not, perform the attacks as two separate passes and label them.

### 1. Architecture attack

Check:

- Information hiding: does a public API expose database schemas, vendor models, SQL types, transport details, or other private choices?
- Change impact: what changes if the database is replaced, an upstream payload changes, or synchronous HTTP becomes asynchronous events?
- State ownership: who owns each record, cache, in-memory value, and transition?
- Failure recovery: what happens after a timeout, partial write, duplicate delivery, retry, stale worker, lost response, or network failure?
- Correctness: are identity, idempotency, ordering, concurrency, rollback, and recovery explicit?
- Contracts: are external DTOs and messages narrow, versioned, and independent of persistence models?

Reject shared mutable state, broad change impact, database models in client-facing APIs, and modules that own unrelated policies or state.

### 2. Delivery attack

Check:

- Slice: is there one thin, end-to-end behavior with a visible acceptance result?
- Scope: are prerequisites, owners, dependencies, migrations, configuration, and deferred work explicit?
- Tests: do tests exercise public behavior and real boundary contracts? Are failure paths covered?
- Rollout: can old and new versions coexist? Are migration, feature flag, rollback, queue, and data-recovery steps defined?
- Operations: are logs, metrics, alerts, limits, runbooks, and ownership shipped with the feature?
- Hidden work: are security, authorization, storage, cleanup, quotas, performance, and support needs included?

Reject a component list that has no supported end-to-end slice, mock-only confidence at external boundaries, or a rollback plan that ignores durable side effects.

## Synthesis

Return this structure:

### Verdict

Use exactly one: `BLOCKED`, `RISKY`, or `READY`.

### Architecture attack

List the strongest findings. For each finding, state:

- Scenario: what fails or changes.
- Cause: which plan choice permits it.
- Impact: what becomes incorrect, unsafe, expensive, or hard to change.
- Required change: the smallest concrete correction.

### Delivery attack

Use the same four-part format. Include the smallest vertical slice, test evidence, rollout conditions, and operational ownership.

### Required plan changes

List only changes required to reach `READY`. Order them by dependency. Give each change an owner, an acceptance condition, or both when the plan provides them.

### Safe next move

Name one bounded action. If the verdict is `BLOCKED` or `RISKY`, resolve the highest-impact finding first. If it is `READY`, start the smallest vertical slice and its public-behavior test.

## Completion Check

Before returning the report, confirm that:

- both attacks are present and independent;
- every finding includes a failure or change scenario and a concrete correction;
- state ownership, recovery, testing, rollout, and operations are explicit;
- the verdict follows from the findings;
- the next move is safe, bounded, and free of implementation code unless the plan is `READY`.
