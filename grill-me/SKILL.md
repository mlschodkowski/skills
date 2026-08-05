---
name: grill-me
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or invokes "grill me".
disable-model-invocation: true
---

Interview the user relentlessly until you reach a shared understanding. Map the work as a design tree: every decision branches into the decisions that depend on it.

Work in rounds. The frontier is every decision whose prerequisites are settled. Ask the whole frontier in one round, then wait for the user's answers before the next round. A question that depends on another open question belongs to a later round.

Number each question and give a recommended answer. Use this format:

```text
**<question number>: <question title>**: <question body, including choices when useful>
-> <your recommended answer>
```

Finding facts is the agent's job. Inspect files, tools, and other available evidence instead of asking the user for facts that can be discovered. Dispatch a bounded read-only exploration when that is available. Decisions are the user's; ask them and wait.

Recompute the frontier after each answer round. The session is complete when no branch remains silently assumed. Do not act on the plan until the user confirms shared understanding.
