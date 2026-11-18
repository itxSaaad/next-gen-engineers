# 02 — Synchronization models and mechanisms

Treat synchronization as a protocol between stateful peers, not “retry the upload.” The client needs durable progress, stable operation identity, and a conflict rule; the server must validate, authorize, and acknowledge durable writes.

## Models and trade-offs

| Model | Behavior | Trade-off / use |
|---|---|---|
| Push | Client sends local changes | Server may not send other-client changes back |
| Pull | Client fetches server changes | Requires another path for local writes |
| Push + pull | Bidirectional exchange | Needs conflict detection and resolution |
| Snapshot | Transfer full current state | Simple recovery; expensive for large data |
| Incremental | Transfer changes after cursor | Efficient; requires reliable tracking/retention |
| Hybrid | Initial snapshot then increments | Common for larger datasets |

Use a server-issued cursor or monotonic sequence for incremental sync when possible. Client timestamps are vulnerable to clock drift, equal timestamps, and late updates. Define cursor expiry: if change history has expired, the client may need a fresh snapshot.

## Event envelope

A useful envelope contains `event_id`, `assessment_id`, `candidate_id`, `entity_id`, `entity_revision`, `client_sequence`, `event_type`, `schema_version`, `created_at`, and payload. Keep client event time distinct from server receive time; don't trust client clocks for causal ordering. The event ID must remain stable across retries.

## Idempotent server handling

Atomically record an idempotency key with the business mutation, or return the previously stored outcome for a duplicate. A unique constraint is a robust deduplication boundary. If the server commits but its response is lost, the client resends the same operation and receives the original outcome. RFC 9110 says idempotent methods can be repeated safely in intended effect, while non-idempotent requests need extra safety before automatic retry ([§9.2.2](https://datatracker.ietf.org/doc/html/rfc9110#section-9.2.2)).

## Batch and checkpoint

Upload bounded batches with per-event results or a clear all-or-nothing contract. Acknowledge only events durably accepted by the server. Persist the highest acknowledged sequence locally; after restart, resume from that checkpoint. If only part of a batch succeeds, retry unacknowledged events with original IDs. Enforce payload-size and concurrency limits.

Use deltas when the server can reconstruct/validate prior state; use snapshots when it cannot or replay cost is too high. Bound payload sizes, page pull results, and expose progress. Large objects need chunking/resumable transfer with chunk identity, checksum, completion manifest, and cleanup for abandoned uploads (expanded in Week 3).

## Ordering and conflicts

Ordering is usually per candidate/assessment or entity, not global. Sequence numbers expose duplicates and gaps. State updates can use optimistic concurrency: apply revision N only if current revision is N-1. On conflict, fetch server state and merge by domain semantics or surface it for deliberate resolution. “Last timestamp wins” is unsafe when device clocks drift and can erase meaningful work.

Preserve audit events separately from mutable answer state. At-least-once event delivery requires idempotent consumers; AWS's [transactional outbox guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html) explains atomic database-plus-outbox writes and duplicate handling. Event sourcing is a separate, higher-complexity storage choice, not a synonym for adding a queue ([Azure Event Sourcing](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)).

## Observability

Record correlation ID, event ID, revision, attempt count, queue age, acknowledgement latency, and error class. Do not log answers or tokens. Track oldest pending event and backlog count to reveal a stuck client.

## Change-tracking choices

- **Timestamp watermark:** simple, but clock/order issues and late updates can cause misses; use overlap plus deduplication if needed.
- **Monotonic server cursor/sequence:** gives order in its defined scope but needs retention and pagination semantics.
- **Database CDC:** captures DB-log changes for replication/integration; it is distinct from the assessment app's user-facing sync contract.
