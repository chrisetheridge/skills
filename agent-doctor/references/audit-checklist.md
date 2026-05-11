# Audit Checklist

## Root Orientation

Check whether the repo tells agents:

- what the repo is
- primary languages, apps, packages, and runtimes
- how to install dependencies
- how to run tests
- how to run lint, typecheck, or formatting
- how to start local services
- how to complete work
- what requires human approval
- what areas are risky or legacy
- how to handle generated files

## Context Routing

Look for:

- a root `CONTEXT-MAP.md` when the repo has multiple domains, apps, packages, or bounded contexts
- domain-specific `CONTEXT.md` files near the relevant code
- clear "use when" routing
- glossary terms agents should preserve
- boundaries between legacy and current systems
- warnings about code that should not be copied into new areas
- links to architecture decisions

Good context routing helps agents read the right small set of docs before editing.

## Agent Docs

Check whether `docs/agents/` or an equivalent location explains:

- issue tracker conventions
- triage labels
- PR and review workflow
- branch naming conventions
- architecture decision records
- domain docs layout
- local agent tools
- repo-specific skills
- release or deployment constraints

Agent docs should describe workflow conventions that do not belong in product docs or code comments.

## Issue Tracker

Check whether the repo says:

- which tracker is authoritative
- which tracker is unused
- which labels represent triage states
- whether agents may create issues directly
- how issue IDs should appear in branches, commits, or PRs
- when to draft an issue instead of creating one

Flag ambiguity when multiple trackers appear active.

## Skill Setup

Check whether setup docs or bootstrap scripts install useful skills.

Do not assume a specific harness. Ask first.

Prefer adding installation to an existing bootstrap path when the repo already has one.

Avoid vendoring unrelated global skills into the repo unless the repo intentionally maintains local skills.

## Cleanup

Flag:

- stale agent instructions
- duplicate instructions across files
- giant root context files
- tool names from another harness without explanation
- unclear issue tracker ownership
- missing domain boundaries
- vague glossary terms
- instructions that conflict with current repo structure
- local docs that describe behavior no longer present in code

## Suggested Priority

Use `High` when the gap can cause wrong edits.

Use `Medium` when the gap causes wasted exploration, repeated questions, or inconsistent workflow.

Use `Low` when the gap is mainly polish, discoverability, or cleanup.
