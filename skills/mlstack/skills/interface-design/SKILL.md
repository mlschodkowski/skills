---
name: interface-design
description: Design or improve a UI around a clear user flow, calm hierarchy, grouped information, and consistent interactions. Use for clutter, uncertain next actions, layout, typography, or mobile interaction problems.
---

# UI craft

Read [working rules](../mlstack/references/rules.md).

Start with the person's goal and the shortest successful path. Read the current
UI, design rules, and state model. Inspect the running screen when available.
A source review alone cannot prove that the interface feels clear.

## Make the next action obvious

1. State what the user wants to do, what they see first, and how they know they
   succeeded. Keep the original product goal through later design decisions.
2. Group each value, state, history entry, and action with the object it belongs
   to. A reader should see where one record ends and the next begins. Use space,
   alignment, type, and surface hierarchy before adding more separators.
3. Make the important information and primary action easy to find. Remove
   repeated explanations, empty groups, competing badges, and decoration that
   makes every element equally loud. Keep necessary recovery and help available.
4. Keep interactions consistent across equivalent objects. If swipe, hold,
   edit, or dismiss works on one type, inspect the corresponding behavior on the
   others. Do not add a hidden gesture as the only way to perform a core action.
5. Design loading, empty, error, repeated-action, and recovery states. Show what
   happened and what the person can do next. Preserve keyboard access, focus,
   readable contrast, and reduced-motion behavior.

## Match the product

Use the established components, visual identity, and platform. For Apple-style
physical interactions and typography, read
[apple-principles.md](references/apple-principles.md). For detailed interaction
and material choices, read [interface-details.md](references/interface-details.md).
For Swiss/Geist composition, read [grid-and-type.md](references/grid-and-type.md)
only when that direction fits the request or existing product.

The user's past black/gray/red palette and font choices belonged to particular
products. Do not turn them into a universal theme. Prefer the current design
system over a new palette or font dependency. Light and dark modes need separate
inspection when the product supports both.

For mobile web, read [mobile-details.md](references/mobile-details.md): viewport,
safe areas, touch, scroll, inputs, and browser behavior. For motion and tactile
feedback, use [interaction-motion](../interaction-motion/SKILL.md). Finish the flow before
adding polish. Simplicity should still feel useful and considered.

## Verify the visible result

Drive the actual user path at relevant widths and input methods. Inspect
grouping, overflow, menus, tables, focus, recovery, and states touched by the
change. Use screenshots or video when the change depends on visual comparison.
Test gestures on hardware when available; label simulator-only evidence.

For review-only work, report a short ranked list with locations, observed
problems, and specific corrections. For implementation, build the requested
slice and verify it. When asked for a plan, save it and stop. Do not turn routine
design choices in an implementation request into extra approval gates.
