# Week 5 — Scalable Backend (Week 4 continuation)

**Week:** 2026-11-16 to 2026-11-22 (Pakistan time)
**Assignment/source:** Muhammad Haseeb Malik, `#next-gen-engineers`, 2026-11-17.

Haseeb said preparation for Week 4 had been insufficient, so Week 5 revisits the same areas and expects deeper understanding and production application. The standard is to justify choices and reason through failure cases, not just define terms. See [Week 4 assignment and foundations](../week-04-scalable-backend/README.md).

## This week's focus
- Database design: relationships, normalization, constraints, indexing.
- SQL performance: query plans, N+1 problems, slow-query analysis.
- Transactions and concurrency: ACID, isolation, locking, deadlocks, race conditions.
- Connection pooling: pool sizing, connection limits, saturation.
- Caching: Redis, TTLs, invalidation, consistency.
- API scalability: pagination, filtering, rate limiting, efficient responses.
- System scaling: load balancing, horizontal scaling, background workers.
- Reliability/performance: load testing, bottleneck identification, timeouts, retries, failure handling.
- Apply to production scenarios: traffic spikes, duplicate updates, database overload, Redis or app-instance failure.

## Expected preparation
- [ ] Review the Week 4 assignment and bring the system design diagram.
- [ ] Bring technical decisions, trade-offs, and open questions.
- [ ] Be ready to justify designs through production scenarios, not just define terms.
- [ ] Record sources and what each source helped clarify in the research log.

## Read in order

1. [Assignment brief and production scenarios](01-week-5-brief.md)
2. [Database design and SQL performance](02-database-and-sql.md)
3. [Transactions and concurrency](03-transactions-and-concurrency.md)
4. [Connection pooling](04-connection-pooling.md)
5. [Caching](05-caching.md)
6. [API scalability and rate limiting](06-api-scalability-rate-limiting.md)
7. [Scaling, reliability, and performance](07-scaling-reliability-performance.md)
8. [Technical design and decision record](08-design-decisions.md)
9. [Research log](09-research-log.md)

## Learning resources shared by Haseeb
- [System Design Primer](https://github.com/donnemartin/system-design-primer) — architecture, scalability, load balancing, caching, replication, trade-offs.
- [PostgreSQL: Number of Database Connections](https://wiki.postgresql.org/wiki/Number_Of_Database_Connections) — connection limits, pooling, and why more connections may hurt performance.
- [Redis key eviction](https://redis.io/docs/latest/develop/reference/eviction/) — memory limits, eviction strategies, cache behavior.

## Daily time target
Haseeb's Week 4 expectation: 1 hour/day, 5 hours/week. Track actual time and learning below.

| Date | Time | Topic / activity | Key takeaway | Follow-up |
|---|---:|---|---|---|
| 2026-11-16 |  |  |  |  |
| 2026-11-17 |  |  |  |  |
| 2026-11-18 |  |  |  |  |
| 2026-11-19 |  |  |  |  |
| 2026-11-20 |  |  |  |  |

## Assignment brief

Haseeb's 2026-11-17 message explicitly continues Week 4 because the group was insufficiently prepared. It lists database design, SQL performance, transactions/concurrency, pooling, caching, API scalability, system scaling, reliability/performance, and scenarios: traffic spikes, duplicate updates, DB overload, Redis/app-instance failures. See [chapter 01](01-week-5-brief.md) for the full brief and [Week 4](../week-04-scalable-backend/README.md) for foundations.

Haseeb's latest channel post on 2026-11-18 is a [video link about handling one million requests per second](https://www.youtube.com/watch?v=W4EwfEU8CGA), shared without explanatory text.
