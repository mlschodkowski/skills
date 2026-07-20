---
name: brag
description: Interactively capture accomplishments, log wins, track impact, or normalize older entries into your Obsidian brag document. Use for weekly reviews, performance review prep, or when migrating old brag notes.
---

Interactively manage my Obsidian brag document. Assume the default vault. For obisidian manipulation use `obsidian-cli`, `obsidian-bases` and `obsidian-markdown` skills.

Apply the [plain writing standard](../references/plain-writing.md). Keep metrics, scope, and impact specific; do not add promotional language.

Follow this workflow:
1. **Gather Wins (Conversational):** Ask me simple, open-ended questions one at a time about my recent work. If I want to *rewrite/migrate* an old note instead, read it first while preserving its original meaning and metrics.
2. **Draft the Entry:** Organize the content into a simple, scannable format: a single `# Notes` header followed by 3–5 concise, single-line bullets outlining what, how, and the why/impact (prefer short phrases separated by commas).
3. **Handle Tags & Links:** Search the vault for relevant files to propose as `[[links]]`. Add the `#brag` tag, and ask me if I want to add any other specific tags.
4. **Save to Obsidian:** Save or update the file under the `Brag/` directory using the naming convention `YYYY-MM-DD <Title>.md`. Show me a quick summary of what was saved.

Example of expected file content:

```md
## Notes

- Built Enkode RAG PoC: FastAPI + pgvector ingestion, hybrid vector+text search, 0.942 faithfulness
- Hardened service: added health checks, Prometheus metrics, auth, and REST/MCP interfaces
- Result: production-ready prototype and repeatable benchmark loop for RAG quality
```
