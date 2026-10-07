---
name: slice-it-vertically
description: Restructure a plan, ticket, spec, task list, or piece of work into tracer-bullet vertical slices. Use when the user says "slice it vertically", "vertical slices", "tracer bullet", or asks to split a plan, ticket, epic, or PR into thinner end-to-end pieces.
disable-model-invocation: true
---

# Slice It Vertically

Apply tracer-bullet vertical slicing to the thing the user names: a plan, ticket, epic, spec, task list, or PR scope. Return the same work, re-cut into slices.

## Process

1. Read the target in full. If it is a reference (path, issue number, URL), fetch it. If the target is unclear, ask.
2. Explore the codebase if needed. Use the project's domain vocabulary. Respect ADRs in the area.
3. Look for prefactoring that makes the change easy. Put it first.
4. Cut vertical slices using the rules below.
5. Give each slice its blocking edges: the slices that must finish before it can start. No blockers means it can start now.
6. Present the slices as a numbered list. Ask if the granularity and edges are right. Iterate until approved.
7. Output in the format of the original artifact (plan section, ticket list, checklist). Publish or write files only if asked.

## Slice rules

- Each slice cuts a narrow but COMPLETE path through every layer (schema, API, UI, tests). It is not a horizontal slice of one layer.
- Each slice is demoable or verifiable on its own.
- Each slice fits in a single fresh context window.
- Prefactoring comes first.
- Describe end-to-end behaviour from the user's view, not a layer-by-layer task list.
- Avoid file paths and code snippets. They go stale.

## Wide refactors

A wide refactor is one mechanical change (rename a column, retype a shared symbol) that breaks many call sites at once. Do not force it into a tracer bullet. Use expand-contract:

1. Expand: add the new form beside the old one.
2. Migrate: move call sites in batches sized by blast radius (per package or directory). Each batch blocks on the expand.
3. Contract: delete the old form. It blocks on every migrate batch.

If batches cannot stay green alone, let them share an integration branch and add a final integrate-and-verify slice.

## Per-slice format

- **Title**: short, descriptive.
- **Blocked by**: other slices, or "None (can start immediately)".
- **What it delivers**: the end-to-end behaviour that works after this slice.
- **Acceptance criteria**: checkable items.
