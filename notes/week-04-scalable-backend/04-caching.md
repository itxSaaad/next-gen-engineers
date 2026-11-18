# 04 — Caching with Redis

Cache only data with a clear key, freshness requirement, and fallback. Cache-aside is a practical starting pattern: read cache; on miss query the system of record; populate cache with a bounded TTL; on update commit authoritative storage and invalidate or refresh the cache.

## Common cache patterns

- **Cache-aside:** application reads/writes cache around the database; flexible, but callers own miss and invalidation logic.
- **Read-through:** cache layer loads on miss; simplifies callers, but loader behavior and stampede prevention still matter.
- **Write-through:** write cache and source during the write path; keeps cache warm but increases write latency and demands failure ordering.
- **Write-behind:** acknowledge cache then persist later; can improve write latency but risks data loss/complex recovery, so it is inappropriate for durable assessment answers unless a durable log protects the write.
- **Local in-process cache:** fastest/local, but per-instance stale copies and duplicated memory.
- **Distributed cache:** shared across instances, but adds network dependency, capacity, and failure behavior.
- **Negative caching:** cache “not found” briefly to reduce repeated misses; invalidate carefully when the record is created.

## Freshness and invalidation

TTL bounds staleness but does not guarantee immediate freshness. For mutable data, invalidate on write and consider race ordering: a slow old read can repopulate a stale value after invalidation. Versioned keys, write-through, or guarded refresh may be appropriate. If stale reads are unacceptable (permissions, balances), do not rely solely on an eventually consistent cache.

## Stampedes and failure modes

Popular keys expiring together can flood the DB. Coalesce concurrent refreshes, use TTL jitter, or serve stale while refreshing where product rules allow. If Redis is down, decide which operations fail, which can fall back, and how fallback load is bounded. Monitor hit rate, memory, evictions, latency, and DB fallback volume. Redis documents [cache-aside and stampede controls](https://redis.io/docs/latest/develop/use-cases/cache-aside/) and [eviction policies](https://redis.io/docs/latest/reference/eviction/).

## Key and memory design

Include tenant/authorization dimensions in keys where needed; define serialization/versioning and avoid storing secrets unnecessarily. Estimate working-set size and max memory. Eviction policy depends on whether all keys are disposable cache entries or Redis also stores durable-ish sessions/queues. Mixing workloads with different eviction and latency needs may require isolation.
