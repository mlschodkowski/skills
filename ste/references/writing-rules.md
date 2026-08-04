# ASD-STE100 Writing Examples

Use these examples as reference patterns for technical prose. Part 1 contains paraphrased rule illustrations from public secondary sources. Part 2 contains original examples for agent output. They are not quotations from the ASD-STE100 standard and do not define the approved-word dictionary.

## Part 1 — Rule Illustrations

| Rule | Before | After | Why |
|---|---|---|---|
| One meaning per word | “Verify the system.” / “Check the connections.” / “Confirm receipt.” | “Make sure the system is correct.” | Near-synonyms can force the reader to guess whether the actions mean the same thing. |
| One part of speech per word | “Oil the valve.” | “Apply oil to the valve.” | Use a word in its approved part of speech. |
| Precise verb meaning | “Follow the safety instructions.” | “Obey the safety instructions.” | “Follow” can mean “come after” or “obey.” Use the unambiguous meaning. |
| Simple tense only | “We have received the technical reports from HQ.” | “We received the technical reports from HQ.” | Simple past avoids an extra question about when the action happened and whether it continues. |

## Part 2 — Applied Examples

These examples show how the same rules help another agent, a translation layer, or a non-native reader parse technical text.

### Example A — Tool Description

Before:

> This tool will attempt to synchronize state across the various backends that have been configured, and if a conflict is detected it may resolve it automatically depending on the strategy that has been set, or otherwise it will surface the conflict for manual review.

Problems:

- Two instructions appear in one sentence: synchronize, then resolve or report.
- Several modal and auxiliary forms add uncertainty.
- The sentence has 55 words and exceeds the 25-word descriptive target.

After:

> The tool synchronizes state across the configured backends. If it finds a conflict, it checks the current strategy. If the strategy allows automatic resolution, the tool resolves the conflict. If not, the tool reports the conflict for manual review.

### Example B — Error Message

Before:

> An error may have occurred while processing your request due to a possible mismatch in the expected data format, which could be caused by an outdated client version.

Problems:

- The passive construction does not identify the actor.
- Several modal and auxiliary forms add uncertainty.
- One sentence carries two claims: the request failed and a client version may be the cause.

After:

> The request failed. The data format did not match what the server expected. Check your client version. An outdated client can cause this error.

### Example C — Inter-Agent Instruction

Before:

> Once the upstream job has completed and assuming no errors were raised, the downstream agent should proceed to consume the output artifact, though it is worth noting that partial artifacts are sometimes produced under timeout conditions.

Problems:

- Subordinate clauses hide the condition and the action.
- One sentence carries three facts: completion, the next action, and a timeout case.
- The instruction exceeds the 20-word procedure target.

After:

> Wait for the upstream job to finish with no errors. Then read the output artifact. Warning: a timeout can produce a partial artifact. Check that the artifact is complete before you use it.

## How to Use These Examples

Part 1 shows the rule pattern. Part 2 shows the transfer to tool descriptions, error messages, and inter-agent instructions. Apply the pattern to the user's facts. Do not copy a word without checking its approved meaning and part of speech when strict STE compliance matters.
