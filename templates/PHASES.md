# Project Phases

This file is the living delivery roadmap. The agent must update it as work progresses.

## Rules

- Break the project into coherent phases from initialization through production readiness.
- Each phase must have an objective, scope, deliverables, verification gates, and status.
- Do not mark a phase complete until its required checks were actually run.
- If scope changes, update this file before continuing substantial work.
- Record deferred work explicitly instead of silently dropping it.

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
7. Reliability, observability, and performance
8. QA, load/capacity validation, and production readiness
9. Deployment and launch verification
10. Post-launch cleanup and documented future scaling triggers
