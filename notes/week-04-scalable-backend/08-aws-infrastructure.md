# 08 — AWS infrastructure and compute choices

**Scope provenance:** The five-module AWS masterclass outline below comes from the expanded study material supplied for this guide. Haseeb's Slack assignment specifically required scalable backend design; it did not itself list every service in this chapter. Use this as a study checklist and validate service fit against current AWS documentation and workload constraints.

## Start from requirements

Decide traffic shape, latency/availability targets, data durability, network exposure, compliance, team operations capacity, deployment frequency, and cost constraints before selecting services. A managed service removes some operational work but still has quotas, failure modes, security configuration, and cost. Avoid diagramming every AWS icon: include only components justified by a requirement.

## Compute choice guide

| Option | Control/operations | Often fits when | Questions |
|---|---|---|---|
| **EC2** | VM and OS control; team manages patching/runtime | Specialized host or full OS control is needed | Who patches, scales, replaces, and hardens instances? |
| **ECS** | AWS-native container orchestrator | Containers are wanted with a simpler AWS-integrated orchestration path | Who owns task scheduling, networking, deployment, and scaling? |
| **EKS** | Kubernetes control plane/ecosystem; more Kubernetes concepts/operations | Kubernetes APIs/ecosystem or existing platform investment is required | Is the portability/extension value worth the operational load? |
| **Fargate** | AWS-managed serverless container capacity used with ECS or EKS | Avoid managing container hosts while retaining container packaging | What resource size, startup, networking, and cost model fit? |
| **Lambda** | Event-driven function execution with service-managed scaling | Short-lived event/request tasks fit function limits and execution model | Cold/startup, concurrency, DB connections, timeout, and state constraints? |

Fargate is a compute option for containers, not an orchestrator in the same sense as ECS/EKS. AWS's current [compute decision guide](https://docs.aws.amazon.com/decision-guides/latest/decision-guides/choosing-aws-compute-service.html) and [container decision guide](https://docs.aws.amazon.com/decision-guides/latest/decision-guides/choosing-aws-container-service.html) help compare these choices. The guild's earlier reported ECS/EC2/EKS and Fargate/Lambda/EC2 comparison is recorded in the [Week 4 research log](10-research-log.md).

## Five-module AWS masterclass checklist

### Module 1 — Foundation and routing

- Capacity sizing and regional/global design.
- DNS with Route 53.
- Global Accelerator vs. CloudFront: network routing vs. content delivery/cache use cases.
- WAF and Shield as distinct web-layer and DDoS protection controls.
- Public/private network entry and trust boundaries.

### Module 2 — Ingress and compute

- API Gateway for managed API front doors and API-specific features.
- ALB for HTTP-aware load balancing; NLB for transport-level/network load balancing.
- EC2, ECS, EKS, Fargate, and Lambda choices from the table above.
- Autoscaling signals, deployment strategies, health checks, rollback, and graceful shutdown.

### Module 3 — Data, cache, and storage

- ElastiCache for in-memory cache patterns; define cache consistency/failure behavior.
- RDS/Aurora for relational workloads; evaluate transaction and connection behavior.
- DynamoDB for key-value/document access patterns; model keys/partition distribution first.
- S3 for object storage and EBS for block storage attached to compute.
- File uploads, integrity checks, consistency, retention, backup, and restore drills.

### Module 4 — Async processing and reliability

- SQS queue delivery/visibility/DLQ semantics; SNS fan-out; EventBridge event routing.
- Transactional outbox, retries, idempotency, event versioning, and ordering boundaries.
- Queue-based load leveling and worker scaling against queue age/depth and DB limits.
- Fault isolation, circuit breakers, timeouts, recovery, and replay controls.

Conceptually, use **SQS** when consumers need to pull and process queued work; **SNS** when a publisher fans notifications out to subscribers; **EventBridge** when routing events by rules between producers and targets. They can be combined, but each adds delivery, retry, ordering, and permissions decisions. Check the service's current delivery semantics before relying on exactly-once or order.

### Module 5 — Production systems

- Scaling/capacity, monitoring and observability, security, cost, availability, performance, and architecture trade-offs.
- Define SLOs and error budgets appropriate to service importance.
- IAM least privilege, secret storage, encryption, network boundaries, audit logs, and incident response.
- Model cost for steady state and peak; check quotas and failure-region behavior.

The service-specific designs should reference official [AWS architecture and decision guides](https://docs.aws.amazon.com/decision-guides/latest/decision-guides/choosing-aws-compute-service.html), [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html), [SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html), and [S3 multipart upload](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html) documentation.

## Learning cycle for each service

1. State the problem and quality attribute.
2. Explain the service's core mechanics and limits.
3. Compare a realistic alternative.
4. Draw the request/data flow and security boundary.
5. Apply it to the assessment/backend use case.
6. Break the design with outage, duplicate, overload, and unauthorized-access scenarios.
7. Defend cost, complexity, and the trigger to change the design.
8. Revisit later from memory and answer a scenario without notes.
