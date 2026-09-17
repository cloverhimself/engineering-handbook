# Sources and Influences

This handbook is an **original engineering synthesis**. It does not reproduce copyrighted books or claim that every rule came verbatim from one source.

The goal of this file is to make the handbook auditable: distinguish established engineering guidance from original AI-agent workflow design, and show which source categories influenced which parts of the handbook.

## Source priority

When sources disagree, prefer them in roughly this order:

1. official language, framework, database, cloud, payment-provider, and security documentation;
2. current standards and authoritative engineering guidance;
3. established software-engineering books and long-running practitioner references;
4. reputable engineering blogs, conference talks, and experienced-practitioner material;
5. community discussions such as Reddit or social posts.

Community sources can reveal useful workflow ideas and recurring problems, but they are not treated as authoritative technical standards.

---

## Architecture, system design, and distributed systems

Primary influences:

- Martin Kleppmann — *Designing Data-Intensive Applications*
- Mark Richards & Neal Ford — *Fundamentals of Software Architecture*
- Neal Ford et al. — *Software Architecture: The Hard Parts*
- Martin Fowler — *Patterns of Enterprise Application Architecture*
- Sam Newman — *Building Microservices*
- Vaughn Vernon / Vlad Khononov — domain-driven design literature, including *Learning Domain-Driven Design*
- Alex Xu — *System Design Interview*, Volumes 1 and 2
- Google SRE resources — https://sre.google/
- The Twelve-Factor App — https://12factor.net/

Influenced handbook areas:

- `architecture/`
- modular-monolith-first guidance
- scaling triggers
- service boundaries
- stateless application processes
- queues, caching, retries, and failure handling
- lifecycle-aware infrastructure decisions

---

## Code quality, readability, refactoring, and maintainability

Primary influences:

- Martin Fowler — *Refactoring*
- John Ousterhout — *A Philosophy of Software Design*
- Martin Fowler — Code Smells: https://martinfowler.com/bliki/CodeSmell.html
- Google Engineering Practices — https://google.github.io/eng-practices/
- official language/framework style guides and ecosystem-standard formatters/linters

Influenced handbook areas:

- `code-quality/clean-code.md`
- `code-quality/code-craftsmanship.md`
- naming and cohesion rules
- clear control flow
- small reviewable changes
- avoiding arbitrary line-count rules
- refactoring based on actual design problems instead of cosmetic churn
- readability over cleverness

Important interpretation used by this handbook:

A long function/file is treated as a **review signal**, not automatic proof of bad code. This is consistent with code-smell thinking: a smell suggests something to inspect, not a rule to enforce mechanically.

---

## Language and stack-specific implementation

Primary influences:

- official language documentation and style guides;
- official framework documentation;
- official package-manager/tooling documentation;
- established formatter/linter/type-checker conventions in the selected ecosystem.

Examples include the official documentation for TypeScript/JavaScript, Python, Go, Java/Kotlin, Rust, SQL/PostgreSQL, and whichever framework a project actually uses.

Influenced handbook areas:

- `code-quality/language-stack-overlays.md`
- stack-native syntax and semantics
- error handling
- async/concurrency models
- type-system usage
- project structure
- formatter/linter choices

The handbook intentionally applies **universal engineering principles with stack-native implementation** rather than forcing one language's patterns onto another.

---

## Databases, indexing, transactions, and concurrency

Primary influences:

- PostgreSQL official documentation — https://www.postgresql.org/docs/
- Alex Petrov — *Database Internals*
- *Designing Data-Intensive Applications*
- relational database and SQL design literature

Influenced handbook areas:

- `database/design.md`
- `specialists/database-indexing-query-optimization.md`
- `specialists/concurrency-locking.md`
- constraints and invariants
- transaction boundaries
- indexes based on real query patterns
- query plans
- locking and race-condition handling
- migrations

Database-specific semantics should always defer to the current official documentation for the database being used.

---

## Security, authentication, sessions, authorization, and uploads

Primary influences:

- OWASP Application Security Verification Standard (ASVS)
- OWASP Cheat Sheet Series — https://cheatsheetseries.owasp.org/
- Authentication Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
- Session Management Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
- Authorization Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- File Upload Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
- Transaction Authorization Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html
- Secure Code Review Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/Secure_Code_Review_Cheat_Sheet.html

Influenced handbook areas:

- `security/security.md`
- `specialists/auth-sessions-jwt.md`
- `specialists/file-uploads.md`
- server-side authorization
- least privilege and deny-by-default
- session/token handling
- sensitive-operation authorization
- trust boundaries
- secure upload handling
- security review of high-risk flows

---

## Reliability, operations, observability, and deployment

Primary influences:

- Google SRE books and public guidance — https://sre.google/
- Michael Nygard — *Release It!*
- The Twelve-Factor App — https://12factor.net/
- cloud-provider architecture and reliability documentation
- official framework/runtime deployment documentation

Influenced handbook areas:

- `reliability/production.md`
- `specialists/observability-slos.md`
- `specialists/production-basics.md`
- explicit timeouts
- bounded retries/backoff
- failure containment
- logs/metrics/health checks
- stateless processes
- environment/config separation
- deployment and rollback thinking
- backup/restore basics

---

## Git, commits, code review, and pull requests

Primary influences:

- GitHub documentation — https://docs.github.com/
- Google Engineering Practices — https://google.github.io/eng-practices/

Influenced handbook areas:

- `workflow/git-commits-prs.md`
- small focused commits
- reviewable pull requests
- self-review before requesting review
- verification before merge
- separating unrelated refactors/features/dependency upgrades

---

## Payments, money movement, ledgers, and reconciliation

Primary influences:

- OWASP transaction/security guidance
- official payment-provider documentation for signatures, webhook verification, payment states, retries, idempotency, and reconciliation
- *Designing Data-Intensive Applications* and database transaction/integrity literature
- common accounting/ledger design principles

Influenced handbook areas:

- `finance/money-tax-payments.md`
- `specialists/ledger-reconciliation.md`
- `profiles/fintech.md`
- `profiles/wallet.md`
- `profiles/ecommerce.md`
- `profiles/marketplace.md`

Core principles include:

- exact money representation;
- explicit currency/asset handling;
- immutable/auditable transaction history;
- idempotent financial operations;
- explicit payment/settlement/refund/reversal states;
- reconciliation with external providers;
- separate customer payment from marketplace payout where relevant.

Provider-specific behavior must always defer to the provider's current official documentation.

Tax, KYC/AML, licensing, accounting, privacy, and other jurisdiction-specific obligations are **not** inferred from these engineering sources. They must come from current authoritative requirements or qualified professionals.

---

## Product thinking and team structure

Primary influences:

- Marty Cagan — *Inspired*
- Team Topologies — Matthew Skelton & Manuel Pais
- Lean/product-discovery literature

Influenced handbook areas:

- `product/product-thinking.md`
- smallest useful scope
- explicit out-of-scope decisions
- user journeys
- ownership boundaries
- avoiding speculative V1 complexity

---

## AI coding agents, context handoff, and multi-agent workflow

This area contains the highest proportion of **original synthesis** in the handbook.

Inputs include:

- current coding-agent product guidance and repository-instruction patterns;
- practical experience with long-running AI-assisted coding sessions;
- community discussions from experienced users on Reddit and other developer communities about context exhaustion, handoff files, fresh chats, and multi-agent coordination;
- observed problems such as agents rereading large chat histories, stale handoff documents, context dilution, unnecessary rewrites, and repeated rediscovery of project decisions.

Representative community discussions include recent threads in communities such as `r/ClaudeCode` about context exhaustion and handoff-file failures. These are treated as **practitioner anecdotes**, not standards.

Influenced handbook areas:

- `workflow/context-budget.md`
- `templates/NOW.md`
- `templates/CONTEXT.md`
- `templates/PHASES.md`
- `workflow/supervisor-mode.md`
- bootstrap/project initialization flow

The exact `NOW.md + CONTEXT.md + PHASES.md` model, supervisor scoring thresholds, lifecycle/profile composition, and cold-start protocol are **handbook-original workflow designs** built from those broader principles and observed problems.

---

## What is sourced vs original synthesis?

Most core software-engineering principles in this repository are established practices adapted from the references above.

The wording, structure, profile system, specialist-module system, lifecycle model, bootstrap flow, AI-agent context strategy, and supervisor workflow are original synthesis created for this handbook.

A rough characterization is:

- core engineering principles: predominantly established practice;
- handbook wording and organization: original;
- AI-agent operating workflow: substantially original synthesis informed by current practitioner experience.

No percentage should be treated as a scientific measurement; the important distinction is whether a rule represents established engineering guidance, provider-specific documentation, community experience, or a handbook-specific workflow convention.

---

## Verification rule

When implementing a real project:

- use this handbook for engineering defaults;
- verify framework/language/database behavior against current official documentation;
- verify provider integrations against current provider docs;
- verify security-sensitive behavior against current OWASP/primary guidance;
- verify jurisdiction-specific legal, tax, accounting, privacy, KYC/AML, licensing, and consumer-protection requirements independently.

The handbook is a decision framework, not a replacement for authoritative technical or legal documentation.
