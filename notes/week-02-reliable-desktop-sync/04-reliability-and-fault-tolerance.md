# 04 — Reliability and fault tolerance

The assignment requires recovery from crashes, network/server outages, duplicates, stale edits, auth expiry, execution failures, final-submit disconnects, disk-full errors, and 50/100/200/500 concurrent candidates.

## Failure concepts

- **Failure domain:** a component boundary where a fault can be contained (device, region, DB, worker pool).
- **Partial failure:** one component or operation fails while the wider workflow remains active.
- **Network partition:** peers cannot communicate; neither side can know whether the other committed.
- **Timeout:** bounds resource use while waiting; it does not prove that the remote operation did not commit.
- **Durability/recovery:** persist pending work and checkpoints so a process restart can resume.

## Resilience patterns

- **Retry:** transient failures only; finite attempts/time, backoff, jitter, stable idempotency key.
- **Circuit breaker:** stop repeated calls to a dependency likely to remain unhealthy; probe recovery cautiously.
- **Bulkhead:** cap concurrency/resource use so one slow operation cannot consume all capacity.
- **Backpressure:** slow or reject producers when consumers/resources saturate; expose queue age and retry guidance.
- **Graceful degradation:** preserve critical assessment functions while deferring noncritical analytics/sync.
- **Redundancy:** helps availability only with designed and exercised failover/state recovery.

Use explicit request timeouts, finite retries, exponential backoff with jitter, and a retry budget. Honor `Retry-After`. Don't retry permanent validation/auth errors unchanged. Queue critical events durably while offline. Microsoft's [transient fault guidance](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults) covers bounded retries and circuit breakers; AWS SQS documents [at-least-once delivery, visibility timeout, and DLQs](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html).

## Availability and consistency choices

During a partition, the desktop may accept local writes but cannot promise server visibility or globally conflict-free state. Show local persistence and server acknowledgement separately. Decide which actions remain available offline and which require online authorization. Resolve conflicts on reconnect using revisions/domain rules; do not label uncertain state as “success.”

## Failure exercise

For network, API, database, queue, and code runner, identify detection, timeout, retry rule, durable state, user experience, and recovery. Inject one failure at a time and verify safety (no loss/duplicate) and liveness (eventual progress).

