# 10 — Research log — Week 4

## Guide research — 2026-11-18

Reviewed PostgreSQL documentation for query plans, statistics, indexes, and transaction isolation; Redis guidance for cache-aside, eviction, and distributed rate limiting; and Microsoft/AWS architecture references for background work, retries, circuit breakers, and outbox processing. The chapters synthesize design guidance against the assignment; no benchmark or implementation test was run.

## Slack-reported study updates

- **2026-11-11:** Muneeb reported database design/relationships/normalization/indexes, query execution, slow queries/N+1, transactions/ACID/isolation/deadlocks/safe updates. Saad reported indexing, query optimization, pooling, caching, and concurrent-request/database-pressure concerns. Haseeb shared a [modern web architecture article](https://medium.com/womenintechnology/modern-web-architecture-101-b430df7b9d8e).
- **2026-11-12:** Muneeb reported deeper database optimization/design. Hammad reported cache stampede: many requests can hit the backend/DB together after a popular cache entry expires. Saad reported comparing ECS/EC2/EKS and Fargate/Lambda/EC2 by workload, control, and scaling requirements.
- **2026-11-13:** Saad posted CAP theorem and CDC vs. SCD as topics.

These are participant-reported subjects, not evidence that a design was validated. Sources: [Nov 11 standup](https://app.slack.com/archives/C0CA0S502AH/p1794402014701879), [Nov 12 standup](https://app.slack.com/archives/C0CA0S502AH/p1794488426423879), [Nov 13 topic post](https://app.slack.com/archives/C0CA0S502AH/p1794578452123519).

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
