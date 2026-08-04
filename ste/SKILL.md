---
name: ste
description: Use when writing, rewriting, reviewing, or simplifying technical text such as documentation, comments, descriptions, PRs, runbooks, ADRs, plans, incident notes, commit messages, or technical explanations; write the result in ASD-STE100 Simplified Technical English (STE).
---

# ASD-STE100 Simplified Technical English (STE)

Use `/ste` as the short command for this skill.

Write all reader-facing technical prose in ASD-STE100 Simplified Technical English. This includes documentation, comments, descriptions, issue text, PR descriptions, commit bodies, runbooks, ADRs, plans, incident notes, summaries, and explanations.

Do not rewrite literal code, commands, file paths, identifiers, API names, status names, log messages, error text, quoted source, or legal text unless the user asks for that change. Apply STE to the surrounding explanation.

This skill is a practical writing guide. The [official ASD-STE100 overview](https://www.asd-ste100.org/about_STE.html) and the [official Issue 9 standard](https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf) are the authority. This skill does not prove formal STE compliance or certification.

## Workflow

1. Identify the reader, artifact, purpose, and required action.
2. Extract facts, decisions, limits, evidence, risks, and exact technical terms.
3. Put the main point and first useful action early.
4. Rewrite the prose with the rules below. Keep one term for one concept.
5. Check meaning, technical tokens, safety, and unsupported claims.
6. Return only the requested artifact unless the user asks for an explanation.

Ask one short question only when an unknown audience, action, or safety condition can change the meaning. Otherwise make the smallest safe assumption and state it in STE when needed.

## Core STE Rules

Use these rules as a practical Issue 9 check:

- Prefer the approved STE dictionary and one meaning for each word. If an exact word is unknown, use a clear approved alternative or reframe the sentence. Do not claim that a word is approved without checking the official dictionary.
- Use active voice. Use passive voice only for a descriptive statement when the agent is unknown or not important.
- Use direct verbs. Avoid nominalizations, phrasal verbs, idioms, metaphors, and vague verbs such as “handle” when a more exact verb exists.
- Use simple verb forms: infinitive, imperative, simple present, simple past, simple future, and past participle as an adjective. Avoid complex auxiliary forms.
- Use `-ing` only for a technical noun or a technical noun modifier. Reframe other uses when practical.
- Use short, clear sentences. Use articles and demonstratives. Keep noun groups short unless the full technical term is established.
- Use consistent terms. Do not replace a precise technical term with a casual synonym.
- Use American spelling and punctuation unless the project convention, exact quote, or code requires another form.
- Do not use contractions. Do not hide the subject, action, condition, or result.
- Reframe a sentence when a word-for-word replacement would change the meaning or make the sentence unnatural.

## Procedures and Descriptions

For a procedure:

- Use the imperative form.
- Put the condition before the command.
- Give one instruction per sentence.
- Keep each instruction to 20 words or fewer when practical.
- Use a numbered list for ordered actions.
- Use a note only for information. Do not put an instruction in a note.

For a description:

- State one topic per sentence.
- Keep each sentence to 25 words or fewer when practical.
- Keep one topic per paragraph and no more than six sentences per paragraph when practical.
- Do not use imperative language in a description.
- Present information in a gradual order: object, action, condition, result.

For a warning or caution:

1. Label the risk with the project format, such as `WARNING` or `CAUTION`.
2. State the condition or unsafe action.
3. State the command or safe action.
4. State the possible result when it helps the reader act safely.

## Artifact Rules

For documentation, comments, plans, ADRs, and explanations, state the fact, reason, action, or result that the reader needs. Remove filler, marketing language, vague authority, and unsupported certainty.

For a PR description or commit body, use short sections when useful:

```markdown
What changed: ...
Why: ...
Tests: ...
```

Keep commands, paths, identifiers, errors, and test names exact. Use active voice around them. State missing verification as “I did not verify ...” instead of hiding the gap.

## Examples

Read [writing-rules.md](references/writing-rules.md) for before-and-after examples. Use the examples to recognize sentence patterns, not as a replacement for the official STE dictionary or standard. Check exact word approval when strict compliance matters.

## Final Check

Before returning the text, check:

- Is the first point or action easy to find?
- Does each sentence have a clear subject and action?
- Are the words, terms, and verb forms simple and consistent?
- Are procedures imperative and descriptions non-imperative?
- Are exact technical tokens unchanged?
- Did the rewrite preserve every fact and avoid invented claims?
- Would a reader know what to do or understand the result without rereading?
