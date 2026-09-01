---
name: git-pr
description: Use when the user asks to open or update a pull request, create a PR, or mentions "/pr". Push the current branch and open a PR with a scoped title. For merging stacked PRs, use github.
license: MIT
allowed-tools: Bash
---

# Git PR

Open or update a pull request for the current branch. Do not commit
unless the user asked. Never include secrets.

Title uses the same scoped form as git-commit: `scope: imperative
summary`. Prefer the primary scope of the commits on the branch. Body:
why, what changed, how to verify. Do not fill empty template sections.

1. Inspect: `git status --porcelain`, `git branch -vv`,
   `git log --oneline <base>..HEAD`, `git diff <base>...HEAD`.
2. If there are uncommitted changes, stop and say so.
3. Base is the repo default branch unless this branch is stacked on
   another; then that branch is the base. Read the default with
   `gh repo view --json defaultBranchRef --jq .defaultBranchRef.name`
   when it is not obvious.
4. Push: `git push -u origin HEAD`. Use `--force-with-lease` only if
   the user asked to rewrite history. Never force-push to `main`,
   `master`, or `develop`.
5. If a PR already exists (`gh pr view`), report its URL. Change
   title or body only if the user asked.
6. Otherwise create it:

```bash
gh pr create --base <base> --title "<scope>: <summary>" --body "$(cat <<'EOF'
<why this change exists>

<what moved, at the level a reviewer needs>

How to verify: <command or check>
EOF
)"
```

7. Report the URL.

Merging a stack of PRs is `github`. Do not change git config. Do not
skip hooks. Do not auto-resolve push rejections.
