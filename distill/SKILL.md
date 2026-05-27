---
name: distill
description: Interrogate a coding plan or newly written green code to ruthlessly burn out future-proofing, indirection, and premature infrastructure.
---

# Distill: Interrogate the Implementation

Attack defensive anxiety masquerading as "scalability," whether inspecting a blueprint or newly green code.

> **The Core Philosophy:** Good code is simple, but simple does not mean easy. True simplicity requires rigorous effort to untangle a problem down to its essential primitives. Do not mistake lazy, unreadable shortcuts for simple design.

### The Interrogation
* **The Monolith Shortcut:** Can a single, boring, linear script or synchronous function replace this entire architecture or freshly written multi-step code today?
* **The Indirection Tax:** Does this force a developer to jump across multiple files or layers to trace one logic path? (If it's an interface, abstraction, or factory with only one concrete use case: kill it).
* **Calculated Crashing:** Can we completely skip complex error-handling/retries, let it crash, log it, and manage it manually if it breaks in production?
* **The Static Illusion:** Can a hardcoded env var, an in-memory dictionary, or a raw JSON blob replace a database schema, ORM layer, or dynamic endpoint for now?
* **The Dependency Audit:** Are you adding an external library or infra (Redis, queues, new tables) for a problem that standard library primitives or local state can solve?

> **The Ultimate Filter:** Is this structure serving *current readability* or *imagined future reuse*? If it's for the future, delete it.

---

## OUTPUT FORMAT

### 1. Code/Structure to Purge
*(The specific generalizations, premature abstractions, patterns, or infrastructure to shift+delete immediately.)*

### 2. The Bare Primitive
*(The single, linear, skeletal path of code that cleanly delivers the core logic right now. Organized beautifully, but stripped of all architectural fluff.)*

### 3. Intentionally Left Naive
*(What is left unoptimized, unhandled, or messy for the sake of immediate speed and feedback.)*
