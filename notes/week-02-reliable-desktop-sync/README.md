# Week 2 — Reliable Desktop Synchronization & Offline-First Protocols

## Curriculum Overview

Week 2 tackles edge reliability: designing desktop assessment client software that reliably synchronizes candidate answers, keystrokes/code deltas, execution outputs, and proctoring violation events with cloud backend services under unpredictable network environments.

---

## Assignment Goals & Deliverables

1. **System Architecture Diagram**: Client components (UI Thread, Local SQLite Database, Transactional Outbox Sync Engine, Network Monitor), API Gateway, Assessment Ingestion Pipeline, and Cloud Persistence.
2. **Technical Design Document**:
   - Local durable persistence & zero-data-loss crash recovery.
   - Idempotent incremental event synchronization and monotonic versioning.
   - Transactional outbox pattern on desktop SQLite.
   - Exponential backoff with full jitter for connection drops and reconnection storms.
   - Deterministic finite state machines for assessment lifecycles (InProgress → Submitting → Submitted).
   - Re-authentication and offline session token rotation.
   - Load management: 50 to 500 concurrent candidates reconnecting simultaneously.

---

## Reading Guide

1. [Offline-First Architecture & Local Persistence](01-offline-first-data.md)
2. [Synchronization Protocols & Incremental Ingestion](02-sync-protocol.md)
3. [Events, Queues & Transactional Outbox Pattern](03-events-and-queues.md)
4. [Reliability, Retries & Exponential Jitter](04-reliability-and-fault-tolerance.md)
5. [Assessment State Machine Modeling](05-assessment-state-machines.md)
6. [Security, Token Rotation & Observability](06-security-testing-observability.md)
7. [Research Log](07-research-log.md)
8. [Sync Architecture Worksheet](08-sync-design-worksheet.md)
