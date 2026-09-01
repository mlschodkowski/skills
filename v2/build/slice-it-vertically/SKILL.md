---
name: slice-it-vertically
description: Use when the user asks to split a feature, system, or task into minimal end-to-end increments with a visible result at each step.
disable-model-invocation: true
---

# Slice it vertically

Split the work into thin end-to-end increments. Each slice should
produce a visible result through the real path, not a finished layer
waiting on the others. Purpose determines the cut: one real capability
per slice, no scaffolding that has no job yet.

Use `$autonoma` when the proposed slices need clearer reader-facing
wording.

1. **Tracer bullet.** The thinnest path that already connects the pieces
   (UI, logic, data, whatever this system actually has) and proves the
   core idea works. Prefer the form native to this stack; do not invent
   layers to make the slice look complete.
2. **Increments.** The next vertical slices on that working skeleton,
   each still end-to-end, each adding one real capability. Keep
   boundaries stable across slices so later change stays localized.

Do not plan "all the backend, then all the UI." Name what the user can
see or run after each slice. Keep the list short enough to start.
