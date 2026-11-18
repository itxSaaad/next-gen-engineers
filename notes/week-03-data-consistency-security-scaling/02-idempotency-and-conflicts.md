# 02 — Idempotency, ordering, and conflict handling

The standups specifically mention unique change IDs, idempotency keys, transactional deduplication, optimistic concurrency/ETags, stale-write rejection, event ordering, and fencing tokens.

## Duplicate safety

Every logical operation gets a stable ID that survives retries. The server records the ID and applies its effect atomically, usually with a uniqueness constraint or deduplication table in the same transaction as the state change. A repeated request returns the prior result or a deterministic duplicate response. If the response was lost after commit, retrying the same ID must not repeat the effect. See [RFC 9110 idempotent methods](https://datatracker.ietf.org/doc/html/rfc9110#section-9.2.2) and Microsoft's [idempotent consumer pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/idempotent-consumer).

## Stale writes and conflicts

Optimistic concurrency attaches an entity revision/ETag. A write carries the revision it read; the server accepts it only if that revision is still current, then increments it. A mismatch becomes an explicit conflict instead of silently overwriting newer work. Define a domain merge or user-resolution path. Timestamps alone are a poor ordering authority when client clocks differ.

## Ordering and fencing

Sequence numbers detect gaps and reordering within a defined stream. Fencing tokens are monotonically increasing ownership epochs; a storage service rejects operations from an older epoch after a newer owner takes over. They can protect lock/lease handoff, but require a single authority to issue epochs and enforcement at the resource being protected. They do not automatically solve semantic conflicts across devices.

## Test matrix

| Case | Expected invariant |
|---|---|
| Same event delivered twice | One business effect |
| Response lost after commit then retried | Original result returned, no duplicate |
| Revision 7 arrives after revision 8 | Stale write rejected or merged by explicit rule |
| Sequence 10 arrives before 9 | Gap/order policy is exercised |
| Old device owner writes after new epoch | Resource rejects stale fencing token |
