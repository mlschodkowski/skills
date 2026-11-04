---
name: clean-code
description: Make the smallest complete code change that fits the codebase's own conventions. Use for implementation, refactoring, review fixes, or reducing an overgrown diff.
---

# Clean code

Read [working rules](../mlstack/references/rules.md).

The codebase sets the style. This skill sets the discipline.

## Fit the codebase first

Before writing, read `AGENTS.md` and two or three sibling files that do the same
job as the code you will touch. Note where they put checks, state, constants, and
external calls. Put yours in the same places.

Authority, highest first: the user's instruction, the project's written rules,
the neighbouring code, this skill. A nearby pattern you dislike is still the
pattern, unless the user or the project rules say otherwise.

## Principles

Name the principle you apply and the decision it changed. A name with no
changed decision means it was not applied.

- **One source of truth.** One decision lives in one place. When two files
  branch on the same rule, give the rule one owner.
- **Reader load.** Count the layers between a question and its answer. Remove a
  wrapper that only forwards. Keep a helper that names a concept.
- **Smallest complete change.** Subtract first. Deliver the whole behavior: callers,
  wiring, fixtures, docs. Add an abstraction, option, dependency, file, or doc only
  when this task needs it. Handle only failures that can actually happen. Leave
  unrelated code alone.
- **Reduce, do not relocate.** Count the concepts a reader must hold before and
  after. A change that moves the same logic elsewhere did not simplify. Prefer the
  change that removes a branch, mode, or layer. These signal a missing owner: a new
  conditional added to an unrelated flow, the same conditional repeated on one
  shape, feature logic in a shared module, a near-duplicate of an existing helper.
  Reuse the helper, or give the rule its own place.
- **Narrow inputs, intent names.** Take what the code needs. Name by the domain
  and the rule, not the mechanism.
- **Preserve behavior.** Keep validation, authorization, errors, logs, and
  recovery. Do not trade a failure for a silent fallback.

## Where does it belong?

Ask these in order:

1. Where do the nearest siblings put the same kind of thing?
2. Who owns the rule or the state? Does anyone else need it?
3. If no sibling shows the way and several callers need it, give the rule a named owner.

Add a concern beside the existing code at the layer that owns it. Do not wrap or
replace working code to fit it in.

## Finish

Remove only what this change made unused. Keep pre-existing dead code unless asked,
and mention it in the report. Move tests with the code they cover. Verify with the
project's own test and lint commands (use [tdd](../tdd/SKILL.md) for behavior
changes). A deliberate shortcut gets a `ponytail:` comment with its ceiling and the
trigger to upgrade, for example `// ponytail: O(n²) scan, index by id past 10k items`.
Find them with `rg -n 'ponytail:' .`.

Report what changed, how you checked it, and material limits. Name each
principle you applied and the decision it changed.
