# AI Bootstrap Prompt

Copy this into Claude Code, Codex, Cursor, or another coding agent from the root of the project you want to build.

Replace the `WHAT I AM BUILDING` section with your product description.

```text
I want this project to follow the engineering standards from:
https://github.com/cloverhimself/engineering-handbook

WHAT I AM BUILDING:
[Describe the product here in normal language. Explain what it should do, who will use it, important features, whether it is experimental/prototype/MVP/live production if known, and any technologies or constraints you already know.]

Set this project up to use that engineering handbook.

Before substantial implementation:

1. Inspect the current codebase if one already exists. Do not destroy or unnecessarily restructure working code.
2. Make the engineering handbook available inside this project under `.engineering/`. Prefer a Git submodule when Git is available; otherwise use an appropriate non-destructive local setup.
3. Read `.engineering/AGENTS.md`, `.engineering/lifecycle/stages.md`, `.engineering/code-quality/`, and `.engineering/workflow/`.
4. Select the relevant project profile or profiles from `.engineering/profiles/` based on what I am building. Use multiple profiles when appropriate and record why they apply.
5. Select the current lifecycle stage from `.engineering/lifecycle/stages.md`: experiment/spike, prototype, MVP, production/growth, or high-scale/high-criticality. If I did not specify one, infer conservatively and explain the choice. Do not choose high-scale/high-criticality without concrete evidence.
6. Identify any domain risk that requires stricter controls than the selected lifecycle stage, especially money movement, authentication, sensitive data, destructive operations, irreversible state transitions, or compliance-sensitive workflows.
7. Select only the specialist modules from `.engineering/specialists/` that are relevant to this project. Do not load complexity the product does not need.
8. Create a concise project-specific `AGENTS.md` in this project's root. Do not copy the entire handbook into it. Reference `.engineering/` and include only rules, constraints, stack decisions, lifecycle stage, commands, selected profiles/specialists, and product-specific instructions that matter to this project.
9. Create `docs/project-design.md` using `.engineering/templates/project-design.md` as the starting point. Record the selected lifecycle stage, why it applies, what it requires now, and what is intentionally deferred until a later stage.
10. Create `docs/PHASES.md` using `.engineering/templates/PHASES.md`. Generate a realistic phase plan from discovery/setup through production readiness, calibrated to the current lifecycle stage. Keep it updated as work progresses and never mark a phase complete unless its required checks were actually run.
11. Create `docs/CONTEXT.md` using `.engineering/templates/CONTEXT.md`. Treat it as durable handoff state for new chats, different AI agents, and human developers. Keep it concise, include the current lifecycle stage, and update it after meaningful work sessions.
12. Based on my product description, fill the design document with reasonable initial assumptions for:
   - users and roles
   - selected project profiles
   - lifecycle stage and stage rationale
   - risk overrides that require stricter controls
   - core workflows
   - V1 scope and out-of-scope items
   - architecture
   - project/folder structure
   - code-quality conventions
   - database design and invariants
   - API boundaries and versioning if needed
   - authentication, sessions/tokens, and authorization
   - expected total users, active users, concurrent users, traffic, and data growth when estimates are possible
   - scalability strategy appropriate to the current lifecycle stage
   - concurrency/locking needs
   - caching needs
   - queues/background jobs if justified
   - rate limiting and abuse controls
   - file/media handling if relevant
   - security and abuse risks
   - reliability and failure handling
   - testing strategy calibrated to lifecycle stage and domain risk
   - observability and SLOs only to the level warranted by the lifecycle stage and operational commitments
   - database indexing/query optimization expectations
   - deployment
   - infrastructure and third-party cost drivers
   - money, payments, refunds, invoices, ledger/reconciliation, tax, payouts, or money movement if relevant
   - important tradeoffs
   - rejected unnecessary complexity
   - future scaling triggers
   - lifecycle transition triggers
13. Prefer conventional, framework-native, boring, well-understood approaches. Do not introduce microservices, queues, Redis, Kafka, Kubernetes, Elasticsearch, custom frameworks, unnecessary abstraction layers, or other infrastructure unless the current requirements justify them.
14. Do not confuse "production-ready" with "high-scale architecture." A production system may still correctly be a modular monolith with one relational database.
15. Follow `.engineering/code-quality/dependency-discipline.md`. Do not install unnecessary, duplicate, unsupported, abandoned, or oversized libraries when the runtime, framework, an existing dependency, or a small local implementation already solves the problem clearly.
16. Follow `.engineering/code-quality/defensive-programming.md`. Defend real trust boundaries and plausible failure modes, but do not add branches for impossible internal states that are already guaranteed by trustworthy types, validated construction, database constraints, or controlled invariants. Do not hide programmer bugs behind fake defaults.
17. Write maintainable code using meaningful names, cohesive functions/modules, low nesting, standard formatting, explicit side effects, and conventional syntax. Refactor when responsibilities become mixed or hard to understand, not to satisfy arbitrary line counts.
18. Clearly distinguish facts I gave you from assumptions you made. Mark assumptions that should be confirmed later, but do not block initial setup on minor unknowns.
19. Do not guess jurisdiction-specific tax, legal, compliance, accounting, KYC/AML, licensing, privacy, or regulatory rules. Treat them as requirements that must come from a verified source or configuration.
20. Follow `.engineering/workflow/git-commits-prs.md`. Plan coherent commits and PR boundaries, but do not commit, push, open PRs, merge, or deploy unless I or the project instructions explicitly authorize those actions.
21. Use `.engineering/workflow/supervisor-mode.md` for substantial or high-risk work. Self-review the diff, run applicable checks, score the change using evidence, fix material issues, and repeat until the readiness threshold is met or further changes would only create churn. Never invent test results or scores for unverified dimensions.
22. Do not begin substantial feature implementation yet.

When setup is complete, show me:
- the files you created or changed;
- the project profiles and specialist modules you selected and why;
- the lifecycle stage you selected and why;
- any risk overrides that require stricter controls;
- the architecture you selected and why;
- the folder/module structure you recommend;
- what has intentionally been deferred because of the current lifecycle stage;
- the major assumptions you made;
- the generated project phases;
- the triggers that would justify moving to the next lifecycle stage;
- anything genuinely important I should decide before implementation;
- the recommended first implementation phase.
```

After reviewing the generated project design, phases, and context, you can continue with:

```text
The project design and phases look good. Begin the current phase.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep docs/project-design.md, docs/PHASES.md, docs/CONTEXT.md, and ADRs updated when meaningful decisions, lifecycle stage, or project state change.
Use supervisor mode for substantial changes.
Do not add next-stage infrastructure early unless current risk or measured requirements justify it.
Run the relevant formatting, linting, type checks, tests, migrations, builds, and verification after each phase and do not claim completion for checks you did not actually run.
```
