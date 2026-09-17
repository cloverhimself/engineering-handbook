# Engineering Constitution for AI Agents

These rules apply to all software work unless the project explicitly overrides a rule in writing.

## 1. Mission

Build the simplest conventional solution that correctly satisfies the current requirements, lifecycle stage, risk level, deployment environment, and required system properties while leaving a reasonable path for future change.

Do not equate more technology with better engineering. Do not add infrastructure, packages, abstractions, services, caches, queues, event buses, databases, or frameworks unless a concrete requirement justifies them.

Simplicity must not sacrifice correctness, durability, security, deployment compatibility, operability, or an explicitly required product property.

## 2. Mandatory pre-implementation process

Before substantial implementation:
1. Read the project requirements and existing codebase.
2. Read `templates/project-design.md` and complete the relevant sections in the project documentation.
3. Select the relevant profile(s) from `profiles/` and record why they apply.
4. Select the current lifecycle stage using `lifecycle/stages.md`, record why it applies, and note which stricter controls are required by domain risk.
5. Read `code-quality/clean-code.md`, `code-quality/project-structure.md`, and `workflow/technology-selection.md` when technology/provider choices are not already settled.
6. Identify functional requirements, non-functional requirements, expected scale, trust boundaries, persistence/durability needs, external dependencies, deployment constraints, and budget constraints.
7. Verify relevant platform/runtime constraints from actual documentation/environment evidence. Do not convert scaffold conventions into imaginary hard platform limits.
8. Inspect existing project conventions and follow them unless there is a strong reason not to.
9. Audit scaffold/default dependencies and configuration rather than assuming they are required.
10. State important assumptions. Do not silently invent business rules.
11. For major choices, compare at least one simpler alternative and document why the chosen option is appropriate.

Do not begin by generating large amounts of code.

## 3. Lifecycle calibration

Engineering rigor must match both lifecycle stage and domain risk.

Stages:
- experiment/spike;
- prototype;
- MVP;
- production/growth;
- high-scale/high-criticality.

Use `lifecycle/stages.md` as the source of truth.

Do not apply high-scale infrastructure by default to an MVP. Do not carry prototype shortcuts into production without an explicit review.

Risk can override stage. Money movement, authentication, sensitive data, destructive operations, irreversible state transitions, and compliance-sensitive workflows may require stricter controls even in an MVP or prototype.

A lifecycle-stage change requires updates to `docs/project-design.md`, `docs/PHASES.md`, and `docs/CONTEXT.md`, plus a gap review. Do not rewrite the application merely because the stage label changes.

## 4. Conventional engineering first

Prefer:
- standard library and framework-native capabilities;
- established, widely maintained packages;
- relational databases for relational transactional data;
- normal HTTP/REST semantics unless another protocol is justified;
- explicit schemas, constraints, migrations, indexes, transactions, and foreign keys;
- straightforward control flow over clever metaprogramming;
- modular monoliths before microservices for ordinary products;
- synchronous workflows before asynchronous workflows unless latency, reliability, or workload characteristics require background processing.

Avoid novelty for novelty's sake.

## 5. Technology, provider, and build-vs-buy choices

Follow `workflow/technology-selection.md`.

Choose the required capability/system property before choosing a vendor. Example: decide that the product needs durable managed PostgreSQL before deciding between Supabase, Neon, Railway, Cloud SQL, RDS, or another provider.

Do not treat a provider selected for convenience as a permanent architecture requirement without documenting why.

PostgreSQL does not imply an ORM. Choose raw parameterized SQL, a query builder, or an ORM based on query complexity, team conventions, type/migration needs, and actual value.

For auth, storage, email, database hosting, payments, monitoring, and similar capabilities, compare build-vs-buy based on security, operational burden, cost, lock-in, lifecycle stage, and deployment fit.

Numeric limits, pool sizes, timeouts, concurrency assumptions, and scaling thresholds must come from requirements, provider constraints, measurements, or be clearly labeled provisional defaults.

## 6. Architecture

Architecture must follow requirements rather than trends.

Default starting point for a typical web product:
client -> application/API -> relational database

Add components only when justified:
- CDN for static/global delivery needs;
- object storage for files;
- cache for demonstrated hot reads or distributed coordination needs;
- queue/workers for slow, retryable, bursty, or asynchronous work;
- read replicas for demonstrated read pressure;
- search engine when database search is measurably insufficient;
- microservices when independent ownership/deployment/scaling boundaries justify their operational cost.

Record major architecture decisions with an ADR.

## 7. Code quality and semantics

Implementation must optimize for clarity, correctness, maintainability, and unsurprising behavior.

Follow `code-quality/clean-code.md` and `code-quality/code-craftsmanship.md`.

Use meaningful names, cohesive functions, low nesting, explicit side effects, framework-standard syntax, consistent formatting, and clear error handling.

Do not optimize for fewer lines. Do not compress logic into clever one-liners when readability suffers.

Long functions and files are review signals, not automatic failures. Split code when responsibilities or reasons to change diverge. A simple codebase can still be well-structured; avoiding overengineering does not justify god files.

Avoid god objects/files, magic business values, stale comments, hidden mutation, silent error swallowing, deep inheritance, unnecessary `any`/unchecked type escapes, and abstractions that exist only to appear sophisticated.

Prefer small focused changes. Separate structural refactors from behavior changes when practical.

## 8. Project and file structure

Use the conventional structure of the selected framework first and follow `code-quality/project-structure.md`.

A file/module should have one coherent responsibility. Split by responsibility and domain, not arbitrary line counts.

Avoid dumping unrelated code into `utils`, `helpers`, `common`, or `services`.

Prefer feature/domain grouping once a codebase becomes non-trivial. Keep cross-domain shared code genuinely generic.

Do not create interfaces, factories, repositories, adapters, base classes, or dependency injection layers merely because they sound architectural. Introduce them when they isolate a real boundary or materially improve testability/changeability.

## 9. Database and persistence

Treat the database as part of the integrity model, not just storage.

Before selecting persistence, verify deployment durability. An ephemeral filesystem is not durable application storage.

Use:
- primary keys;
- foreign keys where relationships require integrity;
- NOT NULL where absence is invalid;
- UNIQUE constraints for true uniqueness invariants;
- constrained/enumerated values when the domain has a fixed valid state set;
- CHECK constraints for simple enforceable invariants;
- explicit delete/referential behavior;
- transactions for multi-step state changes that must be atomic;
- indexes based on real query patterns;
- explicit migrations committed to source control.

If application logic assumes a property such as uniqueness or an allowed state set, enforce it in the database when safe and practical.

Review tenant boundaries across the full parent-resource chain. A child ID alone must not bypass authorization to its owning tenant/parent.

Do not use application code as the only enforcement mechanism for invariants that the database can safely enforce.

Avoid N+1 queries, unbounded reads, accidental full-table scans, and pagination without deterministic ordering.

Define semantics for structured temporal values. A calendar date, local date-time, UTC timestamp, and duration are different concepts; do not let accidental JavaScript/date-library conversion choose the business rule.

## 10. Scale and capacity

Never design from total registered users alone.

Consider:
- daily/monthly active users;
- peak concurrent users;
- requests per second at average and peak;
- read/write ratio;
- request payload sizes;
- file/media bandwidth;
- database row growth;
- retention period;
- background job volume;
- geographic distribution;
- latency targets;
- availability requirements.

Use rough capacity estimates before adding scaling infrastructure. Prefer horizontal stateless application scaling where appropriate. Define specific triggers for introducing new infrastructure, but avoid invented precision.

## 11. Security

Security is a design requirement.

At minimum:
- validate input at trust boundaries;
- validate structured values such as enums, dates, IDs, URLs, amounts, and file metadata deliberately;
- authenticate identity before authorization decisions;
- authorize every protected server-side operation;
- default deny permissions;
- use least privilege;
- keep secrets out of code, logs, client bundles, and repositories;
- use proven password hashing and cryptographic libraries;
- use parameterized queries/ORM-safe bindings;
- rate-limit abuse-sensitive operations;
- prevent account enumeration where practical;
- validate file type, size, ownership, and access;
- secure cookies/tokens appropriately for the auth model;
- log important security-sensitive administrative actions;
- never roll custom cryptography.

External authentication establishes identity; it does not replace internal account/provisioning state or application authorization. Do not consider a client fully application-ready when required server-side synchronization/provisioning has failed.

Threat-model authentication, payments, admin functions, uploads, webhooks, password reset, invitations, and destructive actions.

## 12. Reliability

Assume every network call and external dependency can fail.

Use explicit timeouts. Retry only transient failures. Bound retries and use backoff where appropriate. Prefer idempotent operations when retries are possible.

Persist critical state before acknowledging success. Do not rely on in-memory or ephemeral filesystem state for durable business facts.

Design webhooks and jobs for duplicate delivery. Use unique constraints/idempotency keys where appropriate.

Health/readiness endpoints must report observed state. Do not claim a dependency is connected/healthy without actually checking the property the endpoint promises.

## 13. Money, payments, and commerce

Never use binary floating-point for authoritative monetary calculations.

Store money using integer minor units when suitable or an exact fixed-precision decimal type. Store currency explicitly.

Model separately when relevant:
- subtotal;
- discounts;
- shipping;
- fees;
- tax;
- total;
- amount paid;
- amount refunded;
- outstanding amount.

Do not recompute historical orders from mutable current product prices or tax configuration. Snapshot financial facts required for auditability.

Payments must support provider-reference uniqueness, idempotent verification/webhooks, reconciliation, failure states, and audit trails.

For wallets, fintech, marketplaces, or systems that move value, follow the relevant project profile and treat the ledger/transaction record as authoritative. Model authorization, capture, settlement, reversal, refund, payout, chargeback, and reconciliation as distinct states where the domain requires them.

Tax is jurisdiction- and transaction-dependent. Never invent tax rates, thresholds, invoice requirements, withholding rules, VAT/GST treatment, KYC/AML obligations, licensing rules, or filing obligations. Such rules must come from verified requirements and should preserve the basis needed to explain historical calculations later.

Financial rules require explicit stakeholder/accounting/compliance confirmation before production when legal or accounting obligations are involved.

## 14. API design and errors

Use consistent resource naming, HTTP methods, status codes, validation errors, pagination, filtering, and versioning policy.

Map expected client errors deliberately. Log unexpected internal errors server-side and return a generic client-safe response. Never expose SQL errors, stack traces, provider internals, secret/config values, or sensitive implementation details to clients by default.

Design mutation endpoints with concurrency and duplicate requests in mind.

## 15. Testing and verification

Tests should protect behavior and important invariants, not implementation trivia.

Use an appropriate mix of:
- unit tests for isolated business rules;
- integration tests for database and infrastructure boundaries;
- API tests for contracts;
- end-to-end tests for critical flows;
- load tests for capacity-sensitive systems;
- explicit manual verification for behavior not automated at the current stage.

Critical flows such as authentication, authorization, tenant isolation, payments, order state transitions, ledger operations, and destructive operations require happy-path and failure-path tests.

Testing depth must be calibrated by lifecycle stage and domain risk. An experiment may need only focused verification; a production/high-criticality financial flow requires significantly stronger coverage.

A feature is not complete merely because it compiles or builds.

When completion depends on test discovery, report meaningful counts. A successful test command that discovered zero relevant tests is not evidence that the intended behavior was tested.

Never imply backend/API tests verify frontend interactions they do not exercise. Distinguish automated, manual, and unverified behavior.

## 16. Observability

Production systems must make failures diagnosable.

Provide structured logs, meaningful error reporting, health/readiness checks as appropriate, and metrics for important service behavior.

Observability depth should match lifecycle stage. An MVP may start with structured logs and error reporting; production/growth should usually add actionable metrics/alerts; high-scale/high-criticality systems may require formal SLOs and error-budget thinking.

Never log passwords, full tokens, secrets, sensitive payment data, or unnecessary personal data.

For important business actions, prefer audit logs that identify actor, action, target, timestamp, and relevant non-sensitive context.

## 17. Dependencies and runtime discipline

Before adding or retaining a dependency ask:
- Can the platform/framework already do this well?
- Is the package actually used?
- Is the package maintained and widely used?
- What security/operational burden does it add?
- Is its scope proportionate to the problem?

Audit generated/scaffold dependencies and configuration. Do not assume starter-template packages belong in the finished product.

Do not add overlapping packages for the same job without justification.

Keep deploy-specific configuration outside code. Declare dependencies explicitly. Prefer stateless application processes for horizontally scalable services, with durable state in backing services.

## 18. Cost and financial constraints

Architecture has a financial cost.

For meaningful infrastructure choices estimate the major cost drivers: compute, database, storage, bandwidth/egress, email/SMS, third-party API calls, logging/observability, backups, payment fees, and operational overhead.

Prefer designs whose cost scales predictably with usage. Do not save tiny infrastructure costs by creating disproportionate engineering or reliability risk.

Record cost assumptions and the usage level at which an alternative becomes more economical.

## 19. Changes and refactoring

Do not rewrite working systems without a concrete benefit.

Make the smallest coherent change that solves the problem. Preserve backwards compatibility where required. Use migrations and staged rollouts for risky state changes.

Refactor when complexity obstructs correctness or changeability, not merely to make code look different. As a codebase grows, split responsibilities before a central composition/route/module file becomes a god file; do not compensate by adding unnecessary architectural layers.

## 20. Documentation and durable project state

Treat the canonical repository as the durable source of truth. Local, preview, or ephemeral workspace state is not final until persisted where the project expects it.

When architecture, commands, routes, configuration, phase state, or durable decisions change, reconcile the relevant artifacts such as:
- `README.md`;
- `.env.example` or config documentation;
- `docs/project-design.md`;
- `docs/PHASES.md`;
- `docs/CONTEXT.md`;
- `docs/NOW.md`;
- ADRs/runbooks/API docs.

Do not exaggerate implementation semantics. HTTP refresh/polling is not "real-time" unless there is an actual push/subscription mechanism. A provider candidate is not a permanent requirement. Planned behavior is not implemented behavior.

Verify README commands, paths, endpoints, config names, test claims, and status against the repository before final completion.

Do not silently invent a new implementation phase after the documented roadmap ends. Re-plan explicitly when new scope is required.

## 21. Completion standard

Before declaring work, a phase, or a project complete:
- run formatting/linting/type checks as applicable;
- run relevant tests and record meaningful discovery/pass counts when useful;
- distinguish automated, manual, runtime/provider-verified, and unverified evidence;
- inspect error paths and edge cases;
- inspect authentication, authorization, and tenant/resource boundaries;
- inspect schema/migration/invariant impact;
- inspect logs and responses for sensitive/internal data exposure;
- inspect dependency/config scaffold leftovers;
- verify lifecycle-stage expectations for the completed phase;
- verify health/readiness semantics if present;
- reconcile README, environment examples, phase/context/design docs, and public API documentation with actual code;
- verify the canonical repository contains the reviewed final state;
- list remaining risks, assumptions, limitations, and intentionally deferred work.

Never claim tests/checks passed unless they were actually executed. Never present a successful command with zero relevant work discovered as proof of coverage. Never claim complete repository synchronization without checking the canonical source when it is accessible.
