
## File: distributed-systems-backend-syllabus.md

# Distributed Systems & Backend Engineering

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Python for AI/ML & Backend Engineering (or equivalent), Operating Systems, Computer Networks, Data Structures & Algorithms, Linear Algebra, basic systems programming (C/C++ or Rust preferred)  
**Estimated Duration:** 280–340 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: Systems Foundations & Mathematical Primitives](#module-0-systems-foundations--mathematical-primitives)
4. [Module 1: The Network Layer — Protocols, Semantics, and Performance](#module-1-the-network-layer--protocols-semantics-and-performance)
5. [Module 2: Concurrency, Parallelism, and the Event Loop](#module-2-concurrency-parallelism-and-the-event-loop)
6. [Module 3: Consensus, Replication, and Fault Tolerance](#module-3-consensus-replication-and-fault-tolerance)
7. [Module 4: Distributed Storage Systems](#module-4-distributed-storage-systems)
8. [Module 5: Distributed Messaging, Streaming, and Event-Driven Architecture](#module-5-distributed-messaging-streaming-and-event-driven-architecture)
9. [Module 6: Service Architecture — From Monolith to Mesh](#module-6-service-architecture--from-monolith-to-mesh)
10. [Module 7: Load Balancing, Traffic Management, and Edge Systems](#module-7-load-balancing-traffic-management-and-edge-systems)
11. [Module 8: Observability, Reliability Engineering, and SRE](#module-8-observability-reliability-engineering-and-sre)
12. [Module 9: Security, Identity, and Zero-Trust in Distributed Systems](#module-9-security-identity-and-zero-trust-in-distributed-systems)
13. [Module 10: ML Infrastructure — Distributed Training and Model Serving](#module-10-ml-infrastructure--distributed-training-and-model-serving)
14. [Module 11: Emerging Frontiers — Serverless, WASM, Unikernels, and Beyond](#module-11-emerging-frontiers--serverless-wasm-unikernels-and-beyond)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Distributed Systems** and **Backend Engineering** as a **unified discipline of reliable computation at scale**. The pedagogical approach follows a **Mechanism → Model → System → Scale → Resilience** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Mechanism** | Network protocols, OS primitives, hardware behavior | Correct low-level code |
| **Model** | Formal models (consensus, consistency, CAP), distributed algorithms | Provable reasoning |
| **System** | Database design, message brokers, service meshes | Working infrastructure |
| **Scale** | Horizontal scaling, sharding, federation, multi-region | Production-grade platforms |
| **Resilience** | Fault tolerance, chaos engineering, disaster recovery | Antifragile systems |

**Core Principles:**
- **Every abstraction must be grounded in mechanism.** We do not teach "use Kafka" — we teach *why* log-based replication provides total order, *why* partition leadership matters, *why* exactly-once is a lie.
- **Failures are the primary design constraint.** Network partitions, clock skew, GC pauses, disk corruption, Byzantine faults — every system is designed with explicit failure models.
- **Performance is a correctness property.** Tail latency, throughput variance, and resource efficiency are not afterthoughts; they shape architecture.
- **Observability is not logging.** Distributed tracing, metrics cardinality, and structured events are first-class system outputs.
- **ML infrastructure is distributed systems.** Distributed training, model serving, and feature stores are not "ML topics" — they are distributed systems problems with ML-shaped data.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Distributed Systems Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Understand RPC, REST, basic concurrency, single-node databases | Simple web services |
| **Intermediate** | Implement consensus algorithms, design replicated systems, handle network partitions | Production microservices |
| **Advanced** | Design distributed databases, build custom message brokers, optimize for tail latency | Platform engineering |
| **Expert** | Design planet-scale systems, reason about CAP formally, build custom schedulers | Staff+ infrastructure |

### Backend Engineering Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | REST APIs, basic ORM, containerization, simple caching | CRUD services |
| **Intermediate** | Async services, connection pooling, circuit breakers, message queues | High-throughput APIs |
| **Advanced** | Custom protocols, zero-copy I/O, kernel bypass, eBPF | Low-latency trading, search |
| **Expert** | Design backend platforms, optimize for millions of RPS, build custom load balancers | Hyperscale infrastructure |

### ML Infrastructure Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Single-GPU training, basic model serving with Flask/FastAPI | Research prototypes |
| **Intermediate** | Distributed training (DDP, FSDP), batch inference pipelines, model registries | Production ML |
| **Advanced** | Custom collective communication, pipeline parallelism, speculative serving | LLM platforms |
| **Expert** | Design training supercomputers, build inference accelerators, optimize for petaflops | AI supercomputing |

### Cross-Cutting Competencies
- **Formal reasoning:** Prove safety and liveness properties of distributed algorithms
- **Systems programming:** Write kernel modules, eBPF programs, DPDK applications
- **Operational thinking:** Design runbooks, incident response, post-mortem culture
- **Economic reasoning:** Cost-per-query, TCO analysis, capacity planning

---

## Module 0: Systems Foundations & Mathematical Primitives

**Duration:** 25 hours  
**Purpose:** Establish the mathematical and systems primitives that underpin all distributed systems

### 0.1 The Physics of Distributed Systems
- **Speed of light and latency:** Round-trip times (RTT) — datacenter (~500μs), cross-region (~50ms), cross-planet (~250ms)
- **Bandwidth-delay product:** Why 10Gbps links need large buffers; TCP window scaling
- **Memory hierarchy in distributed context:** Local DRAM (~100ns) → Remote DRAM via RDMA (~1μs) → SSD (~100μs) → Remote SSD (~1ms) → Cross-region object storage (~100ms)
- **Clocks and time:** Physical clocks, logical clocks, clock skew, NTP limitations, TrueTime (Spanner)
- **Production connection:** Why LLM inference batching matters (amortizing RTT); why feature stores need local caching; why Spanner's TrueTime enables external consistency

### 0.2 Mathematical Foundations
- **Partial orders and causal relationships:** Happens-before (Lamport), vector clocks, version vectors
- **Lattice theory:** Join-semilattices, monotonicity, CRDTs as lattice computations
- **Graph theory in distributed systems:** Dependency graphs, DAG scheduling, consensus as graph coloring
- **Probability and tail bounds:** Markov, Chebyshev, Chernoff bounds; why "average latency" is meaningless
- **Queueing theory:** M/M/1, M/M/c, Little's Law, Kingman's formula for tail latency
- **Production connection:** Vector clocks in version control (Git); CRDTs in collaborative editing (Figma); queueing theory for autoscaling

### 0.3 Operating Systems Primitives
- **Processes, threads, and fibers:** Scheduling, context switches, NUMA awareness
- **Virtual memory:** Page tables, TLB, huge pages, memory-mapped files
- **I/O subsystems:** Syscalls, `epoll`/`kqueue`/`io_uring`, DMA, zero-copy (`sendfile`, `splice`)
- **Network stack:** Kernel networking, DPDK, AF_XDP, RDMA (InfiniBand, RoCE)
- **Production connection:** `io_uring` for high-performance I/O; DPDK for custom network stacks; RDMA for distributed training collectives

### 0.4 Computer Networks Deeply
- **Layer 2–4 review:** Ethernet, IP, TCP, UDP — not just "how" but "why"
- **TCP internals:** Congestion control (Reno, CUBIC, BBR), slow start, fast retransmit, SACK, Nagle, delayed ACK
- **QUIC and HTTP/3:** Connection migration, 0-RTT, stream multiplexing, loss recovery
- **gRPC internals:** HTTP/2 framing, flow control, HPACK, protobuf serialization
- **Production connection:** Why BBR improves throughput on lossy links; why QUIC matters for mobile; gRPC streaming for model serving

### 0.5 Lab: Building a High-Performance Network Stack
- **Task:** Implement a minimal TCP-like protocol over UDP
- **Requirements:**
  - Reliable ordered delivery with sequence numbers and ACKs
  - Sliding window flow control
  - Simple congestion control (additive increase, multiplicative decrease)
  - Benchmark against real TCP on loopback and LAN
- **Deliverable:** Working implementation in C/Rust/Go, performance comparison, packet capture analysis with Wireshark

---

## Module 1: The Network Layer — Protocols, Semantics, and Performance

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 1.1 Remote Procedure Call (RPC) Semantics
- **At-least-once:** Idempotency requirements, duplicate detection
- **At-most-once:** Request deduplication, exactly-once processing
- **Exactly-once:** The FLP impossibility result, why exactly-once is a end-to-end property (not a transport property)
- **Request lifecycle:** Serialization, transport, deserialization, dispatch, execution, response
- **Production connection:** Why payment systems need idempotency keys; why Kafka's exactly-once is actually "exactly-once processing" not "exactly-once delivery"

### 1.2 Serialization and Schema Evolution
- **Binary formats:** Protocol Buffers, FlatBuffers, Cap'n Proto, MessagePack, Avro
- **Schema evolution:** Forward compatibility, backward compatibility, default values, reserved fields
- **Zero-copy deserialization:** FlatBuffers/Cap'n Proto — structured access without parsing
- **Text formats:** JSON, YAML, TOML — when and why
- **Production connection:** Protobuf for internal microservices; Avro for Kafka schemas with Schema Registry; FlatBuffers for game state synchronization

### 1.3 Service Discovery and Naming
- **DNS:** TTL, caching, SRV records, load balancing via DNS
- **Service registries:** Consul, etcd, ZooKeeper, Eureka
- **Load balancer integration:** Health checks, dynamic reconfiguration
- **Production connection:** Kubernetes DNS and service discovery; Consul for multi-cluster; etcd as the Kubernetes backing store

### 1.4 Connection Management
- **Connection pooling:** Pool sizing, eviction, health checking, circuit breaking
- **Keep-alive and idle timeouts:** TCP keepalive, HTTP keepalive, application-level heartbeats
- **Backpressure:** TCP flow control, HTTP/2 stream flow control, application-level backpressure
- **Production connection:** Connection pool exhaustion in microservices; backpressure in streaming pipelines; gRPC keepalive for long-lived streams

### 1.5 Lab: Building a Production RPC Framework
- **Task:** Build a minimal gRPC-like framework
- **Requirements:**
  - IDL with code generation (protobuf-style)
  - Binary serialization/deserialization
  - Request multiplexing over a single TCP connection
  - Service discovery integration (Consul or etcd)
  - Load balancing (round-robin, least-connections)
  - Circuit breaker pattern
- **Deliverable:** Working framework in Go/Rust, benchmarks against real gRPC, fault injection tests

---

## Module 2: Concurrency, Parallelism, and the Event Loop

**Duration:** 30 hours  
**Level:** Intermediate → Advanced

### 2.1 Threading Models and Memory Models
- **POSIX threads:** Creation, joining, cancellation, thread-local storage
- **Memory consistency models:** Sequential consistency, TSO, release-acquire, relaxed
- **Lock-free programming:** Atomics, CAS loops, ABA problem, hazard pointers, epoch-based reclamation
- **Memory ordering:** Compiler barriers, CPU fences, `std::atomic` in C++, `atomic` in Rust
- **Production connection:** Lock-free queues in Disruptor (LMAX); epoch-based reclamation in databases; memory ordering bugs in concurrent data structures

### 2.2 The Actor Model
- **Actors as computational entities:** Message passing, isolation, location transparency
- **Actor systems:** Akka, Orleans, Erlang/OTP, Actix (Rust)
- **Supervision trees:** Let-it-crash philosophy, fault containment, restart strategies
- **Distributed actors:** Actor remoting, clustering, sharding, persistent actors
- **Production connection:** WhatsApp's Erlang backend; Orleans for virtual actors in Halo; Akka Cluster for distributed stateful services

### 2.3 Event-Driven and Reactor Patterns
- **Reactor pattern:** Single-threaded event loop, handlers, demultiplexing
- **Proactor pattern:** Asynchronous I/O completion, callback chains
- **`epoll`/`kqueue`/`io_uring`:** Scalable I/O multiplexing, edge-triggered vs. level-triggered
- **Production connection:** Nginx event loop; Redis single-threaded architecture; `io_uring` in modern databases

### 2.4 Async/Await and Structured Concurrency
- **Coroutines and continuations:** Stackful vs. stackless, suspend/resume semantics
- **Async/await in practice:** Task spawning, cancellation, structured concurrency (Kotlin, Swift, Trio)
- **Color problem:** Sync/async function color, bridging strategies
- **Production connection:** Python asyncio for ML serving; Rust async for high-performance proxies; structured concurrency for reliable task management

### 2.5 Parallel Patterns for ML
- **Data parallelism:** Same model, different data, gradient aggregation
- **Model parallelism:** Different model shards, same data, pipeline scheduling
- **Tensor parallelism:** Intra-layer splitting, all-reduce collectives
- **Pipeline parallelism:** Inter-layer pipelining, bubble optimization
- **Production connection:** PyTorch DDP (data parallelism); Megatron-LM (tensor + pipeline); FSDP (sharded data parallelism)

### 2.6 Lab: Building a High-Concurrency Server
- **Task:** Build an HTTP server handling 100K concurrent connections
- **Requirements:**
  - Single-threaded async event loop (from scratch or libuv-based)
  - HTTP/1.1 keepalive and HTTP/2 support
  - Connection pooling and backpressure
  - Benchmark with `wrk`/`wrk2` — target: 1M RPS on a single core
  - Memory profiling under load
- **Deliverable:** Working server in C/Rust/Go, performance report, comparison with Nginx

---

## Module 3: Consensus, Replication, and Fault Tolerance

**Duration:** 35 hours  
**Level:** Advanced → Expert

### 3.1 The Consensus Problem
- **FLP impossibility:** Fischer, Lynch, Paterson — asynchronous systems cannot guarantee consensus with even one faulty process
- **System models:** Synchronous, asynchronous, partially synchronous; crash-stop, crash-recovery, Byzantine
- **Paxos:** Proposers, acceptors, learners; single decree vs. multi-Paxos; liveness issues
- **Raft:** Leader election, log replication, safety, membership changes (joint consensus)
- **Production connection:** etcd uses Raft; ZooKeeper uses Zab (Paxos variant); understanding why leader election takes time

### 3.2 Byzantine Fault Tolerance
- **Byzantine Generals Problem:** The original formulation, oral vs. signed messages
- **PBFT (Practical Byzantine Fault Tolerance):** View changes, request handling, checkpointing
- **BFT variants:** HotStuff, Tendermint, SBFT — modern optimizations
- **Production connection:** Blockchain consensus (Ethereum, Cosmos); distributed systems in adversarial environments; why BFT matters for federated learning

### 3.3 State Machine Replication
- **Deterministic state machines:** Same inputs → same outputs, same order
- **Log replication:** Total order broadcast, primary-backup, active replication
- **Snapshotting and recovery:** Checkpoints, incremental snapshots, log compaction
- **Production connection:** Redis replication; MySQL binlog replication; Kafka log replication

### 3.4 Distributed Transactions
- **Two-Phase Commit (2PC):** Coordinator, participants, blocking problem
- **Three-Phase Commit (3PC):** Non-blocking coordinator recovery, complexity
- **Saga pattern:** Compensating transactions, choreography vs. orchestration
- **Percolator / Spanner:** Two-phase commit with timestamps, external consistency
- **Production connection:** Database transactions across shards; saga pattern in microservices; Spanner for globally consistent databases

### 3.5 Failure Detection and Membership
- **Phi accrual failure detector:** Adaptive suspicion levels, gossip protocols
- **SWIM protocol:** Scalable weakly-consistent infection-style membership
- **Gossip protocols:** Anti-entropy, rumor mongering, dissemination
- **Production connection:** Consul's gossip layer; Cassandra's failure detection; membership in distributed ML clusters

### 3.6 Lab: Implementing Raft
- **Task:** Implement the Raft consensus algorithm
- **Requirements:**
  - Leader election with randomized timeouts
  - Log replication with consistency checks
  - Snapshotting and log compaction
  - Membership changes (single-server or joint consensus)
  - Linearizable reads (read index or lease-based)
  - Fault injection: network partitions, leader crashes, message delays
- **Deliverable:** Working implementation in Go/Rust, Jepsen-style tests, formal safety argument

---

## Module 4: Distributed Storage Systems

**Duration:** 35 hours  
**Level:** Advanced → Expert

### 4.1 Storage Fundamentals
- **Disk I/O:** Seek time, rotational latency, transfer time, SSD vs. HDD, NVMe
- **File systems:** Ext4, XFS, Btrfs, ZFS — journaling, copy-on-write, checksums
- **Page cache and buffer management:** LRU, clock algorithm, double buffering
- **Write-ahead logging (WAL):** Durability, crash recovery, checkpointing
- **Production connection:** Why ZFS matters for data integrity; page cache behavior in databases; WAL in PostgreSQL

### 4.2 B-Trees and LSM-Trees
- **B-Trees:** Node structure, insertion, deletion, rebalancing, B+ trees for range scans
- **LSM-Trees:** Memtable, SSTables, compaction strategies (size-tiered, leveled), Bloom filters
- **Read and write amplification:** Trade-offs, workload characteristics
- **Production connection:** MySQL/InnoDB (B+ tree); Cassandra/RocksDB (LSM); choosing for write-heavy vs. read-heavy workloads

### 4.3 Distributed File Systems
- **GFS/HDFS:** Master-slave architecture, chunking, replication, append-only
- **Ceph:** RADOS, CRUSH algorithm, dynamic placement, self-healing
- **Object storage:** S3 API, consistency model, multipart upload, lifecycle policies
- **Production connection:** HDFS for batch ML training; Ceph for on-premise object storage; S3 as the universal storage layer

### 4.4 Distributed Databases
- **Key-value stores:** Dynamo (consistent hashing, vector clocks, hinted handoff), Riak, Voldemort
- **Wide-column stores:** Cassandra (gossip, anti-entropy, CQL), HBase
- **Document stores:** MongoDB (replica sets, sharding, transactions), Couchbase
- **Graph databases:** Neo4j clustering, JanusGraph (Cassandra + Elasticsearch)
- **NewSQL:** CockroachDB (Raft, serializable default), YugabyteDB, TiDB
- **Production connection:** DynamoDB for high-scale key-value; Cassandra for time-series; CockroachDB for distributed SQL; choosing based on consistency needs

### 4.5 Consistency Models
- **Linearizability:** Single-copy semantics, real-time ordering
- **Sequential consistency:** Program order preserved, no real-time guarantee
- **Causal consistency:** Causally related operations ordered, concurrent operations may diverge
- **Eventual consistency:** No ordering guarantees, convergence via anti-entropy
- **Read-your-writes, monotonic reads, bounded staleness:** Session guarantees
- **Production connection:** Spanner (external consistency = linearizability); DynamoDB (eventual + strong reads); choosing consistency for ML feature stores

### 4.6 Lab: Building a Distributed Key-Value Store
- **Task:** Build a Dynamo-like distributed key-value store
- **Requirements:**
  - Consistent hashing with virtual nodes
  - Replication with tunable consistency (ONE, QUORUM, ALL)
  - Hinted handoff and read repair
  - Gossip protocol for membership and failure detection
  - Vector clocks for conflict resolution
  - Benchmark: 100K ops/sec, <5ms P99 latency
- **Deliverable:** Working system in Go/Rust, Jepsen tests, consistency analysis under partitions

---

## Module 5: Distributed Messaging, Streaming, and Event-Driven Architecture

**Duration:** 25 hours  
**Level:** Advanced

### 5.1 Message Queue Fundamentals
- **Queue semantics:** FIFO, priority, delayed, dead letter
- **Point-to-point vs. pub/sub:** Direct queues, topic exchanges, fanout
- **Message guarantees:** At-most-once, at-least-once, exactly-once processing
- **Backpressure and flow control:** Consumer prefetch, rate limiting, credit-based flow control
- **Production connection:** RabbitMQ for task queues; SQS for cloud-native messaging; choosing based on durability needs

### 5.2 Log-Based Messaging — Kafka Deeply
- **Log abstraction:** Append-only, immutable, ordered partition
- **Partitioning:** Key-based partitioning, partition assignment, rebalancing
- **Replication:** ISR (In-Sync Replicas), leader election, min.insync.replicas
- **Consumer groups:** Group coordination, partition ownership, offset management
- **Exactly-once processing:** Idempotent producers, transactions, EOS semantics
- **Kafka internals:** Zero-copy `sendfile`, pagecache-centric design, compaction
- **Production connection:** Event sourcing architectures; ML feature logging; stream processing for real-time inference

### 5.3 Stream Processing
- **Stream-table duality:** Tables as materialized views of streams, streams as changelog of tables
- **Windowing:** Tumbling, hopping, session, global windows
- **Stateful processing:** Local state stores, changelog topics, state restoration
- **Frameworks:** Apache Flink (checkpointing, savepoints, exactly-once), Kafka Streams, Spark Streaming
- **Production connection:** Real-time feature computation; anomaly detection on streams; streaming ETL for ML pipelines

### 5.4 Event Sourcing and CQRS
- **Event sourcing:** State as reduction of events, event store, snapshotting
- **CQRS (Command Query Responsibility Segregation):** Separate read and write models
- **Materialized views:** Projections, eventual consistency, view rebuilds
- **Production connection:** Audit trails in financial systems; ML experiment tracking; recommendation system updates

### 5.5 Lab: Building a Streaming Platform
- **Task:** Build a Kafka-like log-based messaging system
- **Requirements:**
  - Append-only log with segment files
  - Topic partitioning with configurable replication
  - Producer acks (0, 1, all)
  - Consumer groups with offset management
  - Benchmark: 1M messages/sec ingestion, <100ms end-to-end latency
- **Deliverable:** Working system in Go/Rust, performance benchmarks, fault injection tests

---

## Module 6: Service Architecture — From Monolith to Mesh

**Duration:** 30 hours  
**Level:** Advanced

### 6.1 Monoliths, Microservices, and Modular Monoliths
- **Monolith advantages:** Simplicity, performance, transactional integrity, deployability
- **Microservices drivers:** Independent scaling, team autonomy, polyglot persistence
- **Modular monolith:** Domain boundaries within a deployable unit, migration path
- **Service decomposition strategies:** Domain-driven design, bounded contexts, aggregates
- **Production connection:** When to start with monolith (most cases); when to split (scaling or team constraints); Shopify's modular monolith

### 6.2 API Gateway and Edge Architecture
- **Gateway responsibilities:** Authentication, rate limiting, request routing, protocol translation
- **GraphQL federation:** Schema stitching, entity resolution, query planning
- **gRPC-Web and transcoding:** Binary protocols in browsers, Envoy filters
- **Production connection:** Kong/AWS API Gateway for REST; Apollo Federation for GraphQL; Envoy for gRPC transcoding

### 6.3 Service Mesh
- **Sidecar pattern:** Envoy, Linkerd, Istio — transparent proxying
- **Traffic management:** Canary, blue-green, A/B testing, traffic mirroring
- **Security:** mTLS, certificate rotation, identity-based access
- **Observability:** Automatic metrics, tracing, logging injection
- **Production connection:** Istio for Kubernetes; Linkerd for simplicity; service mesh for zero-trust microservices

### 6.4 Container Orchestration
- **Docker internals:** Namespaces, cgroups, union filesystems, container runtime (runc, crun)
- **Kubernetes architecture:** API server, etcd, scheduler, controller manager, kubelet, kube-proxy
- **Kubernetes abstractions:** Pods, Deployments, Services, Ingress, StatefulSets, DaemonSets
- **Scheduling:** Resource requests/limits, affinity/anti-affinity, taints/tolerations, priority/preemption
- **Production connection:** Kubernetes as the universal control plane; custom operators for ML workloads; GPU scheduling with device plugins

### 6.5 Serverless and FaaS
- **Function-as-a-Service:** AWS Lambda, Google Cloud Functions, Azure Functions
- **Cold start problem:** Initialization time, provisioned concurrency, snapstart
- **Serverless containers:** AWS Fargate, Google Cloud Run, Knative
- **Event-driven serverless:** Event sources, triggers, step functions
- **Production connection:** Lambda for lightweight ML inference; Cloud Run for containerized serving; serverless for cost optimization

### 6.6 Lab: Building a Service Mesh
- **Task:** Build a minimal service mesh with sidecar proxies
- **Requirements:**
  - Automatic sidecar injection (Kubernetes mutating webhook)
  - mTLS between services (certificate generation and rotation)
  - Traffic splitting (canary deployment)
  - Circuit breaker and retry logic
  - Distributed tracing header propagation
  - Metrics collection (Prometheus format)
- **Deliverable:** Working mesh in Go/Rust, demo application, security audit

---

## Module 7: Load Balancing, Traffic Management, and Edge Systems

**Duration:** 20 hours  
**Level:** Advanced

### 7.1 Load Balancing Algorithms
- **Static algorithms:** Round-robin, weighted round-robin, IP hash, random
- **Dynamic algorithms:** Least connections, least response time, consistent hashing
- **Consistent hashing:** Ring hash, jump consistent hash, rendezvous hashing, bounded loads
- **Load balancing layers:** DNS (global), L4 (transport), L7 (application), client-side
- **Production connection:** Maglev (Google) for L4; Envoy ring hash for sticky sessions; consistent hashing for cache sharding

### 7.2 Content Delivery and Edge Computing
- **CDN architecture:** Origin, edge PoPs, cache hierarchies, purge mechanisms
- **Edge computing:** Cloudflare Workers, Lambda@Edge, Vercel Edge Functions
- **Geographic routing:** Anycast, GeoDNS, latency-based routing
- **Production connection:** CDN for model artifact distribution; edge inference for low latency; geographic routing for compliance

### 7.3 Rate Limiting and Admission Control
- **Token bucket:** Algorithm, burst handling, implementation
- **Leaky bucket:** Traffic shaping vs. policing
- **Fixed/sliding window:** Counting-based approaches
- **Distributed rate limiting:** Redis cell, sliding window log, GCRA (Generic Cell Rate Algorithm)
- **Production connection:** API rate limiting; admission control during overload; distributed rate limiting for multi-region APIs

### 7.4 Lab: Building a Global Load Balancer
- **Task:** Build a DNS-based global load balancer
- **Requirements:**
  - Health check integration (HTTP/TCP)
  - Geographic routing with GeoIP
  - Latency-based routing (active measurements)
  - Consistent hashing for cache-friendly routing
  - Anycast simulation (or real deployment if possible)
  - Failover with sub-second detection
- **Deliverable:** Working system, performance under failure scenarios, comparison with commercial solutions

---

## Module 8: Observability, Reliability Engineering, and SRE

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 8.1 Metrics and Monitoring
- **Metric types:** Counters, gauges, histograms, summaries, exemplars
- **Cardinality explosion:** High-cardinality labels, aggregation strategies, recording rules
- **RED method:** Rate, Errors, Duration — for services
- **USE method:** Utilization, Saturation, Errors — for resources
- **Production connection:** Prometheus + Grafana as industry standard; custom metrics for ML serving; cardinality control for cost

### 8.2 Logging and Log Management
- **Structured logging:** JSON format, correlation IDs, trace context
- **Log levels:** DEBUG, INFO, WARN, ERROR, FATAL — semantic meaning
- **Log aggregation:** Fluentd/Fluent Bit, Logstash, cloud logging services
- **Log sampling:** Tail-based sampling, head-based sampling, dynamic sampling
- **Production connection:** Structured logging for queryable logs; correlation IDs for distributed tracing; log sampling for cost control

### 8.3 Distributed Tracing
- **Trace model:** Spans, traces, context propagation, baggage
- **Sampling strategies:** Head-based, tail-based, adaptive, probabilistic
- **OpenTelemetry:** Standardization, instrumentation, collectors, exporters
- **Trace analysis:** Critical path, latency attribution, dependency mapping
- **Production connection:** Jaeger/Zipkin for trace visualization; OpenTelemetry for vendor-neutral instrumentation; trace-driven optimization

### 8.4 Chaos Engineering
- **Principles:** Hypothesis-driven, blast radius control, automated rollback
- **Failure injection:** Network latency/packet loss, CPU/memory pressure, disk I/O errors, process kills, zone/region failures
- **Tools:** Chaos Monkey, Gremlin, Litmus, AWS Fault Injection Simulator
- **Game days:** Planned chaos experiments, team response validation
- **Production connection:** Netflix's Simian Army; chaos engineering for ML serving resilience; automated failure injection in CI

### 8.5 Site Reliability Engineering (SRE)
- **Error budgets:** Balancing reliability vs. velocity, SLOs, SLIs, SLAs
- **Incident management:** On-call rotation, severity classification, incident commander, communication
- **Post-mortems:** Blameless culture, five whys, action items, follow-up
- **Toil reduction:** Automation, self-healing systems, platform engineering
- **Production connection:** SRE for ML platforms; error budgets for model deployment velocity; on-call for distributed training infrastructure

### 8.6 Lab: Building an Observability Platform
- **Task:** Build a unified observability stack for a microservices system
- **Requirements:**
  - Metrics collection (Prometheus client library)
  - Structured logging with correlation IDs
  - Distributed tracing with OpenTelemetry
  - Alerting rules (Prometheus Alertmanager)
  - Dashboards (Grafana)
  - Log aggregation (Loki or ELK)
  - Chaos engineering integration (random failure injection)
- **Deliverable:** Working platform, demo with sample services, runbook for common alerts

---

## Module 9: Security, Identity, and Zero-Trust in Distributed Systems

**Duration:** 20 hours  
**Level:** Advanced

### 9.1 Threat Models for Distributed Systems
- **STRIDE:** Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege
- **Attack surfaces:** Network, APIs, data stores, supply chain, insider threats
- **ML-specific threats:** Model inversion, membership inference, data poisoning, adversarial examples
- **Production connection:** Threat modeling for ML serving APIs; supply chain security for model artifacts; insider threat detection

### 9.2 Authentication and Authorization
- **OAuth 2.0 and OpenID Connect:** Flows (authorization code, client credentials, device), tokens, JWT structure
- **mTLS:** Certificate-based authentication, mutual TLS in service meshes
- **SPIFFE/SPIRE:** Workload identity, automatic certificate provisioning
- **RBAC and ABAC:** Role-based vs. attribute-based access control
- **Production connection:** OAuth for user-facing APIs; mTLS for service-to-service; SPIFFE for zero-trust Kubernetes

### 9.3 Encryption and Data Protection
- **Encryption at rest:** AES-GCM, key management (HSM, KMS), envelope encryption
- **Encryption in transit:** TLS 1.3, certificate pinning, perfect forward secrecy
- **Homomorphic encryption:** Partially homomorphic, somewhat homomorphic, fully homomorphic — trade-offs
- **Differential privacy:** Privacy budget, mechanisms (Laplace, Gaussian), composition
- **Production connection:** KMS for model artifact encryption; TLS for all service communication; differential privacy for federated learning

### 9.4 Zero-Trust Architecture
- **Never trust, always verify:** Per-request authentication, least privilege, micro-segmentation
- **Identity-aware proxies:** BeyondCorp model, identity-aware access
- **Network segmentation:** Micro-segmentation, service mesh as security boundary
- **Production connection:** Google's BeyondCorp; zero-trust for multi-tenant ML platforms; identity-aware proxies for internal tools

### 9.5 Lab: Building a Zero-Trust Service Mesh
- **Task:** Implement zero-trust security for a microservices system
- **Requirements:**
  - Automatic mTLS with certificate rotation
  - JWT-based authentication with OAuth 2.0
  - Fine-grained authorization (RBAC + ABAC)
  - Network micro-segmentation
  - Audit logging for all access decisions
  - Integration with identity provider (Keycloak or Okta)
- **Deliverable:** Working system, security audit report, penetration testing results

---

## Module 10: ML Infrastructure — Distributed Training and Model Serving

**Duration:** 35 hours  
**Level:** Expert

### 10.1 Distributed Training Architectures
- **Data parallelism:** All-reduce, ring-allreduce, bucket-based communication
- **Model parallelism:** Pipeline parallelism (GPipe, PipeDream), tensor parallelism (Megatron-LM)
- **ZeRO (Zero Redundancy Optimizer):** Stage 1 (optimizer states), Stage 2 (gradients), Stage 3 (parameters)
- **FSDP (Fully Sharded Data Parallel):** PyTorch native, automatic sharding, backward prefetching
- **3D parallelism:** Data + tensor + pipeline parallelism combined
- **Production connection:** Training GPT-3 scale models; memory optimization for large models; choosing parallelism strategy based on model size and cluster topology

### 10.2 Collective Communication
- **MPI collectives:** `MPI_Allreduce`, `MPI_Bcast`, `MPI_Scatter`, `MPI_Gather`
- **NCCL (NVIDIA Collective Communications Library):** Optimized for GPU, tree and ring algorithms
- **Gloo:** CPU-optimized collectives, fallback for NCCL
- **RDMA for collectives:** GPUDirect RDMA, InfiniBand, NVLink
- **Production connection:** NCCL for GPU clusters; RDMA for minimizing CPU involvement; topology-aware collective scheduling

### 10.3 Training Orchestration
- **Job schedulers:** Kubernetes + device plugins, Slurm, MPI, Ray
- **Gang scheduling:** All-or-nothing allocation for distributed jobs
- **Elastic training:** Dynamic scaling, checkpoint/resume, fault tolerance
- **Checkpointing strategies:** Synchronous, asynchronous, incremental, distributed checkpointing (PyTorch DistributedCheckpoint)
- **Production connection:** Kubernetes for cloud training; Slurm for HPC clusters; elastic training for spot instance utilization

### 10.4 Model Serving at Scale
- **Batch inference:** Apache Spark, Ray, Dask — throughput optimization
- **Real-time inference:** REST/gRPC APIs, model warm-up, batching (dynamic batching, continuous batching)
- **Model compilation:** ONNX Runtime, TensorRT, TVM, XLA — graph optimization, kernel fusion
- **Quantization:** INT8, FP16, GPTQ, AWQ, SmoothQuant — accuracy vs. latency trade-offs
- **Production connection:** vLLM for LLM serving; TensorRT for CNN inference; quantization for edge deployment

### 10.5 Feature Stores and Online/Offline Consistency
- **Feature store architecture:** Online store (low-latency), offline store (batch), feature registry
- **Point-in-time correctness:** Avoiding leakage, temporal joins, event time processing
- **Feature monitoring:** Distribution drift, PSI, statistical tests
- **Production connection:** Feast/Tecton for feature management; point-in-time joins for training data; drift detection for model retraining triggers

### 10.6 Lab: Building a Distributed LLM Training Platform
- **Task:** Build a system for training large language models
- **Requirements:**
  - Distributed data parallelism with DDP or FSDP
  - Checkpointing to distributed storage (S3/MinIO)
  - Elastic training with spot instance handling
  - Monitoring: GPU utilization, memory, communication bandwidth
  - Fault tolerance: automatic restart on node failure
  - Scale: 8+ GPUs, billion-parameter model
- **Deliverable:** Working training pipeline, performance benchmarks (TFLOPS/GPU), fault injection tests, cost analysis

---

## Module 11: Emerging Frontiers — Serverless, WASM, Unikernels, and Beyond

**Duration:** 15 hours  
**Level:** Expert

### 11.1 WebAssembly (WASM) for Backend
- **WASM runtime:** Wasmer, Wasmtime, WasmEdge — sandboxing, near-native performance
- **WASI (WebAssembly System Interface):** Portable system interface, capability-based security
- **WASM in microservices:** Lightweight isolation, fast startup, polyglot modules
- **ML inference in WASM:** ONNX Runtime Web, TensorFlow.js, edge deployment
- **Production connection:** WASM for sandboxed plugins; edge inference with WASM; FaaS with WASM for cold start elimination

### 11.2 Unikernels and Library OS
- **Unikernel concept:** Single-address-space, library-based OS, minimal attack surface
- **Frameworks:** MirageOS (OCaml), IncludeOS (C++), Unikraft (C)
- **Trade-offs:** Performance vs. compatibility, debugging complexity, ecosystem maturity
- **Production connection:** Unikernels for high-density microservices; security-critical services; research systems

### 11.3 eBPF and Kernel Programming
- **eBPF architecture:** Verifier, JIT compiler, maps, helper functions
- **Use cases:** Observability (tcpdump, profiling), networking (XDP, TC), security (LSM hooks)
- **Cilium:** eBPF-based networking and security for Kubernetes
- **Production connection:** eBPF for high-performance load balancing; Cilium for Kubernetes networking; custom eBPF for ML data plane optimization

### 11.4 Custom Hardware and SmartNICs
- **SmartNICs:** BlueField, IPU, DPU — offloading networking, storage, security
- **FPGA acceleration:** Custom inference accelerators, reconfigurable computing
- **TPU/GPU clusters:** Pod architecture, optical interconnects, topology-aware scheduling
- **Production connection:** SmartNICs for storage offloading; FPGA for custom ML ops; TPU pods for training scale

### 11.5 Lab: Research Replication — eBPF-Based Load Balancer
- **Task:** Implement a layer-4 load balancer using eBPF/XDP
- **Requirements:**
  - XDP program for packet processing at NIC driver level
  - Consistent hashing for backend selection
  - Health check integration
  - Metrics export via eBPF maps
  - Benchmark: 10M packets/sec on single core
- **Deliverable:** Working eBPF program, performance report, comparison with IPVS

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Planet-Scale Distributed Database
- **Scope:** Build a CockroachDB/TiDB-like distributed SQL database
- **Components:**
  - Raft-based consensus for metadata
  - Distributed transactions with 2PC or Percolator
  - Range-based sharding with automatic rebalancing
  - SQL parser and query planner (subset)
  - Distributed execution engine
  - Online schema changes
- **Deliverables:** Working system, Jepsen tests, performance benchmarks, formal consistency analysis

### Capstone B: ML Training Supercomputer Scheduler
- **Scope:** Build a scheduler for large-scale distributed training
- **Components:**
  - Gang scheduling with resource constraints
  - Topology-aware placement (NVLink, InfiniBand)
  - Preemption and checkpointing
  - Elastic scaling with spot instances
  - Fair sharing between users/teams
  - Integration with Kubernetes or Slurm
- **Deliverables:** Working scheduler, simulation with realistic workloads, performance analysis, fairness evaluation

### Capstone C: Zero-Trust AI Serving Platform
- **Scope:** Build a secure, observable, multi-tenant model serving platform
- **Components:**
  - mTLS for all service communication
  - JWT-based authentication with fine-grained authorization
  - Model sandboxing (WASM or containers)
  - Distributed tracing and metrics
  - Rate limiting and admission control
  - A/B testing and canary deployments
  - Audit logging for compliance
- **Deliverables:** Working platform, security audit, performance benchmarks, compliance documentation

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 20% | Code quality, correctness, performance |
| Lab reports | 10% | Design decisions, profiling, formal arguments |
| Peer review | 10% | Reviewing others' systems and architecture docs |

### Examinations (30%)
- **Midterm (15%):** Consensus algorithms, storage systems, networking
- **Final (15%):** ML infrastructure, security, emerging systems, formal reasoning

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 10% |
| System design & architecture | 10% |
| Performance & scalability | 5% |
| Security & reliability | 3% |
| Documentation & presentation | 2% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel insights, production-ready, formal proofs
- **B (80-89):** Solid understanding, minor gaps, good engineering
- **C (70-79):** Adequate understanding, significant gaps, needs improvement
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding

---

## Recommended Tools, Libraries & Infrastructure

### Core Systems
| Tool | Purpose |
|------|---------|
| **Go** | Systems programming, networking, distributed systems |
| **Rust** | Memory-safe systems programming, high performance |
| **C/C++** | Kernel modules, eBPF, DPDK, low-level optimization |
| **Python** | Orchestration, ML frameworks, scripting |

### Networking and RPC
| Tool | Purpose |
|------|---------|
| **gRPC** | High-performance RPC |
| **Protobuf** | Binary serialization |
| **FlatBuffers** | Zero-copy deserialization |
| **Envoy** | L7 proxy, service mesh data plane |
| **Cilium** | eBPF-based networking |

### Consensus and Storage
| Tool | Purpose |
|------|---------|
| **etcd** | Distributed key-value store (Raft) |
| **Consul** | Service discovery, configuration |
| **ZooKeeper** | Coordination, locking |
| **CockroachDB** | Distributed SQL |
| **TiKV** | Distributed transactional key-value |
| **RocksDB** | Embedded key-value (LSM-tree) |

### Messaging and Streaming
| Tool | Purpose |
|------|---------|
| **Apache Kafka** | Distributed log |
| **Apache Flink** | Stream processing |
| **Apache Pulsar** | Tiered storage messaging |
| **Redis Streams** | Lightweight streaming |
| **NATS** | Lightweight pub/sub |

### Orchestration and Containers
| Tool | Purpose |
|------|---------|
| **Kubernetes** | Container orchestration |
| **Docker** | Container runtime |
| **Helm** | Kubernetes package manager |
| **Knative** | Serverless on Kubernetes |
| **Istio/Linkerd** | Service mesh |

### ML Infrastructure
| Tool | Purpose |
|------|---------|
| **PyTorch** | Deep learning framework |
| **Ray** | Distributed computing |
| **vLLM** | LLM serving |
| **TensorRT** | Optimized inference |
| **NCCL** | GPU collective communication |
| **MLflow** | Experiment tracking |

### Observability
| Tool | Purpose |
|------|---------|
| **Prometheus** | Metrics |
| **Grafana** | Visualization |
| **Jaeger** | Distributed tracing |
| **Loki** | Log aggregation |
| **OpenTelemetry** | Instrumentation standard |
| **Chaos Monkey/Gremlin** | Chaos engineering |

### Security
| Tool | Purpose |
|------|---------|
| **Vault** | Secrets management |
| **Keycloak/Okta** | Identity provider |
| **Cert-manager** | Certificate automation |
| **Falco** | Runtime security |
| **OPA (Open Policy Agent)** | Policy enforcement |

---

## References & Further Reading

### Distributed Systems Classics
1. **Tanenbaum & Van Steen,** *Distributed Systems: Principles and Paradigms* — Comprehensive textbook
2. **Coulouris et al.,** *Distributed Systems: Concepts and Design* — Another classic
3. **Lynch,** *Distributed Algorithms* — The definitive formal treatment
4. **Attiya & Welch,** *Distributed Computing: Fundamentals, Simulations, and Advanced Topics* — Formal approach
5. **van Steen & Tanenbaum,** *Distributed Systems* (3rd Ed., free online) — Modern, practical

### Consensus and Replication
1. **Lamport,** "The Part-Time Parliament" — Paxos original paper
2. **Ongaro & Ousterhout,** "In Search of an Understandable Consensus Algorithm" — Raft paper
3. **Castro & Liskov,** "Practical Byzantine Fault Tolerance" — PBFT paper
4. **Burrows,** "The Chubby Lock Service for Loosely-Coupled Distributed Systems" — Practical consensus

### Storage Systems
1. **DeCandia et al.,** "Dynamo: Amazon's Highly Available Key-value Store" — Dynamo paper
2. **Chang et al.,** "Bigtable: A Distributed Storage System for Structured Data" — Bigtable paper
3. **Corbett et al.,** "Spanner: Google's Globally-Distributed Database" — Spanner paper
4. **Lakshman & Malik,** "Cassandra: A Decentralized Structured Storage System" — Cassandra paper

### Messaging and Streaming
1. **Kreps et al.,** "Kafka: a Distributed Messaging System for Log Processing" — Kafka paper
2. **Akidau et al.,** "The Dataflow Model: A Practical Approach to Balancing Correctness, Latency, and Cost in Massive-Scale, Unbounded, Out-of-Order Data Processing" — Dataflow/Beam paper
3. **Carbone et al.,** "Apache Flink: Stream and Batch Processing in a Single Engine" — Flink paper

### Backend and Microservices
1. **Newman,** *Building Microservices* (2nd Ed.) — Practical microservices
2. **Richardson,** *Microservices Patterns* — Patterns catalog
3. **Fowler,** *Patterns of Enterprise Application Architecture* — Classic patterns
4. **Hohpe & Woolf,** *Enterprise Integration Patterns* — Messaging patterns

### ML Infrastructure
1. **Narayanan et al.,** "Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM" — Megatron paper
2. **Rajbhandari et al.,** "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models" — ZeRO paper
3. **Kwon et al.,** "Efficient Memory Management for Large Language Model Serving with PagedAttention" — vLLM paper
4. **Pope et al.,** "Efficiently Scaling Transformer Inference" — PaLM inference paper

### SRE and Reliability
1. **Beyer et al.,** *Site Reliability Engineering* (Google SRE book) — The SRE bible
2. **Beyer et al.,** *The Site Reliability Workbook* — Practical SRE
3. **Allspaw,** "Blameless PostMortems and a Just Culture" — Post-mortem culture

### Security
1. **Stallings & Brown,** *Computer Security: Principles and Practice* — Comprehensive security
2. **Bottum et al.,** *BeyondCorp* papers — Google's zero-trust architecture
3. **OWASP Top 10** — Web application security risks

---

## Appendix A: Formal Notation Reference

| Symbol | Meaning |
|--------|---------|
| $G = (V, E)$ | Graph of nodes and edges |
| $\rightarrow$ | Happens-before relation |
| $\sim$ | Concurrent (not ordered) |
| $\lfloor x \rfloor$ | Floor function |
| $\lceil x \rceil$ | Ceiling function |
| $O(f(n))$ | Big-O complexity |
| $\Omega(f(n))$ | Big-Omega complexity |
| $\Theta(f(n))$ | Big-Theta complexity |

## Appendix B: Latency Numbers Every Engineer Should Know

| Operation | Latency |
|-----------|---------|
| L1 cache reference | 0.5 ns |
| L2 cache reference | 7 ns |
| Main memory reference | 100 ns |
| SSD random read | 10 μs |
| NVMe random read | 1 μs |
| Datacenter round trip | 500 μs |
| Cross-region round trip | 50 ms |
| Cross-planet round trip | 250 ms |

*Source: Jeff Dean's "Numbers Everyone Should Know"*

## Appendix C: CAP Theorem Decision Matrix

| Requirement | CP System | AP System | Example |
|-------------|-----------|-----------|---------|
| Financial transactions | ✓ | | Spanner, CockroachDB |
| Social media feed | | ✓ | Cassandra, DynamoDB |
| Shopping cart | | ✓ | Dynamo (original) |
| Configuration management | ✓ | | etcd, Consul |
| Real-time analytics | | ✓ | Druid, ClickHouse |

## Appendix D: Production Checklist

Before deploying any distributed system to production, verify:

- [ ] **Correctness:** Unit tests, integration tests, Jepsen/chaos tests pass
- [ ] **Consistency:** Formal safety argument, known consistency model documented
- [ ] **Performance:** Benchmarked at scale, tail latency characterized
- [ ] **Reliability:** Fault injection tested, automatic recovery verified
- [ ] **Observability:** Metrics, logs, traces, alerts configured
- [ ] **Security:** Threat model, authentication, authorization, encryption verified
- [ ] **Scalability:** Horizontal scaling tested, capacity planning documented
- [ ] **Operability:** Runbooks, incident response, rollback procedures ready
- [ ] **Cost:** Resource utilization optimized, auto-scaling configured, TCO analyzed

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: distributed-systems-backend-syllabus.md