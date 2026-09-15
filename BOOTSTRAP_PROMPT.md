# AI Bootstrap Prompt

Copy this into Claude Code, Codex, Cursor, or another coding agent from the root of the project you want to build.

Replace the `WHAT I AM BUILDING` section with your product description.

```text
I want this project to follow the engineering standards from:
https://github.com/cloverhimself/engineering-handbook

WHAT I AM BUILDING:
[Describe the product here in normal language. Explain what it should do, who will use it, important features, and any technologies or constraints you already know.]

Set this project up to use that engineering handbook.

Before substantial implementation:

1. Inspect the current codebase if one already exists. Do not destroy or unnecessarily restructure working code.
2. Make the engineering handbook available inside this project under `.engineering/`. Prefer a Git submodule when Git is available; otherwise use an appropriate non-destructive local setup.
3. Read `.engineering/AGENTS.md`, `.engineering/code-quality/clean-code.md`, and `.engineering/code-quality/project-structure.md`.
4. Select the relevant project profile or profiles from `.engineering/profiles/` based on what I am building. Use multiple profiles when appropriate. Record which profiles you selected and why in `docs/project-design.md`.
5. Read the handbook sections relevant to this specific product.
6. Create a concise project-specific `AGENTS.md` in this project's root. Do not copy the entire handbook into it. Reference `.engineering/` and include only rules, constraints, stack decisions, commands, selected profiles, and product-specific instructions that matter to this project.
7. Create `docs/project-design.md` using `.engineering/templates/project-design.md` as the starting point.
8. Based on my product description, fill the design document with reasonable initial assumptions for:
   - users and roles
   - selected project profiles
   - core workflows
   - V1 scope and out-of-scope items
   - architecture
   - project/folder structure
   - code-quality conventions
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
   - money, payments, refunds, invoices, tax, ledgering, payouts, or reconciliation if relevant
   - important tradeoffs
   - rejected unnecessary complexity
   - future scaling triggers
9. Prefer conventional, framework-native, boring, well-understood approaches. Do not introduce microservices, queues, Redis, Kafka, Kubernetes, Elasticsearch, custom frameworks, unnecessary abstraction layers, or other infrastructure unless the current requirements justify them.
10. Write maintainable code using meaningful names, cohesive functions/modules, low nesting, standard formatting, explicit side effects, and conventional syntax. Do not create giant files or arbitrary abstractions. Follow the framework's normal structure unless a clear domain boundary justifies something else.
11. Clearly distinguish facts I gave you from assumptions you made. Mark assumptions that should be confirmed later, but do not block initial setup on minor unknowns.
12. Do not guess jurisdiction-specific tax, legal, compliance, accounting, KYC/AML, licensing, or regulatory rules. Treat them as requirements that must come from a verified source or configuration.
13. Do not begin substantial feature implementation yet.

When setup is complete, show me:
- the files you created or changed;
- the project profiles you selected and why;
- the architecture you selected and why;
- the folder/module structure you recommend;
- the handbook sections this project will rely on most;
- the major assumptions you made;
- anything genuinely important I should decide before implementation;
- the recommended implementation phases.
```

After reviewing the generated project design, you can continue with:

```text
The project design looks good. Begin implementation in the recommended phases.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep docs/project-design.md and ADRs updated when important decisions change.
Keep the codebase clean and conventional as it grows; refactor when responsibilities become mixed or hard to understand, not to satisfy arbitrary line counts.
Run the relevant formatting, linting, type checks, tests, migrations, builds, and verification after each phase and do not claim completion for checks you did not actually run.
```
