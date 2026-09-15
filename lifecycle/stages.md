# Product Lifecycle Stages

Use lifecycle stage to calibrate engineering rigor. Do not apply high-scale production machinery to a prototype, and do not ship prototype shortcuts into production without an explicit decision.

## Stage 0 — Experiment / Spike

Purpose: answer a technical or product question quickly.

Priorities:
- speed of learning;
- minimal setup;
- disposable code is acceptable if clearly marked;
- no premature abstractions or infrastructure;
- no production claims.

Allowed shortcuts:
- hard-coded non-sensitive fixtures;
- simplified local-only flows;
- incomplete observability;
- limited tests where the experiment is temporary.

Not allowed:
- exposing secrets;
- bypassing critical security boundaries when real users/data are involved;
- representing the spike as production-ready.

Exit criteria:
- question answered;
- decision recorded;
- either discard the spike or deliberately convert it into a real implementation.

## Stage 1 — Prototype

Purpose: prove user flow, UX, or feasibility.

Priorities:
- validate behavior;
- simple architecture;
- fast iteration;
- minimal dependency surface.

Typical architecture:
- single application;
- one relational database if persistence is needed;
- managed services where they reduce setup burden;
- no distributed infrastructure unless the prototype specifically tests it.

Expected rigor:
- meaningful naming and structure;
- basic validation;
- basic auth if needed;
- critical-path tests only;
- explicit warning for temporary shortcuts.

Do not add:
- microservices;
- Kafka;
- Kubernetes;
- read replicas;
- complex cache layers;
- multi-region architecture;
unless the prototype's purpose is to validate those technologies.

## Stage 2 — MVP

Purpose: serve real users and validate product-market assumptions.

Priorities:
- correctness on core workflows;
- secure defaults;
- maintainable code;
- cost awareness;
- instrumentation for learning;
- simple rollback/recovery paths.

Expected rigor:
- production-grade authentication and authorization for the product's risk level;
- migrations in source control;
- database constraints for important invariants;
- integration/API tests around critical flows;
- structured logs and error reporting;
- backups if durable user data matters;
- rate limits for abuse-sensitive endpoints;
- explicit payment/idempotency/reconciliation controls where money is involved;
- documented assumptions and known limitations.

Scaling approach:
- estimate current load;
- optimize obvious query/index issues;
- prefer vertical scaling and simple horizontal stateless scaling before distributed redesign;
- add cache/queue only for a clear bottleneck or async requirement.

## Stage 3 — Production / Growth

Purpose: operate reliably for a meaningful user base and business process.

Priorities:
- reliability;
- operational visibility;
- change safety;
- data integrity;
- security;
- predictable cost;
- incident recovery.

Expected rigor:
- CI checks on every merge;
- meaningful code review / PR process;
- tested migrations and rollback strategy where feasible;
- health/readiness checks;
- metrics for latency, traffic, errors, and saturation;
- service-level objectives for important user journeys when useful;
- alerting on actionable failures;
- tested backup/restore process;
- dependency and vulnerability maintenance;
- stronger audit logs for privileged and financial actions;
- documented runbooks for important operational failures.

Architecture may now add:
- queues/workers for durable async workloads;
- Redis/cache for proven hot paths;
- object storage/CDN for media;
- replicas or partitioning after database evidence;
- dedicated search after database search becomes insufficient.

Do not add complexity only because the product is called "production".

## Stage 4 — High Scale / High Criticality

Purpose: handle substantial traffic, strict reliability targets, or high-value/high-risk workflows.

Triggers may include:
- sustained throughput that exceeds simple architecture limits;
- large concurrent user counts;
- multi-region latency/availability requirements;
- strict SLO/SLA commitments;
- large financial exposure;
- heavy asynchronous workloads;
- team boundaries requiring independent deployment;
- database capacity limits;
- regulatory/operational requirements.

Expected rigor:
- capacity models based on measured traffic;
- explicit SLOs/error budgets where appropriate;
- advanced load and failure testing;
- stronger disaster recovery targets;
- clear ownership boundaries;
- concurrency and idempotency reviewed systematically;
- database partitioning/replication/sharding only with concrete evidence;
- cost modeling for infrastructure changes;
- architecture decision records for major distributed-system choices.

Possible architecture:
- horizontally scaled stateless services;
- queues/streams;
- distributed caches;
- read replicas;
- partitioning/sharding;
- service extraction;
- multi-region components.

These are possibilities, not defaults.

## Stage selection rules

At project setup, the agent must choose one current lifecycle stage and record it in `docs/project-design.md` and `docs/CONTEXT.md`.

If the user does not specify one, infer conservatively:
- experiment/spike for throwaway research;
- prototype for non-production demonstrations;
- MVP for new products intended for real early users;
- production/growth for established live systems;
- high-scale/high-criticality only when requirements or evidence justify it.

The agent must state why it selected that stage.

## Stage transition rule

Moving to the next stage is an engineering event, not a label change.

When a project changes stage:
1. update `docs/project-design.md`;
2. update `docs/PHASES.md`;
3. update `docs/CONTEXT.md`;
4. run the lifecycle gap checklist;
5. create ADRs for material architecture changes;
6. add only the controls required by the new risk/scale level.

Do not rewrite the entire application merely because the lifecycle stage changes.

## Anti-overengineering rule

The lifecycle stage sets the minimum practical rigor, not the maximum sophistication.

A production system with 500 users can still be a modular monolith with one PostgreSQL database.

A prototype that handles real money still requires financial correctness on any transaction it actually performs.

Risk can override stage. Security, money movement, privacy, destructive operations, and irreversible state changes may require stricter controls even during MVP/prototype work.
