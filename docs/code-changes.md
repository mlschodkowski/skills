# Code changes

## Before editing

- Read the files, callers, tests, config, and history that the change touches. For shared code, also trace ownership, side effects, and external contracts. A small change does not need a full repository map.

## Size

- Write the minimum code that solves the request. Build only the requested features. Add an abstraction only when a second caller exists. Add configuration only when asked. Handle only failures that can actually happen.
- Add a dependency, config option, file, or doc only when this task needs it. Tests are part of the task; see [testing](testing.md).
- Keep unrelated behaviour, compatibility, and existing seams unchanged.

## Scope

- Leave adjacent code, comments, and formatting as they are. Mention unrelated dead code in your report instead of deleting it.
- Remove imports, variables, and functions that your change made unused. Keep pre-existing dead code unless asked.

## Shortcuts

Mark a deliberate shortcut with a `ponytail:` comment. Name the ceiling and the upgrade trigger:

```
// ponytail: O(n²) scan, index by id when lists pass 10k items
```

`/ponytail-debt` collects these markers.
