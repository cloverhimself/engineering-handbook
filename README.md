# Engineering Handbook

A practical set of engineering rules for AI coding agents such as **Claude Code, Codex, Cursor, and similar tools**.

It helps your coding agent build software using conventional, production-proven engineering practices instead of randomly choosing patterns, packages, or infrastructure.

The handbook covers architecture, project structure, APIs, databases, scalability, security, reliability, testing, product thinking, payments, money, tax considerations, infrastructure cost, and engineering tradeoffs.

You do **not** need to read or manually configure the whole handbook before every project.

## The easiest way to use it

Open your project in your AI coding agent and paste the prompt below.

Replace the `WHAT I AM BUILDING` section with a normal description of your product. You do not need to know the architecture, database schema, folder structure, or scaling strategy yet. That is what the handbook is for.

```text
I want this project to follow the engineering standards from:
https://github.com/cloverhimself/engineering-handbook

WHAT I AM BUILDING:
[Describe the product here in normal language. Explain what it should do, who will use it, important features, and any technologies or constraints you already know.]

Set this project up to use that engineering handbook.

Before substantial implementation:

1. Inspect the current codebase if one already exists. Do not destroy or unnecessarily restructure working code.
2. Make the engineering handbook available inside this project under `.engineering/`. Prefer a Git submodule when Git is available; otherwise use an appropriate non-destructive local setup.
3. Read `.engineering/AGENTS.md` and the handbook sections relevant to this specific product.
4. Create a concise project-specific `AGENTS.md` in this project's root. Do not copy the entire handbook into it. Reference `.engineering/` and include only rules, constraints, stack decisions, commands, and product-specific instructions that matter to this project.
5. Create `docs/project-design.md` using `.engineering/templates/project-design.md` as the starting point.
6. Based on my product description, fill the design document with reasonable initial assumptions for:
   - users and roles
   - core workflows
   - V1 scope and out-of-scope items
   - architecture
   - project/folder structure
   - database design and invariants
   - API boundaries
   - authentication and authorization
   - expected total users, active users, concurrent users, traffic, and data growth when estimates are possible
   - scalability strategy
   - security and abuse risks
   - reliability and failure handling
   - testing strategy
   - observability
   - deployment
   - infrastructure and third-party cost drivers
   - money, payments, refunds, invoices, tax, or reconciliation if relevant
   - important tradeoffs
   - rejected unnecessary complexity
   - future scaling triggers
7. Prefer conventional, framework-native, boring, well-understood approaches. Do not introduce microservices, queues, Redis, Kafka, Kubernetes, Elasticsearch, custom frameworks, unnecessary abstraction layers, or other infrastructure unless the current requirements justify them.
8. Clearly distinguish facts I gave you from assumptions you made. Mark assumptions that should be confirmed later, but do not block initial setup on minor unknowns.
9. Do not guess jurisdiction-specific tax, legal, compliance, or regulatory rules. Treat them as requirements that must come from a verified source or configuration.
10. Do not begin substantial feature implementation yet.

When setup is complete, show me:
- the files you created or changed;
- the architecture you selected and why;
- the handbook sections this project will rely on most;
- the major assumptions you made;
- anything genuinely important I should decide before implementation;
- the recommended implementation phases.
```

That's it.

After the agent finishes the setup, review `docs/project-design.md`. If the assumptions look reasonable, tell the agent to begin implementation phase by phase while following `AGENTS.md`.

For example:

```text
The project design looks good. Begin implementation in the recommended phases.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep docs/project-design.md and ADRs updated when important decisions change.
Run the relevant checks after each phase and do not claim completion for checks you did not actually run.
```

## Example product description

You can describe a product casually. For example:

```text
WHAT I AM BUILDING:

I want to build an ecommerce platform for a streetwear brand.
Customers should be able to register, browse products, manage a cart and wishlist,
save addresses, place orders, pay online, receive notifications and track orders.

Staff should manage products, inventory and orders. Managers should also manage
users, permissions and analytics.

I want a TypeScript backend, PostgreSQL database and a REST API.
I expect the business to start small, but I do not want the architecture to become
a dead end if usage grows later.
```

The coding agent should use that description together with this handbook to decide what matters for the project rather than blindly applying every possible architecture pattern.

## What the handbook is trying to prevent

AI coding agents can produce working code very quickly, but they can also over-engineer simple systems or make unconventional decisions simply because a pattern sounds sophisticated.

This handbook pushes the agent toward a few defaults:

- use established language and framework conventions;
- prefer a modular monolith unless distribution is justified;
- use database constraints and transactions properly;
- design before adding infrastructure;
- scale from measured requirements rather than imagined millions of users;
- treat authentication and authorization separately;
- treat money and payment operations as auditable state transitions;
- never use floating-point arithmetic for monetary values;
- never invent tax or legal rules;
- make retries bounded and idempotent where needed;
- write tests around risk and business invariants;
- consider infrastructure and third-party costs when choosing architecture;
- document meaningful tradeoffs and rejected alternatives;
- keep the codebase understandable to normal developers.

## Repository structure

```text
engineering-handbook/
├── AGENTS.md                 # Core engineering constitution
├── agent/                    # How coding agents should use the handbook
├── architecture/             # Architecture and scalability rules
├── backend/                  # Backend and project-structure conventions
├── database/                 # Relational design and data rules
├── finance/                  # Money, payments, tax boundaries and cost engineering
├── product/                  # Product and scope thinking
├── reliability/              # Production failure-handling practices
├── security/                 # Security principles and trust boundaries
├── testing/                  # Testing strategy
├── checklists/               # Project-start and production-readiness checks
├── templates/                # Project design and ADR templates
└── SOURCES.md                # Books and public standards that influenced the handbook
```

## Existing projects

The same bootstrap prompt works for an existing codebase. The agent is specifically instructed to inspect the current project first and avoid unnecessary rewrites.

It should adapt the handbook to the architecture that already exists, identify meaningful problems, and only recommend migrations or restructuring when there is a concrete reason.

## Updating the handbook in a project

If the handbook was added as a Git submodule, update it with:

```bash
cd .engineering
git pull origin main
cd ..
git add .engineering
git commit -m "chore: update engineering handbook"
```

This means existing projects stay pinned to the handbook version they were built with until you deliberately update them.

## Philosophy

The handbook is not a command to use the most sophisticated architecture available.

The default question is:

> What is the simplest conventional design that satisfies today's requirements, protects important invariants, remains understandable, and leaves a reasonable path for tomorrow?

AI accelerates implementation. It does not remove the need for engineering judgment.
