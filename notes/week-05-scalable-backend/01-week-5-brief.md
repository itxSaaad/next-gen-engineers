# 01 — Week 5 Brief: Production Scenarios & Deep Backend Engineering

## Module Objective

Week 5 deepens scalable-backend architecture with a strict focus on production failure modes, concurrency, high-throughput caching, and API scalability. The curriculum standard requires justifying technical trade-offs with empirical metrics and defending system behavior under extreme failure scenarios.

---

## Core Focus Topics

1. **Database Architecture & Query Optimization**: Relational schema modeling, normalization vs selective denormalization, composite indexing, and EXPLAIN ANALYZE execution plan breakdown.
2. **Transactions & Concurrency Control**: ACID properties, isolation levels (Read Committed vs Repeatable Read vs Serializable), pessimistic (`SELECT FOR UPDATE`) vs optimistic locking, and deadlock resolution.
3. **Database Connection Pooling**: Sizing formulas, client pool vs proxy pool (PgBouncer in transaction pooling mode), and connection saturation protection.
4. **Redis Caching Architecture**: Hierarchical key design, tiered TTL policies, cache-aside vs write-through, stampede mitigation, and cache invalidation.
5. **High-Volume API Scalability**: Keyset (cursor-based) pagination vs offset pagination, indexing for multi-attribute filtering, and payload compression.
6. **Distributed Rate Limiting**: Token-Bucket and Sliding-Window algorithms implemented via atomic Redis Lua scripts with tiered rate policies.
7. **Production Reliability & Outage Behavior**: Circuit breaker patterns, fail-open vs fail-closed strategies, and database load shedding during Redis outages.

---

## Production Stress Scenarios to Defend

- **Traffic Spikes**: 10x traffic surges hitting uncached candidate assessment endpoints.
- **Concurrent Submissions**: Multiple simultaneous submissions of the same assessment payload.
- **Database Overload**: Connection exhaustion and runaway queries saturating CPU.
- **Redis Outage**: Complete Redis node termination or network partition while maintaining high API availability.

---

## Recommended References
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [PostgreSQL Connection Pool Sizing Guidance](https://wiki.postgresql.org/wiki/Number_Of_Database_Connections)
- [Redis Memory Eviction & Key Expiration Policies](https://redis.io/docs/latest/develop/reference/eviction/)
- [Designing for High Throughput (1M req/sec)](https://www.youtube.com/watch?v=W4EwfEU8CGA)
