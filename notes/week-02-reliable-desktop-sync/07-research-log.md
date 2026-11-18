# Research log — Week 2

## Guide research — 2026-11-18

Consulted the HTTP semantics standard for idempotency and retry behavior, AWS guidance on transactional outbox, and Microsoft reliability patterns for retries/backoff. The chapters apply these concepts to Haseeb's assignment scenarios; no implementation or participant testing is claimed.

## Slack-reported learning updates (2026-10-27 to 2026-10-30)

These summaries reflect participant standups, not independent validation.

- **2026-10-27:** Reports covered offline-first local storage, synchronization strategies, event-driven architecture, idempotency, conflict handling, stable IDs, revision checks, and safe retry recovery. Saad explicitly reasoned about atomically saving answers with pending sync records and handling crashes, lost responses, and reconnect surges. Hammad and Muneeb reported studying the first architecture/sync topics.
- **2026-10-29:** Reports covered authentication/token expiry, secure local credential storage, resuming queued work after reauthentication, event IDs/revisions/ordering/persistent queues, duplicate/stale handling, and tying immutable execution results to the exact code revision.
- **2026-10-30:** Hammad reported studying p95/p99 latency and distinguishing logs, metrics, and traces while moving toward a system diagram. Saad reported fault tolerance, state management, authentication, and performance; Muneeb reported broad coverage with deeper review still needed.

Sources: [2026-10-27 standup thread](https://app.slack.com/archives/C0CA0S502AH/p1793106030663159), [2026-10-29 standup thread](https://app.slack.com/archives/C0CA0S502AH/p1793278830069789), [2026-10-30 standup thread](https://app.slack.com/archives/C0CA0S502AH/p1793365220138339).

### Session template

#### YYYY-MM-DD — Topic
- **Question:**
- **What I read / tried:**
- **Findings:**
- **Failure scenario tested:**
- **Source links:**
- **Open questions / next step:**

## Checklist

- [ ] Durable local writes and recovery semantics.
- [ ] Event identity, ordering, idempotency, and conflict policy.
- [ ] Retry/backoff and reconnect storm controls.
- [ ] Explicit state machine for save, sync, execution, and submission.
- [ ] Authentication and local data threat model.
- [ ] Failure and load test plan for stated scenarios.
- [ ] Record actual research sessions and time spent.
