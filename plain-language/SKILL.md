---
name: plain-language
description: Simplify and humanize general prose. Use when rewriting non-technical articles, notes, emails, posts, personal writing, everyday explanations, or AI-sounding text so it is clear, natural, and easy to read. Do not use for code or engineering runbooks.
---

# Plain Language

Rewrite general text so it is easy to understand and sounds like a person wrote it. Keep the meaning, reduce effort for the reader, and remove AI-writing tells without making the result childish or generic.

Apply the mandatory [plain writing standard](../references/plain-writing.md). It takes priority over the style preferences below.

For the full AI-writing rule catalog with examples, read [ai-writing-patterns.md](references/ai-writing-patterns.md) when the text is long, high-stakes, or the first pass still sounds synthetic.

## Process

1. Identify the reader and purpose.
   - Who will read this?
   - What should they understand, feel, or do after reading?
   - Completion: the rewrite has a clear audience and job.

2. Keep the meaning.
   - Preserve facts, names, dates, claims, examples, and tone boundaries.
   - Do not add new claims.
   - Flag unclear or unsupported claims instead of smoothing them over.
   - Completion: the rewrite says the same thing with less effort from the reader.

3. Simplify the structure.
   - Put the main point early.
   - Split long sentences.
   - Use short paragraphs.
   - Remove repeated ideas.
   - Completion: a reader can scan the text and still get the point.

4. Simplify the language.
   - Use common, short words unless a specific term matters.
   - Prefer active voice; avoid familiar figures of speech.
   - Replace abstract nouns with concrete wording.
   - Keep a natural rhythm; not every sentence should be the same length.
   - Completion: the text sounds like a person explaining something clearly.

5. Remove AI polish.
   - Cut empty intensifiers and broad claims.
   - Remove chatbot artifacts: "Great question", "Certainly", "I hope this helps", "Let me know".
   - Avoid "crucial", "delve", "seamless", "robust", "pivotal", "tapestry", "testament", and "landscape".
   - Replace vague authority with specific attribution or remove it: "experts say", "industry observers", "reports suggest".
   - Avoid forced contrast like "not only... but also" and "not just... it is".
   - Break forced rule-of-three lists and false "from X to Y" ranges.
   - Avoid generic endings that summarize without adding anything.
   - Completion: the result is plain, natural, and not promotional.

6. Audit once.
   - Ask internally: "What still makes this obviously AI generated?"
   - Fix the remaining tells before answering.
   - Completion: remaining oddities are either removed or intentionally preserved because they belong to the writer's voice.

## Style Rules

- Keep the reading level around B2 unless the user asks otherwise.
- Keep the writer's voice when a sample or clear tone is present.
- Use warmth only when it fits the text.
- Do not turn everything into bullets.
- Do not make casual writing sound corporate.
- Do not make serious writing cute.
- Do not add personality that was not present in the source or requested by the user.

## Default Output

Return the rewritten text only, unless the user asks for notes.

When the source is unclear or risky, include a short note before the rewrite:

```text
Note: I kept the claim about X, but the source text does not explain why it is true.
```

## Boundary

Use `plain-tech-language` instead when the text is engineering-facing and depends on commands, logs, statuses, incidents, PR review, runbooks, ADRs, or operational decisions.
