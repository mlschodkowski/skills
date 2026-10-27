---
name: clean-code
description: Make the smallest complete code change with clear ownership, direct control flow, and explicit failure behavior. Use for implementation, refactoring, or reducing an overgrown diff.
---

# Small change

Read [working rules](../mlstack/references/rules.md).

Start with the requested behavior and the current diff. Find the smallest
change from the real base that delivers it. Small means little new complexity
and a complete result; line count alone does not decide.

1. Read the touched path, callers, tests, configuration, and relevant decisions.
   For shared or lifecycle code, trace state owners, external effects, and the
   contract that old and new callers expect.
2. State what changes and what stays the same. Preserve existing user edits.
   Find facts yourself. Ask about unresolved behavior or ownership decisions.
3. Reuse a sound local pattern or platform capability. A nearby bad pattern is
   not a reason to repeat it. Keep a little repetition when the rules differ.
4. Use names from the domain, direct conditions, and visible inputs and results.
   Keep related decisions together. Extract a helper when it owns one real rule,
   effect, invariant, or useful boundary; remove pass-through wrappers.
5. Complete all affected callers, exports, fixtures, and contracts. Remove only
   code that this change makes unused. Leave unrelated cleanup in place.
6. Verify the final behavior. Use [tdd](../tdd/SKILL.md) for behavior
   changes and [review-changes](../review-changes/SKILL.md) when a review is requested.

## What reduction must preserve

Keep validation, authorization, useful logs and error levels, recovery, retries
that protect a real failure, accessibility, and required compatibility.
Do not replace a failure with a silent fallback to make the path shorter.
Keep stress and concurrency tests that catch a real failure. Remove redundant
setup or assertions before removing the scenario they protect.

Do not build a general framework, new configuration surface, retry system,
compatibility layer, or dependency for a need the task does not establish.
A deliberate shortcut gets a `ponytail:` comment with its limit and upgrade
trigger. This marker remains compatible with the user's existing debt search.

For a clarity choice that needs an example, read
[clarity-examples.md](references/clarity-examples.md).

Report the changed behavior, the check, and material limits. Explain a surprising
change with one before/after example. Do not make every small edit a full audit.
