---
name: slice-it-vertically
description: Use when the user asks to split a feature, system, or task into minimal end-to-end increments with a visible result at each step.
disable-model-invocation: true
---

Apply the "Tracer Bullet" principle from *The Pragmatic Programmer* to this task.

Apply the [plain writing standard](../references/plain-writing.md) to the proposed slices. Keep the established "Tracer Bullet" term when it helps the user recognize the method.

Do NOT approach this in horizontal layers or isolated phases (e.g., all data/backend first, then all UI/frontend). Instead, break the execution down into vertical, end-to-end slices:

1. **The Tracer Bullet:** Define the thinnest, most minimal end-to-end slice that connects all components/layers immediately to prove the core concept works.
2. **The Increments:** Define the next vertical iterations that build upon that working skeleton to add functionality and complexity incrementally.

Keep the output lean, actionable, and focused on getting a working end-to-end result as fast as possible.
