# Engineering Handbook — Table of Contents

Use this page as the reading map. Most projects should read the core rules, then only the profile, lifecycle, stack, technology-selection, and specialist modules that apply.

## 1. Core

- [`AGENTS.md`](./AGENTS.md) — core engineering constitution.
- [`concepts/glossary.md`](./concepts/glossary.md) — short definitions for recurring terms.
- [`architecture/principles.md`](./architecture/principles.md) — architecture and tradeoff principles.
- [`lifecycle/stages.md`](./lifecycle/stages.md) — experiment, prototype, MVP, production/growth, and high-scale/high-criticality.

## 2. Code quality

- [`code-quality/code-craftsmanship.md`](./code-quality/code-craftsmanship.md) — universal readability, maintainability, data-structure, I/O, database, error, and efficiency rules.
- [`code-quality/language-stack-overlays.md`](./code-quality/language-stack-overlays.md) — adapt implementation style to the actual language/runtime/framework.
- [`code-quality/clean-code.md`](./code-quality/clean-code.md) — naming, functions, modules, formatting, comments, and review principles.
- [`code-quality/project-structure.md`](./code-quality/project-structure.md) — folder/module organization, including separate top-level `frontend/` and `backend/` applications for conventional split full-stack projects.
- [`code-quality/dependency-discipline.md`](./code-quality/dependency-discipline.md)
- [`code-quality/defensive-programming.md`](./code-quality/defensive-programming.md)

Universal principles should remain language-agnostic. Implementation should remain idiomatic to the selected stack.

## 3. Backend, data, security, and reliability

- [`backend/conventions.md`](./backend/conventions.md)
- [`database/design.md`](./database/design.md)
- [`security/security.md`](./security/security.md)
- [`reliability/production.md`](./reliability/production.md)
- [`testing/strategy.md`](./testing/strategy.md) — evidence scope, discovery counts, tenant-boundary tests, and lifecycle-calibrated automation.

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
- [`specialists/production-basics.md`](./specialists/production-basics.md)
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

## 7. Delivery, technology selection, and agent workflow

- [`workflow/technology-selection.md`](./workflow/technology-selection.md) — capability-before-vendor decisions, deployment constraints, database/access-layer selection, build-vs-buy, auth, hosting, and provisional defaults.
- [`workflow/project-readme-standard.md`](./workflow/project-readme-standard.md) — professional project README structure, verified setup instructions, repository map, API/docs linking, and anti-slop rules.
- [`workflow/context-budget.md`](./workflow/context-budget.md) — low-token cold starts, context hygiene, multi-agent handoff, and minimum-sufficient reading.
- [`workflow/git-commits-prs.md`](./workflow/git-commits-prs.md)
- [`workflow/supervisor-mode.md`](./workflow/supervisor-mode.md) — evidence-based final/phase review, canonical-repo verification, and documentation reconciliation.
- [`templates/project-design.md`](./templates/project-design.md)
- [`templates/PHASES.md`](./templates/PHASES.md)
- [`templates/NOW.md`](./templates/NOW.md) — tiny active-task state for fresh chats/agents.
- [`templates/CONTEXT.md`](./templates/CONTEXT.md) — stable project facts only.
- [`templates/adr.md`](./templates/adr.md)
- [`checklists/new-project.md`](./checklists/new-project.md)
- [`checklists/production-readiness.md`](./checklists/production-readiness.md)

## Recommended agent flow

```mermaid
flowchart LR
    A[Read core rules] --> B[Detect stack + deployment constraints]
    B --> C[Choose profile + lifecycle]
    C --> D[Select capability before vendor]
    D --> E[Load relevant specialists]
    E --> F[Create project design]
    F --> G[Create PHASES + CONTEXT + NOW]
    G --> H[Implement current phase]
    H --> I[Verify with evidence]
    I --> J[Supervisor review]
    J --> K[Reconcile docs + canonical repo]
```

## New-chat cold start

```text
AGENTS.md
   ↓
docs/NOW.md
   ↓
docs/CONTEXT.md
   ↓
current task files/tests
   ↓
only then open PHASES / project design / ADRs / deeper handbook modules if needed
```

Do not reread entire chats or the whole repository just to regain orientation when the project context files are current.

Keep the handbook selective: do not load every module into every project. The goal is enough guidance to make sound engineering decisions without wasting context or encouraging unnecessary complexity.

At phase/project completion, the canonical repository — not an ephemeral preview workspace — is the final source of truth. Verification claims, README/config examples, PHASES/NOW/CONTEXT, and implementation should agree before work is declared complete.
