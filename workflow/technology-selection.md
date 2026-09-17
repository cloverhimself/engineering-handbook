# Technology, Provider, and Build-vs-Buy Selection

Choose the least complex option that satisfies required system properties. Simplicity must not sacrifice correctness, durability, security, deployment compatibility, operability, or lifecycle needs.

## 1. Select the capability before the vendor

Decide what the system requires first, then select a product/provider.

Examples:
- requirement: durable relational database;
- candidates: local PostgreSQL for development, managed PostgreSQL for deployed environments;
- possible providers: Supabase, Neon, Railway, Cloud SQL, RDS, or another compatible service.

Do not turn a convenient platform default into a permanent architecture decision without a reason.

Record vendor-specific lock-in only when it materially affects the project.

## 2. Verify the deployment environment

Before choosing persistence, auth, storage, background processing, or networking, verify relevant platform properties:
- whether the filesystem is durable or ephemeral;
- supported ports and process model;
- connection limits and connection pooling expectations;
- cold starts/serverless execution constraints;
- supported runtimes and build output;
- secret/config injection;
- regional availability;
- backup/restore capabilities.

Do not infer hard platform restrictions merely from a starter scaffold, template, or existing folder layout.

## 3. Database choice

Use the simplest datastore that satisfies data relationships, durability, concurrency, querying, deployment, and operational requirements.

Typical guidance:
- SQLite can be excellent for local tools, prototypes, embedded applications, and deployments with durable single-node storage.
- PostgreSQL is a strong default for multi-user transactional applications with relational data.
- Managed PostgreSQL is usually preferable when the deployment environment does not provide durable local storage or when backups/operations should be outsourced.
- Additional databases should solve a concrete requirement rather than represent architectural ambition.

Development and production may use different hosting arrangements while keeping the same database engine and schema expectations.

## 4. Query layer: raw SQL, query builder, or ORM

PostgreSQL does not imply an ORM.

Prefer the least complex data-access approach that remains clear and safe:
- parameterized driver/raw SQL when queries are straightforward and explicit SQL is useful;
- a query builder when composability/type support materially improves development;
- an ORM when domain/query patterns, migrations, relations, or team conventions justify its additional abstraction.

Do not add an ORM only because one is popular. Do not remove an established ORM from a healthy codebase merely to be minimal.

Whatever layer is used, database constraints remain authoritative for enforceable invariants.

## 5. Build vs buy

For each external capability, compare:
- implementation complexity;
- security risk;
- operational burden;
- recurring cost;
- lock-in/migration cost;
- reliability requirements;
- lifecycle stage;
- existing team expertise.

Managed services are often appropriate for security-sensitive or operationally expensive capabilities such as authentication, transactional email, object storage, payment processing, managed databases, monitoring, and backups.

Building locally may be appropriate when the requirement is small, stable, well understood, and materially simpler than integrating another service.

Do not outsource trivial logic merely to accumulate vendors. Do not custom-build security-sensitive infrastructure merely to avoid a reasonable dependency.

## 6. Authentication

Choose the auth model from product needs rather than habit.

Candidates may include:
- framework/server-managed sessions;
- managed auth bundled with a platform such as Supabase;
- Firebase Authentication;
- Clerk/Auth0 or another identity provider;
- organization/enterprise identity when required.

Consider password/reset/email-verification requirements, OAuth providers, session model, account linking, tenancy, authorization ownership, pricing, deployment compatibility, and migration path.

External authentication proves identity. The application must still establish any required internal account/provisioning state and perform server-side authorization.

## 7. Hosting and supporting services

Select hosting based on the actual application shape:
- static frontend;
- server-rendered/full-stack framework;
- long-running API;
- serverless functions;
- workers/background jobs;
- persistent connections;
- file/media workloads.

Similarly, add object storage, cache, queues, search, or realtime infrastructure only when the product requires those capabilities.

A provider's availability is not itself a requirement to use it.

## 8. Decision record

For meaningful choices, record:
- required capability/system property;
- selected technology category;
- selected implementation/provider;
- why it fits now;
- simpler alternatives considered;
- important constraints/costs;
- what evidence would justify switching later.

Avoid fake precision. Numeric limits, pool sizes, scaling thresholds, and capacity triggers should come from provider constraints, measurements, explicit requirements, or be clearly labeled as provisional defaults.