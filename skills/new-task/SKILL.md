---
name: new-task
description: Enforce a lightweight task contract for new agent work so scope, non-goals, acceptance criteria, implementation notes, completion summary, verification, and remaining risks are explicit. Use when a user asks an agent to begin a new task with deliverables, implementation work, research work, debugging work, review work, or verification expectations; when creating a task prompt for another agent; or when delegating work to a subagent.
---

# Agent Task Contract

## Core Rule

Use a task contract when starting new agent work. Do not require the full contract for follow-up instructions inside an already-scoped task conversation unless the follow-up materially changes scope or introduces a new independent task.

Treat "new agent work" as any request that asks an agent to produce, change, investigate, verify, review, or deliver something. This applies to the current agent, a delegated subagent, and task prompts written for another thread.

## Before Starting Work

Ensure the task has:

- Scope: what work is included and what deliverable is expected.
- Non-goals: what should not be changed, solved, researched, or included.
- Acceptance criteria: observable conditions that make the task complete.

If the user did not provide one of these fields:

- Infer it silently for trivial, low-risk tasks where the intent is obvious.
- State assumptions before working when inference is useful but could be wrong.
- Ask a concise clarifying question when missing information could materially change the result.

Do not create paperwork for small obvious edits. A request like "fix the typo in README" can use an implicit contract: change only the typo, avoid unrelated edits, and complete when the typo is fixed.

## Before Writing Code

Once you have figured out the context of the task, show your approach to the user. Use the Task Format template below. Ask them to verify before making changes. The user may ask follow-up questions or ask you to make changes to your approach.

## Continuation Test

Treat a request as a continuation when the conversation already has an active task goal and the new request modifies, extends, verifies, or fixes that same work.

Examples of continuations:

- "also add tests"
- "now fix that failure"
- "do the API part next"
- "change the button copy"
- "rerun the check"

Treat a request as a new task when it introduces a separate deliverable or a materially different goal.

Examples of new tasks:

- "now create a skill for PR reviews"
- "write a separate migration plan for billing"
- "start a fresh investigation into the deploy issue"
- "make a task prompt for another agent to implement search"

## Task Format

When writing an explicit task for an agent, use this structure:

```md
## Scope

[What the agent should do, including the expected deliverable.]

## Non-Goals

[What the agent should avoid or leave unchanged.]

## Acceptance Criteria

- [Observable completion condition.]
- [Observable completion condition.]

## Implementation Notes

- [Constraints, relevant context, suggested approach, files, commands, or known risks.]

## Completion Summary

When finished, report:
- What changed or was learned.
- Verification performed, including commands, tests, checks, or review steps.
- Remaining risks, limitations, or follow-ups.
```

## During Work

Use the contract to keep work scoped. If new information shows the scope, non-goals, or acceptance criteria are wrong or incomplete, pause only when continuing would risk doing the wrong work. Otherwise, state the assumption and proceed.

When delegating to another agent, include enough context for that agent to work independently, but do not include irrelevant conversation history.

## Final Response Requirements

When the agent finishes the task, include:

- Implementation notes: concise details about important decisions, files touched, or approach.
- Completion summary: what was completed or discovered.
- Verification: tests, commands, manual checks, or review steps performed; say explicitly if verification was not run.
- Remaining risks and follow-ups: known gaps, edge cases, deferred work, or reasons no follow-up is needed.

Keep the final response proportional to the task. For tiny tasks, one short paragraph can satisfy all four requirements if it is explicit.