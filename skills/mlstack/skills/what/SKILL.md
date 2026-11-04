---
name: what
description: Restate the agent's last response in simpler, clearer language when the user invokes /what or /what do you mean by that. Based on wait-what; preserves facts, uncertainty, and scope.
---

# What do you mean?

The user does not understand the last answer. Restate it in clear, approachable
language. Use the agent's last substantive response as the target. If the user
quotes a passage, focus on that passage. Read earlier context only when needed
to explain it. If no target response is available, ask for the text.

Follow [wait-what](../wait-what/SKILL.md):

1. Give the context: the goal and why it matters.
2. State where the work stands: done, in progress, or not started.
3. Give the next action, or one numbered decision with a recommendation.

Use [simple-language](../simple-language/SKILL.md) and
[hemingway-style](../hemingway-style/SKILL.md) to restate the answer. Use short,
active sentences and familiar words. Explain necessary technical terms. Add a
small example when it helps. Return the clearer answer, not an editing report,
readability score, or a list of writing rules.

Preserve the original facts, uncertainty, permissions, and scope. Keep paths,
commands, APIs, and errors exact. Name a relevant assumption the user may have
missed and state what did not change. Do not invent either when the context
does not support it. Correct a clear error openly rather than repeating it.

This skill changes the explanation. It does not resume the task, edit files,
or authorize external actions.
