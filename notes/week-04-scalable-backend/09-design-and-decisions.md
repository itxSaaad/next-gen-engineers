# 08 — System design deliverables and technical decisions

Haseeb requested a diagram with clients, load balancer, application instances, APIs, cache, database, background workers, request flow, bottlenecks, and scaling points. The technical document must explain schema/indexes/constraints, query optimization, transactions, pooling, caching, API/rate limiting, scaling, failure handling, testing, and alternatives.

## Design document template

1. **Requirements and assumptions:** concurrent users, read/write mix, data size, latency/availability, consistency, retention, and security.
2. **Architecture:** component diagram plus request and async flows; name source of truth.
3. **Data:** entity model, constraints, indexes, access patterns, and migration plan.
4. **Concurrency:** transaction boundaries, isolation, locking/versioning, idempotency.
5. **Capacity:** rough request/connection/queue calculations and limiting dependency.
6. **Cache/API:** freshness contract, pagination, rate-limit identity/algorithm, overload response.
7. **Failure behavior:** DB/cache/app/queue outage, timeout, retry, recovery, and data loss boundary.
8. **Verification:** load profile, failure injection, correctness invariants, telemetry, SLOs.
9. **Alternatives:** why selected design fits assumptions; cost and trigger to revisit.

## Production scenarios

- Traffic spike: what queues, what sheds load, and what must remain interactive?
- Duplicate update after client timeout: which key/constraint prevents a second effect?
- DB overload: where does backpressure occur, and how are connections protected?
- Redis failure: what is the bounded fallback and which flows fail closed?
- One app instance dies: where is state persisted and how does work resume?

The [Week 5 guide](../week-05-scalable-backend/README.md) deepens these same areas. Week 4's brief establishes deliverables, not completed research.
