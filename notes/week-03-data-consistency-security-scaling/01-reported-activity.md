# 01 — Reported activity and study scope

No separate Haseeb assignment was located for this period. The notes below organize standup content from the continued Week 2 sync work and connect it to the expanded preparation outline supplied by the user. Dates are Slack dates; summaries are participant reports, not independently verified implementation or mastery.

## Reported topics

- **2026-11-02:** Hammad described unique IDs/idempotency for duplicate changes, server versions to reject stale writes, and fencing tokens as a possible defense against concurrent device sessions. Arslan and Muneeb reported researching idempotent operations and duplicate/conflict approaches. Saad listed idempotency keys, transactional deduplication, optimistic concurrency/ETags, stale updates, event ordering, and keeping execution results immutable and tied to code revisions.
- **2026-11-03:** Hammad discussed threats from the candidate, network, and malicious code sent to the runner. Saad reported BOLA/object-level access risks, token expiry, secure local storage, API security, code sandboxing, and compromised-client isolation.
- **2026-11-04:** Saad reported continued study of duplicate/conflict handling and security, including revision checks, server authorization, token handling, and limiting compromised-client access.
- **2026-11-05:** Saad covered synchronized reconnect surges, database pressure, API latency, backpressure, rate limiting, and worker concurrency. Arslan shared offline-first/local-first and sync resources.
- **2026-11-06:** Arslan reported reviewing API types. Hammad covered large file chunking, large offline backlog, half-failed uploads, and slow networks.

Sources: [Nov 2](https://app.slack.com/archives/C0CA0S502AH/p1793624423947769), [Nov 3](https://app.slack.com/archives/C0CA0S502AH/p1793710819407539), [Nov 4](https://app.slack.com/archives/C0CA0S502AH/p1793797213006019), [Nov 5](https://app.slack.com/archives/C0CA0S502AH/p1793883619120909), [Nov 6](https://app.slack.com/archives/C0CA0S502AH/p1793970009510299).

## Learning objective for this continuation

Connect each mechanism to a failure it prevents: idempotency to duplicate delivery, revision/fencing to stale or concurrent writers, authorization to cross-user access, backpressure to overload, and chunk/checkpointing to partial large uploads. Compare each with alternatives and define a test that proves the invariant.
