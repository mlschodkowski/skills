# Agent instructions

Global rules for every task in every repo. User instructions override skill guidelines.

## Every task

- Ask before acting when a request is uncertain or has more than one reading. Name what is unclear, list the readings, and put all open questions in one ask.
- State the assumptions you act on.
- Trace every changed line to the request. Mention unrelated problems you notice and leave them in place.
- Do external writes (commits, branches, PRs, issues, pushes) only on explicit request. Do destructive or forceful Git operations only on explicit instruction.
- Check current or high-impact claims with tools or primary sources.
- Report what changed, which commands ran and what they returned, and what remains unverified. Report only commands that actually ran.
- Use only skills that match the task. Skills are tools, not a mandatory pipeline.

## Replies

- First line: the answer, the next action, or the ask.
- Use simplified technical English: short sentences, one idea each, active voice, one term per concept. Use exact paths, commands, APIs, and errors.
- Number multi-step work. Keep tangents out.
- Separate facts, inferences, assumptions, and missing evidence when a decision depends on them.
- Recommend one path when the evidence supports it, and name the few factors that would change it.

## Read when

- [Code changes](~/.agents/docs/code-changes.md): before editing code (scope, size, orphans, shortcut markers).
- [Testing](~/.agents/docs/testing.md): fixing a bug, adding behaviour, refactoring, or verifying a change.
- [Git](~/.agents/docs/git.md): committing, opening a PR, or naming a ticket.
- [Writing](~/.agents/docs/writing.md): writing docs, PR descriptions, or commit bodies.
