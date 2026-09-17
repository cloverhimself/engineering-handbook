# Professional Project README Standard

A project README is the primary entry point for developers, reviewers, operators, and contributors. It should help someone understand what the project is, how it is structured, how to run it, and where important implementation details live.

Do not generate a README as marketing copy, filler, or a generic template dump. Write it from the actual repository state.

## Core rule

A good README should answer, quickly:

1. What is this project?
2. What problem does it solve?
3. What is the current implementation status?
4. What stack does it use?
5. How is the repository organized?
6. How do I run it locally?
7. What configuration is required?
8. How do the important flows work?
9. Where are the API, database, architecture, and operational details?
10. What should a developer know before changing it?

Keep the root README concise enough to scan. Move deep technical detail into `docs/` and link to it.

## Recommended structure

Use only sections that are relevant to the project.

```text
# Project Name

Short factual description.

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
## Testing
## Deployment
## Important Engineering Decisions
## Documentation
## Contributing
## License
```

Do not create empty sections just because they appear in this list.

## Project description

Use 1-3 factual paragraphs.

Explain:
- what the product/service does;
- who it is for when useful;
- the main problem or workflow it supports.

Avoid phrases such as:
- "powerful and innovative solution";
- "cutting-edge platform";
- "seamless user experience";
- "robust and scalable architecture";

unless the repository contains concrete evidence that makes the statement meaningful.

## Status

State the real lifecycle/status when useful:

```text
Status: MVP / active development
```

or

```text
Status: Production
```

Do not claim production readiness, scale, security, performance, or completeness without evidence.

If major features are incomplete, say so briefly or link to `docs/PHASES.md`.

## Features

List actual product capabilities, not implementation trivia.

Prefer:

```text
- Email/password authentication and account verification
- Product catalog with search, filtering, and pagination
- Persistent cart and checkout
- Paystack payment initialization, verification, and webhook handling
- Role-based administration
```

Avoid inflated feature counts or listing every small UI component.

## Tech stack

List important technologies by responsibility.

Example:

```text
Frontend: Next.js, React, TypeScript
Backend: Node.js, Express, TypeScript
Database: PostgreSQL, Drizzle ORM
Payments: Paystack
Email: SMTP / ZeptoMail
Testing: Vitest
```

Do not dump every package from `package.json` into the README.

## Architecture

Give the reader the smallest useful architecture picture.

Example:

```text
Frontend
   |
   v
Backend API
   |
   +--> PostgreSQL
   +--> Payment provider
   +--> Email provider
```

For larger systems, use a Mermaid diagram when it improves comprehension.

Explain important boundaries, not every class or function.

If detailed architecture documentation exists, link to it instead of duplicating it.

## Repository structure

Show the meaningful top-level and important second-level directories.

For a split full-stack project:

```text
project/
├── frontend/          # Client application
├── backend/           # API and business logic
├── docs/              # Architecture and operational documentation
├── AGENTS.md          # Project-specific agent instructions
└── README.md
```

For a backend:

```text
backend/
├── src/
│   ├── modules/       # Domain modules
│   ├── middleware/    # Request middleware
│   ├── infrastructure/# Database, email, storage integrations
│   ├── config/        # Runtime configuration
│   ├── app.ts         # Application setup
│   └── server.ts      # Process entry point
├── tests/
├── docs/
└── migrations/
```

Do not print enormous directory trees. Show enough structure for a new developer to know where things belong.

Descriptions beside folders should explain responsibility, not restate the folder name.

## Local development

Provide commands that actually exist in the repository.

Include, as relevant:
- required runtime/tool versions;
- dependency installation;
- environment setup;
- database startup;
- migrations/seeding;
- dev command;
- default ports.

Example:

```bash
npm install
cp .env.example .env
npm run db:start
npm run db:setup
npm run dev
```

Never invent scripts or commands. Inspect package/build files first.

## Environment variables

Do not publish secrets or real credentials.

Prefer documenting required variable names and purpose:

```text
DATABASE_URL       PostgreSQL connection string
JWT_SECRET         Token signing secret
PAYSTACK_SECRET_KEY Payment provider server key
```

If `.env.example` exists, link to it rather than duplicating every value.

Mark optional variables clearly.

## Database and migrations

For projects with a database, explain:
- database technology;
- migration command/location;
- seed command/location when applicable;
- whether migrations must run before application deployment;
- any development-specific database setup that would surprise a new developer.

Do not copy the entire schema into the README.

## API and endpoints

Include an API section when the repository exposes an API and the information is useful to developers.

For small APIs, a concise route-group table is enough:

| Area | Base path | Purpose |
|---|---|---|
| Auth | `/auth` | Login, registration, verification, password recovery |
| Products | `/products` | Product browsing and detail |
| Orders | `/orders` | Checkout and customer order operations |
| Admin | `/admin` | Protected management operations |

For large APIs, do not paste every endpoint into the README. Link to OpenAPI/Swagger/Postman or `docs/api.md`.

When specific endpoints matter for onboarding, document method, path, auth requirement, and purpose accurately.

Never invent undocumented endpoints.

## Important engineering decisions

Record only decisions a new developer is likely to question immediately.

Examples:
- why PostgreSQL was chosen;
- why the application is a modular monolith;
- why frontend/backend are separate applications;
- why sessions were chosen over JWTs;
- why a queue/cache was intentionally not introduced;
- why a particular provider owns file storage or payment processing.

Keep explanations brief and link to an ADR or design document for deeper reasoning.

Do not turn the README into an architecture diary.

## Testing

Document actual test/check commands:

```bash
npm test
npm run lint
npm run typecheck
npm run build
```

State important test categories when helpful.

Never write "all tests pass" as permanent README prose. Test results become stale.

## Deployment

Document only stable, useful deployment information:
- target platform/runtime;
- build/start commands;
- required migration step;
- relevant health endpoint;
- link to detailed production/runbook docs.

Do not expose credentials, private infrastructure details, or environment-specific secrets.

## Documentation links

For serious projects, the README should act as a map:

```text
- Architecture: docs/architecture.md
- Authentication: docs/authentication.md
- Payments: docs/payments.md
- Database: docs/database.md
- Development: docs/development.md
```

This is better than copying those documents into the README.

## Screenshots and media

Use screenshots for visual products when they help someone understand the product.

Do not add decorative screenshots to backend/API repositories merely to make the README look busy.

Keep screenshots current.

## Badges

Use badges only when they communicate useful live information such as CI status, package version, coverage, or license.

Avoid walls of decorative badges.

## Writing style

README prose should be:
- factual;
- concise;
- specific;
- professional;
- written for someone unfamiliar with the repository.

Avoid:
- excessive emojis;
- fake enthusiasm;
- generic AI introductions;
- repeated claims about scalability, robustness, performance, or security;
- unnecessary "Why choose this project?" marketing sections;
- filler such as "Welcome to..." when it adds no information;
- duplicating documentation that already lives elsewhere.

## Adapt by project type

### Portfolio/static site

Usually needs:
- short overview;
- stack;
- local setup;
- project structure if useful;
- deployment;
- screenshots/demo link.

It usually does not need database, API, migrations, architecture-decision, or operations sections.

### Frontend application

Usually needs:
- overview;
- stack;
- feature areas;
- routing/state/data-fetching conventions when non-obvious;
- project structure;
- environment variables;
- local development;
- build/deploy.

### Backend/API

Usually needs:
- purpose;
- architecture;
- stack;
- module structure;
- local setup;
- database/migrations;
- configuration;
- API documentation link/route groups;
- auth model;
- testing;
- deployment/health.

### Full-stack product

Usually needs:
- overview;
- architecture;
- clear `frontend/` and `backend/` structure when split;
- commands for each application;
- database and integrations;
- important API/docs links;
- deployment model.

### Financial/ecommerce systems

Add concise links to authoritative documentation for:
- payment flow;
- order/payment states;
- webhook behavior;
- reconciliation;
- inventory/financial invariants when relevant.

Do not place sensitive financial or provider credentials in the README.

## Agent procedure before writing or rewriting a README

1. Inspect the repository root and existing README.
2. Detect project type, stack, package/build commands, runtime, and folder structure.
3. Inspect `.env.example`, migration config, test config, deployment config, API documentation, and important `docs/` files when present.
4. Distinguish verified repository facts from assumptions.
5. Preserve useful existing project-specific information.
6. Remove stale, generic, duplicated, or unsupported claims.
7. Write only sections relevant to this repository.
8. Verify every command/path/endpoint referenced actually exists.
9. Link to deeper docs instead of copying them.
10. Review the README as if onboarding a developer who did not build the project.

## Completion check

Before finishing, ask:

- Can a new developer understand the project in a few minutes?
- Can they find the frontend, backend, tests, database, and docs quickly?
- Can they run it without guessing commands?
- Are configuration requirements clear without exposing secrets?
- Are API links/routes accurate?
- Are major architectural decisions explained only where useful?
- Is detailed documentation linked instead of duplicated?
- Is every claim supported by the repository?
- Does this read like engineering documentation rather than AI-generated promotional copy?
