---
name: ponytail-audit
description: >
  Whole-repo audit for over-engineering. Like ponytail-review, but scans the
  entire codebase instead of a diff: a ranked list of what to delete, simplify,
  or replace with stdlib/native equivalents. Use when the user says "audit this
  codebase", "audit for over-engineering", "what can I delete from this repo",
  "find bloat", "ponytail-audit", or "/ponytail-audit". One-shot report, does
  not apply fixes.
---

# Ponytail audit

ponytail-review, repo-wide. Scan the whole tree instead of a diff. Rank
findings biggest cut first.

Same tags as ponytail-review: `delete:`, `stdlib:`, `native:`, `yagni:`,
`shrink:`.

Hunt: deps the stdlib or platform already ships, single-implementation
interfaces, factories with one product, wrappers that only delegate,
files exporting one thing, dead flags and config, hand-rolled stdlib.

One line per finding, ranked: `<tag> <what to cut>. <replacement>. [path]`.
End with `net: -<N> lines, -<M> deps possible.` Nothing to cut:
`Lean already. Ship.`

Scope: over-engineering and complexity only. Correctness bugs, security
holes, and performance are out of scope. Route them to a normal review
pass. Lists findings, applies nothing. One-shot. "stop ponytail-audit"
or "normal mode" to revert.
