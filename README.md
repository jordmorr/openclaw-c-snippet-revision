# c-snippet-revision

`c-snippet-revision` is an installable skill for interactive C interview practice through visual code inspection.

It runs a one-at-a-time revision game built around short bug-spotting snippets and larger system-style code fragments. The emphasis is on reasoning clearly about correctness, ownership, boundaries, failure paths, and engineering judgment rather than compiling and running code.

## What it does

- presents exactly one C snippet at a time
- supports two difficulty levels:
  - **Level 1**: short, self-contained bug-spotting snippets
  - **Level 2**: larger multi-function or system-style fragments
- gives concise, interview-oriented feedback
- helps sharpen spoken debugging explanations
- supports practical code-review style interview prep

## Use cases

Use this skill when you want to:

- practice C debugging by visual inspection only
- rehearse code-review interview questions
- improve bug-spotting speed and precision
- train on ownership, memory safety, bounds, and error-path issues
- get one-snippet-at-a-time interactive feedback instead of bulk problem dumps

## How the revision loop works

1. get shown one snippet
2. get asked: `Tell me what’s wrong with the code presented.`
3. allowed to answer in freeform
4. feedback given on:
   - what you got right
   - what you missed
   - how to phrase the answer more sharply
5. move to the next snippet

## Skill contents

```text
c-snippet-revision/
├── SKILL.md
├── README.md
├── references/
│   ├── error-pool.md
│   ├── example-snippets.md
│   ├── game-format.md
│   └── interview-notes.md
└── dist/
    └── c-snippet-revision.skill
```

## Installation

Package the skill using the OpenClaw skill packaging tooling, then install the resulting `.skill` file using your usual skill installation flow.

Packaged artifact:

```text
/home/pi/c-snippet-revision/dist/c-snippet-revision.skill
```

## Development notes

This repository contains the source skill directory as well as the packaged `.skill` artifact.

If you edit the skill, repackage it with the skill creator.

## Design goals

- practical, realistic C bugs rather than puzzle trivia
- concise, high-signal feedback
- strong variety across snippet families
- reusable from a cold start without depending on prior chat history
- good support for both ownership-heavy and boundary-heavy debugging problems

## License

Add your preferred license here before publishing.
