# Project Design

## 1. Problem
What real problem is being solved?

## 2. Users
Who are the users and roles?

## 3. Product profiles
Which profiles from `.engineering/profiles/` apply, and why?

## 4. Lifecycle stage
Current stage: `experiment | prototype | MVP | production/growth | high-scale/high-criticality`

Why this stage applies:

What this stage requires now:

What is intentionally deferred until a later stage:

Risk overrides: note any area that needs stricter controls than the general lifecycle stage because of money movement, sensitive data, auth, destructive operations, irreversible state changes, or compliance obligations.

## 5. Scope
### V1
### Explicitly out of scope

## 6. Core user journeys

## 7. Functional requirements

## 8. Non-functional requirements
Latency, availability, durability, privacy, compliance, accessibility, portability, operability, etc.

## 9. Capacity assumptions
- registered users:
- DAU/MAU:
- peak concurrent users:
- average/peak RPS:
- read/write ratio:
- data growth:
- media/bandwidth:
- geographic distribution:

Label provisional estimates clearly. Do not invent precise thresholds without evidence.

## 10. Deployment/runtime constraints
Verify the actual environment rather than inferring it from scaffolding.

Consider:
- durable vs ephemeral filesystem;
- process/port model;
- serverless/cold-start constraints;
- runtime/build restrictions;
- database connection behavior;
- secret/config injection;
- region/latency constraints.

## 11. Architecture
Describe the simplest architecture that satisfies the requirements, deployment environment, required system properties, and current lifecycle stage.

## 12. Technology/provider selection
For meaningful choices, separate the required capability from the selected vendor/tool.

Record as relevant:
- database engine and hosting approach;
- raw SQL / query builder / ORM choice;
- auth/session provider/model;
- hosting/runtime provider;
- object/file storage;
- email/SMS;
- payments;
- monitoring/observability;
- queues/cache/search/realtime only if needed.

For each material choice note why it fits now, simpler alternatives considered, build-vs-buy reasoning, cost/lock-in/operational concerns, and what would justify switching later.

## 13. Data model and invariants
Document true uniqueness, allowed state sets, foreign keys, referential/delete behavior, tenant boundaries, transactional invariants, and concurrency-sensitive rules.

If application logic relies on a property that the database can safely enforce, state whether it is enforced there.

## 14. Temporal/data semantics
When relevant define calendar dates, local date-times, UTC timestamps, durations, money units, identifiers, and other structured values whose meaning can otherwise become ambiguous.

## 15. Authentication and authorization
Distinguish external identity/authentication from internal account provisioning and server-side authorization.

## 16. External dependencies
Include failure behavior, lifecycle ownership, lock-in, and cost model.

## 17. Security/threat model

## 18. Money/tax/payment model
If applicable. Include currency, exactness, tax source/configuration, payment lifecycle, refunds, reconciliation.

## 19. Reliability
Timeouts, retries, idempotency, jobs, backups, health/readiness behavior.

Health/readiness claims should describe observed checks rather than assumed dependency state.

## 20. Observability and audit
State what is appropriate for the current lifecycle stage and what is deferred.

## 21. Testing and verification strategy
State the current lifecycle-stage baseline and any stricter domain-specific tests.

Distinguish automated testing, manual verification, runtime/provider checks, and currently unverified behavior. Define what evidence is required before a phase can be called complete.

## 22. Deployment and environments

## 23. Estimated cost drivers

## 24. Tradeoffs and rejected alternatives

## 25. Scaling triggers
Specify measurable triggers when evidence exists. Avoid fake precision.

## 26. Lifecycle transition triggers
What evidence would justify moving this product to the next lifecycle stage?

## 27. Durable project-state rules
Identify the canonical repository/source of truth and which documents/config examples must stay synchronized with implementation, such as README, `.env.example`, PHASES, CONTEXT, NOW, API docs, and ADRs.
