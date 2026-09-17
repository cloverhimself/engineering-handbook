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
- manual UI/runtime verification;
- provider/environment verification;
- unverified assumptions.

Do not claim backend/API integration tests verify frontend state transitions or browser behavior unless they actually exercise them.

Critical authorization tests should attempt cross-tenant/cross-parent access through direct child IDs, not only normal route flows. Validate the full ownership chain from authenticated user to tenant/workspace to parent resource to child resource.

For structured inputs such as dates, enums, IDs, amounts, and file metadata, test invalid values and boundary semantics when those rules matter to the product.

Performance testing should model realistic concurrency, payloads, think time, and bottlenecks rather than chasing arbitrary request counts.

Testing depth should remain proportional to lifecycle stage and risk. Do not add a heavy browser/E2E framework merely to satisfy a checklist when build/manual verification is sufficient for the current MVP; add stronger automation when the risk, regression rate, team size, or release process justifies it.
