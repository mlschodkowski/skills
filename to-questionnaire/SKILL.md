---
name: to-questionnaire
description: Use when the user cannot answer a decision alone and needs to collect missing facts or decisions from a specific person.
disable-model-invocation: true
---

# To Questionnaire

Use only when the user invokes `$to-questionnaire`. Ask about the send, not the subject.

1. Ask who will receive it, their role, expertise, and relationship to the user. This sets the context and tone.
2. Ask what facts or decisions the user needs back. Convert the answer into a concrete list.
3. Write `to-questionnaire-<slug>.md` in the current directory and report its path.

Use this structure:

```markdown
# Questionnaire title

**Purpose:** Decision or action this supports.

**From:** User — **To:** Recipient — **How answers will be used:** Destination.

## Context

One short paragraph with the needed background.

## How to answer

Deadline, effort, and permission to mark uncertainty.

## Important topic

### One question

_Why this matters: explain only when the question could be misunderstood._

>

## Anything else?
```

Order questions by importance. Keep one idea per question. Cover every fact or decision named in step 2.
