# 01 — Database design and query performance

The assignment explicitly calls for relationships, normalization, constraints, indexes, query plans, N+1 detection, and slow-query analysis.

## Model and enforce invariants

Start from entities, ownership, cardinality, and access patterns. Normalize duplicated facts to avoid update anomalies; denormalize only for a measured read/latency need and define how the copy stays correct. Use primary keys, foreign keys, `NOT NULL`, `UNIQUE`, and `CHECK` constraints to make invalid states hard to persist. Constraints are the final concurrent guard where application-side prechecks can race.

## Index for real queries

Indexes trade write cost and storage for lookup speed. Choose columns/order from predicates, joins, and sort patterns; a composite index's leading columns matter. A partial index covers a subset under a predicate; a covering/index-only plan may serve selected columns from the index when visibility conditions allow. Avoid indexing every column. Check whether the index is used under representative data. PostgreSQL's [index documentation](https://www.postgresql.org/docs/current/indexes.html) and [index usage guidance](https://www.postgresql.org/docs/17/indexes-examine.html) explain index types and examination.

## Data lifecycle and tenancy

Plan migrations alongside the schema: additive change, backfill, dual-read/write only when needed, then remove old columns after compatible clients are gone. Multi-tenant systems must include tenant ownership in authorization and relevant query/index design. Audit/history tables preserve change evidence but increase storage and retention obligations. Choose soft delete when restore/history is a product requirement; otherwise hard delete may better satisfy data minimization. Decide this from lifecycle/retention requirements rather than convention.

## Diagnose before tuning

Use `EXPLAIN` to inspect scan and join choices, estimated rows, and cost; use `EXPLAIN (ANALYZE, BUFFERS)` carefully on safe queries to compare actual rows/timing and I/O. `ANALYZE` statistics inform planner estimates, so stale or skewed data can explain a poor plan ([Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html), [ANALYZE](https://www.postgresql.org/docs/current/sql-analyze.html)). Instrument query count and duration per request to detect N+1 patterns: repeated child queries usually call for joins, eager/batched loading, or an explicit endpoint contract.

## Investigation sequence

Capture the slow query, parameters/data scale, query count, plan, and baseline p50/p95. Change one thing, rerun with representative data, and compare read latency, write latency, index size, and lock impact. A sequential scan can be correct for small tables or broad retrieval; do not force an index just because one exists.
