---
name: understand-before-ship
description: Explain a change and check the user's understanding with scenario questions before shipping. Use when the user asks to be quizzed on a change or invokes understand-before-ship. This checks understanding, not release readiness.
---

# Understand a change

Read [working rules](../mlstack/references/rules.md).

Use the requested change or the change discussed in this chat. Read its diff,
relevant source, contracts, decisions, and recorded checks. Treat earlier agent
summaries as pointers. If the target is unclear and context cannot resolve it,
ask which change to use.

## Explain

Use [simple-language](../simple-language/SKILL.md). Explain the goal, the path
from request to side effect, and the key decisions. Aim for three decisions
when the change has enough substance. For each, give the reason, a relevant
alternative, and the tradeoff. Separate documented requirements from choices
made by the agent.

Show one realistic failure and recovery path. Cite the relevant source. State
what changed, what stayed unchanged, and what the checks leave unverified.
Do not invent a failure mode or treat source inspection as runtime evidence.

## Ask, then wait

Ask three short scenario questions, or fewer for a small change. Test whether
the user can predict behavior, explain a decision, or recover from a failure.
Use the actual change rather than trivia about names or syntax.

Do not give answers, an answer key, or leading hints with the questions.
Stop and wait for the user's answers.

## Check the answers

Compare each answer with the source and contract. Say what is correct, name
any gap, and explain it with a concrete example. Ask a focused follow-up when
an answer is unclear. Mark questions unresolved when the available evidence
cannot establish the answer.

This skill checks understanding. It does not certify readiness, create a merge
gate, edit code, or authorize commits, pushes, or deployment.
