# Merge a stacked PR chain

Merge stacked GitHub PRs into main as individual squash commits. Each
PR targets the previous branch (PR #2 → PR #1's branch → main). The
sequence follows the real dependency order of the stack.

## Identify the chain

```text
main
  └── #1 (base: main, branch: feat-a)
        └── #2 (base: feat-a, branch: feat-b)
              └── #3 (base: feat-b, branch: feat-c)
```

## Merge in order

First PR (already based on main):

```bash
gh pr merge <N> --squash --title "<PR title> (#N)"
git pull origin main
```

Each later PR:

```bash
git checkout <next-branch>
git rebase --onto origin/main <old-base-branch> <next-branch>
git push --force-with-lease origin <next-branch>
gh pr edit <N> --base main
gh pr merge <N> --squash --title "<PR title> (#N)"
git fetch origin main
git checkout main
git pull origin main
```

`git rebase --onto <new-base> <old-base> <branch>` replays commits that
are in `<branch>` but not in `<old-base>` onto `<new-base>`. That drops
the already-merged commits and keeps this PR's unique changes.

Always pass `--title`. GitHub may otherwise use the branch name or the
first commit. Use `--force-with-lease`, not `--force`. Update the PR
base to `main` after the rebase so GitHub records it as merged into
main.

## Conflicts

When `git rebase --onto` stops:

1. Ask the user to resolve the conflicts.
2. After they resolve: `git add <resolved-files> && git rebase --continue`
3. To abandon: `git rebase --abort`

Do not auto-resolve conflicts.
