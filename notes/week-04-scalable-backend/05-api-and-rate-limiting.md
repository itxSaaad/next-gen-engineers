# 05 — API scalability and distributed rate limiting

Efficient API responses bound work and response size. Use pagination with a stable ordering and tie-breaker; cursor/keyset pagination performs better for deep traversal and avoids some offset drift. Validate filters, cap page sizes, select only needed fields, batch related lookups, and set request timeouts. Version contracts and return consistent error shapes.

## Rate limiter algorithms

- **Fixed window:** atomic counter per identity/window; simple and cheap, but permits near-2× bursts across a boundary.
- **Sliding log:** exact timestamps in a rolling interval; accurate but uses more memory and operations.
- **Sliding window counter:** approximate rolling count using current and previous windows; lower memory with approximation.
- **Token bucket:** refill tokens at a configured rate up to a capacity; permits bounded bursts while enforcing long-term rate.
- **Leaky bucket:** queue/smooth requests to a configured output rate; useful for smoothing work, but adds wait/queue semantics and may not fit interactive requests.

Choose per business rule: identity (user, tenant, API key, IP), window, burst allowance, fairness, and failure policy. Redis documents practical [rate-limiter patterns](https://redis.io/docs/latest/develop/use-cases/rate-limiter/); atomic scripts/transactions are needed so simultaneous app instances do not overspend a shared limit.

Use HTTP `429 Too Many Requests` for a rejected client quota, with a clear retry window where possible. `Retry-After` may be a delay or date per [RFC 9110](https://datatracker.ietf.org/doc/html/rfc9110#section-10.2.3). Define headers and scope consistently. Monitor allowed/denied counts, limiter latency/errors, key cardinality/hot tenants, and downstream saturation.

## Redis failure and response contract

For abuse prevention or expensive downstream protection, fail closed or apply a conservative local fallback; for low-risk limits, a bounded fail-open policy may preserve availability. State the choice and its risk. Return a clear throttling response and retry guidance; RFC 9110 defines `Retry-After` for indicating when a client should retry ([HTTP semantics](https://datatracker.ietf.org/doc/html/rfc9110#section-10.2.3)). Ensure limiter keys expire and shard/partition dimensions do not create hot keys.
