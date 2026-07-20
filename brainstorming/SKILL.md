---
name: brainstorming
description: Explore ambiguous product, design, architecture, or feature ideas before implementation. Use when the request has unclear goals, multiple plausible approaches, UX/product tradeoffs, broad scope, or the user explicitly asks to brainstorm. Do not use for small mechanical edits, obvious bug fixes, commits, formatting, or tasks where the user already gave a concrete implementation target.
---

# Brainstorming

Turn an unclear idea into a concrete design the user can approve. Keep the loop light: discover just enough context, ask the highest-value questions, propose options, and stop when the next action is clear.

Apply the [plain writing standard](../references/plain-writing.md) to questions, options, and the final recommendation.

## Use This When

- The goal, audience, constraints, or success criteria are unclear.
- There are several reasonable designs and the tradeoff matters.
- The work crosses product, UX, architecture, data model, or workflow boundaries.
- The user asks to brainstorm, explore options, shape a feature, or think through a design.

Do not use this for narrow code edits, obvious bug fixes, validation runs, commits, or requests where the user already chose the implementation.

## Workflow

1. **Read the local context.**
   - Inspect the relevant files, docs, or recent changes before asking broad questions.
   - Completion: you can name the current shape and the unknowns that matter.

2. **Frame the decision.**
   - State the problem in one or two sentences.
   - If the request is too large, split it into smaller independent pieces and choose the first piece with the user.
   - Completion: the user can see what decision you are helping them make.

3. **Ask only useful questions.**
   - Ask one question at a time.
   - Prefer multiple-choice when it will reduce friction.
   - Skip questions whose answers can be discovered from the repo or safely assumed.
   - Completion: goal, constraints, and success criteria are clear enough to design.

4. **Offer options.**
   - Present two or three approaches with tradeoffs.
   - Lead with your recommendation and why.
   - Completion: the user can choose, reject, or combine options.

5. **Write the design.**
   - Scale the design to the work: a short paragraph for small changes, structured sections for larger work.
   - Cover behavior, data/control flow, edge cases, and verification.
   - Use a project-local docs path only when a durable design doc is useful or requested.
   - Completion: there is an approved design or a clear reason to pressure-test it.

6. **Exit cleanly.**
   - If the user wants challenge, invoke `grill-me`.
   - If the user approves implementation, stop using this skill and follow the normal coding workflow.

## Visual Companion

If upcoming decisions are easier to judge visually, such as layouts, diagrams, or UI alternatives, offer the browser companion once in its own message. If accepted, read `visual-companion.md` before using it.

Do not use the visual companion for ordinary requirements, tradeoff lists, scope decisions, or text-only architecture discussion.
