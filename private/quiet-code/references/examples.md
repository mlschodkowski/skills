# Examples

### Go

Keep the invariant and the operation that protects it on the value that owns
the state.

```go
type Invoice struct {
    amountCents int64
    settled     bool
}

func (i Invoice) Settle(paymentCents int64) (Invoice, error) {
    if i.settled {
        return Invoice{}, ErrAlreadySettled
    }

    if paymentCents < i.amountCents {
        return Invoice{}, ErrUnderpaid
    }

    i.settled = true
    return i, nil
}
```

### Rust

Keep normalization and domain decisions explicit and free of effects when they
do not need I/O.

```rust
fn reserve(
    available: Capacity,
    raw_requested: u32,
) -> Result<Capacity, ReservationError> {
    let requested = Capacity::try_from(raw_requested)?;

    if requested > available {
        return Err(ReservationError::InsufficientCapacity);
    }

    Ok(available.subtract(requested))
}
```
