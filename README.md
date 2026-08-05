# Personal Codex Skills

Small, composable skills for Codex. They support evidence-based engineering, explicit decisions, preserved architecture, bounded changes, and proportionate verification.

These skills started from, or were inspired by, [Matt Pocock's skills](https://github.com/mattpocock/skills). They are adapted for this Codex setup and preserve the model's natural reasoning and voice.

## Core skills

- `simple-language` — clear technical writing with optional ASD-STE100-style and approximately B2 language guidance.
- `evidence-barrier` — shared evidence before multi-agent, multi-repository, or cross-boundary changes.
- `grill-me` — design-tree pressure testing in question rounds.
- `tdd` — public behavior contracts and red-green-refactor loops.
- `slice-it-vertically` — minimal end-to-end increments with a visible result.
- `handoff` — compact context for another agent or session.
- `obvious-code` — readable code that is safe to review and change.
- `hyperplan` — hostile architecture and delivery review.
- `oracle` — final `GO`, `GO_WITH_CAVEATS`, or `NO_GO` decision.
- `abstraction-audit` — decide whether an abstraction earns its cost now.
- `architecture-design` — domain models, boundaries, dependencies, and incremental architecture.
- `writing-for-agents` — reliable skills and agent-facing documents.
- `to-questionnaire` — collect missing facts or decisions from a specific person.

Other active skills cover brainstorming, diagnosis, ADRs, Go, Git, GitHub, reviews, taste checks, and skill discovery.

## Invocation

Use `$skill-name` for direct invocation. Deliberate workflows such as `grill-me`, `tdd`, `hyperplan`, `oracle`, and `to-questionnaire` are user-invoked. Contextual skills can trigger when their description clearly matches the task.

Skills are composable, not a mandatory pipeline. Use only the path the task needs.

## Maintenance

Keep skills short, focused, and independently useful. Put triggers in frontmatter, keep one source of truth, preserve exact identifiers and commands, and validate changes against a realistic task before publishing.

## Reference links

- [Matt Pocock skills](https://github.com/mattpocock/skills)
- [ASD-STE100](https://www.asd-ste100.org/)
