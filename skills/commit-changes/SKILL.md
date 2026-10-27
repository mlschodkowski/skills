---
name: commit-changes
description: Create a scoped Git commit from authorized changes while preserving unrelated work. Use only when the user requests a commit; it does not push or open a PR.
---

# Save a commit

Read [working rules](../mlstack/references/rules.md). A commit needs an explicit
request. Read applicable repository Git instructions before naming it.

1. Inspect status, unstaged and staged diffs, current branch, and recent commit
   subjects. Identify the requested slice and any user changes or local bypasses.
2. Group by coherent scope. Stage explicit paths or hunks. One completed slice
   can be one commit when its cross-layer changes belong together; split unrelated
   scopes. Leave unrelated staged changes out without discarding them.
3. Verify the exact staged diff and the relevant checks. Check for credentials,
   generated noise, temporary admin bypasses, and unintended files.
4. Commit with the repository format. The user's default is:

```text
module/submodule: imperative summary [#ticket]
```

Prefer two scope levels when the repository has them. Use a meaningful one-level
scope when it does not. Keep the subject under 72 characters. Use `scope!: ...`
and a `BREAKING CHANGE:` footer when required. A short body explains why when
the subject cannot. Preserve repository-required trailers.

Tickets are optional unless the repository requires one. Accept `none` without
asking again. Do not substitute `fix(scope): ...` for the user's scoped format.
Write multiline bodies to a temporary file and use `git commit -F <file>`.

If a hook fails, inspect whether a commit was created, fix the actual failure,
and retry within the requested scope. Do not skip hooks or amend history unless
authorized. Confirm the resulting commit and remaining working-tree changes.

Do not commit on a protected/default branch when the user requests another
branch. Branch creation itself requires an explicit request; prepare the staged
result and ask only if that missing action blocks the requested commit.
No push, PR, config change, or destructive Git operation follows automatically.
