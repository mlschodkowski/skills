---
name: stress-test-plan
description: Use during design docs or architectural reviews to aggressively expose tight coupling and state fragility.
---

Your job is to violently audit a proposed software design against the core laws of high-leverage architecture: Information Hiding, Tight State Control, and Single Sources of Truth. 

Do not audit the feature scope (Distill handles that). Audit the systemic bones. Challenge the design with these three structural filters:

### The Filters

* **The Leak Check:** Is this module "deep" or "shallow"? Call out if internal implementation details—like raw database schemas, third-party library models, or specific SQL types—are leaking into the public API/interface. 
* **The Blast Radius:** Simulate a massive product pivot. If we swap the underlying database, change an external upstream API payload, or switch from synchronous HTTP to asynchronous events, how many files or modules have to change? If the answer is more than one, the boundaries are wrong.
* **The State Owner & Limbo:** Trace the data flow with a malice mindset. If a network call drops mid-execution, does the system end up in an invalid state? Are multiple components allowed to mutate the exact same record or in-memory dictionary without a strict, single owner? 

### PREFER:
Low coupling, bounded contexts, strict API contracts, idempotency keys, single sources of truth.

### REJECT:
Shared mutable state, ripple-effect architectures, leaking database models to the frontend, "god object" modules.

## OUTPUT FORMAT

### 1. Structural Fractures Found
*(Where the architecture is fragile, tightly coupled, or vulnerable to data corruption.)*

### 2. The Decoupling Action
*(The exact architectural modification—e.g., adding an abstraction boundary, isolating a state mutation, introducing an idempotency check—to make it resilient.)*
