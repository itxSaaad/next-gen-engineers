# Week 4 — Designing a Scalable Backend System

## Curriculum Overview

Week 4 focuses on architecting backend systems that sustain high concurrency while maintaining sub-second latency, transactional consistency, and fault tolerance.

---

## Assignment Goals & Deliverables

1. **System Architecture Blueprint**: Multi-tier architecture diagram showing request flow across reverse proxies/load balancers, stateless API servers, PgBouncer connection pools, PostgreSQL primary/read replicas, Redis cache clusters, and asynchronous Celery workers.
2. **Technical Design Document**:
   - Relational schema modeling and composite indexing strategies.
   - SQL query optimization, N+1 query elimination, and execution plan benchmarks.
   - ACID transaction boundaries, locking mechanisms, and deadlock avoidance.
   - Connection pool sizing formulas for high-concurrency workloads.
   - Redis caching policies (Cache-Aside, Write-Through, TTL strategies).
   - Distributed rate-limiting architecture (Fixed Window vs Sliding Window vs Token Bucket).
   - Auto-scaling policies, failure modes, and catastrophic recovery plans.
3. **Distributed Rate Limiter Case Study**:
   - Shared Redis state management across stateless application instances.
   - Lua scripting for atomic rate checking and token decrements.
   - Behavior during Redis failover and network partitions.

---

## Reading Guide

1. [Database Design & Query Performance](01-database-and-query-performance.md)
2. [Transactions & Concurrency Control](02-transactions-and-concurrency.md)
3. [Connection Pooling & Saturation](03-connection-pooling.md)
4. [Caching with Redis](04-caching.md)
5. [API Scalability & Rate Limiting](05-api-and-rate-limiting.md)
6. [System Scaling & Asynchronous Background Tasks](06-scaling-and-background-work.md)
7. [Reliability, Observability & Performance Testing](07-reliability-and-performance.md)
8. [AWS Cloud Infrastructure & Compute Topology](08-aws-infrastructure.md)
9. [System Design Deliverables & Trade-off Matrices](09-design-and-decisions.md)
10. [Research Log](10-research-log.md)
