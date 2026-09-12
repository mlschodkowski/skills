# Skill kit instructions

These rules keep the skill kit small, discoverable, and useful to more capable
models.

- Each skill must stand on its own: its description says what it does and when
  it applies. The body contains only the constraints and decisions needed for
  that job.
- Keep the root instructions stable. Put workflow-specific detail in the
  matching skill, and put conditional deep detail in a directly linked
  reference or script.
- Prefer judgment and clear completion conditions over fixed itineraries,
  repeated checklists, and instructions that merely restate the root
  AGENTS.md.
- Preserve user intent, scope, authorization, and existing invocation metadata.
  Do not turn a report-only or explicit-invocation skill into an automatic
  mutation workflow.
- When editing a skill, check its trigger against neighboring skills, keep
  examples only when they disambiguate behavior, and remove stale tool names,
  impossible steps, and duplicated policy.
- Validate every changed skill with the bundled quick validator. If its
  allowlist rejects an existing invocation or metadata key, preserve the key,
  report the validator mismatch, and run an equivalent frontmatter check.
  Then inspect links, boundaries, and a realistic trigger example.
