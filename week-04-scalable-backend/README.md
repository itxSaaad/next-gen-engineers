# Week 4 Assignment Deliverable: Scalable Backend Architecture

## Overview
This folder contains the official submission for the Week 4 scalable backend engineering assignment.

### Core Objectives
1. **System Architecture**: High-level and component diagrams showing traffic flow from clients through load balancers, application clusters, PgBouncer connection pools, PostgreSQL primaries and read replicas, Redis caches, and Celery background workers.
2. **Technical Design Document (`technical-design-doc.md`)**:
   - Database schema & composite index strategies
   - SQL query optimization and N+1 prevention
   - Transaction boundaries and concurrency isolation
   - Connection pool sizing formulas for high-concurrency workloads
   - Redis caching layers and invalidation triggers
   - Horizontal scaling, auto-scaling thresholds, and bottleneck remediation
3. **Distributed Rate Limiter**:
   - Comparison of Fixed Window, Sliding Window Log, and Token Bucket
   - Shared Redis state management across stateless app instances
   - Failure-handling and fallback behaviors

---

### Files
- [technical-design-doc.md](file:///d:/Projects/next-gen-engineers/week-04-scalable-backend/technical-design-doc.md) — Comprehensive technical design document.
- `distributed-rate-limiter/` — Reference implementation & benchmarks.
