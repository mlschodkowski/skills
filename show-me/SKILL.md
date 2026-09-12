---
name: show-me
description: Use when a visual explanation, diagram, code-shape sketch, or focused HTML artifact will materially clarify the user's question.
---

# Show me

Use the smallest visual that makes the important relationship obvious. Keep
the prose beside it short, and preserve exact names, paths, states, and
boundaries from the code or source.

Choose the view by the question:

- Pseudocode for an algorithm or decision.
- A call tree for runtime control flow.
- A component or file tree for ownership and structure.
- Mermaid for a graph, dependency, data-flow, or sequence relationship.
- A focused HTML file only when layout, state, or a dense comparison is easier
  to inspect than in a text diagram.

Example call tree:

    submitForm
      createSession
        persistPrompt
        launchAgent
      navigateToSession

Use a diff-shaped sketch when the question is what changed. Show the whole
block only when omitted context would hide ownership, order, or state.

For HTML, write one self-contained artifact in the OS temporary directory,
using real labels and data relevant to the question. Open it when the
environment supports that action and report the absolute path. Do not add
visual treatment, interaction, or responsive structure that the question does
not need.

Do not combine views merely to make the answer look complete. Stop when the
visual answers the question; offer another view only when it resolves a
different ambiguity.
