# Design worksheet — Reliable desktop synchronization

## Assumptions and requirements

- **Data/events synchronized:**
- **Durability boundary (when is a local save committed?):**
- **Ordering and conflict requirements:**
- **Availability / latency targets:**

## Proposed design

- **Components and responsibilities:**
- **Local persistence and crash recovery:**
- **Event envelope / IDs / revisions:**
- **Batching, retries, backoff, and idempotency:**
- **Conflict resolution and stale update protection:**
- **Submission confirmation:**
- **Auth and local data protection:**
- **Backpressure and reconnect surge handling:**

## Failure matrix

| Failure | Locally durable state | Client behavior | Server behavior | Recovery / user feedback |
|---|---|---|---|---|
| App crash/restart | | | | |
| Network unavailable | | | | |
| Server/database unavailable | | | | |
| Token expires | | | | |
| Duplicate/stale request | | | | |
| Disk full/local DB failure | | | | |
| Execution timeout | | | | |
| Final submission disconnect | | | | |
| Reconnect surge | | | | |

## Tests and trade-offs

- **Tests / load levels:**
- **Observability:**
- **Alternatives considered:**
- **Open questions:**
