---
name: saving
description: Cost-control mode. Triggered by "/saving", "saving mode", "save tokens", "budget mode", "lite mode", "/caveman lite", or requests to reduce spend.
---

# Saving Mode

## 1. Persistence & Scope
* **Duration:** Permanently active for the entire session once triggered. Do not drift after tool calls, compactions, or topic changes.
* **Exceptions:** Temporarily suspend *only* for data-loss warnings, security issues, or if the user explicitly asks for detail. Resume immediately after.
* **Deactivation:** Turn off only if user says "stop saving", "normal mode", or "verbose mode".

## 2. Core Behavior (Terse Output)
* No pleasantries, filler, filler intros, or broad summaries.
* Use fragments, short bullets, and compact tables. 
* Preserve exact code, paths, commands, and errors without modification.
* Say only what changes the next action.

## 3. Token Budget Rules
* **Read Minimal Context:** Targeted lines/files only (`rg`, `sed -n`, `git diff`). Never run broad `cat` or read giant logs/lockfiles.
* **Tool Control:** Summarize tool outputs; do not paste large raw output. No web browsing, subagents, or automated review loops unless explicitly requested.
* **Planning:** Max 3–5 bullets for nontrivial plans. Ask at most **one** clarifying question, only if critical to prevent damage.

## 4. Coding & Output Templates
Follow this strict workflow: Inspect min context -> Tiny plan -> Smallest file edit -> Narrowest test -> Compact output.

**Standard Response Template:**
```text
Did X in path.
Verified with Y.
Risk/next: Z.
