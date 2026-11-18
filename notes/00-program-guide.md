# 00 — Program Guide: System Design, Architecture, and Engineering Leadership

## Program Rationale & Objectives

This structured engineering program is designed to develop system-design excellence, architectural judgment, production ownership, and technical communication. The intended outcome is to design, scale, and operate maintainable, fault-tolerant distributed systems in production.

---

## Core Curriculum Pillars

1. **System-Design Fundamentals & Engineering Principles**: Modular decomposition, high cohesion, loose coupling, and clean interfaces.
2. **Software Architecture & Patterns**: Layered architecture, Domain-Driven Design (DDD), Dependency Injection, and Event-Driven Architecture.
3. **Database Architecture, Optimization & Scaling**: Schema modeling, indexing strategies, normalization/denormalization, ACID semantics, connection pooling, and read replicas.
4. **Caching, Messaging & Asynchronous Processing**: Redis multi-tier caching, cache-aside/write-through patterns, stampede mitigation, Celery task pipelines, and dead-letter queues.
5. **Distributed Systems & Fault Tolerance**: CAP theorem, consensus, idempotency keys, distributed locks, circuit breakers, and bulkheads.
6. **Scalability & Performance Engineering**: Keyset pagination, query optimization, horizontal auto-scaling, load balancing, and rate limiting.
7. **Infrastructure & Cloud Architecture**: Docker containerization, AWS compute tiers (ECS/EC2/Fargate), VPC networking, and security perimeters.
8. **Observability & Reliability**: Structured logging, Prometheus metrics, distributed tracing, error budgets, and SLA/SLO definition.
9. **Production Incident Management & Security**: Threat modeling, rate limiting, least-privilege RBAC, and disaster recovery.
10. **Engineering Leadership & Decision Defense**: Architecture Decision Records (ADRs), trade-off matrices, and technical design defense.

---

## Primary Technology Stack
- **Languages & Frameworks**: Python, FastAPI, Django, Django REST Framework
- **Data & Caching**: PostgreSQL, Redis, PgBouncer
- **Async & Background Processing**: Celery, Redis Streams, AWS SQS
- **Infrastructure & Cloud**: Docker, AWS (ECS, ALB, RDS, ElastiCache, S3)

---

## Weekly Module Roadmap

- **[Week 1: Engineering Fundamentals & Clean Code](week-01-engineering-fundamentals/README.md)**: SOLID principles, architectural layering, assigned system analysis, and URL Shortener system design.
- **[Week 2: Reliable Desktop Synchronization](week-02-reliable-desktop-sync/README.md)**: Offline-first synchronization, local SQLite queues, event-driven state machines, and retry protocols.
- **[Week 3: Data Consistency, Security & Large Data Sync](week-03-data-consistency-security-scaling/README.md)**: Conflict resolution, idempotent event ordering, mutual TLS/device fingerprinting, and chunked large-payload sync.
- **[Week 4: Scalable Backend Architecture](week-04-scalable-backend/README.md)**: Database optimization, connection pooling with PgBouncer, caching tiers, distributed rate limiting, and horizontal scaling.
- **[Week 5: Deep Production Scenarios — Redis Caching & API Scalability](week-05-scalable-backend/README.md)**: High-concurrency candidate and assessment APIs, keyset pagination, cache invalidation, stampede prevention, and Redis failure handling.

---

## Engineering Study Methodology

For each architectural concept and deliverable:
1. **Define the Invariant**: What absolute rule must the system never violate (e.g. zero double-spends, exactly-once processing semantics)?
2. **Evaluate Alternatives**: Compare at least two viable patterns with an explicit trade-off matrix.
3. **Model the Failure Modes**: Walk through network partitions, process crashes, database timeouts, duplicate messages, and cache outages.
4. **Verify & Benchmark**: Implement runnable proofs-of-concept, measure p99 latency, throughput, and error rates.
5. **Document Architecture Decision Records (ADRs)**: Defend all architectural choices with empirical evidence and clear constraints.
