---
name: taste-review
description: Use on a completed Pull Request, git diff, or final implementation brief right before the final commit or merge.
---

# Taste Review (Post-Implementation Quality Gate)

Evaluate the holistic aesthetics and maintenance legibility of the finished work.

### The Filter
* **The "Midnight Wake-Up" Test:** Can an on-call engineer diagnose a failure in this file within 30 seconds using only the layout, naming conventions, and logging primitives?
* **Defensive Noise:** Strip out walls of apologetic comments or verbose names trying to compensate for clumsy layouts.

---

## OUTPUT FORMAT

### 1. Elegant Accents
*(Code layout, naming choices, or sections that are exceptionally clear and satisfying to read.)*

### 2. Awkward Friction
*(Where the code layout feels clumsy, variables are poorly named, or the cognitive load spikes.)*

### 3. Polish Diff
*(The final cosmetic edits to flatten, rename, or polish the code to make it beautiful.)*
