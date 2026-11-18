# 06 — Security, testing, and observability

## Security fundamentals

- **Authentication** proves who the actor is; **authorization** decides what that actor can do. Check both on every server operation.
- Bind requests to the authenticated candidate and active assessment; never trust a client-supplied object ID alone.
- Store tokens securely, scope them narrowly, handle expiry while offline, and never log credentials.
- Encrypt sensitive local data where needed; protect keys and define retention/cleanup.
- Validate and size-limit uploads; treat execution artifacts as untrusted. Isolate code execution from API credentials and other candidates.
- Keep secrets out of URLs/errors/logs; return errors that don't disclose another candidate's records.

For modern OAuth deployments, use current security guidance rather than copying a legacy flow; see [RFC 9700 OAuth 2.0 Security BCP](https://www.rfc-editor.org/rfc/rfc9700.html). Week 3 expands object authorization, local-device threats, and sandboxing.

## Failure and load tests

1. Kill client after local commit but before upload; restart and verify pending work recovers.
2. Commit server-side but drop response; retry same event ID and verify one effect.
3. Deliver events out of order/twice/with a gap; assert deterministic handling.
4. Expire auth mid-batch; refresh and resume without losing checkpoint.
5. Simulate disk full, corrupt local store, DB/cache outage, and slow execution.
6. Load at 50/100/200/500 clients, then simulate synchronized reconnects with jitter.
7. Assert final submission remains pending until durable server acknowledgement.

Track loss/duplication, backlog age, sync latency percentiles, retry volume, conflicts, reconnect burst rate, and saturation. Load test the pipeline, including database, queue, and execution service.

## Observability

Logs explain events, metrics quantify behavior, and traces connect a request across components. Use correlation IDs across desktop sync, API, queue, worker, and DB. Track request rate, error rate, latency p50/p95/p99, sync queue depth/oldest age, retries, DLQ, pool waits, and execution latency. Avoid high-cardinality identifiers as metric labels and redact assessment content.

- [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/)
