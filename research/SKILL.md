---
name: research
description: Use when a question needs investigation against high-trust primary sources, current docs or API facts, or delegated reading captured as cited Markdown findings.
---

# Research

Investigate the question; do not fill gaps with plausible memory.

1. Define the question, scope, date or version boundary, and decisions the findings must support.
2. Prefer primary sources: official docs, source code, specifications, first-party APIs, and authoritative project records. Use secondary sources only for leads or context, and label that use.
3. Follow each important claim back to the source that owns it. Record the source link, relevant version or date, and the evidence supporting the claim.
4. Separate facts, inferences, assumptions, conflicts, and missing evidence. Distinguish current behavior from historical behavior.
5. Write one Markdown file in the repository's existing notes or research location. If no convention exists, choose a sensible scoped location and report the path.
6. Start with the answer, then findings and evidence, implications, open questions, and sources. Use `$simple-language` when the findings need clearer wording for their readers. Do not write production code while researching.

If background-agent support is available, delegate bounded reading and continue other work. Give the delegated task the same source, file, citation, and stop rules. Otherwise perform the research in the current task.

Use `$research` when the user explicitly requests research or when the task requires current, source-backed investigation. Do not use it for a quick stable fact or a code review that needs only local repository evidence.
