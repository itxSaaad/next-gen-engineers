# 06 — Scaling and background work

Scaling means adding capacity at the bottleneck while preserving behavior. Vertical scaling raises capacity of one node but has limits and a larger failure unit. Horizontal scaling adds instances and requires stateless request handling or shared state, safe concurrent writes, and deployment/health management.

## Load balancing and stateless services

Health checks should distinguish readiness from liveness; remove unhealthy instances from traffic without causing restart loops. Avoid sticky sessions unless required; externalize session state to a suitable shared store. Autoscaling on request rate or CPU is not instantaneous, so protect the service with queues, admission limits, and capacity headroom.

## Background workers and queues

Move long-running or bursty work off interactive requests. A queue buffers demand and workers consume at a controlled rate; scale workers against queue depth/age while respecting downstream DB/API limits. Queues add eventual consistency, duplicate delivery, ordering, poison-message, and backpressure concerns. Acknowledgement should follow durable processing; consumers should be idempotent. Microsoft's [Web-Queue-Worker architecture](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/web-queue-worker) and [background job guidance](https://learn.microsoft.com/en-us/azure/architecture/best-practices/background-jobs) describe trade-offs and independent scaling.

Worker pools should be sized by workload: CPU-bound jobs are limited by CPU and memory; I/O-bound tasks by downstream limits and safe concurrency. Async I/O can free threads but does not remove DB/API quotas. Track throughput, consumer lag, queue depth, and oldest message age. Configure bounded retries, poison-message handling, and a DLQ. For SQS, visibility timeout expiry can redeliver work and standard queues are at-least-once, so handlers must be idempotent ([SQS visibility timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html)).

## Capacity and bottleneck model

Measure request rate, service time, queue depth, concurrency, DB pool waits, cache hits, and downstream limits. Estimate per-request resource consumption and identify the narrowest stage. More app instances can worsen DB saturation; scale the full pipeline and use load shedding when demand exceeds safe capacity.
