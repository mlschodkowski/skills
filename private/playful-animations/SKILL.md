---
name: playful-animations
description: Design playful motion for existing interactions, or inspect a native iPhone or web codebase for animation opportunities and motion that needs restraint. Use for physical and emotional motion design, opportunity reviews, and implementation of selected interactions.
---

# Playful animations

Make existing actions feel tangible, responsive, and satisfying. Give motion a reason before giving it a curve. Playfulness can be a small catch or a clean release; it does not require bounce, spectacle, or a new interaction.

Use **review** to find and rank opportunities, or **implementation** to build the requested slice. Reviews stay read-only unless the user requests a saved artifact. Implementation requests include the necessary inspection and verification; do not insert a separate approval gate for routine design choices within scope.

## Find opportunities in a codebase

1. Inspect the product's interaction rules, stack, deployment target, and motion conventions. Identify system-owned navigation, controls, and gestures. Preserve their behavior. Map existing animation helpers, tokens, springs, and reduced-motion handling before adding values or abstractions.
2. Search with `rg`, then follow the relevant callers and state changes. For SwiftUI/UIKit, look for `withAnimation`, `.animation`, `.transition`, `matchedGeometryEffect`, `phaseAnimator`, `keyframeAnimator`, `UIView.animate`, `UIViewPropertyAnimator`, and gesture handlers. For web, look for `transition`, `@keyframes`, `animate`, `useSpring`, `motion.`, WAAPI, and `prefers-reduced-motion`. Search action handlers and completion paths too: missing motion has no animation symbol.
3. Trace the full interaction: input, direct manipulation, accepted transition, completion, reversal, cancellation, and failure. Inspect empty, loading, error, and repeated-action states. Identify where something jumps, loses its origin, resists the finger, restarts abruptly, or falsely signals success.
4. Look for moments with a physical or emotional reason to feel something: a snap into place, a release, a meaningful discrete step, an earned completion, or a reversible object manipulation. Examine frequent actions as carefully as prominent ones; a small irritation repeated daily matters.
5. Vet each candidate against its actual code and product purpose. Separate missing feedback from existing motion that should be shortened, simplified, or removed. Keep system motion when it already fits. Routine navigation, passive refresh, and every element entering the viewport are weak reasons for extra choreography.
6. Return a short ranked list by user value, frequency, and implementation risk. Give the file and symbol, current behavior, event, purpose, intended feeling, proposed motion, interruption behavior, reduced-motion variant, and verification. Label inferred frequency and unobserved behavior. Recommend one coherent slice. Zero additions is a valid recommendation.

Frequency changes the design budget, not whether an interaction deserves inspection. Frequent actions favor immediate tracking, tiny responses, or instant changes. Rare milestones can carry a short expressive resolution. Keyboard input is not a blanket exclusion: preserve immediate results and focus, and keep any useful continuity unobtrusive.

## Design the feeling

Before selecting an API, write one sentence: “When [event], [object] should feel [physical or emotional quality], so the person understands [meaning].” If the sentence cannot identify a benefit, use an instant state change.

Choose a purpose: feedback, spatial continuity, state clarity, explanation, or earned delight. Explanation belongs where the person needs to learn something. Delight earns its place through the significance of the event and the product's character.

- **Give the object a physical story.** Identify its origin, destination, contact point, constraint, and release. An anchored element moves from its anchor; a dragged object follows the finger; a settled object stops moving.
- **Keep one dominant beat.** Contact, acceptance, or resolution carries the emphasis. Supporting movement stays quiet. Avoid making an entire screen celebrate a small action.
- **Design contrast.** Direct tracking can resolve into a soft catch. A deliberate hold can end with a crisp release. A rare completion can have one small overshoot that settles. The contrast must explain the action.
- **Preserve continuity.** Keep identity, direction, and geometry legible across states. Reverse toward the actual prior state or interaction origin when that helps comprehension; do not impose symmetric exits where navigation or the gesture implies another path.
- **Respect attention.** Keep reading content and actionable targets stable. Do not make a person wait for decorative motion before the next action works. Avoid stagger that serializes useful content.
- **Build a consistent vocabulary.** Similar objects and events share behavior. Reserve a distinctive rhythm for a meaningful exception. Reuse established values before adding another token.
- **Use restraint as a design tool.** Compare the expressive version with a simpler version and no motion. Keep the smallest response that improves understanding or satisfaction.

## Translate the feeling into motion

Choose the smallest existing tool that can express the interaction. Preserve native system transitions. In SwiftUI, scope animation to the relevant state and view; avoid animating unrelated changes through a broad transaction. Use UIKit animation tools at an existing bridge when needed. On web, use CSS transitions for simple retargetable state changes; choose WAAPI or an existing motion library when playback control, layout, or gesture dynamics justify it. Do not install a library for a fade.

Prefer decelerating motion for a quick response that settles. Use continuous, gentle easing for movement between stable positions. Use a spring when release velocity, interruption, or a physical constraint matters. Linear motion fits genuine constant progress, not a default entrance.

Treat these as prototype ranges, not universal requirements: small responses around 100–180 ms; ordinary transitions around 150–300 ms; a larger spatial transition around 250–450 ms. Reuse the project's values first. Springs depend on the platform's parameter model; do not copy CSS curves or web spring configurations into SwiftUI. Tune displacement and overshoot before adding duration. Large travel and repeated oscillation often cost more attention than a slightly longer settle.

On web, favor transform and opacity when suitable. Verify layout and paint costs when animating geometry. Compositor behavior depends on the property, library, and browser; inspect rather than claiming an API is always GPU accelerated. Native layout animation follows different rules; preserve correct reflow instead of importing web restrictions.

For a gesture, track input directly, then resolve on release. Retarget from the current presentation state and preserve velocity where the API supports it. Rapid toggles, repeated taps, reversal mid-flight, and cancellation must reach the correct final state without jumping to an obsolete starting pose.

Use sequences for real multi-stage events. Tie completion feedback to confirmed completion, not a timer or optimistic button press. Cancel stale sequences when the view disappears or the action changes. Keep business state independent from decorative completion callbacks.

If haptics already accompany the interaction, align the tactile peak with visible contact or resolution. Add haptics only when requested or within the authorized scope; consult `playful-haptics` for their design. Avoid stacking independent celebrations across sound, motion, and touch.

## Ship all interaction states

Include reduced motion in the same slice. Preserve meaning through an instant state update, a quiet opacity change, or another suitable alternative. Remove unnecessary travel, zoom, parallax, and oscillation. Reduced motion does not require retaining a fade if an instant change is clearer.

Preserve focus, hit targets, scrolling, accessibility semantics, and system gesture behavior during transitions. On web, gate hover-only motion to devices with hover and a fine pointer. Check large text and changed content sizes so geometry remains correct.

## Verify and report

Compare baseline and candidate at normal speed first. Use slow playback and frame stepping to inspect onset, contact, overshoot, interruption, and settling; return to normal speed to judge comfort. Repeat the action in a realistic sequence, not just a polished demonstration.

Check rapid retriggering, reversal, cancellation, leaving the screen, reduced motion, large text, empty/error/busy states, and focus or gesture behavior where affected. Run focused regression tests for state or lifecycle changes. Use recordings or runtime inspection for visual claims. Test gesture feel and performance on a physical device when relevant; simulator captures do not establish those qualities.

Report what changed, why the event merits motion, the chosen tool and timing or spring, checks actually run, and remaining evidence. Keep rejected opportunities brief. If runtime inspection is unavailable, label the result a prototype and name the exact feel-check still needed.

## Basis

Adapted from the purpose-first construction sequence in [animate](../../emilkowalski/animate/SKILL.md) and the evidence-based audit in [improve-animations](../../emilkowalski/improve-animations/SKILL.md). This skill owns its workflow. Those skills are optional further reading, not mandatory steps. The timing ranges and frequency guidance here are design heuristics, not platform guarantees.
