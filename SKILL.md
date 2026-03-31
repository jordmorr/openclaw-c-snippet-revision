---
name: c-snippet-revision
description: "Run a one-at-a-time C debugging and code-review revision game for interview preparation. Use when the user wants C bug-spotting practice, asks for C snippets to inspect visually, wants mixed difficulty snippet drills, or wants interactive feedback on what is wrong with a C code sample. Supports two levels: (1) short self-contained bug-spotting snippets, and (2) larger multi-function/system-style snippets with realistic ownership, API-contract, error-path, and boundary bugs."
---

# C Snippet Revision

Run an interactive C code-review drill focused on visual inspection, explanation quality, and practical debugging judgment.

## Core loop

- Show exactly one snippet at a time.
- Randomly choose Level 1 or Level 2 unless the user asks for a specific level or theme.
- After showing the snippet, ask only: `Tell me what’s wrong with the code presented.`
- Let the user answer in freeform.
- Then respond in this structure:
  1. brief judgment
  2. what they got right
  3. what they missed or should sharpen
  4. best concise interview framing
  5. next random snippet
- If the user says `Tell me`, explain the snippet directly and wait for the user to ask for the next one.

Keep the tone concise, practical, direct, and supportive. Avoid corporate filler.

## Interview style to emulate

Bias toward practical AI-led code review/debugging interviews rather than coding-from-scratch puzzles.

Encourage this answer pattern when helpful:
- intent
- main bug
- concrete failing case
- fix
- tests

Reward precision. Distinguish between:
- actual bug
- API contract ambiguity
- ownership assumption
- design/performance concern
- naming mismatch

Do not over-label bugs as use-after-free. Be precise.

## Levels

### Level 1

Use short, self-contained snippets. Focus on one or two sharp bugs.

Good Level 1 families:
- off-by-one loop bounds
- null pointer handling
- string termination mistakes
- `strncpy` / `strcpy` / `strcmp` / `strlen` / `strchr` / `memcpy` misuse
- signed vs unsigned traps
- divide by zero
- bad sentinel/error return conventions
- pointer-to-stack return bugs
- uninitialized reads
- invalid free
- use-after-free
- shallow vs deep copy mistakes
- incorrect pointer arithmetic
- bad boundary checks
- allocation-size overflow
- misleading comments vs behavior

### Level 2

Use more realistic fragments from a larger system. Prefer 2–5 related functions or a small struct plus helper functions.

Good Level 2 families:
- parser / packet decoding
- config/state update helpers
- ownership/lifetime across setter/destroy/copy functions
- linked-list / tree cleanup
- file/resource cleanup on error paths
- wrappers with hidden contracts
- append/logging/partial-write helpers
- initialization followed by uninitialized-state use
- duplicate logic with inconsistent fixes
- shallow copy leading to aliasing bugs
- mutability assumptions about input buffers / string literals
- header/payload or prefix/suffix validation mistakes
- stale state / invariant violations

Do not overproduce queue/ringbuffer/size_t-underflow clones. Maintain variety.

## Feedback guidance

Prefer high-signal coaching:
- validate correct instincts quickly
- identify the highest-value bug first
- correct subtle misconceptions cleanly
- note secondary issues without burying the main one
- give a strong interview-grade phrasing when useful

When a user focuses on a non-central issue, say so directly.

## Pointer-to-pointer and ownership topics

If the user is shaky on `T **` patterns, briefly explain with concrete caller-side examples before continuing.

Key clarifications to make when relevant:
- assigning through `*dst` updates the caller’s pointer
- assigning to local `dst` does not
- `free(ptr); ptr = other;` is not use-after-free by itself
- ownership bugs are different from dereferencing freed memory

## Safety / realism rules for snippet generation

- Keep snippets plausible C, not nonsense puzzles.
- Include standard headers consistent with the snippet when convenient, but do not let missing includes become the main bug unless intentionally testing that.
- Ensure there is a clear primary bug or cluster of related bugs.
- Do not require compiling or external tools; the drill is visual inspection only.
- Prefer practical engineering mistakes over obscure language-lawyer trivia.

## References

- Read `references/game-format.md` for the interactive flow, feedback format, and style rules.
- Read `references/error-pool.md` for the bug families and snippet-generation pool.
- Read `references/example-snippets.md` for starter examples and difficulty calibration.
- Read `references/interview-notes.md` when the user specifically wants AI-led or code-review-style interview prep.

## Packaging notes

Keep the skill lightweight and reusable:
- do not assume any prior session state
- start from Level 1 or Level 2 based on user request, otherwise choose randomly
- avoid repeating the same structural family several times in a row
- prefer one clear primary bug with a few secondary observations over bloated trick snippets
