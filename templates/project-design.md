# Project Design

## 1. Problem
What real problem is being solved?

## 2. Users
Who are the users and roles?

## 3. Product profiles
Which profiles from `.engineering/profiles/` apply, and why?

## 4. Lifecycle stage
Current stage: `experiment | prototype | MVP | production/growth | high-scale/high-criticality`

Why this stage applies:

What this stage requires now:

What is intentionally deferred until a later stage:

Risk overrides: note any area that needs stricter controls than the general lifecycle stage because of money movement, sensitive data, auth, destructive operations, irreversible state changes, or compliance obligations.

## 5. Scope
### V1
### Explicitly out of scope

## 6. Core user journeys

## 7. Functional requirements

## 8. Non-functional requirements
Latency, availability, privacy, compliance, accessibility, portability, etc.

## 9. Capacity assumptions
- registered users:
- DAU/MAU:
- peak concurrent users:
- average/peak RPS:
- read/write ratio:
- data growth:
- media/bandwidth:
- geographic distribution:

## 10. Architecture
Describe the simplest architecture that satisfies the requirements and current lifecycle stage.

## 11. Data model and invariants

## 12. Authentication and authorization

## 13. External dependencies
Include failure behavior and cost model.

## 14. Security/threat model

## 15. Money/tax/payment model
If applicable. Include currency, exactness, tax source/configuration, payment lifecycle, refunds, reconciliation.

## 16. Reliability
Timeouts, retries, idempotency, jobs, backups.

## 17. Observability and audit
State what is appropriate for the current lifecycle stage and what is deferred.

## 18. Testing strategy
State the current lifecycle-stage baseline and any stricter domain-specific tests.

## 19. Deployment and environments

## 20. Estimated cost drivers

## 21. Tradeoffs and rejected alternatives

## 22. Scaling triggers
Specify measurable triggers, not vague future concerns.

## 23. Lifecycle transition triggers
What evidence would justify moving this product to the next lifecycle stage?
