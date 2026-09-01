# Spec document reviewer

Use this prompt when dispatching a spec reviewer. Verify the spec is
complete enough to plan from: consistent, legible ownership and
constraints, and free of gaps that would force rediscovery later.

Review the spec at `[SPEC_FILE_PATH]`. Flag only issues that would cause
real problems during planning: TODOs and placeholders, internal
contradictions, requirements ambiguous enough to build the wrong thing,
scope that covers several independent subsystems, unrequested features,
missing failure or boundary conditions when those would change the plan.
Minor wording and uneven detail are not issues. Completeness of what
planners need matters more than polish. Approve unless a gap would lead
to a flawed plan.

```text
## Spec review

**Status:** Approved | Issues Found

**Issues (if any):**
- [Section]: [issue] — [why it matters for planning]

**Recommendations (advisory, do not block approval):**
- [suggestion]
```
