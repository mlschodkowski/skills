# Interface design for testability

Good interfaces make correct use natural and incorrect assumptions hard.
Contracts should be readable from types, names, and return shapes —
testing then becomes ordinary.

1. **Accept dependencies; do not create them**

   ```python
   def process_order(order, payment_gateway):
      return payment_gateway.charge(order.total)

   # Hard to test: constructs PaymentGateway inside
   def process_order(order):
      gateway = PaymentGateway()
      return gateway.charge(order.total)
   ```

2. **Return results; do not hide the effect**

   ```go
   func CalculateDiscount(cart Cart) Discount

   // Harder to test: mutates the cart
   func ApplyDiscount(cart *Cart) {
      cart.Total -= discount
   }
   ```

   Preserve information callers need until there is a reason to hide it.
   Side effects that matter should be visible in the contract.

3. **Small surface.** Fewer methods, fewer tests. Fewer parameters,
   simpler setup. Every method and parameter should have a job.
