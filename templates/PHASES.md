# Project Phases

This file is the living delivery roadmap. The agent must update it as work progresses.

## Current lifecycle stage

`experiment | prototype | MVP | production/growth | high-scale/high-criticality`

Why this stage applies:
- 

Stage-specific expectations:
- 

## Rules

- Break the project into coherent phases appropriate to the current product target. Do not create phases merely to make the roadmap look comprehensive.
- Each phase must have an objective, scope, deliverables, verification gates, and status.
- Identify the primary user journeys introduced or changed by each user-facing phase.
- Do not mark a phase complete until its required checks were actually run, relevant user journeys were functionally accepted, and evidence exists.
- A passing command is not enough when it may discover zero relevant work; record useful discovery/pass counts where appropriate.
- Distinguish automated tests/checks, browser/device/manual verification, runtime/provider verification, and unverified behavior.
- If scope changes, update this file before continuing substantial work.
- Do not silently invent a new phase after the documented roadmap ends. Explicitly re-plan and explain the new scope.
- Record deferred work explicitly instead of silently dropping it.
- When architecture, configuration, public API, or durable decisions change, reconcile README, `.env.example`/config docs, `docs/project-design.md`, `docs/CONTEXT.md`, and `docs/NOW.md` as relevant.
- When the lifecycle stage changes, update this file, `docs/project-design.md`, and `docs/CONTEXT.md`, then review the gap between old-stage and new-stage requirements.
- Risk can override stage: money movement, auth, destructive operations, sensitive data, and irreversible state transitions may require stricter controls even in an MVP.
- Run supervisor mode before completing any substantial phase and before final project completion.
- Before final project completion, run a small smoke test of the product's primary happy paths and verify the canonical repository contains the reviewed state.

## Status values

`not-started` | `in-progress` | `blocked` | `complete` | `deferred`

## Phase template

### Phase N — <name>
Status: `not-started`

Objective:

Scope:
- 

Primary user journeys changed/introduced:
- 

Deliverables:
- 

Verification gates:
- [ ] relevant tests/checks executed and expected work discovered
- [ ] useful discovered/passed/failed counts recorded when relevant
- [ ] lint/type/build checks pass where applicable
- [ ] primary user journeys exercised through the highest practical layer
- [ ] resulting persisted/visible state verified, not only request status
- [ ] at least one important failure path verified where applicable
- [ ] automated vs browser/device/manual vs provider/runtime verification is clear
- [ ] security/auth/tenant/resource-boundary impact reviewed
- [ ] database/migration/invariant impact reviewed
- [ ] error paths and internal-data exposure reviewed
- [ ] supervisor mode executed and reported for substantial phases
- [ ] documentation/config/context reconciled with implementation
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
8. QA, functional acceptance, capacity validation, and production readiness
9. Deployment and launch verification
10. Post-launch measurement, cleanup, and future scaling decisions

A small MVP may legitimately use far fewer phases.

## Stage calibration

### Experiment / spike
Use the fewest phases necessary to answer the question. Do not pretend experimental shortcuts are production-ready.

### Prototype
Prioritize working user flows and feasibility. Keep architecture simple and document shortcuts that must be removed before real-user production use.

### MVP
Real users require real correctness on core workflows, secure defaults, durable persistence/migrations, meaningful tests, functional acceptance of primary journeys, basic observability, backups where needed, and cost-aware infrastructure.

### Production / growth
Add stronger CI/review discipline, operational metrics, alerting, tested recovery, repeatable acceptance/regression checks, runbooks, dependency maintenance, and safer change management.

### High-scale / high-criticality
Add explicit capacity models, SLO/error-budget thinking where useful, stronger failure/load testing, disaster-recovery targets, and distributed architecture only when measured constraints justify it.

See `.engineering/lifecycle/stages.md` for the full rules.
