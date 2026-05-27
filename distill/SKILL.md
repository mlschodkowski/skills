---
name: distill
description: Use at the absolute beginning of a feature request, bug fix, or implementation plan to aggressively eliminate scope creep and premature infrastructure.
---

# Distill (for Code)

Your job is to violently boil a feature request, bug fix, or implementation plan down to its absolute bare structural primitives. You must ruthlessly strip away defensive anxiety masquerading as "clean code," "future-proofing," or "scalability" before a single line of unnecessary infrastructure is built.

Do not audit architecture coupling (Stress Test handles that) or code aesthetics (Taste Review handles that). Audit *necessity*. Challenge every proposed file, class, dependency, and abstraction layer with these filters:

### The Filters

* **The Monolith Shortcut:** Can this entire multi-step asynchronous pipeline, background worker, or microservice be solved by a single, boring, synchronous function or a linear script today?
* **The Abstraction Tax:** Did you write an interface, a factory, or a generic wrapper just to avoid writing 15 lines of raw, repetitive conditional code? (Remember: duplication is far cheaper than the wrong abstraction).
* **Calculated Crashing:** What happens if we completely ignore complex error-handling, retries, and edge cases for this iteration? Can we just let it crash, log it, and handle it manually if it actually breaks in production?
* **The Static Illusion:** Can we hardcode this outcome entirely? Can a volatile in-memory dictionary, an environment variable, or a raw JSON blob replace a database schema, an ORM layer, or a dynamic API endpoint for now?
* **The Dependency Audit:** Are you installing an external library or adding heavy infrastructure (like a Redis cache, a message queue, or a new database table) to solve a problem that standard library primitives or local state could handle?

> **The Golden Code Filter:** Ask yourself: *"Is this not overengineered compared to what user wanted?"* If you have to spend more than 3 seconds justifying why it is *not*, it is. Simplify it.

---

### PREFER:
Monolithic scripts, global search-and-replace, raw SQL/mutations, copy-pasting code (Rule of Three), in-memory state, and standard libraries.

### REJECT:
Design patterns for the sake of patterns, custom ORM wrappers, early microservices, "just-in-case" configuration files, and dry-at-all-costs architecture.

---

## OUTPUT FORMAT

When applying **Distill** to a coding scenario, output exactly these three sections:

### 1. Code to Purge
*(Specific abstractions, design patterns, third-party packages, configuration files, or database migrations to shift+delete immediately.)*

### 2. The Bare Primitive
*(The absolute minimum, skeletal path of executable code that delivers the core logic. The single file or function that gets the job done.)*

### 3. Intentionally Left Naive
*(What you are choosing to leave unoptimized, unhandled, hardcoded, or messy for the sake of speed and immediate feedback.)*
