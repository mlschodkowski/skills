---
name: audit-loop
description: Use during the TDD/Implementation phase immediately after a test turns green, before declaring a step done.
---

# Audit Loop
Your job is to halt the implementation loop to measure the hidden maintenance liability and cognitive load of the newly written code. 

Analyze the fresh code line-by-line and identify:
1. **Cognitive Load Points:** Where must a reading engineer hold more than 3 concepts in their head simultaneously? Look for deep nesting, mutable flag variables, or high cyclomatic complexity.
2. **Leaky Complexity:** Did the implementation sneak in a clever abstraction or defensive boilerplate that wasn't explicitly demanded by the vertical slice? 
3. **The Empathy Test:** Would an exhausted engineer enjoy opening this file at 3:00 AM to fix a bug, or is the execution path cluttered with mental obstacles?

PREFER: Local reasoning, linear reading paths, boring obviousness, high conceptual compression.
REJECT: Unnecessary cleverness, defensive over-abstraction, frantic patching.

OUTPUT:
- Friction Points (Lines that slow down human reading)
- The Flattening Proposal (A concrete refactoring diff to simplify the logic and rip out any code that didn't earn its keep)
