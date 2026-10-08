---
name: playful-haptics
description: Design playful haptic feedback for native iPhone interactions, or inspect an existing codebase for actions that would benefit from it. Use for tactile pattern design, haptic opportunity reviews, and implementation of selected opportunities.
---

# Playful haptics

Make an existing action feel tangible, satisfying, and easy to understand. Playfulness comes from timing, rhythm, and a fitting physical metaphor. Stronger vibration is not a substitute for character.

Use two modes: **review** finds and ranks opportunities; **implementation** designs and adds feedback within the requested scope. A review request stays read-only. For either mode, inspect the product's interaction rules, deployment target, existing feedback, and user preferences first. Default to native iPhone guidance; verify platform support before applying it elsewhere.

## Find opportunities in a codebase

1. Map the existing tactile vocabulary. Search with `rg` for `sensoryFeedback`, `UIImpactFeedbackGenerator`, `UISelectionFeedbackGenerator`, `UINotificationFeedbackGenerator`, `CHHaptic`, `AHAP`, `haptic`, and `feedback`. Follow wrappers to their callers. Inspect standard controls for feedback they already provide.
2. Trace user actions to actual state transitions. Search action handlers, gesture callbacks, completion handlers, and reducers or stores. Inspect surrounding code rather than treating keyword matches as candidates. Separate touch-down, threshold crossing, accepted action, completed operation, cancellation, and failure.
3. Look for moments with a physical or emotional reason to feel something: a snap into place, a release, a meaningful discrete step, an earned completion, or a reversible object manipulation. Examine frequent actions as carefully as prominent ones; a small irritation repeated daily matters.
4. Reject weak candidates. Routine navigation, every button tap, passive refresh, view appearance, and arbitrary scroll offsets seldom justify added feedback. Keep an existing system response when it already fits. Avoid sensor-sensitive moments such as active capture or recording until their physical effects have been checked.
5. Return a short ranked list. For each candidate, give the exact file and symbol, current feedback, trigger, metaphor, expected frequency, proposed pattern/API, suppression conditions, and risk. Include rejected candidates with a brief reason when they explain the recommendation. Recommend the smallest coherent slice; zero additions is a valid result.

A candidate earns implementation when it reinforces a meaningful event, has an exact trigger, adds value beyond existing feedback, and remains pleasant under realistic repetition. Do not add a new action or animation just to host a haptic.

## Design the feeling

Apple's baseline: preserve standard feedback meanings, connect sensation to its cause, coordinate it with visual or audio cues, keep ordinary app feedback brief, and provide a way to disable it. The experience must remain understandable without touch feedback. See [Apple HIG](https://developer.apple.com/design/human-interface-guidelines/playing-haptics).

The following are design heuristics, not Apple requirements:

- Describe the sensation in plain words first: “a soft catch,” “a crisp detent,” or “a small bounce that settles.” Then choose the waveform.
- Establish a quiet everyday vocabulary and reserve distinctive rhythm for rare moments. A repeated completion deserves less ceremony than the end of a long task.
- Use contrast within a short pattern: soft then crisp, a small impulse then a softer echo, or a brief swell then release. Keep the result legible as one event.
- Match the tactile peak to the visible contact, threshold, or resolution. Do not delay the product action to accommodate a pattern.
- Keep the same event's meaning stable. Avoid random patterns for routine actions. Distinguish progress from completion and cancellation from failure.
- Choose silence when the visual action already has enough emphasis. Test the sensation with audio muted so sound cannot conceal poor timing.

For candidate patterns and API decisions, read [Pattern design and implementation](references/pattern-design.md) when designing or changing feedback.

## Implement at the event boundary

Attach feedback to the accepted transition, not rendering, polling, or a broad model observation. For asynchronous work, acknowledge an accepted gesture separately from confirmed success. A success response follows the product's actual success boundary.

Use one owner for each event. Guard against double taps, retries, duplicate callbacks, repeated values, restored state, and background updates. For a drag, fire on meaningful boundary crossings; use hysteresis or rearming to prevent chatter around a threshold. Cancel pending feedback when the interaction ends or becomes stale. Prefer a scheduled Core Haptics pattern over a collection of unrelated delayed closures for precise rhythm.

Reuse the app's existing feedback boundary where it fits. Add only the ownership needed for the selected interactions. Keep feedback failure separate from operation success. Preserve the deployment target and verify API availability against the current SDK.

## Verify and report

Check event routing with focused tests: one response for one accepted event, no completion response on failure, and suppression when disabled or stale. Test shared feedback logic where it exists; avoid building a framework solely for tests.

On a physical supported iPhone, compare the baseline and candidate. Try isolated actions and rapid repetition, cancellation, leaving the screen, background/foreground transitions, and disabled feedback. For custom engines, include interruption recovery. Evaluate timing, comfort, distinctness, and competing system feedback. Check affected camera, microphone, or motion-sensor flows when relevant.

Keep visual and accessible status cues intact. Check the app's motion and sound preferences; Reduce Motion is not itself a universal haptic-disable setting. Follow explicit product preferences rather than inventing a platform policy.

Report selected and rejected opportunities, changed files, checks actually run, and remaining device evidence. Simulator and unit tests can establish routing; they cannot establish tactile quality. Label untested patterns as prototypes.
