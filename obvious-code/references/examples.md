# Obvious Code Examples

Use these examples when the pattern is unfamiliar. The examples use Go because
small, explicit control flow is easy to inspect. Apply the same judgment in C,
Go, or an object-oriented language.

These are patterns, not defaults. First fit the surrounding codebase; choose
the procedural or object form that makes its existing boundaries clear.

## Code: prefer a direct procedural path

```go
func writeRecords(w io.Writer, records []Record) error {
    for _, record := range records {
        if err := record.Validate(); err != nil {
            return err
        }
        if _, err := fmt.Fprintln(w, record); err != nil {
            return err
        }
    }
    return nil
}
```

The loop shows the validation, write, error path, and result. A helper or
custom interface is not needed when this is the only flow.

## Code: use an object for owned state

```go
type Queue struct {
    items []Item
    limit int
}

func (q *Queue) Push(item Item) error {
    if len(q.items) >= q.limit {
        return ErrFull
    }
    q.items = append(q.items, item)
    return nil
}
```

`Queue` owns its capacity invariant. An object is clearer here because callers
should not duplicate the check or modify the queue state directly.

## Comment: explain a constraint

Avoid:

```python
# Check status before sending.
```

Prefer:

```python
# Do not retry after an unknown write result. The server can complete the first request.
```

The comment explains the risk, not the code.

## Documentation: state condition, action, and result

Avoid:

```text
The database is checked and the command can then be executed.
```

Prefer:

```text
If the database is reachable, run the backup command. The command creates one archive in `BACKUP_DIR`.
```
