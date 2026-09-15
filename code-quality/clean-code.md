# Code Quality and Maintainability

These rules apply to implementation work across project types. The goal is code that ordinary software engineers can read, change, test, and review without needing the original author or AI session.

## Core rule

Prefer clarity over cleverness.

Readable code is a scalability feature: teams, codebases, and products change more often than they are initially written.

## Naming

Use names that communicate intent.

Good names answer what something represents or does without forcing the reader to inspect the implementation.

Prefer:

```ts
const activeSubscription = ...
const paymentReference = ...
const isOrderExpired = ...
const calculateOrderTotal = () => ...
```

Avoid:

```ts
const x = ...
const data2 = ...
const temp = ...
const handle = ...
const process = ...
```

unless the surrounding scope makes the meaning genuinely obvious.

Use nouns for values and domain objects. Use verbs for actions and functions. Boolean names should usually read like conditions: `isActive`, `hasPermission`, `canRetry`, `shouldNotify`.

Do not encode type information into names when the language already provides it. Avoid noisy prefixes and unnecessary abbreviations.

## Functions

Functions should have one clear responsibility and operate at a consistent level of abstraction.

Prefer small, cohesive functions, but do not split logic mechanically just to satisfy a line-count target. A long function is a review signal, not an automatic defect.

Extract logic when doing so improves at least one of:
- naming of an idea;
- reuse;
- testability;
- reduction of nesting;
- separation of side effects from pure logic;
- readability of the main workflow.

Avoid functions that simultaneously validate input, perform persistence, call third-party services, transform output, emit notifications, and write audit logs without orchestration boundaries.

Use early returns to reduce nesting when they improve clarity.

Avoid hidden mutation and surprising side effects.

## Files and modules

A file should have one primary responsibility or cohesive domain purpose.

Do not create `god` files that accumulate unrelated routes, helpers, models, services, constants, and business logic.

Do not split files solely because they cross an arbitrary number of lines. Split when responsibilities, ownership, or reasons to change diverge.

Prefer domain or feature grouping as systems grow. Generic folders such as `utils/`, `helpers/`, and `common/` should not become dumping grounds.

Shared code must be genuinely shared and stable enough to justify a shared location.

## Syntax and semantics

Use the language's conventional syntax and idioms.

Prefer straightforward control flow over compressed expressions that reduce readability.

Avoid deeply nested ternaries, dense one-liners, implicit coercion, and overly clever metaprogramming unless they are standard practice in the language/framework and materially improve the solution.

Write code whose structure mirrors the domain problem.

Do not optimize for fewer lines of code. Optimize for easier comprehension and correct change.

## Formatting

Use the ecosystem-standard formatter and linter where practical.

Formatting should be automated and consistent. Do not spend engineering effort debating whitespace that tooling can decide.

Repository formatting rules should be checked in and reproducible.

## Constants and magic values

Avoid unexplained literals for business rules or infrastructure values.

Prefer named constants or configuration for values with domain meaning, for example:

```ts
const MAX_LOGIN_ATTEMPTS = 5;
const PENDING_ORDER_TTL_MINUTES = 30;
```

Do not move every literal into a constant merely for ceremony.

## Comments and documentation

Prefer code that explains itself through naming and structure.

Comments should explain **why**, constraints, non-obvious tradeoffs, external requirements, or dangerous edge cases. Avoid comments that simply restate the code.

Public APIs and complex domain logic should have concise documentation where it materially improves correct use.

Remove stale comments when code changes.

## Error handling

Do not swallow errors silently.

Use domain-appropriate error types or error codes when callers need to distinguish failure classes.

Do not expose internal stack traces, secrets, or sensitive implementation details to clients.

Logs should contain enough context to investigate failures without leaking protected data.

Handle errors at the boundary where there is enough context to make a meaningful decision.

## Dependencies

Use the standard library or existing project dependencies when they solve the problem cleanly.

Do not add a package for trivial behavior that can be implemented clearly and safely in a few lines.

Do not reimplement complex security, cryptography, parsing, or protocol behavior that established libraries already provide.

Every dependency increases maintenance, upgrade, security, and supply-chain surface area.

## Complexity

Avoid premature abstraction.

Duplication is sometimes cheaper than the wrong abstraction. Extract when the common concept is stable and genuinely shared.

Prefer composition over deep inheritance hierarchies unless the framework strongly expects inheritance.

Avoid unnecessary generic layers, factories, registries, interfaces, adapters, and base classes that exist only to appear architectural.

## Change discipline

Keep structural refactors and behavioral changes separate when practical. This makes review and debugging easier.

Prefer small, focused changes over giant unrelated rewrites.

Preserve public behavior during refactors unless a behavior change is explicitly intended and tested.

## Performance

Write clear code first, then optimize measured bottlenecks.

Avoid obviously wasteful work in hot paths, such as repeated database queries inside loops, loading unbounded datasets, unnecessary serialization, or repeated remote calls.

Use batching, pagination, indexes, caching, streaming, or concurrency only when the workload justifies them.

Performance improvements must not silently weaken correctness or consistency guarantees.

## Review questions

Before considering implementation complete, ask:

- Can another developer understand the main flow without tracing every helper?
- Do names express domain intent?
- Are functions cohesive?
- Are modules separated by meaningful responsibilities?
- Is nesting reasonable?
- Are side effects explicit?
- Are business rules centralized enough to stay consistent?
- Are errors observable and useful?
- Is there unnecessary abstraction or duplication?
- Are hot-path queries and loops bounded?
- Does the implementation follow the project's framework conventions?
- Would a normal engineer consider this unsurprising code?
