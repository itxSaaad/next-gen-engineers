# 04 — Connection pooling and saturation

Haseeb calls out pool sizing, DB connection limits, and saturation. Pooling reuses connections; it does not increase safe DB concurrency. Too large a pool increases DB contention; too small queues requests. See [Week 4 foundations](../week-04-scalable-backend/03-connection-pooling.md).

## Sizing model

Calculate `max app replicas × pool max + worker pools + scheduled tasks + admin/migration reserve`. Compare with usable DB connection budget and leave failover/operations headroom. Autoscaling maximum matters: a pool safe at 2 replicas may exceed limits at 20.

## Find the cause

Track pool wait duration, active/idle/overflow connections, checkout timeouts, transaction duration, DB active queries, lock waits, and query latency. Slow queries/long transactions hold connections; investigate leaks and lifecycle. Bound pool wait and request deadline.

Transaction-pooling proxies improve utilization but may break session state, temporary table, prepared statement, or advisory lock assumptions; validate driver semantics. On shutdown stop new work, finish/rollback transactions, then close the pool.

## Exercise

With 120 usable connections, reserve 20 for operations/failover; propose pool maxima for 4–10 app replicas plus two workers. Which metrics indicate an undersized pool versus a saturated database?
