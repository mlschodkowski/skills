# Spec document reviewer

Use this prompt when dispatching a spec reviewer. Verify the spec is
complete, consistent, and ready for implementation planning.

Review the spec at `[SPEC_FILE_PATH]`. Flag only issues that would cause
real problems during planning: TODOs and placeholders, internal
contradictions, requirements ambiguous enough to build the wrong thing,
scope that covers several independent subsystems, unrequested features.
Minor wording and uneven detail are not issues. Approve unless a gap
would lead to a flawed plan.

```text
## Spec review

**Status:** Approved | Issues Found

**Issues (if any):**
- [Section]: [issue] — [why it matters for planning]

**Recommendations (advisory, do not block approval):**
- [suggestion]
```
