# 02 — SOLID principles

SOLID is a set of design heuristics for managing change. Apply them to reduce concrete coupling and contract failures; don't treat them as a mandate to create an interface or class for every type.

## S — Single Responsibility Principle

A module should have one cohesive responsibility and one primary reason to change. Gather behavior that changes together; separate behavior with unrelated change pressures. Example: separating invoice calculation from email delivery lets each evolve independently.

## O — Open/Closed Principle

Extend behavior without repeatedly modifying stable core logic. A policy interface or strategy can help when a real variation point exists. A giant hierarchy or plugin system created for hypothetical future cases adds complexity rather than extensibility.

## L — Liskov Substitution Principle

An implementation must preserve the expectations of the abstraction it replaces. It must honor valid inputs, output guarantees, invariants, and error behavior. A subclass that unexpectedly rejects a valid base-class input violates substitutability.

## I — Interface Segregation Principle

Consumers should not depend on operations they don't use. Split a broad interface when different clients rely on separate capabilities or change at different rates. Keep the interface cohesive; don't split it into meaningless one-method abstractions automatically.

## D — Dependency Inversion Principle

High-level business rules depend on abstractions owned by the policy boundary, not on low-level database, queue, or HTTP implementations. Dependency injection supplies concrete adapters at the composition root. This makes dependencies explicit and supports focused tests, but does not make every dependency replaceable in production.

## Diagnostic exercise

For one feature, draw a dependency graph from UI/controller to domain logic to persistence/external service. Mark policy vs detail. Identify one dependency that should point inward, one contract that needs tests, and one abstraction that can be removed.

## References

- [Microsoft architectural principles](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles)
- [Microsoft dependency injection guidelines](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection-guidelines)
- [Martin Fowler on dependency injection](https://martinfowler.com/articles/injection.html)
