# Engineering Constitution for AI Agents

These rules apply to all software work unless the project explicitly overrides a rule in writing.

## 1. Mission
Build the simplest conventional solution that correctly satisfies the current requirements, current lifecycle stage, and risk level while leaving a reasonable path for future change.

Do not equate more technology with better engineering. Do not add infrastructure, packages, abstractions, services, caches, queues, event buses, databases, or frameworks unless a concrete requirement justifies them.

## 2. Mandatory pre-implementation process
Before substantial implementation:
1. Read the project requirements and existing codebase.
2. Read `templates/project-design.md` and complete the relevant sections in the project documentation.
3. Select the relevant profile(s) from `profiles/` and record why they apply.
4. Select the current lifecycle stage using `lifecycle/stages.md`, record why it applies, and note which stricter controls are required by domain risk.
5. Read `code-quality/clean-code.md` and `code-quality/project-structure.md`.
6. Identify functional requirements, non-functional requirements, expected scale, trust boundaries, persistence needs, external dependencies, deployment constraints, and budget constraints.
7. Inspect existing project conventions and follow them unless there is a strong reason not to.
8. State important assumptions. Do not silently invent business rules.
9. For major choices, compare at least one simpler alternative and document why the chosen option is appropriate.

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

## 5. Architecture
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

## 6. Code quality and semantics
Implementation must optimize for clarity, correctness, maintainability, and unsurprising behavior.

Follow `code-quality/clean-code.md`.

Use meaningful names, cohesive functions, low nesting, explicit side effects, framework-standard syntax, consistent formatting, and clear error handling.

Do not optimize for fewer lines. Do not compress logic into clever one-liners when readability suffers.

Long functions and files are review signals, not automatic failures. Split code when responsibilities or reasons to change diverge.

Avoid god objects/files, magic business values, stale comments, hidden mutation, silent error swallowing, deep inheritance, and abstractions that exist only to appear sophisticated.

Prefer small focused changes. Separate structural refactors from behavior changes when practical.

## 7. Project and file structure
Use the conventional structure of the selected framework first and follow `code-quality/project-structure.md`.

A file/module should have one coherent responsibility. Split by responsibility and domain, not arbitrary line counts.

Avoid dumping unrelated code into `utils`, `helpers`, `common`, or `services`.

Prefer feature/domain grouping once a codebase becomes non-trivial. Keep cross-domain shared code genuinely generic.

Do not create interfaces, factories, repositories, adapters, base classes, or dependency injection layers merely because they sound architectural. Introduce them when they isolate a real boundary or improve testability/changeability.

## 8. Database and persistence
Treat the database as part of the integrity model, not just storage.

Use:
- primary keys;
- foreign keys where relationships require integrity;
- NOT NULL where absence is invalid;
- UNIQUE constraints for true uniqueness invariants;
- CHECK constraints for simple enforceable invariants;
- transactions for multi-step state changes that must be atomic;
- indexes based on real query patterns;
- explicit migrations committed to source control.

Do not use application code as the only enforcement mechanism for invariants that the database can safely enforce.

Avoid N+1 queries, unbounded reads, accidental full-table scans, and pagination without deterministic ordering.

## 9. Scale and capacity
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

Use rough capacity estimates before adding scaling infrastructure. Prefer horizontal stateless application scaling where appropriate. Define specific triggers for introducing new infrastructure.

## 10. Security
Security is a design requirement.

At minimum:
- validate input at trust boundaries;
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

Threat-model authentication, payments, admin functions, uploads, webhooks, password reset, invitations, and destructive actions.

## 11. Reliability
Assume every network call and external dependency can fail.

Use explicit timeouts. Retry only transient failures. Bound retries and use backoff where appropriate. Prefer idempotent operations when retries are possible.

Persist critical state before acknowledging success. Do not rely on in-memory state for durable business facts.

Design webhooks and jobs for duplicate delivery. Use unique constraints/idempotency keys where appropriate.

## 12. Money, payments, and commerce
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

## 13. API design
Use consistent resource naming, HTTP methods, status codes, validation errors, pagination, filtering, and versioning policy.

Never expose internal stack traces or sensitive implementation details to clients.

Design mutation endpoints with concurrency and duplicate requests in mind.

## 14. Testing
Tests should protect behavior and important invariants, not implementation trivia.

Use an appropriate mix of:
- unit tests for isolated business rules;
- integration tests for database and infrastructure boundaries;
- API tests for contracts;
- end-to-end tests for critical flows;
- load tests for capacity-sensitive systems.

Critical flows such as authentication, authorization, payments, order state transitions, ledger operations, and destructive operations require happy-path and failure-path tests.

Testing depth must be calibrated by lifecycle stage and domain risk. An experiment may need only focused verification; a production/high-criticality financial flow requires significantly stronger coverage.

A feature is not complete merely because it compiles.

## 15. Observability
Production systems must make failures diagnosable.

Provide structured logs, meaningful error reporting, health/readiness checks as appropriate, and metrics for important service behavior.

Observability depth should match lifecycle stage. An MVP may start with structured logs and error reporting; production/growth should usually add actionable metrics/alerts; high-scale/high-criticality systems may require formal SLOs and error-budget thinking.

Never log passwords, full tokens, secrets, sensitive payment data, or unnecessary personal data.

For important business actions, prefer audit logs that identify actor, action, target, timestamp, and relevant non-sensitive context.

## 16. Dependencies and runtime discipline
Before adding a dependency ask:
- Can the platform/framework already do this well?
- Is the package maintained and widely used?
- What security/operational burden does it add?
- Is its scope proportionate to the problem?

Do not add overlapping packages for the same job without justification.

Keep deploy-specific configuration outside code. Declare dependencies explicitly. Prefer stateless application processes for horizontally scalable services, with durable state in backing services.

## 17. Cost and financial constraints
Architecture has a financial cost.

For meaningful infrastructure choices estimate the major cost drivers: compute, database, storage, bandwidth/egress, email/SMS, third-party API calls, logging/observability, backups, payment fees, and operational overhead.

Prefer designs whose cost scales predictably with usage. Do not save tiny infrastructure costs by creating disproportionate engineering or reliability risk.

Record cost assumptions and the usage level at which an alternative becomes more economical.

## 18. Changes and refactoring
Do not rewrite working systems without a concrete benefit.

Make the smallest coherent change that solves the problem. Preserve backwards compatibility where required. Use migrations and staged rollouts for risky state changes.

Refactor when complexity obstructs correctness or changeability, not merely to make code look different.

## 19. Completion standard
Before declaring work complete:
- run formatting/linting/type checks as applicable;
- run relevant tests;
- inspect error paths and edge cases;
- inspect authorization boundaries;
- inspect schema/migration impact;
- inspect logs for sensitive data;
- verify lifecycle-stage expectations for the completed phase;
- update documentation;
- list remaining risks or intentionally deferred work.

Never claim tests passed unless they were actually executed.
