# Functional Acceptance

Engineering checks are not enough if the product workflow itself does not work.

For user-facing applications, a phase that implements a user journey is not complete until the journey has been exercised through the highest practical layer available.

## Core rule

Verify the product as a user would experience it, not only the individual layers underneath it.

Examples:
- login -> create workspace -> create project -> create task -> see the task;
- add product -> add to cart -> checkout -> payment state updates;
- upload file -> file appears -> authorized user can retrieve it;
- submit form -> persisted result appears after refresh.

An API test proving `POST /tasks` works does not prove the task-creation form works. A frontend build does not prove a button submits the expected payload. A database constraint test does not prove the end-to-end flow reaches that database path correctly.

## Acceptance ladder

Use the highest practical layer for each critical journey:

1. Browser/device end-to-end automation when already available or clearly justified.
2. Lightweight browser/manual smoke test when full E2E tooling would be disproportionate.
3. API/integration tests that reproduce the exact payload and sequence used by the client.
4. Unit tests only for isolated logic; never use them alone as proof of a complete user journey.

Do not add Cypress, Playwright, Appium, or another heavy tool automatically. The goal is confidence in the workflow, not tooling for its own sake.

## Realistic inputs

Acceptance checks must exercise realistic boundary values and the same shapes the client sends, including relevant:
- dates/date-times/timezones;
- enum values;
- nullable/optional fields;
- identifiers;
- assignees/owners;
- files;
- money/currency;
- pagination/filter/query values;
- provider responses.

If the UI sends a different payload from an existing API test, add coverage for the actual UI payload or verify the UI flow directly.

## Phase gate

Before completing a phase that changes a critical user journey:
- identify the journeys introduced or changed;
- exercise each journey end-to-end or record why that layer is unavailable;
- verify the persisted/resulting state, not only the HTTP status;
- verify at least one important failure path;
- record whether evidence is automated or manual.

If a critical journey remains unverified, mark the phase as not fully verified. Do not describe the feature as fully functional.

## Release smoke test

Before a user-facing MVP/release is called complete, run a short product smoke test covering the primary happy paths from a clean/realistic starting state.

The smoke test should be small enough to run repeatedly. Prefer the few journeys whose failure would make the product unusable.

## Regression rule

When a real user-visible bug escapes verification, add the cheapest durable regression protection at the layer that would have caught it.

Do not merely fix the bug and move on. Ask why the previous verification allowed it through.
