---
name: encode-lesson
description: Turn one correction into a lasting rule in the right place. Use when the user corrects your approach, repeats an instruction, or says a mistake happened before. For a whole-session review use reflect.
---

# Encode lesson

Read [working rules](../mlstack/references/rules.md).

A correction that lives only in this chat happens again next session. Capture it
as a rule, put it where it will be read, and ask before you write it.

For lessons across a whole session, use [reflect](../reflect/SKILL.md).

## Steps

1. **State the rule in one line.** Write it concrete and positive, with its scope:
   "Put request checks in the operation's validator." Avoid "be careful with X"
   and "do not do X".
2. **Test that it lasts.** Ask: would the next session repeat this mistake without
   the rule? A one-time preference for this task is not a lesson. Drop it and say so.
3. **Pick the home.** Choose the most structural place that fits:
   1. A lint rule, test, script, or hook that enforces it.
   2. The repo's `AGENTS.md`, for a rule about this codebase.
   3. A skill, for a workflow that recurs across repos.
   4. The global `AGENTS.md`, for a rule that holds in every repo.
4. **Check what exists.** Search the chosen home for a rule that already covers it.
   If one does, tighten that line instead of adding a new one. If an existing rule
   was ignored, make it shorter or move it up, not longer.
5. **Ask before writing.** Number the decision and recommend one home:
   "Rule: <line>. 1 add to <home> (recommended), 2 other home, 3 drop."
   Write only after I answer. Make a one-line edit.
6. **Report** the file and the line you changed, and what stayed unchanged.

## Limits

Never write to a shared or cached skill path. Use the editable personal or project
copy. A correction does not authorize a commit, push, or PR.
