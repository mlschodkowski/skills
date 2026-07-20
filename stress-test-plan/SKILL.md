---
name: stress-test-plan
description: Use during design docs or architectural reviews to aggressively expose tight coupling and state fragility.
---

Audit a proposed software design against information hiding, clear state ownership, and single sources of truth.

Apply the [plain writing standard](../references/plain-writing.md) to the report. Describe concrete weaknesses and changes.

Do not review feature scope; `distill` covers that. Test the design's structure. Treat each filter as a way the design could fail in production or become costly to change.

### The Filters

* **Information hiding:** Check whether a public API exposes database schemas, vendor models, SQL types, transport details, or other implementation choices. Identify every caller that would need to know a private detail. Reject wrappers that merely pass those details through.
* **Change impact:** Test three changes: replace the database, change an upstream API payload, and move from synchronous HTTP to asynchronous events. For each, trace the files and modules that must change. If a change spreads beyond the boundary that owns it, name the coupling and the boundary that should contain it.
* **State ownership and failure:** Trace each state change, including retries, timeouts, partial writes, duplicate delivery, and a network failure between steps. Identify the one owner for every record or in-memory state. Flag missing idempotency, unclear rollback or recovery, and any path that can leave invalid or ambiguous state.

### Prefer

Low coupling, bounded contexts, narrow API contracts, idempotency keys, explicit recovery, and one source of truth.

### Reject

Shared mutable state, broad change impact, database models in client-facing APIs, and modules that own unrelated policies or state.

## OUTPUT FORMAT

### 1. Structural failures

For each finding: describe the failure or change scenario, cite the design element that causes it, and explain the impact.

### 2. Required design change

State the smallest concrete change that removes or contains the problem. Examples: narrow an API boundary, isolate a state mutation, add an idempotency key, or define recovery after a partial failure.
