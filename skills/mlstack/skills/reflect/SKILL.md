---
name: reflect
description: Review a session through judgment, tooling, and divergent lenses, surface durable learnings, and route them to existing skill edits or structural checks. Use for reflect or a session retrospective.
---

# Reflect

Read [working rules](../mlstack/references/rules.md).

Mine the current conversation for durable learnings, then route them into skill edits.

Invoke when the user says "reflect" or "/reflect". Skip when the conversation is trivial, off-topic, or already covered by an existing skill the parent followed correctly. One-offs are not learnings.

## 1. Locate the active transcript

Locate the current conversation with the host's chat tools or the transcript path supplied by the host. Do not search unrelated projects. If the full transcript is unavailable, use a tight digest and state the evidence limit.

## 2. Review through three lenses

Read the three prompt templates: [judgment](references/judgment-reviewer.md), [tooling](references/tooling-reviewer.md), and [divergent](references/divergent-reviewer.md). Apply each lens to the same transcript or digest. Keep their findings separate until synthesis.

Use three parallel reviewers only when delegation is authorized and available. Give them bounded read-only work and the relevant template. Use the current host's available tools and configured model; no Cursor Task API or model roster is required. Otherwise run the three lenses in the current agent.
## 3. Synthesize

Use [the synthesizer prompt](references/synthesizer.md) with the three lens outputs. Spot-check consequential citations against the underlying artifacts. Return Accepted / Rejected / Backlog. An independent synthesizer is optional under the same delegation rules.
## 4. Structural enforcement check

Move any Accepted item that a lint rule, script, metadata flag, or runtime check would enforce more reliably to Backlog. Prefer the structural check over another prose instruction when it can enforce the rule reliably.

## 5. Apply

Present Accepted / Rejected / Backlog with exact destination paths. A reflect-only request does not authorize skill edits. Apply only the subset the user requests; an existing explicit request to apply scoped corrections is sufficient.

Report Backlog items locally. File issues or external comments only on an explicit request.

Never edit a skill under `plugins/cache/`. Use the installed personal or project skill path. Copy a cached skill to an authorized editable destination before changing it. Never open a PR or push.

Follow each approved row's Routing exactly:

- Trivial existing-skill edit (a one-line bullet, a tightened sentence, a stale fact corrected): the parent does it directly.
- Substantive existing-skill edit (a new section, a new pattern table, more than ~10 lines): use the available skill-authoring workflow and validate the result.
- `tune description: <skill path>` (the skill exists but didn't trigger when it should have): use the available skill-authoring workflow to improve and check its trigger.
- `new skill via create-skill: <kebab-name>`: use the available skill-authoring workflow. Do not invent the shape ad hoc.

If your environment ships a SKILL.md validator, run it on every touched skill before declaring done.

## 6. Summarize for the user

Short list, no preamble:

- Edits applied: `<skill path>`. What changed, one line each.
- New skills created: `<skill path>`. One line each (rare).
- Backlog filed to the devex tracker: `<issue title>` (`<tags>`). One line each.
- Dropped: one line per rejected finding + reason from the synthesizer.
