# Engineering Handbook

A practical engineering rulebook for AI coding agents such as **Claude Code, Codex, Cursor, and similar tools**.

You describe what you want to build. The AI uses this handbook to decide how the project should be structured, which engineering rules apply, what tradeoffs matter, and what should be documented before implementation.

It covers:

- architecture and scalability;
- clean, maintainable code;
- project and file structure;
- APIs and backend conventions;
- database design and integrity;
- security;
- reliability and observability;
- testing;
- product thinking;
- payments, money movement, ledgers, refunds and reconciliation;
- tax/compliance boundaries;
- infrastructure and third-party costs;
- engineering tradeoffs.

The goal is **conventional, production-proven engineering**, not maximum architectural complexity.

## Quick start

You do not need to read the whole handbook.

1. Open the project you want to build in Claude Code, Codex, Cursor, or another coding agent.
2. Open [`BOOTSTRAP_PROMPT.md`](./BOOTSTRAP_PROMPT.md).
3. Copy the prompt.
4. Replace `WHAT I AM BUILDING` with a normal description of your product.
5. Paste it into your coding agent from the project root.

The agent will then:

- inspect your existing project if there is one;
- add this handbook under `.engineering/`;
- choose the relevant project profile(s);
- generate a small project-specific `AGENTS.md`;
- create `docs/project-design.md`;
- propose an appropriate architecture and folder structure;
- document assumptions, scale, security, cost and tradeoffs;
- stop before substantial implementation so you can review the design.

You can describe the product casually. You do **not** need to know the database schema, architecture, traffic model, folder structure or scaling strategy first.

Example:

```text
WHAT I AM BUILDING:

I want an ecommerce platform for a streetwear brand.
Customers should register, browse products, manage a cart and wishlist,
save addresses, place orders, pay online and track orders.

Staff should manage products, inventory and orders.
Managers should also manage users, permissions and analytics.

I want TypeScript, PostgreSQL and a REST API.
The business will start small but the codebase should remain easy to scale and maintain.
```

## Project profiles

The handbook contains profiles that add extra rules depending on what you are building:

- SaaS
- ecommerce
- fintech
- marketplace
- wallet
- content platform
- internal tool
- portfolio/static site
- mobile app
- API-only service
- dashboard

A project can use multiple profiles. For example, a multi-vendor commerce platform might use `saas + marketplace + ecommerce + dashboard`.

The coding agent selects the relevant profiles automatically and records the selection in the project design.

See [`profiles/`](./profiles/) for the profile rules.

## Code quality

Architecture alone is not enough. The handbook also tells agents how to write ordinary maintainable software:

- meaningful variable, function and module names;
- cohesive functions with clear responsibilities;
- low nesting and straightforward control flow;
- standard language/framework syntax and semantics;
- automated formatting and linting;
- explicit side effects and error handling;
- no giant god files;
- no arbitrary abstraction layers;
- domain-oriented file organization as projects grow;
- no magic business values;
- comments that explain *why*, not what the code already says;
- small focused changes and reviewable refactors;
- performance work based on actual workload, not guesswork.

There is deliberately **no arbitrary universal line limit** for functions or files. Size is treated as a signal to review cohesion and responsibility, not as a rule to game.

See [`code-quality/clean-code.md`](./code-quality/clean-code.md) and [`code-quality/project-structure.md`](./code-quality/project-structure.md).

## Money, payments and financial systems

The handbook includes stricter principles for systems that handle financial value.

Depending on the selected profile, agents are instructed to consider:

- exact monetary representation;
- explicit currency/asset handling;
- immutable transaction history;
- ledger-based balances;
- idempotent payment and transfer operations;
- authorization, capture, settlement, reversal, refund and chargeback states;
- payout separation in marketplaces;
- provider webhook verification;
- reconciliation;
- duplicate, delayed and reordered events;
- fee and rounding rules;
- auditability;
- infrastructure and processor cost;
- tax and regulatory requirements as externally verified inputs rather than guessed code.

For wallets and fintech systems, financial correctness takes priority over convenience.

## Core philosophy

The handbook repeatedly asks:

> What is the simplest conventional design that satisfies today's requirements, protects important invariants, remains understandable to ordinary developers, and leaves a reasonable path for tomorrow?

That means it will not recommend Kafka, Redis, Kubernetes, Elasticsearch, microservices, queues or custom abstraction layers merely because they sound scalable.

It should be able to explain **what problem each additional component solves and when that component becomes necessary**.

## Repository structure

```text
engineering-handbook/
├── AGENTS.md
├── BOOTSTRAP_PROMPT.md
├── profiles/
├── code-quality/
├── architecture/
├── backend/
├── database/
├── finance/
├── product/
├── reliability/
├── security/
├── testing/
├── checklists/
├── templates/
└── SOURCES.md
```

## Existing projects

The bootstrap flow also works for existing projects.

The agent is told to inspect the codebase first, preserve working conventions, and avoid gratuitous rewrites. The handbook should improve a project incrementally rather than forcing every application into the same architecture.

## After setup

Review the generated `docs/project-design.md`.

If it looks reasonable, tell your coding agent:

```text
The project design looks good. Begin implementation in the recommended phases.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep the design document and ADRs updated when important decisions change.
Keep the codebase clean and conventional as it grows.
Run the relevant checks after each phase and do not claim completion for checks you did not actually run.
```

## References

This handbook is an original engineering synthesis rather than copied book text. See [`SOURCES.md`](./SOURCES.md) for books, engineering references and public standards that influence it.

AI accelerates implementation. It does not remove the need for engineering judgment.
