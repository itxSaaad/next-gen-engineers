# 06 — API scalability and rate limiting

Bound API work and response size: cap page size, validate filters/sort fields, fetch needed columns, batch related lookups, and set deadlines. Offset pagination is simple but deep offsets scan/discard rows and can drift under concurrent writes. Cursor/keyset pagination uses a stable order plus unique tie-breaker for efficient traversal.

## Distributed API rate limiter discussion
The technical curriculum's Week 4 assignment named this as Friday's system-design discussion. Be prepared to compare:
- **Fixed window:** simplicity vs boundary bursts.
- **Sliding window:** smoother limits vs additional state/work.
- **Token bucket:** controlled bursts with a sustained refill rate.

### Proposed design worksheet
- **Algorithm and why:**
- **Redis key/state model:** Scope by limit identity and time/algorithm state; expire old keys.
- **Atomicity:** Use atomic Redis script/transaction so instances cannot spend the same allowance.
- **Limit dimensions:** user, API key, IP, endpoint, or tenant.
- **Response:** status, retry guidance, headers.
- **Traffic spikes / hot keys:**
- **Redis failure policy:** fail-open, fail-closed, or degraded local limits; justify by endpoint risk.
- **Operational metrics:** allowed/denied requests, latency, Redis errors, hot keys.
- **Trade-offs and alternatives:**

## Scenario walkthroughs
| Scenario | Expected behavior | Remaining question |
|---|---|---|
| Burst at window boundary |  |  |
| Multiple app instances handle same key |  |  |
| Redis is unavailable |  |  |
| A single tenant becomes hot |  |  |

## Sources
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [Redis rate limiter guide](https://redis.io/docs/latest/develop/use-cases/rate-limiter/)
- [RFC 9110 Retry-After](https://datatracker.ietf.org/doc/html/rfc9110#section-10.2.3)
- [Week 4 API foundations](../week-04-scalable-backend/05-api-and-rate-limiting.md)
