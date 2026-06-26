# skills

My Codex skills.

Many started from, or were inspired by, Matt Pocock's skills:
https://github.com/mattpocock/skills

This repo keeps my versions. They have narrower triggers, fewer assumptions from other agent runtimes, and more direct instructions.

## Core engineering skills

- `diagnose` - find the real cause of hard bugs, then fix and regression-test it.
- `simplify-codebase` - make code easier to trace during an incident without changing behavior or damaging useful architecture.
- `tdd` - use public-interface tests and small red/green loops.
- `distill` - remove speculative infrastructure, boilerplate, and premature abstractions from plans or green code.
- `slice-it-vertically` - cut a plan into the thinnest useful end-to-end slice.
- `stress-test-plan` - review a design for coupling, fragile state, and hidden blast radius.
- `review` - review a diff on two axes: documented standards and requested spec.
- `taste-review` - final naming, formatting, and ergonomics pass before commit or merge.
- `zoom-out` - map a code area from one level higher when the local details are unclear.

## Planning and decision skills

- `brainstorming` - shape unclear product, design, architecture, or feature ideas before implementation.
- `grill-me` - question a plan or idea until the decision tree is clear.
- `hyperplan` - run hostile plan review from multiple angles.
- `oracle` - ask for a final go/no-go decision.
- `flow-map` - show the full engineering gauntlet when I want the whole process visible.

## Workflow skills

- `git-commit` - create scoped commits with a clean message.
- `handoff` - write a compact handoff for the next session.
- `saving` - reduce token use and verbosity.
- `adr` - draft Architecture Decision Records from approved plans or implementation briefs.

## Writing skills

- `plain-language` - simplify and humanize general prose while keeping meaning and voice.
- `plain-tech-language` - simplify and humanize technical prose for engineers, runbooks, PRs, ADRs, and incident notes.
- `writing-great-skills` - review and improve skills with predictable triggers, pruning, and bad-skill-smell checks.

## Other local skills

- `audit-loop` - audit-oriented loop kept from earlier workflow experiments.
- `karpathy-guidelines` - Karpathy-inspired engineering guidance.

## Changes from Matt Pocock's skills

The upstream repo is the main source of inspiration. These local versions are tuned for my Codex setup:

- Removed unsupported frontmatter and assumptions from other agent runtimes.
- Reframed `brainstorming` so it is not a required gate before every small task. It now triggers only for unclear product, design, architecture, or feature work.
- Simplified `review` so it does not depend on another runtime's `Agent` tool or setup commands.
- Simplified `handoff` frontmatter while keeping the behavior.
- Tightened `zoom-out` into a small context-mapping skill.
- Added `simplify-codebase` for on-call readability: preserve behavior, keep useful abstractions, and make the main path easy to trace.
- Merged `humanizer` into `plain-language` and `plain-tech-language`, so plain rewriting also removes AI-writing tells. The full pattern catalog now lives in each skill's `references/ai-writing-patterns.md`.
- Added `writing-great-skills` for pruning, splitting, validating, and spotting bad skill smells.
- Removed generic `refactor` because `simplify-codebase` better matches how I want code cleanup done.
- Removed `algorithmic-art` because it is not part of my normal engineering workflow.

## Reference links

- Matt Pocock skills: https://github.com/mattpocock/skills
- Pragmatic Programmer notes and patterns: https://github.com/lighthousand/books/blob/master/the-pragmatic-programmer.pdf
- Free programming books: https://github.com/EbookFoundation/free-programming-books/blob/main/books/free-programming-books-subjects.md
