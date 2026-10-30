---
name: create-pr
description: Push the current branch and open or update a requested pull request with a short scoped title and source-checked description. Does not commit or merge automatically.
---

# Send a PR

Read [working rules](../mlstack/references/rules.md). Use an authenticated GitHub
connector or `gh`. Read the repository's PR template and Git instructions.

1. Inspect the current branch, remote, actual base, commits, and full diff.
   Check staged and unstaged work. A PR contains committed changes only;
   unrelated local edits do not block opening it.
2. Determine the base from the request or branch relationship. A stacked PR uses
   its parent branch; otherwise use the repository default. Check for an existing
   PR before creating one.
3. Write a scoped title using the same format as
   [commit-changes](../commit-changes/SKILL.md). Honor the requested ticket and draft state.
4. Lead the body with the problem and resulting behavior. Explain deployment
   order, migration, or rollback only when they matter. Describe the final diff,
   including material review fixes, rather than repeating an obsolete plan.
   Report validation in one or two sentences with its limits.
5. Push the requested branch with a normal push. Create the PR, or update its
   title/body only when the request covers that update. Prefer a structured body
   argument; with `gh`, write a temporary file and use `--body-file <file>`.
6. Read back the result and report the URL, base, draft state, and any requested
   changes that remain uncommitted or unverified.

Do not create commits, broaden scope, resolve push rejections with history
rewrites, or merge by default. Preserve user-authored body sections unless the
requested edit changes them. A requested PR update does not authorize posting
review replies. Use [babysit](../babysit/SKILL.md) when monitoring is requested.
