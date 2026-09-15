# Concurrency and Locking

Assume concurrent requests can race whenever multiple actors can update the same state.

Prefer database constraints, atomic statements, compare-and-set/version columns, and short transactions before introducing application-level distributed locks.

Use pessimistic row locks only when concurrent writers must serialize and contention is acceptable. Use optimistic concurrency when conflicts are expected to be uncommon and retries are safe.

Never hold database locks across slow network calls. Keep transactions short.

Protect critical transitions such as inventory reservation, balance movement, one-time token consumption, job claiming, and order/payment state changes from double execution.

Design retries carefully: a retry after a conflict must not duplicate irreversible side effects.
