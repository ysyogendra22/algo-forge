# System Design Study Roadmap

For a beginner from a mobile development background preparing for FAANG system design interviews.

Study the numbered topics in order. Focus on understanding request flows, choosing components, explaining trade-offs, and handling failures. This roadmap covers high-level system design; coding and low-level design need separate preparation.

## 1. Client & Server Basics

- Client, server, frontend, and backend.
- How a mobile app communicates with a backend.
- Requestâ€“response lifecycle.
- Trace one example: loading a list of posts.

## 2. Networking and HTTP

- IP addresses, domain names, ports, and DNS.
- TCP vs UDP: purpose and basic differences only.
- HTTP vs HTTPS.
- Request and response: headers, body, methods, and status codes.
- Connections and timeouts.

## 3. API Basics

- Endpoints, REST, and JSON.
- Pagination: offset vs cursor.
- Authentication vs authorization.
- Sessions and tokens.
- Input validation and error responses.

## 4. Backend Basics

- Request handling and business logic.
- Reading and writing database records.
- Synchronous processing vs background work.
- Trace an API request from the app to the database and back.

## 5. Databases and Data Modeling

- Tables, rows, columns, primary keys, and foreign keys.
- CRUD: create, read, update, and delete.
- Basic SQL and joins.
- One-to-one, one-to-many, and many-to-many relationships.
- Design schemas around required queries.
- Normalization vs denormalization.

## 6. Indexes, Transactions, and Concurrency

- Indexes and composite indexes.
- Read benefits vs write and storage costs.
- Transactions and ACID: atomicity, consistency, isolation, durability.
- Isolation basics and concurrent updates.
- Optimistic vs pessimistic locking.
- Example: preventing two users from booking the same seat.

## 7. Practical Checkpoint: Notes Backend

- Build create, list, update, and delete APIs.
- Use one server and one database.
- Connect a mobile app to the APIs.
- Handle validation, errors, and timeouts.
- Explain the full request flow without looking at the code.

## 8. Requirements and Scope

- Functional requirements: what the system does.
- Non-functional requirements: performance, scale, and reliability needs.
- Availability vs durability.
- Identify key user flows and explicit exclusions.
- Clarify requirements before choosing technology.

## 9. Capacity and Performance

- Latency vs throughput.
- Requests per second, peak traffic, and concurrent users.
- Daily active users vs simultaneous users.
- Rough storage and bandwidth estimates.
- Percentile latency: p50, p95, and p99.
- Estimate only what influences the design.

## 10. Scaling and Load Balancing

- Vertical scaling: a larger server.
- Horizontal scaling: more servers.
- Stateful vs stateless services.
- Sharing session state across servers.
- Load balancers, reverse proxies, and health checks.
- Identify bottlenecks and single points of failure.

## 11. Caching

- Cache hits and misses.
- Cache-aside: read the cache first, then the database on a miss.
- Time to live (TTL), eviction, and invalidation.
- Stale data and consistency trade-offs.
- Cache stampede and hot keys.

## 12. File Storage and Content Delivery

- Object storage for images, videos, and documents.
- Store file metadata in a database.
- Upload and download flows, including large-file uploads.
- Signed URLs for controlled access.
- Content delivery networks (CDNs).

## 13. Choosing a Database

- Relational vs non-relational databases.
- Key-value, document, and wide-column models: basic use cases.
- Choose based on access patterns, transactions, and scale.
- Avoid choosing a database only because it is popular.

## 14. Replication

- Leaderâ€“follower replication and read replicas.
- Synchronous vs asynchronous replication.
- Replication lag and stale reads.
- Failover when a database server fails.
- Why replication does not replace backups.

## 15. Partitioning and Sharding

- Split data across servers.
- Hash vs range partitioning.
- Choosing a shard key.
- Hotspots, uneven distribution, and rebalancing.
- Consistent hashing: basic purpose and trade-offs.

## 16. Message Queues and Event Streams

- Producers and consumers.
- Queues vs publishâ€“subscribe.
- Background jobs and asynchronous workflows.
- Event streams, consumer groups, and replay.
- Ordering within a queue or partition.

## 17. Reliable Requests and Message Processing

- Timeouts and retries with backoff and jitter.
- Idempotency: retrying without repeating the effect.
- At-most-once vs at-least-once delivery.
- Duplicate detection and dead-letter queues.
- Why exactly-once effects need carefully defined boundaries.

## 18. Distributed Consistency

- Strong vs eventual consistency.
- Read-your-writes consistency.
- Network partitions and CAP trade-offs during a partition.
- Quorums: basic read/write coordination and limitations.
- Select consistency requirements for each user flow.

## 19. Real-Time Communication

- Short polling and long polling.
- WebSockets and server-sent events (SSE).
- Choosing a communication method.
- Connection management, reconnection, and missed-message recovery.

## 20. Overload and Failure Handling

- Rate limiting: token bucket and sliding-window basics.
- Backpressure: slow producers when consumers cannot keep up.
- Circuit breakers: stop repeatedly calling a failing dependency.
- Load shedding: reject excess work to protect the system.
- Graceful degradation: preserve essential features during failures.

## 21. Service Boundaries and Data Workflows

- Monolith vs microservices.
- Synchronous vs asynchronous service communication.
- REST vs gRPC: when each fits.
- Transactional outbox: reliably connect database changes to events.
- Sagas: coordinate multi-step workflows with compensating actions.
- Learn through an order or payment example; skip framework details.

## 22. Production Essentials

- Logs, metrics, and distributed tracing.
- Service-level indicators (SLIs) and objectives (SLOs).
- Access control, encryption, and secrets management.
- Backups and recovery.
- Safe deployments, backward compatibility, and rollback.
- Compute, storage, and network cost trade-offs.

## 23. Interview Answer Structure

- Clarify requirements and scope.
- Estimate scale where it changes decisions.
- Define APIs and the data model.
- Draw a simple high-level design.
- Walk through the main request flows.
- Deep-dive into the most important bottlenecks and failure cases.
- Explain trade-offs and how the system could evolve.

## 24. Practice Designs â€” Recommended Order

- Notes application: request flow, APIs, and data modeling.
- URL shortener: identifiers, storage, caching, and scaling.
- File storage and sharing: uploads, metadata, permissions, and CDN.
- Rate limiter: algorithms, atomic updates, and distributed state.
- Notification system: queues, retries, preferences, and deduplication.
- Chat application: live connections, ordering, and offline delivery.
- Social news feed: fan-out, pagination, and popular accounts.
- Video streaming: transcoding, adaptive streaming, and content delivery.
- Search autocomplete: prefix lookup, ranking, and index updates.
- Ticket booking: concurrent reservations, expiry, and transactions.
- Payment system: idempotency, state transitions, and reconciliation.

## 25. Follow-Up Topics â€” After Core Practice

- Leader election and consensus: purpose only, not algorithm implementation.
- Distributed locks, leases, and fencing tokens.
- Multi-region design: activeâ€“passive vs activeâ€“active.
- Recovery point objective (RPO) and recovery time objective (RTO).
- Large data migrations: backfills, validation, and cutover.

## How to Proceed

1. For each topic, explain what it is, what problem it solves, how it works, and one limitation.
2. Complete the small backend at Step 7 before moving into distributed systems.
3. Start URL shortener and file-storage practice after Step 12; revisit them as you learn replication and sharding.
4. Add the remaining practice designs as you learn their required concepts.
5. Learn specialized concepts, such as video transcoding, within their practice problem.
6. Do not wait to finish all theory before practicing designs.
7. Skip consensus proofs, Kubernetes internals, service-mesh configuration, and exhaustive cloud-product comparisons initially.