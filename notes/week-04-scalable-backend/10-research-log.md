# 10 — Research log — Week 4

## Guide research — 2026-11-18

Reviewed PostgreSQL documentation for query plans, statistics, indexes, and transaction isolation; Redis guidance for cache-aside, eviction, and distributed rate limiting; and Microsoft/AWS architecture references for background work, retries, circuit breakers, and outbox processing. The chapters synthesize design guidance against the assignment; no benchmark or implementation test was run.

## Reported study updates

- **2026-11-11:** Team Member reported database design/relationships/normalization/indexes, query execution, slow queries/N+1, transactions/ACID/isolation/deadlocks/safe updates. Saad reported indexing, query optimization, pooling, caching, and concurrent-request/database-pressure concerns. Technical Leadership shared a [modern web architecture article](https://medium.com/womenintechnology/modern-web-architecture-101-b430df7b9d8e).
- **2026-11-12:** Team Member reported deeper database optimization/design. Team Member reported cache stampede: many requests can hit the backend/DB together after a popular cache entry expires. Saad reported comparing ECS/EC2/EKS and Fargate/Lambda/EC2 by workload, control, and scaling requirements.
- **2026-11-13:** Saad posted CAP theorem and CDC vs. SCD as topics.

These are participant-reported subjects, not evidence that a design was validated. Sources: [Nov 11 standup](#), [Nov 12 standup](#), [Nov 13 topic post](#).

### Session template

#### YYYY-MM-DD — Topic
- **Question / hypothesis:**
- **Source / workload tested:**
- **Finding:**
- **Production implication:**
- **Evidence (plan, graph, benchmark, or diagram):**
- **Open question / next step:**

## Assignment checklist

- [ ] System design diagram includes clients, load balancer, app instances, API, cache, DB, workers, flows, bottlenecks, scaling points.
- [ ] Technical design records schema, queries, transactions, pool, cache, API/rate limit, scaling, failure behavior, and alternatives.
- [ ] Rate limiter compares Fixed Window, Sliding Window, and Token Bucket; documents shared Redis state, atomicity, traffic spikes, and Redis failure.
- [ ] Actual tests and discussion outcomes are linked here when available.
