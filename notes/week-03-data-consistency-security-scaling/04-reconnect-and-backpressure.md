# 04 — Reconnect bursts, backpressure, and partial sync

When many offline clients reconnect together, retries can turn an outage into a traffic spike. The standups explicitly raised simultaneous reconnects, database pressure, API latency, backpressure, rate limits, worker concurrency, large offline backlogs, partial upload, and slow networks.

## Drain a backlog safely

Persist pending work; upload in bounded chunks/batches; checkpoint each acknowledged chunk; resume from the last durable acknowledgement. Use per-client concurrency limits and server-side quotas so one large backlog cannot monopolize capacity. Apply exponential backoff with jitter after transient errors. Respect server `Retry-After`. Prioritize final submission or critical violation events only if the product's correctness and ordering rules permit it.

## Backpressure and queues

Return clear “retry later” signals when admission capacity is exhausted. A queue can buffer durable work, but queue depth/age must be bounded and monitored. Scale workers against backlog while protecting DB and execution-service capacity. Chunking helps recover large transfers, but define chunk IDs, checksums, completion manifests, duplicate handling, and cleanup for abandoned uploads.

## Capacity and observability

Measure reconnect rate, requests per client, upload backlog size, oldest pending age, chunk retries, API p95/p99, DB pool waits, queue age, and worker concurrency. Test synchronized reconnects after realistic downtime, not only steady traffic. Increase throughput only after identifying the constrained stage.

## Sources

- [Microsoft transient-fault handling](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults)
- [Microsoft retry pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/retry)
- [Haseeb's Week 2 brief](../week-02-reliable-desktop-sync/README.md)
