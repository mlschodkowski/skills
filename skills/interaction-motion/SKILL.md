---
name: interaction-motion
description: Build, review, or plan purposeful physical motion and tactile feedback for web or native UI. Use for animations, springs, gestures, transitions, haptics, or motion that feels disconnected from the action.
---

# Motion craft

Read [working rules](../mlstack/references/rules.md).

The user's bar is a physical object responding to input, with a stable frame of
reference. A page that slides like paper is different from a camera-like fade
or a generic route transition. Use the supplied video, reference, or interaction
description to identify what moves, what stays still, and what the gesture owns.

## Pick the requested mode

- **Build:** implement the named interaction and verify it.
- **Review:** inspect existing motion and report supported findings; leave source
  unchanged. Use [motion-audit.md](references/motion-audit.md) for the review lenses.
- **Discover:** find missing feedback or spatial continuity. Use
  [opportunity-filter.md](references/opportunity-filter.md) to reject weak ideas.
- **Plan:** save an implementation plan, then stop. Use
  [motion-plan.md](references/motion-plan.md) as a reference, sized to the task.

Keep work in the current agent. No mode requires an executor model, worktree,
rendering framework, or review subagent.

## Give each movement a reason

1. Trace input, manipulation, threshold, accepted state, completion, cancellation,
   reversal, and failure. Decide whether motion helps at all. Frequent actions
   need immediate feedback and little delay; rare moments can carry more character.
2. Preserve spatial ownership: origin, axis, layer, and the part of the interface
   that stays stable. Direct manipulation follows the finger. Release uses the
   current velocity and position rather than restarting a canned animation.
3. Pick the smallest existing tool that fits. Use CSS for simple web state
   transitions, the installed motion library when appropriate, and platform
   animation APIs for native work. Avoid a new dependency for a small effect.
4. Read [motion-construction.md](references/motion-construction.md) for curves,
   durations, springs, interruption, exit, and property choices. Use
   [motion-recipes.md](references/motion-recipes.md) for a matching web component.
   Treat numeric values as starting points within the product's actual behavior.
5. Add haptics where they distinguish meaningful events: selection, threshold,
   accepted action, completion, or failure. Use a coherent range of soft and
   stronger patterns; strength alone is not character. Read
   [tactile-patterns.md](references/tactile-patterns.md) when choosing APIs,
   timing, engine lifecycle, or suppression rules.

Keep haptics tied to actual state, avoid duplicating system feedback, and respect
hardware support and user settings. Coordinate sound, visuals, and touch without
making any one channel essential. Support reduced motion with equivalent
information and control.

## Feel-check

Exercise rapid repeats, interruption, reversal, cancellation, slow completion,
failure, keyboard input, and reduced motion. Inspect exits and the next action,
not just a polished entrance. Watch a recording in slow motion when the physical
effect is hard to judge. Check real hardware for gestures and haptics when possible.

Report what was observed, exact properties or values changed, and what still
needs device testing. A build or static source review does not prove that the
movement feels right. Preserve the interaction's meaning when choosing a simpler
implementation.
