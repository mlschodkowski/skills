---
name: git-commit
description: 'Use when the user asks to commit changes, create a Git commit, or mentions "/commit"; stage files by scope and write a scoped commit message with an optional STE description.'
license: MIT
allowed-tools: Bash
---

# Git Commit with Scoped Commits

Apply `ste` to commit subjects and bodies. Keep scoped-commit syntax and repository terms exact.

## Overview

Create highly structured, semantic git commits using the **Scoped Commits** specification (built on top of Conventional Commits). Every commit must explicitly map to a defined **scope** representing the specific module, package, or architectural layer being modified, ensuring clear repository history and automated changelogs.

---

## Scoped Commit Format

```
<scope>: <description>

[optional body]

[optional footer(s)]
```

> **Note:** Unlike standard conventional commits where the scope is optional, Scoped Commits treat the `<scope>` as a **required** component to maintain granular traceability across the codebase.

---

## Scope Rules & Detection

The `<scope>` must accurately reflect the module or area of the codebase being changed.

### 1. Determining the Scope

- **Monorepos / Workspaces:** Use the specific package or application directory name (e.g., `server`, `client`, `shared-ui`).
- **Polyrepos / Single Apps:** Use the underlying architectural layer, module, or component group (e.g., `auth`, `db`, `api`, `views`).
- **Cross-cutting / Global:** Use `global`, `root`, or `repo` only if the changes genuinely span across all boundaries without a primary target.

### 2. Multi-Scope Changes

If a change affects multiple distinct scopes, it should ideally be broken down into **separate, isolated commits**. If inseparable, use a broader parent scope or comma-separated scopes if configured by the project conventions.

---

## Breaking Changes

```
# Exclamation mark after the mandatory scope

# BREAKING CHANGE footer
BREAKING CHANGE: `extends` key behavior changed
```

---

## Workflow

### 1. Analyze Diff & Identify Scope

Examine changed files to group them logically by their respective code paths and determine the appropriate scope.

```bash
# Verify modified and staged files
git status --porcelain

# Analyze changes to isolate distinct scopes
git diff --staged
git diff
```

### 2. Stage Files by Scope Boundary

Do not stage unrelated scopes together. Keep commits atomically scoped.

```bash
# Stage files belonging to a specific scope/module
git add src/modules/auth/*

# Interactive staging for precise scope separation
git add -p
```

> ⚠️ **Critical Safety:** NEVER stage or commit sensitive data (`.env`, private keys, local credentials).

### 3. Generate the Scoped Commit Message

Construct the message following these structural criteria:

- **Scope:** Provide the identified module/package name in the format required by the repository. Use lowercase, exact repository terms when no local convention exists.
- **Description:** Write a concise, imperative, present-tense summary (e.g., "add integration tests" instead of "added integration tests"), keeping it under 72 characters.

### Short STE Description (Encouraged)

The scoped title is required. Add a very short body in ASD-STE100 Simplified Technical English when the title alone does not explain the change, reason, tests, or risk.

### 4. Execute Commit

```bash
# Single-line scoped commit
git commit -m "foo/bar/baz: handle token expiration gracefully"

# Multi-line scoped commit with body/footer
git commit -m "$(cat <<'EOF'
ui.foo.bar: implement dynamic dashboard grid

- Add responsive layout support for mobile viewports
- Optimize rendering performance for widget heavy views

Refs: #892
EOF
)"
```

---

## Git Safety Protocol

- **NEVER** update local or global git configurations programmatically.
- **NEVER** run destructive commands (`git reset --hard`, `git push --force`) without explicit, direct user instructions.
- **NEVER** skip git hooks (`--no-verify`) unless explicitly forced by the user.
- **NEVER** force-push directly to protected branches (`main`, `master`, `develop`).
- If a commit fails due to a pre-commit validation or linter hook, address the underlying code issue and trigger a **new commit** (avoid unexpected amends).
