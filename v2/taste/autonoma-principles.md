# Autonoma

Autonoma is a design philosophy and technical standard for creating software, systems, interfaces, and technical artifacts whose form is appropriate to their purpose, context, constraints, and use.

It is concerned with both **what a thing is** and **how it is made**.

Its central question is:

**Does the form of the thing follow from the thing itself?**

A design is stronger when its structure can be explained by real requirements, relationships, constraints, and use rather than by fashion, abstraction for its own sake, or the preferences of its creator.

Autonoma does not prescribe minimalism, simplicity, or conventionality. Complexity is acceptable when the problem requires it. Simplicity is valuable when complexity does not.

## 1. Purpose determines structure

Software should be structured around what it actually does.

Responsibilities, boundaries, APIs, data models, and abstractions should correspond to meaningful concepts in the problem and system.

A module should exist because there is a meaningful responsibility to isolate. An abstraction should exist because several things share a meaningful concept or because a boundary provides a real benefit.

Do not introduce structure before there is a reason for it.

Do not remove structure merely because it looks complex.

**Technical standard:** Every significant structural element should have an identifiable responsibility, relationship, constraint, or operational purpose.

## 2. Prefer the form native to the context

Software exists inside an ecosystem.

A new component should fit the language, framework, repository, deployment environment, operational model, and conventions around it.

Established conventions should be preferred when they already express the required behavior adequately.

This reduces cognitive load and allows existing knowledge to transfer.

Deviation is appropriate when the existing form does not fit the actual problem.

**Technical standard:** New code should follow existing local conventions unless there is a concrete reason to introduce a different form.

## 3. Boundaries should represent reality

A boundary is useful when it corresponds to something real.

Good boundaries commonly follow ownership, responsibility, lifecycle, consistency requirements, security, deployment, or independent change.

Bad boundaries exist only because a diagram looks cleaner when divided into more boxes.

A service should not be separated merely because “microservices are cleaner.” A module should not own data merely because its name suggests that it should.

**Technical standard:** Define boundaries around real differences in responsibility, ownership, lifecycle, consistency, failure, or change.

## 4. Abstractions should earn their existence

Abstraction is a tool for managing complexity, not evidence of sophistication.

An abstraction is justified when it removes meaningful duplication, isolates meaningful variation, establishes a useful contract, or expresses an important domain concept.

Premature abstraction hides information before there is enough information to know what should be hidden.

**Technical standard:** Prefer concrete implementations until a stable concept, repeated behavior, or meaningful boundary justifies abstraction.

## 5. Make relationships legible

The important relationships in a system should be understandable from its structure.

A reader should be able to determine where behavior belongs, who owns data, what depends on what, and where changes will propagate.

Names, types, interfaces, directory structure, dependency direction, and data flow should reinforce this understanding.

The implementation does not need to expose every detail.

It should expose the details necessary to construct an accurate mental model.

**Technical standard:** Important ownership, dependency, lifecycle, and data-flow relationships should be represented explicitly rather than requiring extensive external explanation.

## 6. Minimize accidental complexity

Complexity that comes from the problem is unavoidable.

Complexity introduced by the design is not.

Distinguish between the two.

A distributed system may require retries, idempotency, observability, failure recovery, and eventual consistency. Removing those concepts from the code does not make the system simpler; it merely moves the complexity somewhere less visible.

Autonoma therefore does not minimize complexity indiscriminately.

It minimizes **complexity that has no corresponding requirement**.

**Technical standard:** For every significant abstraction, dependency, state transition, configuration option, or architectural component, there should be a reason tied to system behavior or constraints.

## 7. Prefer explicit mechanisms over unnecessary machinery

Mechanisms should be as direct as the problem allows.

Prefer a normal function over a framework when a function is sufficient. Prefer a direct dependency over an abstraction layer when substitution provides no value. Prefer explicit data flow over implicit global behavior.

Machinery is justified when it provides capabilities that the simpler mechanism cannot provide adequately.

**Technical standard:** Use the smallest mechanism that satisfies the actual requirement without compromising correctness, operability, or future change.

## 8. Preserve information until there is a reason to hide it

Every abstraction hides something.

Hiding information can make a system easier to use, but it can also make behavior harder to understand and debug.

Information should therefore be hidden at deliberate boundaries, not merely because encapsulation is considered universally good.

The public API should expose what consumers need to depend on. Internal implementation should remain internal when exposing it would create unnecessary coupling.

**Technical standard:** Hide implementation details that consumers should not depend on, while keeping behavior, contracts, state transitions, and important failure modes observable.

## 9. Design for change through stable boundaries

Change is inevitable, but its exact form is difficult to predict.

Do not attempt to make every part replaceable.

Instead, identify where change is likely to occur and keep those boundaries stable.

A stable interface between volatile implementations is useful. A generalized extension mechanism for hypothetical future requirements usually is not.

**Technical standard:** Optimize for cheap, localized change rather than universal extensibility.

## 10. Treat operational behavior as part of the design

Software does not end at compilation.

Startup, shutdown, deployment, configuration, observability, failure, recovery, migration, scaling, and maintenance are part of the system.

A design that is elegant in source code but difficult to operate is incomplete.

**Technical standard:** Operational behavior must be considered part of the interface and architecture, not an implementation detail added after development.

## 11. Design for failure, not only success

Failure is part of normal system behavior.

Errors, timeouts, partial failure, retries, unavailable dependencies, invalid input, and interrupted operations should have deliberate behavior.

Do not allow failure semantics to emerge accidentally from implementation details.

**Technical standard:** For every external dependency or state-changing operation, define relevant failure behavior, retry semantics, idempotency requirements, and recovery strategy.

## 12. Let interfaces communicate contracts

An interface is not merely a collection of methods or endpoints.

It defines what another component can assume.

Types, names, validation, errors, state transitions, defaults, and side effects should make those assumptions clear.

An interface is good when correct usage is natural and incorrect assumptions are difficult to make.

**Technical standard:** Contracts should be explicit in types, schemas, names, validation, documentation, and observable behavior wherever practical.

## 13. Consistency is a form of usability

Consistency allows knowledge to transfer.

If two operations behave similarly, they should normally look and behave similarly. If they differ, the difference should correspond to a real difference in behavior.

Consistency applies to APIs, naming, errors, configuration, UI behavior, architecture, and operational procedures.

Do not standardize differences away when those differences carry meaning.

**Technical standard:** Reuse conventions for equivalent concepts and preserve distinctions that correspond to meaningful behavioral differences.

## 14. Change existing things carefully

Existing software contains accumulated knowledge.

It also contains accumulated dependencies, assumptions, workarounds, and operational history.

Changing it should therefore begin with understanding what already exists.

Prefer localized corrections when the problem is localized. Broader redesign is justified when the existing structure itself prevents the required behavior.

**Technical standard:** Before changing an established system, identify its current responsibilities, consumers, dependencies, invariants, and observable behavior. Change only the scope required by the problem.

## 15. Completeness is more important than appearance

A technically elegant design that ignores inconvenient requirements is not elegant.

Tests, validation, migrations, rollback, access control, monitoring, documentation, compatibility, and edge cases may not improve the visual simplicity of a system.

They improve the system itself.

**Technical standard:** Do not remove necessary behavior merely because it makes the design less aesthetically clean.

## 16. Use language precisely

Technical language is part of the system.

Names, comments, documentation, APIs, error messages, diagrams, and specifications should communicate the actual behavior of the thing.

Avoid terminology that sounds architectural without conveying a concrete distinction.

Prefer precise language over fashionable terminology.

**Technical standard:** Every important term should have a stable meaning within its context, and names should describe behavior, responsibility, or domain concepts rather than implementation fashion.

## 17. Optimize for use, not inspection

Software is used repeatedly by people and other systems.

Code is read, modified, operated, debugged, tested, and extended far more often than it is initially written.

Architecture is operated rather than admired.

Interfaces are learned through repetition.

Optimize for these activities rather than for the appearance of sophistication during review.

**Technical standard:** Evaluate designs by how easily they can be understood, used, changed, tested, operated, and debugged—not by how impressive they appear in isolation.

## 18. Remove what has no job

Every element should contribute to the system.

This applies to code, configuration, abstractions, services, dependencies, UI elements, processes, documentation, and architectural components.

Removal is valuable when it eliminates something without removing necessary capability.

But minimality is not the objective.

**Technical standard:** Remove elements that provide no necessary behavior, constraint, clarity, safety, or future value. Keep elements whose contribution is justified even when they increase apparent complexity.

## The Autonoma test

A design should be questioned when its form cannot be explained by the thing itself.

Why does this abstraction exist?

Why is this boundary here?

Why does this dependency exist?

Why does this state exist?

Why does this interface behave differently?

Why does this component need to be separate?

Why does this configuration exist?

Why does this complexity exist?

The answer should ultimately lead back to purpose, behavior, constraints, context, or use.

If the answer is only convention, fashion, theoretical flexibility, architectural taste, or “because this is how we usually do it,” reconsider the form.

Autonoma does not seek the simplest system.

It seeks a system whose complexity has a reason.

It does not seek the most conventional system.

It seeks a system whose conventions fit.

It does not seek minimal code.

It seeks no unnecessary code.

It does not seek invisible design.

It seeks design that becomes natural through use.

**The form should follow the thing.**
