# Project Phases

This file is the living delivery roadmap. The agent must update it as work progresses.

## Current lifecycle stage

`experiment | prototype | MVP | production/growth | high-scale/high-criticality`

Why this stage applies:
- 

Stage-specific expectations:
- 

## Rules

- Break the project into coherent phases from initialization through production readiness.
- Each phase must have an objective, scope, deliverables, verification gates, and status.
- Do not mark a phase complete until its required checks were actually run.
- If scope changes, update this file before continuing substantial work.
- Record deferred work explicitly instead of silently dropping it.
- When the lifecycle stage changes, update this file, `docs/project-design.md`, and `docs/CONTEXT.md`, then review the gap between old-stage and new-stage requirements.
- Risk can override stage: money movement, auth, destructive operations, sensitive data, and irreversible state transitions may require stricter controls even in an MVP.

## Status values

`not-started` | `in-progress` | `blocked` | `complete` | `deferred`

## Phase template

### Phase N — <name>
Status: `not-started`

Objective:

Scope:
- 

Deliverables:
- 

Verification gates:
- [ ] relevant tests pass
- [ ] lint/type/build checks pass where applicable
- [ ] security/authorization impact reviewed
- [ ] database/migration impact reviewed
- [ ] documentation/context updated
- [ ] lifecycle-stage expectations satisfied for this phase

Decisions / notes:

Deferred / follow-up:

## Recommended lifecycle

Typical projects should adapt these rather than copy them blindly:
1. Discovery and product definition
2. Architecture and project setup
3. Core data/auth foundations
4. Primary product workflows
5. Secondary workflows and integrations
6. Security and abuse hardening
7. Reliability, observability, and performance appropriate to the lifecycle stage
8. QA, capacity validation, and production readiness
9. Deployment and launch verification
10. Post-launch measurement, cleanup, and future scaling decisions

## Stage calibration

### Experiment / spike
Use the fewest phases necessary to answer the question. Do not pretend experimental shortcuts are production-ready.

### Prototype
Prioritize working user flows and feasibility. Keep architecture simple and document shortcuts that must be removed before real-user production use.

### MVP
Real users require real correctness on core workflows, secure defaults, durable migrations, meaningful tests, basic observability, backups where needed, and cost-aware infrastructure.

### Production / growth
Add stronger CI/review discipline, operational metrics, alerting, tested recovery, runbooks, dependency maintenance, and safer change management.

### High-scale / high-criticality
Add explicit capacity models, SLO/error-budget thinking where useful, stronger failure/load testing, disaster-recovery targets, and distributed architecture only when measured constraints justify it.

See `.engineering/lifecycle/stages.md` for the full rules.
