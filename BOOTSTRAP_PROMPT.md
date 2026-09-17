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
3. Read `.engineering/AGENTS.md`, `.engineering/lifecycle/stages.md`, `.engineering/workflow/technology-selection.md`, `.engineering/code-quality/code-craftsmanship.md`, `.engineering/code-quality/language-stack-overlays.md`, `.engineering/code-quality/dependency-discipline.md`, `.engineering/code-quality/defensive-programming.md`, `.engineering/workflow/context-budget.md`, and `.engineering/workflow/project-readme-standard.md`.
4. Select the relevant project profile or profiles from `.engineering/profiles/` based on what I am building. Use multiple profiles when appropriate and record why they apply.
5. Select the current lifecycle stage from `.engineering/lifecycle/stages.md`: experiment/spike, prototype, MVP, production/growth, or high-scale/high-criticality. If I did not specify one, infer conservatively and explain the choice. Do not choose high-scale/high-criticality without concrete evidence.
6. Identify the actual stack: language(s), runtime, frontend/backend framework(s), database/query layer, package manager/build tool, test framework, formatter/linter/type checker, and deployment/runtime constraints. Apply universal code-quality principles while keeping the implementation idiomatic to that language/framework. Do not force patterns from one language onto another.
7. Verify relevant deployment/platform facts before choosing persistence or infrastructure: durable vs ephemeral filesystem, supported process/port model, serverless/cold-start behavior, runtime/build restrictions, database connection limits, config/secret injection, and region constraints. Do not infer hard platform restrictions from a starter scaffold or folder layout.
8. Identify any domain risk that requires stricter controls than the selected lifecycle stage, especially money movement, authentication, sensitive data, destructive operations, irreversible state transitions, or compliance-sensitive workflows.
9. Select only the specialist modules from `.engineering/specialists/` that are relevant to this project. Do not load complexity the product does not need.
10. For meaningful technology choices, decide the required capability/system property before choosing a vendor. Separate things such as `durable managed PostgreSQL` from the current provider candidate. Compare build-vs-buy where relevant for auth, database hosting, storage, email, payments, monitoring, and similar capabilities.
11. Do not assume PostgreSQL requires an ORM. Choose parameterized raw SQL, a query builder, or an ORM based on actual query/domain complexity, migrations/types, project conventions, and team value.
12. Audit generated/scaffold dependencies and configuration. Remove or reject defaults that have no project requirement rather than assuming starter-template packages are intentional.
13. Create a concise project-specific `AGENTS.md` in this project's root. Do not copy the entire handbook into it. Reference `.engineering/` and include only rules, constraints, stack decisions, lifecycle stage, important commands, selected profiles/specialists, high-risk invariants, and product-specific instructions that matter to most tasks.
14. Create `docs/project-design.md` using `.engineering/templates/project-design.md` as the starting point. Record the selected lifecycle stage, deployment constraints, stack/provider choices, why the architecture applies, required invariants, what it requires now, and what is intentionally deferred until a later stage.
15. Create `docs/PHASES.md` using `.engineering/templates/PHASES.md`. Generate a realistic phase plan from discovery/setup through the current product target, calibrated to the lifecycle stage. Keep it updated as work progresses. Never mark a phase complete unless required checks were actually run. Do not silently invent a new phase after the roadmap ends; explicitly re-plan when new scope appears.
16. Create `docs/CONTEXT.md` using `.engineering/templates/CONTEXT.md`. Store only durable project facts, architecture, important invariants, accepted decisions, long-lived constraints, and persistent risks. Keep it concise and do not turn it into a session transcript.
17. Create `docs/NOW.md` using `.engineering/templates/NOW.md`. Use it as the small active-task handoff for new chats/agents. Update it after meaningful work sessions and replace stale information rather than appending a diary.
18. Follow `.engineering/workflow/context-budget.md`: new sessions should cold-start from `AGENTS.md`, `docs/NOW.md`, and `docs/CONTEXT.md`, then inspect only task-relevant source files. Read `PHASES.md`, project design, ADRs, and specialist modules only when the task needs them. Do not reread old chats to reconstruct state when these files are current.
19. For a conventional project with separate frontend and backend applications, keep them as separate top-level folders under the same parent project, for example `frontend/` and `backend/`. Do not mix backend-only code, database access, server secrets, or migrations into the frontend tree. Use a different structure only when the chosen full-stack framework intentionally combines them or there is a documented reason. Avoid both speculative architecture layers and giant god files as the codebase grows.
20. Create or improve the root `README.md` using `.engineering/workflow/project-readme-standard.md`. Write it from verified repository facts, not generic AI prose. Verify every command, path, endpoint, config name, test claim, feature status, and architecture statement before including it. Keep deep details in `docs/` and link to them instead of turning the README into a giant manual.
21. Based on my product description, fill the design document with reasonable initial assumptions for:
   - users and roles
   - selected project profiles
   - lifecycle stage and stage rationale
   - stack and language/framework conventions
   - verified deployment/runtime constraints
   - required system properties such as durability/security/availability
   - technology category vs provider/tool decisions
   - database engine and raw SQL/query-builder/ORM choice
   - build-vs-buy decisions
   - risk overrides that require stricter controls
   - core workflows
   - V1 scope and out-of-scope items
   - architecture
   - project/folder structure
   - code-quality conventions
   - database design, uniqueness, allowed states, foreign keys, delete behavior, transactions, tenant boundaries, and concurrency-sensitive invariants
   - temporal/data semantics such as calendar dates vs timestamps when relevant
   - API boundaries and versioning if needed
   - authentication, internal provisioning, sessions/tokens, and authorization
   - expected total users, active users, concurrent users, traffic, and data growth when estimates are possible
   - scalability strategy appropriate to the current lifecycle stage
   - concurrency/locking needs
   - caching needs
   - queues/background jobs if justified
   - rate limiting and abuse controls
   - file/media handling if relevant
   - security and abuse risks
   - reliability and failure handling
   - testing and verification strategy calibrated to lifecycle stage and domain risk
   - observability and SLOs only to the level warranted by the lifecycle stage and operational commitments
   - database indexing/query optimization expectations
   - deployment
   - infrastructure and third-party cost drivers
   - money, payments, refunds, invoices, ledger/reconciliation, tax, payouts, or money movement if relevant
   - important tradeoffs
   - rejected unnecessary complexity
   - future scaling triggers without fake numeric precision
   - lifecycle transition triggers
   - canonical repository/source-of-truth expectations
22. Prefer conventional, framework-native, boring, well-understood approaches. Do not introduce microservices, queues, Redis, Kafka, Kubernetes, Elasticsearch, custom frameworks, unnecessary abstraction layers, or other infrastructure unless current requirements justify them.
23. Do not confuse "production-ready" with "high-scale architecture." A production system may still correctly be a modular monolith with one relational database.
24. Follow `.engineering/code-quality/code-craftsmanship.md`. Optimize code for comprehension, correctness, changeability, and appropriate efficiency. Use meaningful domain names, cohesive functions/modules, clear control flow, suitable data structures, bounded I/O, efficient database access, explicit mutation, meaningful errors, and profiling/measurement before complex optimization.
25. Follow `.engineering/code-quality/language-stack-overlays.md`. Use the actual language's idioms, type system, error model, concurrency model, formatter/linter/static-analysis tools, and framework conventions. Avoid unnecessary unchecked type escapes such as `any` when the language can represent the validated type clearly.
26. Follow `.engineering/code-quality/dependency-discipline.md`. Do not install or retain unnecessary, duplicate, unsupported, abandoned, or oversized libraries when the runtime, framework, an existing dependency, or a small local implementation already solves the problem clearly.
27. Follow `.engineering/code-quality/defensive-programming.md`. Defend real trust boundaries and plausible failure modes, but do not add branches for impossible internal states already guaranteed by trustworthy types, validated construction, database constraints, or controlled invariants. Do not hide programmer bugs behind fake defaults.
28. Validate structured external inputs deliberately, including IDs, enums, dates, URLs, money/amounts, and file metadata when relevant. Define calendar-date/timezone semantics instead of allowing incidental runtime conversions to choose the business rule.
29. For authentication, distinguish external identity-provider success from the application's usable authenticated state. If backend provisioning/synchronization is required, do not mark the client ready when that step failed. Authorization always remains server-side.
30. Health/readiness endpoints must report observed state. Do not hard-code a dependency as connected/healthy without checking the property the endpoint promises.
31. Map expected client errors intentionally. Log unexpected database/provider/internal failures server-side and return generic client-safe responses. Do not expose SQL messages, stack traces, secret/config values, or provider internals by default.
32. Clearly distinguish facts I gave you from assumptions you made. Mark assumptions that should be confirmed later, but do not block initial setup on minor unknowns.
33. Do not guess jurisdiction-specific tax, legal, compliance, accounting, KYC/AML, licensing, privacy, or regulatory rules. Treat them as requirements that must come from a verified source or configuration.
34. Follow `.engineering/workflow/git-commits-prs.md`. Plan coherent commits and PR boundaries, but do not commit, push, open PRs, merge, or deploy unless I or the project instructions explicitly authorize those actions.
35. Use `.engineering/workflow/supervisor-mode.md` for substantial or high-risk work, phase completion, and final release review. Self-review the diff, run applicable checks, distinguish automated/manual/provider/unverified evidence, record meaningful discovery/pass counts, fix material issues, reconcile documentation/config with code, and verify the canonical repository contains the reviewed state before declaring completion.
36. Do not begin substantial feature implementation yet.

When setup is complete, show me:
- the files you created or changed;
- the project profiles and specialist modules you selected and why;
- the lifecycle stage you selected and why;
- the detected stack and language/framework conventions;
- the verified deployment/runtime constraints;
- the technology category/provider/build-vs-buy decisions and their rationale;
- any risk overrides that require stricter controls;
- the architecture you selected and why;
- the folder/module structure you recommend;
- what has intentionally been deferred because of the current lifecycle stage;
- the major assumptions you made;
- the generated project phases;
- how the README is structured and which deeper docs it links to;
- how new agent/chat sessions should cold-start with minimal context;
- the triggers that would justify moving to the next lifecycle stage;
- anything genuinely important I should decide before implementation;
- the recommended first implementation phase.
```

After reviewing the generated project design, phases, context, and README, you can continue with:

```text
The project design and phases look good. Begin the current phase.
Follow AGENTS.md and the engineering handbook throughout the project.
Keep docs/NOW.md current for the active task.
Update docs/CONTEXT.md only when durable project facts or decisions change.
Update docs/PHASES.md only when phase state or scope changes.
Keep README.md and environment/config examples accurate when setup, commands, architecture, public API, config reads, or important developer-facing behavior changes.
Use supervisor mode for substantial changes and every phase/project completion gate.
Do not add next-stage infrastructure early unless current risk or measured requirements justify it.
Run the relevant formatting, linting, type checks, tests, migrations, builds, runtime/provider verification, and manual verification after each phase.
Report what each check actually verified, including meaningful discovery/pass counts when relevant.
Do not claim automated coverage for behavior the tests did not exercise.
Before declaring a phase/project complete, reconcile durable docs and verify the canonical repository contains the reviewed final state.
```
