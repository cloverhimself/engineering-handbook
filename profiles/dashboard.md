# Dashboard Profile

Use for analytics, reporting, operations, admin, BI, or monitoring dashboards.

Priorities:
- define metric ownership, freshness, and source of truth explicitly;
- distinguish operational data from derived analytics;
- avoid expensive unbounded aggregate queries on request paths;
- precompute, cache, or materialize expensive metrics only when measured need justifies it;
- paginate large tables and bound date ranges;
- make filters and sorting predictable and index-supported where possible;
- enforce permissions server-side for every dataset and action;
- separate read-heavy reporting concerns from transactional write flows when needed;
- show data freshness and partial-failure states honestly;
- avoid silently mixing currencies, time zones, units, or incompatible date windows;
- use clear visual hierarchy and accessible interaction patterns;
- audit destructive admin actions when the dashboard also controls operational state.
