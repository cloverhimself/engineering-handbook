# Project Context

This file stores **durable project facts** for AI agents and developers. Keep it concise, factual, and current.

Do not use it as a chat transcript or active-task diary. Active work belongs in `docs/NOW.md`.

## Project

Name:
Purpose:
Primary users:
Current stack:
Repository:
Current lifecycle stage: `experiment | prototype | MVP | production/growth | high-scale/high-criticality`
Why this stage applies:
Selected profiles:

## Architecture summary

Applications/services:
Database/storage:
Authentication/authorization:
Important domain boundaries:
External integrations:
Deployment/runtime:

## Critical invariants

- 

Examples: tenant isolation, unique payment references, inventory cannot fall below allowed rules, balances derive from ledger entries.

## Decisions that must not be rediscovered

- Decision:
  Reason:
  Reference/ADR:

## Long-lived constraints

- 

Examples: required provider, deployment restriction, compatibility contract, regulatory input that was explicitly supplied.

## Active assumptions

- Assumption:
  Confidence:
  Needs confirmation from:

## Known persistent risks / technical debt

- 

## Verification baseline

Last known production/release state:
Important test suites/checks:
Known persistent failing checks:

Do not use this section as proof that old checks still pass after new changes. Current-task verification belongs in `docs/NOW.md`.

## Lifecycle review

Has the project outgrown its current lifecycle stage? `yes/no`
Evidence:
Next-stage gaps, if any:
- 

## Context rules

- Keep this file short enough for a new agent to scan quickly.
- Move detailed decisions to ADRs/design docs and reference them here.
- Update only when durable project facts change.
- Do not duplicate `PHASES.md` or `NOW.md`.
- Git history preserves old versions; remove stale facts instead of accumulating history.

## New-session protocol

1. Read root `AGENTS.md`.
2. Read `docs/NOW.md`.
3. Read this file.
4. Verify Git branch/status.
5. Inspect only files relevant to the current task.
6. Read `PHASES.md`, design docs, ADRs, or specialist handbook modules only when the task requires them.

See `.engineering/workflow/context-budget.md` for the full context discipline.