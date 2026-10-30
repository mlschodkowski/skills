---
name: vertical-slices
description: Divide a plan, feature, ticket, or refactor into small, testable end-to-end changes with explicit dependencies. Use for vertical slicing or reducing delivery scope.
---

# Thin slice

Read [working rules](../mlstack/references/rules.md).

Read the whole target and enough code to find the real path. Keep its goal and
accepted decisions. Start with the narrowest behavior that proves the intended
flow through every necessary layer. Add one useful behavior per next slice.

Each slice states:

1. The behavior a user or caller gains.
2. The slices that block it, or none.
3. The public entry point and observable acceptance result.
4. The focused failing-before check and passing-after check.
5. Compatibility or rollout conditions when the slice changes a shared contract.

A schema-only, API-only, or test-only task is usually a step inside a slice.
Each slice must be independently verifiable. Keep necessary prefactoring small;
do not put a speculative framework ahead of the first useful behavior.

For a wide contract change, use expand, migrate, contract. Keep old and new forms
compatible during migration. If a mechanical migration cannot stay green in
separate batches, say so and define the smallest combined verification boundary.

Keep the original artifact format. When asked for a plan, save it and stop.
When asked to execute, complete one slice and its checks before the next.
Commit per slice only if commits are explicitly requested; staging by itself
does not prove a slice works. Keep uncommitted user work intact.
