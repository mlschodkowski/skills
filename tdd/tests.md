# Good and Bad Tests

## Good Tests

**Integration-style**: Test through real interfaces, not mocks of internal parts.

```python
# GOOD: Tests observable behavior
def test_user_can_checkout_with_valid_cart():
    cart = create_cart()
    cart.add(product)

    result = checkout(cart, payment_method)

    assert result.status == "confirmed"
```

Characteristics:

- Tests behavior users/callers care about
- Uses public API only
- Survives internal refactors
- Describes WHAT, not HOW
- One logical assertion per test

## Bad Tests

**Implementation-detail tests**: Coupled to internal structure.

```javascript
// BAD: Tests implementation details
test("checkout calls paymentService.process", async () => {
  const mockPayment = { process: vi.fn() };
  await checkout(cart, payment);
  expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

Red flags:

- Mocking internal collaborators
- Testing private methods
- Asserting on call counts/order
- Test breaks when refactoring without behavior change
- Test name describes HOW not WHAT
- Verifying through external means instead of interface

```go
// BAD: Bypasses interface to verify
func TestCreateUserSavesToDatabase(t *testing.T) {
    user, err := CreateUser(CreateUserInput{Name: "Alice"})
    if err != nil {
        t.Fatal(err)
    }

    row := testDB.QueryRow("SELECT name FROM users WHERE id = ?", user.ID)
    _ = row
}
```

```go
// GOOD: Verifies through interface
func TestCreateUserMakesUserRetrievable(t *testing.T) {
    user, err := CreateUser(CreateUserInput{Name: "Alice"})
    if err != nil {
        t.Fatal(err)
    }

    retrieved, err := GetUser(user.ID)
    if err != nil {
        t.Fatal(err)
    }

    if retrieved.Name != "Alice" {
        t.Fatalf("got %q", retrieved.Name)
    }
}
```
