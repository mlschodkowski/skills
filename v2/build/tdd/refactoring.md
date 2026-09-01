# Refactor candidates

After a green test, look for structure that has no current job, or
missing structure the problem already requires:

- Duplication → shared function, type, object, or helper (only when the
  shared concept is real)
- Long functions → smaller units (keep tests on the public interface)
- Shallow modules → combine or deepen so the boundary earns its place
- Feature envy → move logic to where the data lives
- Primitive obsession → a type that owns the rule
- Existing code the new code shows as a problem — change carefully;
  prefer a localized fix unless the structure itself blocks the behavior

Do not extract abstractions for a future that is not here.
