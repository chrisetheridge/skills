# Legacy Code

Legacy refactoring starts by making behavior observable before making structure better.

## Missing Tests

Use characterization tests when:

- The code is hard to understand.
- The behavior is business-critical.
- You need to preserve current behavior, including odd edge cases.
- Existing tests are too coupled to internals to protect a refactor.

Write characterization tests at the public interface or nearest stable seam. Capture current behavior before judging whether to keep it.

## Finding Seams

A seam lets you vary behavior without editing the code at that place.

Look for seams at:

- Public functions, classes, commands, endpoints, or handlers.
- Constructor parameters or dependency injection points.
- Filesystem, network, database, queue, clock, random, environment, or process boundaries.
- Serialization/deserialization edges.
- Existing adapters or test doubles.

Do not introduce a seam for test convenience. A seam should clarify behavior or isolate real variation.

## Safe Legacy Loop

1. Identify the behavior that must not change.
2. Add or find a characterization test around that behavior.
3. Break the smallest dependency needed to observe it.
4. Make one refactoring step.
5. Re-run the characterization test and relevant checks.
6. Remove obsolete tests once stronger public-interface tests cover the behavior.

## High-Risk Areas

Slow down around:

- Migrations, persisted data, and serialization formats.
- Public APIs and client contracts.
- Security, auth, billing, and permissions.
- Concurrency, ordering, retries, idempotency, and time.
- Performance-sensitive hot paths.
- Error messages or logs used by operators or external systems.

If you cannot protect behavior well enough, report the risk before changing the code.

## Source Influences

- Michael Feathers: seams and characterization tests.
- Martin Fowler: small behavior-preserving transformations and keeping the system working.
- Local project principles: tests through public interfaces, locality, leverage, and separate refactors from behavior changes.
