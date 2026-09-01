---
name: hyperplan
description: Use when the user asks for a hostile architecture and delivery review of a plan, design, specification, or rollout before implementation.
disable-model-invocation: true
---

# Hyperplan

Find blockers before code. Review the proposed solution; do not invent a
different product. Do not write implementation code before the review is
complete. Attack accidental complexity and missing necessary complexity
alike — elegance that ignores failure or operations is incomplete.

Run two independent attacks:

1. **Architecture:** Check that boundaries match reality (ownership,
   lifecycle, failure, independent change). Check dependency direction,
   state ownership, contracts, identity, idempotency, ordering,
   concurrency, rollback, and recovery after timeouts, retries, partial
   writes, duplicates, and outages. Flag abstractions and layers that
   have no job, and missing behavior that the problem requires.
2. **Delivery:** Check the smallest end-to-end slice, scope, owners,
   dependencies, public-behavior tests, rollout, migration, rollback,
   observability, operations, and hidden work. Operational behavior is
   part of the design.

For every finding, state:

- **Scenario:** what fails or changes;
- **Cause:** which plan choice permits it;
- **Impact:** what becomes incorrect, unsafe, expensive, or hard to change;
- **Required change:** the smallest concrete correction.

Return:

```text
VERDICT: BLOCKED | RISKY | READY
ARCHITECTURE_ATTACK:
DELIVERY_ATTACK:
REQUIRED_PLAN_CHANGES:
SAFE_NEXT_MOVE:
```

`READY` requires one supported vertical slice, explicit ownership and
recovery, public-behavior test evidence, and a bounded next action.
