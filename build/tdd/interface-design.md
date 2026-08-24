# Interface design for testability

Good interfaces make testing ordinary.

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

3. **Small surface.** Fewer methods, fewer tests. Fewer parameters,
   simpler setup.
