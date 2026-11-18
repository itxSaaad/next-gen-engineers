# 03 — Transactions and concurrency

Week 5 adds explicit emphasis on locking, deadlocks, and race conditions. See [Week 4 foundations](../week-04-scalable-backend/02-transactions-and-concurrency.md).

- **Check-then-write races:** two requests can both observe availability. Put the invariant in a unique constraint, conditional update, version check, or lock.
- **Optimistic concurrency:** update only when expected version matches; zero rows means conflict. Useful when conflicts are uncommon and merge/retry behavior is defined.
- **Pessimistic locking:** lock rows for short critical sections where needed. Acquire in consistent order; avoid remote calls while locked.
- **Isolation:** PostgreSQL Serializable detects non-serializable interleavings and aborts a transaction that must be retried. Read Committed and Repeatable Read provide different visibility guarantees ([isolation](https://www.postgresql.org/docs/current/transaction-iso.html), [explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html)).
- **Deadlocks:** database aborts one participant. Log context, shorten transactions, acquire locks consistently, retry the whole transaction only when safe and bounded.
- **External effects:** a DB transaction cannot include payment/broker atomically. Use an outbox and idempotent consumer.

## Scenario

Two clients submit changes against revision 12. Specify the SQL predicate, version constraint, duplicate operation behavior, and outcome if a commit succeeds but its response is lost.
