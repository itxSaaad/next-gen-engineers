# 05 — Scaling and large-data synchronization

This chapter combines the channel-reported reconnect/backpressure work with the supplied study outline's large-data synchronization scope.

## Scaling the service

Vertical scaling increases one node's capacity but has hardware limits and a larger failure unit. Horizontal scaling adds instances and requires stateless request handling (or deliberately shared state), safe concurrent writes, health checks, and a deployment plan. Load balancing distributes traffic; autoscaling reacts with delay, so use capacity headroom, admission limits, and queues. Scale workers against queue depth/age while protecting DB/API limits. Throughput and latency are different measures; capacity planning uses expected concurrency and resource cost per request.

## Large transfers

- **Full vs incremental:** snapshots are straightforward recovery, but expensive for large datasets; cursors/deltas reduce repeat transfer but need reliable change tracking and retention.
- **Chunking/streaming:** bound memory and retry only failed chunks. Use chunk ID/index, total size, upload/session ID, checksum, and final manifest. Make duplicate chunk writes safe.
- **Resume/checkpoints:** persist acknowledged offsets/chunk IDs; resume from last durable checkpoint after disconnect or process restart.
- **Integrity/deduplication:** checksums detect corruption; content hashes can identify identical bytes but should not be used as authorization. Define cryptographic hash and scope; avoid exposing sensitive content through predictable hashes.
- **Compression/batching:** balance bytes saved with CPU, memory, latency, and failure blast radius. Tune batch size using telemetry.
- **Rate and priority:** cap per-client concurrency, add jitter, protect critical submission/violation paths by explicit product policy, and report progress.

Amazon S3 multipart uploads support independent parts, pause/resume, and checksum validation; see [S3 multipart uploads](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html). For API payload sync, the same design ideas need application-level session, authorization, and cleanup semantics.

## Reconnect bursts and backpressure

After an outage, clients should not all retry immediately. Use exponential backoff with jitter, server `Retry-After`, per-client limits, bounded worker concurrency, and a queue where durable buffering is appropriate. Monitor reconnect rate, pending backlog, oldest item age, chunk retry count, API p95/p99, DB pool waits, queue age, and worker throughput.

## Capacity walkthrough

Estimate requests/chunks per candidate, peak simultaneous reconnects, average payload, DB writes per event, worker concurrency, and downstream calls. Test steady state plus a reconnect wave; scale the actual saturated stage rather than simply adding web replicas.
