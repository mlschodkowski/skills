---
name: apple-design
description: Use when designing, reviewing, or improving UI/UX for Apple-platform apps or cross-platform apps targeting Apple platforms, especially SwiftUI, UIKit, AppKit, Flutter, or React Native. Apply it to screens, flows, motion, accessibility, app icons, and visual direction; do not use it for backend or generic brand work.
---

# Apple design

Make the result feel native to the target Apple platform, calm, legible, and
intentional. Use Apple Human Interface Guidelines as a decision aid, not as a
checklist or a reason to replace a product decision with a stock component.
For cross-platform code, translate the behavior into the framework's native
equivalent while preserving the platform convention.

## Before deciding

- Identify the platform, framework, device input, app category, user goal, and
  exact surface or flow under review.
- Read the repository's product and visual authority first. In Rounds, inspect
  UI-GUIDE.md and VISUAL-IDENTITY.md when they cover the surface.
- Separate observed problems, HIG-backed constraints, product choices, and
  personal taste. State uncertainty instead of inventing a rule.
- Inspect the whole flow, including empty, loading, error, destructive,
  permission, offline, keyboard, large-text, dark-mode, and reduced-motion
  states when they are relevant.

## Core review order

Review in this order and fix the smallest high-impact problem first:

1. **Accessibility and reachability** — Support Dynamic Type, VoiceOver,
   sufficient contrast, meaningful labels and traits, keyboard access where
   applicable, and more than one cue for important state. Keep controls
   reachable and do not move a control under the user's finger during an
   interaction. Use the platform's target-size guidance; do not claim an
   exact size without checking the relevant reference.
2. **Platform behavior** — Prefer native navigation, bars, sheets, menus,
   alerts, text input, permission flows, share sheets, and system colors when
   they fit. Preserve expected back gestures, scrolling, focus, selection,
   keyboard, safe areas, and window behavior. A custom pattern needs a
   concrete user benefit.
3. **Hierarchy and density** — Give each screen one clear primary job. Use
   spacing, type scale, alignment, and progressive disclosure to establish
   hierarchy. Remove repeated explanation, decorative containers, and controls
   that compete with the task.
4. **State and feedback** — Make status, progress, completion, failure, and
   recovery visible without relying on color alone. Prefer quiet, local,
   non-layout-shifting feedback. Make destructive and irreversible actions
   clear and recoverable where possible.
5. **Visual system** — Use semantic colors, platform typography, consistent
   iconography, and materials with a reason. Check light and dark appearance,
   large text, localization, and contrast rather than judging one screenshot.
6. **Motion and sound** — Motion should explain continuity, state, or spatial
   relationship; it should not delay the task or decorate every tap. Respect
   Reduce Motion. Use haptics and sound sparingly, at meaningful state changes,
   and never as the only feedback.

## The premium Apple feeling

When the task includes a launch screen, product video, hero visual, animation,
or marketing surface, use the source material's useful principles:

- One frame or beat should communicate one idea. Let the main object or action
  breathe instead of filling every area with effects.
- Keep the type system small and consistent. Titles, UI copy, and supporting
  text should feel like one family, with hierarchy doing the work.
- Keep the surrounding field quiet and let one intentional color or object
  carry emphasis. Use contrast deliberately; minimal color is not the goal,
  controlled color is.
- Make transitions nearly disappear when continuity is the point. Avoid
  flashy transitions that call attention to the edit instead of the product.
- If sound is part of the deliverable, align it to meaningful changes and keep
  it subordinate to the picture and user intent.

These principles are a polish layer, not a mandate for black backgrounds,
minimalism, or Apple imitation. Apply them only when they improve the user's
understanding, trust, or focus.

## Using the references

Do not load every reference. Start with references/hig-lookup.md, then read
only the files relevant to the surface. For any substantive review, normally
include:

- references/hig/accessibility.md
- references/hig/color.md
- references/hig/layout.md
- references/hig/typography.md

Add focused references for the actual pattern, such as gestures.md,
motion.md, feedback.md, loading.md, modality.md, writing.md, dark-mode.md,
sf-symbols.md, or liquid-glass.md. Translate framework terms into the user's
implementation language, but keep the platform behavior precise. Cite the
reference path or section for important recommendations.

## When improving rather than reviewing

First identify the few highest-impact issues. Then propose or implement
concrete changes in this order: accessibility, broken platform behavior,
hierarchy and content, states and recovery, then polish. Preserve working
product behavior and existing visual direction unless the evidence requires
changing it. Do not add a tour, gesture, animation, abstraction, or custom
component without a case in the requested flow.

## Review output

Keep the report proportional to the problem:

1. Summary and overall severity.
2. Findings ordered by impact, each with **what**, **why**, and **fix**.
3. Positive patterns worth preserving.
4. Platform, framework, and verification notes.

Distinguish facts from inference. If the source, device, assistive technology,
or implementation was not checked, say so. A screenshot review cannot prove
runtime behavior, haptic feel, performance, or production service behavior.
