# Database Design

Start from business entities, relationships, invariants, and access patterns.

Before schema implementation answer:
- What must be unique?
- What may be null?
- What must remain historically immutable?
- What state transitions are legal?
- Which changes must be atomic?
- Which queries dominate traffic?
- How large can each table become?
- What data requires retention/deletion policies?
- What is auditable?

Normalize transactional data by default. Denormalize deliberately for a measured read/performance need.

Indexes are workload tools. Add them for real filters, joins, sort patterns, uniqueness, and hot queries; verify with query plans where performance matters.

Every migration should be safe for the deployment strategy and include a rollback/forward-fix plan for risky changes.
