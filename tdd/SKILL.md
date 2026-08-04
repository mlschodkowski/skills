---
name: tdd
description: Test-driven development broken into planning contracts (Pre-Implementation) and execution loops (Construction). Driven entirely from public interfaces and vertical tracer slices.
---

# Test-Driven Development (TDD)

Execute TDD in two distinct phases: first as an architectural strategy to bake into the implementation plan, and second as a strict execution loop.

> **Architectural Guardrail:** Align all test strategies, interface boundaries, and mocking setups with the repository standard in `../principles.md`. Do not build decoupled mocks or complex interfaces outside those boundary rules.

---

## PHASE 1: Strategy & Contract Design (Incorporate into Plan)
Do this *before* any implementation code is written. Use this step to anchor your planning phase in concrete code design.

1. **Interface Contract:** Define the exact public interface signatures, types, and module entry points. Keep modules deep (small interface, heavy implementation).
2. **Behavior Checklist:** List the explicit, user-observable behaviors that represent success. Do not list implementation steps; list behavior inputs and expected outcomes.
3. **Boundary Isolation:** Identify system boundaries (external APIs, time, DB) that require dependency injection. Confirm no internal logic will be mocked.

*Add this contract and behavior checklist directly into the implementation plan. Use `hyperplan` before implementation when architecture or delivery risk is unclear.*

---

## PHASE 2: Execution Loop (Construction)
Run this loop iteratively for each behavior defined in your Phase 1 checklist.

              ┌─────────────────────────┐
              ▼                         │
[ RED ] ──> [ GREEN ] ──> [ SIMPLIFY & REFACTOR ]

1. **Tracer Bullet:** Select the thinnest vertical behavior from your checklist. Write a single test that fails (RED).
2. **Minimal Code:** Write the absolute bare minimum code required to make that specific test pass (GREEN). No speculative features or "just-in-case" flexibility.
3. **Simplify & Refactor:** **CRITICAL GATE.** The moment the test turns green, apply `simplify-codebase` to the new code. Use the refactoring triggers in `../principles.md` to flatten logic, remove indirection, and keep only earned abstractions before moving to the next behavior.

---

## TEST CALIBRATION

### Good Tests (Integration-style, Observable Behavior)
Tests public interfaces, describes WHAT the system does, and survives internal refactoring.
```python
# GOOD: Tests observable behavior via public API
def test_user_can_checkout_with_valid_cart():
    cart = create_cart()
    cart.add(product)
    result = checkout(cart, payment_method)
    assert result.status == "confirmed"
    ```

### Bad Tests (Implementation-detail Coupled)
Mocks internal collaborators, asserts on call order/counts, or tests private methods. Breaks during minor refactoring even if behavior remains correct.

```js
// BAD: Coupled to internal structure and mocking own code
test("checkout calls paymentService.process", async () => {
    const mockPayment = { process: vi.fn() };
    await checkout(cart, mockPayment);
    expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

Checklist Per Cycle:
[ ] Behavior is defined in the plan's checklist before coding.

[ ] Test uses the public interface only (zero internal mocking).

[ ] Code written is the absolute minimum to pass.

[ ] simplify-codebase was applied immediately upon hitting GREEN.
