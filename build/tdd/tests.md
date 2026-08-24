# Tests

Test observable behavior through the public interface. The test should
survive an internal refactor.

```python
def test_user_can_checkout_with_valid_cart():
    cart = create_cart()
    cart.add(product)

    result = checkout(cart, payment_method)

    assert result.status == "confirmed"
```

A test that is about how, not what:

```javascript
test("checkout calls paymentService.process", async () => {
  const mockPayment = { process: vi.fn() };
  await checkout(cart, payment);
  expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

Avoid: mocking internal collaborators, testing private methods,
asserting on call counts or order, names that describe how, verifying
through a side channel instead of the interface.

```go
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

The weaker version would `SELECT` from the table to prove `CreateUser`
wrote a row. Prove it by reading the user back through the same
interface.
