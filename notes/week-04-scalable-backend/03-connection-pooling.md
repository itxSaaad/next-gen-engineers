# 03 — Connection pooling and saturation

Database connections are finite resources. Each web request should borrow a connection briefly and return it; opening a fresh database connection per request adds setup overhead and can overwhelm the server.

## Size from the whole deployment

The maximum possible connections are roughly replicas × per-replica pool maximum, plus workers, migrations, monitoring, and administrative headroom. Compare that sum to the database's usable connection budget. Pooling does not create database capacity: a larger pool can move the queue into the database, increase memory/context-switching, and worsen latency.

## Diagnose saturation

Observe pool wait time, active/idle connections, checkout timeouts, DB active queries, lock waits, and query duration. A saturated pool may be a symptom of slow SQL, long transactions, leaks, or too many replicas. Avoid raising limits until the bottleneck is identified. Bound request wait time and fail predictably when saturated.

## Multiplexing/proxy caveats

Transaction pooling can improve utilization but changes session semantics: session state, temporary tables, prepared statements, and advisory locks may not behave as expected across transactions. Validate driver/proxy compatibility. On shutdown, stop taking new work, finish/rollback checked-out transactions, then close the pool.

## Sizing exercise

Given a database connection budget, allocate headroom first, then calculate pool maxima across all app and worker replicas. Test worst-case deployment scale and a slow-query scenario; ensure application queues and timeouts fail before resource exhaustion cascades.

## AWS RDS Proxy

For AWS-hosted RDS/Aurora, RDS Proxy maintains a server-side connection pool and can multiplex client connections across DB connections when session state permits. It can queue/throttle excess connects and reduce connection churn, especially for bursty/serverless clients. It does not make expensive queries or unlimited concurrency safe, and session pinning can reduce multiplexing. Check pinning and connection metrics, network prerequisites, failover behavior, and cost. Compare it with application pooling and PgBouncer based on engine, session behavior, operations, and workload. See [RDS Proxy concepts](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.howitworks.html) and [planning guidance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy-planning.html).

## Pool math example

If 10 API replicas each allow 30 DB connections and 10 workers each allow 20, peak client-side potential is `10×30 + 10×20 = 500` connections. Compare that to DB budget and all other clients. A proxy may reduce backend connection count, but still bound requests and watch pool wait/DB saturation.
