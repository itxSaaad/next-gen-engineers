# Week 1 — Engineering Fundamentals & System Design

## Curriculum Overview

Week 1 establishes foundational software engineering principles, clean code standards, architectural separation of concerns, and hands-on system architecture analysis.

The engineering focus is to present production architectures, explain architectural trade-offs, and reason through scalability, fault tolerance, database performance, caching layers, asynchronous queues, observability, and structural bottlenecks.

---

## Core Topics

- **Clean Code & Readability**: Self-documenting code, cohesion, function complexity, and maintainable abstractions.
- **SOLID Principles**: Practical application of Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.
- **Architectural Layering**: Decoupling Controller / Presentation → Service / Domain Logic → Repository / Persistence layers via Dependency Injection.
- **Technical Debt Management**: Distinguishing deliberate architectural trade-offs from reckless code rot; refactoring strategies.

---

## Production System Analysis Focus

Architectural diagrams and design reviews focus on production-grade systems across distinct distributed patterns:

1. **Financial Ledger & Payment Integration Engine (Bluesky / Paymentology)**: Double-entry ledger consistency, idempotent payment webhooks, replay safety, and database concurrency locks.
2. **Distributed Workflow Engine (Prefect)**: Resilient task graph orchestration, worker heartbeat monitoring, and distributed task state tracking.
3. **High-Throughput Queue Processing (SQS)**: Asynchronous event ingestion, dead-letter queue routing, and worker backpressure management.
4. **Edge Telemetry Ingestion (ShipIn)**: Offline-capable edge buffering, intermittent network synchronization, and batch cloud ingestion.

---

## Shared System Design Case Study: Distributed URL Shortener

Design a high-scale URL Shortener service (e.g., bit.ly / tinyurl):
- Short code generation algorithms (Base62 encoding vs MD5/SHA256 truncation vs KGS - Key Generation Service).
- Database schema design, read/write ratio analysis (100:1 read-heavy), and indexing strategies.
- HTTP redirect semantics (301 Permanent Redirect vs 302 Found) and their impact on analytics.
- Redis caching layers, eviction policies (LRU), and cache stampede protection.
- High availability, database sharding by hash prefix, and failure recovery.

---

## Reading Guide

1. [Code Quality & Clean Code](01-code-quality.md)
2. [SOLID Principles in Production](02-solid-principles.md)
3. [Architectural Fundamentals & Layering](03-architectural-fundamentals.md)
4. [Technical Debt & Maintainability](04-maintainability-and-debt.md)
5. [Production System Architectures & Reference Diagrams](05-assigned-systems.md)
6. [Distributed URL Shortener Design](06-url-shortener.md)
7. [Research Log & Technical Topics](07-research-log.md)
