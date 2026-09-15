# Backend Engineering Study Roadmap

For a beginner in backend engineering from a mobile development background, preparing for backend roles and FAANG interviews.

Study the numbered topics in order. Focus on building, debugging, testing, and operating APIs. Backend knowledge complements coding, low-level design, and system design preparation; it does not replace them.

## 1. Understand the Backend

- Client, server, API, and database.
- What happens when a mobile app calls an API.
- Request validation, business logic, storage, and response generation.
- Synchronous requests vs background work.

## 2. Choose One Language and Runtime

- Use one backend language initially; do not learn several stacks together.
- Reuse a language you already know when practical.
- Collections, functions, classes, interfaces, and error handling.
- Null handling, serialization, and date/time handling.
- Package management, dependencies, and build commands.
- Runtime basics: memory, garbage collection, and blocking operations.
- Review familiar programming concepts briefly rather than restarting from scratch.

## 3. Development and Command-Line Basics

- Project structure and configuration.
- Environment variables and keeping secrets out of Git.
- Terminal navigation, files, permissions, and processes.
- Git branches, commits, pull requests, and conflict resolution.
- Run, debug, and stop a server locally.
- Inspect requests using an HTTP client or curl.

## 4. Networking and HTTP

- IP addresses, domains, ports, and DNS.
- TCP and TLS: their roles in a secure connection.
- HTTP methods, headers, bodies, and status codes.
- JSON and content types.
- Cookies, connection reuse, and timeouts.
- Trace a request from client to server and back.

## 5. Build Your First API

- Learn one web framework.
- Routes, handlers/controllers, middleware, and services.
- Path parameters, query parameters, and request bodies.
- Input validation and consistent error responses.
- Centralized error handling.
- Build a health endpoint and an in-memory notes API.

## 6. Relational Databases and SQL

- Tables, rows, columns, and data types.
- Primary keys, foreign keys, and constraints.
- Create, read, update, and delete operations.
- Filtering, sorting, joins, grouping, and aggregation.
- NULL handling and parameterized queries.
- Learn SQL before relying on an object-relational mapper (ORM).

## 7. Data Modeling and Schema Migrations

- One-to-one, one-to-many, and many-to-many relationships.
- Model data around required queries and business rules.
- Normalization and deliberate denormalization.
- Unique, non-null, and foreign-key constraints.
- Schema migrations: versioned database changes.
- Timestamps, time zones, and accurate money representation.

## 8. Connect the API to a Database

- Database drivers and connection pools.
- ORM basics and the SQL it generates.
- Separate HTTP handling, business logic, and database access.
- Handle missing records and constraint violations.
- Avoid N+1 queries: repeated queries caused by loading related records individually.
- Persist the notes API and connect it to a mobile app.

## 9. API Design

- Resource naming and appropriate HTTP methods.
- Correct status codes and stable response contracts.
- Pagination: offset vs cursor.
- Filtering and sorting.
- Idempotency: repeating a request without repeating its effect.
- Backward compatibility and versioning when needed.
- API documentation using OpenAPI.

## 10. Authentication and Authorization

- Authentication: who is making the request.
- Authorization: what that identity may access.
- Password hashing with established libraries; never store plaintext passwords.
- Sessions vs access tokens.
- Expiry, logout, revocation, and refresh-token basics.
- Role-based permissions and ownership checks on individual records.
- OAuth 2.0 and OpenID Connect: roles in delegated access and sign-in.
- Use established authentication components rather than inventing cryptography.

## 11. Backend Security Essentials

- Validate input and limit request sizes.
- Prevent SQL injection using parameterized queries.
- Prevent users from accessing or modifying another user's records.
- HTTPS and secure secret handling.
- CORS: browser access rules, not authentication.
- CSRF protection when credentials are sent automatically, such as cookies.
- Server-side request forgery (SSRF): risks when fetching user-supplied URLs.
- Avoid exposing passwords, tokens, and sensitive data in logs or errors.
- Login throttling and dependency updates.

## 12. Testing and Debugging

- Unit tests for meaningful business rules.
- Integration tests for database and external-service behavior.
- API tests for validation, permissions, and error responses.
- Test isolation, fixtures, and deterministic tests.
- Mock external boundaries selectively.
- Reproduce bugs using logs, breakpoints, and failing tests.

## 13. Transactions and Concurrent Updates

- ACID: atomicity, consistency, isolation, and durability.
- Commit and rollback.
- Isolation levels and race conditions.
- Atomic updates and database constraints.
- Optimistic vs pessimistic locking.
- Deadlocks and bounded transaction retries.
- Practice preventing duplicate reservations or negative inventory.

## 14. Application Concurrency

- Processes, threads, and asynchronous tasks.
- Blocking vs non-blocking I/O.
- The concurrency model of your chosen runtime.
- Shared mutable state and thread safety.
- Bounded worker pools and connection pools.
- Cancellation, deadlines, and resource cleanup.
- Avoid blocking request workers with long-running work.

## 15. Query and API Performance

- Indexes and composite indexes.
- Read benefits vs write and storage costs.
- Query plans using EXPLAIN.
- Slow queries, N+1 queries, and excessive data fetching.
- Latency percentiles, throughput, and bottlenecks.
- Basic load testing and profiling.
- Measure before optimizing.

## 16. Caching

- In-process vs shared caches.
- Cache-aside: check the cache, then load missing data from the database.
- Cache keys, time to live (TTL), and eviction.
- Invalidation and stale-data trade-offs.
- Cache stampedes and hot keys.
- Keep authorization correct when caching user-specific data.

## 17. Background Jobs and Queues

- Producers, consumers, and workers.
- Move slow work out of API requests.
- Acknowledgments, retries, backoff, and dead-letter queues.
- At-least-once delivery and duplicate processing.
- Idempotent job handlers.
- Scheduling, ordering, and bounded concurrency.
- Practice sending a notification through a worker.

## 18. External Service Integrations

- HTTP clients, connection pooling, and timeouts.
- Retry transient failures only when the operation is safe to retry.
- Rate limits and exponential backoff with jitter.
- Webhooks: signature verification, duplicate events, and replay protection.
- Handling unavailable dependencies.
- Keep external calls outside database transactions where practical.

## 19. File Uploads and Storage

- Multipart uploads and file metadata.
- Object storage vs local server storage.
- Signed upload/download URLs.
- File size, type, and access validation.
- Large-file uploads and interrupted transfers.
- Cleanup of abandoned files and metadata.

## 20. Logging and Observability

- Structured logs and request/correlation IDs.
- Metrics: request rate, errors, latency, and resource usage.
- Distributed tracing when requests cross services.
- Health and readiness checks.
- Actionable alerts.
- Diagnose an incident from symptoms to root cause.

## 21. Packaging and Deployment

- Build a deployable application artifact.
- Container basics: image, container, ports, and volumes.
- Environment-specific configuration and secrets.
- Continuous integration (CI): build, checks, and tests.
- Continuous delivery/deployment (CD): release workflow.
- Deploy to one environment and verify it works.
- Graceful shutdown, schema migration safety, and rollback.

## 22. Reliability and Scaling

- Stateless services and horizontal scaling.
- Load balancing and shared session storage.
- Database connection limits as server counts grow.
- Rate limiting and backpressure.
- Circuit breakers and graceful degradation.
- Database backups and tested restoration.
- Replication and sharding: basic concepts; study their design trade-offs in the system design roadmap.

## 23. Code Structure and Low-Level Design

- Clear responsibilities and small, cohesive modules.
- Dependency injection and explicit dependencies.
- Composition, interfaces, and testable business logic.
- Model business rules and valid state transitions.
- Use design patterns only when they solve a concrete problem.
- Keep one application modular before splitting it into microservices.

## 24. Backend Interview Preparation

- Explain an API request from network entry to database response.
- Design an API and schema from a short requirement.
- Write SQL with joins and aggregation; explain index choices.
- Debug a slow endpoint, failed job, or concurrency bug.
- Explain authentication, authorization, transactions, and idempotency.
- Discuss testing, deployment, monitoring, and a production failure scenario.
- Continue data structures and algorithms separately.
- Practice low-level design and system design according to the role.

## 25. Practice Projects â€” In Order

- Notes API: CRUD, SQL, migrations, validation, and pagination.
- Extend the notes API: authentication, ownership checks, tests, and deployment.
- Notification workflow: queue, worker, retries, and duplicate prevention.
- Inventory/reservation API: transactions, concurrent requests, expiry, and idempotency.
- Add an external sandbox integration: verified webhooks, retries, and state transitions.

## 26. Optional Topics â€” After the Core

- WebSockets and server-sent events for real-time features.
- NoSQL databases when a concrete access pattern calls for them.
- gRPC for typed service-to-service communication.
- Event streams and consumer groups.
- Transactional outbox and sagas for cross-service workflows.
- Search indexes for full-text search.

## How to Proceed

- Use one language, one framework, and one relational database initially.
- Build the first API at Step 5; add persistence at Step 8.
- Extend the same project with authentication, tests, and transactions as you learn.
- Complete a basic deployment once you have a working, tested API; deepen deployment knowledge at Step 21.
- For each topic, explain its purpose, implement a small example, and check a failure case.
- Prefer a few complete projects over many unfinished tutorials.
- Skip Kubernetes internals, service meshes, event sourcing, custom authentication protocols, and multiple cloud certifications initially.