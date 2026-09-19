---
name: interface-taste
description: Use when designing, specifying, reviewing, or implementing user-facing interface details where calm hierarchy, precise interaction, motion, materials, haptics, or high-quality feedback matter. Apply after the user's goal and core flow are clear; pair with platform and accessibility guidance rather than using polish to compensate for a confusing product.
---

# Interface taste

Turn “make it feel polished” into behavior another agent can build and a person
can notice. Treat taste as a way to improve understanding, control, confidence,
and comfort—not as permission to add decoration.

Use this as a polish-and-control layer alongside:

- $human-first-product-flow for the actor, desired result, shortest successful
  path, canonical ownership, necessary branches, and recovery. Do not polish a
  flow whose normal path is still unclear.
- $apple-design for Apple-platform behavior, accessibility, native patterns,
  hierarchy, state feedback, materials, motion, sound, and the relevant HIG
  references. Translate those decisions into the target framework on
  cross-platform work.

Read the product and visual authority, current implementation, and relevant
runtime evidence before changing an established surface. Separate observed
behavior, platform guidance, product decisions, and personal taste. If a
device, assistive technology, or runtime behavior was not checked, say so.

## The governing balance

Use the leading principle: **calm by default, precision on demand**.

- At rest, reduce noise. Give the screen one clear job, a stable hierarchy,
  quiet surfaces, and only the feedback needed to orient the person.
- During manipulation, become precise. Track the user's input directly, make
  the active control legible, preserve context, and give the person a forgiving
  way to reach a useful result.
- At commitment or change, be reassuring. Confirm meaningful state changes
  locally, with feedback proportional to their consequence.
- When continuity matters, let transitions nearly disappear. Motion should
  explain where something came from, what changed, or what can be controlled.

Every detail must earn its cost by improving comprehension, reducing effort or
error, preserving control, or making state legible. If it only makes a screen
look busier or tries to manufacture “delight,” remove it.

## Work in this order

### 1. Ground the decision

Name the platform, framework, device and input method, surface, actor, current
state, and user goal. Identify whether the person is reading, choosing,
manipulating, waiting, recovering, or committing. Inspect the normal path before
the edge cases, then cover only the states that can change the decision.

For an existing surface, distinguish what is observed from what is documented
or inferred. For a new flow, establish its shortest understandable path with
$human-first-product-flow before choosing motion or visual treatment.

Completion check: the intended result, starting state, primary action, and
visible completion state are concrete.

### 2. Write the interaction contract

Specify behavior before adjectives. For each important control or transition,
state:

1. **Trigger** — what starts it and what input is accepted.
2. **Immediate response** — what changes under the finger, pointer, keyboard,
   or VoiceOver focus.
3. **Continuous behavior** — what follows the input and what stays stable.
4. **Settle or commit** — how the final state is chosen, reached, and confirmed.
5. **Interruption** — whether the person can cancel, reverse, re-grab, or
   continue while feedback is still settling.
6. **Recovery** — what happens on invalid input, failure, dismissal, or loss of
   connection.
7. **Accessible equivalent** — how the same outcome works without the gesture,
   fine motor control, color cue, sound, or motion.

Completion check: another agent could implement the interaction without
guessing what “smooth,” “intuitive,” or “delightful” means.

### 3. Shape hierarchy and density

Use the smallest visual system that supports the job:

- establish one primary action and a clear next step;
- use type, spacing, alignment, scale, and progressive disclosure before adding
  containers or effects;
- keep supporting information available without competing with the task;
- reserve strong contrast, color, blur, and motion for meaningful emphasis;
- keep feedback local and preferably non-layout-shifting;
- preserve the person's context when opening detail, changing modes, or showing
  a result.

Choose materials for a reason: separation, legibility, focus, or continuity.
Describe what a blur or translucency is separating and how it behaves in light,
dark, large-text, high-contrast, and reduced-transparency conditions. Do not
stack effects just because the implementation makes them easy.

Completion check: the primary job remains obvious in a quiet screenshot and
after the interface has entered an active state.

### 4. Specify motion, tactility, and sound

Name the property, curve, relationship, and stopping condition instead of
writing “make it smooth.” Use the least motion that communicates the change.

- **Direct manipulation:** the object or divider follows the input with no
  artificial lag; surrounding content stays stable unless the behavior requires
  it to respond.
- **Continuity:** use a short “ease-in-out” or another appropriate continuity
  curve when an element changes state without being directly dragged. State why
  the chosen curve fits the relationship.
- **Release and settling:** use “ease-out” or a restrained, damped spring when a
  control completes a gesture. It should settle on a legible target without
  distracting overshoot, and remain immediately re-grabbable.
- **Entry and exit:** use “ease-in” only when the delayed departure or arrival
  helps explain causality. Do not make people wait for decorative motion.
- **Interruption:** animations should yield to new input, preserve the latest
  meaningful state, and avoid moving a control underneath the person's finger.
- **Reduced motion:** provide a useful reduced-motion path, such as a direct
  state change or restrained fade, while preserving hierarchy and feedback.
- **Performance:** keep motion stable under real content, scrolling, keyboard
  appearance, and device load. Do not claim a tactile or performance quality
  from a static screenshot.

Use haptics at meaningful boundaries—such as a confirmed snap, selection,
success, warning, or failure—when they improve state recognition. Keep them
brief, sparse, and subordinate to visible feedback. Do not buzz continuously
through a drag or make haptics the only confirmation. Use platform-native
feedback where available and provide an understandable non-haptic equivalent.
Apply the same restraint to sound.

Completion check: each animated, tactile, or audible detail has a user-facing
purpose, a stopping condition, and a non-decorative fallback.

## Precision patterns

Give people precision when the task demands it, but do not make precision work
the default cost of ordinary use.

For a draggable split view, write a contract like this:

    The divider follows the pointer or finger directly within readable
    minimums. On release, it chooses the nearest useful snap point—such as
    25%, 50%, or 75% when those proportions preserve the content—rather than
    requiring a perfect landing. The handle settles with a short ease-out or
    restrained damped spring, emits at most one meaningful snap cue, and can be
    grabbed immediately. The person can still make a fine adjustment through
    direct dragging and an accessible value-based control; the current
    proportion and limits are perceivable without relying on color.

Adapt this pattern to the content and platform. Snap points should represent
useful semantic states, respect minimum and maximum readable sizes, and avoid
jitter near a boundary. Persist the last useful position only when doing so
helps the person's ongoing task. Provide keyboard, pointer, and assistive
technology adjustments where the platform supports them.

The same rule applies to sliders, timelines, crop handles, reorderable lists,
zoom, and canvas tools: make the common result easy to reach, expose precision
when requested, and let the person correct a mistake without starting over.

## Native, accessible, and stateful by design

Before calling a treatment finished, check the relevant parts of this list:

- Dynamic Type or equivalent text scaling, localization, contrast, dark and
  light appearance, and content that can grow without clipping;
- VoiceOver or equivalent labels, traits, focus order, adjustable values, and
  a non-gesture path to every consequential action;
- platform-appropriate target sizes, reachability, keyboard and pointer input,
  safe areas, focus, selection, scrolling, back navigation, and window behavior;
- loading, empty, error, offline, permission, destructive, cancellation,
  interruption, and recovery states when they affect the user's result;
- visible feedback that does not rely on color, sound, haptics, or motion alone;
- state changes that preserve context, remain reversible where possible, and do
  not steal focus or unexpectedly move content.

Prefer native navigation, sheets, menus, alerts, text input, system colors,
gestures, and feedback when they fit. A custom treatment needs a concrete user
benefit and an equivalent accessible path.

## Language for agent-readable design

Replace vague taste words with observable instructions:

- “quiet at rest” → “keep secondary controls visually subordinate until the
  person enters the relevant mode”;
- “smooth drag” → “track the input directly, then settle to the nearest target
  with a short ease-out and no layout jump”;
- “premium blur” → “use one material layer to separate the foreground from the
  scrolling content while preserving text contrast and context”;
- “delightful feedback” → “confirm the completed state locally with one brief
  visual change and, where appropriate, one restrained haptic”;
- “intuitive” → describe the affordance, threshold, result, and recovery.

For a design specification, use this compact contract and fill only the fields
that matter:

    ### [Surface or interaction]
    Intent: [the person's goal]
    Starting state: [what is visible and available]
    Trigger: [input and affordance]
    Direct response: [what follows the input; what stays stable]
    Motion: [property, curve or spring, interruption, stopping condition]
    Settle/commit: [target, threshold, snap, confirmation]
    Feedback: [visual, haptic, or sound cue and purpose]
    Accessible equivalent: [non-gesture, label, value, keyboard, or focus path]
    Reduced motion/material behavior: [fallback]
    Failure/recovery: [correction, undo, retry, or resume]
    Acceptance: [observable scenarios for common, boundary, and recovery cases]

## Review and delivery contract

When reviewing or proposing interface work, report findings in impact order:

1. user goal and flow problems;
2. accessibility or broken platform behavior;
3. hierarchy, content, and density;
4. state visibility and recovery;
5. interaction precision and control;
6. motion, material, haptic, sound, and visual polish.

For each non-trivial recommendation, state **what changes**, **why it helps**,
and **how to observe that it works**. Include positive patterns worth keeping.
For implementation work, preserve existing product behavior and visual
authority unless the evidence requires a change. Keep acceptance scenarios
concrete: a first-time person, a returning person, a boundary value, an
interrupted action, and the relevant accessibility or reduced-motion path.

Done means the interface is calmer when idle, more precise when manipulated,
clearer when state changes, and still understandable and controllable across
the relevant platform states. It does not mean every screen has an animation,
blur, or haptic.
