# mlstack

My skills for clear code, useful tests, simple explanations, and considered UI.
Works with any agent that can read Markdown. No required harness or model.

## Use

Copy the contents of `skills/mlstack/skills/` into your agent's skill directory.
Keep the folders together because
skills share references. Ask for a skill by name, or start with `mlstack`.

For example: “Use bug-diagnosis to investigate this failure” or “Use plan-work
and vertical-slices to prepare a plan. Do not implement it.”

## Repository layout

- `skills/mlstack/skills/` contains the current stack: 24 skills, including the
  router, the five pstack additions, and `wait-what`.
- [Package README](skills/mlstack/README.md) describes the copied stack.
- `skills/<name>/` contains older copies. Do not combine those copies with the
  nested stack during installation.
- `docs/` contains [code-change rules](docs/code-changes.md),
  [testing and verification](docs/testing.md), [Git rules](docs/git.md), and
  [writing rules](docs/writing.md).

## Skills

| Skill | What it does |
| --- | --- |
| [mlstack](skills/mlstack/skills/mlstack/SKILL.md) | Select the workflow for the task. |
| [plan-work](skills/mlstack/skills/plan-work/SKILL.md) | Resolve decisions, save a plan, and stop. |
| [vertical-slices](skills/mlstack/skills/vertical-slices/SKILL.md) | Split work into small end-to-end changes. |
| [clean-code](skills/mlstack/skills/clean-code/SKILL.md) | Make the smallest complete change with clear code. |
| [tdd](skills/mlstack/skills/tdd/SKILL.md) | Run one red–green–refactor cycle at a time. |
| [bug-reproduction](skills/mlstack/skills/bug-reproduction/SKILL.md) | Build a minimal check that shows the reported bug. |
| [bug-diagnosis](skills/mlstack/skills/bug-diagnosis/SKILL.md) | Find the cause from code, logs, metrics, and reproduction. |
| [review-changes](skills/mlstack/skills/review-changes/SKILL.md) | Review correctness, requirements, standards, and simplicity. |
| [security-review](skills/mlstack/skills/security-review/SKILL.md) | Find security vulnerabilities and report evidence gaps. |
| [babysit](skills/mlstack/skills/babysit/SKILL.md) | Watch CI and reviews; handle authorized fixes. |
| [commit-changes](skills/mlstack/skills/commit-changes/SKILL.md) | Commit the requested changes with a scoped message. |
| [create-pr](skills/mlstack/skills/create-pr/SKILL.md) | Open or update a PR with a short description. |
| [create-issue](skills/mlstack/skills/create-issue/SKILL.md) | Create an issue with What, Why, and Definition of Done. |
| [explain-code](skills/mlstack/skills/explain-code/SKILL.md) | Explain flow, ownership, and module design. |
| [interface-design](skills/mlstack/skills/interface-design/SKILL.md) | Improve layout, hierarchy, and interaction. |
| [interaction-motion](skills/mlstack/skills/interaction-motion/SKILL.md) | Build or review physical motion and haptic feedback. |
| [simple-language](skills/mlstack/skills/simple-language/SKILL.md) | Explain the problem, change, and result in simple language. |
| [wait-what](skills/mlstack/skills/wait-what/SKILL.md) | Re-pitch the goal, current state, and next action when an explanation loses the reader. |
| [session-handoff](skills/mlstack/skills/session-handoff/SKILL.md) | Save the state and next step for another session. |
| [create-verification-skill](skills/mlstack/skills/create-verification-skill/SKILL.md) | Create or maintain a runnable project verification skill. |
| [recall](skills/mlstack/skills/recall/SKILL.md) | Rebuild working context from history and current state. |
| [reflect](skills/mlstack/skills/reflect/SKILL.md) | Turn durable session lessons into scoped skill changes or structural checks. |
| [blast-radius](skills/mlstack/skills/blast-radius/SKILL.md) | Prove the critical safety assumption beyond a change’s diff. |
| [statechart](skills/mlstack/skills/statechart/SKILL.md) | Check a TLA+ model and draw states, rule failures, and bug paths. |

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

## Pstack additions

The five additions retain pstack's names and core workflows. Imported from
[cursor/plugins at 4dd1d05](https://github.com/cursor/plugins/tree/4dd1d05818d19792e7cd6e818f1667f95f7e1dbe/pstack).
The imported files use the [upstream MIT license](https://github.com/cursor/plugins/blob/4dd1d05818d19792e7cd6e818f1667f95f7e1dbe/pstack/LICENSE).

Local changes replace Cursor-only paths, model rosters, and unavailable sibling
skills with mlstack references and current-host tools. Delegation is optional.
Recall searches relevant shared sources instead of every source by default.
Reflect does not file backlog issues automatically. Existing authorization rules
apply. The verification maintenance workflow is a supporting reference, not a
sixth skill. Statechart scripts, tests, and rendering reference are unchanged.

Statechart needs a TypeScript-capable runtime and TLC with Java 11 or later.
Its launcher can provision TLC and Java with mise, or use `TLA2TOOLS` and `JAVA`.
Model checking proves properties of the model; replay bug paths against real code.

## Examples

- “Use create-verification-skill for DB4U approval cancellation. Reuse existing
  runners. Verify the callback and stored state. Run the generated recipe once.”
- “Use create-verification-skill to maintain the existing Rounds verification
  skill. Check its feature map against source and the running app.”
- “Use recall for my DB4U cancellation work from the last month. Check current
  branches and issue status. Tell me the next action; do not resume coding.”
- “Use reflect on this session. Show durable lessons, proposed skill edits, and
  checks that could enforce them. Do not apply edits yet.”
- “Use blast-radius on this restore-revert diff. Prove that the original
  entrypoint is restored. Keep unverified risks separate.”
- “Use statechart to model approval, cancellation, and late callbacks. Check
  that cancellation cannot grant access. Show the shortest violating path and
  replay it against the implementation.”
