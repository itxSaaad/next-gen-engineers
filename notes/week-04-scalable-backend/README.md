# Week 4 — Designing a scalable backend system

**Assignment source:** Muhammad Haseeb Malik, [`#next-gen-engineers`, 2026-11-10](https://app.slack.com/archives/C0CA0S502AH/p1794322873661849). Week 5 ([2026-11-17](https://app.slack.com/archives/C0CA0S502AH/p1794929453790629)) explicitly revisits and deepens this assignment because preparation was insufficient.

## Assignment goal

Design a backend that handles hundreds of concurrent users while maintaining performance, data consistency, and reliability. The deliverables are a system diagram and technical design document covering schema and indexes, query optimization, transactions, pooling, cache, API design/rate limits, scaling, failure handling, load tests, and trade-offs. Friday's case study was a **distributed API rate limiter**: compare Fixed Window, Sliding Window, Token Bucket; explain shared Redis state across instances; handle traffic spikes and Redis failure.

## Read in order

1. [Database design and query performance](01-database-and-query-performance.md)
2. [Transactions and concurrency](02-transactions-and-concurrency.md)
3. [Connection pooling and saturation](03-connection-pooling.md)
4. [Caching with Redis](04-caching.md)
5. [API scalability and rate limiting](05-api-and-rate-limiting.md)
6. [Scaling and background work](06-scaling-and-background-work.md)
7. [Reliability, observability, and performance testing](07-reliability-and-performance.md)
8. [AWS infrastructure and compute choices](08-aws-infrastructure.md)
9. [System design deliverables and trade-offs](09-design-and-decisions.md)
10. [Research log and reported activity](10-research-log.md)

The detailed AWS module checklist in chapter 08 comes from the expanded study outline supplied for preparation; it is broader than Haseeb's specific Week 4 assignment brief.

## Core deliverables

- [ ] Diagram clients, load balancer, app instances, APIs, cache, database, workers, request flow, bottlenecks, and scaling points.
- [ ] Technical design explains schema/constraints/indexes, query plans, transactions, pooling, cache policy, API/rate limits, scaling, failure handling, performance tests, and alternatives.
- [ ] Defend choices with traffic spikes, duplicate updates, DB overload, and dependency failures.

Read [Week 5](../week-05-scalable-backend/README.md) for the required deeper follow-up. The guide below explains concepts; the unchecked boxes are assignment artifacts that still need evidence.
