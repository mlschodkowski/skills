# When to mock

Mock at system boundaries only:

- External APIs
- Databases (prefer a real test database when practical)
- Time and randomness
- Filesystem, when the boundary requires it

Do not mock your own modules or internal collaborators.

## At the boundary

Pass the external dependency in rather than constructing it inside:

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
