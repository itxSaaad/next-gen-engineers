# Week 2 — Reliable desktop app synchronization

**Source:** Muhammad Haseeb Malik, [`#next-gen-engineers`, 2026-10-26](https://app.slack.com/archives/C0CA0S502AH/p1793037494033859).
**Week leader:** Hammad Mubeen.

## Assignment

Design a desktop application that reliably synchronizes assessment answers, code changes, execution results, and violation events with a server. Primary objective: prevent data loss, avoid duplicate operations, and resume reliable synchronization after connectivity returns.

## Topics to research

- Offline-first architecture: local database, durable storage, crash recovery.
- Synchronization: incremental sync, batching, queues, conflict resolution.
- Event-driven design: event IDs, revisions, ordering, persistent queues.
- Idempotency and consistency: retries, duplicate prevention, concurrent updates.
- Fault tolerance: exponential backoff, jitter, partial failures, recovery.
- State machines: local-save, synchronization, execution, submission.
- Authentication/security: token expiry, session recovery, encryption, authorization.
- Performance: backpressure, connection management, 50–500 concurrent candidates.
- Testing and observability: failure simulation, tests, metrics, logs.

## Required scenarios

Crashes/restarts; slow or lost internet; server/database downtime; duplicate requests, stale updates and concurrent edits; expired authentication during an assessment; execution failures/timeouts; network loss during final submission; unsynchronized answers or violation events on exit; disk-full/local-storage failure; hundreds of candidates reconnecting together.

## Deliverables and acceptance criteria

- [ ] Diagram desktop app, local storage, sync engine, APIs, database, code execution service, data flow, failure points, and recovery.
- [ ] Technical design covering persistence, batching/retries/order/conflicts, idempotency, state, failure recovery, security, performance, tests, and trade-offs.
- [ ] No loss of locally committed answers in tested recoverable failures.
- [ ] Retries have no duplicate effects and do not overwrite newer answers.
- [ ] Sync resumes automatically when online; submission is confirmed only after server confirmation.
- [ ] UI remains responsive; load strategy covers 50, 100, 200, and 500 concurrent candidates.
- [ ] Explain the why; design and document before coding.

## Read in order

1. [Offline-first architecture and local data](01-offline-first-data.md)
2. [Synchronization models and mechanisms](02-sync-protocol.md)
3. [Events, queues, and transactional outbox](03-events-and-queues.md)
4. [Reliability and fault tolerance](04-reliability-and-fault-tolerance.md)
5. [Assessment state machines](05-assessment-state-machines.md)
6. [Security, testing, and observability](06-security-testing-observability.md)
7. [Research log and Slack-reported activity](07-research-log.md)
8. [Design worksheet](08-sync-design-worksheet.md)

## Evidence and completion

An assignment brief is not evidence that deliverables were submitted. Add actual artifacts and review outcomes when found.
