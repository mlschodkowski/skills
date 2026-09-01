---
name: over-engineering-audit
description: >
  Whole-repo scan for accidental complexity. Ranked list of what to delete,
  simplify, or replace with stdlib or platform features. Use when the user
  asks to audit bloat or find what to delete across the repo. Report only; do
  not apply fixes. For a single diff, use over-engineering-review.
disable-model-invocation: true
---

# Over-engineering audit

Same job as `$over-engineering-review`, over the whole tree. Rank by
largest useful cut first. Do not edit files unless asked.

Hunt accidental complexity — structure with no job. Keep complexity the
problem requires. Abstractions must earn existence; remove what provides
no behavior, clarity, or safety. Prefer fewer clear lines when behavior
stays the same, not shortness for its own sake.

Look for: dependencies already covered by stdlib or the platform;
interfaces or factories with one implementation; wrappers that only
forward; thin files that add no real boundary; dead flags, config, and
unused flexibility; hand-rolled standard-library equivalents.

Skip `node_modules`, `.git`, build output, and generated vendor trees.

Do not flag needed validation, auth, observability, compatibility, or
one focused check for non-trivial logic. Correctness, security, and
performance stay out of scope. Use `$code-review`.

One ranked line per finding:

`<tag> <what to cut>. <replacement>. [path]`

Tags match `$over-engineering-review`: `delete:`, `stdlib:`, `native:`,
`yagni:`, `shrink:`.

Done: `net: -<N> lines, -<M> deps possible.` If nothing to cut:
`Nothing extra to remove.`

Report only. Apply nothing.
