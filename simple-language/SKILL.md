---
name: simple-language
description: Use when general prose or technical writing is unclear, dense, jargon-heavy, AI-sounding, or hard to act on. Use for articles, emails, explanations, PRs, runbooks, incident notes, plans, and handoffs while preserving meaning, exact technical terms, and natural voice.
---

# Simple Language

Minimize cognitive load; change wording, not facts, code, or decisions.

1. Establish context.
   - Classify the source as general prose or technical text.
   - Identify reader, purpose, and action; ask only if missing context changes meaning.
   - For technical text, default to an on-call engineer acting safely.

2. Preserve meaning.
   - Keep facts, names, dates, examples, tone, and uncertainty; distinguish claims from facts.
   - Do not add claims or decisions, repair unclear evidence, or turn vague claims into concrete ones. Flag uncertainty that affects a decision, safety, or credibility; otherwise remove the flourish.
   - Preserve exact commands, paths, API names and fields, class names, statuses, errors, and quoted or legal text.

3. Simplify the language and structure.
   - Optimize for one-pass understanding, not word count. Do not mirror the source's order or sentence count.
   - Give each sentence one job. Keep context and connective words when removing them would make the reader infer a relationship, condition, cause, or uncertainty.
   - Delete repeated facts, commands, rationale, and context that adds no understanding, action, safety, or trust. Do not explain a command twice.
   - Shorter is not better if it makes the text denser or more ambiguous.
   - For technical prose, extract the spine before rewriting: what happened, evidence or reason, impact or risk, and next action. Remove status theatre, marketing tone, vague importance claims, and filler.
   - State the status, risk or uncertainty, and next action early. Use bullets, labels, or a short sequence when they scan faster than paragraphs.
   - Split sentences that combine status, cause, condition, and action. Name the subject instead of using ambiguous pronouns.
   - Use short active sentences, common words, familiar syntax, concrete nouns and verbs, and one term per concept.
   - Brevity: state the main points in short, crisp paragraphs; cut padding and indirect phrases; move supporting detail to an appendix or reference when it is not needed to act.
   - Target CEFR B2 or simpler for English. For other languages, use the equivalent plain-language level: clear to an educated non-specialist, not childish, slangy, or overly formal.
   - In technical prose, prefer "because" and "fails when" over abstract alternatives.
   - Keep natural rhythm and voice; do not make casual writing corporate, serious writing cute, or technical writing promotional. Do not force one shape.

4. For technical artifacts, make reasoning and action visible.
   - Use: "We check X because Y. If X says Z, do A."
   - Show reasoning when it helps the reader trust the action; do not over-explain obvious steps.
   - Runbook: when it matters, check, good signal, bad signal, next action.
   - Incident note: event, evidence, impact, current state or uncertainty, next action.
   - PR body: change, reason, tests, review notes.
   - Plan: current state, intended change, guardrails, test plan, acceptance criteria.

5. Use the AI-pattern reference.
   - Read [ai-writing-patterns.md](references/ai-writing-patterns.md) when prose sounds polished, generic, promotional, or machine-made. Use its scan and editing pass without flattening the writer's voice.

6. Remove synthetic polish.
   - Cut chatbot artifacts: "Great question", "Certainly", "I hope this helps", and "Let me know".
   - Replace broad claims, vague authority, and decorative praise with evidence or remove them. Do not paraphrase vague benefits.
   - Prefer "is", "has", and "uses" over inflated alternatives such as "serves as", "boasts", and "stands as".

7. Audit for cognitive load.
   - Apply the 03:00 test: would a freshly woken on-call engineer find the status, risk, and next action in one pass and about 10 seconds, without reconstructing the logic? If not, simplify the structure or add missing context.
   - Delete once more: if removing a phrase does not lose a fact, safety condition, decision, next action, or useful connection, remove it. If two sentences do the same job, combine them.
   - Do not delete a phrase solely to reduce length if it makes a relationship, condition, or uncertainty harder to follow.
   - Does every technical sentence explain what happened, why, what to check, or what to do?
   - Are exact terms unchanged and uncertainty honest?

Return only the requested artifact unless asked for an explanation. Use `$simple-language` when explicitly invoked.

Do not use this skill to change code logic or to flatten a creative or personal voice.
