# 05 — Caching, TTLs, invalidation, and consistency

Technical Leadership calls out Redis, TTL, invalidation, and consistency. Cache-aside is a practical start: read cache; on miss read source of truth and populate; after committed write invalidate/update. See [Week 4 foundations](../week-04-scalable-backend/04-caching.md).

For each value define acceptable staleness, TTL, invalidation event, and fallback. Invalidate after authoritative commit. Consider a slow old read repopulating cache after invalidation; versioned values/guarded writes can help. Do not use stale values for authorization/balance checks unless explicitly acceptable.

Popular-key expiry can stampede the DB. Coalesce refreshes, randomize TTLs, or serve stale while refreshing where safe. On Redis failure, bound DB fallback concurrency. Monitor hit rate, latency, evictions, memory, and fallback load. Redis documents [cache-aside](https://redis.io/docs/latest/develop/use-cases/cache-aside/) and [eviction policies](https://redis.io/docs/latest/reference/eviction/). Cache entries are disposable; sessions or queues may require different eviction/availability requirements or isolated capacity.

| Data | Source of truth | Stale tolerance | TTL/invalidation | Redis failure behavior |
|---|---|---|---|---|
| Public catalog | | | | |
| User profile | | | | |
| Permission/balance | | | | |
