# Database Indexing and Query Optimization

Indexes exist to serve real query patterns, constraints, and ordering needs. Do not index every column.

Before adding an index, identify the query, expected selectivity, sort/filter pattern, write overhead, and whether an existing index already covers the need.

Use `EXPLAIN`/`EXPLAIN ANALYZE` or the database's equivalent before guessing about query performance.

Watch for N+1 queries, unbounded result sets, non-sargable predicates, expensive sorts, repeated full scans, missing pagination, and large joins without appropriate indexes.

Composite index column order must match the dominant filtering/sorting pattern. Remove redundant or unused indexes when evidence supports it.

Pagination should use deterministic ordering. Prefer keyset/cursor pagination for large or frequently changing datasets when offset pagination becomes expensive or inconsistent.

Optimize after measuring. Schema clarity and correctness come before micro-optimizing ordinary queries.
