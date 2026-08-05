---
name: hyperplan
description: Use when the user asks for a hostile architecture and delivery review of a plan, design, specification, or rollout before implementation.
disable-model-invocation: true
---

# Hyperplan

Find blockers before code. Review the proposed solution; do not invent a different product scope. Do not write implementation code before the review is complete.

Run two independent attacks:

1. **Architecture:** Check boundaries, dependency direction, state ownership, contracts, identity, idempotency, ordering, concurrency, rollback, and recovery after timeouts, retries, partial writes, duplicates, and outages.
2. **Delivery:** Check the smallest end-to-end slice, scope, owners, dependencies, public-behavior tests, rollout, migration, rollback, observability, operations, and hidden work.

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

`READY` requires one supported vertical slice, explicit ownership and recovery, public-behavior test evidence, and a bounded next action.
