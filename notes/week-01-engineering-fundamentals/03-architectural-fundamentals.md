# 03 — Architectural fundamentals

The technical curriculum's Week 1 agenda named loose coupling, high cohesion, separation of concerns, layered architecture, and dependency injection. The kickoff also asked everyone to explain system components and communication in one prior project.

## Separation of concerns, cohesion, and coupling

Separate responsibilities that change for different reasons. High cohesion keeps related rules/data together. Loose coupling limits assumptions between modules. Draw dependencies and data ownership; package names alone don't create boundaries. A useful module boundary has a clear responsibility and a small contract.

## Layered and ports/adapters architecture

The Week 1 example was Controller → Service → Repository. A fuller separation can distinguish:

- **Presentation:** HTTP/desktop/UI concerns, input/output mapping.
- **Application:** use-case orchestration and transaction boundaries.
- **Domain:** business rules and invariants.
- **Infrastructure:** database, queue, email, cloud SDK, and external adapters.

Not every application needs four deployable layers or a repository around every table. Keep business policy independent from transport and persistence where change/testing benefit justifies it. Dependency injection wires concrete implementations at the composition root.

## Domain boundaries and modular monolith vs. microservices

Use domain boundaries to group concepts with shared language, rules, and data ownership. A modular monolith can enforce boundaries in one deployment and avoid distributed-operation costs. Microservices add independent deployment/scaling and fault isolation, but also introduce network failure, eventual consistency, service ownership, observability, and operational overhead. Split services when organizational or workload needs justify the cost, not as a default badge of scale.

## Composition, inheritance, patterns, and reuse

Composition delegates behavior to collaborators; it often keeps variation explicit and avoids brittle base-class contracts. Inheritance is appropriate when a subtype truly honors the base contract. Design patterns are names for recurring trade-offs, not templates to insert without a problem. Reuse components when ownership and semantics are shared; over-abstraction creates indirection and accidental coupling.

## ADRs

An Architectural Decision Record should capture context, decision, alternatives, consequences, and revisit triggers. Keep it short, link it to code/design, and update with a new decision rather than silently rewriting the history.

## Practice

Diagram a real request. Mark trust boundaries, layers, state owners, and sync/async edges. Identify one domain boundary and defend whether it belongs inside a modular monolith or a separate service today.
