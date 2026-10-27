---
name: mlstack
description: Select a personal mlstack workflow for plans, implementation, bugs, reviews, security, UI, motion, Git, or a handoff. Use when mlstack is named or the user asks which workflow fits.
---

# mlstack

Read [working rules](references/rules.md). Select one primary workflow from the
request. Read its Markdown file directly; a host-specific invocation API is
optional. Load supporting references only when they affect the task.

| Need | Workflow |
| --- | --- |
| Resolve choices and save a plan | [plan-work](../plan-work/SKILL.md) |
| Cut work into end-to-end steps | [vertical-slices](../vertical-slices/SKILL.md) |
| Make a small, clear implementation change | [clean-code](../clean-code/SKILL.md) |
| Work test-driven | [tdd](../tdd/SKILL.md) |
| Prove a reported bug | [bug-reproduction](../bug-reproduction/SKILL.md) |
| Find a cause or fix an incident | [bug-diagnosis](../bug-diagnosis/SKILL.md) |
| Review code and spec fit | [review-changes](../review-changes/SKILL.md) |
| Audit trust boundaries | [security-review](../security-review/SKILL.md) |
| Stay with a PR through CI and reviews | [babysit](../babysit/SKILL.md) |
| Commit, file a PR, or create an issue | [commit-changes](../commit-changes/SKILL.md), [create-pr](../create-pr/SKILL.md), [create-issue](../create-issue/SKILL.md) |
| Explain flow, ownership, or model design | [explain-code](../explain-code/SKILL.md) |
| Improve UI hierarchy and interaction | [interface-design](../interface-design/SKILL.md) |
| Build or assess physical motion and haptics | [interaction-motion](../interaction-motion/SKILL.md) |
| Explain a result or rewrite prose | [simple-language](../simple-language/SKILL.md) |
| Leave exact state for the next session | [session-handoff](../session-handoff/SKILL.md) |

Combine workflows only when needed: an authorized fix can reuse a repro and a
red-to-green test. A review stays a review. A plan is saved before execution.
Do not run every skill as a fixed pipeline.
