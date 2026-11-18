# 03 — Event ordering and causal consistency

The Nov 2 standups explicitly mentioned event ordering and immutable execution results. Correctness requires defining where ordering matters and what each event refers to.

## Per-entity vs global order

Most business workflows need order within one entity (assessment/candidate/answer), not one global sequence for the entire system. A per-entity sequence partitions naturally and lets independent entities progress concurrently. If cross-entity invariants exist, coordinate them explicitly at the transaction/domain boundary.

## Sequence numbers, timestamps, and clocks

Use a monotonic server sequence or revision for authoritative order where possible. Timestamps describe time but do not prove causality: clocks drift, events can arrive late, and equal timestamps happen. Store client-created and server-received times separately. Detect sequence gaps, duplicate sequence values, and stale revisions.

## Late and duplicate events

Consumers should deduplicate by stable event ID, validate expected revision, and decide what to do when an event arrives out of order: buffer briefly, reject/retry, or reconcile from a snapshot. Do not process a later event against invalid prior state and silently continue.

## Immutable results and replay

An execution result should reference the exact source code revision, execution attempt, runtime/image version, and relevant test configuration. Treat it as an immutable record; a later run creates a new result. Event replay requires versioned schemas and deterministic handlers. Use event-sourcing only when audit/history and reconstruction needs justify its operational complexity.

## Exercise

Two device streams each contain revisions 20–22, with updates arriving 22, 20, 21 and duplicated 22. Define expected storage, dedupe key, ordering rule, conflict response, and UI state.
