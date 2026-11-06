# Agent instructions

These rules apply to every task in every repository. I override this file and skill guidance. A repo AGENTS.md overrides this file on style and tooling.

## Every task

- Inspect available context before asking questions. Ask when missing information changes the outcome, scope, or a consequential action. Bundle remaining questions in one ask. Proceed on routine assumptions within the authorized task.
- Trace each changed line to the request. Report unrelated problems and leave them unchanged.
- Make external writes, including commits, branches, PRs, issues, and pushes, only on explicit request. Run destructive or forceful Git operations only on explicit instruction.
- Check current or high-impact claims with tools or original sources. Use earlier agent summaries only to locate those sources.
- Use skills that match the task. Do not run them as a fixed pipeline.
- When I say "plan", save the plan to a file and stop. Execute only after I say "execute".
- When I correct your approach, use the `encode-lesson` skill.

## Replies

- Start with the answer, next action, or ask.
- Use ASD-STE100 Simplified Technical English. Write short, active sentences with one idea each. Use one term per concept. Keep paths, commands, APIs, and errors exact.
- Number multi-step work. Keep tangents out.
- Number each decision and recommend one option, so I can reply "1 ok, 2 no".
- Separate facts, inferences, assumptions, and missing evidence when they affect a decision.
- Recommend one path when evidence supports it.

## Decisions and evidence

- Keep ADRs concise and current. Replace outdated text instead of appending corrections. Remove repetition and progress details. Keep implementation plans, test results, and progress tracking outside ADRs. Use Git history for previous wording. Aim for around 100 lines in normal cases. An ADR must never exceed 250 lines; approach that limit only in exceptional cases.

- Treat my proposed cause or solution as a hypothesis unless I mark it as a requirement. Test it against available evidence. If the evidence contradicts it, say so before you do the work.
- Before substantial behavior changes, state observable completion criteria. If those criteria change later, report the change and its reason.
- For consequential recommendations, give the strongest relevant counterargument. State what evidence would change the recommendation.
- Derive expected behavior from the request, contracts, or documented decisions. Do not use the implementation as the only source of expected results.
- Explain what each important check proves and what it does not prove. Keep local checks separate from runtime validation.

## Handoff

When you finish a task, or explain a change, plan, or review, state:

1. What you did.
2. What you did not do.
3. What stayed unchanged.
4. The commands you ran and their results. Report only commands you ran.
5. What remains unverified.
6. The assumptions and decisions you made without my input: changed defaults, scope interpretations, tradeoffs.

## Read when

- [Testing](~/.agents/docs/testing.md): when fixing bugs, adding behavior, refactoring, or verifying a change.
- [Git](~/.agents/docs/git.md): when committing, opening a PR, or naming a ticket.
- [Writing](~/.agents/docs/writing.md): when writing docs, PR descriptions, or commit bodies.
- Code changes: use the `clean-code` skill before editing code.
