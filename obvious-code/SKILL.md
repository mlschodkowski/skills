---
name: obvious-code
description: Use when code or tests are difficult to read, debug, review, maintain, or trust because names, control flow, ownership, side effects, or abstractions force the reader to infer behavior.
---

# Obvious Code

Make the path obvious at 3 AM. Reduce inference. Preserve behavior.

## Workflow

1. **Map the contract.** Read callers, tests, data shapes, side effects, errors,
   and compatibility.
2. **Use one vocabulary.** Use one term for each concept. Rename unclear
   local and private symbols. Preserve external names.
3. **Expose behavior.** Show the subject, action, condition, effect, and result.
   Put conditions before commands. Prefer guard clauses and direct calls.
4. **Simplify a slice.** Keep one responsibility per function, method, and block.
   Do not split code only to reduce unit size.
5. **Verify.** Run focused tests first, then broader checks when shared code
   changes. Inspect contract output.
6. **Review at 3 AM.** Find the main path, failure path, state owner,
   observability, and tests quickly.

## Rules

- Reduce ambiguity, not characters.
- Obvious code is readable code. Judge it from the next reader's view: can
  another engineer follow, review, and safely change it without guessing?
- Prefer direct code over a helper that only renames or forwards.
- Keep an abstraction for a current rule, lifecycle, boundary, variation,
  side effect, or test seam.
- Preserve validation, authorization, observability, retries, transactions,
  domain logic, errors, and compatibility.
- Ask when valid designs differ in behavior, ownership, or a public
  boundary. Otherwise choose the smallest clear change.

## Tests

- Keep tests for public behavior, failures, compatibility, boundaries,
  invariants, and regressions.
- Remove tests that only prove mock calls or private steps. Keep
  mocks for real external boundaries and side effects.
- Add a test only for a distinct branch, boundary, invariant, failure mode,
  data shape, permission, or regression.

**REQUIRED SUB-SKILL:** Use `tdd` before behavior changes.

**REQUIRED SUB-SKILL:** Use `abstraction-audit` when creating, changing, or
proposing an abstraction.

**REQUIRED SUB-SKILL:** Use `ste` when changing comments, documentation, or
technical reports.

## Examples

### Code: expose control flow

Before:

```python
def handle(request):
    return process(request, True, False)
```

After:

```python
def create_order(request):
    validate_create_order(request)
    authorizer.require(request.user_id, "create_order")

    order = Order.from_request(request)
    orders.save(order)
    return order
```

It shows the action, conditions, effect, and result.

### Code: keep an abstraction only for a current boundary

When one concrete provider exists, prefer:

```python
def create_order(order, store: SqlOrderStore):
    return store.save(order)
```

Do not add a protocol and forwarding wrapper for imagined future providers.
Keep it for a real boundary or variation.

### Comment: explain a constraint

Avoid:

```python
# Check status before sending.
```

Prefer:

```python
# Do not retry after an unknown write result. The server can complete the first request.
```

It explains the risk, not the code.

### Documentation: state condition, action, and result

Avoid:

```text
The database is checked and the command can then be executed.
```

Prefer:

```text
If the database is reachable, run the backup command. The command creates one archive in `BACKUP_DIR`.
```

## Final report

Report simplifications, decisions, verification, and risk.
