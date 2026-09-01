# When to mock

Mock at system boundaries only — places where ownership, side effects,
or external lifecycle actually differ:

- External APIs
- Databases (prefer a real test database when practical)
- Time and randomness
- Filesystem, when the boundary requires it

Do not mock your own modules or internal collaborators. A mock inside
your design usually means the seam does not match reality.

## At the boundary

Pass the external dependency in rather than constructing it inside.
Prefer an explicit ordinary mechanism over indirection that adds no
capability:

```go
func ProcessPayment(order Order, client PaymentClient) error {
    return client.Charge(order.Total)
}
```

Prefer one function per external operation over a generic fetcher that
the mock has to branch on:

```javascript
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch('/orders', { method: 'POST', body: data }),
};
```

Each mock then returns one shape. The test shows which endpoints it
exercises.
