# mlstack

My skills for clear code, useful tests, simple explanations, and considered UI.
Works with any agent that can read Markdown. No required harness or model.

## Use

Add `skills/` to your agent's skill directory. Keep the folders together because
skills share references. Ask for a skill by name, or start with `mlstack`.

For example: “Use bug-diagnosis to investigate this failure” or “Use plan-work
and vertical-slices to prepare a plan. Do not implement it.”

## Skills

| Skill | What it does |
| --- | --- |
| [mlstack](skills/mlstack/SKILL.md) | Select the workflow for the task. |
| [plan-work](skills/plan-work/SKILL.md) | Resolve decisions, save a plan, and stop. |
| [vertical-slices](skills/vertical-slices/SKILL.md) | Split work into small end-to-end changes. |
| [clean-code](skills/clean-code/SKILL.md) | Make the smallest complete change with clear code. |
| [tdd](skills/tdd/SKILL.md) | Run one red–green–refactor cycle at a time. |
| [bug-reproduction](skills/bug-reproduction/SKILL.md) | Build a minimal check that shows the reported bug. |
| [bug-diagnosis](skills/bug-diagnosis/SKILL.md) | Find the cause from code, logs, metrics, and reproduction. |
| [review-changes](skills/review-changes/SKILL.md) | Review correctness, requirements, standards, and simplicity. |
| [security-review](skills/security-review/SKILL.md) | Find security vulnerabilities and report evidence gaps. |
| [babysit](skills/babysit/SKILL.md) | Watch CI and reviews; handle authorized fixes. |
| [commit-changes](skills/commit-changes/SKILL.md) | Commit the requested changes with a scoped message. |
| [create-pr](skills/create-pr/SKILL.md) | Open or update a PR with a short description. |
| [create-issue](skills/create-issue/SKILL.md) | Create an issue with What, Why, and Definition of Done. |
| [explain-code](skills/explain-code/SKILL.md) | Explain flow, ownership, and module design. |
| [interface-design](skills/interface-design/SKILL.md) | Improve layout, hierarchy, and interaction. |
| [interaction-motion](skills/interaction-motion/SKILL.md) | Build or review physical motion and haptic feedback. |
| [simple-language](skills/simple-language/SKILL.md) | Explain the problem, change, and result in simple language. |
| [session-handoff](skills/session-handoff/SKILL.md) | Save the state and next step for another session. |

Plans stop before implementation. Reviews stay read-only unless fixes are
requested. Commits, pushes, PRs, issues, and messages need an explicit request.

GitHub workflows use a connector or `gh`. The optional PR watcher also needs
Python 3.10+ and POSIX locking. UI and motion references load only when needed.

## Sources

Adapted from my private skills and session history, with ideas and references from
[mroowa-stack](https://github.com/jakub-mrow/mroowa-stack),
[tstack](https://github.com/t3dotgg/tstack),
[pstack](https://github.com/cursor/plugins/tree/main/pstack),
[Matt Pocock](https://github.com/mattpocock/skills),
[Emil Kowalski](https://emilkowal.ski/),
[ponytail](https://github.com/DietrichGebert/ponytail), and
[Cloudflare's security audit](https://github.com/cloudflare/security-audit-skill).
