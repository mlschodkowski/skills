---
name: github
description: GitHub patterns using gh CLI for pull requests, stacked PRs, code review, branching strategies, and repository automation. Use when working with GitHub PRs, merging strategies, or repository management tasks.
license: MIT
metadata:
  author: Callstack
  tags: github, gh-cli, pull-request, stacked-pr, squash, rebase
---

# GitHub

Use `gh` for GitHub operations. Prefer it over GitHub MCP servers.

Use `$super-normal` when drafting PR titles, bodies, comments, and issue
text. Keep commands and GitHub terms exact.

```bash
gh pr create --title "auth/session: reject empty bearer token" --body "..."
gh pr merge <PR_NUMBER> --squash --title "auth/session: reject empty bearer token (#<PR_NUMBER>)"
gh pr status
gh pr checks <PR_NUMBER>
```

## Stacked PRs

When each PR targets the previous branch:

1. Squash-merge the first PR into main.
2. For each later PR: rebase onto main, set its base to main, squash-merge.
3. On conflicts, stop and ask the user to resolve.

```bash
git rebase --onto origin/main <old-base-branch> <next-branch>
git push --force-with-lease origin <next-branch>
gh pr edit <N> --base main
gh pr merge <N> --squash --title "<PR title> (#N)"
```

Full sequence: [stacked-pr-workflow.md](references/stacked-pr-workflow.md).
