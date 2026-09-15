# Engineering Handbook

A practical engineering rulebook and operating system for AI coding agents such as **Claude Code, Codex, Cursor, and similar tools**.

You describe what you want to build. The AI uses this handbook to decide how the project should be structured, which engineering rules apply, what tradeoffs matter, how work should be phased, and what project state must be preserved between chats or agents.

The goal is **conventional, production-proven engineering**, not maximum architectural complexity.

## Quick start

You do not need to read the whole handbook.

1. Open the project you want to build in your coding agent.
2. Open [`BOOTSTRAP_PROMPT.md`](./BOOTSTRAP_PROMPT.md).
3. Copy the prompt.
4. Replace `WHAT I AM BUILDING` with a normal product description.
5. Paste it into the coding agent from the project root.

The agent will:

- inspect an existing project without gratuitously rewriting it;
- add this handbook under `.engineering/`;
- choose relevant project profiles;
- choose the current lifecycle stage;
- choose only relevant specialist modules;
- generate a small project-specific `AGENTS.md`;
- create `docs/project-design.md`;
- create and maintain `docs/PHASES.md` from setup through production readiness;
- create and maintain `docs/CONTEXT.md` for new chats, multiple AI agents, and human handoffs;
- propose architecture, database and folder structure;
- document assumptions, traffic/scale, security, cost and tradeoffs;
- enforce dependency/package discipline;
- avoid excessive defensive programming for impossible internal states;
- use supervisor/self-review mode for substantial changes;
- plan clean commit and PR boundaries;
- stop before substantial implementation so you can review the plan.

## Lifecycle stages

The handbook now distinguishes between:

- **experiment / spike** — answer a question quickly;
- **prototype** — prove UX or feasibility;
- **MVP** — serve real early users with real correctness on core flows;
- **production / growth** — operate reliably for a meaningful user base and business process;
- **high-scale / high-criticality** — handle substantial traffic, strict reliability commitments, large financial exposure, or complex operational requirements.

See [`lifecycle/stages.md`](./lifecycle/stages.md).

The lifecycle stage changes how much rigor is expected around testing, observability, CI, backups, scaling infrastructure, runbooks, capacity modeling, and failure testing.

It does **not** weaken domain-critical correctness. An MVP wallet still needs correct money movement. A prototype that handles real credentials still needs secure auth boundaries.

A production product also does not automatically need microservices, Kubernetes, Redis, Kafka, or multiple databases. Production readiness and high-scale architecture are different things.

## Project profiles

Available profiles include:

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

A project can combine profiles. A multi-vendor commerce platform might use `saas + marketplace + ecommerce + dashboard`.

See [`profiles/`](./profiles/).

## Specialist engineering modules

The agent loads these only when relevant:

- API versioning
- concurrency and locking
- caching strategy
- queues and background jobs
- rate limiting
- file uploads and media
- authentication, sessions and JWTs
- observability and SLOs
- database indexing and query optimization
- ledger and reconciliation

See [`specialists/`](./specialists/).

## Clean code without dogma

The handbook covers meaningful names, cohesive functions/modules, low nesting, standard formatting, explicit side effects, error handling, project structure, reviewable refactors, and performance discipline.

There is no universal function/file line limit. Size is a signal to inspect cohesion and responsibility, not a metric to game.

It also has two explicit AI safeguards:

- [`code-quality/dependency-discipline.md`](./code-quality/dependency-discipline.md): do not install unnecessary, duplicate, abandoned, unsupported, or oversized libraries when the runtime/framework/existing dependencies already solve the problem.
- [`code-quality/defensive-programming.md`](./code-quality/defensive-programming.md): defend real trust boundaries and plausible failures, but do not litter the codebase with branches for impossible states already guaranteed by reliable invariants.

See [`code-quality/`](./code-quality/).

## Persistent project memory

AI chat context is temporary; project state should not be.

Every serious project created with the bootstrap flow gets:

### `docs/PHASES.md`

A living roadmap from initial discovery through production readiness. Each phase has scope, deliverables, verification gates, status, decisions and deferred work. Agents update it as the product is built.

It also records the current lifecycle stage so phase expectations are calibrated appropriately.

### `docs/CONTEXT.md`

A compact durable handoff containing current state, architecture, lifecycle stage, active assumptions, verified checks, current task, risks and next actions.

When switching from Claude Code to Codex, starting a fresh chat, or handing work to another developer, the receiving agent reads `AGENTS.md`, `docs/CONTEXT.md`, `docs/PHASES.md` and relevant ADRs instead of relying on a manually written chat summary.

Templates live in [`templates/`](./templates/).

## Supervisor mode

[`workflow/supervisor-mode.md`](./workflow/supervisor-mode.md) defines an optional evidence-based review loop for substantial work.

It scores areas such as correctness, readability, maintainability, security, testing, architecture fit, performance, failure handling, documentation accuracy and unnecessary complexity.

Default readiness requires no critical dimension below 8/10 and an overall mean of at least 8.5/10. High-risk financial/auth/security work requires stronger correctness/security scores.

The agent must justify scores with actual evidence and mark unverified dimensions as unverified. It must stop when further iteration would become churn rather than meaningful improvement.

## Git, commits and pull requests

[`workflow/git-commits-prs.md`](./workflow/git-commits-prs.md) tells agents to:

- work in coherent reviewable units;
- commit at meaningful checkpoints rather than every tiny edit or only once after a giant change;
- avoid mixing unrelated refactors/features/dependency upgrades;
- self-review diffs before PRs;
- run applicable checks first;
- keep PRs focused and split large work by meaningful layers;
- update phases/context before handoff;
- never commit, push, open PRs, merge or deploy unless the user/project explicitly authorizes it.

## Money, payments and financial systems

Financial systems receive stricter rules for:

- exact monetary representation;
- currencies/assets;
- immutable transaction history;
- ledger-based balances;
- idempotent payments and transfers;
- authorization/capture/settlement/reversal/refund/chargeback states;
- marketplace payouts;
- provider signature/reference verification;
- reconciliation;
- duplicates, delayed and reordered events;
- concurrency and locking;
- fees and rounding;
- auditability;
- processor/infrastructure cost;
- tax/accounting/compliance requirements as verified external inputs rather than invented code.

For wallets and fintech systems, financial correctness takes priority over convenience regardless of lifecycle stage.

## Core philosophy

The handbook repeatedly asks:

> What is the simplest conventional design that satisfies today's requirements, current lifecycle stage, and real risk level, protects important invariants, remains understandable to ordinary developers, and leaves a reasonable path for tomorrow?

That means it will not recommend Kafka, Redis, Kubernetes, Elasticsearch, microservices, queues, custom abstraction layers, or extra packages merely because they sound scalable.

Each additional component should have a concrete problem it solves, a tradeoff, and a trigger that justified introducing it.

## Repository structure

```text
engineering-handbook/
├── AGENTS.md
├── BOOTSTRAP_PROMPT.md
├── lifecycle/
├── profiles/
├── specialists/
├── code-quality/
├── workflow/
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

The bootstrap flow works for existing projects too. Agents are instructed to inspect the codebase first, preserve working conventions, choose the lifecycle stage from the actual state of the product, and improve incrementally instead of forcing every application into the same architecture.

## After setup

Review `docs/project-design.md`, `docs/PHASES.md`, and `docs/CONTEXT.md`.

Then tell the agent:

```text
The project design and phases look good. Begin the current phase.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep docs/project-design.md, docs/PHASES.md, docs/CONTEXT.md, and ADRs updated when meaningful decisions, lifecycle stage, or project state change.
Use supervisor mode for substantial changes.
Do not introduce next-stage infrastructure early unless current risk or measured requirements justify it.
Run the relevant checks after each phase and do not claim completion for checks you did not actually run.
```

## References

This handbook is an original engineering synthesis rather than copied book text. See [`SOURCES.md`](./SOURCES.md) for books, engineering references and public standards that influence it.

AI accelerates implementation. It does not remove the need for engineering judgment.
