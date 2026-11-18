# 04 — Technical debt and maintainability

## Intentional and accidental debt

Intentional debt is a conscious shortcut with an understood cost and a reason to take it. Accidental debt comes from incomplete understanding, weak boundaries, or drift. Record the constraint, risk, affected area, owner, and trigger to revisit. A TODO without context rarely supports a decision.

## Refactoring and regression risk

Refactoring changes internal structure while preserving externally observable behavior. First define behavior with focused tests or characterization tests; make small changes; compare outputs and error paths. Regression risk depends on untested behavior, boundary count, and change size, not just test coverage percentage.

## Meaningful tests

Test important behavior and invariants at appropriate boundaries. Unit tests can explain domain rules; integration tests can verify DB constraints and transaction behavior; contract tests can protect API compatibility. A high line-coverage number can still miss stale writes, permissions, or failure recovery.

## Reviews and compatibility

Code review should check correctness, clarity, security, failure behavior, and maintainability. Design review should challenge assumptions, operational cost, migration path, and failure modes before implementation becomes expensive. Backward compatibility requires attention to API schemas, stored data, queued events, and clients deployed at different versions. Prefer additive migrations and explicit deprecation windows when old clients must continue working.

## Study prompts

- Which shortcut in an assigned system was deliberate, and what would trigger paying it down?
- What test protects the core invariant during a refactor?
- How would an older client behave after the API/event schema evolves?

## Sources

- [Fowler: Code smell](https://martinfowler.com/bliki/CodeSmell.html)
- [Microsoft architectural principles](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles)
