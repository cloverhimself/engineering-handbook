# Testing Strategy

Test the behavior whose failure would matter.

Prioritize:
- business invariants;
- auth and permissions;
- data integrity;
- state transitions;
- payment success/failure/duplicate flows;
- retry/idempotency behavior;
- integration with persistence;
- public API contracts;
- critical user journeys.

Avoid excessive mocking that causes tests to pass while integrations are broken. Prefer real database integration tests for meaningful persistence behavior where feasible.

Performance testing should model realistic concurrency, payloads, think time, and bottlenecks rather than chasing arbitrary request counts.
