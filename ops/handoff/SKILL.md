---
name: handoff
description: Use when the user asks to compact the current task into a handoff document for another agent or session.
disable-model-invocation: true
---

# Handoff

Write a handoff so a fresh agent can continue. Save it in the OS
temporary directory, not the workspace.

Use `$super-normal` when the next agent needs clearer wording. Write
facts, decisions, open work, and risks directly.

Do not duplicate content already in PRDs, plans, ADRs, issues, commits,
or diffs. Point to those by path or URL.

Redact secrets, passwords, and personal data.

If the user passed arguments, treat them as what the next session will
focus on.

Include:

- Goal and current state
- What is done, with paths
- What is not done, in order
- Decisions and why
- Open risks
- Suggested skills for the next session, only those the remaining work
  actually needs
