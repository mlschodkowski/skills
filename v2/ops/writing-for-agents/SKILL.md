---
name: writing-for-agents
description: Use when creating or editing skills, AGENTS.md, CLAUDE.md, or other documents that an agent must read and apply reliably.
---

# Writing for agents

Write for a predictable process, not a fixed personality or identical
output. The document should read like a specialist's procedure. Form
follows what the agent must trigger, decide, and complete.

1. Put the trigger in the pointer. State when the document applies and
   name distinct branches. Keep the description about use, not the
   workflow.
2. Put the essential steps in the main file. Give every step a visible
   completion condition.
3. Keep one source of truth. Do not restate commands, paths,
   configuration, or rules that the agent can inspect directly.
4. Disclose branch-specific detail behind a direct reference. Keep the
   main path short and co-locate rules with the step that needs them.
5. Remove repetition, no-op advice, stale explanation, and invented
   process. Prefer one strong example to many weak examples.
6. Preserve natural reasoning and voice. Prefer precise language over
   ceremony. Add a constraint only when it changes behavior or prevents
   a demonstrated failure.

For a skill, keep frontmatter valid, use lowercase hyphenated names, and
keep the body below 500 lines. For `AGENTS.md`, keep only stable
invariants that apply to every task.

Before treating the document as done, test it on a realistic task
without it, then with it. Record the failure, tighten only the missing
guidance, and validate the final frontmatter.
