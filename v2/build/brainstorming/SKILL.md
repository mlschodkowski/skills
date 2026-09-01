---
name: brainstorming
description: Explore ambiguous product, design, architecture, or feature ideas before implementation. Use when the request has unclear goals, multiple plausible approaches, UX/product tradeoffs, broad scope, or the user explicitly asks to brainstorm. Do not use for small mechanical edits, obvious bug fixes, commits, formatting, or tasks where the user already gave a concrete implementation target.
---

# Brainstorming

Turn an unclear idea into a design the user can approve. Discover just
enough context, ask the questions that change the answer, propose
options, and stop when the next action is clear.

Use `$autonoma` for questions, options, and the recommendation when the
reader needs clearer wording.

Do not use this for narrow code edits, obvious bug fixes, validation
runs, commits, or requests where the user already chose the
implementation.

1. **Read the local context.** Inspect the relevant files, docs, or
   recent changes before asking broad questions. Prefer forms and
   constraints already native to the project.
   Done when you can name the current shape and the unknowns that matter.

2. **Frame the decision.** State the problem in one or two sentences. If
   the request is too large, split it and choose the first piece with
   the user. Purpose first; cut scope that has no job yet.
   Done when the user can see what decision you are helping them make.

3. **Ask only useful questions.** One at a time. Prefer multiple-choice
   when it reduces friction. Skip answers you can discover from the repo
   or safely assume. Preserve uncertainty that affects the decision;
   do not invent constraints.
   Done when goal, constraints, and success criteria are clear enough to
   design.

4. **Offer options.** Two or three approaches with tradeoffs. Lead with
   your recommendation and why — including how boundaries, failure, and
   change differ when that is what separates the options.
   Done when the user can choose, reject, or combine them.

5. **Write the design.** Scale it to the work: a short paragraph for
   small changes, structured sections for larger work. Cover behavior,
   data and control flow, edge cases, failure modes, and verification.
   Write a durable design doc only when that is useful or requested.
   Done when there is an approved design, or a clear reason to
   pressure-test it.

6. **Exit.** If the user wants challenge, invoke `grill-me`. If they
   approve implementation, stop using this skill and follow the normal
   coding workflow.

If upcoming decisions are easier to judge visually (layouts, diagrams,
UI alternatives), offer the browser companion once in its own message.
If accepted, read `visual-companion.md` before using it. Do not use it
for ordinary requirements, tradeoff lists, scope decisions, or text-only
architecture discussion.
