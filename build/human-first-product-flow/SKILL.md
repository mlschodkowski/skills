---
name: human-first-product-flow
description: Design or simplify application behavior, user journeys, and business processes around the user's shortest understandable path to a result. Use before implementation or when an existing product has too many steps, states, choices, roles, exceptions, or duplicate ways to perform the same action. Do not use for purely visual styling or backend-only design with no user-facing workflow.
---

# Human-first product flow

Design the behavior a person needs before designing the machinery that supports
it. Make the normal path obvious, short, and forgiving. Complexity is justified
only by a real user need, business rule, legal obligation, or material risk.

Use one of two modes:

- **Design** for a new or materially changed workflow.
- **Simplify** when an existing application or specification already defines
  the workflow.

## 1. Establish reality

Read the product authority, relevant code, current screens, support evidence,
analytics, and existing rules that are available. Do not invent a business rule
from the data model or current implementation.

State:

- who is acting and what situation brought them here;
- the result they want in their own terms;
- what starts the process and what visibly means it is finished;
- which rules are confirmed, assumed, or still unknown.

If several people take part, give each one a separate goal and shortest path.
Expose only the information and decisions that participant needs. Do not solve a
handoff by giving everyone the same status-heavy workflow or dashboard.

For an existing product, walk the current end-to-end path and distinguish
observed behavior from documentation and inference.

Done when the actor, trigger, desired result, and evidence are concrete.

## 2. Write the shortest successful path

Describe one ordinary scenario as actions and responses, from entry to visible
completion. Use the person's language, not screen names, database entities, API
calls, or internal statuses unless the person actually needs those concepts.

For every step or decision, ask:

- Does the person need to do or understand this to reach the result?
- Can the application infer it, remember it, default it, or defer it?
- Is the choice meaningful now, or only an implementation concern?
- Does it repeat information or work already given?

Remove, automate, combine, remember, or defer anything that does not earn its
place. Do not hide necessary complexity behind vague copy; remove its cause when
the product can safely own it.

### One intent, one process

Inventory every place where the person can start each core action. When two
entry points express the same intent and produce the same result, give that
action one canonical home in the product and one canonical flow. Do not let the
person perform the same process through separate buttons, cards, menus, or
intermediate actions with their own wording, rules, defaults, validation, or
outcomes.

If the action must be discoverable from several contexts, secondary entry
points may link into the canonical flow. They must converge before the person
makes a consequential choice. Do not copy or fork the process.

Keep separate flows only when the person's goal, required information, rules,
or consequences materially differ. Name that difference explicitly; screen
location or implementation convenience is not sufficient.

Done when the normal path contains only necessary human actions and decisions,
and each user intent has one identifiable process for reaching its result.

## 3. Add only necessary branches

Add a branch only when it changes what the person must do, what the application
may do, or what outcome is possible. Prefer good defaults and progressive
disclosure over asking everyone to configure rare cases.

Cover the relevant boring paths:

- missing or invalid input;
- interruption, cancellation, and later resumption;
- failure with a clear recovery action;
- destructive or irreversible consequences;
- permissions, offline behavior, handoffs, or approvals when the workflow
  genuinely depends on them.

Do not model hypothetical roles, statuses, settings, and exceptions merely
because the architecture can support them. Do not make people reproduce the
system's internal state by hand.

Done when every remaining branch has a concrete reason and recovery behavior.

## 4. Control the complexity budget

Review the process as a whole. Challenge each concept, required choice, state,
role, handoff, confirmation, and configuration surface. Name the rule or risk it
protects and the cost it creates for the normal user.

Prefer:

- one clear primary action at a time;
- safe and useful defaults;
- recognition instead of recall;
- information requested at the moment it becomes necessary;
- automatic persistence and resumption;
- undo or correction instead of preventive ceremony;
- one canonical process instead of several equivalent implementations.

If two concepts behave the same from the user's perspective, combine them. If a
status exists only to coordinate implementation, keep it out of the user's
mental model.

Done when no remaining complexity is justified only by flexibility,
future-proofing, technical symmetry, or completeness for its own sake.

## 5. Produce the behavior contract

Keep the output proportional. For an ordinary flow, provide:

1. **Person and result** — who needs what and why.
2. **Shortest successful path** — numbered human actions and application
   responses.
3. **Application-owned work** — defaults, inference, persistence, and automation.
4. **Canonical ownership** — where each core action lives and which secondary
   entry points, if any, only link into it.
5. **Necessary branches and recovery** — only cases that materially change the
   path.
6. **Deliberate omissions** — configuration, states, roles, duplicate entry
   points, or variants excluded to keep the product understandable.
7. **Acceptance scenarios** — concrete examples proving completion, failure, and
   recovery through observable behavior.

In Simplify mode, also show the observed current path, the proposed target path,
and a ranked cut list. For every cut, state what disappears, what behavior is
preserved, and any migration or compatibility consequence.

Do not turn the contract into a catalogue of every theoretical edge case or a
screen-by-screen implementation specification.

## 6. Verify before implementation

Walk the contract from the perspective of a first-time person and a returning
person performing the common task. Check that they can tell:

- what to do next;
- what the application did for them;
- whether the process finished;
- how to correct a mistake or continue after interruption.

Start each core action from every visible entry point. Confirm that equivalent
intents converge on the same process before any consequential decision and
cannot drift into different rules or results.

For an existing application, verify important claims against the real behavior
and preserve them with focused acceptance coverage when changes are requested.
Do not claim that a flow is simple solely because it uses fewer screens; count
hidden decisions, unfamiliar concepts, waiting, and recovery work too.

If a consequential product rule remains unresolved, ask one concrete question
and recommend the simplest safe default. Otherwise, present the contract and
continue into design or implementation when the user's request includes it.

Done when the flow can be explained plainly, its complexity is accounted for,
and its success is observable from outside the implementation.
