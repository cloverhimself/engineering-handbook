# Code Craftsmanship

This module defines implementation-quality rules that apply across languages and frameworks. The goal is code another competent developer can understand, change, review, test, and debug without needing the original author or AI conversation.

## 1. Optimize for comprehension

Code is read and changed far more often than it is initially written.

Prefer code whose intent is obvious from names, structure, and control flow. Avoid cleverness that saves a few lines while increasing mental effort.

A reviewer should be able to answer:
- what this code does;
- why it exists;
- what inputs and outputs matter;
- what state it changes;
- what can fail;
- which business invariant it protects.

## 2. Naming

Use domain language consistently.

- Values and entities: descriptive nouns.
- Functions/actions: clear verbs.
- Booleans: conditions such as `isActive`, `hasAccess`, `canRetry`, `shouldSendReceipt`.
- Collections: plural names.
- Units should be visible when ambiguity is dangerous: `timeoutMs`, `amountMinor`, `distanceKm`.

Avoid vague names such as `data`, `info`, `thing`, `obj`, `manager`, `handler`, `process`, or `temp` when a more specific domain name exists.

Do not use different words for the same domain concept without reason.

## 3. Functions

A function should do one coherent job at one useful level of abstraction.

Prefer:
- explicit inputs and outputs;
- few hidden dependencies;
- limited mutation;
- early exits when they reduce nesting;
- pure computation separated from I/O where practical;
- orchestration functions that read like the business workflow.

A function is probably doing too much when its name needs words such as `And`, when unrelated failure modes are mixed together, or when changing one business rule repeatedly affects unrelated logic.

Do not split functions only to satisfy arbitrary line counts.

## 4. Control flow

Make the common path easy to see.

Avoid:
- deeply nested conditionals;
- long chains of boolean flags;
- hidden fallthrough;
- clever ternary nesting;
- control flow that depends on surprising side effects.

Prefer guard clauses and named predicates where they improve readability.

State machines are preferable to scattered booleans when an entity has meaningful lifecycle states.

## 5. Data structures and algorithms

Choose structures that match the operation.

Examples:
- repeated membership checks usually want a set/hash structure rather than repeated linear scans;
- keyed lookup usually wants a map/dictionary;
- ordered processing may need a queue;
- uniqueness belongs in a set or database constraint when appropriate.

Do not optimize asymptotic complexity ceremonially for tiny bounded inputs, but do not write obviously quadratic or repeated-I/O logic in paths that can grow.

Before optimizing, identify:
- input size;
- expected frequency;
- hot path or cold path;
- memory cost;
- I/O cost;
- database/network cost.

## 6. I/O is usually more expensive than syntax

Performance problems commonly come from database, network, filesystem, serialization, or repeated remote calls rather than local arithmetic.

Watch for:
- queries inside loops;
- one remote call per item when batching is available;
- reading entire files/datasets when streaming or pagination fits;
- repeatedly parsing or serializing the same data;
- holding database transactions open during slow network calls.

Measure before introducing caches, concurrency, or complex batching.

## 7. Database-aware code

Application code must respect database behavior.

- Fetch only columns/rows needed for the operation when practical.
- Bound list endpoints and batch jobs.
- Avoid N+1 query patterns.
- Use transactions for atomic invariants.
- Prefer database constraints for invariants the database can enforce safely.
- Use indexes based on actual query patterns.
- Do not move relational work into application loops when a clear database query performs it better.

## 8. Mutation and state

Make mutation obvious.

Prefer immutable values or localized mutation when the language and workload make that natural. Do not clone large structures repeatedly merely to imitate functional style when it materially hurts performance.

Shared mutable state requires stronger reasoning, especially under concurrency.

## 9. Errors

Errors should preserve useful meaning.

- Do not swallow failures.
- Do not convert every failure to a generic message internally.
- Add context at meaningful boundaries.
- Avoid catching exceptions/errors only to rethrow the same thing without value.
- Keep expected domain failures distinguishable from unexpected programmer/system failures.
- Do not use exceptions for ordinary branching when the language/ecosystem provides a clearer conventional mechanism.

## 10. Comments

Comments should explain non-obvious **why**, constraints, external requirements, or dangerous assumptions.

Do not narrate obvious code.

Prefer:

`// Provider may deliver this webhook more than once, so reference uniqueness is required.`

instead of:

`// Check if reference exists.`

Delete stale comments when behavior changes.

## 11. Public interfaces

Keep public APIs/modules smaller and more stable than internal implementation.

Do not expose implementation details that force callers to understand internals.

Prefer explicit contracts and predictable behavior over flexible APIs with many optional flags.

## 12. Duplication vs abstraction

Do not abstract merely because two blocks look similar.

Extract when they represent the same stable concept and should change together.

A little duplication is often safer than an incorrect shared abstraction that couples unrelated domains.

## 13. Efficiency without premature optimization

Prefer the simplest implementation that meets the known workload.

Optimize when:
- profiling identifies a bottleneck;
- capacity estimates show a real risk;
- an obviously inefficient pattern sits on a large/hot path;
- latency, memory, CPU, I/O, or cost targets require it.

When optimizing, document the reason if the resulting code becomes less obvious.

## 14. Resource discipline

Release resources according to the language/runtime conventions.

Examples include:
- database connections;
- file handles;
- streams;
- locks;
- goroutines/tasks/threads;
- subscriptions/listeners;
- timers.

Avoid leaked background work and unbounded concurrency.

## 15. Tests and changeability

Write code so important behavior can be tested without reproducing the entire production environment.

Do not distort production architecture only to satisfy tests, but isolate true external boundaries where doing so improves reliability and changeability.

Test observable behavior and invariants rather than private implementation details.

## 16. Review standard

Before completion, ask:

- Can another developer find the main workflow quickly?
- Are names based on domain meaning?
- Is any function/module mixing unrelated responsibilities?
- Is there avoidable repeated I/O or database work?
- Are collections and algorithms appropriate for expected size?
- Is mutation obvious?
- Are errors meaningful?
- Are edge cases plausible rather than imaginary?
- Does the code follow the language's normal idioms?
- Would a maintainer know where to make the next change?

Clarity, correctness, and appropriate efficiency matter more than brevity.