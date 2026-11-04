---
name: hemingway-style
description: Use when reviewing or improving any written content — marketing copy, technical docs, blog posts, specs, or AI-generated text. Identifies passive voice, adverbs, complex sentences, jargon, and AI slop. Provides rewrites.
---

Edit the supplied text for clarity, directness, and economy. Use Hemingway's principles. Give specific corrections.

For technical instructions, preserve commands, identifiers, requirement words,
conditions, and evidence limits. Keep uncertainty when the evidence requires it.
Apply simpler-word suggestions only when they preserve the technical meaning.

## Analysis Framework

Analyze across these dimensions:

### 1. Sentence Complexity

- Sentences over 25 words: "hard to read"
- Sentences over 40 words: "very hard to read"
- Count embedded clauses, suggest breaking them up

For each: quote original, explain why, provide rewrite.

### 2. Passive Voice Detection

Flag every instance:

- "was/were [verb]ed", "is being [verb]ed", "has been [verb]ed", "will be [verb]ed"

For each phrase, quote it and offer an active rewrite. Note when passive voice fits, such as an unknown actor or deliberate emphasis on the object.

### 3. Adverb Audit

Flag weakening adverbs:

- "very", "really", "extremely", "quite", "rather"
- Most "-ly" adverbs (quickly, slowly, carefully)
- "just", "actually", "basically", "literally"

For each: quote phrase, suggest stronger verb. "ran quickly" → "sprinted"

### 4. Simpler Alternatives

| Avoid        | Use Instead             |
| ------------ | ----------------------- |
| utilize      | use                     |
| implement    | do, start, run          |
| leverage     | use                     |
| facilitate   | help, enable            |
| optimize     | improve                 |
| prioritize   | focus on                |
| synergy      | teamwork                |
| paradigm     | model, pattern          |
| innovative   | new                     |
| disruptive   | (often delete)          |
| seamless     | smooth                  |
| robust       | strong                  |
| scalable     | (be specific)           |
| holistic     | complete, full          |
| impactful    | effective               |
| learnings    | lessons                 |
| deliverables | work, results           |
| stakeholders | people, team, customers |
| bandwidth    | time, capacity          |
| circle back  | follow up               |
| deep dive    | analysis, review        |

### 5. Weak Constructions

- **Hedge words**: "I think", "I believe", "perhaps", "maybe", "somewhat", "might"
- **Nominalizations**: Verbs turned into nouns ("make a decision" → "decide")
- **Empty phrases**: "in order to" → "to", "due to the fact that" → "because"
- **Throat-clearing**: First sentences that don't add value
- **Weasel words**: "some people say", "studies show" (without citation)

### 6. Readability Score

Calculate and report:

- **Word count**, **Sentence count**, **Avg sentence length**
- **Grade level** (Flesch-Kincaid approximation)
  - Target: Grade 6-8 general, 9-12 professional/technical, above 12 too complex

## Output Format

```
## Summary
[2-3 sentence overview]

**Readability Stats:**
- Words: [X] | Sentences: [X] | Avg length: [X] words
- Grade level: [X] (Target: [X])
- Passive voice: [X] | Adverbs: [X] | Complex sentences: [X]

---

## Issues Found
### Hard to Read Sentences
[Each with original, explanation, rewrite]

### Passive Voice
[Each with original and active rewrite]

### Adverbs to Reconsider
[Each with original and stronger alternative]

### Simpler Alternatives
[Word swaps]

### Other Improvements
[Hedge words, nominalizations, empty phrases]

---

## Revised Version
[Complete rewritten text]

---

## Key Takeaways
[3-5 bullets on most important improvements]
```

## Tone & Approach

Be direct. "This sentence is too long" not "This sentence might be considered somewhat lengthy." Quote specific text. Acknowledge when something works well.

## Modes

### Standard Modes

**"Quick review"**: Summary + Revised Version only.

**"Just stats"**: Readability statistics only.

**"Focus on [X]"**: Single dimension (e.g., "Focus on passive voice").

**"Make it shorter"**: Standard analysis + aggressive cuts that maintain meaning.

### Product Marketing

**Trigger:** "product marketing" or "marketing copy"

In addition to full analysis, apply these layers:

**Specificity audit:**

- Flag every claim without a number, metric, or concrete proof point
- "Faster performance" → How much faster? Cite a benchmark
- "Trusted by thousands" → Cite exact count or name logos
- "Enterprise-grade" → What specifically makes it enterprise-grade?

**Value prop clarity:**

- Can a reader state what the product does in one sentence after reading? If not, flag
- Is the primary benefit above the fold / in the first paragraph? If buried, flag
- Does the copy address _who_ it's for? Generic = weak

**Buzzword escalation (stricter than standard jargon table):**

| Kill            | Why                                              |
| --------------- | ------------------------------------------------ |
| seamless        | Nobody believes this. Say what's smooth and how  |
| end-to-end      | Specify start and end                            |
| best-in-class   | Compared to whom? Cite evidence or delete        |
| cutting-edge    | Just describe the technology                     |
| next-generation | Say what changed from previous generation        |
| AI-powered      | Say what the AI does specifically                |
| empower         | Use "help", "enable", or describe the capability |
| transform       | Describe the before and after concretely         |
| unlock          | Say what becomes possible                        |
| supercharge     | Describe the improvement with numbers            |

**CTA audit:**

- Is there one clear call-to-action? Multiple CTAs dilute
- Does the CTA match the reader's stage? (awareness → "Learn more", decision → "Start free trial")
- Flag generic CTAs: "Click here", "Learn more" without context

**Social proof check:**

- Are proof points near claims they support?
- Testimonials without name/title/company → flag as weak
- Logos without context → suggest adding "Used by X at [Company] for [use case]"

### Technical Specification

**Trigger:** "technical spec" or "spec review"

In addition to full analysis, apply these layers:

**Precision audit:**

- Flag ambiguous quantifiers: "fast", "lightweight", "scalable", "efficient" → demand numbers
- Flag undefined terms on first use. Every acronym gets expanded once
- Flag "should" vs "must" vs "may" inconsistency — pick one convention (RFC 2119) and enforce it

**Completeness check:**

- Are inputs, outputs, and error states defined for every operation?
- Are edge cases addressed or explicitly marked as out of scope?
- Are constraints and limitations stated, not just capabilities?

**Structure enforcement:**

- Does every section answer: What? Why? How? What if it fails?
- Are requirements traceable — can each be verified independently?
- Flag narrative paragraphs that should be tables, lists, or diagrams

**Passive voice exception:** In specs, passive voice is acceptable when the actor is the system and emphasis belongs on the action or object. "The request is validated against the schema" is fine. "Mistakes were made" is not.

### Technical Blog

**Trigger:** "technical blog" or "tech blog"

In addition to full analysis, apply these layers:

**Hook audit:**

- Does the opening sentence create urgency, curiosity, or recognition?
- Flag openings that start with definitions ("X is a..."). Start with the problem or a surprising fact
- First 50 words must answer: "Why should I keep reading?"

**Code-prose ratio:**

- Flag code blocks without preceding explanation of _why_ (not just what)
- Flag explanations without code when a 5-line example would be clearer
- Code comments should explain _why_, prose should explain _what_ and _when_

**Depth vs breadth check:**

- Flag sections that skim a topic without going deep enough to be actionable
- "You can configure X" → Show the config. Show what happens if you don't
- Every technical claim should be verifiable — link to docs, show output, cite a benchmark

**Structure check:**

- Does the post follow: Problem → Why it matters → Solution → Proof → Takeaway?
- Flag posts that dump information without a narrative arc
- Cross-links: does the post connect to related concepts? Isolated posts lose readers

**Audience calibration:**

- Flag unexplained jargon that the target audience wouldn't know
- Flag over-explanation of concepts the audience already knows
- Grade level target: 9-12 (technical but not academic)

### SEO Blog

**Trigger:** "seo blog" or "seo content"

In addition to full analysis, apply these layers:

**Search intent alignment:**

- What query would someone type to find this? State it explicitly
- Does the post _answer_ that query in the first 100 words?
- Flag posts that bury the answer — Google rewards direct answers

**Title and heading audit:**

- H1: Contains primary keyword naturally? Under 60 chars?
- H2s: Do they map to sub-queries a searcher would have?
- Flag heading-stuffed keywords — headings must read naturally
- Flag clickbait that doesn't deliver

**Content structure for SERP:**

- Is there a featured-snippet-worthy paragraph? (Direct answer in 40-60 words)
- Are there lists, tables, or structured data that could earn rich results?
- Flag walls of text without subheadings — aim for heading every 200-300 words

**Keyword integration:**

- Primary keyword in: title, first paragraph, one H2, meta description?
- Flag forced keyword insertion that breaks natural reading
- Flag keyword absence in critical positions
- Semantic variations: are related terms used naturally throughout?

**Internal linking:**

- Flag posts with zero internal links. Every post should link to 2-3 related pages
- Flag orphan content — is this post linked FROM other pages?

**Meta check:**

- Meta description: compelling, under 160 chars, contains keyword?
- Does the description match the content? Misleading meta = high bounce rate

**E-E-A-T signals:**

- Experience: Does the author demonstrate first-hand experience?
- Expertise: Are claims backed by data, code, or citations?
- Authority: Author bio, credentials, or track record mentioned?
- Trust: Are sources cited? Any unsubstantiated claims?

### De-slop AI Text

**Trigger:** "de-slop", "deslop", "ai cleanup", or "remove ai slop"

AI-generated text has distinctive failure patterns. This mode targets them specifically.

**Slop markers — flag and kill every instance:**

| Pattern                   | Example                                                                            | Fix                                                            |
| ------------------------- | ---------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Enthusiasm padding        | "Great question!", "Absolutely!", "That's a fantastic point!"                      | Delete entirely                                                |
| Filler transitions        | "Now, let's dive into...", "Let's explore...", "Let's take a closer look at..."    | Cut or replace with direct statement                           |
| Sycophantic hedging       | "This is a really great start, but...", "You've done an excellent job, however..." | State the issue directly                                       |
| False certainty           | "This will definitely...", "This ensures that..."                                  | Qualify appropriately or cite evidence                         |
| Meaning-free intensifiers | "truly", "incredibly", "remarkably", "significantly"                               | Delete or replace with specific measure                        |
| Cliche metaphors          | "game-changer", "deep dive", "level up", "at the end of the day"                   | Rewrite with concrete language                                 |
| Summary repetition        | Restating what was just said in slightly different words                           | Delete the repetition                                          |
| Emoji seasoning           | Random emoji that add no meaning                                                   | Delete                                                         |
| List-itis                 | Converting everything to bullet points when prose flows better                     | Rewrite as prose where appropriate                             |
| Fake structure            | "In this article, we will..." / "In conclusion..."                                 | Delete throat-clearing; if the conclusion adds nothing, cut it |
| Hollow acknowledgment     | "That's an interesting approach"                                                   | Delete or engage with the specifics                            |
| Thesaurus syndrome        | Using 3 synonyms where 1 word works ("efficient, effective, and streamlined")      | Pick the best one                                              |
| Corporate passive         | "It should be noted that...", "It is important to..."                              | Say who notes it and why, or delete                            |

**Tone normalization:**

- AI text tends toward relentless positivity. Flag sentences that are positive without justification
- AI text avoids strong opinions. If the content _should_ take a stance, flag wishy-washy both-sidesing
- AI text over-qualifies. "In many cases, this can potentially help to..." → "This helps..."

**Structure de-slop:**

- Flag unnecessary introductions that restate the title
- Flag conclusions that only summarize without adding insight
- Flag sections that exist for "completeness" but add no value to the reader
- Flag bullet-point lists that would read better as 2-3 sentences

**Voice consistency:**

- Compare the text's voice against the surrounding content (if available)
- Flag tonal shifts that suggest AI-written sections were inserted into human-written text
- If the user has a style guide or prior writing samples, match to that voice

## Example

**Input**: "The decision was made by the committee to utilize a more robust framework that would facilitate better outcomes for all stakeholders involved in the process."

**Output**:

```
## Summary

Bloated with passive voice and corporate jargon. 26 words that say what 5 could.

**Readability Stats:**
- Words: 26 | Sentences: 1 | Avg length: 26 words
- Grade level: 14 (Target: 8)
- Passive voice: 1 | Adverbs: 0 | Complex sentences: 1

---

## Issues Found

### Hard to Read Sentences

**Original**: "The decision was made by the committee to utilize a more robust framework that would facilitate better outcomes for all stakeholders involved in the process."

**Problems**: Passive voice ("was made by"), "utilize" → "use", "robust" is vague, "facilitate better outcomes" is meaningless, "stakeholders involved in the process" is padding.

**Rewrite**: "The committee chose a stronger framework."

### Passive Voice

"The decision was made by the committee" → "The committee decided"

### Simpler Alternatives

| Original | Replacement |
|----------|-------------|
| utilize | use |
| robust | strong (or be specific) |
| facilitate | help |
| stakeholders | people (be specific: customers, team) |

---

## Revised Version

The committee chose a stronger framework.

---

## Key Takeaways

- Lead with who did what (active voice)
- "Utilize" always means "use"
- Delete phrases that add no meaning ("involved in the process")
- If you can't define "robust" or "stakeholders" specifically, cut them
```

## Remember

Cut words that add no meaning. Split long sentences when this improves clarity. Name the actor when passive voice hides responsibility.
