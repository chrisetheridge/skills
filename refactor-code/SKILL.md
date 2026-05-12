---
name: refactor-code
description: Refactor existing code without changing observable behavior. Use when the user asks to improve structure, reduce technical debt, remove code smells, split large functions/classes, reduce duplication, make code easier to test, or prepare code for a feature while preserving behavior.
---

# Refactor Code

Refactor existing code by changing structure while preserving observable behavior.

## Quick Start

1. State the behavior contract: what callers, users, tests, APIs, data, logs, errors, and side effects must observe.
2. Run or create the smallest useful safety net.
3. Make one behavior-preserving transformation.
4. Verify the change.
5. Stop when the next step becomes a feature, bug fix, rewrite, or architecture redesign.

## Core Rules

- Preserve behavior. If behavior changes, name it as a feature or bug fix, not a refactor.
- Refactor while green. If the baseline is red, identify unrelated failures before editing.
- Keep the system working after every step.
- Test through the same interface callers use. Tests coupled to private helpers are not refactor-safe.
- Separate refactoring from feature work. Small preparatory cleanup is fine; behavior changes should be their own change.
- Prefer locality over aesthetic neatness. A refactor earns its keep when future changes concentrate in fewer places.
- Do not introduce abstraction to remove duplication. Duplication is cheaper than the wrong abstraction until the shared concept is clear.
- Favor deletion when wrappers, dead branches, stale flags, obsolete tests, or speculative hooks no longer earn their keep.
- Respect project language, ADRs, local style, and nearby patterns.

## Workflow

### 1. Frame

For each refactor, state:

```text
Refactor target: Make <area> easier to <next change> by <structural move>.
Behavior to preserve: <observable contract>.
Safety net: <tests/checks/manual verification>.
Stop line: <where this becomes behavior change or redesign>.
```

If you cannot name the next change, infer it from the user request and code context. Avoid broad goals like "make it cleaner."

### 2. Explore

Read call sites before internals. Understand how the module is used.

Look for friction:

- One concept requires bouncing through many files.
- One change requires edits in many places.
- The interface is almost as complex as the implementation.
- Tests mock internals that callers never see.
- Duplication expresses the same concept in multiple places.
- Names hide domain concepts that already exist elsewhere.

Apply the deletion test: if deleting a module makes complexity vanish, it was pass-through; if complexity reappears across callers, it earned its keep.

### 3. Protect

If relevant tests exist, run the smallest set before changing code.

If tests are missing and behavior matters, add characterization tests at the public interface or nearest stable seam. Prefer integration-style tests that exercise real code paths and survive internal reshuffling.

If no useful automated safety net exists, say so and use smaller steps plus manual verification.

For legacy-code tactics, see [references/legacy-code.md](references/legacy-code.md).

### 4. Transform

Choose the least dramatic path that improves the next change:

- Clarify names, variables, types, or misleading comments.
- Compose long logic with extract or inline operations.
- Consolidate duplication after the shared concept has a name.
- Move behavior toward the data or domain concept it belongs with.
- Deepen a module by hiding repeated caller knowledge behind a smaller interface.
- Simplify data by replacing primitive obsession, long parameter lists, or parallel arrays.
- Retire dead code and speculative structure.

For smell and technique prompts, see [references/smells-and-techniques.md](references/smells-and-techniques.md).

### 5. Verify and Report

For each step:

1. Make one transformation.
2. Run the tightest relevant verification.
3. Inspect the diff for accidental behavior changes.
4. Continue while the next step has a clear reason.

Final report:

```text
Changed: <structural change>.
Verified: <tests/checks/manual verification>.
Residual risk: <meaningful remaining risk, or none>.
```

If the work exposes a larger design issue, stop and present it as a separate candidate instead of expanding scope.
