# 03 — System design case study: URL shortener

The technical curriculum's Week 1 discussion asked for URL generation, database design, redirects, caching, scalability, and failure handling. On 2026-10-21 he emphasized requirement extraction and shared an [article](https://medium.com/@sugamsays/design-a-url-shortener-bit-ly-tinyurl-e5351ccad56e), [video 1](https://www.youtube.com/watch?v=16d35un5a9Q), and [video 2](https://www.youtube.com/watch?v=9OtPnpTiLag).

## Requirements first

Clarify custom aliases, expiry, analytics, revocation, tenancy, read/write rates, peak traffic, latency, availability, and retention. Define abuse controls for malicious links and rate limits. A shortener is often read-heavy, but the workload needs an explicit estimate.

## Identifier strategy

- **Random token:** generate entropy, enforce a unique DB constraint, retry on collision. Avoids obvious insertion order, but uniqueness is probabilistic until checked.
- **Sequence + base encoding:** simple uniqueness and compactness, but reveals approximate order and introduces centralized allocation concerns.
- **Distributed ID:** can scale allocation; requires clear bit layout, collision assumptions, and consideration of leaked metadata.

Choose alphabet and length from namespace capacity, expected lifetime, privacy, and desired opacity. The database unique constraint is the correctness guard; application “check then insert” alone races.

## Storage and redirect path

A minimal record may have `code` (unique), normalized destination URL, owner/tenant, created/expiry/revoked timestamps, and policy state. Validate allowed schemes and normalize consistently. `code → destination` is the hot lookup. Decide temporary vs permanent redirect based on link mutation, browser caching, analytics, and revocation needs.

Do not make a redirect wait on heavyweight analytics storage. Emit a durable event or bounded async record and define its loss tolerance. Avoid logging sensitive query strings by default.

## Cache and scale

Cache-aside: read cache, fall back to DB, populate with bounded TTL, invalidate/update after mutation. A revoked link must not stay live in cache beyond accepted staleness. Popular-key expiration can stampede the DB; coalesce refreshes or randomize TTLs. Cache loss should degrade safely to the DB. Add replicas, partitions, or sharding only when measured workload and key distribution justify them.

## Failure analysis

| Failure | Design question |
|---|---|
| Database unavailable | Is a cached redirect safe? What response and alert? |
| Cache unavailable | Can fallback avoid overwhelming the database? |
| Duplicate create retry | Is there a client idempotency key or unique alias constraint? |
| Malicious destination | How are links blocked, reviewed, and revoked? |
| Expiration/revocation | How quickly do cache and replicas reflect change? |
| Analytics backlog | Is redirect success decoupled from event processing? |

Draw creation and redirect flows separately. Mark source of truth, unique constraints, cache policy, async analytics, abuse controls, and failure behavior. State traffic assumptions and calculate namespace capacity rather than picking code length by intuition.
