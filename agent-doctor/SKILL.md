---
name: agent-doctor
description: Audit a repository's agent-readiness. Use when a user wants to improve AGENTS.md, CLAUDE.md, CONTEXT.md, repo-local agent docs, domain context, issue tracker guidance, bootstrap/setup for agents, or install Matt Pocock skills for their agent harness.
metadata:
  short-description: Audit and improve repo agent-readiness
---

# Agent Doctor

Audit the current repository for agent-readiness and recommend concrete improvements.

## Workflow

1. Inspect the repo shape.
   - Find root agent docs: `AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `.windsurfrules`.
   - Find context docs: `CONTEXT.md`, `CONTEXT-MAP.md`, nested `CONTEXT.md`, nested `AGENTS.md`.
   - Find agent support docs: `docs/agents/**`, `docs/adr/**`, architecture docs, onboarding docs.
   - Find setup paths: bootstrap scripts, package scripts, setup docs, devcontainer files.
   - Find issue tracker hints: Linear, GitHub Issues, Jira, ClickUp, labels, PR conventions.

2. Read relevant docs.
   - Start with the root agent doc.
   - If `CONTEXT-MAP.md` exists, read it before individual context files.
   - Read only context files relevant to the repo structure or requested area.
   - Prefer nearby docs over broad repository-wide reading.

3. Diagnose gaps.
   - Use `references/audit-checklist.md`.
   - Separate missing information from unclear or duplicated information.
   - Treat stale or conflicting instructions as higher risk than missing optional docs.

4. Recommend changes.
   Group findings by impact:
   - `High`: an agent is likely to make wrong code changes without this.
   - `Medium`: an agent will waste time or need repeated user guidance.
   - `Low`: cleanup, consistency, or maintainability.

5. Offer implementation.
   - Do not edit files unless the user asks.
   - If asked to implement, keep changes small and repo-specific.
   - Prefer improving existing docs over adding new files.
   - Add new files only when they create a clearer routing structure.

6. Skill installation.
   - If the user wants Matt Pocock skills installed, ask which harness they use before giving commands.
   - Use `references/install-skills.md`.
   - Do not assume Codex, Claude, Cursor, Pi, or any other harness.

## Output Format

Return:

1. Current state
2. Gaps by priority
3. Recommended file changes
4. Suggested setup or bootstrap changes
5. Open questions, only where repo conventions are ambiguous

Keep recommendations specific to the repository. Avoid generic agent advice.
