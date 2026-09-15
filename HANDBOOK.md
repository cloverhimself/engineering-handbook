# Engineering Handbook — Table of Contents

Use this page as the reading map. Most projects should read the core rules, then only the profile, lifecycle, and specialist modules that apply.

## 1. Core

- [`AGENTS.md`](./AGENTS.md) — core engineering constitution.
- [`concepts/glossary.md`](./concepts/glossary.md) — short definitions for recurring terms.
- [`architecture/principles.md`](./architecture/principles.md) — architecture and tradeoff principles.
- [`lifecycle/stages.md`](./lifecycle/stages.md) — experiment, prototype, MVP, production/growth, and high-scale/high-criticality.

## 2. Code quality

- [`code-quality/clean-code.md`](./code-quality/clean-code.md)
- [`code-quality/project-structure.md`](./code-quality/project-structure.md)
- [`code-quality/dependency-discipline.md`](./code-quality/dependency-discipline.md)
- [`code-quality/defensive-programming.md`](./code-quality/defensive-programming.md)

## 3. Backend, data, security, and reliability

- [`backend/conventions.md`](./backend/conventions.md)
- [`database/design.md`](./database/design.md)
- [`security/security.md`](./security/security.md)
- [`reliability/production.md`](./reliability/production.md)
- [`testing/strategy.md`](./testing/strategy.md)

## 4. Specialist modules

Load only when relevant:

- [`specialists/api-versioning.md`](./specialists/api-versioning.md)
- [`specialists/auth-sessions-jwt.md`](./specialists/auth-sessions-jwt.md)
- [`specialists/caching.md`](./specialists/caching.md)
- [`specialists/concurrency-locking.md`](./specialists/concurrency-locking.md)
- [`specialists/database-indexing-query-optimization.md`](./specialists/database-indexing-query-optimization.md)
- [`specialists/file-uploads.md`](./specialists/file-uploads.md)
- [`specialists/ledger-reconciliation.md`](./specialists/ledger-reconciliation.md)
- [`specialists/observability-slos.md`](./specialists/observability-slos.md)
- [`specialists/queues-background-jobs.md`](./specialists/queues-background-jobs.md)
- [`specialists/rate-limiting.md`](./specialists/rate-limiting.md)

## 5. Product profiles

Choose one or more as appropriate:

- [`profiles/saas.md`](./profiles/saas.md)
- [`profiles/ecommerce.md`](./profiles/ecommerce.md)
- [`profiles/fintech.md`](./profiles/fintech.md)
- [`profiles/marketplace.md`](./profiles/marketplace.md)
- [`profiles/wallet.md`](./profiles/wallet.md)
- [`profiles/content-platform.md`](./profiles/content-platform.md)
- [`profiles/internal-tool.md`](./profiles/internal-tool.md)
- [`profiles/portfolio-static-site.md`](./profiles/portfolio-static-site.md)
- [`profiles/mobile-app.md`](./profiles/mobile-app.md)
- [`profiles/api-only.md`](./profiles/api-only.md)
- [`profiles/dashboard.md`](./profiles/dashboard.md)

## 6. Finance and product thinking

- [`finance/money-tax-payments.md`](./finance/money-tax-payments.md)
- [`finance/cost-engineering.md`](./finance/cost-engineering.md)
- [`product/product-thinking.md`](./product/product-thinking.md)

## 7. Delivery workflow

- [`workflow/git-commits-prs.md`](./workflow/git-commits-prs.md)
- [`workflow/supervisor-mode.md`](./workflow/supervisor-mode.md)
- [`templates/project-design.md`](./templates/project-design.md)
- [`templates/PHASES.md`](./templates/PHASES.md)
- [`templates/CONTEXT.md`](./templates/CONTEXT.md)
- [`templates/adr.md`](./templates/adr.md)
- [`checklists/new-project.md`](./checklists/new-project.md)
- [`checklists/production-readiness.md`](./checklists/production-readiness.md)

## Recommended agent flow

```mermaid
flowchart LR
    A[Read core rules] --> B[Choose profile]
    B --> C[Choose lifecycle stage]
    C --> D[Load relevant specialists]
    D --> E[Create project design]
    E --> F[Create PHASES.md]
    F --> G[Implement]
    G --> H[Supervisor review]
    H --> I[Update CONTEXT.md]
```

Keep the handbook selective: do not load every module into every project. The goal is enough guidance to make sound engineering decisions without wasting context or encouraging unnecessary complexity.
