# 02 — Assigned systems and architecture diagrams

Haseeb requested a diagram for each assigned system showing architecture, components, data flow, integrations, and how the week's engineering principles apply.

| Participant | Assigned system / focus |
|---|---|
| Muhammad Arslan Waqar | Lingopal — Prefect |
| Hammad Mubeen | Lingopal — SQS |
| Muhammad Saad Faisal | Bluesky — Paymentology |
| Muhammad Muneeb | ShipIn |

These are assignment labels from Slack. This guide does not assert product internals; diagrams should be based on verified system knowledge, with uncertain edges marked as assumptions.

## Diagramming sequence

1. **Set scope:** user goal, system boundary, use cases, and non-goals.
2. **List actors/components:** client, API, identity provider, services, database, cache, queue, worker, and external integrations where applicable.
3. **Draw flows:** distinguish request/response from async messages; show data ownership and direction.
4. **Annotate state/failure:** persistence points, retries, duplicates, timeouts, bottlenecks, and recovery.
5. **Explain choices:** why a component exists, which quality attribute it supports, cost, and alternative.
6. **Connect principles:** ownership boundaries, cohesive modules, dependency direction, and test seams.

Walk through one normal request, then a failure path and a load spike. State which component is the source of truth. Label unknown internals as assumptions; do not present guesses as facts.

## Review checklist

- [ ] System boundaries and user goals are clear.
- [ ] Data flows and integrations are labeled.
- [ ] Synchronous and asynchronous work are distinguishable.
- [ ] Failure, retry, duplicate, and recovery paths are shown.
- [ ] Bottlenecks and scaling points have rationale.
- [ ] Design choices include trade-offs and evidence.
