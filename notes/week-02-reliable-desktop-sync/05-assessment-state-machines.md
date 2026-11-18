# 05 — Assessment and synchronization state machines

Represent workflows with explicit states and valid transitions rather than scattered booleans. Persist enough state to recover after restart; make side effects idempotent or record them transactionally with the transition.

## Assessment lifecycle example

`Created → Started → InProgress → Paused → InProgress → Submitted → EvaluationPending → Evaluated → Reviewed`

Alternative transitions may include `Started → Expired`, `InProgress → Expired`, and `InProgress → Submitted`. Define legal transitions, authorized actors, and which transitions require an online server check.

## Sync lifecycle

`LocalDirty → LocallyDurable → PendingUpload → Uploading → ServerAcknowledged`

Transient failure returns `Uploading → PendingUpload` with retry metadata. Conflict can transition to `ConflictNeedsResolution`; expired credentials to `WaitingForAuthentication`. Final submission is distinct from autosave and becomes `Confirmed` only after server acknowledgement.

## State-machine concepts

- **Guard:** precondition for transition, such as matching revision.
- **Invariant:** always-true rule, e.g., confirmed submission has a server receipt.
- **Side effect:** DB write, publish, notification; make it recoverable/idempotent.
- **Persistence:** atomically store state and outbox/sequence where required.
- **Crash recovery:** reload durable state and resume without repeating effects.
- **Illegal transition:** reject explicitly and log diagnostics without leaking secrets.

## Exercise

Draw answer autosave, sync, code execution, and final-submission states. For each edge, state actor, guard, persisted update, emitted event, retry behavior, and user-visible label. Include a process crash between every pair of side effects.
