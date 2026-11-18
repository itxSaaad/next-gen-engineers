# Next-Gen Engineers — System Architecture & Engineering Leadership

Welcome to the **Next-Gen Engineers** repository by Muhammad Saad. This repository houses the curriculum notes, production architecture blueprints, weekly engineering deliverables, and hands-on implementations for the system design and leadership program led by Muhammad Haseeb Malik.

---

## 📂 Repository Structure

```
next-gen-engineers/
├── notes/                                  # Structured study guides & research logs (Weeks 1–5)
│   ├── 00-program-guide.md
│   ├── week-01-engineering-fundamentals/
│   ├── week-02-reliable-desktop-sync/
│   ├── week-03-data-consistency-security-scaling/
│   ├── week-04-scalable-backend/
│   └── week-05-scalable-backend/
│
├── week-04-scalable-backend/               # Week 4 Assignment Deliverable
│   ├── README.md
│   ├── technical-design-doc.md             # Scalable backend system design document & architecture
│   └── distributed-rate-limiter/           # Distributed rate limiter implementation & benchmarks
│
├── week-05-redis-caching-scalability/      # Week 5 Assignment Deliverable (Haseeb's Core Brief)
│   ├── README.md
│   ├── technical-design-doc.md             # In-depth design: Endpoints, Caching, Rate Limiting, Failure Recovery
│   └── implementation/                     # Production-grade working implementation (FastAPI, Redis, Docker)
│       ├── app/
│       ├── tests/
│       └── docker-compose.yml
│
└── capstone-project/                       # Capstone Project & Final Production System Deliverable
    └── README.md
```

---

## 🎯 High-Volume Assessment & Candidate Platform (Week 5 Focus)

### Core Assignment Objectives
1. **Endpoint Design**: High-volume candidate & assessment APIs with cursor-based pagination and deterministic filtering.
2. **Redis Caching Strategy**: Hierarchical key design, tiered TTLs, cache-aside with write-through/invalidation, and cache stampede protection.
3. **Distributed Rate Limiting**: Redis Sliding-Window / Token-Bucket algorithms implemented via atomic Lua scripts with client/endpoint tiers.
4. **Resilience & Invalidation Strategy**: Event-driven invalidation, Stale-While-Revalidate, Circuit Breakers, and graceful degradation during Redis outages.

**Target Evaluation**: Passing standard is **4.5 / 5.0 (90%)**; designed and defended for a perfect **5.0 / 5.0**.
