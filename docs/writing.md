# Writing docs, PR descriptions, and commit bodies

Chat replies follow the Replies rules in `~/.agents/AGENTS.md`. Longer prose goes through three passes:

1. Draft in simplified technical English: short sentences, one idea each, active voice, common words, one term per concept. Use lists only for parallel or sequential items.
2. Shape for an ADHD reader: put the next action or the main point first, number the steps, and keep state on the page. Full rules: `~/.agents/skills/private/i-have-adhd/SKILL.md`.
3. Edit with the `no-ai-slop` skill: keep the writer's voice and replace abstractions with concrete facts. Then do a final sweep with the check step of the `humanizer` skill (not-X-but-Y contrasts, one-line closers, dashes, triads, bold labels).

Done means all three passes ran and the sweep finds no tells.
