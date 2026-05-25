---
name: adr
description: Write and maintain concise Architecture Decision Records that capture durable technical decisions in the repository. Use when the user asks for an ADR, architecture decision record, decision log, to record a technical decision, to compare architectural options, or to update/supersede an existing decision.
metadata:
  short-description: Write concise architecture decision records
---

# ADR

Write decision records that preserve why a technical choice was made, what was decided, and what future agents must respect.

## Core Rules

- Record decisions, not essays. Keep ADRs short unless the decision has real complexity.
- Put ADRs in the repository, reviewed like code. Prefer the existing ADR directory:
  - `docs/adr/`
  - `docs/adrs/`
  - `docs/work/decisions/`
- Do not put durable ADRs under `docs/superpowers/`, `.pi/`, `.codex/`, or other agent scratch folders.
- Match the repo's existing numbering, filename style, status names, and section headings.
- Prefer one decision per ADR. Split unrelated choices.
- Include non-goals when the boundary matters.
- Preserve the user's direct, implementation-oriented style. Avoid motivational or tutorial prose.

## Workflow

1. Find the local convention.
   - Read `AGENTS.md`, `CONTEXT.md`, `CONTEXT-MAP.md`, and existing ADRs if present.
   - Identify whether ADRs are global or domain-specific.
   - If no ADR convention exists, use `docs/adr/NNNN-kebab-title.md`.

2. Understand the decision.
   - Inspect relevant code and docs before drafting.
   - Distinguish accepted facts from open questions.
   - Ask only blocking questions. If a reasonable assumption is safe, state it in the ADR context or consequences.

3. Draft the ADR.
   Use the repo's existing template. If none exists, use:

   ```md
   # ADR NNNN: <Decision title>

   ## Status

   Proposed or Accepted

   ## Context

   <Current state, forces, constraints, and why a decision is needed.>

   ## Decision

   <The chosen path. Be specific about ownership, boundaries, APIs, data, deployment, or workflow rules.>

   ## Non-Goals

   <What this decision intentionally does not do. Omit if not useful.>

   ## Consequences

   - <Positive or neutral consequence.>
   - <Tradeoff, risk, migration cost, or follow-up decision.>
   ```

4. Include alternatives when useful.
   - Add `## Alternatives considered` only when options were seriously evaluated or the rejected path will be tempting later.
   - Keep each alternative to why it was rejected, not a full design.

5. Connect the ADR to execution.
   - Update `CONTEXT.md`, `CONTEXT-MAP.md`, `AGENTS.md`, architecture docs, or specs only when they need to route future agents to the decision.
   - If an ADR changes a previous decision, mark the old ADR as `Superseded` or add a clear supersession note, following local style.

6. Self-review before finishing.
   - Does the title say the decision, not the topic?
   - Can a future agent tell what code boundaries or behavior must be preserved?
   - Are rejected options and non-goals clear enough to prevent repeat debate?
   - Are consequences honest about tradeoffs?
   - Is the ADR shorter than the design discussion that produced it?

## Style

- Use concrete nouns from the codebase: package names, commands, protocols, schemas, directories, and domain terms.
- Write in present tense for accepted decisions.
- Avoid vague claims like "better", "more scalable", or "cleaner" unless tied to a specific constraint.
- Prefer bullets in consequences and alternatives.
- Include small code or command snippets only when they define the decision.

## Status Names

Follow local convention first. Common statuses:

- `Proposed`: drafted but not accepted.
- `Accepted` or `Approved`: the decision is active.
- `Superseded`: replaced by a later ADR.
- `Rejected`: recorded but not adopted.

## When Not To Write An ADR

- The change is an obvious implementation detail.
- The decision can be captured as a short comment in a spec or task.
- The code is a throwaway prototype.
- The choice is still exploratory and no durable decision exists yet.
