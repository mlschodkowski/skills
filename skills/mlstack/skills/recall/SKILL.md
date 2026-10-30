---
name: recall
description: "Reconstruct your recent working context from your own chat history, live state, and the shared record (user reports, prior fixes, incidents), then hand back a tight current-state brief. Use for 'recall my work on X', 'catch me up', 'what have I been working on', 'where did I leave off', before starting or resuming work."
---

# Recall

Read [working rules](../mlstack/references/rules.md).

**Before you start or resume work, you rebuild the user's recent working context and hand back a tight capsule of where things stand now and what to do next.**

Keep it tight and on-topic. Read only what the in-scope threads need, then stop.

Your context lives in two records. Your own chat history holds what you did and decided. The shared record holds everything that happened around the same code under other names: the symptoms users keep reporting, the fixes that shipped and got reverted, the errors still firing in prod. Search that second record in relevant source control history, issues, team discussions, documentation, and runtime evidence when it affects the named work. A feature with a long bug tail keeps most of its story there, so don't reconstruct it from your transcripts alone.

Read history with the current host's chat tools and cursors. Use local transcripts only when those tools are unavailable or omit evidence the task needs. Resolve the target workspace from actual metadata; do not assume a Cursor path layout.

1. Classify, then route. For one specific prior chat, read that chat and validate its handoff directly. Turning habits into durable skill changes belongs to [reflect](../reflect/SKILL.md). A human-readable summary of your work is a different task. Recall loads working context across recent chats before you act. If the user already gave you a full state capsule (paths, branch, the change), use it and skip the mining.
2. Lock the scope before searching. Pin the window ("recent" is a real range, default the last 7 days), the topic if named, and the workspace (default the active one. Never read another project's transcripts without being asked). State the scope back. Never quietly turn "all" into "recent N".
3. Search your chat history. Order candidates by actual update time, filter the topic first, and read only relevant turns. Skip the current chat and obvious noise (subagent, eval, and test chats). For each relevant chat, record topic, user goal, decisions, open threads, struggles and corrections, and artifacts (PRs, tickets, branches), citing the chat ID. For a large corpus, use parallel readers only when delegation is authorized and available; keep raw transcripts out of the main thread. Otherwise partition the same search in the current agent.
4. Sweep the shared record when a named feature or bug has relevant history outside your chats. Start with the surfaced PRs, tickets, and source history; expand to discussions, docs, or runtime evidence when they can change the brief. Ask what is current, what was tried and did not hold, and what users still report. Report unavailable material sources. Skip this for pure activity recall with no named target.
5. Verify against live state. Take the PRs, branches, and tickets that the mining and the sweep surfaced and check them with `git` and `gh`. When the answer hinges on what an agent actually did (the tools it ran, files it read, errors it hit), read the full transcript, not just a trimmed local copy.
6. Write the brief to the contract below. Group by thread. Stay on the named topic.

## Output contract

Lead with the capsule, then the thread status, then the problems, then the next move. Deeper detail goes below or gets cut.

- **Capsule.** At most 5 bullets. What this work is and where it stands overall.
- **Threads.** One line each, prefixed with exactly one status tag: `[merged #N]`, `[open PR #N]`, `[in flight <branch>]`, `[verified, uncommitted]`, `[reverted #N]`, `[planned, not started]`, `[blocked <reason>]`, or `[status unverified]`. A thread with no tag is not done yet, so tag it.
- **Problems.** At most 5, the recurring ones. Include the symptoms users keep reporting and any fix that shipped and was reverted, so the next attempt starts where the last one failed.
- **Next move.** The single most useful next action, concrete.

An adjacent feature or ticket stays out unless it blocks this one. When the capsule and thread lines outgrow a screen, cut detail before you cut threads. Use [simple-language](../simple-language/SKILL.md) when the brief needs a clarity pass, cite chat findings by UUID and shared-record findings by their source (PR #, ticket ID, chat permalink, error-tracker issue), and sanitize private context before any public output.

**Reply:** the brief, to the contract above.
