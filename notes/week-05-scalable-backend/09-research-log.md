# Research log — Week 5

## Guide research — 2026-11-18

Reviewed PostgreSQL documentation on plans, statistics, transactions, and locking; Redis documentation on cache-aside, eviction, and rate limiting; RFC 9110; AWS transactional outbox guidance; and Microsoft architecture/reliability patterns. Chapters synthesize those sources against Haseeb's Week 5 scope. No load test, production experiment, or participant deliverable is claimed.

Use one entry per study session. Keep claims linked to sources; distinguish what the source says from our design decisions.

## Session template
### YYYY-MM-DD — Topic
- **Question:**
- **What I read / tried:**
- **Findings:**
- **Production implication:**
- **Source links:**
- **Open questions / next step:**

## Questions to resolve this week
- What indexes support the important query patterns, and what write/storage costs do they add?
- How will we detect N+1 and slow queries from plans and production telemetry?
- Which isolation/locking strategy prevents duplicate or conflicting updates?
- How will pool size account for DB connection limits and all app replicas?
- What cache consistency/invalidation behavior is acceptable for each data type?
- Which rate limiter algorithm fits the product's fairness and burst requirements?
- What are the timeout, retry, and fallback policies when Redis, DB, or an app instance fails?
