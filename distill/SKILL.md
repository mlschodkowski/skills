---
name: distill
description: Interrogate the coding plan to ruthlessly burn out future-proofing, indirection, and premature infrastructure.
---

# Distill: Interrogate the Plan

Interrogate the proposed implementation. Attack defensive anxiety masquerading as "scalability." 

> **The Core Philosophy:** Good code is simple, but simple does not mean easy. True simplicity requires rigorous effort to untangle a problem down to its essential primitives. Do not mistake lazy, unreadable shortcuts for simple design.

### The Interrogation

* **The Monolith Shortcut:** Can a single, boring, linear script or synchronous function replace this entire pipeline/worker/architecture today?
* **The Indirection Tax:** Does this force a developer to jump across multiple files or layers to trace one logic path? (If it's an interface or factory with only one concrete use case: kill it).
* **Calculated Crashing:** Can we completely skip complex error-handling/retries, let it crash, log it, and manage it manually if it breaks in production?
* **The Static Illusion:** Can a hardcoded env var, an in-memory dictionary, or a raw JSON blob replace a database schema, ORM layer, or dynamic endpoint for now?
* **The Dependency Audit:** Are you adding an external library or infra (Redis, queues, new tables) for a problem that standard library primitives or local state can solve?

> **The Ultimate Filter:** Is this structure serving *current readability* or *imagined future reuse*? If it's for the future, delete it.

---

## OUTPUT FORMAT

### 1. Code to Purge
*(The specific generalizations, patterns, or premature infrastructure to shift+delete immediately.)*

### 2. The Bare Primitive
*(The single, linear, skeletal path of code that delivers the core logic right now. Organized beautifully, but stripped of all architectural fluff.)*

### 3. Intentionally Left Naive
*(What is left unoptimized, unhandled, or messy for immediate speed and feedback.)*
