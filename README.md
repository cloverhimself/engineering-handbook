# Engineering Handbook

A practical engineering rulebook for AI coding agents such as **Claude Code, Codex, Cursor, and similar tools**.

Its purpose is simple: help an AI agent build software using conventional, maintainable, production-aware engineering practices without over-engineering the project or under-engineering required system properties.

## Quick start

1. Open your project in your coding agent.
2. Open [`BOOTSTRAP_PROMPT.md`](./BOOTSTRAP_PROMPT.md).
3. Replace `WHAT I AM BUILDING` with a normal description of your product.
4. Paste the prompt from the project root.

The agent will inspect the project, choose the relevant product profile, lifecycle stage, technology/provider approach, and specialist modules, then create the project-specific engineering files before substantial implementation.

Typical generated files:

```text
project/
├── AGENTS.md
├── .engineering/
├── docs/
│   ├── project-design.md
│   ├── PHASES.md
│   ├── CONTEXT.md
│   ├── NOW.md
│   └── adr/
└── src/
```

Actual application structure should follow the selected framework and project shape rather than this illustrative tree.

## How the handbook works

```mermaid
flowchart LR
    A[Product description] --> B[Core rules]
    B --> C[Profile + lifecycle]
    C --> D[Deployment + technology selection]
    D --> E[Relevant specialists]
    E --> F[Project design + phases + context]
    F --> G[Implementation]
    G --> H[Evidence-based verification]
    H --> I[Supervisor review]
    I --> J[Docs + canonical repo reconciled]
```

The layers mean:

- **Core rules** — general engineering standards.
- **Profiles** — extra rules for SaaS, ecommerce, fintech, wallet, marketplace, mobile, APIs, dashboards, and similar products.
- **Lifecycle stage** — experiment, prototype, MVP, production/growth, or high-scale/high-criticality.
- **Technology selection** — capability-before-vendor, build-vs-buy, database/query-layer, auth, hosting, deployment, and provider decisions.
- **Specialists** — deeper modules loaded only when relevant, such as caching, queues, auth, concurrency, indexing, observability, or ledger/reconciliation.
- **Supervisor review** — final evidence gate that checks implementation, tests, documentation, and the canonical repository before completion claims.

## What the handbook enforces

- conventional framework-native solutions first;
- simplicity without sacrificing required durability, security, deployment, or correctness properties;
- capability/system-property decisions before provider/vendor lock-in;
- build-vs-buy reasoning for auth, database hosting, storage, email, payments, and similar services;
- raw SQL/query-builder/ORM chosen by actual need rather than habit;
- verified deployment constraints instead of scaffold assumptions;
- clear project/module structure without speculative layers or god files;
- meaningful naming, idiomatic types, and maintainable code;
- no unnecessary, unsupported, duplicate, or leftover scaffold dependencies;
- no excessive defensive programming for impossible internal states;
- database constraints, referential behavior, transactions, and tenant boundaries where they protect real invariants;
- explicit authentication, internal provisioning, and server-side authorization boundaries;
- deliberate structured input/date/time semantics;
- realistic traffic and scaling assumptions without fake precision;
- idempotent and auditable payment/money flows;
- truthful health/readiness and client-safe error handling;
- persistent `PHASES.md`, `CONTEXT.md`, and `NOW.md` for multi-agent work;
- verification claims scoped to what was actually tested or manually/provider verified;
- README/config/docs reconciled with real commands, routes, configuration reads, and implementation;
- canonical repository verification before a phase/project is declared complete.

## Navigation

- [`HANDBOOK.md`](./HANDBOOK.md) — concise table of contents and reading map.
- [`AGENTS.md`](./AGENTS.md) — core engineering constitution.
- [`BOOTSTRAP_PROMPT.md`](./BOOTSTRAP_PROMPT.md) — copy/paste project bootstrap flow.
- [`workflow/technology-selection.md`](./workflow/technology-selection.md) — provider/build-vs-buy/database/auth/hosting decision guidance.
- [`concepts/glossary.md`](./concepts/glossary.md) — quick definitions for common terms.
- [`profiles/`](./profiles/) — product-specific rules.
- [`lifecycle/`](./lifecycle/) — stage-specific expectations.
- [`specialists/`](./specialists/) — deeper technical guidance.
- [`code-quality/`](./code-quality/) — code structure, dependencies, and defensive-programming rules.
- [`workflow/`](./workflow/) — technology selection, context, README, supervisor mode, Git, commits, and PRs.
- [`templates/`](./templates/) — project design, phases, context, active-task state, and ADR templates.

## Core philosophy

> Build the simplest conventional system that correctly solves today's problem, protects important invariants and required system properties, and leaves a sensible path for tomorrow.

Production-ready does not automatically mean microservices, Redis, Kafka, Kubernetes, or multiple databases. Simplicity also does not mean ephemeral persistence, unverified auth assumptions, giant files, or pretending a passing build proves correctness. Add complexity only when a concrete requirement, risk, provider constraint, or measured bottleneck justifies it.
