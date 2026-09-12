---
name: adr
description: Create an ADR from an approved plan, design, or implementation brief. Use when the user wants a decision recorded in docs/decisions/.
---

# ADR

Write the ADR from the plan the user already provided. Do not ask
follow-up questions. If something important is missing, infer a
reasonable default and make the assumption explicit in the draft.

Use `$super-normal` when the wording needs it. Preserve established
repository terms and the local ADR template.

Inspect `docs/decisions/` and mirror the local style before writing.
Suggest the next numeric prefix from existing ADRs. Reuse repo evidence
instead of asking for information already in code or docs. Never reveal
secrets.

Modes: `draft`, `short`, `deep`. Default: `short`.

Output:

- Suggested filename: `docs/decisions/NNNN-short-slug.md`
- Full ADR markdown

Structure:

1. YAML front matter: `status`, `date` (`YYYY-MM-DD`), `decision-makers`,
   `consulted`, `informed`
2. `# NNNN: short title`
3. `## Context and Problem Statement`
4. `## Decision Drivers`
5. `## Considered Options`
6. `## Decision Outcome`
7. `## Requirements` only when the plan includes explicit requirements
   worth preserving
8. `## Consequences`
9. `## More Information` only when it materially improves clarity

If the plan already implies the chosen option, say so in Decision
Outcome and keep the alternatives concise but real. If the repo has a
template or a similar ADR, follow its naming and phrasing.
