# Week 5 Assignment Deliverable: Redis Caching & API Scalability

## Assignment Brief (Private Review by Muhammad Haseeb Malik)

> **Goal**: Design APIs for a platform receiving high request volumes, with frequently accessed candidate and assessment data. Explain what should be cached, how stale data is handled, and how the APIs remain reliable.

### Evaluation Criteria (Passing Score: 4.5 / 5.0 | 90%)
- **Conceptual understanding and technical accuracy** (1.0 pt)
- **Architecture/design and technical decisions** (1.0 pt)
- **Practical implementation or working example** (1.0 pt)
- **Real-world scenarios and failure handling** (1.0 pt)
- **Explanation, trade-offs, and ability to defend decisions** (1.0 pt)

---

## Deliverables Checklist

### 1. Endpoint Design & High-Volume Pagination/Filtering
- [ ] Candidate directory endpoint (`GET /api/v1/candidates`) with keyset/cursor-based pagination (`cursor = base64(created_at, id)`).
- [ ] Candidate details & profile cache projection (`GET /api/v1/candidates/{id}`).
- [ ] Assessment status & submission endpoints (`GET /api/v1/assessments/{id}`, `POST /api/v1/assessments/{id}/submit`).
- [ ] Filtering strategies aligned with PostgreSQL B-Tree / GIN indexes and Redis cache keys.
- [ ] Response payload optimization (field masks, sparse fieldsets, gzip/brotli compression).

### 2. Redis Caching Strategy
- [ ] Key design conventions: Namespaced keys (`{entity}:{id}:{view}:{version}`).
- [ ] Storage data types: Hashes vs JSON strings vs Sorted Sets for specific read patterns.
- [ ] Tiered TTL policies:
  - Static reference data / Assessment definitions: Long TTL (hours/days) + event invalidation.
  - Candidate profile & submission status: Medium TTL (5–15 minutes) + write-through/invalidation.
  - Active session / live assessment draft: Short TTL (60–120 seconds) + sliding expiration.
  - Search/filter listings: Short TTL (30–60 seconds) or deterministic tag-based caching.
- [ ] Cache stampede mitigation: Probabilistic early expiration (XFetch algorithm) and distributed mutexes (`Redlock` / Redis `SET NX EX`).

### 3. Distributed Rate-Limiting Design
- [ ] Algorithm selection: Sliding Window Counter vs Token Bucket.
- [ ] Atomic execution using Lua scripts to prevent race conditions.
- [ ] Tiered rate limits:
  - Unauthenticated endpoints (IP-based): 60 req/min
  - Candidate session & submission APIs: 300 req/min
  - High-frequency live telemetry / autosave: 120 req/min
  - Internal recruiter / admin queries: 1000 req/min
- [ ] Rate limit headers (`X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`, `Retry-After`).

### 4. Cache Invalidation & Failure Handling Strategy
- [ ] Invalidation patterns: Cache-aside with event-driven invalidation (Change Data Capture / domain events on model updates).
- [ ] Consistency trade-offs: Dual-write race condition mitigation via transactional outbox or Redis delete-after-commit.
- [ ] Redis Outage / Network Partition handling:
  - Circuit Breakers (fail-fast vs fail-open).
  - DB protection: Degraded response modes, read-replica shed, stale-while-revalidate fallback.
  - Thundering herd prevention when Redis recovers.

### 5. Practical Implementation & Working Example
- [ ] Runnable FastAPI application + Redis + PostgreSQL in Docker Compose.
- [ ] Working implementation of the cursor pagination, Redis caching layer with Lua scripts, and circuit-breaker resilience.
- [ ] Integration test suite & load benchmark simulation scripts.
