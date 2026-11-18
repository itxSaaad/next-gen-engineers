# 02 — Production System Architectures & Reference Diagrams

A comprehensive engineering evaluation requires clear architecture diagrams showing components, data flow, external integrations, boundary contexts, and how foundational engineering principles apply.

| Architecture Archetype | System Scope / Focus | Primary Technology Stack |
|---|---|---|
| Distributed Workflow Engine | Workflow orchestration & resilient task DAGs | Prefect, Python, PostgreSQL, Docker |
| Asynchronous Queue Pipeline | High-throughput event publishing & dead-letter routing | AWS SQS, Celery, Redis |
| **Financial Ledger & Payment Gateway** | **Double-entry consistency, idempotent payments, ledger auditing** | **FastAPI/Django, Paymentology API, PostgreSQL, Redis** |
| Edge Telemetry Ingestion Platform | Intermittent connectivity, edge buffers, batch ingestion | Edge SQLite, MQTT, REST, AWS S3 |

---

## Diagramming Standards & Methodology

1. **System Scope & Boundary**: Explicitly document user actors, system boundaries, use cases, and non-goals.
2. **Components & Interfaces**: Differentiate API gateways, application services, persistence layers (PostgreSQL), memory stores (Redis), message queues (SQS/Celery), and external third-party processors (e.g. Paymentology).
3. **Data Flows & Protocols**: Distinguish synchronous HTTP/REST from asynchronous events; document payload schemas and direction of ownership.
4. **Resilience & Failure Topography**: Annotate persistence points, retry mechanisms, idempotency keys, timeout budgets, circuit breakers, and dead-letter queues.
5. **Architectural Trade-offs**: Justify why each component is chosen over alternatives, identifying latency, consistency, and operational cost boundaries.
6. **Code & Structural Principles**: Enforce single-responsibility modules, loose coupling via Dependency Injection, and strict separation between domain logic and external infrastructure.

---

## Review Checklist

- [ ] System boundaries and client entry points are clearly delimited.
- [ ] Data flows and third-party integrations are explicitly labeled with protocol and payload direction.
- [ ] Synchronous RPC paths and asynchronous message queues are clearly differentiated.
- [ ] Failure recovery, exponential backoff retries, and idempotency mechanisms are documented.
- [ ] Bottlenecks, database lock contention points, and horizontal scaling tiers have documented rationales.
- [ ] All architectural decisions include measurable trade-offs and mitigation plans.
