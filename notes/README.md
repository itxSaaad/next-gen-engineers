# Next-Gen Engineers — Study Notes & Architectural Research

This directory contains comprehensive, source-referenced study guides and research logs covering system design, scalable architecture, and production engineering practices across the entire curriculum.

---

## 📚 Curriculum Index

| Module | Focus Area | Key Architectural Deliverables & Topics |
| :--- | :--- | :--- |
| **[Program Guide](00-program-guide.md)** | Overview | Engineering objectives, primary technology stack, and curriculum roadmap |
| **[Week 1](week-01-engineering-fundamentals/README.md)** | Engineering Fundamentals | Clean Code, SOLID, architectural layering, DI, and URL Shortener system design |
| **[Week 2](week-02-reliable-desktop-sync/README.md)** | Reliable Desktop Sync | Offline-first synchronization, local SQLite queues, event-driven state machines, and retry protocols |
| **[Week 3](week-03-data-consistency-security-scaling/README.md)** | Consistency, Security & Scaling | Conflict resolution, idempotency keys, device fingerprinting, and large-data chunked sync |
| **[Week 4](week-04-scalable-backend/README.md)** | Scalable Backend Architecture | Query optimization, connection pooling (PgBouncer), caching tiers, and distributed rate limiting |
| **[Week 5](week-05-scalable-backend/README.md)** | Production Backend & Redis Scalability | High-volume candidate & assessment APIs, cursor pagination, cache stampede prevention, and outage resilience |

---

## 🛠️ Technology Stack & Standards
- **Core Languages**: Python (FastAPI, Django, DRF)
- **Persistence & Caching**: PostgreSQL, PgBouncer, Redis
- **Message Queues**: Celery, Redis Streams, AWS SQS
- **Architecture Paradigms**: Domain-Driven Design (DDD), Event-Driven Architecture (EDA), Cache-Aside, Token-Bucket Rate Limiting
