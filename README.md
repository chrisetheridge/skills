# chrisetheridge/skills

Personal skills for Pi.

## Install

Install this package from a local checkout:

```bash
pi install ./path/to/skills
```

Install it from git:

```bash
pi install git:github.com/chrisetheridge/skills
```

## Skills

### Brainstorm

Turns ambiguous requests into sufficiently settled designs without implementing them. It inspects repository context first, asks one focused question at a time, and recommends the lightest useful next step.

### ADR

Writes concise architecture decision records in the repository. Use it to record durable technical decisions, compare serious architectural options, or update/supersede an existing ADR.

### Agent Doctor

Audits a repository's agent-readiness. Use it to improve agent docs, domain context, setup guidance, issue tracker notes, and skill installation guidance.

### Code Simplify

Refactors working code for clarity without changing behavior. Use it when code has become harder to read, maintain, or extend.

### New Task

Creates a lightweight task contract for new agent work. Use it to make scope, non-goals, acceptance criteria, implementation notes, verification, and remaining risks explicit.

### Refactor Code

Refactors existing code without changing observable behavior. Use it to improve structure, reduce technical debt, split large functions, reduce duplication, or prepare code for a feature while preserving behavior.

### Setup TypeScript Pre-Commit

Sets up a standard TypeScript pre-commit workflow with:

- Biome for linting and formatting
- Husky for commit hooks
- lint-staged for staged-file checks
- type checking and tests when the repo already has scripts for them

### To Spec

Turns settled requirements, ADRs, technical decisions, architecture discussions, or brownfield refactor context into an implementation-ready engineering spec.

Use it when behaviour must be agreed before implementation, work crosses boundaries, acceptance criteria matter, or substantial technical work needs to be handed off.

## Workflow

Use the lightest process that fits:

```text
Ambiguous request → Brainstorm → ADR when warranted → Spec when useful → Implement and verify
Clear, local change → Inspect → Implement → Verify
```

Brainstorming, ADRs, and specs are composable capabilities, not mandatory lifecycle stages. A separate implementation plan is only useful when the approved spec is too large or interdependent to implement directly.
