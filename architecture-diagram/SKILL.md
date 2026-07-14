---
name: architecture-diagram
description: Map a codebase architecture into Excalidraw by exploring module-by-module, tracing dependencies and runtime flows, and producing one or multiple .excalidraw files. Use when the user wants architecture reverse-engineering, module/link flow diagrams, or code-driven system maps.
---

# Architecture Diagram

Turn source code into architecture diagrams with an evidence-first pass. Default to multiple files for readability.

## Workflow

1. **Frame scope and level.**
   - Confirm repository root and target slice (entire system or selected package/service).
   - Default diagram depth: Context + Containers + key module flows.
   - If goals are ambiguous, invoke `brainstorming` before diagram work.
   - Completion: target scope and depth are explicit.

2. **Inventory modules and boundaries.**
   - Discover modules one-by-one from folders, package manifests, and entrypoints.
   - For each module, capture:
     - Public entrypoints/interfaces
     - Internal submodules
     - Owned data stores/state
     - Inbound dependencies (who calls/imports it)
     - Outbound dependencies (what it calls/imports)
   - Completion: every in-scope module has a filled evidence record.

3. **Trace links and flows.**
   - Build two distinct flow sets:
     - **Static structure**: imports, package dependencies, ownership boundaries.
     - **Runtime/control/data flows**: request path, async jobs, events, persistence, external APIs.
   - Mark uncertain edges as `unknown` and keep them visible instead of guessing.
   - Completion: every module has inbound/outbound links and at least one validated flow path.

4. **Choose output partitioning.**
   - Default output: separate Excalidraw files:
     - `01-system-context.excalidraw`
     - `02-container-view.excalidraw`
     - `03-module-dependencies.excalidraw`
     - `04-key-runtime-flows.excalidraw`
   - If the system is small, merge into one file.
   - If user explicitly asks, create one file with clearly separated sections using `--- <section name> ---` labels.
   - Completion: output plan fits complexity without unreadable density.

5. **Generate Excalidraw JSON (standalone).**
   - Produce valid `.excalidraw` JSON directly.
   - Minimum shape:
     ```json
     {
       "type": "excalidraw",
       "version": 2,
       "source": "https://excalidraw.com",
       "elements": [],
       "appState": { "viewBackgroundColor": "#ffffff" },
       "files": {}
     }
     ```
   - Use unique IDs for all elements.
   - Use `fontFamily: 5` for text elements.
   - Keep arrows directional and labeled for non-obvious relationships.
   - Completion: each output file opens in Excalidraw with readable layout and no broken structure.

6. **Run coverage gate before finalizing.**
   - Do not finalize until all in-scope modules are accounted for and mapped.
   - Verify each module appears in at least one structural diagram and one flow narrative (directly or by grouped boundary with explicit legend).
   - Completion: no missing module, no unlabeled critical edge, no implied-but-undrawn major flow.

7. **Deliver diagrams with short evidence summary.**
   - Return file list and a concise mapping summary:
     - module count
     - edge count
     - key runtime flows captured
     - unresolved unknowns
   - If the user wants pressure testing, invoke `grill-me` after delivery.
   - Completion: user can open diagrams immediately and understand what is covered vs unknown.

## Rules

- Prefer multiple diagrams over one dense canvas.
- Never invent dependencies or flows not supported by repository evidence.
- Keep architecture level stable; do not mix low-level function detail into high-level views unless requested.
- Separate control flow and data flow when combining them would reduce readability.
