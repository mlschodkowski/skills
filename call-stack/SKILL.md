---
name: call-stack
description: Explain code changes with focused execution trees that combine call stacks and minimal control-flow pseudocode. Use when execution flow changes and the reader needs to understand calls, branches, loops, failures, side effects, or exits; show a current execution tree when there is no useful before/after difference.
---

# Call Stack

Show a focused execution tree when explaining a code change. Keep function calls as the primary nodes and add only the control statements needed to preserve the important behavior.

## Build the tree

1. Set the scope to the relevant execution path. Keep unrelated callers, callees, and implementation details out.
2. Use a diff when the execution path changed. Mark added and removed nodes with `+` and `-` and keep unchanged context small.
3. If there is no useful before/after difference, show the current execution tree instead.
4. Write function calls as tree nodes. Add a control node only when omitting it would hide a meaningful path, outcome, repetition, failure, side effect, or early exit.
5. Use plain, language-neutral labels such as `if valid`, `for each item`, `while retryable`, `return`, or `raise`. This is not a fixed list: choose the smallest set of control statements that makes the behavior clear.
6. Nest branches and call outcomes under their control node. Show a loop body once; do not draw loop-back arrows. Preserve exact identifiers, error names, and API names from the source, and do not invent unverified behavior.
7. Follow the tree with a short explanation of what changed and why it matters.

Long example — use a diff when the execution path changed:

```diff
-ImportJob.run()
-└─ readBatch()
-   └─ writeAll(records)
+ImportJob.run()
+├─ readBatch()
+│  └─ for each record
+│     ├─ if record.valid
+│     │  ├─ normalize(record)
+│     │  └─ reserve(record.key)
+│     │     ├─ if reservation succeeds
+│     │     │  └─ write(record)
+│     │     └─ else
+│     │        └─ retryReserve(record.key)
+│     │           ├─ while attempts < 3
+│     │           │  └─ reserve(record.key)
+│     │           ├─ if reservation succeeds
+│     │           │  └─ write(record)
+│     │           └─ else
+│     │              ├─ recordError(record)
+│     │              └─ continue item loop
+│     └─ else
+│        ├─ recordError(record)
+│        └─ continue
+└─ finalizeBatch()
+   ├─ if errors exist
+   │  ├─ publishFailureReport()
+   │  └─ return failed
+   └─ else
+      ├─ commitBatch()
+      └─ return completed
```

Short example — if there is no useful before/after diff, show a plain execution tree:

```
Cache.get(key)
├─ if cache hit
│  └─ return value
└─ else
   ├─ Repository.load(key)
   └─ return value
```
