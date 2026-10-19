---
name: simple-language
description: Use when technical writing is unclear, dense, jargon-heavy, or must be rewritten for a specific reader while preserving the author's natural voice.
disable-model-invocation: true
---

# Simple Language

Make the reader's task and the relationships between ideas easy to understand.
Apply this skill to the requested text or explanation.

## Process

1. Identify the reader, their question, and the action or understanding they need.
   Ask only when missing context would change the meaning.
2. Extract the facts, decision, conditions, risks, and next action.
   Preserve the distinctions the reader needs to act correctly.
3. Arrange the content by importance and dependency.
   Lead with the answer, decision, or action. Put supporting evidence beside
   the claim it supports. Put prerequisites before dependent steps.
4. Give each paragraph one main idea. Use headings for distinct topics,
   numbered lists for sequences, and tables for comparisons.
   Let structure show how the parts relate.
5. Write short active sentences with concrete verbs and one term per concept.
   Use parallel wording for comparable items. State conditions and results.
6. Remove repetition, filler, vague claims, and formatting that adds no meaning.
   Keep explanations, examples, and qualifications that prevent misunderstanding.
7. Read from the intended reader's position. Check that they can find the
   main point, follow the reasoning, and identify the next action.

Prefer ASD-STE100 principles and aim for approximately CEFR B2 language when
the reader and subject permit. Treat both as guidance.

Preserve exact identifiers, commands, paths, API names, error text, quoted
text, and legal text. Preserve the author's natural voice and intended meaning.

Return only the requested artifact unless the user asks for an explanation.
Use `$simple-language` for explicit invocation.

This skill changes language and organization. Changes to code behavior need
their own task scope.
