---
name: shortcut-debt
description: >
  Find deliberate shortcut markers in the repo and list them as a debt ledger.
  Use when the user asks for shortcut debt, limit comments, deferred upgrades,
  or marked corner cuts. Report only unless asked to write a file.
disable-model-invocation: true
---

# Shortcut debt

List places where someone chose a simple approach and wrote down its
limit.

Markers are written while building (`$super-normal-code`). This skill
only collects them.

A shortcut without a revisit condition becomes permanent by accident.
The comment stores two facts: **limit** (what breaks, slows, or becomes
unsafe if load grows) and **trigger** (the measurable signal that means
replace this now). Example: global lock is fine until lock wait shows
up in profiles.

```text
// limit: <what breaks or gets slow>; upgrade when <trigger>
```

Also accept `# limit: ...` and older `ceiling:` / `ponytail:` comments
with the same idea. Ignore prose that only mentions the words outside a
comment.

Skip `node_modules`, `.git`, and build output:

```bash
rg -n -e '(#|//)\s*(limit|ceiling|ponytail):' .
```

Add other comment prefixes only if the stack needs them. Each hit is
one row.

Group by file:

```text
<path>:<line>, <what was simplified>. limit: <bound>. upgrade: <trigger>.
```

Read limit and trigger from the comment. Tag `no-trigger` if the upgrade
condition is missing.

End with: `<N> markers, <M> with no trigger.`

If none: `No shortcut markers found.`

Write a file only if the user asks.
