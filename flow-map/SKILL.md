---
name: flow-map
description: Use at the start of a session or phase transition to display the complete agentic engineering gauntlet and provide an exact user-system conversation blueprint.
---

# Engineering Workflow Guide

Print the 13-step engineering workflow. State that it should help people think clearly and avoid needless process.

Apply the [plain writing standard](../references/plain-writing.md) to any text around the fixed map below. Do not alter the map itself.

Display the following map exactly:
```
Brainstorm ───────────> [Command: "Let's brainstorm X"]

Grill Me ─────────────> [Command: "Grill me on this idea"]

Draft Plan ───────────> [Command: "Create the implementation plan from our grill session"]

TDD Strategy ─────────> [Command: "Incorporate TDD into the plan"]

Distill (Plan) ───────> [Command: "Distill the plan"]

Slice Vertically ─────> [Command: "Slice this vertically"]

Stress Test ──────────> [Command: "Run stress test"]

Hyperplan ────────────> [Command: "Execute hyperplan"]

Oracle ───────────────> [Command: "Call the oracle"]

Implement (Red/Green) > [Command: "Start TDD loops"]

Distill (Code) ──────> [Command: "Distill the green code"]

Taste Review ────────> [Command: "Run taste review"]

Git Commit ──────────> [Command: "/commit"]
```

DO NOT DISPLAY THE BELOW, THIS IS FOR DEVELOPER EYES ONLY

```
## The Execution Manual

### Phase 1: Expansion & Discovery
* **1. Brainstorm:** Natural, collaborative dialogue to map out the raw feature request, user intent, and high-level requirements.
* **2. Grill Me:** Relentless, high-friction interrogation. The system cross-examines the proposed ideas to unearth hidden edge cases, challenge assumptions, and solidify decisions before a plan exists.

### Phase 2: Structuring & Contract Design
* **3. Draft Plan:** Formulate a concrete architectural blueprint derived entirely from the outcomes of the grilling session.
* **4. TDD Strategy:** Invoke `tdd` (Phase 1). Define explicit public signatures and a checklist of observable behavioral tests, baking them directly into the drafted plan.
* **5. Distill (Plan):** Invoke `distill` on the fully populated plan to evaporate speculative infrastructure, indirection, and future-proofing before execution begins.

### Phase 3: Structural Verification (Critique)
* **6. Slice Vertically:** Invoke `slice-it-vertically` to extract the thinnest end-to-end tracer bullet path from the plan.
* **7. Stress Test:** Invoke `stress-test-plan`. Audit the plan's interfaces for hidden leakages, blast radius, and state fragility.
* **8. Hyperplan:** Invoke `hyperplan` to unleash parallel hostile subagents to locate execution and deployment blind spots.
* **9. Oracle:** Invoke `oracle` to secure a high-reasoning `YES | OK | NO_FIX` final blueprint sign-off.

### Phase 4: Construction & Refinement (Execution Loop)
* **10. Implement (Red -> Green):** Cycle the active `tdd` coding loop. Write *one* behavior test from the plan's checklist $\rightarrow$ watch it fail $\rightarrow$ write minimal code to pass.
* **11. Distill (Code):** **Immediate In-Flight Gate.** The second a test turns green, run `distill` on the raw code syntax to strip boilerplate, inline logic, and flatten nested statements using rules in `skills/programming/principles.md`. Tick off the checklist item. Repeat steps 10 and 11 until all behaviors pass.
* **12. Taste Review:** Invoke `taste-review` to polish formatting, ergonomics, naming, and telemetry logging primitives.
* **13. Git Commit:** Trigger `git-commit` (`/commit`) to stage changes logically and generate a conventional commit message.

---

## EXAMPLE USER-SYSTEM CONVERSATION

**User:** Let's brainstorm a simple local in-memory event emitter service for our app.

**System:** *(Invokes brainstorming)* Let's look at the context. We have a lightweight event loop. We could build an array-backed lookup or a map-backed broker. Let's unpack the core goals.

**User:** Grill me on this idea.

**System:** *(Invokes grill-me)* Interrogating the concept. Answer these one-by-one:
1. Do listeners need to backpressure asynchronous handlers, or is this strictly fire-and-forget synchronous execution today?
2. What happens if a listener throws an error? Should it crash the entire emitter event loop or catch and log it?

**User:** Synchronous fire-and-forget. If a listener throws, catch and log it but don't stop execution. Create the implementation plan from our grill session.

**System:** *(Drafts Implementation Plan)* I have initialized the implementation plan at `docs/superpowers/plans/event-emitter-plan.md` using the constraints from the grilling session. It outlines creating `events.js`, setting up error-contained callback loops, and tracking state.

**User:** Incorporate TDD into the plan.

**System:** *(Invokes tdd Phase 1)* Updating `docs/superpowers/plans/event-emitter-plan.md` to append the TDD Strategy contract and behavioral checklist:

**Public Interface Signatures:**
* `on(event: string, cb: Function): void`
* `emit(event: string, data: any): void`

**Behavior Checklist:**
* [ ] Behavior 1: Registering a listener executes it when the matching event fires.
* [ ] Behavior 2: Emitting an event passes payload data successfully to listeners.
* [ ] Behavior 3: An error in one listener does not prevent subsequent listeners from executing.

**User:** Distill the plan.

**System:** *(Invokes distill on the plan)* Interrogating the implementation plan. Here is the distilled output:
1. *Code to Purge:* Shifting away any asynchronous event queues, async/await processing, or wildcards found in the design.
2. *The Bare Primitive:* A single class `EventEmitter` using a local map of arrays wrapped in a straightforward `try/catch` execution loop within `events.js`.
3. *Intentionally Left Naive:* Listener unbind timeouts or execution tracking metrics are completely ignored.

**User:** Looks solid. Slice it vertically, run stress test, execute hyperplan, and call the oracle.

**System:** *(Invokes slice-it-vertically, stress-test-plan, hyperplan, and oracle)*
*Vertical Slice:* The tracer bullet is Behavior 1—proving an event hits a stored callback.
*Stress Test:* Ensured listener callbacks don't leak internal map structures outside.
*Hyperplan Attack:* Subagent warns that identical handlers could be registered multiple times; plan adjusted to address array deduplication.
*Oracle Verdict:* DECISION: YES | WHY: Minimal synchronous footprint, explicitly bounded.

**User:** Great, start TDD loops.

**System:** *(Invokes tdd Phase 2)*
Executing Behavior 1 loop.
🔴 **RED:** Created `test_event_hits_callback`. It throws `TypeError: EventEmitter is not a function`.
🟢 **GREEN:** Implemented minimal skeleton in `events.js`. The test passes.

⚡ **AUTOMATIC GATEWAY: Distill (Code)**
1. *Code to Purge:* Removed an unnecessary wrapper object added during code generation.
2. *The Bare Primitive:* `EventEmitter { events = new Map(); }`
3. *Intentionally Left Naive:* Map keys are left uncleaned if listener arrays go empty.

Ready for the next checklist item?

**User:** Yes, finish the remaining loops, then run taste review and commit.

**System:** *(Executes remaining loops, runs distill on code, then invokes taste review)*
*Taste Review Polish:* Flattened the execution loop block into a clean, readable linear sequence and renamed variables to ensure perfect 3:00 AM ergonomics.
*(Invokes git-commit)* Committed change: `feat(events): implement minimal fault-tolerant synchronous event emitter`
```
