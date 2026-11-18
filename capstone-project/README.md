# Capstone Project: High-Throughput Distributed Candidate Assessment & Evaluation Platform

## Overview
This folder is dedicated to the capstone project for the Next-Gen Engineers curriculum. It synthesizes the full scope of system design, distributed data synchronization, scalable backend architectures, high-performance Redis caching, and real-time observability.

---

## Architecture Pillars
1. **Offline-First Reliable Synchronization**: Resilient client sync protocols, local SQLite queues, and idempotent event replay.
2. **High-Throughput Ingestion & Evaluation**: Distributed Celery / Redis Streams task pipeline for automated code and assessment grading.
3. **Data Consistency & Caching**: Multi-tier Redis caching, stampede protection, database connection pooling with PgBouncer, and read-replica distribution.
4. **Resilience & Security**: Distributed rate limiting, mutual TLS / request signing, circuit breakers, and graceful degradation under catastrophic outages.
