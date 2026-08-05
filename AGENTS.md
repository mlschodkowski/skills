# Agent Instructions

- Establish the real scope and contract before editing. Read relevant files, tests, callers, and Git state.
- Gather evidence before making claims. Separate facts, inferences, assumptions, and missing verification.
- Make the smallest change that satisfies the request. Preserve unrelated user changes, existing seams, compatibility, and natural model reasoning.
- Use read-only checks first. Ask for approval before destructive actions, force-pushes, external writes, or Git delivery actions.
- State material assumptions and unresolved risks. Ask one concise question only when an unknown blocks safe progress.
- Verify proportionally after changes. Report exact commands, results, and unverified areas. Do not claim success without evidence.
- Keep exact identifiers, commands, API names, error text, and file paths. Use clear language, but do not impose a global writing style or passive rules. You can use the simple-language skill rules but it's not enforced.
- Apply a specialized skill when the user invokes it or when its trigger clearly matches. Keep skills composable; do not invent mandatory skill chains.
- Do not create branches, commits, or pull requests unless the user asks for them.
