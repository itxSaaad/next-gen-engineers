# 02 — Database design and SQL performance

Week 5 calls for deeper work on relationships, normalization, constraints, indexes, query plans, N+1 patterns, and slow queries. See [Week 4 foundations](../week-04-scalable-backend/01-database-and-query-performance.md).

## Study guide

1. Model entities/cardinality from business rules. Normalize to keep each fact authoritative and avoid update anomalies. Treat denormalization as an intentional read optimization with a synchronization strategy.
2. Encode invariants in `NOT NULL`, foreign keys, unique constraints, and checks. Application validation improves feedback, but DB constraints arbitrate concurrent writers.
3. Derive indexes from predicates, joins, and sort orders. Composite column order matters; indexes cost storage and writes. Inspect plans on representative data.
4. Use `EXPLAIN`/`EXPLAIN ANALYZE` to compare estimates and actual rows, scans, joins, loops, buffers. Keep planner statistics fresh; PostgreSQL `ANALYZE` feeds the planner ([EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html), [ANALYZE](https://www.postgresql.org/docs/current/sql-analyze.html)).
5. Detect N+1 with per-request query counts and repeated child lookups. Consider joins, eager loading, prefetch, batching, or an endpoint contract that loads related records together.

## Practice questions

- What are the entities, relationships, and invariants?
- Which queries dominate workload, and what indexes support them?
- How do plans change at representative volume and skew?
- What telemetry locates slow SQL without exposing sensitive bind values?

## References

- [PostgreSQL: Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)
- [PostgreSQL: ANALYZE](https://www.postgresql.org/docs/current/sql-analyze.html)
- [PostgreSQL: Examining index usage](https://www.postgresql.org/docs/17/indexes-examine.html)
