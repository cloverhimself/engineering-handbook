# Production Reliability

Every external call needs a failure policy: timeout, retry policy, idempotency behavior, error mapping, and observability.

Retries are not a substitute for correctness. Retry only errors likely to succeed later, with bounded attempts and backoff.

Use database transactions for atomic business changes. Use outbox/queue patterns only when cross-system delivery reliability requires them.

Jobs must tolerate process termination and duplicate execution when the job system provides at-least-once delivery.

Backups are meaningful only if restoration is possible; production data plans should include restore testing appropriate to business risk.
