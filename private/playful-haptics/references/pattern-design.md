# Pattern design and implementation

Research checked on 2026-10-07. Numerical recipes below are original starting points, not Apple presets or validated perceptual thresholds.

## Choose the smallest API

| Need | Starting point | Decision |
| --- | --- | --- |
| Existing standard control | Built-in feedback | Check it on device before adding anything. |
| Discrete state change in SwiftUI | `sensoryFeedback` | Use a precise trigger and condition. Confirm symbol and platform availability. |
| Selection, impact, or outcome in UIKit | Corresponding feedback generator | Preserve its documented meaning. |
| Designed rhythm, envelope, or evolving texture | Core Haptics | Use only when simpler feedback cannot express the intended sensation. |

[SwiftUI SensoryFeedback](https://developer.apple.com/documentation/swiftui/sensoryfeedback) defines semantic feedback. Its [conditional modifier](https://developer.apple.com/documentation/swiftui/view/sensoryfeedback(_:trigger:condition:)) plays on a trigger change that passes a condition. A collection count alone cannot distinguish user completion from sync or restore; choose an event or transition with enough context.

For UIKit, retain the generator for the interaction. Call [`prepare()`](https://developer.apple.com/documentation/uikit/uifeedbackgenerator/prepare()) when feedback becomes likely, before the trigger. Calling it immediately before playback does not reduce latency. Avoid keeping hardware prepared indefinitely.

## Compose a short tactile phrase

[Core Haptics](https://developer.apple.com/documentation/corehaptics) provides transient events for impulses and continuous events for sustained sensations. Intensity sets strength. [Sharpness](https://developer.apple.com/documentation/corehaptics/chhapticevent/parameterid/hapticsharpness) runs from rounded to crisp, with event values from 0 to 1. Lower sharpness does not mean lower intensity.

Write a timeline before code. State the event type, relative time in milliseconds, intensity, sharpness, and continuous duration if applicable. Relate each event to something the person sees or does.

| Prototype | Timeline `(ms, intensity, sharpness)` | Fit and caution |
| --- | --- | --- |
| Soft catch | Transient `(0, 0.30, 0.20)` | A gentle accepted placement. Compare against one system impact first. |
| Tiny bounce | Transients `(0, 0.45, 0.45)`, `(65, 0.20, 0.20)` | Visible contact followed by settling. Drop the echo if it feels like two actions. |
| Earned finish | Transients `(0, 0.25, 0.25)`, `(90, 0.50, 0.60)` | A rare culmination. Compare against standard success; do not stack both. |
| Detent | One low-intensity transient per accepted discrete step | Map to values, not pixels or frames. Limit density during fast traversal. |

Start with one impulse. Add another only when it conveys a perceptible part of the action. Tune one dimension at a time: onset, spacing, intensity, then sharpness. If a double pulse reads as an alert, simplify it. Use continuous feedback only when a sustained interaction supplies a clear start, evolution, and stop; ordinary waiting does not need a vibration loop.

For live modulation, read Apple's [continuous and transient sample](https://developer.apple.com/documentation/corehaptics/updating-continuous-and-transient-haptic-parameters-in-real-time). Event parameters, dynamic controls, and curves have different scopes and ranges; verify them rather than copying event values into dynamic controls. For stable designer-authored timelines, consider AHAP; for input-derived patterns, programmatic events may fit better.

## Make custom playback reliable

Follow [Preparing your app to play haptics](https://developer.apple.com/documentation/corehaptics/preparing-your-app-to-play-haptics): check `CHHapticEngine.capabilitiesForHardware().supportsHaptics`, retain the engine, install handlers before starting, and recover from resets by rebuilding players and registered resources as needed. Restart for valid new playback after stoppage; do not replay a stale completion.

Treat unsupported hardware and playback errors as silent feedback loss. Keep the operation usable. Do not copy sample `fatalError` handling into a production feedback path. Manage engine activity around actual use rather than starting an engine for each frame or keeping it active without need.

[`stoppedHandler`](https://developer.apple.com/documentation/corehaptics/chhapticengine/stoppedhandler-swift.property) runs outside the main thread. Protect shared state and cross to the correct actor for UI work. Respect the app's audio-session ownership; adding touch feedback does not justify disrupting other audio.

## Research basis

Apple's [Designing Audio-Haptic Experiences, WWDC19](https://developer.apple.com/videos/play/wwdc2019/810/) explains designing sensation alongside sound and visuals. Use it to reason about rhythm and physical coherence, rather than treating waveform values as a universal recipe. The [Playing haptics HIG](https://developer.apple.com/design/human-interface-guidelines/playing-haptics) remains the design baseline. Recheck current Apple documentation when implementing unfamiliar APIs or supporting another platform.
