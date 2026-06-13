  
  ## File: system-design-foundations-syllabus.md

# System Design Foundations for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Distributed Systems & Backend Engineering (or equivalent), Database Design (or equivalent), TypeScript & Node.js Backend Engineering (or equivalent), strong understanding of data structures, algorithms, operating systems, and computer networks  
**Estimated Duration:** 240–300 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: First Principles — Constraints, Trade-offs, and Reasoning](#module-0-first-principles--constraints-trade-offs-and-reasoning)
4. [Module 1: Scalability Laws and Capacity Planning](#module-1-scalability-laws-and-capacity-planning)
5. [Module 2: API Design and Interface Contracts](#module-2-api-design-and-interface-contracts)
6. [Module 3: Data Modeling and Storage Architecture](#module-3-data-modeling-and-storage-architecture)
7. [Module 4: Caching Strategy and Content Delivery](#module-4-caching-strategy-and-content-delivery)
8. [Module 5: Load Balancing and Traffic Management](#module-5-load-balancing-and-traffic-management)
9. [Module 6: Microservices, Service Boundaries, and Communication Patterns](#module-6-microservices-service-boundaries-and-communication-patterns)
10. [Module 7: Message Queues, Event Streaming, and Async Architecture](#module-7-message-queues-event-streaming-and-async-architecture)
11. [Module 8: Reliability Patterns — Resilience, Fault Tolerance, and Chaos](#module-8-reliability-patterns--resilience-fault-tolerance-and-chaos)
12. [Module 9: Observability, Debugging, and Performance Engineering](#module-9-observability-debugging-and-performance-engineering)
13. [Module 10: Security Architecture and Zero-Trust Design](#module-10-security-architecture-and-zero-trust-design)
14. [Module 11: AI/ML System Design — Training, Inference, and Feature Platforms](#module-11-aiml-system-design--training-inference-and-feature-platforms)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **System Design** not as a collection of interview patterns, but as a **rigorous engineering discipline for architecting reliable, scalable, and maintainable systems from first principles**. The pedagogical approach follows a **Constraints → Trade-offs → Architecture → Validation → Evolution** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Constraints** | Business requirements, technical constraints, regulatory boundaries | Clear problem definition |
| **Trade-offs** | CAP, PACELC, latency vs. consistency, cost vs. performance | Documented decisions |
| **Architecture** | Components, interfaces, data flow, failure modes | Design documents |
| **Validation** | Back-of-envelope calculations, prototypes, load testing | Confidence in design |
| **Evolution** | Versioning, migration, deprecation, organizational scaling | Long-term viability |

**Core Principles:**
- **Every design starts with numbers.** We do not architect systems for "millions of users" — we calculate QPS, storage, bandwidth, and latency requirements from business metrics and derive architecture from those numbers.
- **There are no best practices — only contextual trade-offs.** We reject "always use microservices" or "always use NoSQL." We teach the decision framework: given these constraints, these workloads, these team capabilities, this is the rational choice.
- **Failure is the primary design input.** We design for specific failure modes: network partitions, cascading failures, thundering herds, poison pills, clock skew. Every component has a failure budget and a graceful degradation path.
- **The system is not the diagram.** We teach that architecture is the set of invariants, constraints, and decisions that remain when the diagram is erased. The diagram is merely a communication tool.
- **AI systems are systems first.** LLM serving, distributed training, and RAG pipelines are not "AI problems" — they are system design problems with AI-shaped constraints. We apply the same rigor to model serving as we do to payment processing.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### System Design Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Design simple CRUD systems, basic scaling, single-database architectures | Small web applications |
| **Intermediate** | Design for 100K+ QPS, multi-region, caching, message queues, basic microservices | Production platforms |
| **Advanced** | Design for 1M+ QPS, custom protocols, zero-downtime migrations, multi-tenant isolation | Hyperscale systems |
| **Expert** | Design platforms, define organizational architecture standards, mentor staff engineers | Principal+ engineering |

### Analytical Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Back-of-envelope calculations, basic latency analysis | Initial capacity planning |
| **Intermediate** | Queueing theory, tail latency analysis, cost modeling | Detailed capacity planning |
| **Advanced** | Statistical analysis of failure modes, probabilistic reasoning, formal verification sketches | Risk assessment |
| **Expert** | Build custom capacity planning tools, define SLO frameworks, design chaos experiments | Platform engineering |

### AI/ML System Design Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Design simple model serving APIs, basic batch inference | Prototype ML systems |
| **Intermediate** | Design feature stores, distributed training platforms, model registries | Production ML platforms |
| **Advanced** | Design LLM serving infrastructure, RAG systems, multi-modal pipelines | LLM platforms |
| **Expert** | Design AI supercomputers, custom inference accelerators, learned system components | AI infrastructure |

### Cross-Cutting Competencies
- **Communication:** Produce architecture decision records (ADRs), RFCs, and design docs that persuade
- **Collaboration:** Lead design reviews, incorporate feedback, build consensus across teams
- **Economic reasoning:** TCO analysis, cost-per-request optimization, vendor evaluation
- **Evolutionary thinking:** Design for change, deprecation, and organizational scaling

---

## Module 0: First Principles — Constraints, Trade-offs, and Reasoning

**Duration:** 20 hours  
**Purpose:** Establish the mental models and reasoning frameworks that underpin all system design

### 0.1 The Nature of System Design
- **Design vs. implementation:** Architecture as constraint, not code; the architecture is the set of invariants
- **Wicked problems:** No definitive formulation, no stopping rule, no true/false solutions
- **Conway's Law:** System structure mirrors organizational structure; designing systems requires designing teams
- **Production connection:** Why microservices fail at small companies (Conway's Law); why architecture reviews must include org design

### 0.2 Constraints and Requirements Analysis
- **Functional requirements:** What the system must do, user stories, use cases
- **Non-functional requirements:** Performance, availability, scalability, security, maintainability, cost
- **Business constraints:** Time to market, regulatory (GDPR, HIPAA, SOC2), team size, existing tech stack
- **Technical constraints:** Latency budgets, throughput floors, consistency requirements, durability guarantees
- **Production connection:** Why "fast" is not a requirement; why latency budgets must be derived from user experience research; why regulatory constraints shape data flow

### 0.3 Back-of-the-Envelope Calculations
- **The estimation framework:** Knowns, unknowns, assumptions, sensitivity analysis
- **Common numbers:** QPS per user, storage per object, bandwidth per request, memory per connection
- **Latency budgets:** End-to-end latency decomposition, per-component allocation, headroom
- **Scaling factors:** Linear, sublinear, superlinear — when and why
- **Production connection:** Estimating storage for a photo-sharing app; latency budget for a real-time bidding system; QPS for a search engine

### 0.4 Trade-off Frameworks
- **CAP Theorem:** Consistency, Availability, Partition tolerance — choose two, but understand the nuance
- **PACELC:** If partitioned, choose Availability or Consistency; Else, choose Latency or Consistency
- **Latency vs. consistency:** Strong consistency requires coordination; coordination requires waiting
- **Cost vs. performance:** Horizontal scaling, instance types, reserved vs. spot, storage tiers
- **Simplicity vs. functionality:** YAGNI, premature optimization, over-engineering
- **Production connection:** Why Dynamo chose AP; why Spanner chose CP with latency trade-offs; why "eventual consistency" is often the right choice

### 0.5 Design Documentation
- **Architecture Decision Records (ADRs):** Context, decision, consequences, status
- **Request for Comments (RFCs):** Problem, proposal, alternatives, risks, timeline
- **Design docs:** Overview, goals, non-goals, system diagram, data flow, API design, storage design, security, monitoring, rollout plan
- **Production connection:** ADRs for tracking decisions; RFCs for cross-team alignment; design docs for implementation guidance

### 0.6 Lab: Designing a System from a Vague Request
- **Task:** Given "build a URL shortener" — derive complete requirements and architecture
- **Requirements:**
  - Interview stakeholders to extract functional and non-functional requirements
  - Perform back-of-envelope calculations for 1B URLs/day
  - Document trade-offs (hash vs. sequential IDs, SQL vs. NoSQL, cache strategy)
  - Write ADR for each major decision
  - Produce complete design document
  - Present to peers and incorporate feedback
- **Deliverable:** Complete design document set, stakeholder interview notes, calculation spreadsheet

---

## Module 1: Scalability Laws and Capacity Planning

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 1.1 Amdahl's Law and Gustafson's Law
- **Amdahl's Law:** Speedup limit from parallelization, serial fraction dominates
- **Gustafson's Law:** Scaled speedup, problem size grows with processors
- **Universal Scalability Law (USL):** Contention and coherence penalties, modeling superlinear and retrograde scaling
- **Production connection:** Why adding servers doesn't always help; why USL predicts throughput collapse; modeling database read replica scaling

### 1.2 Queueing Theory for System Design
- **Little's Law:** $L = \lambda W$ — relating queue length, arrival rate, and wait time
- **M/M/1 queue:** Steady-state probabilities, utilization, response time
- **M/M/c queue:** Multiple servers, Erlang C formula, queueing probability
- **Kingman's approximation:** G/G/1 queue, variability impact on wait time
- **Tail latency:** Why P99 grows faster than mean; why queueing dominates tail latency
- **Production connection:** Sizing connection pools; predicting latency under load; why 80% utilization is often the practical limit

### 1.3 Capacity Planning Methodologies
- **Trend-based:** Historical growth projection, seasonality, anomaly detection
- **Workload-based:** Per-user metrics, feature-based scaling, what-if analysis
- **Stress-based:** Load testing to failure, identifying bottlenecks, headroom planning
- **Economic capacity planning:** Cost-per-request, marginal cost analysis, reserved capacity vs. elastic scaling
- **Production connection:** Capacity planning for Black Friday; why trend-based fails for step changes; elastic scaling economics

### 1.4 Horizontal vs. Vertical Scaling
- **Vertical scaling:** Bigger machines, NUMA effects, diminishing returns, single points of failure
- **Horizontal scaling:** More machines, data partitioning, statelessness, coordination overhead
- **Elastic scaling:** Auto-scaling groups, Kubernetes HPA, predictive scaling, cooldown periods
- **Production connection:** When vertical scaling is sufficient (databases); when horizontal is required (stateless services); why databases are hard to scale horizontally

### 1.5 The Latency Numberline
- **Latency at every layer:** CPU instruction (1ns), L1 cache (1ns), L2 cache (4ns), L3 cache (20ns), DRAM (100ns), SSD read (10μs), NVMe read (1μs), Datacenter RTT (500μs), Cross-region RTT (50ms), Cross-planet RTT (250ms)
- **Latency budget decomposition:** Per-component allocation, cumulative budgets, headroom
- **Production connection:** Why caching is essential; why SSD matters for databases; why cross-region replication is expensive

### 1.6 Lab: Capacity Planning for a Hyperscale System
- **Task:** Create a capacity plan for a system scaling from 1K to 100M users
- **Requirements:**
  - Define per-user resource requirements (storage, compute, bandwidth)
  - Project infrastructure costs at each scale tier
  - Identify bottleneck transitions (single DB → read replicas → sharding)
  - Model queueing behavior at each tier
  - Design elastic scaling strategy
  - Document cost optimization opportunities
- **Deliverable:** Capacity plan document with cost projections, bottleneck analysis, scaling roadmap

---

## Module 2: API Design and Interface Contracts

**Duration:** 20 hours  
**Level:** Intermediate → Advanced

### 2.1 RESTful Design Principles
- **Resources and representations:** Nouns not verbs, stateless interactions, uniform interface
- **HTTP semantics:** Methods (GET, POST, PUT, PATCH, DELETE), idempotency, safety, cacheability
- **Status codes:** Correct usage, error representation (RFC 7807 Problem Details)
- **HATEOAS:** Hypermedia as the Engine of Application State, link relations, discovery
- **Versioning:** URL, header, media type strategies, deprecation policies
- **Production connection:** Why PATCH is preferred over PUT for partial updates; why idempotency keys are essential for payments; versioning for backward compatibility

### 2.2 GraphQL Design
- **Schema design:** Types, queries, mutations, subscriptions, introspection
- **Resolver patterns:** N+1 problem, DataLoader batching, field-level authorization
- **Federation:** Subgraphs, gateway, entity resolution, query planning
- **Production connection:** When GraphQL beats REST (flexible client queries); when REST beats GraphQL (simple CRUD, caching); federation for microservices APIs

### 2.3 gRPC and Binary Protocols
- **Protocol Buffers:** Schema evolution, binary efficiency, code generation
- **gRPC patterns:** Unary, streaming, bidirectional, deadlines, cancellation
- **Production connection:** gRPC for internal microservices; protobuf for high-throughput APIs; streaming for real-time data

### 2.4 WebSocket and Real-Time APIs
- **WebSocket design:** Connection lifecycle, message framing, backpressure, reconnection
- **SSE (Server-Sent Events):** Unidirectional push, HTTP compatibility, automatic reconnection
- **Production connection:** WebSockets for collaborative editing; SSE for live notifications; choosing based on directionality needs

### 2.5 Idempotency and Safety
- **Idempotency keys:** Generation, storage, deduplication, expiration
- **Exactly-once semantics:** Why exactly-once is an end-to-end property, not a transport property
- **Production connection:** Stripe-style idempotency; why retries require idempotency; distributed idempotency with Redis

### 2.6 Lab: Designing a Multi-Protocol API Platform
- **Task:** Design APIs for a system supporting REST, GraphQL, and gRPC
- **Requirements:**
  - Unified domain model across all protocols
  - Idempotency for mutation operations
  - Rate limiting and authentication across protocols
  - Documentation (OpenAPI, GraphQL schema, proto files)
  - Backward compatibility strategy
  - Performance comparison between protocols
- **Deliverable:** API design document, protocol specifications, performance benchmarks, compatibility matrix

---

## Module 3: Data Modeling and Storage Architecture

**Duration:** 30 hours  
**Level:** Advanced

### 3.1 Relational Data Modeling
- **Entity-Relationship modeling:** Entities, relationships, cardinality, weak entities
- **Normalization:** 1NF through BCNF, functional dependencies, decomposition
- **Denormalization:** When and why, materialized views, read replicas
- **Production connection:** Normalized OLTP schemas; denormalized analytical schemas; choosing based on read/write ratio

### 3.2 NoSQL Data Modeling
- **Document modeling:** Embedding vs. referencing, array growth, document size limits
- **Key-value patterns:** Session storage, caching, counters, leaderboards
- **Wide-column patterns:** Time-series, messaging, event sourcing
- **Graph modeling:** Nodes, edges, properties, traversal patterns
- **Production connection:** Document embedding for one-to-few; referencing for one-to-many; wide-column for time-series

### 3.3 Polyglot Persistence
- **Choosing storage by access pattern:** OLTP (PostgreSQL), OLAP (ClickHouse), cache (Redis), search (Elasticsearch), graph (Neo4j), vectors (Pinecone)
- **Data synchronization:** CDC (Change Data Capture), event sourcing, dual-write, saga pattern
- **Consistency across stores:** Eventual consistency, compensation, read repair
- **Production connection:** E-commerce platform with 5+ storage types; synchronizing orders, inventory, search, analytics

### 3.4 Multi-Tenant Data Architecture
- **Isolation models:** Shared schema, separate schema, separate database
- **Tenant identification:** Tenant ID in every query, row-level security, schema search path
- **Resource allocation:** Per-tenant quotas, noisy neighbor isolation, connection pooling
- **Production connection:** SaaS platforms (Salesforce model); compliance requirements (healthcare); cost optimization

### 3.5 Time-Series and Event Data
- **Time-series characteristics:** High write volume, time-ordered queries, aggregation, retention
- **Schema patterns:** Wide vs. narrow tables, hypertables, bucketing
- **Retention and downsampling:** TTL, continuous aggregation, tiered storage
- **Production connection:** Metrics storage (Prometheus, InfluxDB); event logs; IoT sensor data

### 3.6 Lab: Designing a Polyglot Data Architecture
- **Task:** Design storage for a complex platform (e.g., e-commerce, social media, ML platform)
- **Requirements:**
  - Identify all data types and access patterns
  - Choose appropriate storage for each (minimum 4 types)
  - Design data flow and synchronization between stores
  - Document consistency model and failure handling
  - Model multi-tenancy if applicable
  - Project storage costs at 10x scale
- **Deliverable:** Architecture document, data flow diagrams, consistency analysis, cost projections

---

## Module 4: Caching Strategy and Content Delivery

**Duration:** 20 hours  
**Level:** Intermediate → Advanced

### 4.1 Caching Fundamentals
- **Cache layers:** Browser, CDN, edge, application, distributed, database
- **Cache patterns:** Cache-aside, read-through, write-through, write-behind, refresh-ahead
- **Cache invalidation:** TTL, explicit invalidation, event-driven, probabilistic early expiration
- **Production connection:** Cache-aside for flexibility; write-through for consistency; event-driven for real-time invalidation

### 4.2 Cache Eviction and Replacement
- **Eviction policies:** LRU, LFU, FIFO, random, custom (W-TinyLFU in Caffeine)
- **Size-based eviction:** Max entries, max weight, memory-based
- **Expiration:** TTL, sliding expiration, absolute expiration
- **Production connection:** LRU for general workloads; LFU for skewed access; W-TinyLFU for optimal hit rates

### 4.3 Distributed Caching
- **Redis:** Data structures, persistence, replication, cluster mode, RedLock
- **Memcached:** Simple key-value, slab allocation, no persistence
- **Consistent hashing:** Ring hash, virtual nodes, rendezvous hashing
- **Cache coherence:** Invalidation protocols, lease-based caching, stampedes
- **Production connection:** Redis for complex data structures; Memcached for simple caching; consistent hashing for cache sharding

### 4.4 CDN and Edge Caching
- **CDN architecture:** Origin, edge PoPs, cache hierarchies, purge mechanisms
- **Cache-Control directives:** `max-age`, `s-maxage`, `no-cache`, `no-store`, `must-revalidate`, `stale-while-revalidate`
- **Edge computing:** Cloudflare Workers, Lambda@Edge, Vercel Edge Functions
- **Production connection:** CDN for static assets and API responses; edge computing for personalization; stale-while-revalidate for freshness

### 4.5 Lab: Designing a Multi-Tier Caching Strategy
- **Task:** Design caching for a high-traffic content platform
- **Requirements:**
  - Browser cache for static assets
  - CDN for API responses and images
  - Redis for session and application data
  - Database query cache
  - Cache invalidation strategy (event-driven)
  - Stampede prevention (probabilistic early expiration)
  - Hit rate targets per tier
- **Deliverable:** Caching architecture document, invalidation flow diagrams, hit rate projections, failure mode analysis

---

## Module 5: Load Balancing and Traffic Management

**Duration:** 20 hours  
**Level:** Intermediate → Advanced

### 5.1 Load Balancing Algorithms
- **Static algorithms:** Round-robin, weighted round-robin, IP hash, random
- **Dynamic algorithms:** Least connections, least response time, least loaded, consistent hashing
- **Health checking:** Active (HTTP/TCP probes), passive (response code analysis), custom
- **Production connection:** Round-robin for homogeneous servers; least connections for long-lived connections; consistent hashing for cache affinity

### 5.2 Layer 4 vs. Layer 7 Load Balancing
- **L4 (Transport):** TCP/UDP load balancing, NAT, DSR (Direct Server Return), faster, less intelligent
- **L7 (Application):** HTTP routing, SSL termination, content-based routing, slower, more flexible
- **Production connection:** L4 for database connections; L7 for API gateways; combining both for optimal performance

### 5.3 Global Server Load Balancing (GSLB)
- **DNS-based GSLB:** Round-robin DNS, GeoDNS, latency-based routing, health-aware
- **Anycast:** Same IP from multiple locations, BGP routing, automatic failover
- **Production connection:** Route 53 for DNS-based GSLB; Cloudflare for anycast; latency-based routing for global APIs

### 5.4 Traffic Shaping and Rate Limiting
- **Rate limiting algorithms:** Token bucket, leaky bucket, fixed window, sliding window log, sliding window counter, GCRA
- **Traffic shaping:** Policing vs. shaping, burst handling, QoS
- **Circuit breaking:** Failure detection, half-open state, recovery, bulkheads
- **Production connection:** Token bucket for API rate limiting; circuit breakers for external service calls; bulkheads for resource isolation

### 5.5 Lab: Designing a Global Load Balancing Architecture
- **Task:** Design load balancing for a global SaaS platform
- **Requirements:**
  - DNS-based geographic routing
  - L4 load balancing within regions
  - L7 routing for microservices
  - Health checking and automatic failover
  - Rate limiting per tenant
  - Circuit breakers for downstream services
  - Benchmark: <100ms failover, <1% error rate during failure
- **Deliverable:** Architecture document, traffic flow diagrams, failover test results, rate limiting configuration

---

## Module 6: Microservices, Service Boundaries, and Communication Patterns

**Duration:** 30 hours  
**Level:** Advanced

### 6.1 Monoliths, Microservices, and Modular Monoliths
- **Monolith advantages:** Simplicity, performance, transactional integrity, deployability
- **Microservices drivers:** Independent scaling, team autonomy, polyglot persistence, fault isolation
- **Modular monolith:** Domain boundaries within a deployable unit, migration path
- **Service decomposition strategies:** Domain-driven design, bounded contexts, aggregates, strangler fig pattern
- **Production connection:** Starting with monolith (most cases); splitting when scaling or team size demands; modular monolith as pragmatic middle ground

### 6.2 Service Communication Patterns
- **Synchronous:** REST, gRPC — request/response, timeout handling, retry policies
- **Asynchronous:** Message queues, event buses, CQRS, saga pattern
- **Choreography vs. orchestration:** Event-driven coordination, process managers, state machines
- **Outbox pattern:** Reliable event publishing from transactions
- **Production connection:** gRPC for internal sync; Kafka for async events; outbox for transactional consistency; saga for distributed transactions

### 6.3 API Gateway and Backend-for-Frontend (BFF)
- **Gateway responsibilities:** Authentication, rate limiting, request routing, protocol translation, caching
- **BFF pattern:** Client-specific APIs, aggregation, optimization
- **GraphQL federation:** Subgraphs, gateway, query planning, entity resolution
- **Production connection:** API gateway for cross-cutting concerns; BFF for mobile vs. web optimization; federation for microservices APIs

### 6.4 Service Discovery and Configuration
- **Service registries:** Consul, etcd, Eureka, Kubernetes DNS
- **Client-side discovery:** Load balancer per client, health-aware routing
- **Server-side discovery:** Load balancer as intermediary, transparent to clients
- **Configuration management:** Externalized config, feature flags, dynamic updates
- **Production connection:** Kubernetes DNS for container-native; Consul for multi-cloud; feature flags for safe rollouts

### 6.5 Data Consistency in Microservices
- **Saga pattern:** Compensating transactions, choreography vs. orchestration
- **Event sourcing:** State as event stream, event store, projections
- **CQRS:** Separate read and write models, eventual consistency
- **Production connection:** Saga for order→payment→inventory; event sourcing for audit trails; CQRS for read-heavy workloads

### 6.6 Lab: Designing a Microservices Platform
- **Task:** Design a complete microservices architecture for a complex domain
- **Requirements:**
  - Identify bounded contexts and service boundaries
  - Design synchronous and asynchronous communication
  - Implement saga pattern for a critical flow
  - Design API gateway with BFF
  - Service discovery and configuration
  - Data consistency strategy per flow
  - Failure handling and circuit breakers
- **Deliverable:** Architecture document, service interaction diagrams, saga flow diagram, consistency analysis

---

## Module 7: Message Queues, Event Streaming, and Async Architecture

**Duration:** 25 hours  
**Level:** Advanced

### 7.1 Message Queue Fundamentals
- **Queue semantics:** FIFO, priority, delayed, dead letter, retry
- **Delivery guarantees:** At-most-once, at-least-once, exactly-once processing
- **Backpressure:** Producer blocking, consumer prefetch, credit-based flow control
- **Production connection:** RabbitMQ for complex routing; SQS for simplicity; exactly-once processing with idempotency

### 7.2 Log-Based Messaging — Kafka Architecture
- **Log abstraction:** Append-only, immutable, ordered partition
- **Partitioning:** Key-based, round-robin, custom partitioner
- **Replication:** ISR (In-Sync Replicas), leader election, min.insync.replicas
- **Consumer groups:** Group coordination, partition assignment, offset management
- **Exactly-once:** Idempotent producers, transactions, EOS semantics
- **Production connection:** Kafka for event sourcing; partition design for ordering guarantees; consumer lag monitoring

### 7.3 Stream Processing
- **Stream-table duality:** Tables as materialized views of streams
- **Windowing:** Tumbling, hopping, session, global windows
- **Stateful processing:** Local state stores, changelog topics, state restoration
- **Frameworks:** Apache Flink, Kafka Streams, Spark Structured Streaming
- **Production connection:** Real-time feature computation; stream processing for anomaly detection; windowing for session analysis

### 7.4 Event-Driven Architecture
- **Event types:** Domain events, integration events, notification events
- **Event schema evolution:** Forward compatibility, backward compatibility, schema registry
- **Event sourcing:** Event store, snapshots, projections, event versioning
- **CQRS:** Command handlers, query handlers, read model optimization
- **Production connection:** Domain events for business logic; integration events for cross-service communication; event sourcing for auditability

### 7.5 Lab: Designing an Event-Driven Platform
- **Task:** Design an event-driven architecture for a complex workflow
- **Requirements:**
  - Kafka as event backbone
  - Schema registry with Avro/Protobuf
  - Stream processing for real-time analytics
  - Event sourcing for critical domain
  - CQRS for read optimization
  - Exactly-once processing semantics
  - Monitoring: consumer lag, throughput, error rate
- **Deliverable:** Architecture document, event schema definitions, stream topology diagram, processing guarantees analysis

---

## Module 8: Reliability Patterns — Resilience, Fault Tolerance, and Chaos

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 8.1 Failure Modes and Failure Taxonomy
- **Hardware failures:** Disk failure, memory corruption, network partition, power loss
- **Software failures:** Bugs, resource exhaustion, deadlock, livelock, thundering herd
- **Operational failures:** Configuration errors, deployment failures, human error
- **Byzantine failures:** Malicious or arbitrary behavior, consensus in adversarial settings
- **Production connection:** Designing for specific failure modes; MTBF and MTTR calculations; failure mode and effects analysis (FMEA)

### 8.2 Redundancy and Replication
- **Active-passive:** Primary-backup, failover, split-brain prevention
- **Active-active:** Multi-master, conflict resolution, vector clocks
- **Quorum systems:** Read and write quorums, tunable consistency, hinted handoff
- **Production connection:** Active-passive for databases; active-active for CDNs; quorum for distributed key-value stores

### 8.3 Circuit Breakers and Bulkheads
- **Circuit breaker pattern:** Closed, open, half-open states, failure threshold, recovery
- **Bulkhead pattern:** Resource isolation, thread pool separation, failure containment
- **Retry patterns:** Exponential backoff, jitter, maximum attempts, circuit breaker integration
- **Production connection:** Circuit breaker for external API calls; bulkhead for critical path isolation; retry with jitter for transient failures

### 8.4 Graceful Degradation and Fallbacks
- **Degradation strategies:** Feature flags, reduced functionality, cached responses, static fallbacks
- **Fallback chains:** Primary → cache → static → error message
- **Load shedding:** Admission control, request prioritization, dropping non-critical work
- **Production connection:** Degrading search to cached results; falling back to static content; shedding load during overload

### 8.5 Chaos Engineering
- **Principles:** Hypothesis-driven, blast radius control, automated rollback
- **Failure injection:** Network latency, packet loss, CPU pressure, memory pressure, disk failure, process kills, zone failures
- **Game days:** Planned chaos experiments, team response validation, post-mortem
- **Tools:** Chaos Monkey, Gremlin, Litmus, AWS Fault Injection Simulator
- **Production connection:** Netflix's Simian Army; chaos engineering for resilience validation; automated chaos in CI/CD

### 8.6 Lab: Designing a Resilient Payment System
- **Task:** Design a payment processing system with comprehensive resilience patterns
- **Requirements:**
  - Idempotent payment processing
  - Circuit breaker for payment gateway
  - Retry with exponential backoff and jitter
  - Saga pattern for distributed transaction (payment→inventory→shipping)
  - Graceful degradation (queue payments if gateway down)
  - Chaos testing: gateway failure, database slowdown, network partition
  - Target: 99.99% success rate under failure
- **Deliverable:** Architecture document, resilience test results, chaos experiment report, incident runbook

---

## Module 9: Observability, Debugging, and Performance Engineering

**Duration:** 25 hours  
**Level:** Advanced

### 9.1 The Three Pillars of Observability
- **Metrics:** Counters, gauges, histograms, summaries, exemplars, cardinality
- **Logs:** Structured logging, correlation IDs, log levels, aggregation
- **Traces:** Spans, traces, context propagation, sampling strategies
- **Production connection:** Metrics for alerting; logs for debugging; traces for latency analysis

### 9.2 Metrics and Alerting
- **Metric types:** Counter (monotonic), gauge (point-in-time), histogram (distribution), summary (quantiles)
- **RED method:** Rate, Errors, Duration — for services
- **USE method:** Utilization, Saturation, Errors — for resources
- **Alerting:** Threshold-based, anomaly detection, SLO-based, alert fatigue prevention
- **Production connection:** Prometheus + Grafana for metrics; SLO-based alerting for error budgets; cardinality control for cost

### 9.3 Distributed Tracing
- **Trace model:** Spans, parent-child relationships, context propagation, baggage
- **Sampling:** Head-based, tail-based, adaptive, probabilistic
- **OpenTelemetry:** Standardization, auto-instrumentation, manual spans, collectors
- **Production connection:** Jaeger for trace visualization; tail-based sampling for error analysis; OpenTelemetry for vendor neutrality

### 9.4 Performance Engineering
- **Profiling:** CPU profiling, memory profiling, I/O profiling, flame graphs
- **Load testing:** Throughput, latency, error rate, saturation point
- **Stress testing:** Breaking point, graceful degradation, recovery
- **Soak testing:** Memory leaks, resource exhaustion, long-term stability
- **Production connection:** Profiling for hot path optimization; load testing before production; soak testing for memory leak detection

### 9.5 Lab: Building an Observability Platform
- **Task:** Design and implement observability for a distributed system
- **Requirements:**
  - Metrics collection (Prometheus client)
  - Structured logging with correlation IDs
  - Distributed tracing with OpenTelemetry
  - Alerting rules (Prometheus Alertmanager)
  - Dashboards (Grafana)
  - Log aggregation (Loki or ELK)
  - Custom SLO definitions and error budgets
  - Chaos engineering integration
- **Deliverable:** Working observability stack, demo with sample services, SLO dashboard, incident response runbook

---

## Module 10: Security Architecture and Zero-Trust Design

**Duration:** 20 hours  
**Level:** Advanced

### 10.1 Threat Modeling
- **STRIDE:** Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege
- **Attack trees:** Goal-oriented threat analysis, AND/OR decomposition
- **Threat modeling process:** Identify assets, identify threats, mitigate, validate
- **Production connection:** Threat modeling for API design; attack trees for payment systems; regular threat model updates

### 10.2 Authentication and Authorization
- **OAuth 2.0 / OpenID Connect:** Flows, tokens, JWT structure, refresh tokens
- **mTLS:** Certificate-based authentication, mutual TLS in service meshes
- **SPIFFE/SPIRE:** Workload identity, automatic certificate provisioning
- **RBAC and ABAC:** Role-based vs. attribute-based access control
- **Production connection:** OAuth for user-facing APIs; mTLS for service-to-service; SPIFFE for zero-trust Kubernetes

### 10.3 Data Protection
- **Encryption at rest:** AES-GCM, key management (KMS, HSM), envelope encryption
- **Encryption in transit:** TLS 1.3, certificate pinning, perfect forward secrecy
- **Tokenization:** Replacing sensitive data with non-sensitive equivalents
- **Production connection:** KMS for database encryption; TLS for all service communication; tokenization for PCI compliance

### 10.4 Zero-Trust Architecture
- **Never trust, always verify:** Per-request authentication, least privilege, micro-segmentation
- **Identity-aware proxies:** BeyondCorp model, context-aware access
- **Network segmentation:** Micro-segmentation, service mesh as security boundary
- **Production connection:** Google's BeyondCorp; zero-trust for multi-tenant SaaS; identity-aware proxies for internal tools

### 10.5 Lab: Designing a Zero-Trust Architecture
- **Task:** Design zero-trust security for a microservices platform
- **Requirements:**
  - mTLS for all service communication
  - JWT-based authentication with RBAC
  - Fine-grained authorization (ABAC)
  - Network micro-segmentation
  - Audit logging for all access decisions
  - Integration with identity provider
  - Threat model documentation
- **Deliverable:** Security architecture document, implementation guide, audit trail demo, penetration testing plan

---

## Module 11: AI/ML System Design — Training, Inference, and Feature Platforms

**Duration:** 30 hours  
**Level:** Expert

### 11.1 ML Training Infrastructure
- **Data pipeline:** Ingestion, validation, transformation, feature engineering
- **Training orchestration:** Experiment tracking, hyperparameter tuning, distributed training
- **Model versioning:** Artifact storage, lineage, reproducibility
- **Production connection:** MLflow for experiment tracking; Kubeflow for pipeline orchestration; DVC for data versioning

### 11.2 Model Serving Architecture
- **Batch inference:** Scheduled jobs, large-scale processing, result storage
- **Real-time inference:** REST/gRPC APIs, model warm-up, batching, caching
- **Model optimization:** Quantization, pruning, compilation (ONNX, TensorRT)
- **A/B testing:** Shadow traffic, canary deployments, statistical evaluation
- **Production connection:** Batch for offline predictions; real-time for user-facing features; TensorRT for GPU inference

### 11.3 Feature Store Design
- **Architecture:** Online store (low-latency), offline store (batch), feature registry
- **Point-in-time correctness:** Temporal joins, event time processing, preventing leakage
- **Consistency:** Training-serving skew detection, feature validation, drift monitoring
- **Production connection:** Feast/Tecton for feature management; point-in-time joins for training; drift detection for retraining triggers

### 11.4 LLM System Design
- **Inference optimization:** KV-cache, continuous batching, speculative decoding, quantization
- **Serving frameworks:** vLLM, TensorRT-LLM, TGI, custom runtimes
- **RAG architecture:** Document ingestion, embedding, vector retrieval, context assembly
- **Agent systems:** Tool use, multi-agent orchestration, state management
- **Production connection:** vLLM for high-throughput serving; RAG for enterprise knowledge bases; agents for autonomous workflows

### 11.5 Lab: Designing an End-to-End ML Platform
- **Task:** Design a complete ML platform from data to serving
- **Requirements:**
  - Data ingestion and validation pipeline
  - Feature store with online and offline stores
  - Distributed training with experiment tracking
  - Model registry with versioning
  - Real-time serving with A/B testing
  - Monitoring: model drift, latency, throughput
  - Cost tracking and optimization
  - Security: model access control, data privacy
- **Deliverable:** Architecture document, component interaction diagrams, data flow, cost model, security analysis

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Global E-Commerce Platform
- **Scope:** Design a platform serving 100M+ users across 5 continents
- **Components:**
  - Multi-region architecture with data residency
  - Polyglot persistence (SQL, NoSQL, cache, search, vector)
  - Microservices with event-driven communication
  - Global load balancing and CDN
  - Real-time inventory and pricing
  - Fraud detection pipeline
  - Comprehensive observability
- **Deliverables:** Architecture document, back-of-envelope calculations, trade-off analysis, cost model, failure mode matrix

### Capstone B: Real-Time AI Inference Platform
- **Scope:** Design a platform for real-time ML model serving at scale
- **Components:**
  - Model serving with dynamic batching and GPU optimization
  - Feature store with <10ms online serving
  - A/B testing and shadow traffic
  - Multi-model composition (ensemble, pipeline)
  - Streaming inference for real-time data
  - Auto-scaling based on queue depth
  - Model drift detection and automatic retraining triggers
- **Deliverables:** Architecture document, latency budget, throughput analysis, cost model, reliability analysis

### Capstone C: LLM-Powered Enterprise Platform
- **Scope:** Design a platform for enterprise LLM applications with RAG
- **Components:**
  - Multi-tenant document ingestion and processing
  - Vector database with hybrid search
  - LLM serving with streaming and cost control
  - Agent framework for multi-step reasoning
  - Human-in-the-loop feedback system
  - Compliance and audit trail
  - Cost optimization and token budgeting
- **Deliverables:** Architecture document, security analysis, cost projections, scalability analysis, compliance documentation

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Design exercises | 20% | Architecture documents, trade-off analyses |
| Lab implementations | 10% | Working prototypes of designed systems |
| Peer review | 10% | Reviewing and critiquing others' designs |

### Examinations (30%)
- **Midterm (15%):** Scalability laws, caching, load balancing, microservices
- **Final (15%):** Reliability, observability, security, AI/ML system design

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 8% |
| System design & architecture | 10% |
| Trade-off reasoning | 5% |
| Scalability & performance | 4% |
| Documentation & presentation | 3% |

### Grading Rubric
- **A (90-100):** Publication-quality design, novel insights, production-ready, persuasive communication
- **B (80-89):** Solid understanding, minor gaps, good engineering reasoning
- **C (70-79):** Adequate understanding, significant gaps, needs improvement
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding

---

## Recommended Tools, Libraries & Infrastructure

### Design and Documentation
| Tool | Purpose |
|------|---------|
| **Draw.io / Excalidraw** | Architecture diagrams |
| **PlantUML / Mermaid** | Diagrams as code |
| **Notion / Confluence** | Design documentation |
| **ADR Tools** | Architecture Decision Records |

### Cloud Platforms
| Tool | Purpose |
|------|---------|
| **AWS** | Primary cloud platform |
| **GCP** | Alternative cloud, AI/ML services |
| **Azure** | Enterprise cloud, hybrid |
| **Terraform / Pulumi** | Infrastructure as code |

### Container and Orchestration
| Tool | Purpose |
|------|---------|
| **Docker** | Containerization |
| **Kubernetes** | Orchestration |
| **Helm** | Package management |
| **Istio / Linkerd** | Service mesh |

### Messaging and Streaming
| Tool | Purpose |
|------|---------|
| **Apache Kafka** | Event streaming |
| **Apache Pulsar** | Tiered storage messaging |
| **RabbitMQ** | Message queue |
| **Redis Streams** | Lightweight streaming |

### Observability
| Tool | Purpose |
|------|---------|
| **Prometheus** | Metrics |
| **Grafana** | Visualization |
| **Jaeger** | Tracing |
| **Loki** | Log aggregation |
| **OpenTelemetry** | Instrumentation |

### Load Balancing
| Tool | Purpose |
|------|---------|
| **Nginx** | L7 load balancer |
| **HAProxy** | L4/L7 load balancer |
| **Envoy** | Service proxy |
| **AWS ALB / NLB** | Cloud load balancers |

### Security
| Tool | Purpose |
|------|---------|
| **Vault** | Secrets management |
| **Keycloak / Okta** | Identity provider |
| **Cert-manager** | Certificate automation |
| **Falco** | Runtime security |

### ML/AI
| Tool | Purpose |
|------|---------|
| **Kubeflow** | ML pipelines |
| **MLflow** | Experiment tracking |
| **Feast** | Feature store |
| **vLLM** | LLM serving |
| **LangChain** | LLM applications |

---

## References & Further Reading

### System Design Classics
1. **Kleppmann,** *Designing Data-Intensive Applications* — The definitive systems book
2. **Newman,** *Building Microservices* (2nd Ed.) — Practical microservices
3. **Richardson,** *Microservices Patterns* — Patterns catalog
4. **Hohpe & Woolf,** *Enterprise Integration Patterns* — Messaging patterns
5. **Fowler,** *Patterns of Enterprise Application Architecture* — Classic patterns

### Scalability and Performance
1. **Nygard,** *Release It!* — Stability patterns
2. **Allspaw,** *The Art of Capacity Planning* — Practical capacity planning
3. **Schwartz et al.,** *The Universal Scalability Law* — Formal scalability modeling

### Reliability and SRE
1. **Beyer et al.,** *Site Reliability Engineering* — Google SRE book
2. **Beyer et al.,** *The Site Reliability Workbook* — Practical SRE
3. **Allspaw,** "Blameless PostMortems and a Just Culture" — Post-mortem culture

### Security
1. **Stallings & Brown,** *Computer Security: Principles and Practice*
2. **Bottum et al.,** *BeyondCorp* papers — Google's zero-trust architecture

### AI/ML Systems
1. **Huyen,** *Designing Machine Learning Systems* — MLOps from first principles
2. **Sculley et al.,** "Machine Learning: The High Interest Credit Card of Technical Debt" — ML systems paper
3. **vLLM paper:** "Efficient Memory Management for Large Language Model Serving with PagedAttention"

---

## Appendix A: Back-of-the-Envelope Calculation Template

```
1. Requirements
   - Users: _____
   - Daily active: _____
   - Peak QPS: _____
   - Data per user: _____
   - Total storage: _____
   - Growth rate: _____

2. Latency Budget
   - End-to-end target: _____ ms
   - DNS: _____ ms
   - TLS handshake: _____ ms
   - Load balancer: _____ ms
   - Application: _____ ms
   - Database: _____ ms
   - Cache: _____ ms
   - Network: _____ ms
   - Headroom (20%): _____ ms

3. Capacity
   - Requests per server: _____
   - Servers needed: _____
   - Database connections: _____
   - Cache memory: _____
   - Storage growth: _____ GB/month
```

## Appendix B: Trade-off Decision Matrix

| Decision | Option A | Option B | Criteria | Winner |
|----------|----------|----------|----------|--------|
| Consistency | Strong | Eventual | Latency budget | _____ |
| Storage | SQL | NoSQL | Query complexity | _____ |
| Communication | Sync | Async | Response time | _____ |
| Scaling | Vertical | Horizontal | Cost | _____ |
| Caching | Write-through | Cache-aside | Consistency | _____ |

## Appendix C: Failure Mode Checklist

For every component, document:
- [ ] **Failure mode:** What can go wrong?
- [ ] **Detection:** How do we know it failed?
- [ ] **Impact:** What is the blast radius?
- [ ] **Mitigation:** How do we contain it?
- [ ] **Recovery:** How do we restore service?
- [ ] **Prevention:** How do we prevent recurrence?

## Appendix D: Production Checklist

Before any system design is approved for implementation, verify:

- [ ] **Requirements:** Functional and non-functional requirements documented and agreed
- [ ] **Calculations:** Back-of-envelope calculations completed and reviewed
- [ ] **Trade-offs:** Major decisions documented with rationale in ADRs
- [ ] **Failure modes:** Failure mode analysis completed for all components
- [ ] **Security:** Threat model completed, security requirements defined
- [ ] **Observability:** Metrics, logs, traces, alerts designed
- [ ] **Capacity:** Scaling plan documented, cost model approved
- [ ] **Migration:** Rollout plan, rollback plan, deprecation plan defined
- [ ] **Operations:** Runbooks written, on-call rotation defined
- [ ] **Review:** Design reviewed by at least two senior engineers

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: system-design-foundations-syllabus.md