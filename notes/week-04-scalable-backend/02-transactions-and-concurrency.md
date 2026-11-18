# 02 — Transactions and concurrency

Use transactions to make a set of related database changes atomic. ACID summarizes atomicity, consistency, isolation, and durability; the chosen isolation level determines which concurrent anomalies are prevented and which retries/locks are required.

## Match isolation to invariant

Read committed is a common baseline but a transaction can see new committed data between statements. Repeatable read provides a stable transaction snapshot in PostgreSQL, while serializable detects executions that cannot be equivalent to a serial order and may abort one transaction. Applications must retry serialization failures safely. PostgreSQL documents isolation behavior and trade-offs in [transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html).

## Prevent races

“Read, check, then write” can race when two requests act concurrently. Encode invariants in unique/check constraints; use atomic conditional updates (e.g., decrement inventory only where available > 0); use optimistic version columns for conflicts; or lock rows when contention/invariant requires it. Keep transactions short and acquire locks in consistent order to reduce deadlocks. Retrying a deadlock/serialization abort is safe only when the operation is idempotent and side effects are not duplicated.

## External side effects

A database transaction does not atomically include a payment gateway or message broker. Do not hold DB locks while calling a slow remote API. Use an outbox written in the same transaction as business state, then publish asynchronously; make the consumer idempotent. For multi-step distributed workflows, define compensating actions and observable states rather than claiming global ACID.

## CAP theorem in context

CAP is about trade-offs in distributed data systems under a network partition: a system cannot guarantee both linearizable consistency and availability for every request during the partition. It is not a universal rule that every architecture must “pick any two” at all times. Define the operation's consistency requirement, partition behavior, and recovery model. A single PostgreSQL transaction is not itself a CAP design exercise; the question becomes relevant when data is replicated across nodes/services.

## CDC vs. SCD

These acronyms describe different layers. **Change Data Capture (CDC)** records/streams row-level inserts, updates, and deletes from a source system so another consumer can process changes. **Slowly Changing Dimensions (SCD)** are data-warehouse modeling patterns for how dimension history is stored: Type 1 overwrites old values; Type 2 keeps versions/effective periods. CDC can feed an SCD Type 1 or Type 2 target; they are not alternatives at the same level. See [Microsoft Fabric CDC and SCD overview](https://learn.microsoft.com/fabric/data-factory/cdc-copy-job) and [SCD modeling](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#slowly-changing-dimensions).

## Discussion scenario

Two identical “submit answer” requests arrive concurrently. Specify the unique key, revision check, transaction boundaries, duplicate response behavior, and what happens if commit succeeds but the HTTP response is lost.
