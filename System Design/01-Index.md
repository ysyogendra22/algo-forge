
## Best learning order

### 1. Learn the building blocks

Study these first:

- HTTP, REST, WebSocket and DNS
- Latency, throughput and availability
- Vertical vs horizontal scaling
- Load balancers and reverse proxies
- SQL vs NoSQL databases
- Indexes, replication, partitioning and transactions
- Caching and cache invalidation
- Message queues and event-driven processing
- Object storage and CDN
- Authentication, authorization and rate limiting
- Monitoring, logging and alerting

Do not spend months here. Give this stage **2–3 weeks**.

### 2. Learn the core trade-offs

You must be able to explain:

- Consistency vs availability
- Synchronous vs asynchronous processing
- Normalisation vs denormalisation
- SQL vs NoSQL
- Strong vs eventual consistency
- Push vs pull
- Stateful vs stateless services
- Build vs buy

System design is mainly about choosing trade-offs—not drawing boxes.

### 3. Use one design framework

For every problem, follow this sequence:

1. Clarify functional requirements
2. Define non-functional requirements
3. Estimate traffic, storage and bandwidth
4. Define APIs
5. Model the data
6. Draw the high-level architecture
7. Identify bottlenecks
8. Scale individual components
9. Discuss failures, security and observability
10. Explain trade-offs

### 4. Practise in increasing difficulty

Start here:

1. URL shortener
2. Pastebin
3. Rate limiter
4. Notification service
5. File upload service
6. Chat application
7. News feed
8. Ride-booking system
9. Video-streaming platform
10. Payment system

Design **one system per week**. Explain it aloud in 30–45 minutes and record yourself.