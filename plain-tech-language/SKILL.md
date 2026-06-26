---
name: plain-tech-language
description: Humanize and simplify technical prose. Use when rewriting engineering docs, PR bodies, runbooks, ADRs, handoffs, incident notes, technical plans, or engineering explanations so they are plain, concrete, and useful to an on-call engineer. Do not use for code changes or generic non-technical writing.
---

# Plain Tech Language

Rewrite text so a tired engineer can understand it quickly and act on it safely.

This skill also removes AI-writing tells from engineering prose. For the full rule catalog with examples, read [ai-writing-patterns.md](references/ai-writing-patterns.md) when the text is long, high-stakes, or the first pass still sounds synthetic.

## Process

1. Identify the reader and moment.
   - Default reader: an on-call engineer at 03:00.
   - Ask only if the audience or action is unclear.
   - Completion: you know who must read it and what they need to do next.

2. Extract the spine.
   - Keep the facts, decisions, commands, examples, risks, and next actions.
   - Remove status theatre, marketing tone, vague importance claims, and filler.
   - Completion: every remaining sentence either explains what happened, why it matters, what to check, or what to do.

3. Rewrite in plain language.
   - Use short sentences and familiar words.
   - Prefer concrete nouns and active verbs.
   - Keep technical names exact: commands, paths, statuses, API fields, classes, error text.
   - Use examples when they make the rule easier to apply.
   - Completion: the text can be scanned without rereading long clauses.

4. Make the reasoning visible.
   - Show the simple thought process when it helps the reader trust the text.
   - Use patterns like: "We check X because Y. If X says Z, do A."
   - Do not over-explain obvious steps.
   - Completion: a reader can see why the recommended action follows from the evidence.

5. Do an anti-slop pass.
   - Remove AI tells: "crucial", "delve", "seamless", "robust", "leverage", "underscores", "pivotal", "testament", "landscape".
   - Remove chatbot artifacts: "Great question", "Certainly", "I hope this helps", "Let me know".
   - Remove promotional tone: "groundbreaking", "rich", "vibrant", "powerful", "must-have".
   - Replace vague authority with exact evidence or remove it: "experts say", "industry observers", "reports suggest".
   - Remove fake contrast: "not only... but also", "not just... it is".
   - Remove tail slogans: "no guessing", "no wasted motion", "no surprises".
   - Break forced rule-of-three lists and false "from X to Y" ranges.
   - Prefer simple verbs over copula avoidance: use "is", "has", and "uses" instead of "serves as", "boasts", and "stands as".
   - Remove broad claims unless there is evidence.
   - Completion: the result sounds like a practical teammate, not a press release.

6. Check operational usefulness.
   - For docs and runbooks: include the trigger, the check, the expected good/bad signal, and the next action.
   - For PR bodies: include the problem, the fix, tests, and reviewer notes only when useful.
   - For plans: include the current state, intended change, guardrails, test plan, and acceptance criteria.
   - Completion: the reader can act without hunting through the code or chat history.

## Style Rules

- Language level: B2 or simpler.
- Keep paragraphs short.
- Use bullets when they help scanning; do not force every answer into bullets.
- Prefer "because" over abstract cause words.
- Prefer "this fails when..." over "this introduces a risk that...".
- Prefer "the restore polls S3 with `pbm describe-restore -c <config>`" over "the system leverages a config-backed polling mechanism".
- Keep uncertainty honest: "I did not verify X" is better than hiding the gap.
- Do not make the text warmer by adding fluff.

## Shape By Artifact

### PR Body

Use this shape unless the repo has a stricter template:

```markdown
## What changed
- ...

## Why
- ...

## Tests
- ...

## Notes for review
- ...
```

Keep examples minimal and real:

```markdown
Before: restore waited on PBM through the target cluster.
After: restore starts, then polls `pbm describe-restore <id> -c <tmp-config> -o json`.

This matters because physical restore can make the target MongoDB unavailable while PBM status still exists in S3.
```

### Runbook Or Procedure

Use this shape:

```markdown
## When this matters
...

## What to check
...

## Good signal
...

## Bad signal
...

## What to do next
...
```

### Explanation

Use this shape:

```markdown
The short version: ...

The key detail is ...

Example:
...

So the rule is ...
```

## Final Check

Before finishing, ask:

- Can an on-call engineer find the first action in under 30 seconds?
- Are the examples small enough to copy mentally?
- Did I keep exact commands, errors, file paths, and statuses intact?
- Did I remove words that sound polished but add no decision value?

If any answer is no, revise once more.
