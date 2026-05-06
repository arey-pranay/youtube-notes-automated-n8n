# Distributed Transactions: ACID vs. Sagas

## TL;DR
Distributed transactions ensure data consistency across multiple services, often using ACID properties. However, in large-scale distributed systems, ACID transactions can be problematic due to blocking and performance issues. The Saga pattern offers an alternative, managing distributed transactions through a sequence of local transactions with compensating actions to handle failures, ensuring eventual consistency.

## Key Takeaways
- ACID properties (Atomicity, Consistency, Isolation, Durability) guarantee strong consistency in transactions.
- Two-Phase Commit (2PC) is a common protocol for distributed transactions but suffers from blocking and performance bottlenecks at scale.
- The Saga pattern breaks down a distributed transaction into a series of local transactions, each with a corresponding compensating action.
- Choreography-based sagas use event-driven communication between services, while orchestration-based sagas use a central orchestrator.
- The transactional outbox pattern ensures that events are published reliably after a local transaction commits.

## Timestamped Sections
| Timestamp | Topic | What You Need to Know |
|-----------|-------|----------------------|
| 00:00 | Introduction to Transactions | When building applications, transactions are crucial for maintaining data integrity. |
| 00:01 | Basic Transaction Flow | A typical transaction involves charging a card, reserving inventory, and recording the transaction. |
| 00:13 | Transaction Failure | If any part of a transaction fails, the system should roll back all changes to maintain consistency. |
| 00:18 | ACID Guarantees | Databases provide ACID guarantees (Atomicity, Consistency, Isolation, Durability) to ensure reliable transactions. |
| 00:25 | Atomicity | Atomicity ensures that all operations within a transaction either complete successfully or none of them do. |
| 00:35 | Isolation | Isolation ensures that concurrent transactions do not interfere with each other, preventing data corruption. |
| 00:47 | Database Handling | Databases manage transaction complexity internally, allowing developers to focus on application logic. |
| 00:51 | Scaling Challenges | As applications scale, a single database can become a bottleneck, leading to performance issues. |
| 01:00 | Sharding and Microservices | To scale, databases can be sharded across multiple machines or broken down into microservices, each with its own database. |
| 01:20 | Distributed Transactions | When transactions span multiple services and databases, managing consistency becomes complex. |
| 02:08 | Distributed Transaction Problem | A single logical operation spanning multiple independent databases or services presents a challenge for maintaining consistency. |
| 02:23 | Two-Phase Commit (2PC) | 2PC is a classic solution for distributed transactions, involving a coordinator and participants. |
| 02:34 | 2PC Phases | Phase 1 (Prepare): Coordinator asks participants if they can commit. Phase 2 (Commit/Abort): Coordinator decides based on participant responses. |
| 03:53 | Why 2PC Fails at Scale | 2PC is a blocking protocol, and failures in any participant can halt the entire transaction, leading to deadlocks and performance issues. |
| 04:43 | 2PC Failure Scenarios | Slow participants or network partitions can cause transactions to stall indefinitely. |
| 05:16 | Pat Helland's Paper | Pat Helland's paper "Life beyond Distributed Transactions: an Apostle's Opinion" highlights the challenges of distributed transactions at internet scale. |
| 05:51 | The Saga Pattern | Sagas offer an alternative to 2PC, focusing on eventual consistency through a sequence of local transactions and compensating actions. |
| 06:14 | Saga Choreography | In choreography, services react to each other's events without a central orchestrator. |
| 07:22 | Saga Orchestration | In orchestration, a central orchestrator manages the sequence of transactions and compensating actions. |
| 08:30 | Orchestration Example | An orchestrator calls each service in sequence, waiting for confirmation before proceeding. |
| 09:36 | Making Sagas Reliable | Idempotent operations and transactional outbox patterns are key to building reliable sagas. |
| 10:40 | The Dual Write Problem | A common issue where a service tries to write to both a database and a message broker, leading to inconsistencies if one fails. |
| 11:11 | Transactional Outbox | Solves the dual write problem by writing to the database and an outbox table transactionally, then publishing events from the outbox. |
| 12:23 | Decision Framework | When designing distributed transactions, consider if a distributed transaction is truly necessary. |
| 14:07 | YugabyteDB Example | Distributed SQL databases like YugabyteDB can handle distributed transactions internally, simplifying development. |
| 14:40 | Saga Orchestration Benefits | Orchestration provides better visibility and control over the transaction flow, especially for complex sagas. |

## Core Concepts Explained

### ACID Properties
ACID is a set of properties that guarantee the reliability of database transactions.
- **Atomicity:** Ensures that all operations within a transaction are completed successfully, or none are. If any operation fails, the entire transaction is rolled back.
- **Consistency:** Guarantees that a transaction brings the database from one valid state to another, maintaining data integrity rules.
- **Isolation:** Ensures that concurrent transactions do not interfere with each other. Each transaction appears to execute in isolation, preventing race conditions and data corruption.
- **Durability:** Guarantees that once a transaction has been committed, it will remain committed even in the event of system failures (like power outages or crashes).

### Two-Phase Commit (2PC)
2PC is a distributed transaction protocol that ensures all participants in a distributed transaction either commit or abort together. It involves a coordinator and multiple participants.
- **Phase 1 (Prepare):** The coordinator sends a "prepare" request to all participants. Each participant must then ensure it can commit the transaction and locks the necessary resources. If a participant can commit, it responds with "yes"; otherwise, it responds with "no."
- **Phase 2 (Commit/Abort):** If the coordinator receives "yes" from all participants, it sends a "commit" command. If any participant responds with "no" or times out, the coordinator sends an "abort" command. This ensures that all participants either commit or abort, maintaining atomicity.

### Saga Pattern
The Saga pattern is an alternative to distributed transactions for managing data consistency across multiple services. Instead of a single, atomic transaction, a saga is a sequence of local transactions. Each local transaction updates data within a single service and then triggers the next local transaction in the sequence. If a local transaction fails, the saga executes a series of compensating transactions to undo the preceding local transactions, effectively rolling back the entire operation.

#### Choreography vs. Orchestration
- **Choreography:** In this approach, each service involved in the saga emits events when it completes its local transaction. Other services listen for these events and react accordingly, triggering their own local transactions or compensating actions. There's no central coordinator.
- **Orchestration:** A central orchestrator (often a dedicated service) manages the entire saga. It explicitly tells each participant service what to do and when, and handles compensating actions if a step fails.

### Transactional Outbox
The transactional outbox pattern is a reliable way to publish events from a service after a local transaction commits.
1.  **Atomic Write:** The service writes its data changes and the event to be published to its database within a single atomic transaction.
2.  **Outbox Table:** The event is written to a special "outbox" table in the same database.
3.  **Event Publishing:** A separate process (or the service itself) monitors the outbox table and publishes the events to a message broker or event bus.
This ensures that an event is only published if the transaction successfully commits, preventing data inconsistencies.

## Interview Perspective
### Why This Matters
Understanding distributed transactions and patterns like Sagas is crucial for designing scalable and reliable microservice architectures. Interviewers want to see if you can identify the trade-offs between strong consistency (ACID) and eventual consistency (Sagas) and choose the appropriate pattern for different scenarios.

### Concepts Likely to Be Asked
- **ACID vs. BASE:** Be prepared to discuss the differences between ACID (Atomicity, Consistency, Isolation, Durability) and BASE (Basically Available, Soft state, Eventually consistent) and when each is appropriate.
- **2PC Drawbacks:** Explain why 2PC is often avoided in microservices due to blocking, performance, and availability issues.
- **Saga Implementation:** Describe how to implement sagas using either choreography or orchestration, and the pros/cons of each.
- **Idempotency:** Explain why idempotent operations are critical for sagas, especially for compensating actions.
- **Transactional Outbox:** Explain how this pattern ensures reliable event publishing in distributed systems.

### At a Glance Checkpoints
- [ ] Can you explain the ACID properties and why they are important for transactions?
- [ ] Can you explain the two phases of the Two-Phase Commit protocol and its limitations?
- [ ] Can you explain the Saga pattern, including choreography and orchestration?
- [ ] Can you explain the transactional outbox pattern and why it's used?
- [ ] Can you give an example of a compensation action in a Saga?

## Quick Reference
- **ACID:** Atomicity, Consistency, Isolation, Durability.
- **2PC:** Two-Phase Commit (Prepare, Commit/Abort). Blocking, prone to deadlocks.
- **Saga:** Sequence of local transactions with compensating actions. Eventual consistency.
- **Choreography:** Event-driven, decentralized control.
- **Orchestration:** Centralized control, explicit commands.
- **Transactional Outbox:** Ensures reliable event publishing by writing events to a database table within the same transaction as data changes.
- **Idempotency:** Operations can be executed multiple times without changing the result beyond the initial execution. Crucial for retries and compensating actions.

## Metadata
**Category:** System Design
**Tags:** `distributed transactions`, `ACID`, `Saga pattern`, `2PC`, `choreography`, `orchestration`, `transactional outbox`, `idempotency`
**Interview Relevance:** Must Know
**Difficulty:** Intermediate
**Est. Read Time:** 10 min

---

**Source:** https://www.youtube.com/watch?v=DOFflggE_0Q  
**Saved:** 2026-05-06T17:32:47.243Z
**AI Source:** gemini
