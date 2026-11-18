# 00 — Program guide: system design, architecture, and engineering leadership

## Why this program exists

On [2026-10-18](https://app.slack.com/archives/C0CA0S502AH/p1792348055844489), Muhammad Haseeb Malik introduced a structured program to improve system-design thinking, technical judgment, production ownership, communication, and leadership. The intended outcome is to design, scale, and operate maintainable, reliable systems—not simply learn tools.

## Program curriculum named at kickoff

- System-design fundamentals and engineering principles.
- Software architecture and design patterns.
- Database design, optimization, and scaling.
- Caching, queues, and asynchronous processing.
- Distributed systems and fault tolerance.
- Scalability, performance, and capacity planning.
- Infrastructure, Docker, AWS, and deployment architecture.
- Observability: logs, metrics, traces, monitoring, alerts.
- Production reliability, security, and incident management.
- System-design case studies.
- Leadership, ownership, communication, and technical decisions.

Haseeb said to apply these to the team's stack: Python, Django, DRF, FastAPI, PostgreSQL, Redis, Celery, and AWS. He asked the group to focus on engineering judgment rather than repeat basics.

## Working method and expectations

- Progress through concepts with practical examples and production scenarios.
- Post daily learning updates in the channel; mention reasons when missing planned activity.
- Review designs, challenge assumptions, discuss trade-offs, and learn from mistakes.
- Rotate one weekly leader to collect updates, follow up, and keep the group on track.
- Kickoff expectation: each person presents a prior-project system design, explains components and decisions, and discusses scaling, faults, database performance, caching, queues, observability, bottlenecks, and improvements.
- Week 1 later specified one hour of learning per day, five hours per week, and Monday evaluation / Friday design discussion.

## How to study from this guide

For each chapter, explain the invariant, alternatives, failure modes, and verification plan in your own words. Draw data/request flows. Link actual deliverables and log real sessions. These notes summarize assignment scope and researched concepts; they do not claim an individual completed work.

## Preparation cycle

1. Understand the problem and why the concept exists.
2. Learn terminology, mechanisms, and constraints.
3. Compare alternatives and trade-offs.
4. Visualize it with a diagram, sequence, state machine, or data model.
5. Apply it to a real system in the assessment/recruitment platform.
6. Break it with failures, duplicates, concurrency, timeouts, overload, and attack scenarios.
7. Defend the design, costs, and conditions that would trigger a change.
8. Revisit later from memory and answer scenarios without notes.

## Five-hour weekly preparation plan

Haseeb's Week 1 expectation was one hour per day, five hours per week. A practical structure:

| Session | 60-minute plan | Output |
|---|---|---|
| 1 — Recall and frame | 10 min recall; 20 min clarify requirements; 20 min read; 10 min open questions | One-sentence problem and assumptions |
| 2 — Understand | 10 min retrieval; 35 min study one topic; 15 min explain it without notes | Concept summary and source |
| 3 — Compare | 10 min recall; 25 min compare alternatives; 25 min trade-off table | Decision options and when each fits |
| 4 — Apply | 10 min recall; 35 min diagram/design; 15 min failure walkthrough | Updated architecture or sequence/state diagram |
| 5 — Defend | 10 min recall; 30 min scenarios; 20 min review and next steps | Design defense, gaps, evidence links |

Add dated entries to that week's research log. You are ready when you can state the problem, describe the mechanism, compare an alternative, walk through a failure, and cite the source or test behind the decision.

## Week map

- [Week 1](week-01-engineering-fundamentals/README.md): clean code/SOLID, assigned system diagrams, URL shortener.
- [Week 2](week-02-reliable-desktop-sync/README.md): offline-first reliable assessment synchronization.
- [Week 3](week-03-data-consistency-security-scaling/README.md): conflicts, security, and scaling; standups report continued Week 2 sync work, expanded by the supplied outline.
- [Week 4](week-04-scalable-backend/README.md): scalable backend design and distributed rate limiter.
- [Week 5](week-05-scalable-backend/README.md): required deeper continuation of Week 4.

## Slack record timeline

- **2026-10-18:** program kickoff and broad curriculum; first prior-project system-design assignment.
- **2026-10-20:** [Week 1 topics and assignments](https://app.slack.com/archives/C0CA0S502AH/p1792505770722239), schedule, weekly leader, URL-shortener discussion, and study-hour expectation.
- **2026-10-21:** Haseeb shared URL-shortener requirement-extraction [article and videos](https://app.slack.com/archives/C0CA0S502AH/p1792531582687699).
- **2026-10-26:** [Week 2 reliable desktop synchronization brief](https://app.slack.com/archives/C0CA0S502AH/p1793037494033859); Hammad named leader.
- **2026-11-10:** [Week 4 scalable backend assignment](https://app.slack.com/archives/C0CA0S502AH/p1794322873661849), technical deliverables, and Friday distributed API rate limiter.
- **2026-11-17:** [Week 5 continuation](https://app.slack.com/archives/C0CA0S502AH/p1794929453790629) and deeper production scenarios after insufficient preparation.
- **2026-11-18:** latest channel history included a [YouTube link](https://app.slack.com/archives/C0CA0S502AH/p1794983426432089) without assignment details; its title is about designing for one million requests per second.

No distinct Week 3 assignment is present in the reviewed channel history. Meeting logistics, automated reminders, and bare links do not establish research outcomes. The expanded Week 3 scope is attributed to the supplied preparation outline.
