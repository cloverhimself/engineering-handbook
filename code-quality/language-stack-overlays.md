# Language and Stack Overlays

The handbook contains universal engineering rules, but code should still look natural in the language and framework being used.

An AI agent must not force TypeScript patterns into Go, Java patterns into Python, or framework-independent abstractions into a framework that already provides a conventional solution.

## Selection rule

At project setup, identify:

- language(s);
- runtime;
- framework(s);
- database/ORM/query layer;
- test framework;
- formatter/linter/static-analysis tools;
- package manager/build tool;
- deployment/runtime constraints.

Record the stack in `docs/project-design.md` and root `AGENTS.md`.

Then follow:

1. the universal handbook rules;
2. official language/framework conventions;
3. repository-established conventions;
4. only then custom project preferences.

If these conflict, prefer correctness and the ecosystem's established conventions unless the project has a documented reason to differ.

## General language-aware rules

### Type systems

Use the type system to make invalid states harder to represent, but do not create elaborate type machinery that makes ordinary changes difficult.

Strong/static typing languages:
- prefer precise domain types where they reduce ambiguity;
- avoid excessive `any`, unsafe casts, unchecked nulls, or equivalent escape hatches;
- let the compiler prove what it can instead of duplicating checks everywhere.

Dynamic languages:
- use clear contracts, validation at boundaries, tests, type hints/annotations where conventional, and small cohesive units to preserve reasoning.

### Error model

Follow the language's normal error style.

Examples:
- exceptions where exceptions are conventional;
- explicit returned errors where that is conventional;
- result/option types where idiomatic.

Do not invent a cross-language error abstraction merely to make every stack look identical.

### Concurrency model

Respect the runtime's model:
- event loop / async-await;
- threads;
- goroutines/channels;
- async tasks/futures;
- actors or other framework models.

Do not block an event loop with avoidable synchronous work. Do not create unbounded threads/tasks/goroutines. Use concurrency because the workload benefits, not because syntax makes it easy.

### Memory and allocation

In garbage-collected environments, avoid needless large allocations in hot paths but do not micro-manage memory prematurely.

In ownership/manual-memory environments, follow the language's safety/resource conventions carefully and prefer clear ownership over clever lifetime/aliasing tricks.

## Common stack examples

These are directional, not exhaustive.

### JavaScript / TypeScript

- Prefer `const` by default; use mutation intentionally.
- TypeScript should model domain contracts rather than silence errors with casts.
- Avoid `any` unless there is a justified boundary and narrow it quickly.
- Distinguish `null`/`undefined` deliberately according to project conventions.
- Use async/await consistently for asynchronous flows.
- Avoid sequential awaits inside loops when operations are independent and safe to batch/concurrently execute.
- Do not use uncontrolled `Promise.all` for huge inputs; bound concurrency where necessary.
- Use the framework's standard validation, routing, rendering, and data-loading patterns.
- Prefer ecosystem-standard formatter/linter/typecheck tooling.

### Python

- Follow normal Python naming and readability conventions.
- Use type hints where they improve contracts and tooling, especially in non-trivial applications.
- Prefer comprehensions when simple; use normal loops when they are clearer.
- Be conscious of blocking I/O in async applications.
- Use context managers for resource lifetime.
- Do not use metaprogramming or decorators merely to hide straightforward control flow.

### Go

- Prefer simple explicit code and small interfaces defined near their consumers.
- Handle returned errors intentionally; add context where useful without wrapping meaninglessly.
- Avoid unnecessary abstraction layers and Java-style class architecture.
- Keep goroutine lifetime and cancellation explicit.
- Use contexts for request-scoped cancellation/deadlines where conventional.
- Do not start goroutines without a clear ownership/termination strategy.

### Java / Kotlin

- Use the framework's dependency injection and lifecycle mechanisms when they are already standard; do not add parallel custom infrastructure.
- Prefer composition and focused services over large inheritance hierarchies.
- Keep DTO/domain/persistence separation proportionate to application complexity.
- Use nullability/type features rather than repetitive defensive checks when guarantees are trustworthy.
- Be conscious of thread pools, blocking I/O, and transaction boundaries.

### Rust

- Use ownership and borrowing to make resource/lifetime rules explicit without fighting the compiler through unnecessary cloning.
- Prefer expressive `Result`/`Option` handling over panics for expected failures.
- Reserve `unwrap`/`expect` for states whose invariant is genuinely established or for appropriately scoped tooling/tests.
- Avoid excessive cloning in hot paths when borrowing or ownership transfer is clearer.
- Keep unsafe code minimal, isolated, and justified.

### SQL

SQL is part of the application, not an implementation detail to ignore.

- Make queries deterministic where ordering matters.
- Avoid `SELECT *` in stable performance-sensitive paths when explicit columns are practical.
- Understand joins and cardinality.
- Use set-based operations rather than application loops when clearer and more efficient.
- Inspect query plans for important slow queries.
- Parameterize user input.

## Framework awareness

Before introducing a custom pattern, ask whether the framework already has a standard place for the concern.

Examples:
- routing;
- middleware/interceptors;
- validation;
- dependency injection;
- configuration;
- database transactions;
- auth/session handling;
- background jobs;
- error boundaries/handlers;
- lifecycle hooks.

Prefer framework-native mechanisms when they are production-proven and fit the requirement.

## Repository consistency

When entering an existing codebase, inspect nearby representative files before writing new code.

Match established conventions for:
- naming;
- file placement;
- import organization;
- error handling;
- testing;
- API responses;
- database access;
- logging.

Do not mechanically preserve a local convention that is clearly unsafe or broken; document the reason before changing it.

## Agent rule

The agent should never say "clean code requires X" when X is merely a convention from another language or framework.

Universal principles should remain universal; implementation style should be native to the selected stack.