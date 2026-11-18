# 08 — System design and technical decisions

Week 5 expects a system diagram, technical decisions, and production scenario reasoning. Use [Week 4 deliverables and design template](../week-04-scalable-backend/09-design-and-decisions.md). A decision should explain assumptions, mechanism, failure mode, and evidence that could disprove it.

## Decision record template

### Decision: <short title>
- **Date / owner:**
- **Requirement and assumptions:**
- **Decision and rationale:**
- **Alternatives:**
- **Trade-offs / failure cases:**
- **Verification / metric:**
- **Revisit trigger:**

## Review questions

1. Does the diagram identify source of truth and data ownership?
2. Can two identical writes safely occur, and how is a lost response handled?
3. What saturates first under a spike; what is queued or rejected?
4. What remains available when Redis, DB, worker, or one app instance fails?
5. Which test/telemetry would show the design assumption is wrong?
