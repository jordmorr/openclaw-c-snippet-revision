# Error Pool

Use these families to generate a broad mix of snippets.

## Level 1

- off-by-one loop conditions
- string termination mistakes
- copy-size bugs
- destination-capacity vs source-length mismatch
- unchecked `strchr` / delimiter search failure
- unchecked `malloc` / `realloc`
- invalid free
- use-after-free
- returning pointer to local storage
- null pointer handling
- uninitialized heap or stack reads
- signed/unsigned comparisons
- modulo / division by zero
- bad sentinel/error conventions
- allocation-size overflow before malloc
- index arithmetic overflow
- hidden assumptions about valid digits / valid strings / valid lengths
- `memcmp` vs `strncmp` semantic mismatch
- copying raw bytes when string semantics were intended

## Level 2

- copy / clone functions with shallow-copy failure semantics
- setter/destroy ownership mismatches
- borrowed-view vs owning-buffer confusion
- helper function contract mismatch across multiple functions
- cleanup-path leaks
- partial initialization left behind on error
- linked list / tree cleanup order bugs
- parser functions that validate the wrong length field
- aliasing / lifetime hazards across returned pointers
- resource wrappers that free caller-owned inputs
- stale or inconsistent state after realloc/copy failure
- duplicate logic with one branch fixed and another not
- performance/design issues only when they are realistic and not the sole point

## Generation rules

- keep snippets plausible and readable
- avoid repeating queue/ringbuffer examples too often
- vary between memory safety, ownership, validation, API design, and partial failure cases
- prefer snippets where a strong engineer would reason verbally rather than compile
