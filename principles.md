# Architectural & Testing Principles

## 1. Deep Modules
Aim for deep modules (small interface + massive hidden implementation) over shallow modules (large interface + thin pass-through logic).
* Reduce public method counts.
* Minimize and simplify method parameters.

## 2. Interface Design for Testability
* **Inject Dependencies:** Accept external boundaries as parameters; do not instantiate clients internally.
* **Return Results:** Prefer pure functions returning data shapes over mutating shared state pointers or generating hidden side effects.

## 3. Boundary Mocking Protocol
Mock strictly at system boundaries that you do not control:
* External APIs (Payment gateways, third-party notification wrappers).
* Time, randomness, and direct disk file-system calls.
* **NEVER** mock internal collaborators, business logic units, or code within your local repository control.

## 4. Refactoring Triggers
Post-Green TDD checks: Duplication (Rule of Three), Primitive Obsession (introduce value objects), Feature Envy (move methods closer to data), and Deepening shallow abstractions.
