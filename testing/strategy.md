# Testing Strategy

Test the behavior whose failure would matter.

Prioritize:
- business invariants;
- auth and permissions;
- tenant/resource boundaries;
- data integrity;
- state transitions;
- payment success/failure/duplicate flows;
- retry/idempotency behavior;
- integration with persistence;
- public API contracts;
- critical user journeys.

Avoid excessive mocking that causes tests to pass while integrations are broken. Prefer real database integration tests for meaningful persistence behavior where feasible.

A passing command is evidence only for what it actually exercised. When discovery matters, report useful counts such as tests discovered/passed/failed. A test runner that exits successfully after discovering zero relevant tests does not prove the intended test foundation exists.

Distinguish verification categories explicitly:
- automated unit/integration/API/E2E tests;
- manual/browser/device UI verification;
- provider/environment verification;
- unverified assumptions.

Do not claim backend/API integration tests verify frontend state transitions, payload shaping, routing, browser behavior, or client/server integration unless they actually exercise them.

For user-facing features, follow `workflow/functional-acceptance.md`. At least one acceptance check should use the same realistic payload/sequence as the actual client. If the UI sends dates, optional fields, assignees, files, money, or other structured values, do not rely on a narrower API test that omits them.

Critical authorization tests should attempt cross-tenant/cross-parent access through direct child IDs, not only normal route flows. Validate the full ownership chain from authenticated user to tenant/workspace to parent resource to child resource.

For structured inputs such as dates, enums, IDs, amounts, and file metadata, test invalid values and boundary semantics when those rules matter to the product.

Before a user-facing MVP/release is called complete, run a small smoke test of the primary journeys from a realistic starting state. The purpose is to catch integration failures that isolated tests can miss.

When a real user-visible defect escapes, add the cheapest regression protection at the layer that would have caught it. Do not only patch the bug.

Performance testing should model realistic concurrency, payloads, think time, and bottlenecks rather than chasing arbitrary request counts.

Testing depth should remain proportional to lifecycle stage and risk. Do not add a heavy browser/E2E framework merely to satisfy a checklist when a lightweight browser/manual smoke check provides sufficient confidence for the current MVP. Add stronger automation when regression risk, release frequency, team size, or product criticality justifies it.
