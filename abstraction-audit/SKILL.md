---
name: abstraction-audit
description: Audit every abstraction created, changed, or explicitly proposed in a coding task or diff. Explain its responsibility, cost, concrete need, and keep/simplify/defer/remove decision. Use when a user asks to justify abstractions, review added layers, or decide whether an object, interface, helper, dependency, configuration, or test seam earns its cost.
---

# Abstraction Audit

Create a concise decision record for each in-scope abstraction. Prefer plain functions, simple data, and concrete dependencies unless an abstraction earns its cost now.

## Scope

Audit every abstraction created, changed, or explicitly proposed by the task, diff, or user. Do not audit every existing abstraction encountered while tracing the code unless it is explicitly brought into scope.

Treat these as abstractions when they hide a policy, boundary, or meaningful behavior:

- types and objects;
- interfaces, protocols, factories, strategies, modules, and layers;
- helpers that hide a meaningful decision;
- configuration, dependencies, retries, state, and policy objects;
- test fixtures, helpers, and seams.

Do not list ordinary private functions or local values that only make direct code easier to read.

## Audit

1. Establish the contract.
   - Read the task, diff, entrypoints, callers, and tests needed to understand each item.
   - Identify behavior, failures, observability, compatibility, and existing patterns that constrain the decision.
   - For tests, identify the public behavior, boundary, failure mode, or regression each test must prove.
   - Completion: every in-scope abstraction has enough context for a keep or remove decision.

2. Explain each abstraction.
   - State its responsibility in one sentence.
   - State the boundary it protects, if any.
   - State its cost: indirection, state, coupling, configuration, dependency, or test burden.
   - State why it earns that cost now. If the reason is future-only, name the concrete committed trigger that will make it necessary.
   - Completion: no entry relies on “we may need it later.”

3. Decide.
   - Keep an abstraction that has a real current responsibility, boundary, or established codebase role.
   - Simplify one that has a valid job but more machinery than its job needs.
   - Defer one that will be needed only after a specific future change.
   - Remove one that only supports imagined reuse, scale, flexibility, or modes that do not exist.
   - Completion: every entry has one clear decision and a concrete next action.

## Tests

Apply the same rules to test code:

- Keep a fixture, helper, mock, builder, or test seam only when it makes a real test boundary clearer or removes repeated setup without hiding the behavior under test.
- Prefer tests that prove public behavior, business rules, failures, compatibility, and regressions.
- Do not keep tests that only assert private implementation steps or mock calls without a useful outcome.
- Add a case only when it reaches a distinct branch, boundary, invariant, failure, data shape, permission, or regression.
- Do not add a test abstraction for imagined future scenarios. Add it when repeated, current test work proves it earns its cost.

## Output

Use one short row per abstraction:

| Abstraction | Responsibility and need now | Cost | Decision |
| --- | --- | --- | --- |
| `Name` | What it owns or protects; why it is needed now | What extra complexity it adds | Keep, simplify, defer, or remove; next action |

Keep the explanation plain. Use exact code names and evidence from the diff or callers. State uncertainty instead of guessing.

Minimal example:

| Abstraction | Responsibility and need now | Cost | Decision |
| --- | --- | --- | --- |
| `PaymentGateway` interface | One live provider; no caller needs substitution | Extra file and indirection | Remove. Inject `StripeClient` directly; add an interface when a second provider is being implemented. |
