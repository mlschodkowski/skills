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
2. Inspect uncommitted changes and leave unrelated work untouched. A PR of existing commits can proceed with unrelated local edits; report when requested changes still need an explicitly authorized commit.
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
gh pr create --base <base> --title "<scope>: <summary> [<ticket-number>]" --body "$(cat <<'EOF'
## Why

<why this change exists>

## What

<what moved, at the level a reviewer needs>
EOF
)"
```

EXAMPLE TITLE:
`net/http/client: adjust default parameters [#1234]`

Ticket suffixes are optional unless the repository requires them. Accept “none” without asking again. An explicit user request to omit a ticket takes precedence.

7. Report the URL.

Merging a stack of PRs is `github`. Do not change git config. Do not
skip hooks. Do not auto-resolve push rejections.

8. Language rules

Simple and direct, no fillers. If humanizer skill is available, then use it for writing PR body.
