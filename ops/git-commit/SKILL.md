---
name: git-commit
description: 'Use when the user asks to commit changes, create a Git commit, or mentions "/commit"; stage files by scope and write a scoped commit message with an optional super-normal description.'
license: MIT
allowed-tools: Bash
---

# Git commit

Stage by scope. One commit per module, package, or layer. Never commit
secrets (`.env`, private keys, local credentials).

Use `$super-normal` for the subject and body when the wording needs it.
Keep scoped-commit syntax and repository terms exact.

## Message

```text
<scope>: <imperative summary>

[optional short body]

[optional footer]
```

Scope is required. Prefer two levels when the tree has them
(`auth/session`). In a monorepo, use the package or app directory. In a
single app, use the layer or module. Use `repo` (or `global` / `root`)
only when there is no primary home.

Split mixed scopes into separate commits. If they cannot be split, use
the parent scope or the project's comma-separated convention.

Keep the subject under 72 characters, present tense, imperative. A
one- or two-sentence body is useful when the why is not in the subject.

Breaking change: `scope!: ...` and a `BREAKING CHANGE:` footer.

## Steps

1. Inspect: `git status --porcelain`, `git diff`, `git diff --staged`,
   recent `git log --oneline`.
2. Group files by scope. Stage one group (`git add` or `git add -p`).
3. Commit. Example:

```bash
git commit -m "$(cat <<'EOF'
auth/session: reject empty bearer token

Empty tokens were treated as a missing header and returned 401 with
the wrong body.

EOF
)"
```

4. If a hook fails, fix the code and make a new commit. Do not
   `--no-verify` unless the user said to.
5. Confirm with `git status`.

## Safety

Do not change git config. Do not `reset --hard`, force-push, or skip
hooks unless the user asked. Do not force-push to `main`, `master`, or
`develop`.
