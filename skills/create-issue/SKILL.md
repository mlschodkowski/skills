---
name: create-issue
description: Create a requested GitHub issue in the current repository with What, Why, and Definition of Done. Preserve the user's established project and current-iteration workflow where applicable.
---

# Track an issue

Read [working rules](../mlstack/references/rules.md). Create an issue only on an
explicit request. Use the current repository unless another one is named.
Use an authenticated GitHub connector or `gh`.

1. Resolve the repository and collect facts from the request. Inspect code when
   a fact matters. Ask once if missing context changes the issue's meaning.
2. Write an imperative title under 70 characters. Use short, natural technical
   English. The body has exactly these sections, each with a few useful lines:

```markdown
## What

The problem or requested change.

## Why

The concrete impact.

## Definition of Done

- An observable result that proves completion.
```

3. Create the issue with a structured body argument or `gh issue create` using
   `--body-file <file>`. Do not add labels, assignees, milestones, duplicate
   searches, or a ticket number unless requested or required by the repository.
4. For an `allegro-internal` repository, follow the established
   [Fusion iteration workflow](references/fusion-iteration.md) automatically.
   For other repositories, use their documented project convention or leave
   project membership unset. Do not apply a company project to a personal repo.
5. Report the issue URL and iteration, or the exact project step that failed.
   If issue creation succeeded but placement failed, keep the issue and retry
   placement on that issue; do not create a duplicate.
