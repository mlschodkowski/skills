---
name: evidence-barrier
description: Use when work spans multiple independent investigations, agents, repositories, or risky cross-boundary decisions and changes must wait for shared evidence.
---

# Evidence Barrier

Use this skill only when at least two independent investigations or a risky cross-boundary decision can affect the change. Do not add it to a small single-file task.

1. **Discovery:** Fan out bounded, read-only missions. Give each mission a scope, required evidence, forbidden writes, and a stop condition.
2. **Barrier:** Stop before implementation. Separate facts, inferences, conflicts, and missing evidence. Resolve material conflicts with the user.
3. **Decision:** Choose one bounded change, one writer, one checkout, and one verification target.
4. **Execution:** Keep other workers read-only. Serialize writes and preserve unrelated changes.
5. **Proof:** Run the agreed checks and report changed files, results, residual risks, and the next action.

Use this compact checkpoint:

```text
FACTS:
CONFLICTS:
DECISION:
WRITER:
PROOF:
RISKS:
NEXT:
```

Do not use this as a tracker or a replacement for `handoff`, `tdd`, `slice-it-vertically`, or `hyperplan`. Use `$evidence-barrier` for explicit invocation.
