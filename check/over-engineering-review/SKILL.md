---
name: over-engineering-review
description: >
  Review a diff only for unnecessary complexity. List what to delete or
  replace (extra abstractions, reinvented stdlib, unused flexibility). Use when
  the user asks to simplify a change, review for over-engineering, or find what
  to delete in a diff. Does not judge correctness, security, or performance —
  use code-review for those.
disable-model-invocation: true
---

# Over-engineering review

List complexity in the change that does not pay for itself. Do not edit
files unless asked. For behavior, security, or performance, use
`$code-review`.

Find base and head the usual way: working tree or staged → `HEAD`; one
commit → its parent; range, branch, or PR → requested ends, or
merge-base. State base and head in one line. If unclear, ask once.

Look for: dead code and unused options; hand-rolled logic already in
the standard library; a dependency or custom path that duplicates a
platform feature; one-implementation interfaces, unused config, layers
with one caller; the same behavior in fewer clear lines.

Do not flag one focused check for non-trivial logic, or needed
validation, auth, observability, or compatibility.

One line per finding:

`L<line>: <tag> <what>. <replacement>.`

Multi-file: `<file>:L<line>: <tag> <what>. <replacement>.`

| Tag | Meaning |
|-----|---------|
| `delete:` | Remove it. Replacement: nothing. |
| `stdlib:` | Use this standard-library tool instead. Name it. |
| `native:` | Use this platform feature instead. Name it. |
| `yagni:` | Structure not earned yet (extra type, config, layer). |
| `shrink:` | Same behavior, shorter clear form. Show the form. |

```text
L12-38: stdlib: 27-line email validator. "@" check plus confirmation mail.
L4: native: moment.js for one format call. Intl.DateTimeFormat.
repo.py:L88: yagni: AbstractRepository with one implementation. Inline until a second exists.
L52-71: delete: retry wrapper around an idempotent local call. Nothing.
L30-44: shrink: manual dict loop. dict(zip(keys, values)).
```

Done: `net: -<N> lines possible.` (add `-<M> deps` if relevant). If
nothing to cut: `Nothing extra to remove.`

Every finding names a concrete cut and a replacement (or nothing). No
behavior verdict and no P0/P1/P2 list here.
