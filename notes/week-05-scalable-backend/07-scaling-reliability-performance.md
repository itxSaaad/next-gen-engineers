# 07 — Scaling, reliability, and performance

See [Week 4 scaling foundations](../week-04-scalable-backend/06-scaling-and-background-work.md). Week 5 expects evidence from realistic load and failure scenarios.

## Bottleneck and load method

Record workload mix, data size, cache state, ramp-up, sustained peak, burst, and recovery. Measure throughput, p50/p95/p99 latency, errors, CPU/memory, DB/pool waits, cache hit rate, queue depth/age, and downstream throttles. Request rate without correctness assertions can miss lost/duplicate writes.

1. Establish an SLO and baseline.
2. Find the saturated resource from telemetry.
3. Change one variable and repeat the workload.
4. Compare latency, throughput, correctness, and cost.
5. Document the safe limit and scale/load-shed trigger.

## Resilience policy

Set per-dependency timeouts; use finite retries with exponential backoff and jitter only for transient faults; ensure writes are idempotent before retry. Honor `Retry-After`; use circuit breakers for persistent failures, bulkheads for isolation, and queues for bounded async work. Avoid retries at every layer because nested policies multiply load. See Microsoft's [transient fault guidance](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults) and [circuit breaker pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker).

## Required failure walkthroughs

- Traffic spike: queue/buffer, admission control, autoscale lag, load shedding.
- Database overload: pool protection, query diagnosis, safe degraded behavior.
- Redis outage: fallback cap and cache/rate-limit behavior.
- App-instance crash: request recovery, job redelivery, idempotency.
- Worker backlog: queue age, scaling signals, poison-message/dead-letter path.
