---
name: taste-review
description: Use when a completed PR, git diff, commit range, or implementation brief needs a final readability and maintainability check before commit or merge, especially after the behavior has a clear contract and verification.
---

# Taste Review

Use for the final review of changed scope. Check whether the work is readable, operable, and maintainable. It does not replace contract, security, performance, or test review.

Apply the [plain writing standard](../references/plain-writing.md). Review only by default; edit files only when the user asks.

## Review procedure

1. **Set the boundary.** Review the supplied diff, commit range, or brief. Read context only to understand changed behavior or ownership. Cite `path:line` or symbols.
2. **Trace three paths.** Find the normal, failure, and test or observability paths. Confirm each is visible.
3. **Apply the filters.**
   - **Midnight wake-up:** Find the main path, failure path, ownership, and useful logs within 30 seconds.
   - **Directness:** Use precise names; do not hide rules in nesting, forwarding, duplication, or comments.
   - **Boundaries:** Keep abstractions owning policy, lifecycle, state, side effects, external or compatibility boundaries, or test seams. Question one-use forwarders and imagined reuse.
   - **Signal:** Errors, logs, and metrics add context without leaks. Tests show behavior and surface errors.
   - **Scope:** Suggest the smallest change with a current benefit.
4. **Separate evidence from preference.** If a polish concern may change behavior, state old and new behavior and the missing contract fact. Do not guess.

## Output format

### Verdict

Produce exactly these five sections, in this order: `Verdict`, `Elegant accents`, `Awkward friction`, `Polish diff`, and `Limits`.

Choose one verdict: `Ship`, `Polish before merge`, or `Needs decision`. Give one sentence with the reason. If no safe change is warranted, say so plainly.

### Elegant accents

List only clear strengths. Cite the location when it helps.

### Awkward friction

Use one row per finding. Use exactly one priority: `Block`, `Polish`, or `Preference`.

| Priority | Location | Evidence and impact | Smallest useful action |
| --- | --- | --- | --- |
| Block | `path:line` or symbol | Demonstrated contract, behavior, or observability risk | Focused correction or verification |
| Polish | `path:line` or symbol | Concrete readability or maintenance cost | Focused edit |
| Preference | `path:line` or symbol | Optional style choice with no current risk | Leave unchanged or make the small edit |

Use `Block` only for a demonstrated risk or an unverified behavior change, not for personal style. If missing context prevents a firm verdict, choose `Needs decision` and state the missing fact. Report the strongest findings first. If there are none, write `None`.

### Polish diff

Describe only exact, local, behavior-preserving edits. If none is worthwhile, write: `No safe polish change is warranted in this scope.`

### Limits

State what you reviewed, what verification was provided or run, and unknowns that prevent a firm verdict. Never claim an unrun test or command.
