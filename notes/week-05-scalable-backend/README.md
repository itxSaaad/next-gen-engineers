# Week 5 — Scalable Backend: Deep Production Scenarios & Redis Architecture

## Curriculum Overview

Week 5 deepens backend scalability, moving beyond definitions into rigorous architectural defense, production resilience, and hands-on deliverables. The core evaluation bar requires defending technical choices under production stress and handling systemic failures.

---

## Core Focus Areas

1. **Relational Data Modeling & Indexing**: Composite indexes matching queries, covering indexes, and eliminating table scans.
2. **Transactions & Isolation**: Preventing dirty reads, non-repeatable reads, phantom reads, and write skew.
3. **Connection Pooling (PgBouncer)**: Transaction-level pooling to handle thousands of application worker connections without exhausting PostgreSQL memory.
4. **Redis Multi-Tier Caching**: Key naming conventions, serialization formats, TTL policies, and stampede prevention.
5. **High-Volume API Scalability**: Cursor pagination, filtering pipelines, and sparse response projections.
6. **Distributed Rate Limiting**: Shared state across stateless containers via Redis Lua scripts.
7. **Failure Recovery & Circuit Breaking**: Protecting the primary database when Redis fails; fail-open vs fail-closed policies.

---

## Deliverables & Documentation

- [01 — Week 5 Brief & Production Scenarios](01-week-5-brief.md)
- [02 — Database Design & SQL Optimization](02-database-and-sql.md)
- [03 — Transactions, Locking & Concurrency](03-transactions-and-concurrency.md)
- [04 — Connection Pooling & Saturation](04-connection-pooling.md)
- [05 — Caching Strategy & Redis Patterns](05-caching.md)
- [06 — API Scalability & Rate Limiting](06-api-scalability-rate-limiting.md)
- [07 — System Scaling, Reliability & Performance](07-scaling-reliability-performance.md)
- [08 — Architecture Decision Records (ADRs)](08-design-decisions.md)
- [09 — Research Log](09-research-log.md)
