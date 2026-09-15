# Engineering Handbook — Guide and Table of Contents

This page is the main reading map for the handbook.

You do not need to read everything before building a project. Start with the **Foundations** section, then use the **Project Profiles**, **Lifecycle Stages**, and **Specialist Modules** that match the product you are building.

---

## 1. How the handbook works

The handbook is layered.

```mermaid
flowchart TD
    A[Core engineering principles] --> B[Project profile]
    A --> C[Lifecycle stage]
    A --> D[Code quality rules]
    B --> E[Relevant specialist modules]
    C --> E
    D --> E
    E --> F[Project-specific AGENTS.md]
    F --> G[Project design]
    G --> H[PHASES.md]
    H --> I[Implementation]
    I --> J[Supervisor review]
    J --> K[CONTEXT.md update]
```

Think of the layers like this:

- **Core rules** = engineering values that apply almost everywhere.
- **Profile** = what kind of product this is.
- **Lifecycle stage** = how mature or critical the product currently is.
- **Specialists** = deeper rules used only when needed.
- **Project files** = the specific decisions for the product being built.

---

# Table of Contents

## Part I — Foundations

1. [`concepts/foundations.md`](./concepts/foundations.md) — beginner-friendly explanations of common software/system concepts.
2. [`concepts/request-lifecycle.md`](./concepts/request-lifecycle.md) — how routes, middleware, controllers, services, databases, auth, validation and errors work together during one request.
3. [`concepts/glossary.md`](./concepts/glossary.md) — short definitions of recurring terms.
4. [`AGENTS.md`](./AGENTS.md) — the core engineering constitution.
5. [`architecture/principles.md`](./architecture/principles.md) — architecture principles and tradeoff thinking.
6. [`lifecycle/stages.md`](./lifecycle/stages.md) — experiment, prototype, MVP, production, and high-scale stages.

## Part II — Writing and Organizing Code

7. [`code-quality/clean-code.md`](./code-quality/clean-code.md) — naming, functions, modules, comments, readability, and complexity.
8. [`code-quality/project-structure.md`](./code-quality/project-structure.md) — how to organize files by project size and domain.
9. [`code-quality/dependency-discipline.md`](./code-quality/dependency-discipline.md) — rules for packages and libraries.
10. [`code-quality/defensive-programming.md`](./code-quality/defensive-programming.md) — defend plausible failures without coding for impossible states.

## Part III — Architecture and Scale

11. [`architecture/scaling.md`](./architecture/scaling.md) — vertical/horizontal scaling, concurrency, traffic, and capacity.
12. [`specialists/caching.md`](./specialists/caching.md) — when caching helps and when it hurts.
13. [`specialists/queues-background-jobs.md`](./specialists/queues-background-jobs.md) — async work, retries, and workers.
14. [`specialists/concurrency-locking.md`](./specialists/concurrency-locking.md) — race conditions, locking, optimistic concurrency, and transactions.
15. [`specialists/rate-limiting.md`](./specialists/rate-limiting.md) — abuse control and fairness.
16. [`specialists/observability-slos.md`](./specialists/observability-slos.md) — logs, metrics, tracing, SLI/SLO/SLA.

## Part IV — Backend and APIs

17. [`backend/conventions.md`](./backend/conventions.md) — normal backend layering and request flow.
18. [`specialists/api-versioning.md`](./specialists/api-versioning.md) — compatibility and versioning rules.
19. [`specialists/auth-sessions-jwt.md`](./specialists/auth-sessions-jwt.md) — login, sessions, access tokens, refresh tokens, and revocation.
20. [`specialists/file-uploads.md`](./specialists/file-uploads.md) — file/media handling and storage.

## Part V — Database and Data Integrity

21. [`database/design.md`](./database/design.md) — schema design, constraints, transactions, and migrations.
22. [`specialists/database-indexing-query-optimization.md`](./specialists/database-indexing-query-optimization.md) — indexes, query plans, N+1, pagination, and performance.

## Part VI — Security and Reliability

23. [`security/security.md`](./security/security.md) — authentication, authorization, trust boundaries, secrets, uploads, and admin operations.
24. [`reliability/production.md`](./reliability/production.md) — timeouts, retries, idempotency, failure handling, and production safety.

## Part VII — Money, Payments, and Financial Systems

25. [`finance/money-tax-payments.md`](./finance/money-tax-payments.md) — exact money representation, taxes, payment state, refunds, and provider verification.
26. [`finance/cost-engineering.md`](./finance/cost-engineering.md) — infrastructure and third-party cost thinking.
27. [`specialists/ledger-reconciliation.md`](./specialists/ledger-reconciliation.md) — ledger-first financial state, settlement, reconciliation, reversals, and discrepancies.

## Part VIII — Product Profiles

28. [`profiles/saas.md`](./profiles/saas.md)
29. [`profiles/ecommerce.md`](./profiles/ecommerce.md)
30. [`profiles/fintech.md`](./profiles/fintech.md)
31. [`profiles/marketplace.md`](./profiles/marketplace.md)
32. [`profiles/wallet.md`](./profiles/wallet.md)
33. [`profiles/content-platform.md`](./profiles/content-platform.md)
34. [`profiles/internal-tool.md`](./profiles/internal-tool.md)
35. [`profiles/portfolio-static-site.md`](./profiles/portfolio-static-site.md)
36. [`profiles/mobile-app.md`](./profiles/mobile-app.md)
37. [`profiles/api-only.md`](./profiles/api-only.md)
38. [`profiles/dashboard.md`](./profiles/dashboard.md)

## Part IX — Delivery Workflow

39. [`workflow/git-commits-prs.md`](./workflow/git-commits-prs.md) — branches, commits, pull requests, and review discipline.
40. [`workflow/supervisor-mode.md`](./workflow/supervisor-mode.md) — evidence-based self-review before completion.
41. [`templates/project-design.md`](./templates/project-design.md) — design decisions before implementation.
42. [`templates/PHASES.md`](./templates/PHASES.md) — implementation roadmap from setup to production.
43. [`templates/CONTEXT.md`](./templates/CONTEXT.md) — durable project handoff between agents/chats.
44. [`templates/adr.md`](./templates/adr.md) — architecture decision record.
45. [`checklists/new-project.md`](./checklists/new-project.md) — project startup checklist.
46. [`checklists/production-readiness.md`](./checklists/production-readiness.md) — launch checklist.

---

# Recommended reading paths

## If you are new to system design

Read in this order:

```text
Foundations
   ↓
Request lifecycle
   ↓
Architecture principles
   ↓
Backend conventions
   ↓
Database design
   ↓
Authentication
   ↓
Scaling
   ↓
Caching / queues / concurrency
   ↓
Security / reliability
   ↓
Your project profile
```

## If you are starting a new project with an AI agent

```mermaid
flowchart LR
    A[Describe product] --> B[Run bootstrap prompt]
    B --> C[Select profile]
    C --> D[Select lifecycle stage]
    D --> E[Select specialist modules]
    E --> F[Generate project design]
    F --> G[Generate PHASES.md]
    G --> H[Generate CONTEXT.md]
    H --> I[Review]
    I --> J[Implement phase by phase]
```

## If you are joining an existing project

Read:

1. `AGENTS.md`
2. `docs/CONTEXT.md`
3. `docs/PHASES.md`
4. `docs/project-design.md`
5. relevant ADRs
6. only the handbook modules referenced by that project

---

# Key philosophy

The handbook is not trying to make every project look enterprise-scale.

It is trying to make each project:

- easy to understand;
- conventional;
- correct;
- safe where risk matters;
- efficient enough for its real workload;
- structured enough to grow;
- documented enough that another developer or AI agent can continue the work.

The question is not:

> What is the most advanced architecture we can build?

The question is:

> What is the simplest conventional design that correctly solves the current problem and can evolve when evidence says it should?
