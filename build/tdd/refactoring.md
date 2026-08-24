# Refactor candidates

After a green test, look for:

- Duplication → shared function, type, object, or helper
- Long functions → smaller units (keep tests on the public interface)
- Shallow modules → combine or deepen
- Feature envy → move logic to where the data lives
- Primitive obsession → a type that owns the rule
- Existing code the new code shows as a problem
