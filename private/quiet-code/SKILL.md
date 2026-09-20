---
name: quiet-code
description: Use when a coding task asks for cleaner, simpler, more readable, or structurally elegant implementation code within an existing architecture across application, backend, data, scripts, tests, or infrastructure. Do not use for system architecture, API design, or domain-modeling decisions.
---

# Quiet Code

Quiet code shapes implementation code, not system architecture. Start from the
repository's existing boundaries and reduce reader effort without changing
behavior or inventing a new structural direction.

## Scope

Use this skill for functions, types, local file and package layout, errors,
state, tests, and small collaborators. Keep system boundaries, public API
strategy, persistence topology, deployment shape, and domain decomposition
under the repository's existing design decisions.

When a code change appears to require a new architectural boundary, surface that
decision explicitly and keep this skill focused on the implementation impact.

## Composition

Shape code so a reader can quickly find:

- the entrypoint and the main operation;
- the domain terms and invariants that matter;
- the boundaries where effects occur;
- the expected and failed outcomes; and
- the owner of each responsibility.

Use a small, visible group for each conceptual phase. Keep supporting mechanics
behind named local boundaries. Give semantic emphasis to important decisions,
not to clever identifiers or decorative structure. Let unusual domain behavior
remain explicit instead of flattening it into a generic abstraction.

## Operating Method

### 1. Establish the local contract

Read the task, the relevant files, nearby callers, tests, configuration,
external contracts, and existing local changes. Identify current behavior,
desired behavior, invariants, side effects, and failure cases.

Before editing, be able to name the entrypoint, affected callers, relevant
checks, and meaningful effects. Mark anything still unknown instead of filling
the gap with an assumption.

### 2. Trace one understandable path

Describe the normal path in one sentence:

```text
input → normalize → decide → effect → result
```

Open helpers for implementation detail, not to reconstruct the intent of the
feature. Keep exceptional paths beside the normal path through early returns,
explicit result types, or named policies.

Check: the normal path can be explained using domain-named operations without
walking a large file tree.

### 3. Compose and co-locate

Prefer a readable sequence:

```text
receive → normalize → reject or short-circuit → derive → decide → commit → return
```

Keep a concept's definition, invariants, constructor or parser, primary
operations, errors, and direct tests near each other when they form one cohesive
behavior. Prefer the shortest understandable path through the file tree:

- keep related code in the same file or package when it changes together;
- keep directories shallow and names predictable;
- place a small abstraction near its primary consumer and implementation;
- split code only when cohesion, ownership, effects, or local convention justify
  the extra jump; and
- follow the repository's test locality convention rather than scattering tests
  far from the code they explain.

Introduce an interface, trait, protocol, or function boundary only where a
dependency changes independently, performs an effect, or needs an isolated
test seam. Keep the boundary minimal and within the existing architecture.

Check: a developer can understand one behavior without traversing unrelated
directories or opening a chain of pass-through helpers.

### 4. Verify the result

Run the narrowest relevant formatter, linter, test, build, or type check. Inspect
the final diff and verify the changed path rather than trusting aesthetic
confidence.

Check that:

- behavior and existing contracts are preserved or intentionally changed;
- normal, invalid, boundary, and failure paths are explicit;
- every meaningful effect has one owner;
- abstractions remove duplicated knowledge or branching;
- no dead code, hidden work, or silent fallback was introduced; and
- observed checks are separated from behavior that remains unverified.

For a formal multi-axis review or pre-merge audit, use `$code-review-and-quality`.
Keep this skill focused on implementation code, not on prescribing a review
report or an architecture.

## Domain-Driven Design for Code

Use Domain-Driven Design as a local vocabulary and cohesion discipline, not as a
reason to redesign the system.

- **Ubiquitous language**: use the domain's stable terms in types, functions,
  files, tests, and errors.
- **Entity**: keep behavior that protects an existing identity and lifecycle
  close to that type.
- **Value object**: keep validation, equality, and behavior for a meaningful
  value together.
- **Aggregate**: when the code already has an aggregate, keep its invariants
  behind its existing entrypoint; do not invent one merely to reorganize files.
- **Domain service**: use a focused function or type only when a rule does not
  naturally belong to one existing domain type.
- **Application service**: keep existing use-case orchestration readable and
  separate from the domain calculation it coordinates.
- **Bounded context**: treat the existing module or package boundary as a
  constraint unless the user explicitly asks for architectural design.

DDD reinforces locality because code that expresses one domain concept should be
easy to find together. Locality itself is a code-organization and cognitive
load rule; it does not require a new domain model.

## Programming Principles

Apply formal principles as implementation decisions:

- **Cohesion**: keep code that changes for the same reason together.
- **Coupling**: make dependencies explicit and keep their direction deliberate.
- **Information hiding**: expose behavior and invariants, not incidental
  representation.
- **Separation of concerns**: keep parsing, policy, orchestration, and effects
  distinct when they change for different reasons.
- **Design by contract**: make preconditions, invariants, postconditions, and
  failure outcomes visible in types, names, or control flow.
- **Referential transparency where practical**: keep domain calculations free
  from I/O, time, randomness, and environment access so they can be reasoned
  about independently.

## Code Rules

### Functions and types

Give a function one primary responsibility and one readable path. Keep cohesive
logic together when extraction would create wrappers without reducing concepts.
Use nouns for values and types, verbs for operations, and `is`, `has`, `can`, or
`should` for predicates. Prefer names such as `unpaidInvoice`, `retryPolicy`,
`parseConfiguration`, and `reserveCapacity` over `data`, `result`, `process`, or
`handle`.

### Effects, errors, and state

Keep I/O, filesystem, process execution, time, randomness, and environment access
visible at the existing effect edges. Represent expected alternatives with enums,
tagged results, optionals, or the language's equivalent. Preserve error context.
Distinguish not-found, not-applicable, invalid, and failed outcomes. Make
unknown input and fallback behavior explicit and justified.

### Repetition and abstraction

Use data when cases share one invariant and differ only by values. Use separate
code when ownership, invariants, failure semantics, or reasons to change differ.

Extract an abstraction when it has a real repeated behavior, removes duplicated
knowledge or branching, and has a clear owner. Delete pass-through wrappers,
no-op variables, stale compatibility layers, and confirmed dead branches.

## Structural Remedies

When code feels noisy, choose the smallest move that removes a concept or
clarifies its owner:

- separate orchestration from pure domain logic;
- move feature rules out of shared utility code;
- replace a conditional chain with typed state, a named policy, or a dispatcher;
- make an unclear local boundary explicit;
- extract a focused collaborator only when it reduces reader effort;
- split a file by ownership rather than arbitrary line count;
- replace scattered flags with one meaningful state model; or
- convert repeated case logic into data when the cases share an invariant.

## Examples

Read [references/examples.md](references/examples.md) when a concrete
implementation shape would help.

## Completion Checklist

Before handing off, confirm:

- the local contract, entrypoint, callers, effects, and relevant checks are
  known;
- the main path is readable as a domain-named sequence;
- related definitions, behavior, errors, and tests are co-located where
  practical;
- the existing architecture and public boundaries were preserved;
- failure and unknown states are visible;
- each abstraction has a demonstrated reason to exist;
- relevant checks ran and the final diff was inspected; and
- any remaining device, production, release, or integration evidence is called
  out as unverified.

Quiet code is not code with no detail. It is code where each detail has a clear
place, owner, and reason to exist.
