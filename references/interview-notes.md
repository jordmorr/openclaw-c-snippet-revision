# Interview Notes

Use this reference when the user specifically wants AI-led or practical code-review-style interview prep.

## Typical constraints

- Examples are in C.
- The user may not be allowed to use tools; debugging may be visual inspection only.
- Common structure:
  - Level 1: short bug-spotting snippets
  - Level 2: a few functions from a larger C system with a realistic error

## Best emulation style

- Ask the user to explain what the code is trying to do, what the bug is, what failing case exposes it, how to fix it, and what tests to run.
- Reward concise spoken-debugging structure.
- Prefer practical bugs over puzzle-like tricks.
- Bias toward code review / reasoning clarity rather than coding from scratch.

## Good answer structure to coach

1. `This function is trying to...`
2. `The main bug is...`
3. `A concrete failing case is...`
4. `I’d fix it by...`
5. `I’d test...`
