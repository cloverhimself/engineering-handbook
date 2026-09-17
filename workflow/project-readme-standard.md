# Professional Project README Standard

A project README is the primary entry point for developers, reviewers, operators, and contributors. It should explain what the project is, how it is structured, how to run it, and where deeper details live.

Do not generate marketing copy, filler, or a generic template dump. Write from the actual canonical repository state.

## Core rule

A good README should quickly answer:
1. What is this project and its current status?
2. What does it actually do now?
3. What stack and architecture does it use?
4. Where do important frontend/backend/data modules live?
5. How do I run it locally?
6. What configuration is required?
7. How do important API/data/auth flows work?
8. What verification exists and what remains manual/unverified?
9. How is it deployed?
10. Where are deeper docs?

Keep the root README scannable. Move deep detail into `docs/` and link to it.

## Recommended sections

Use only what applies:

```text
# Project Name
## Overview
## Status
## Features
## Tech Stack
## Architecture
## Repository Structure
## Requirements
## Local Development
## Environment Variables
## Database / Migrations
## API
## Testing / Verification
## Deployment
## Important Engineering Decisions
## Documentation
## Contributing
## License
```

Do not create empty sections merely because they appear here.

## Accuracy rules

Every developer-facing claim must be supported by the repository or verified runtime/provider state.

Do not:
- call planned features implemented;
- call HTTP refresh/polling "real-time" without actual push/subscription behavior;
- call a provider candidate a permanent architecture requirement;
- call a partial route group full CRUD;
- claim security, scalability, performance, production readiness, or completeness without evidence;
- state that tests cover frontend/browser behavior when only backend/API tests exist.

When the canonical repository is accessible, inspect it after local/preview work is persisted. Local workspace state is not sufficient final evidence.

## Overview and status

Use factual language and real lifecycle/status.

Good:
```text
Status: MVP / active development
```

Avoid generic claims such as "cutting-edge", "robust and scalable", or "seamless" unless they convey a verified property.

## Features

List actual product capabilities, not implementation trivia or inflated feature counts.

## Tech stack and architecture

List important technologies by responsibility, not every package.

Explain the smallest useful architecture picture and major boundaries. Link to project design/ADRs for deeper reasoning.

Distinguish capability from provider where useful. Example: "PostgreSQL, currently hosted on Cloud SQL" is different from making Cloud SQL part of the conceptual data model.

## Repository structure

Inspect the current tree. Show meaningful top-level/second-level paths and responsibilities only.

Never reuse an intended folder layout after the implementation has changed. Verify paths such as root `server.ts`, `src/routes/`, `frontend/`, `backend/`, migrations, tests, and docs actually exist.

## Local development

Document only commands that exist in package/build/task files and have the stated purpose.

Include as relevant:
- runtime/tool versions;
- dependency installation;
- environment setup;
- database startup/migrations/seeding;
- dev command;
- build/start commands;
- default ports.

Do not invent commands.

## Environment/configuration

Inspect actual configuration reads and `.env.example` together.

Required variable names in the README and environment example must match the code. Remove stale scaffold variables that the product no longer uses.

Never include real secrets. Clearly distinguish client-public configuration from server secrets. If `.env.example` is authoritative, link to it rather than duplicating every placeholder.

## Database and migrations

State the database engine, migration mechanism/location, required setup commands, and important deployment order when useful. Do not dump the whole schema.

## API

For small APIs, list implemented route groups or endpoints accurately. For larger APIs, link to OpenAPI/Postman/API docs.

Verify method, path, auth expectations, and capability against route registration/source. Do not describe endpoints that do not exist or broaden partial capabilities into "CRUD".

## Authentication

When relevant, state the identity/session model and where server authorization occurs. Do not imply that a managed identity provider owns application authorization unless that is actually true.

## Testing and verification

Document actual commands and stable test categories.

Distinguish:
- automated unit/integration/API/E2E coverage;
- manual frontend/runtime verification;
- provider/environment verification;
- known unautomated areas.

Do not permanently write "all tests pass" without a live badge/CI source. If citing a current count as part of a release/status snapshot, make clear what those tests cover.

A successful backend test suite does not prove browser state transitions, accessibility, rendering, or frontend navigation unless those behaviors are exercised.

## Deployment

Document stable target/runtime assumptions, build/start commands, migrations, configuration expectations, and health endpoints. Do not invent infrastructure detail or expose secrets.

## Important engineering decisions

Record only decisions a new developer is likely to question, such as:
- modular monolith vs services;
- database/access-layer choice;
- auth/session approach;
- intentionally omitted queue/cache;
- provider choice when it materially affects development.

Keep explanations short and link to ADRs/project design.

## Documentation map

Link to deeper authoritative documents rather than copying them into README:

```text
- Architecture: docs/project-design.md
- Context/invariants: docs/CONTEXT.md
- Roadmap: docs/PHASES.md
- Active task: docs/NOW.md
```

## Adapt by project type

Portfolio/static sites can be lightweight. Frontend apps should explain build/deploy and non-obvious state/data conventions. Backend/API projects should emphasize configuration, database/migrations, auth, API docs, tests, and health/deploy. Full-stack projects should make frontend/backend boundaries and commands obvious. Financial/ecommerce systems should link to authoritative payment/order/webhook/reconciliation/invariant docs.

Do not force irrelevant sections onto simple projects.

## Agent procedure before writing or finalizing a README

1. Inspect the canonical repository root and current README.
2. Detect project type, stack, package/build commands, runtime, folder structure, and deployment configuration.
3. Inspect actual config reads plus `.env.example`.
4. Inspect migration/test config and route registration/API docs when present.
5. Inspect project design, PHASES/CONTEXT/NOW, ADRs, and important operational docs only as needed.
6. Distinguish repository facts, runtime/provider facts, assumptions, and stale intent.
7. Preserve useful project-specific information; remove obsolete scaffold/generated claims.
8. Verify every command, path, endpoint, config name, test-scope claim, feature status, and architecture statement.
9. Link to deeper docs instead of duplicating them.
10. After local/preview edits are persisted, re-check the canonical repository before declaring the README reconciled.

## Completion check

Before finishing, ask:
- Can a new developer understand the project and current state quickly?
- Can they find code, tests, database, config, and docs?
- Can they run it without guessing commands?
- Do environment examples match actual configuration reads?
- Are repository paths and API routes accurate?
- Are verification claims scoped to what was actually exercised?
- Are architecture/provider statements precise rather than overstated?
- Are stale phase/status/features removed?
- Does the canonical repository contain this final README?
- Does it read like engineering documentation rather than AI-generated promotional copy?
