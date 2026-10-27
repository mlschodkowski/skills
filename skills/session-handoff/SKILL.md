---
name: session-handoff
description: Save a compact handoff that lets a fresh agent resume the exact task, decisions, authorization, working tree, and verification state. Use for handoff or session continuation requests.
---

# Carry state

Read [working rules](../mlstack/references/rules.md).

Read existing plans and handoffs first. Inspect the current files and Git state
when relevant. The handoff describes the state now, including corrections made
after an older plan. Do not turn an earlier assistant summary into source truth.

Use the requested path. If none is supplied, save `handoff.md` in the current
workspace. Keep existing handoff files unless the user asks to replace them.

Record only what the next agent needs:

1. Goal, requested next step, and whether the task is planning, diagnosis,
   review, or execution. State what is authorized and what still needs a request.
2. Current repository, branch, reviewed revision, and dirty or untracked work.
   Identify user edits and deliberate local-only changes that must be preserved.
3. Accepted decisions, scope limits, and important rejected approaches with
   the evidence that ruled them out.
4. Completed and remaining slices. Link to the canonical plan, issue, PR, docs,
   or diff instead of duplicating their contents.
5. Exact commands run, observed results, reproduction fixtures, and verification
   gaps. Distinguish a local pass from an untested dev or production result.
6. The next concrete action, current blocker, and the relevant stack skill files.

Redact secrets. Do not embed raw transcripts, environment dumps, or credentials.
The next agent must be able to locate the actual edited artifact and rerun the
useful check without guessing what a previous session meant.

Report the file path and stop. Writing a handoff does not authorize the next
session's external actions or mark unfinished work complete.
