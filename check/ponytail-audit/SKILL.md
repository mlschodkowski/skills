---
name: ponytail-audit
description: Use when the user explicitly asks for a ponytail audit or invokes ponytail for a repo-wide shortest-path review; report cuts without applying them.
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
