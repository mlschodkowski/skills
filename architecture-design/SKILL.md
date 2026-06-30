---
name: architecture-design
description: Architecture design for creating a new project architecture, reshaping an existing codebase, improving module boundaries, or cleaning up domain models. Use when the user asks for a new architecture, architecture plan, system shape, codebase design, domain modeling, modularization, service/module boundaries, or an architecture improvement plan; coordinate with brainstorming when the problem is still open and with grill-me when the user wants pressure testing.
---

# Architecture Design

Design architecture from the domain outward. The output is a concrete shape the user can implement: modules, boundaries, dependencies, domain model, migration slices, and verification.

## Workflow

1. **Classify the architecture job.**
   - New project: discover product goal, domain language, actors, core workflows, data ownership, integrations, non-functional constraints, and the first vertical slice.
   - Existing project: inspect the repo, docs, tests, dependency graph, public APIs, persistence boundaries, and known pain points before proposing changes.
   - Improvement request: identify the smallest boundary or model change that removes the current pain without starting a rewrite.
   - Completion: you can state whether this is new design, existing-codebase redesign, or targeted improvement, and name the primary architecture decision.

2. **Use optional companion skills deliberately.**
   - If goals, workflows, constraints, or success criteria are unclear, invoke `brainstorming` before drafting the architecture.
   - If the user asks to be challenged, says "grill me", or presents a plan that needs pressure testing, invoke `grill-me` after you have a concrete candidate.
   - If neither branch applies, continue directly.
   - Completion: every open strategic uncertainty is either answered, explicitly assumed, or routed to a question.

3. **Map the domain.**
   - List the domain nouns, verbs, lifecycle states, invariants, policies, and events using the project's language.
   - Separate true domain concepts from transport DTOs, database records, framework objects, UI state, and vendor API shapes.
   - Identify aggregate roots or ownership centers: the object, module, or service that owns each invariant and state transition.
   - Completion: each core workflow has an owner, each critical invariant has one enforcement home, and each external shape has an adapter or boundary.

4. **Design deep modules.**
   - Prefer modules with small public interfaces and substantial internal responsibility.
   - Push complexity behind stable capabilities instead of spreading it through callers.
   - Watch for shallow modules: wrappers that expose underlying details, pass-through services, managers with no clear invariant, and layers that exist only to mirror another layer.
   - Completion: every proposed module can be described by responsibility, public interface, private decisions, owned data, dependencies, and failure modes.

5. **Shape dependencies and boundaries.**
   - Draw or describe the dependency direction between domain, application workflow, infrastructure, UI/API, and external services.
   - Keep domain rules independent from delivery mechanisms unless the existing codebase deliberately uses another pattern.
   - Name cross-boundary contracts: commands, queries, events, repositories, ports, adapters, API schemas, or explicit function calls.
   - Completion: no dependency cycle or hidden shared mutable state is left unaccounted for.

6. **Plan implementation as vertical slices.**
   - For new projects, start with the smallest end-to-end slice that exercises the core model, persistence or state, and delivery path.
   - For existing projects, keep compatibility while moving one workflow, model, or boundary at a time.
   - Include migration steps, temporary adapters, deletion points, and fallback or rollback notes where risk warrants them.
   - Completion: the plan can be executed incrementally without a flag-day rewrite unless the user explicitly accepts that cost.

7. **Write the architecture.**
   - Keep the artifact scaled to the request: concise inline plan, durable doc, ADR, or implementation checklist.
   - Include: current context, goals/non-goals, proposed shape, module responsibilities, domain model, data/control flow, tradeoffs, migration slices, and verification.
   - For significant decisions, state the rejected alternatives and why they lost.
   - Completion: a future implementer can start work without rediscovering the boundaries.

8. **Verify the design against pressure points.**
   - Test the design mentally against the hardest workflow, failure path, data migration, concurrency case, integration outage, and likely future feature.
   - Check whether any module is too shallow, any domain concept is only a DTO in disguise, or any invariant is enforced in multiple places.
   - Completion: the final answer names the remaining risks, the first implementation slice, and the evidence still needed if uncertainty remains.

## Architecture Checks

- Domain-first: business rules have names and homes, not just tables, handlers, or controllers.
- Deep modules: simple interface, meaningful hidden complexity, clear ownership.
- Explicit boundaries: adapters at the edges, stable contracts between modules, dependency direction visible.
- Incremental path: each slice leaves the system working and removes or reduces a real ambiguity.
- Tradeoff honesty: name what the design makes harder, not only what it improves.

## Output Shapes

- **New architecture:** target structure, first vertical slice, core model, module map, integration map, and validation plan.
- **Existing-codebase improvement:** current pain, proposed boundary/model change, migration slices, compatibility strategy, and deletion plan.
- **Domain model cleanup:** vocabulary, lifecycle, invariants, ownership centers, persistence mapping, and API/DTO boundaries.
- **Grilled architecture:** candidate design, question log, resolved decisions, remaining weak assumptions, and revised design.
