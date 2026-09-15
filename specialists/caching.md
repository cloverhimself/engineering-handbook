# Caching Strategy

Do not add a cache before identifying a measurable problem.

Caches trade latency and load reduction for invalidation, staleness, failure modes, operational cost, and debugging complexity.

Prefer the simplest cache appropriate to the problem: browser/CDN cache for public static content, in-process cache for process-local immutable/reference data, shared cache only when multiple instances need the same hot data or coordination.

Define ownership, TTL, invalidation strategy, acceptable staleness, fallback behavior, and metrics before production use.

Never make correctness depend on a cache unless the cache is intentionally the system of record.

Cache keys must include every dimension that affects the result, especially tenant, user, locale, permissions, and version where applicable.
