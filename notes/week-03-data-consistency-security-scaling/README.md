# Week 3 — Data Consistency, Security & Large-Scale Synchronization

## Curriculum Overview

Week 3 bridges reliable edge synchronization with distributed backend consistency, addressing distributed conflicts, secure communication across untrusted networks, and scaling ingestion pipelines for large assessment payloads.

---

## Core Topics & Engineering Deliverables

1. **Conflict Resolution & Idempotency**: Last-Write-Wins (LWW) vs operational transforms vs deterministic vector clocks; database-enforced unique idempotency keys.
2. **Event Ordering & Causality**: Monotonic sequencing, distributed timestamps, and out-of-order event buffering.
3. **Security, Trust & Device Integrity**: Device fingerprinting, asymmetric request signing, mutual TLS, and token replay defense.
4. **Large-Data Synchronization**: Chunked file upload protocols, resumable HTTP transfers, content-addressable storage (S3 pre-signed URLs), and backend backpressure.
5. **API Protocol Trade-offs**: Evaluating REST, WebSockets, gRPC, and Server-Sent Events (SSE) for assessment telemetries.

---

## Reading Guide

1. [Architectural Scope & Analysis](01-reported-activity.md)
2. [Idempotency & Distributed Conflict Resolution](02-idempotency-and-conflicts.md)
3. [Event Ordering & Causal Consistency](03-event-ordering.md)
4. [Security Architecture & Zero-Trust Perimeter](04-security-and-trust.md)
5. [Scaling & Large-Data Synchronization](05-large-data-sync-and-scaling.md)
6. [API Protocol Evaluation (REST vs WebSocket vs gRPC)](06-api-protocols.md)
7. [Device Fingerprinting & Payload Integrity](07-fingerprinting.md)
8. [Research Log](08-research-log.md)
