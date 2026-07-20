---
name: distill
description: Distill a coding plan or newly green code to remove premature optimization, unnecessary layers, and needless indirection while preserving the current contract. Use when a user asks to challenge complexity, remove overengineering, or make a plan or implementation smaller and more direct.
---

# Distill

Distill is a review, not an implementation pass. Find the smallest clear shape that serves today's contract. Report it; edit only when the user explicitly asks to apply the result.

Apply the [plain writing standard](../references/plain-writing.md) to the report. Name the evidence and proposed change directly.

## The earned rule

Prefer plain functions, simple data objects, concrete dependencies, and visible control flow.

An object, interface, factory, strategy, configuration knob, dependency, retry, or test case stays only when it earns its cost through a current responsibility or boundary:

- ownership, lifecycle, state, or a business invariant;
- a stable public or compatibility boundary;
- multiple real implementations or policies that vary now;
- an external dependency, side effect, or necessary test seam;
- an existing codebase pattern that makes the surrounding code clearer.

Do not keep a layer for imagined reuse, scale, flexibility, or a future mode.

## Review

1. Establish the contract.
   - Read the entrypoint, callers, tests, data shapes, and operational behavior in scope.
   - List behavior, errors, observability, security, compatibility, and architecture boundaries that must remain.
   - Completion: the review can distinguish safe deletion from a contract change.

2. Trace the main path.
   - Follow one normal path and each meaningful failure or state path.
   - Mark hops, wrappers, configuration, objects, and dependencies that make the reader build unnecessary state in their head.
   - Completion: each candidate has a concrete reading or change cost, not a general dislike of abstraction.

3. Apply the earned rule.
   - Replace unearned indirection with the smallest obvious function-and-data shape.
   - Prefer direct calls and concrete dependencies. Keep interfaces, factories, strategies, and dependency injection only when their current boundary earns them.
   - Keep or introduce a small object when it makes ownership, lifecycle, policy, or state clearer, or when it fits the established codebase shape.
   - Completion: every proposed removal has a simpler replacement or a clear reason to delete it outright.

4. Protect the load-bearing path.
   - Do not simplify by removing validation, distinct error handling, required retries, logging, metrics, authorization, transactions, compatibility behavior, or useful tests.
   - Do not recommend replacing durable state, an external integration, or a real failure boundary with a hardcoded value or local state merely to make the design smaller.
   - Completion: the simpler shape still satisfies the contract from step 1.

## Report

Return only what is useful for a decision:

1. **Remove or collapse** — the exact unearned layers and why they do not earn their cost.
2. **Keep** — the objects, boundaries, or safeguards that do earn their cost.
3. **Smallest safe shape** — a concise function-and-data outline of the main path.
4. **Contract check** — behavior or verification that must remain after applying the change.

If no safe simplification is found, say so plainly.
