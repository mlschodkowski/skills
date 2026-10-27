---
name: simple-language
description: Explain code, incidents, decisions, plans, PRs, or issues in short, natural technical language. Use for dense text, before-and-after explanations, or a requested voice edit.
---

# Plain talk

Read [working rules](../mlstack/references/rules.md).

Give the reader the answer first. Use casual professional English, usually at
B2 level, with ASD-STE100 principles. Preserve the writer's voice and technical
meaning. Exact names, commands, errors, and quoted text stay exact.

For a fix, use the facts the reader needs:

1. What failed and the concrete condition that triggered it.
2. How the old path behaved and what the change does differently.
3. What now works, what did not change, and how it was checked.

Use that order without forcing three headings onto a short answer. Show a small
input/output or code example when the mechanism is hard to picture. Separate
facts from a likely explanation and name the missing evidence.

For a decision, number the item and recommend one path. Explain the effect of
that choice. Ask only for a consequential choice the available context cannot
settle. Use a table when alternatives are easier to compare there.

Write short active sentences with one term per concept. Keep evidence beside
the claim. Remove filler, inflated claims, staged questions, forced contrasts,
repeated summaries, and an inventory of implementation details the reader does
not need. Preserve qualifications that affect the reader's decision.

PRs and issues should explain the problem and result in a few useful lines.
Do not add a large verification section when one sentence reports the checks.
For technical reports, keep enough detail to support the cause and limits.

This skill changes expression and organization. It does not authorize a code
change, publication, or a message to another person.
