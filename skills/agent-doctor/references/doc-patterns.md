# Doc Patterns

## Root Agent Doc

Use a root `AGENTS.md` or equivalent to orient agents.

Good contents:

- repo purpose
- major apps or packages
- setup commands
- test commands
- lint and formatting commands
- completion expectations
- important boundaries
- links to deeper context docs

Keep root docs short. Route to deeper docs instead of explaining every domain at the root.

## Context Map

Use `CONTEXT-MAP.md` when the repo has multiple domains, products, packages, or services.

Suggested shape:

```markdown
# Context Map

Read the context that matches the area you are changing before exploring code.

| Context | Path | Use when |
| ------- | ---- | -------- |
| Billing | `apps/billing/CONTEXT.md` | Working on invoices, subscriptions, plans, payment flows, or billing jobs. |
| Admin | `apps/admin/CONTEXT.md` | Working on internal admin screens, user management, permissions, or support workflows. |

Also read the nearest `AGENTS.md` for local coding rules.
```

## Domain Context

Use local `CONTEXT.md` files to teach agents the domain language and boundaries.

Suggested sections:

```markdown
# <Domain> Context

## Scope

What this area owns.

## Core Language

Important terms and definitions.

## Responsibilities

What each major package, app, module, or service owns.

## Product Areas

Major directories, modules, or workflows.

## Data Flow

How data moves through this area.

## Authorization and Ownership

Access rules, tenancy rules, or ownership boundaries.

## Implementation Rules

Repo-specific rules agents must follow.

## Architectural Rules

Layering, dependency direction, data ownership, adapter boundaries, or other design constraints that must be preserved.

## Verification Commands

Commands agents should run after changing this area.

## Boundaries

What not to copy, inspect, or change without approval.
```

Prefer concrete bullets over narrative. Good `CONTEXT.md` files should preserve the repo's terms of art and "do not violate this" rules, not just summarize what the code does.

## Agent Support Docs

Use `docs/agents/` for workflow conventions that apply to agents but are not domain context.

Useful files:

- `docs/agents/issue-tracker.md`
- `docs/agents/triage-labels.md`
- `docs/agents/domain.md`
- `docs/agents/review.md`
- `docs/agents/bootstrap.md`

## Issue Tracker Doc

Suggested shape:

```markdown
# Issue Tracker

Issues for this repo live in <tracker>.

## Conventions

- Team or project:
- Labels:
- GitHub Issues usage:
- Agent issue creation policy:
- Branch, commit, and PR linking:

## When a skill says "publish to the issue tracker"

Create an issue only if the user explicitly requested issue creation. Otherwise, draft the issue content and ask for confirmation.
```

## Triage Labels Doc

Suggested shape:

```markdown
# Triage Labels

| Label | Meaning |
| ----- | ------- |
| `needs-triage` | Maintainer needs to evaluate this issue |
| `needs-info` | Waiting on reporter for more information |
| `ready-for-agent` | Fully specified, ready for agent-assisted work |
| `ready-for-human` | Requires human implementation |
| `wontfix` | Will not be actioned |
```
