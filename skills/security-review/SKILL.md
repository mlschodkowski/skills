---
name: security-review
description: Audit source code for exploitable trust-boundary failures, including authorization, injection, secrets, supply chain, cloud, data isolation, and AI tools. Use for security audits or focused vulnerability reviews; report evidence and coverage gaps.
---

# Security audit

Read [stack rules](../mlstack/references/rules.md).

This workflow adapts Cloudflare's source-first audit and mroowa's scoped levels.
It runs in one agent and requires no model panel, sandbox product, or plugin.
Use independent verification only when delegation is requested and available;
otherwise identify the review as a single-agent audit.

## Scope and evidence

Record the target, revision, dirty worktree state, request, and excluded paths.
For a focused question, inspect that boundary. For a broad audit, default to a
standard source review. State the depth and scope:

- **Quick:** inspect the highest-risk entry paths. State which paths you sampled.
- **Standard:** map entry surfaces and trust boundaries, then examine the relevant
  attack classes across the requested scope.
- **Deep:** add local validation where safely available, revisit coverage gaps,
  and retain a report when requested. More depth is not proof of completeness.

Use inline findings unless the user requests files. For saved reports, use an
authorized output directory and keep source unchanged. No level requires
subagents, a particular output schema, or executing the target.

## Audit

1. **Map:** identify lower-trust principals, entry points, identity propagation,
   resource ownership, sensitive sinks, and existing controls. Include alternate
   routes, jobs, queues, imports, exports, and recovery paths in scope.
2. **Cover:** use [threat-checks.md](references/threat-checks.md). For each relevant
   surface and attack class, record `checked`, `candidate`, `blocked`, or
   `not checked`, with a source location or reason. Inapplicable classes need
   only a short reason. Prior reports guide checks; recheck changed source.
3. **Trace:** follow each candidate from attacker-controlled input to a sensitive
   effect. Name the principal, resource, crossed boundary, prerequisites, and
   strongest control. Search for an upstream or downstream control that defeats
   the claim. Deduplicate candidates by root cause.
4. **Validate:** try to disprove each candidate. Use source and an existing safe
   local fixture. If a decisive fact needs unavailable runtime state, preserve
   that exact uncertainty. Do not infer exploitability from a pattern match,
   package version, or missing defense-in-depth control alone.
5. **Report:** present supported findings and coverage gaps. Recommend the
   smallest control at the owning boundary. Leave remediation as separate work
   unless the user requested fixes.

## Local validation boundary

Static reading is the default. Before running target-controlled code, use an
isolated environment with synthetic principals and data, no ambient credentials,
bounded resources and time, no external network, and writes confined to a
disposable workspace. Inspect the proposed command and its effects first.
If those controls are unavailable, keep the lead as `needs validation`.

Do not probe live services, other tenants, production credentials, or shared
infrastructure as part of a source audit. Such work needs an explicit scope and
authorization. Keep the reproduction to the minimum local effect that proves
the boundary failure. Redact secrets; report their location instead of value.

## Finding states

- **Confirmed:** a complete current-source trace and an observed, bounded local
  result establish the boundary failure. Include the exact command and result.
- **Likely:** source establishes a reachable boundary failure, but it was not
  executed. Label impact and severity provisional.
- **Needs validation:** the claim depends on a named unresolved fact. Include
  that fact and a safe check. Assign no severity yet.
- **Rejected:** evidence disproves the candidate. Keep a short reason when a
  saved report needs the decision trail; omit noise from inline findings.

Severity follows supported impact and prerequisites. Missing hardening alone
does not establish a vulnerability. Check current advisories against primary
sources when dependency findings rely on affected versions.

## Output

Lead with actionable findings. For each include state, severity when supported,
`path:line`, principal, affected resource, trace, failed control, prerequisites,
observed or inferred result, and smallest fix. Separate unresolved leads.

State revision, scope, coverage, checks actually run, blockers, and unreviewed
surfaces. A clean sampled pass means no supported finding in the checked scope.
It does not certify the repository as secure.
