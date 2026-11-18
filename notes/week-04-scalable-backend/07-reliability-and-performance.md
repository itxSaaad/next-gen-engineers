# 07 — Reliability and performance testing

Reliability is observable behavior under faults, not just uptime. Define user-facing SLOs for latency, availability, and correctness. Set timeouts at each dependency boundary so a slow downstream call does not consume unbounded threads/connections.

## Retry and failure policy

Retry only transient failures, with finite attempts, exponential backoff, jitter, and an overall deadline. Retrying non-idempotent writes can duplicate effects; use idempotency keys or do not retry automatically. Circuit breakers stop calls to a dependency that is persistently failing; bulkheads limit how many requests can consume a resource. Specify behavior for DB, Redis, queue, and worker failure separately.

## Load test with a question

Test realistic traffic mix, data volume, warm/cold cache, ramp-up, sustained peak, and burst/recovery. Record throughput, p50/p95/p99 latency, errors, saturation, queue age, DB waits, and resource usage. Include failure injection (Redis unavailable, slow queries, worker restart) and verify recovery. A test that only reports requests/sec without correctness assertions can miss duplicate or lost updates.

## Bottleneck loop

1. Capture a baseline and agree on target SLO.
2. Identify the saturated resource from telemetry.
3. Form one hypothesis and change one design variable.
4. Repeat the same workload and compare latency, throughput, correctness, and cost.
5. Keep or revert based on evidence; document limits and rollback.

## Observability: logs, metrics, traces

- **Logs** explain individual events and errors; include structured fields and correlation IDs, redact sensitive payloads.
- **Metrics** quantify behavior over time: request rate, error rate, latency histograms, saturation, DB pool wait, cache hit/miss, queue depth/age, worker throughput, retry/DLQ count.
- **Traces** connect one request across API, DB, broker, worker, and downstream calls; propagate trace context and inspect slow spans.

Use p50/p95/p99 latency to see tail behavior; averages can hide slow users. Tie alerts to user-facing SLOs and actionable saturation signals. Avoid high-cardinality metric labels such as raw user IDs. [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/) defines the telemetry categories, and the Week 2 notes apply them to sync flows.

If the workload includes AI calls, also track model latency/failure rate, token use, tool execution time, and cost per successful task. Treat prompts and model output as sensitive when deciding log detail.
