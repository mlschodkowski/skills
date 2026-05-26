# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   ```python
   # Testable
   def process_order(order, payment_gateway):
      return payment_gateway.charge(order.total)

   # Hard to test
   def process_order(order):
      gateway = PaymentGateway()
      return gateway.charge(order.total)
   ```

2. **Return results, don't produce side effects**

   ```go
   // Testable
   func CalculateDiscount(cart Cart) Discount

   // Hard to test
   func ApplyDiscount(cart *Cart) {
      cart.Total -= discount
   }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup
