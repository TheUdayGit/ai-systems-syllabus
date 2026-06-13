## File: typescript-nodejs-backend-syllabus.md

# TypeScript & Node.js Backend Engineering

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Distributed Systems & Backend Engineering (or equivalent), strong JavaScript/ES6+ fundamentals, basic understanding of event-driven programming, familiarity with HTTP protocols and REST design  
**Estimated Duration:** 220–280 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: TypeScript Foundations — Beyond Type Annotations](#module-0-typescript-foundations--beyond-type-annotations)
4. [Module 1: Advanced TypeScript — The Type System as a Proof Engine](#module-1-advanced-typescript--the-type-system-as-a-proof-engine)
5. [Module 2: Node.js Runtime Internals & V8 Deep Dive](#module-2-nodejs-runtime-internals--v8-deep-dive)
6. [Module 3: Event-Driven Architecture & Async Patterns](#module-3-event-driven-architecture--async-patterns)
7. [Module 4: HTTP, gRPC, and Service Communication](#module-4-http-grpc-and-service-communication)
8. [Module 5: Database Engineering — SQL, NoSQL, and Beyond](#module-5-database-engineering--sql-nosql-and-beyond)
9. [Module 6: Caching, Rate Limiting, and Edge Optimization](#module-6-caching-rate-limiting-and-edge-optimization)
10. [Module 7: Microservices, Service Mesh, and Distributed Node.js](#module-7-microservices-service-mesh-and-distributed-nodejs)
11. [Module 8: Real-Time Systems — WebSockets, SSE, and Streaming](#module-8-real-time-systems--websockets-sse-and-streaming)
12. [Module 9: Testing, Observability, and Production Readiness](#module-9-testing-observability-and-production-readiness)
13. [Module 10: ML/AI Integration — Model Serving, RAG, and LLM Pipelines](#module-10-mlai-integration--model-serving-rag-and-llm-pipelines)
14. [Module 11: Performance Engineering & Systems Programming in Node.js](#module-11-performance-engineering--systems-programming-in-nodejs)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **TypeScript** and **Node.js** not as a web development stack, but as a **high-performance systems platform** for building production AI infrastructure. The pedagogical approach follows a **Types → Runtime → Architecture → Scale → Resilience** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Types** | Structural typing, type-level programming, compile-time contracts | Zero-runtime-overhead safety |
| **Runtime** | V8 internals, event loop, memory management, C++ addons | Deep performance understanding |
| **Architecture** | Hexagonal/clean architecture, DDD, API design, protocol semantics | Maintainable, testable systems |
| **Scale** | Clustering, worker threads, horizontal scaling, load balancing | Production-grade throughput |
| **Resilience** | Circuit breakers, graceful degradation, chaos engineering | Antifragile services |

**Core Principles:**
- **The type system is a design tool, not just a linter.** We use TypeScript's type system to encode domain invariants, API contracts, and state machines at compile time — eliminating entire classes of runtime failures.
- **Node.js is a systems runtime, not just a web server.** We study libuv, V8, and the C++ layer to understand why `fs.readFile` blocks the event loop, why `cluster.fork()` shares nothing, and why NAPI addons matter for ML inference.
- **Every abstraction must be traceable to mechanism.** We do not teach "use Express" — we teach *why* middleware is a continuation-passing pattern, *why* Fastify's schema compilation beats runtime validation, *why* NestJS's module system mirrors Angular's DI container.
- **ML infrastructure is backend infrastructure.** Model serving, feature stores, RAG pipelines, and LLM orchestration are backend engineering problems with AI-shaped payloads. We build them with the same rigor as payment systems.
- **Observability is a first-class system output.** Distributed tracing, structured logs, and metrics are not " DevOps" — they are engineering requirements that shape API design and data flow.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### TypeScript Language Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Basic types, interfaces, generics, type inference | Type-safe CRUD APIs |
| **Intermediate** | Conditional types, mapped types, template literal types, type guards | Domain modeling, API SDK generation |
| **Advanced** | Type-level programming, recursive types, branded types, phantom types | Compile-time state machines, zero-cost abstractions |
| **Expert** | Custom type system extensions, compiler API, AST transformation | Code generation, lint rules, DSL design |

### Node.js Runtime Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Event loop basics, streams, buffers, basic clustering | Simple HTTP services |
| **Intermediate** | Worker threads, C++ addons, memory profiling, libuv internals | CPU-intensive workloads, native integration |
| **Advanced** | Custom V8 isolates, NAPI lifecycle management, shared memory | High-performance inference, real-time systems |
| **Expert** | V8 engine modification, custom event loops, kernel bypass | Runtime engineering, custom platforms |

### Backend Engineering Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Express/Fastify basics, REST APIs, basic ORM, JWT auth | Simple web services |
| **Intermediate** | GraphQL federation, gRPC, message queues, caching layers | High-throughput APIs |
| **Advanced** | Custom protocols, zero-copy streaming, backpressure design, circuit breakers | Low-latency trading, search, streaming |
| **Expert** | Platform design, multi-tenant architecture, custom load balancers | Hyperscale infrastructure |

### ML/AI Integration Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | ONNX Runtime Node.js, basic model serving, OpenAI API integration | Simple inference endpoints |
| **Intermediate** | TensorFlow.js, custom ML pipelines, feature caching, batch inference | Production model serving |
| **Advanced** | LLM streaming, RAG architecture, vector DB integration, agent orchestration | LLM platforms, RAG systems |
| **Expert** | Custom inference runtimes, model compilation, distributed serving | AI supercomputing edge |

### Cross-Cutting Competencies
- **Systems:** Design services handling >50K RPS with <10ms P99 latency
- **Formal reasoning:** Use types to prove API correctness and state validity
- **Operational thinking:** Debug memory leaks, event loop starvation, GC pauses in production
- **Economic reasoning:** Cost-per-request analysis, cold start optimization, serverless economics

---

## Module 0: TypeScript Foundations — Beyond Type Annotations

**Duration:** 20 hours  
**Purpose:** Establish deep TypeScript fluency; eliminate "I know TypeScript" false confidence from JavaScript developers

### 0.1 The TypeScript Compiler Architecture
- **Compilation pipeline:** Scanner → Parser → Binder → Checker → Emitter
- **Program structure:** `ts.Program`, `ts.SourceFile`, AST nodes, symbol table
- **Type checking phases:** Control flow analysis, type inference, structural typing
- **`tsconfig.json` deep dive:** `strict` mode flags, `target`, `module`, `moduleResolution`, `paths`, `baseUrl`, `outDir`, `declaration`
- **Production connection:** Why `strictNullChecks` eliminates billion-dollar bugs; why `isolatedModules` matters for Babel transpilation; declaration file generation for library authors

### 0.2 Structural Typing vs. Nominal Typing
- **Structural equivalence:** Duck typing formalized, width subtyping, excess property checks
- **Nominal emulation:** Branded types, phantom types, `unique symbol` tags
- **Discriminated unions:** Tagged unions, exhaustive checking, `never` exhaustiveness
- **Production connection:** Why TypeScript's structural typing enables seamless API evolution; branded types for user IDs vs. product IDs (preventing accidental mixing); discriminated unions for Redux actions and state machines

### 0.3 Generics and Type Parameters
- **Generic constraints:** `extends`, `keyof`, `typeof`, conditional constraints
- **Variance:** Covariance, contravariance, bivariance, invariance — `strictFunctionTypes`
- **Generic defaults and inference:** Default type parameters, contextual typing, inference priorities
- **Production connection:** Generic repository patterns; covariant return types for API responses; contravariant callbacks for event handlers

### 0.4 Type Narrowing and Control Flow
- **Type guards:** `typeof`, `instanceof`, `in`, custom type predicates (`is`), assertion functions (`asserts`)
- **Control flow analysis:** Assignment narrowing, switch narrowing, loop narrowing, try-catch narrowing
- **Nullable types:** `null`, `undefined`, `nullish coalescing` (`??`), optional chaining (`?.`), non-null assertion (`!`)
- **Production connection:** Eliminating null pointer exceptions; type-safe error handling; exhaustive switch statements for state machines

### 0.5 Utility Types and Type Manipulation
- **Built-in utilities:** `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`, `Exclude`, `Extract`, `ReturnType`, `Parameters`, `Awaited`
- **Custom utilities:** Deep partial, deep readonly, flatten, tuple manipulation
- **Template literal types:** String literal manipulation, pattern matching, route parameter extraction
- **Production connection:** API response transformation types; deep immutable state for Redux; URL parameter extraction for type-safe routing

### 0.6 Lab: Building a Type-Safe API SDK Generator
- **Task:** Build a tool that generates TypeScript SDKs from OpenAPI specs
- **Requirements:**
  - Parse OpenAPI 3.0/3.1 schemas
  - Generate discriminated unions for oneOf/anyOf
  - Generate branded types for entity IDs
  - Generate exhaustive switch handlers for enums
  - Validate that generated types are assignable to original schemas
- **Deliverable:** CLI tool with tests, example SDKs, documentation

---

## Module 1: Advanced TypeScript — The Type System as a Proof Engine

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 1.1 Conditional Types and Type-Level Programming
- **Conditional types:** `T extends U ? X : Y`, distributive conditional types, `infer`
- **Recursive types:** Recursive conditional types, type-level fixed points, depth limits
- **Type-level arithmetic:** Peano arithmetic, tuple length manipulation, numeric ranges
- **Production connection:** Type-safe SQL query builders (Prisma, Kysely); type-level routing; compile-time configuration validation

### 1.2 Mapped Types and Key Remapping
- **Mapped types:** `[K in keyof T]`, modifiers (`readonly`, `?`), `as` clauses (key remapping)
- **Filtering keys:** `PickByValue`, `OmitByValue`, conditional key inclusion
- **Production connection:** Type-safe database schema migrations; API version type transformations; feature flag type systems

### 1.3 The `never` Type and Bottom Types
- **`never` as the bottom type:** Uninhabitable, assignability rules, exhaustiveness checking
- **Using `never` for totality:** Compile-time proof that all cases are handled
- **Production connection:** State machine totality proofs; ensuring all error cases are handled; type-safe reducers

### 1.4 Higher-Kinded Types and Type Classes (Emulation)
- **The HKT problem:** Why TypeScript doesn't have native HKTs, workarounds
- **Type class emulation:** `Functor`, `Monad`, `Applicative` patterns via interfaces and conditional types
- **fp-ts and io-ts:** Functional programming primitives, runtime type validation
- **Production connection:** Railway-oriented programming for error handling; io-ts for API boundary validation; functional composition for data pipelines

### 1.5 Decorators, Metadata, and Reflection
- **Decorators proposal:** Stage 3 TC39, legacy vs. modern, parameter decorators, method decorators, class decorators
- **`reflect-metadata`:** Design-time type information, dependency injection metadata
- **Production connection:** NestJS DI container implementation; ORM entity decorators (TypeORM, MikroORM); API documentation generation from decorators

### 1.6 Compiler API and AST Manipulation
- **TypeScript compiler API:** `ts.createProgram`, `ts.forEachChild`, `ts.TransformerFactory`
- **Code generation:** Templating, AST transformation, custom emit
- **Lint rule development:** TSLint (deprecated) vs. ESLint with TypeScript parser
- **Production connection:** Custom code generation for GraphQL schemas; lint rules for API contract enforcement; AST-based refactoring tools

### 1.7 Lab: Building a Compile-Time State Machine
- **Task:** Implement a type-safe state machine where invalid transitions are compile-time errors
- **Requirements:**
  - States and events as literal types
  - Transition table as a mapped type
  - Current state tracked at the type level
  - Invalid transitions produce `never` or compile errors
  - Runtime implementation mirrors type-level logic
- **Deliverable:** Library with examples, tests proving compile-time rejection of invalid transitions

---

## Module 2: Node.js Runtime Internals & V8 Deep Dive

**Duration:** 30 hours  
**Level:** Intermediate → Advanced

### 2.1 V8 Architecture and JavaScript Execution
- **V8 pipeline:** Parser → Ignition (bytecode) → Sparkplug (baseline) → Maglev (mid-tier) → TurboFan (optimizing)
- **Hidden classes and inline caching:** Object shape tracking, monomorphic vs. polymorphic vs. megamorphic property access
- **Heap structure:** New space (semi-space), old space (mark-sweep-compact), large object space, code space, map space
- **Garbage collection:** Scavenge (minor GC), Mark-Compact (major GC), Orinoco (concurrent marking), Oilpan (cppgc)
- **Production connection:** Why hidden class stability matters (avoid deleting properties); why megamorphic access kills performance; GC tuning for low-latency services

### 2.2 The Event Loop and libuv
- **libuv architecture:** Event loop phases (timers, I/O callbacks, idle/prepare, poll, check, close callbacks), thread pool
- **Event loop starvation:** CPU-intensive tasks blocking I/O, `setImmediate` vs. `setTimeout` vs. `process.nextTick`
- **Microtasks:** Promise resolution queue, `queueMicrotask`, `async`/`await` microtask scheduling
- **Production connection:** Why `process.nextTick` can starve I/O; why `setImmediate` yields to I/O; event loop latency monitoring

### 2.3 Streams and Backpressure
- **Stream types:** Readable, Writable, Duplex, Transform
- **Backpressure mechanisms:** `readable.pause()`, `writable.write()` return value, `drain` event, `pipe()` internal backpressure
- **Object mode vs. buffer mode:** Use cases, performance implications
- **Production connection:** Streaming JSON parsing for large payloads; backpressure in Kafka consumers; preventing memory exhaustion in upload pipelines

### 2.4 Buffers, TypedArrays, and Binary Data
- **Buffer internals:** `Buffer` as `Uint8Array` subclass, pool allocation (`Buffer.poolSize`), zero-fill
- **TypedArrays and DataView:** Endianness, alignment, shared memory (`SharedArrayBuffer`)
- **Binary protocols:** Protocol Buffers, MessagePack, BSON — parsing and serialization
- **Production connection:** Zero-copy buffer slicing for packet processing; shared memory for worker thread communication; binary serialization for high-throughput APIs

### 2.5 Clustering and Process Management
- **`cluster` module:** Master-worker architecture, `fork()`, IPC, shared ports, sticky sessions
- **PM2:** Process manager, clustering, zero-downtime reload, log aggregation
- **Process lifecycle:** `SIGTERM`, `SIGINT`, graceful shutdown, `uncaughtException`, `unhandledRejection`
- **Production connection:** Horizontal scaling on single machine; graceful shutdown for in-flight requests; process crash recovery

### 2.6 Worker Threads and Shared Memory
- **`worker_threads`:** `Worker`, `MessageChannel`, `MessagePort`, `Atomics`, `SharedArrayBuffer`
- **Structured clone algorithm:** What can be transferred vs. cloned
- **Thread pool patterns:** `generic-pool`, `piscina`, worker thread pools for CPU-intensive work
- **Production connection:** Offloading image processing to worker threads; shared memory for concurrent data structures; thread pools for ML preprocessing

### 2.7 Lab: Building a Custom Thread Pool Scheduler
- **Task:** Implement a work-stealing thread pool for CPU-intensive tasks
- **Requirements:**
  - Task queue with priority support
  - Work-stealing between worker threads
  - SharedArrayBuffer for result aggregation
  - Atomics for lock-free synchronization
  - Graceful shutdown with in-flight task completion
  - Benchmark against `piscina` and native `cluster`
- **Deliverable:** Working implementation, performance analysis, memory profiling under load

---

## Module 3: Event-Driven Architecture & Async Patterns

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 3.1 Callbacks, Promises, and Async/Await
- **Callback pattern:** Error-first callbacks, callback hell, continuation-passing style
- **Promises:** `Promise` state machine, `then`, `catch`, `finally`, `Promise.all`, `Promise.race`, `Promise.allSettled`, `Promise.any`
- **Async/await:** Desugaring to generators, `async` function return type, `await` microtask scheduling
- **Production connection:** Promise anti-patterns (floating promises, `await` in loops); `Promise.all` for parallel I/O; `Promise.race` for timeouts

### 3.2 Generators and Async Generators
- **Generator functions:** `function*`, `yield`, `next()`, `return()`, `throw()`
- **Async generators:** `async function*`, `for await...of`, backpressure in async iteration
- **Producer-consumer patterns:** Bounded queues, backpressure via `await` in generators
- **Production connection:** Streaming database query results; paginated API consumption with backpressure; async iterables for Kafka consumers

### 3.3 Event Emitters and Pub/Sub
- **`EventEmitter`:** `on`, `once`, `emit`, `removeListener`, memory leak detection (`maxListeners`)
- **Typed events:** Strictly typed event emitters, event maps, discriminated events
- **Pub/Sub patterns:** In-memory, Redis Pub/Sub, Redis Streams, NATS
- **Production connection:** Type-safe event buses; Redis Streams for reliable event delivery; event-driven microservices

### 3.4 Reactive Programming with RxJS
- **Observables and observers:** `Observable`, `Observer`, `Subscription`, cold vs. hot observables
- **Operators:** `map`, `filter`, `mergeMap`, `switchMap`, `concatMap`, `debounceTime`, `throttleTime`, `buffer`, `window`
- **Backpressure strategies:** Buffer, drop, throttle, debounce, sample
- **Production connection:** Real-time data pipelines; API rate limiting with RxJS; complex event processing for monitoring

### 3.5 Structured Concurrency and Abort Signals
- **`AbortController` and `AbortSignal`:** Cancellation propagation, fetch abortion, stream cancellation
- **Structured concurrency:** `Promise` trees, cancellation scopes, resource cleanup
- **Production connection:** Request cancellation in long-polling; graceful shutdown with abort signals; preventing resource leaks in async operations

### 3.6 Lab: Building a Reactive Event Processing Pipeline
- **Task:** Build a real-time event processing system with backpressure
- **Requirements:**
  - Kafka consumer with async generator pattern
  - RxJS pipeline for filtering, aggregation, windowing
  - Backpressure handling (drop vs. buffer vs. throttle)
  - Abort signal propagation for graceful shutdown
  - Exactly-once processing semantics
  - Benchmark: 100K events/sec with <100ms processing latency
- **Deliverable:** Working pipeline, backpressure behavior analysis, failure mode testing

---

## Module 4: HTTP, gRPC, and Service Communication

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 4.1 HTTP/1.1, HTTP/2, and HTTP/3
- **HTTP/1.1:** Pipelining, head-of-line blocking, keep-alive, chunked transfer encoding
- **HTTP/2:** Binary framing, multiplexed streams, flow control, HPACK header compression, server push (deprecated)
- **HTTP/3:** QUIC transport, connection migration, 0-RTT, independent stream loss recovery
- **Production connection:** Why HTTP/2 matters for gRPC; why HTTP/3 matters for mobile; keep-alive tuning for connection pools

### 4.2 REST API Design and HATEOAS
- **Resource modeling:** Nouns not verbs, nested resources, collection patterns
- **HTTP semantics:** Methods (GET, POST, PUT, PATCH, DELETE), idempotency, safety
- **Status codes:** Correct usage, error representation (RFC 7807 Problem Details)
- **HATEOAS:** Hypermedia as the Engine of Application State, link relations, HAL, JSON:API
- **Versioning strategies:** URL, header, media type, deprecation policies
- **Production connection:** Idempotent payment APIs; RFC 7807 for consistent error handling; API versioning for backward compatibility

### 4.3 Fastify and High-Performance HTTP
- **Fastify architecture:** Plugin system, encapsulation, hook lifecycle, schema-based validation (AJV compilation)
- **Route registration:** Prefixes, constraints, async handlers, error handlers
- **Validation and serialization:** JSON Schema compilation, response serialization, type provider integration
- **Production connection:** Why Fastify outperforms Express (schema compilation, minimal overhead); plugin architecture for modular services; AJV for zero-cost validation

### 4.4 gRPC and Protocol Buffers
- **Protocol Buffers:** Schema definition, binary encoding, field numbers, backward compatibility
- **gRPC over HTTP/2:** Unary, server streaming, client streaming, bidirectional streaming
- **Deadlines and cancellation:** Context propagation, timeout chains
- **Load balancing:** Client-side vs. server-side, health checking, retry policies
- **Production connection:** Internal microservices communication; streaming inference results; deadline propagation for cascading timeouts

### 4.5 GraphQL and Federation
- **GraphQL schema:** Types, queries, mutations, subscriptions, introspection
- **Resolver pattern:** N+1 problem, DataLoader batching and caching
- **Federation:** Subgraphs, gateway, entity resolution, query planning, `@key` directives
- **Production connection:** Apollo Federation for microservices APIs; DataLoader for database query optimization; GraphQL for flexible client queries

### 4.6 Webhooks and Async Callbacks
- **Webhook design:** Idempotency, signature verification (HMAC), retry with exponential backoff
- **Circuit breakers:** Failure detection, half-open state, recovery
- **Production connection:** Stripe-style webhook handling; GitHub webhook integration; reliable callback delivery

### 4.7 Lab: Building a High-Performance API Gateway
- **Task:** Build an API gateway supporting REST, gRPC, and GraphQL
- **Requirements:**
  - Fastify-based HTTP proxy with request/response transformation
  - gRPC transcoding to REST (Envoy-style)
  - GraphQL federation gateway
  - JWT authentication with RBAC
  - Rate limiting (token bucket, distributed)
  - Request/response logging with correlation IDs
  - Circuit breaker per upstream service
  - Benchmark: 50K RPS, <5ms P99 latency
- **Deliverable:** Working gateway, architecture document, load testing results, security audit

---

## Module 5: Database Engineering — SQL, NoSQL, and Beyond

**Duration:** 30 hours  
**Level:** Advanced

### 5.1 PostgreSQL Deeply
- **Architecture:** Process-per-connection, shared buffers, WAL, checkpointing, vacuum
- **Indexing:** B-tree, hash, GiST, GIN, BRIN, partial indexes, expression indexes, covering indexes
- **Query planning:** EXPLAIN ANALYZE, cost model, join strategies (nested loop, hash join, merge join), statistics
- **Concurrency control:** MVCC, isolation levels, row-level locking, advisory locks, `FOR UPDATE`/`FOR SHARE`
- **Advanced features:** JSONB, full-text search, window functions, CTEs (recursive), partitioning, logical replication
- **Production connection:** JSONB for flexible schemas; GIN indexes for array/JSONB search; partitioning for time-series; logical replication for read replicas

### 5.2 Connection Pooling and Query Builders
- **PgBouncer:** Transaction pool vs. session pool vs. statement pool
- **Node.js drivers:** `pg`, `postgres.js`, `slonik` — prepared statements, parameterization, type parsers
- **Query builders:** Knex.js, Kysely, Zapatos — type-safe SQL generation
- **ORMs:** Prisma, TypeORM, Drizzle — schema definition, migrations, relation handling
- **Production connection:** Connection pool sizing (Little's Law); prepared statement caching; type-safe query builders preventing SQL injection; ORM N+1 problem and solutions

### 5.3 Redis and In-Memory Data Structures
- **Data structures:** Strings, lists, sets, sorted sets, hashes, bitmaps, hyperloglogs, streams, geospatial
- **Persistence:** RDB snapshots, AOF, hybrid, fsync policies
- **Replication:** Master-replica, sentinel, cluster mode, replica reads
- **Redis Streams:** Consumer groups, pending entries, claim mechanism, stream trimming
- **RedisJSON, RediSearch, RedisGraph:** Module ecosystem
- **Production connection:** Caching with TTL and eviction policies; Redis Streams for event sourcing; sorted sets for leaderboards; geospatial for location services

### 5.4 MongoDB and Document Databases
- **Document model:** BSON, schema design (embedding vs. referencing), array operations
- **Indexing:** Single field, compound, multikey, text, geospatial, wildcard, clustered indexes
- **Aggregation pipeline:** Match, group, project, lookup, unwind, facet
- **Replication:** Replica sets, elections, read preferences, write concerns
- **Sharding:** Shard keys, chunks, balancer, zone sharding
- **Production connection:** Schema flexibility for rapid iteration; compound indexes for query patterns; aggregation for analytics; sharding for horizontal scaling

### 5.5 Vector Databases
- **Vector indexing:** Flat, IVF, HNSW, PQ (Product Quantization), SCaNN
- **Approximate nearest neighbor (ANN):** Recall vs. latency trade-offs, index build time
- **Vector DBs:** Pinecone, Weaviate, Milvus, pgvector, RedisVector
- **Hybrid search:** Dense + sparse vectors, reranking, metadata filtering
- **Production connection:** RAG document retrieval; image search; recommendation embeddings; hybrid search for accuracy

### 5.6 Lab: Building a Multi-Model Data Platform
- **Task:** Build a system using PostgreSQL + Redis + Vector DB
- **Requirements:**
  - PostgreSQL for transactional data with JSONB flexibility
  - Redis for caching and real-time leaderboards
  - pgvector or Pinecone for semantic search
  - Consistency between systems (cache invalidation, eventual consistency)
  - Type-safe database layer with Prisma or Kysely
  - Migration strategy with rollback capability
  - Benchmark: 10K writes/sec, 100K reads/sec, <10ms cache hit latency
- **Deliverable:** Working system, schema design document, consistency analysis, performance report

---

## Module 6: Caching, Rate Limiting, and Edge Optimization

**Duration:** 20 hours  
**Level:** Advanced

### 6.1 Caching Strategies and Patterns
- **Cache layers:** Browser, CDN, edge, application, database, distributed
- **Cache patterns:** Cache-aside, write-through, write-behind, read-through, refresh-ahead
- **Cache invalidation:** TTL, explicit invalidation, event-driven invalidation, cache warming
- **Cache eviction:** LRU, LFU, FIFO, random, custom policies
- **Production connection:** CDN for static assets and API responses; Redis for application caching; cache stampede prevention (probabilistic early expiration)

### 6.2 Distributed Caching
- **Redis Cluster:** Slot allocation, resharding, failover, cross-slot operations
- **Consistent hashing:** Ring hash, jump consistent hash, rendezvous hashing
- **Cache coherence:** Invalidation protocols, lease-based caching, stampedes
- **Production connection:** Redis Cluster for session storage; consistent hashing for cache sharding; lease-based caching for thundering herd prevention

### 6.3 Rate Limiting and Throttling
- **Algorithms:** Token bucket, leaky bucket, fixed window, sliding window log, sliding window counter, GCRA
- **Distributed rate limiting:** Redis cell, shared state, coordination overhead
- **Client-side rate limiting:** Exponential backoff, jitter, circuit breakers
- **Production connection:** API gateway rate limiting; user-level vs. IP-level throttling; adaptive rate limiting based on load

### 6.4 Edge Computing and CDN
- **Edge functions:** Cloudflare Workers, Vercel Edge Functions, Lambda@Edge
- **Edge caching:** Cache-Control, ETags, stale-while-revalidate, surrogate keys
- **Geographic routing:** Anycast, GeoDNS, latency-based routing
- **Production connection:** Edge inference for low latency; A/B testing at the edge; geographic data residency

### 6.5 Lab: Building a Smart Caching Layer
- **Task:** Build a caching middleware with intelligent invalidation
- **Requirements:**
  - Redis-backed cache with consistent hashing
  - Cache-aside with write-through option
  - Event-driven invalidation via Redis Pub/Sub
  - Probabilistic early expiration (preventing stampede)
  - Metrics: hit rate, miss rate, eviction rate, latency
  - Benchmark: 95% hit rate, <1ms hit latency, stampede resistance
- **Deliverable:** Working middleware, performance benchmarks, failure mode analysis

---

## Module 7: Microservices, Service Mesh, and Distributed Node.js

**Duration:** 30 hours  
**Level:** Advanced → Expert

### 7.1 NestJS Architecture and Dependency Injection
- **Module system:** `@Module`, providers, controllers, exports, dynamic modules
- **Dependency injection:** Constructor injection, custom providers (value, factory, existing), injection scopes (DEFAULT, REQUEST, TRANSIENT)
- **Lifecycle hooks:** `OnModuleInit`, `OnApplicationBootstrap`, `OnModuleDestroy`, `BeforeApplicationShutdown`
- **Interceptors, guards, pipes, filters:** Cross-cutting concerns, AOP in Node.js
- **Production connection:** NestJS for enterprise Node.js; DI for testability; interceptors for logging and metrics; guards for authorization

### 7.2 Service Communication Patterns
- **Synchronous:** REST, gRPC — request/response, timeout handling
- **Asynchronous:** Message queues, event buses, CQRS, saga pattern
- **Choreography vs. orchestration:** Event-driven coordination, process managers
- **Outbox pattern:** Reliably publishing events from transactions
- **Production connection:** gRPC for internal sync calls; Kafka/NATS for async events; outbox pattern for transactional event publishing; saga for distributed transactions

### 7.3 Service Mesh with Istio/Linkerd
- **Sidecar proxy:** Envoy, transparent interception, iptables/nftables redirection
- **Traffic management:** Canary, blue-green, A/B testing, traffic mirroring, fault injection
- **Security:** mTLS automatic, certificate rotation, identity-based policies
- **Observability:** Automatic metrics, tracing, logging without code changes
- **Production connection:** Istio for Kubernetes microservices; automatic mTLS for zero-trust; canary deployments for safe model rollouts

### 7.4 Distributed Tracing and Context Propagation
- **OpenTelemetry:** Traces, spans, context, baggage, instrumentation
- **Context propagation:** W3C Trace Context, B3, Jaeger format, carrier injection
- **Sampling:** Head-based, tail-based, adaptive, probabilistic
- **Production connection:** Tracing requests across microservices; identifying latency bottlenecks; tail-based sampling for error analysis

### 7.5 Kubernetes for Node.js
- **Containerization:** Multi-stage Docker builds, distroless images, non-root execution
- **Deployment strategies:** Rolling update, blue-green, canary, Helm charts
- **Resource management:** Requests/limits, HPA, VPA, cluster autoscaling
- **Probes:** Liveness, readiness, startup probes
- **Production connection:** Distroless Node.js images for security; HPA based on custom metrics (request queue depth); graceful shutdown with preStop hooks

### 7.6 Lab: Building a Distributed E-Commerce Platform
- **Task:** Build a microservices system with 5+ services
- **Requirements:**
  - NestJS services: user, product, order, payment, notification
  - gRPC for internal sync communication
  - Kafka for async events (order placed, payment processed)
  - Saga pattern for order→payment→inventory
  - Outbox pattern for reliable event publishing
  - Istio service mesh with mTLS
  - Distributed tracing with OpenTelemetry
  - Kubernetes deployment with Helm
- **Deliverable:** Working system, architecture diagram, chaos engineering tests, performance benchmarks

---

## Module 8: Real-Time Systems — WebSockets, SSE, and Streaming

**Duration:** 20 hours  
**Level:** Advanced

### 8.1 WebSocket Protocol and Implementation
- **Protocol handshake:** HTTP upgrade, framing, opcodes, masking, ping/pong, close
- **WS libraries:** `ws`, `Socket.IO`, `µWebSockets` (C++ binding performance)
- **Scaling WebSockets:** Sticky sessions, Redis adapter, pub/sub for broadcast
- **Backpressure in WS:** `bufferedAmount`, flow control, slow consumer handling
- **Production connection:** Real-time dashboards; collaborative editing; live sports updates; scaling to millions of concurrent connections

### 8.2 Server-Sent Events (SSE)
- **SSE protocol:** `text/event-stream`, `id`, `event`, `data`, `retry`, automatic reconnection
- **SSE vs. WebSockets:** Unidirectional vs. bidirectional, HTTP compatibility, simpler scaling
- **Implementation patterns:** Event stream from database (logical replication), cache invalidation streams
- **Production connection:** Live notifications; stock price streams; log tailing; simpler than WS for server→client push

### 8.3 Streaming Protocols
- **HTTP streaming:** Chunked transfer encoding, infinite response bodies
- **gRPC streaming:** Server streaming, client streaming, bidirectional
- **WebRTC:** P2P data channels, signaling servers, ICE, STUN, TURN
- **Production connection:** Streaming LLM token generation; real-time video processing; low-latency data sync

### 8.4 Real-Time Data Synchronization
- **Operational Transform (OT):** Concurrent editing, transformation functions
- **CRDTs (Conflict-free Replicated Data Types):** State-based, operation-based, merge semantics
- **Local-first software:** SQLite on client, sync with server, conflict resolution
- **Production connection:** Figma's multiplayer (OT); Notion's sync (CRDTs); local-first apps for offline capability

### 8.5 Lab: Building a Real-Time Collaborative Editor
- **Task:** Build a Google Docs-like collaborative text editor
- **Requirements:**
  - WebSocket or SSE for real-time sync
  - CRDT implementation (Yjs-style or custom)
  - Presence awareness (cursor positions, user list)
  - Offline support with local storage sync
  - Conflict resolution without server coordination
  - Scale: 100 concurrent editors per document
- **Deliverable:** Working editor, CRDT correctness tests, performance under concurrent edits

---

## Module 9: Testing, Observability, and Production Readiness

**Duration:** 25 hours  
**Level:** Advanced

### 9.1 Testing Strategies for Node.js
- **Unit testing:** Jest, Vitest, Mocha — mocks, spies, stubs, fakes
- **Integration testing:** Testcontainers, Docker Compose, database setup/teardown
- **E2E testing:** Playwright, Cypress, Supertest — realistic user flows
- **Contract testing:** Pact, consumer-driven contracts
- **Property-based testing:** fast-check, Hypothesis-style generation
- **Production connection:** Testcontainers for integration tests; Pact for microservice contract verification; property-based testing for parsers

### 9.2 Performance Testing
- **Load testing:** Artillery, k6, Locust — throughput, latency, error rate
- **Stress testing:** Finding breaking points, graceful degradation
- **Soak testing:** Memory leaks, resource exhaustion over time
- **Chaos testing:** Gremlin, Chaos Monkey — random failure injection
- **Production connection:** Load testing before production deploys; soak testing for memory leak detection; chaos testing for resilience validation

### 9.3 Observability Stack
- **Metrics:** Prometheus client, custom metrics, cardinality control
- **Logging:** Pino, Winston, structured JSON, correlation IDs, log levels
- **Tracing:** OpenTelemetry auto-instrumentation, manual span creation, baggage
- **Alerting:** Prometheus Alertmanager, PagerDuty, SLO-based alerting
- **Dashboards:** Grafana, custom dashboards, RED/USE methods
- **Production connection:** Pino for high-performance logging; OpenTelemetry for vendor-neutral instrumentation; SLO-based alerting for error budgets

### 9.4 Error Handling and Resilience Patterns
- **Circuit breaker:** State machine (closed, open, half-open), failure threshold, recovery
- **Retry with backoff:** Exponential backoff, jitter, maximum attempts
- **Bulkhead:** Resource isolation, thread pool separation
- **Timeout and deadline propagation:** Context deadlines, cascading cancellation
- **Fallback and degradation:** Graceful degradation, static fallbacks, cached responses
- **Production connection:** Circuit breaker for external API calls; retry with jitter for transient failures; bulkhead for critical path isolation

### 9.5 Lab: Building a Resilient Payment Processing System
- **Task:** Build a payment system with full resilience patterns
- **Requirements:**
  - Idempotent payment processing (idempotency keys)
  - Circuit breaker for payment gateway integration
  - Retry with exponential backoff and jitter
  - Outbox pattern for event publishing
  - Saga pattern for distributed transaction (payment→inventory→shipping)
  - Comprehensive observability (metrics, traces, structured logs)
  - Chaos testing: gateway failure, database slowdown, network partition
  - Benchmark: 99.99% success rate under failure
- **Deliverable:** Working system, resilience test report, observability dashboard, incident runbook

---

## Module 10: ML/AI Integration — Model Serving, RAG, and LLM Pipelines

**Duration:** 30 hours  
**Level:** Advanced → Expert

### 10.1 ONNX Runtime and TensorFlow.js in Node.js
- **ONNX Runtime Node.js:** Model loading, inference session, input/output binding, execution providers
- **TensorFlow.js Node.js backend:** GPU acceleration via CUDA, model conversion, saved model loading
- **Performance optimization:** Batch inference, warm-up, memory pooling, input preprocessing
- **Production connection:** ONNX Runtime for cross-platform model serving; TensorFlow.js for Node.js-native GPU inference; batching for throughput

### 10.2 Model Serving Architecture
- **REST API serving:** Fastify endpoint, request validation, response streaming
- **gRPC serving:** Bidirectional streaming for real-time inference
- **Batch inference:** Queue-based batching, dynamic batching, scheduling
- **Model versioning:** A/B testing, canary deployment, shadow traffic
- **Production connection:** REST for simple inference; gRPC streaming for LLM token generation; dynamic batching for cost efficiency

### 10.3 LLM Integration and Streaming
- **OpenAI/Anthropic APIs:** Chat completions, streaming, function calling, embeddings
- **Streaming architecture:** Server-Sent Events for token streaming, backpressure, cancellation
- **Prompt engineering patterns:** System prompts, few-shot, chain-of-thought, ReAct
- **Token management:** Counting, budgeting, truncation strategies
- **Production connection:** Streaming LLM responses for UX; function calling for tool use; token budgeting for cost control

### 10.4 RAG (Retrieval-Augmented Generation) Systems
- **Document ingestion:** Parsing (PDF, HTML, Markdown), chunking strategies, metadata extraction
- **Embedding generation:** OpenAI embeddings, open-source models, batch processing
- **Vector retrieval:** Similarity search, hybrid search (dense + sparse), reranking
- **Context assembly:** Chunk selection, prompt construction, token limit management
- **Evaluation:** Retrieval accuracy, answer relevance, latency
- **Production connection:** Enterprise knowledge bases; customer support chatbots; document Q&A systems

### 10.5 Agent Frameworks and Orchestration
- **LangChain.js / LlamaIndex:** Chains, agents, tools, memory, document loaders
- **Multi-agent systems:** Agent communication, task delegation, consensus
- **Tool use:** Function calling, API integration, code execution (sandboxed)
- **Production connection:** Autonomous research agents; multi-step reasoning systems; tool-augmented customer service

### 10.6 Lab: Building a Production RAG Platform
- **Task:** Build an end-to-end RAG system for enterprise documents
- **Requirements:**
  - Document ingestion pipeline (PDF, Word, web pages)
  - Chunking with overlap, metadata preservation
  - Embedding generation with caching
  - Vector database (Pinecone/pgvector/Weaviate)
  - Hybrid retrieval (semantic + keyword)
  - LLM integration with streaming responses
  - Source attribution in responses
  - Evaluation framework (retrieval recall, answer accuracy)
  - Rate limiting and cost tracking
  - Benchmark: <2s end-to-end latency, >90% retrieval accuracy
- **Deliverable:** Working platform, evaluation report, cost analysis, demo application

---

## Module 11: Performance Engineering & Systems Programming in Node.js

**Duration:** 20 hours  
**Level:** Expert

### 11.1 V8 Performance Tuning
- **Hidden class optimization:** Object shape stability, property ordering, avoid `delete`
- **Inline caching:** Monomorphic → polymorphic → megamorphic, IC state inspection
- **Function optimization:** TurboFan inlining, deoptimization triggers, `--trace-opt`, `--trace-deopt`
- **Memory optimization:** Object pooling, `ArrayBuffer` vs. arrays, `Map` vs. object
- **Production connection:** Hidden class stability in hot paths; avoiding deoptimization in tight loops; object pooling for high-frequency allocation

### 11.2 Native Addons and N-API
- **N-API:** Stable ABI, `node-addon-api` C++ wrapper, lifecycle management
- **node-ffi:** Foreign function interface for calling C libraries
- **Rust addons:** `napi-rs` for memory-safe, high-performance addons
- **WASM integration:** `WebAssembly` in Node.js, WASI, near-native performance
- **Production connection:** N-API for crypto operations; Rust addons for image processing; WASM for sandboxed plugins

### 11.3 Kernel Bypass and High-Performance Networking
- **`io_uring` in Node.js:** liburing bindings, async I/O without syscalls
- **DPDK/AF_XDP:** Userspace networking, packet processing
- **Kernel bypass for databases:** Direct I/O, SPDK for NVMe
- **Production connection:** `io_uring` for high-throughput file I/O; DPDK for custom network stacks; kernel bypass for database engines

### 11.4 Memory and CPU Profiling
- **Heap profiling:** `--heap-prof`, Chrome DevTools, `heapdump`, leak detection
- **CPU profiling:** `--prof`, `--prof-process`, `0x` flamegraphs, `clinic.js`
- **Event loop monitoring:** `clinic.js` bubbleprof, `0x` event loop latency
- **Production connection:** Memory leak detection in long-running services; CPU profiling for hot path optimization; event loop latency monitoring for SLOs

### 11.5 Lab: Building a High-Performance Proxy Server
- **Task:** Build a reverse proxy with custom load balancing
- **Requirements:**
  - HTTP/2 and HTTP/3 support
  - Consistent hashing for backend selection
  - Connection pooling and keep-alive
  - Zero-copy forwarding where possible
  - Circuit breaker per backend
  - Metrics: RPS, latency, error rate, active connections
  - Benchmark: 100K RPS, <1ms P99 latency
- **Deliverable:** Working proxy, performance report, comparison with Nginx/Envoy

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Real-Time Financial Trading Platform
- **Scope:** End-to-end trading system with real-time data and ML inference
- **Components:**
  - Market data ingestion via WebSocket (100K ticks/sec)
  - In-memory order book with Redis Streams
  - ML model serving for price prediction (ONNX Runtime)
  - Order execution with circuit breaker and retry
  - Real-time P&L calculation and risk checks
  - WebSocket dashboard for traders
  - Full observability and audit trail
- **Deliverables:** Working system, latency benchmarks (<10ms tick-to-trade), chaos tests, regulatory compliance documentation

### Capstone B: Multi-Tenant SaaS LLM Platform
- **Scope:** Production-grade LLM serving platform with RAG
- **Components:**
  - Multi-tenant architecture with isolation
  - Document ingestion and embedding pipeline
  - Vector database with hybrid search
  - LLM streaming with token-level billing
  - Rate limiting per tenant
  - Model A/B testing framework
  - Cost tracking and optimization
  - Full observability and alerting
- **Deliverables:** Working platform, multi-tenant load tests, cost analysis, security audit

### Capstone C: Distributed Real-Time Analytics Engine
- **Scope:** Build an analytics platform processing high-volume event streams
- **Components:**
  - Kafka ingestion (1M events/sec)
  - Stream processing with windowing and aggregations
  - Real-time materialized views in Redis
  - GraphQL API for ad-hoc queries
  - Alerting engine with complex event processing
  - Backpressure and graceful degradation
  - Horizontal scaling with Kubernetes
- **Deliverables:** Working engine, performance benchmarks, fault tolerance tests, scaling analysis

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 20% | Code quality, correctness, performance |
| Lab reports | 10% | Design decisions, profiling analysis, type system proofs |
| Peer review | 10% | Reviewing others' code and architecture docs |

### Examinations (30%)
- **Midterm (15%):** TypeScript type system, Node.js internals, API design
- **Final (15%):** Distributed systems, ML integration, performance optimization, resilience patterns

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 10% |
| System design & architecture | 10% |
| Performance & scalability | 5% |
| Observability & reliability | 3% |
| Documentation & presentation | 2% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel type-level abstractions, production-ready, formal reasoning
- **B (80-89):** Solid understanding, minor gaps, good engineering
- **C (70-79):** Adequate understanding, significant gaps, needs improvement
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding

---

## Recommended Tools, Libraries & Infrastructure

### TypeScript Ecosystem
| Tool | Purpose |
|------|---------|
| **TypeScript 5.x** | Language compiler |
| **ts-node / tsx** | TypeScript execution |
| **esbuild / swc** | Fast transpilation |
| **tsc** | Type checking and declaration emit |
| **typescript-eslint** | Lint rules for TypeScript |

### Node.js Runtime
| Tool | Purpose |
|------|---------|
| **Node.js 20+ LTS** | Runtime |
| **Deno** | Alternative secure runtime |
| **Bun** | Fast JavaScript runtime (evaluation) |
| **nvm / fnm** | Version management |

### Web Frameworks
| Tool | Purpose |
|------|---------|
| **Fastify** | High-performance HTTP framework |
| **NestJS** | Enterprise Node.js framework |
| **Express** | Legacy/learning (understand, then move to Fastify) |
| **Hono** | Lightweight edge-compatible framework |

### Databases
| Tool | Purpose |
|------|---------|
| **PostgreSQL 15+** | Primary relational database |
| **Redis 7+** | Caching, streams, real-time |
| **MongoDB** | Document store |
| **pgvector** | Vector search in PostgreSQL |
| **Pinecone / Weaviate** | Managed vector databases |

### Communication
| Tool | Purpose |
|------|---------|
| **gRPC / @grpc/grpc-js** | High-performance RPC |
| **GraphQL / Apollo** | Flexible API layer |
| **Kafka / kafkajs** | Event streaming |
| **NATS** | Lightweight messaging |
| **WebSocket / ws** | Real-time bidirectional |

### ML/AI
| Tool | Purpose |
|------|---------|
| **ONNX Runtime Node.js** | Cross-platform inference |
| **TensorFlow.js Node** | GPU-accelerated inference |
| **OpenAI SDK** | LLM integration |
| **LangChain.js** | LLM application framework |
| **LlamaIndex.TS** | RAG and data indexing |

### Observability
| Tool | Purpose |
|------|---------|
| **Pino** | High-performance logging |
| **OpenTelemetry** | Instrumentation standard |
| **Prometheus client** | Metrics collection |
| **Jaeger** | Distributed tracing |
| **Grafana** | Visualization |

### Testing
| Tool | Purpose |
|------|---------|
| **Vitest** | Fast unit testing |
| **Playwright** | E2E testing |
| **Testcontainers** | Integration testing |
| **Pact** | Contract testing |
| **Artillery / k6** | Load testing |

### Infrastructure
| Tool | Purpose |
|------|---------|
| **Docker** | Containerization |
| **Kubernetes** | Orchestration |
| **Helm** | Package management |
| **Istio / Linkerd** | Service mesh |
| **Terraform** | Infrastructure as code |

---

## References & Further Reading

### TypeScript
1. **TypeScript Handbook** — Official documentation, essential reference
2. **Marius Schulz,** *Effective TypeScript* — 62 specific ways to improve TypeScript
3. **Mariusschulz.com blog** — Deep dives into type system features
4. **Matt Pocock,** Total TypeScript course — Advanced patterns and type-level programming
5. **TypeScript Compiler API documentation** — For AST and code generation

### Node.js Internals
1. **Node.js Design Patterns** (3rd Ed.) — Mario Casciaro, Luciano Mammino
2. **Node.js Internals** blog series — Deep dives into libuv, V8, C++ layer
3. **V8 blog** (v8.dev) — Engine internals, optimization, new features
4. **libuv documentation** — Event loop, thread pool, platform abstraction

### Backend Engineering
1. **Newman,** *Building Microservices* (2nd Ed.) — Platform-agnostic microservices
2. **Richardson,** *Microservices Patterns* — Patterns catalog
3. **Fowler,** *Patterns of Enterprise Application Architecture* — Classic patterns
4. **Hohpe & Woolf,** *Enterprise Integration Patterns* — Messaging patterns

### NestJS
1. **Kamil Myśliwiec,** *NestJS in Action* — Framework author
2. **NestJS documentation** — Comprehensive, well-maintained

### Databases
1. **PostgreSQL documentation** — The best open-source documentation
2. **Redis documentation** — Commands, data types, modules
3. **Martin Kleppmann,** *Designing Data-Intensive Applications* — The definitive data systems book

### ML/AI in Node.js
1. **ONNX Runtime documentation** — Node.js API reference
2. **TensorFlow.js documentation** — Node.js backend guide
3. **OpenAI API documentation** — Best practices for integration
4. **LangChain.js documentation** — Application patterns

### Performance
1. **Node.js performance best practices** — Official guides
2. **Clinic.js documentation** — Profiling and diagnostics
3. **0x documentation** — Flamegraph generation

---

## Appendix A: TypeScript Version Feature Timeline

| Version | Key Features for Backend Engineering |
|---------|--------------------------------------|
| 4.0 | Variadic tuple types, labeled tuple elements |
| 4.1 | Template literal types, key remapping |
| 4.2 | Abstract construct signatures, leading rest elements |
| 4.3 | `override`, static index signatures |
| 4.4 | Control flow analysis for aliased conditions |
| 4.5 | Module suffixes, `lib` from `node_modules` |
| 4.6 | `infer` in template literal types, improved recursion |
| 4.7 | `extends` constraints on `infer`, optional variance annotations |
| 4.8 | Improved inference, `infer` in conditional types |
| 4.9 | `satisfies` operator, auto-accessors |
| 5.0 | Decorators (stage 3), `const` type parameters |
| 5.1 | Easier implicit returns, unrelated type improvements |
| 5.2 | `using` declarations, `Object.groupBy` |
| 5.3 | Import attributes, resolution improvements |
| 5.4 | `NoInfer<T>`, `Object.groupBy` types |
| 5.5 | Type inference improvements, regex types |

## Appendix B: Node.js Event Loop Phases (libuv)

```
   ┌───────────────────────────┐
┌─>│           timers          │
│  │     (setTimeout,          │
│  │      setInterval)         │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks       │
│  │   (I/O callbacks deferred │
│  │    to next loop iteration) │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare         │
│  │    (internal libuv use)     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll              │
│  │  (retrieve new I/O events;  │
│  │   execute I/O callbacks)    │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           check             │
│  │      (setImmediate)         │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │      close callbacks        │
│  │    (socket.on('close', ...))│
│  └───────────────────────────┘
```

## Appendix C: Performance Checklist

Before deploying any Node.js service to production, verify:

- [ ] **Type Safety:** `strict` mode enabled, no `any` in hot paths, exhaustive checks
- [ ] **Performance:** Profiled with clinic.js/0x, hidden classes stable, no megamorphic sites
- [ ] **Memory:** Heap dumps analyzed, no leaks in closures or event listeners
- [ ] **Event Loop:** Latency monitored, CPU-intensive work offloaded to workers
- [ ] **Security:** Dependencies audited (npm audit), secrets in Vault, input validated
- [ ] **Observability:** Pino structured logging, OpenTelemetry traces, Prometheus metrics
- [ ] **Reliability:** Circuit breakers, retry with jitter, graceful shutdown, health checks
- [ ] **Scalability:** Horizontal scaling tested, connection pools sized, cache hit rate >90%
- [ ] **Cost:** Resource utilization optimized, auto-scaling configured, serverless economics analyzed

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: typescript-nodejs-backend-syllabus.md