# 03 — Event-driven architecture, queues, and outbox

## Commands, events, queues, and buses

- A **command** asks a specific owner to act and may be rejected.
- An **event** states something happened; it is normally immutable and may have multiple subscribers.
- A **queue** distributes work among consumers; a **pub/sub topic or event bus** fans events out. Products may combine capabilities, so inspect delivery semantics.
- **Async processing** decouples request latency from slow work but introduces pending states, eventual consistency, retries, and backlog operations.

## Delivery guarantees

At-most-once delivery may lose work; at-least-once may duplicate work. Exactly-once delivery is rarely an end-to-end property across client, network, database, broker, and downstream effects. Effect-once behavior can often be achieved within a defined boundary with stable operation IDs, atomic deduplication, idempotent consumers, and transactional state changes. State the boundary and retention window.

## Transactional outbox

When a DB change must publish an event, write the business row and outbox row in one DB transaction. A relay publishes committed outbox rows and tracks progress. Relay crashes may publish duplicates, so consumers deduplicate; the outbox avoids the “DB committed but publish never happened” dual-write gap. See [AWS transactional outbox guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html).

## Consumer safety and operations

Consumers validate schema/version, process idempotently, commit business changes before acknowledging, and bound retries. Route poison messages to a dead-letter queue (DLQ) for investigation/replay. Preserve order only where the domain needs it, often by entity key/partition. Add correlation IDs and schema evolution rules; avoid in-place mutation of historical events without a replay/migration plan.

For the assessment app, the local pending-change table can act like an outbox. The sync worker uploads stable event IDs; server processing records accepted IDs with the relevant answer/state mutation. Keep violations/audit events distinct from answer snapshots because retention and ordering rules differ.
