---
name: brainstorm
description: Use when a request is ambiguous, requirements or non-goals are unclear, several valid designs exist, or product and technical decisions need exploration before implementation.
---

# Brainstorm

Turn an unclear request into a sufficiently settled design. This is a temporary discovery mode, not a required development lifecycle.

## Rules

- Do not implement while brainstorming.
- Inspect relevant code, tests, documentation, configuration, and similar features before asking questions.
- Do not ask questions whose answers can be discovered from the repository.
- Ask one focused question per turn. Process the answer before choosing the next question.
- Challenge assumptions and explain material trade-offs.
- Keep the human in control of product and architectural decisions.
- Distinguish repository facts, confirmed decisions, assumptions, and open questions.
- Do not force an ADR, spec, or plan when direct implementation is appropriate.

## Process

1. Establish repository context and existing constraints.
2. Identify the uncertainty most likely to change the design.
3. Ask one focused question about it.
4. Repeat until remaining uncertainty would not materially change the design.
5. Summarize the result and recommend the lightest useful next step.

Explore only relevant concerns, such as:

- goals, non-goals, and expected behaviour
- ownership and interface boundaries
- failure modes and recovery
- security and privacy
- compatibility, migration, and rollout
- operational constraints and observability

## Completion Summary

Include:

- Problem
- Goals and non-goals
- Constraints
- Proposed approach
- Alternatives considered
- Important edge cases
- Confirmed decisions
- Assumptions
- Open questions

Recommend exactly one next step:

| Outcome | Next step |
| --- | --- |
| Clear, local, low-risk change | Implement directly |
| Behaviour must be agreed or handed off | Create a spec |
| Durable, costly-to-reverse technical choice | Create an ADR |
| Durable decision plus substantial behavioural change | Create an ADR, then a spec |

## Example

Request: "Let users delete their organisation."

After inspecting ownership, deletion, and retention code, ask the single most consequential unresolved question, such as: "Should deletion be immediately permanent, or recoverable for a retention period?" Do not send a questionnaire or begin implementation.

## Common Mistakes

- Asking a generic questionnaire instead of one consequential question.
- Asking the user about behaviour already established in code or tests.
- Treating an assumption as a decision.
- Continuing discovery after the design is sufficiently clear.
- Automatically routing every result through ADR, spec, and plan.
