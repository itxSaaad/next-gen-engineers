# 01 — Offline-first data and state

Week 2 asks for a desktop assessment application to sync answers, code changes, execution results, and violation events. Its key invariant is that the interface must not claim submission is confirmed until the server confirms it, while locally committed answers survive recoverable failures.

## Make local durability explicit

Define what “saved” means. A keystroke, in-memory buffer, OS cache, and committed local transaction are different durability levels. In-memory storage is fast but lost on process/device crash; an embedded DB such as SQLite or a durable local journal can preserve state across restarts. Persist important changes locally before showing durable-saved state. Handle disk-full/local-DB errors without falsely reporting success. At startup, recover the journal, validate version/integrity, and rebuild the pending queue. Store answer state and its outbox event atomically so a crash cannot persist one but not the other. Encrypt local data when the threat model requires it; protect keys with OS secure storage.

## Model lifecycle explicitly

For example: `editing → locally_saved → queued → sending → server_acknowledged`. Failures return an item to queued with retry metadata. Final submission should distinguish `not_submitted`, `pending`, `confirmed`, and `needs_attention`. Avoid one ambiguous `synced` boolean. Keep execution lifecycle separate from answer persistence so an execution timeout does not erase code or result history.

## Classify data and ordering

Answers are state-like: newer revisions may supersede older ones. Violation events and audit records are event-like: dropping or reordering them may be invalid. Execution results should identify the code revision and attempt that produced them. Give each object stable identity and a local sequence/revision where order matters.

## Local working state vs server authority

The desktop may own a local working copy so reads and writes remain available offline. The backend remains authoritative for shared state, authorization, and final submission. This hybrid model means local state can be temporarily stale or conflict with another device. Make that divergence visible and reconcile with revisions; don't label an unacknowledged local write as globally saved.

## UX and bounded storage

Show local-save state separately from server-sync state: “saved on this device,” “waiting to sync,” and “accepted by server.” Bound logs and execution output; never silently discard unacknowledged critical events. Define behavior for device loss, corruption, and multi-device use.

## Study questions

- What transaction makes an answer durable locally?
- Which records can be compacted to latest state, and which require event history?
- What must be backed up, encrypted, retained, or erased?
- How can the UI truthfully present confirmation during a network partition?
