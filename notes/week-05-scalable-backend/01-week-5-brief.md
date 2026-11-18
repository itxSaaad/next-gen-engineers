# 01 — Week 5 brief and production scenarios

**Slack source:** Muhammad Haseeb Malik, [`#next-gen-engineers`, 2026-11-17](https://app.slack.com/archives/C0CA0S502AH/p1794929453790629). He asked the group to continue Week 4's scalable-backend topics, revisit them due to insufficient preparation, and go deeper instead of moving to a new topic.

## Focus list from Haseeb

- Database design: relationships, normalization, constraints, indexes.
- SQL performance: plans, N+1 problems, slow-query analysis.
- Transactions/concurrency: ACID, isolation, locking, deadlocks, race conditions.
- Connection pooling: sizing, connection limits, saturation.
- Caching: Redis, TTLs, invalidation, consistency.
- API scalability: pagination, filtering, rate limits, efficient responses.
- System scaling: load balancing, horizontal scaling, workers.
- Reliability/performance: load tests, bottlenecks, timeouts, retries, failure handling.

Apply the concepts to traffic spikes, duplicate updates, database overload, and Redis or app-instance failure. Haseeb asked participants to review Week 4 and bring the system diagram, technical decisions, and questions. Resources in his post: [System Design Primer](https://github.com/donnemartin/system-design-primer), [PostgreSQL connection guidance](https://wiki.postgresql.org/wiki/Number_Of_Database_Connections), and [Redis eviction docs](https://redis.io/docs/latest/develop/reference/eviction/).

On 2026-11-18, Haseeb shared a bare [YouTube link](https://www.youtube.com/watch?v=W4EwfEU8CGA), whose title is “Let’s Handle 1 Million Requests per Second, It’s Scarier Than You Think!” The Slack message had no accompanying description, so treat it as a current resource, not a change to the assignment scope.

For each topic, explain the invariant, chosen mechanism, failure behavior, and measurable trade-off. Record actual work in the research log; the assignment post does not prove submitted deliverables or completed sessions.
