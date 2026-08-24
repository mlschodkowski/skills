# Agent kit

Personal operating rules and focused procedures for coding agents. They work with any harness that reads `AGENTS.md` and a folder of named procedures.

Evidence before claims. Explicit decisions. Bounded changes. Verification in proportion to risk.

`AGENTS.md` holds invariants for every task. Each folder below is one job. Use only the path the work needs. Do not run them as a pipeline.

`taste/super-normal-principles.md` is the shared bar for code, architecture, fixes, and prose. The taste skills apply it. Other procedures should not name it; they should just do their job.

## Layout

```text
taste/     how work should feel
build/     decide, slice, implement, debug
check/     review the change
ops/       commit, handoff, docs, tooling
```

### taste/

- `super-normal-code` — ordinary code that fits the codebase; add structure only when needed
  *Example:* a rate limiter; prefer stdlib/`dict` over a new cache package.
- `super-normal` — ordinary prose and documents
  *Example:* a design doc where the decision and tradeoffs are obvious.
- `super-normal-ui` — familiar, calm interfaces
  *Example:* a settings form; platform controls instead of a custom widget kit.

### build/

- `grill-me` — design-tree pressure testing in question rounds  
  *Example:* before locking an API shape, answer hard cases about failure and ownership.
- `hyperplan` — hostile architecture and delivery review  
  *Example:* “Can we ship this migration in one release?” get a harsh plan review.
- `oracle` — final `GO`, `GO_WITH_CAVEATS`, or `NO_GO`  
  *Example:* last gate before a risky cutover.
- `slice-it-vertically` — thinnest end-to-end increment with a visible result  
  *Example:* first user-visible slice of “export reports”, not the full export platform.
- `brainstorming` — shape an unclear idea before a plan  
  *Example:* “we need better onboarding” → goals, options, and what to build first.
- `architecture-design` — domain, boundaries, and module shape  
  *Example:* split billing from catalog; name owners and contracts.
- `tdd` — public behavior contracts and red-green-refactor  
  *Example:* new pricing rule; write the failing behavior test, then the code.
- `diagnose` — repro loop for hard bugs  
  *Example:* flaky timeout in production; shrink, instrument, fix, lock with a check.

### check/

- `code-review` — review a diff as a behavior change  
  *Example:* PR changes retry logic; trace success, failure, and double-submit paths.
- `over-engineering-review` — diff-only complexity cut list  
  *Example:* PR adds a repository interface with one impl; list what to inline.
- `over-engineering-audit` — repo-wide complexity cut list  
  *Example:* “what can we delete from this service?” ranked cut list across the tree.
- `shortcut-debt` — harvest `limit:` markers into a ledger  
  *Example:* before a perf push, list every marked simple path and its upgrade trigger.

### ops/

- `git-commit` — scoped commits
  *Example:* stage only the auth fix; message `auth/session: reject empty bearer token`.
- `handoff` — compact context for another agent or session  
  *Example:* pause mid-migration; leave state, next step, and open risks.
- `github` — stacked PRs and `gh` workflows  
  *Example:* open PR 2 stacked on PR 1 without merging base first.
- `adr` — write an architecture decision record  
  *Example:* record “Postgres over Dynamo for orders” with context and consequences.
- `research` — cited primary-source findings  
  *Example:* “does this AWS API paginate?” answer from current docs with links.
- `writing-for-agents` — documents an agent must apply reliably  
  *Example:* edit a skill so the trigger and done-condition are unmistakable.
- `evidence-barrier` — shared evidence before cross-boundary writes  
  *Example:* two repos; do not change B until A’s findings are written down.
- `to-questionnaire` — collect facts or decisions from a specific person  
  *Example:* product owner must pick retention days before implementation.

## Use

Name a procedure to run it. Some fire from a matching request; others wait until you ask (`grill-me`, `tdd`, `hyperplan`, `oracle`, `code-review`, `over-engineering-review`, `over-engineering-audit`, `shortcut-debt`, `to-questionnaire`).

## Maintenance

Keep each procedure short and independently useful. One home per fact. Preserve exact identifiers and commands. Check a change against a real task before treating it as done.
