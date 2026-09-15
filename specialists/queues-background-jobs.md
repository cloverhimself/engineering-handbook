# Queues and Background Jobs

Use background processing for work that is slow, retryable, bursty, scheduled, or unnecessary to complete before the user receives a response.

Do not add a queue merely because work is asynchronous. A database-backed job table or platform-native background mechanism may be sufficient at small scale.

Jobs must define: idempotency behavior, retry policy, maximum attempts, timeout, dead-letter/failure handling, observability, ownership, and whether ordering matters.

Assume at-least-once delivery unless the infrastructure explicitly guarantees otherwise. Therefore consumers must tolerate duplicate delivery.

Store durable business facts before enqueuing side effects when consistency matters. Consider an outbox pattern when database state and event publication must stay coordinated.

Avoid unbounded retry loops. Poison jobs must become visible to operators.
