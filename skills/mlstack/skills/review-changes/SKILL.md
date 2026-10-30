---
name: review-changes
description: Review a diff, branch, PR, or working changes for correctness, repository standards, spec fit, security risks, and needless complexity. Return evidence-backed findings without editing code or posting a review.
---

# Code review

Read [stack rules](../mlstack/references/rules.md).

## Scope

Resolve the requested base, commit, PR, or working changes. For a branch,
determine its actual base and compare from the merge-base. For a working-tree
review, include staged and unstaged changes and relevant untracked files.
State the reviewed revision and scope. Ask only when plausible choices would
review different work and context cannot resolve the choice.

Read the request or spec, repository standards, changed code, callers, and
relevant tests. If the spec is missing, say so and assess observable correctness;
do not require a particular issue tracker or setup skill.

## Review lenses

- **Correctness:** trace triggers through state, side effects, errors, lifecycle,
  concurrency, and recovery. Check the calls around a changed function.
- **Spec:** identify missing behavior, wrong behavior, and additions outside the
  request. Separate a requirement from an inferred intention.
- **Standards:** cite documented rules. Treat design smells as judgment calls;
  a preference alone is not a defect.
- **Risk:** inspect authorization, input boundaries, data loss, compatibility,
  resource use, and tests where the change reaches them.
- **Simplicity:** apply [clean-code](../clean-code/SKILL.md). Preserve real boundaries and controls.

Work in the current agent. If independent reviewers are explicitly requested
and supported, give each a bounded, read-only scope. Re-read every consequential
claim yourself. Never claim model consensus from one review.

## Validate findings

Compare each claimed regression with the actual base. Separate introduced
defects, pre-existing defects, scope changes, and optional improvements. A seeded
state that the public flow cannot create needs that prerequisite stated. Assess
whether a test failure blocks the requested behavior rather than treating every
failing assertion as equal evidence.

For each candidate, identify a concrete trigger, reachable failure path,
affected behavior, and source location. Seek the control or caller that could
disprove it. Drop disproved claims. Label unresolved risks and the missing fact.
Run a focused non-mutating check when available and relevant. Do not edit source,
weaken tests, or run a full security audit as a side effect of a normal review.

## Report

Lead with actionable findings, ordered by impact. For each, give priority,
`path:line`, trigger, impact, evidence, and the smallest useful correction.
Tag the lens as Correctness, Spec, Standards, Security, or Simplicity.
Keep confirmed defects separate from suggestions and open questions.

If no actionable finding remains, say so. State the scope, important checks run,
missing spec or execution evidence, and what remains unverified. Leave code,
PR comments, and approval state unchanged unless separately requested.
