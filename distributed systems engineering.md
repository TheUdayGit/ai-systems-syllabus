  ## File: distributed-systems-engineering-syllabus.md

# Distributed Systems Engineering for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** System Design Advanced (or equivalent), Database Design (or equivalent), strong systems programming background (C/C++/Rust/Go), formal methods exposure, 5+ years production engineering experience  
**Estimated Duration:** 300–380 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: The Physics and Mathematics of Distributed Systems](#module-0-the-physics-and-mathematics-of-distributed-systems)
4. [Module 1: Formal Models, Consensus Theory, and Impossibility Results](#module-1-formal-models-consensus-theory-and-impossibility-results)
5. [Module 2: Clocks, Time, and Causality](#module-2-clocks-time-and-causality)
6. [Module 3: Replication — State Machine, Primary-Backup, and Quorum Systems](#module-3-replication--state-machine-primary-backup-and-quorum-systems)
7. [Module 4: Distributed Transactions and Atomic Commit](#module-4-distributed-transactions-and-atomic-commit)
8. [Module 5: Distributed Storage — From Filesystem to Database](#module-5-distributed-storage--from-filesystem-to-database)
9. [Module 6: Distributed Messaging and Stream Processing](#module-6-distributed-messaging-and-stream-processing)
10. [Module 7: Distributed Coordination, Locking, and Metadata](#module-7-distributed-coordination-locking-and-metadata)
11. [Module 8: Fault Tolerance, Recovery, and Chaos Engineering](#module-8-fault-tolerance-recovery-and-chaos-engineering)
12. [Module 9: Distributed ML and AI Infrastructure](#module-9-distributed-ml-and-ai-infrastructure)
13. [Module 10: Network Protocols, Kernel Bypass, and Custom Transports](#module-10-network-protocols-kernel-bypass-and-custom-transports)
14. [Module 11: Verification, Testing, and Correctness in Production](#module-11-verification-testing-and-correctness-in-production)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Distributed Systems Engineering** as a **foundational discipline of reliable computation across unreliable components**. The pedagogical approach follows a **Impossibility → Mechanism → Proof → System → Verification** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Impossibility** | FLP, CAP, two-generals, fundamental limits | Understanding of what cannot be done |
| **Mechanism** | Protocols, algorithms, data structures | Working implementations |
| **Proof** | Safety, liveness, invariants, TLA+ | Provable correctness |
| **System** | Storage, messaging, coordination, ML infrastructure | Production-grade platforms |
| **Verification** | Model checking, Jepsen, chaos engineering, formal methods | Confidence in correctness |

**Core Principles:**
- **You cannot build what you do not understand, and you cannot understand what you cannot prove.** We begin with impossibility results (FLP, CAP, Fischer-Lynch-Paterson) and derive all subsequent design decisions from these constraints.
- **The network is not a pipe — it is a hostile adversary.** We design for network partitions, message delays, clock skew, Byzantine failures, and correlated failures as the default case, not the exception.
- **State is the enemy of distributed systems.** We study stateless design, immutable data, CRDTs, and event sourcing as techniques for managing the complexity of distributed state.
- **Performance without correctness is not performance — it is corruption at speed.** We verify before we optimize. Every optimization must preserve the proven invariants.
- **ML infrastructure is distributed systems with tensor-shaped data.** Distributed training, model serving, and feature stores are not "ML problems" — they are distributed systems problems with specific consistency, latency, and throughput requirements.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Theoretical Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Prove impossibility results, derive protocols from first principles | Protocol design |
| **Expert** | Design new consensus protocols, prove safety and liveness formally | Research and platform engineering |
| **Distinguished** | Challenge fundamental assumptions, invent new models of distributed computation | Field-defining contributions |

### Implementation Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Implement Raft, Paxos, distributed transactions from scratch | Core infrastructure |
| **Expert** | Implement custom consensus, storage engines, messaging systems | Platform engineering |
| **Distinguished** | Build production systems handling 1B+ operations/day with formal correctness | Hyperscale infrastructure |

### Operational Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Debug distributed deadlocks, partition scenarios, consistency violations | SRE and platform |
| **Expert** | Design chaos engineering frameworks, automated verification pipelines | Reliability engineering |
| **Distinguished** | Define organizational standards for distributed systems correctness | Technical leadership |

### ML Infrastructure Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Design distributed training collectives, parameter servers, ring-allreduce | Production ML |
| **Expert** | Design custom collective communication, elastic training, model parallelism | AI supercomputing |
| **Distinguished** | Invent new distributed algorithms for ML workloads | Research engineering |

---

## Module 0: The Physics and Mathematics of Distributed Systems

**Duration:** 25 hours  
**Purpose:** Establish the physical and mathematical foundations that constrain all distributed systems

### 0.1 The Speed of Light and Latency Physics
- **Fundamental limits:** Minimum round-trip time between any two points on Earth (~67ms for antipodes)
- **Datacenter topology:** Clos networks, fat-trees, dragonfly, torus — diameter and bisection bandwidth
- **Optical vs. electrical signaling:** Propagation delay, dispersion, amplification, regeneration
- **Production connection:** Why synchronous replication across continents is physically impossible; why eventual consistency is not a choice but a law of physics

### 0.2 The CAP Theorem and Its Nuances
- **Original formulation:** Consistency, Availability, Partition tolerance — choose two
- **Formal proof:** Brewer's conjecture, Gilbert and Lynch proof, asynchronous vs. partially synchronous
- **PACELC:** If partitioned, choose Availability or Consistency; Else, choose Latency or Consistency
- **Practical implications:** What "choose two" actually means, why partition tolerance is not optional
- **Production connection:** Why Dynamo chose AP; why Spanner chose CP with TrueTime; why "CAP-theorem compliant" is meaningless marketing

### 0.3 The FLP Impossibility Result
- **The theorem:** Fischer, Lynch, Paterson — no deterministic consensus in asynchronous systems with even one faulty process
- **Proof sketch:** Adversarial scheduler, indistinguishability, bivalence argument
- **Implications:** Why timeouts are necessary, why partial synchrony is required, why randomization helps
- **Production connection:** Why Raft uses randomized timeouts; why leader election takes time; why "asynchronous consensus" is impossible without randomization or clocks

### 0.4 Partial Synchrony and System Models
- **Synchronous systems:** Known bounds on message delay and processing time
- **Asynchronous systems:** No bounds, FLP applies
- **Partial synchrony:** Bounds hold eventually, unknown when, Dwork-Lynch-Stockmeyer model
- **Failure models:** Crash-stop, crash-recovery, Byzantine, omission, timing
- **Production connection:** Why practical systems assume partial synchrony; why failure model choice determines protocol complexity

### 0.5 Probabilistic Methods in Distributed Systems
- **Randomization:** Ben-Or consensus, Rabin's common coin, randomized exponential backoff
- **Probabilistic quorum systems:** Load, availability, probe complexity trade-offs
- **Gossip protocols:** Epidemic dissemination, probabilistic guarantees, anti-entropy
- **Production connection:** Randomized consensus in blockchain; gossip for membership; probabilistic quorums for load balancing

### 0.6 Lab: Proving CAP and FLP
- **Task:** Write formal proofs of CAP and FLP
- **Requirements:**
  - Formal statement of CAP with proof sketch
  - Complete proof of FLP impossibility
  - Analysis of what breaks under each assumption relaxation
  - Implications for real-world system design
  - Document: when is synchronous consensus possible? When is it impossible?
- **Deliverable:** Formal proof document, presentation, peer review

---

## Module 1: Formal Models, Consensus Theory, and Impossibility Results

**Duration:** 35 hours  
**Level:** Expert

### 1.1 I/O Automata and Formal Models
- **I/O Automata:** States, actions, transitions, composition, hiding, fairness
- **Invariants and simulation relations:** Forward simulation, backward simulation, refinement mappings
- **Lynch's methodology:** Invariant assertion method, progress functions, timing-based proofs
- **Production connection:** Using I/O automata to model consensus protocols; proving correctness via simulation relations

### 1.2 Paxos Family of Protocols
- **Single-decree Paxos:** Proposers, acceptors, learners, ballot numbers, promise and accept messages
- **Multi-Paxos:** Leader election, log replication, catch-up, snapshotting
- **Fast Paxos:** Quorum intersection relaxation, fast path vs. slow path
- **Generalized Paxos:** Command structures, dependency tracking, commutative commands
- **Production connection:** Chubby (Multi-Paxos); ZooKeeper Zab (Paxos variant); understanding why Paxos is hard to implement correctly

### 1.3 Raft and Its Variants
- **Core Raft:** Leader election, log replication, safety, membership changes
- **Raft optimizations:** Pre-vote, checkquorum, joint consensus, single-server changes
- **Raft vs. Paxos:** Understandability trade-offs, performance comparison, implementation complexity
- **Production connection:** etcd (Raft); CockroachDB (Multi-Raft); why Raft won in practice despite Paxos's theoretical elegance

### 1.4 Byzantine Consensus
- **Byzantine Generals Problem:** Oral vs. signed messages, lower bounds (3f+1)
- **PBFT (Practical Byzantine Fault Tolerance):** Normal operation, view change, checkpointing, complexity
- **HotStuff:** Linear communication, chained consensus, responsiveness
- **Tendermint:** Bonded validators, block-based consensus, slashing conditions
- **Production connection:** Blockchain consensus (Ethereum, Cosmos); why BFT is 100x more expensive than crash-fault consensus; when BFT is worth it

### 1.5 Randomized and Leaderless Consensus
- **Ben-Or algorithm:** Exponential information gathering, random coin flips, expected rounds
- **HoneyBadgerBFT:** Asynchronous BFT, threshold encryption, batching
- **DAG-based consensus:** Narwhal/Tusk, Bullshark, asynchronous ordering without leaders
- **Production connection:** HoneyBadger for asynchronous BFT; DAG-based consensus for high-throughput blockchains; leaderless consensus for censorship resistance

### 1.6 Lab: Implementing and Verifying a Consensus Protocol
- **Task:** Implement Raft or HotStuff with formal verification
- **Requirements:**
  - Complete protocol implementation in Rust/Go
  - TLA+ specification of the protocol
  - Model checking with TLC for safety and liveness
  - Jepsen testing with network partitions and node failures
  - Performance benchmarking: latency under load, leader failover time
  - Formal proof of safety properties
- **Deliverable:** Working implementation, TLA+ spec, model checking results, Jepsen report, performance analysis

---

## Module 2: Clocks, Time, and Causality

**Duration:** 25 hours  
**Level:** Expert

### 2.1 Physical Clocks and Synchronization
- **Clock drift and skew:** Why physical clocks diverge, NTP fundamentals, precision limits
- **Clock synchronization protocols:** Cristian's algorithm, Berkeley algorithm, Marzullo's algorithm
- **GPS and atomic clocks:** Time sources, leap seconds, relativistic effects
- **Production connection:** Why NTP is insufficient for distributed transactions; why Spanner uses atomic clocks; GPS timing for financial systems

### 2.2 Logical Clocks
- **Lamport timestamps:** Happens-before relation, partial ordering, limitations
- **Vector clocks:** Full causality tracking, scalability limits, version vectors
- **Matrix clocks:** Transitive closure of causality, even higher overhead
- **Production connection:** Vector clocks in Riak, Voldemort; version vectors in distributed version control; why vector clocks don't scale beyond ~10 nodes

### 2.3 Hybrid Logical Clocks (HLC)
- **HLC design:** Physical clock + logical counter, causality tracking without coordination
- **Properties:** Bounded clock drift, self-stabilizing, no single point of failure
- **CockroachDB implementation:** Timestamp allocation, serializable transactions, clock uncertainty bounds
- **Production connection:** HLC in CockroachDB; why HLC enables serializable transactions without global locks; clock uncertainty and read refreshing

### 2.4 Causal Consistency and Causal Broadcast
- **Causal consistency:** Causally related operations ordered, concurrent operations may diverge
- **Causal broadcast:** Deliver messages in causal order, implementation strategies
- **Causal+ consistency:** Convergence under causality, read-your-writes, monotonic reads
- **Production connection:** Causal consistency in collaborative editing (Figma); causal broadcast in distributed messaging; why causal consistency is the strongest achievable without coordination

### 2.5 TrueTime and Spanner
- **TrueTime API:** TTinterval, TT.now(), TT.after(), uncertainty bounds
- **External consistency:** Linearizability with real-time ordering, commit wait
- **Clock synchronization:** GPS + atomic clocks, reference masters, daemon polling
- **Production connection:** Why Spanner's external consistency is unique; why commit wait adds ~7ms latency; when TrueTime is worth the cost

### 2.6 Lab: Implementing a Causality-Tracking System
- **Task:** Build a distributed system with causal consistency guarantees
- **Requirements:**
  - Implement vector clocks or HLC
  - Causal broadcast protocol
  - Read-your-writes and monotonic reads session guarantees
  - Conflict resolution for concurrent updates (last-writer-wins or custom merge)
  - Benchmark: causality tracking overhead vs. eventual consistency
  - Formal proof of causal consistency properties
- **Deliverable:** Working system, consistency tests, performance analysis, formal proof document

---

## Module 3: Replication — State Machine, Primary-Backup, and Quorum Systems

**Duration:** 30 hours  
**Level:** Expert

### 3.1 State Machine Replication (SMR)
- **Deterministic state machines:** Same inputs in same order → same outputs and same state
- **Total order broadcast:** Atomic broadcast, consensus equivalence, implementation
- **Replicated state machines:** Log replication, snapshotting, catch-up, reconfiguration
- **Production connection:** ZooKeeper as replicated state machine; etcd for Kubernetes; replicated logs in Kafka

### 3.2 Primary-Backup Replication
- **Synchronous replication:** Wait for all backups, strong consistency, high latency
- **Asynchronous replication:** Return after primary, fast, risk of data loss
- **Semi-synchronous:** Wait for at least one backup, balance of consistency and performance
- **Chain replication:** Ordered chain of replicas, quorum reads, head-tail optimization
- **Production connection:** MySQL semi-sync; PostgreSQL synchronous replication; chain replication in Ceph and HDFS

### 3.3 Quorum Systems
- **Majority quorums:** Read and write quorums intersect, ensuring consistency
- **Grid quorums:** 2-dimensional layout, read and write quorums
- **Probabilistic quorums:** Probabilistic intersection, load balancing, probe complexity
- **Weighted quorums:** Heterogeneous nodes, capacity-weighted voting
- **Production connection:** Dynamo's N, R, W configuration; Cassandra's tunable consistency; why R=1, W=N is CP

### 3.4 CRDTs and Conflict-Free Replicated Data Types
- **State-based CRDTs:** Join-semilattice, merge function, monotonicity, delta-state optimization
- **Operation-based CRDTs:** Causal delivery, unique identifiers, commutativity
- **CRDT variants:** Counters (G-Counter, PN-Counter), sets (G-Set, 2P-Set, OR-Set), maps, graphs, sequences
- **Production connection:** CRDTs in collaborative editing (Figma, Notion); Riak's CRDT support; Redis CRDTs; why CRDTs enable leaderless replication

### 3.5 Lab: Building a Replicated Key-Value Store
- **Task:** Build a replicated store with configurable consistency
- **Requirements:**
  - Primary-backup and quorum replication modes
  - Synchronous, asynchronous, and semi-synchronous options
  - Chain replication option
  - CRDT support for conflict resolution
  - Configurable read and write quorums
  - Jepsen testing for consistency violations
  - Benchmark: latency vs. consistency trade-off
- **Deliverable:** Working system, consistency analysis, performance benchmarks, Jepsen report

---

## Module 4: Distributed Transactions and Atomic Commit

**Duration:** 30 hours  
**Level:** Expert

### 4.1 Two-Phase Commit (2PC)
- **Protocol:** Prepare phase, commit phase, coordinator, participants, logs
- **Blocking problem:** Coordinator failure blocks participants, timeout uncertainty
- **Optimizations:** Presumed abort, presumed commit, read-only optimization
- **Production connection:** 2PC in distributed databases (CockroachDB, YugabyteDB); why 2PC is avoided in microservices; saga pattern as alternative

### 4.2 Three-Phase Commit (3PC)
- **Protocol:** CanCommit, PreCommit, DoCommit, non-blocking recovery
- **Limitations:** Network partitions break agreement, complexity, rarely used
- **Production connection:** Why 3PC is theoretical; why practical systems use 2PC with timeouts or alternative protocols

### 4.3 Percolator and Snapshot Isolation
- **Percolator design:** Timestamp oracle, prewrite, primary lock, commit, secondary locks
- **Snapshot isolation:** First-committer-wins, write skew, serializable snapshot isolation (SSI)
- **Lazy cleanup:** Asynchronous garbage collection of old versions
- **Production connection:** Percolator in Google Bigtable; TiDB's transaction model; why snapshot isolation is the sweet spot for distributed transactions

### 4.4 Calvin and Deterministic Databases
- **Calvin architecture:** Replication layer, scheduling layer, storage layer, deterministic locking
- **Deterministic execution:** Replicated inputs, no nondeterminism, no 2PC needed
- **Trade-offs:** Read scalability, replication overhead, transaction latency
- **Production connection:** FaunaDB (Calvin-inspired); why deterministic databases avoid 2PC; when deterministic execution is worth the complexity

### 4.5 Sagas and Compensating Transactions
- **Saga pattern:** Sequence of local transactions, compensating actions for rollback
- **Choreography:** Event-driven saga coordination, event listeners, decentralized
- **Orchestration:** Central saga coordinator, command-based, state machine
- **Production connection:** Saga for order→payment→inventory; choreography for loose coupling; orchestration for complex flows; why sagas are the microservices transaction pattern

### 4.6 Lab: Implementing a Distributed Transaction Manager
- **Task:** Build a transaction manager supporting multiple protocols
- **Requirements:**
  - 2PC implementation with coordinator recovery
  - Percolator-style snapshot isolation
  - Saga pattern with choreography and orchestration modes
  - Configurable isolation levels
  - Deadlock detection and timeout handling
  - Benchmark: throughput vs. latency vs. consistency
  - Jepsen testing for atomicity violations
- **Deliverable:** Working transaction manager, protocol comparison, performance analysis, correctness tests

---

## Module 5: Distributed Storage — From Filesystem to Database

**Duration:** 30 hours  
**Level:** Expert

### 5.1 Distributed File Systems
- **GFS/HDFS architecture:** Master-slave, chunking, replication, append-only, single master bottleneck
- **Ceph architecture:** RADOS, CRUSH algorithm, self-healing, no single point of failure
- **Erasure coding:** Reed-Solomon, LRC (Locally Repairable Codes), XOR-based, repair bandwidth
- **Production connection:** HDFS for batch analytics; Ceph for unified storage; erasure coding for cold storage cost reduction

### 5.2 Object Storage
- **S3 architecture:** Buckets, objects, keys, consistency model, multipart upload, lifecycle
- **MinIO/Ceph RGW:** S3-compatible, erasure coding, distributed, self-healing
- **Tiered storage:** Hot, warm, cold, glacier — automated lifecycle policies
- **Production connection:** S3 as the universal storage layer; MinIO for on-premise object storage; tiered storage for cost optimization

### 5.3 Distributed Block Storage
- **iSCSI, FC, NVMe-oF:** Protocols, performance, distance limitations
- **Distributed block stores:** Ceph RBD, Portworx, StorageOS — replication, snapshots, thin provisioning
- **Production connection:** Ceph RBD for VM storage; Portworx for Kubernetes persistent volumes; NVMe-oF for low-latency remote storage

### 5.4 Distributed SQL and NewSQL
- **CockroachDB:** Multi-raft, serializable default, cost-based optimizer, follower reads
- **YugabyteDB:** DocDB storage, YSQL/YCQL, Raft groups, distributed transactions
- **TiDB:** TiKV (Raft), TiFlash (columnar), HTAP, Spark integration
- **Google Spanner:** TrueTime, external consistency, global distribution, F1 frontend
- **Production connection:** Choosing between CockroachDB, YugabyteDB, TiDB, Spanner based on requirements and budget

### 5.5 Lab: Building a Distributed Storage System
- **Task:** Build a distributed object store with erasure coding
- **Requirements:**
  - S3-compatible API (subset: PUT, GET, DELETE, LIST)
  - Reed-Solomon erasure coding (configurable m+n)
  - Distributed metadata with Raft consensus
  - Data placement with CRUSH-like algorithm
  - Self-healing on node failure
  - Benchmark: throughput, latency, repair bandwidth
  - Compare with MinIO and Ceph
- **Deliverable:** Working object store, erasure coding analysis, performance benchmarks, failure recovery tests

---

## Module 6: Distributed Messaging and Stream Processing

**Duration:** 25 hours  
**Level:** Expert

### 6.1 Log-Based Messaging Deeply
- **Kafka internals:** Zero-copy `sendfile`, pagecache-centric design, segment files, compaction
- **Replication details:** ISR management, leader election, min.insync.replicas, unclean leader election
- **Consumer group mechanics:** Rebalance protocol, partition assignment strategies, offset management
- **Exactly-once semantics:** Idempotent producers, transactions, EOS, limitations
- **Production connection:** Kafka as the central nervous system; why pagecache design matters; exactly-once as "exactly-once processing" not delivery

### 6.2 Stream Processing Frameworks
- **Apache Flink:** Checkpointing, savepoints, exactly-once, state backends, watermarking
- **Kafka Streams:** Embedded processing, state stores, changelog topics, interactive queries
- **Spark Structured Streaming:** Micro-batch, continuous processing, watermarking, state store
- **Comparison:** Latency, throughput, state management, fault tolerance, operational complexity
- **Production connection:** Flink for complex event processing; Kafka Streams for simple transformations; Spark for batch+stream unification

### 6.3 Event Sourcing and CQRS at Scale
- **Event store design:** Stream ID, event type, payload, metadata, sequence number, timestamp
- **Projection engines:** Read model builders, eventual consistency, view rebuilds
- **Snapshotting:** Snapshot store, snapshot frequency, state restoration optimization
- **Production connection:** Event sourcing for audit trails; CQRS for read-heavy systems; why event stores are append-only logs

### 6.4 Lab: Building a Distributed Stream Processor
- **Task:** Build a minimal stream processing engine
- **Requirements:**
  - Kafka-like log abstraction with partitions
  - Stateful processing with local state stores
  - Checkpointing for fault tolerance
  - At-least-once and exactly-once semantics
  - Windowing: tumbling, hopping, session
  - Benchmark: 100K events/sec, <100ms processing latency
  - Compare with Kafka Streams and Flink
- **Deliverable:** Working stream processor, state management analysis, fault tolerance tests, performance benchmarks

---

## Module 7: Distributed Coordination, Locking, and Metadata

**Duration:** 20 hours  
**Level:** Expert

### 7.1 Distributed Locking
- **Chubby:** Paxos-based locking, coarse-grained, sessions, keepalives, caching
- **Redis RedLock:** Multi-master locking, clock drift sensitivity, controversy
- **ZooKeeper locks:** Ephemeral sequential nodes, herd effect, watch optimization
- **Lease-based locking:** Timeout, automatic expiration, fencing tokens
- **Production connection:** Chubby for Google internal locking; ZooKeeper for Hadoop ecosystem; why distributed locks are hard and often unnecessary

### 7.2 Leader Election and Membership
- **Bully algorithm:** Process IDs, message complexity, failure sensitivity
- **Ring algorithm:** Token passing, unidirectional ring, fault tolerance
- **Gossip-based membership:** SWIM protocol, failure detection, dissemination
- **Production connection:** etcd for Kubernetes leader election; Consul for service mesh membership; SWIM in HashiCorp products

### 7.3 Distributed Configuration and Metadata
- **etcd:** Raft-backed key-value, watches, transactions, leases
- **ZooKeeper:** ZAB protocol, znodes, watches, ephemeral nodes, sequential nodes
- **Consul:** Raft + gossip, service discovery, health checking, KV store
- **Production connection:** etcd as Kubernetes brain; ZooKeeper for Kafka and Hadoop; Consul for multi-cloud service discovery

### 7.4 Lab: Building a Distributed Coordination Service
- **Task:** Build a ZooKeeper-like coordination service
- **Requirements:**
  - Hierarchical namespace (znodes)
  - Watches for change notification
  - Ephemeral and sequential nodes
  - Distributed locking with fencing tokens
  - Leader election
  - Configuration management
  - Benchmark: 50K operations/sec, <10ms watch latency
- **Deliverable:** Working coordination service, correctness tests, performance benchmarks, comparison with ZooKeeper

---

## Module 8: Fault Tolerance, Recovery, and Chaos Engineering

**Duration:** 25 hours  
**Level:** Expert

### 8.1 Failure Taxonomy and Detection
- **Failure modes:** Crash-stop, crash-recovery, omission, timing, Byzantine
- **Failure detectors:** Perfect, eventually perfect, unreliable, Phi accrual
- **Correlated failures:** Shared fate, blast radius, zone/region failures, maintenance windows
- **Production connection:** Phi accrual in Cassandra; why correlated failures dominate availability; zone design for blast radius containment

### 8.2 Checkpointing and Recovery
- **Coordinated checkpointing:** Global consistent state, domino effect, latency
- **Uncoordinated checkpointing:** Independent checkpoints, orphan messages, message logging
- **Incremental checkpointing:** Delta checkpoints, log-based, copy-on-write
- **Production connection:** Flink checkpointing; database PITR; why incremental checkpointing is essential for large state

### 8.3 Replication for Disaster Recovery
- **RTO and RPO:** Recovery Time Objective, Recovery Point Objective, trade-offs
- **Cross-region replication:** Synchronous, asynchronous, semi-synchronous, quorum-based
- **Failover automation:** Health checks, decision logic, split-brain prevention, failback
- **Production connection:** RTO/RPO for financial systems (<1 minute / 0); cross-region replication costs; automated failover risks

### 8.4 Chaos Engineering
- **Principles:** Hypothesis-driven, blast radius control, production experimentation
- **Failure injection:** Network latency, partition, CPU pressure, memory pressure, disk failure, zone failure
- **Game days:** Planned experiments, team response, post-mortem
- **Tools:** Chaos Monkey, Gremlin, Litmus, AWS Fault Injection Simulator, ChaoSlingr
- **Production connection:** Netflix's Simian Army; chaos engineering for ML serving; automated chaos in CI/CD pipelines

### 8.5 Lab: Chaos Engineering a Distributed System
- **Task:** Design and execute chaos experiments on a distributed system
- **Requirements:**
  - Define steady-state hypothesis
  - Design 5+ chaos experiments (network, CPU, memory, disk, zone)
  - Measure blast radius and recovery time
  - Identify and fix weaknesses discovered
  - Automate experiments in CI/CD
  - Document findings and remediation
  - Target: <5% availability impact during experiments
- **Deliverable:** Chaos engineering plan, experiment results, remediation actions, automated pipeline, post-mortem

---

## Module 9: Distributed ML and AI Infrastructure

**Duration:** 30 hours  
**Level:** Expert

### 9.1 Distributed Training Architectures
- **Parameter servers:** Centralized, asynchronous, stale gradients, convergence
- **All-reduce:** Ring-allreduce, tree-allreduce, bucket-based, recursive halving and doubling
- **Gossip averaging:** Decentralized, asynchronous, convergence guarantees
- **Pipeline parallelism:** GPipe, PipeDream, bubble optimization, schedule variants
- **Production connection:** Why all-reduce dominates; why parameter servers fail at scale; pipeline parallelism for large models

### 9.2 Collective Communication Optimization
- **MPI collectives:** All-reduce, all-gather, all-to-all, broadcast, reduce-scatter
- **NCCL:** GPU-optimized, tree and ring algorithms, topology-aware scheduling
- **RDMA for collectives:** GPUDirect RDMA, InfiniBand, NVLink, CXL
- **Gradient compression:** Quantization, sparsification, error feedback, local steps
- **Production connection:** NCCL for GPU clusters; RDMA for minimizing CPU involvement; gradient compression for bandwidth-limited training

### 9.3 Elastic and Fault-Tolerant Training
- **Elastic training:** Dynamic scaling, checkpoint/resume, spot instance handling
- **Fault tolerance:** Automatic restart, elastic checkpointing, straggler mitigation
- **Data parallelism at scale:** Sharding, loading, preprocessing, pipeline optimization
- **Production connection:** Elastic training for cost reduction; automatic restart for long-running jobs; straggler mitigation for synchronous training

### 9.4 Distributed Inference and Model Serving
- **Model parallelism:** Tensor parallelism, pipeline parallelism, expert parallelism (MoE)
- **Speculative decoding:** Draft model, acceptance criteria, tree-based speculation
- **Continuous batching:** In-flight batching, iteration-level scheduling, KV-cache management
- **Production connection:** vLLM for LLM serving; continuous batching for throughput; speculative decoding for latency; MoE for cost efficiency

### 9.5 Lab: Building a Distributed Training Framework
- **Task:** Build a minimal distributed training system
- **Requirements:**
  - Ring-allreduce implementation
  - Data parallelism with DDP-like semantics
  - Checkpointing and elastic restart
  - Fault tolerance (automatic recovery from node failure)
  - Integration with PyTorch or JAX
  - Scale: 8+ GPUs, ResNet-50 or GPT-2 training
  - Benchmark: throughput (images/sec or tokens/sec), scaling efficiency
- **Deliverable:** Working framework, scaling analysis, fault tolerance tests, performance benchmarks

---

## Module 10: Network Protocols, Kernel Bypass, and Custom Transports

**Duration:** 25 hours  
**Level:** Expert

### 10.1 RDMA and High-Performance Networking
- **InfiniBand:** Queue pairs, send/receive, RDMA read/write, atomic operations
- **RoCE (RDMA over Converged Ethernet):** v1/v2, PFC, ECN, congestion control
- **GPUDirect RDMA:** GPU memory access from NIC, zero-copy, CPU bypass
- **CXL (Compute Express Link):** Memory pooling, cache coherency, composable systems
- **Production connection:** InfiniBand for AI supercomputers; RoCE for data center RDMA; GPUDirect for distributed training; CXL for disaggregated memory

### 10.2 DPDK and Userspace Networking
- **DPDK architecture:** Poll-mode drivers, huge pages, core pinning, NUMA awareness
- **Packet processing pipeline:** RX burst, classification, processing, TX burst
- **AF_XDP:** Express Data Path, zero-copy, BPF program for steering
- **Production connection:** DPDK for custom load balancers; AF_XDP for high-throughput packet processing; userspace TCP for 10M+ connections

### 10.3 Custom Transport Protocols
- **Reliable UDP:** QUIC, RUDP, custom protocols — design considerations
- **Congestion control customization:** BBR, COPA, HPCC, data center TCP variants
- **Message-oriented middleware:** ZeroMQ, Nanomsg, custom protocols — patterns and anti-patterns
- **Production connection:** QUIC for HTTP/3; custom congestion control for RDMA; ZeroMQ for high-frequency trading

### 10.4 Lab: Building a Custom Transport for AI Workloads
- **Task:** Design a transport protocol optimized for distributed training
- **Requirements:**
  - Reliable ordered delivery
  - Congestion control optimized for bursty all-reduce traffic
  - RDMA integration for zero-copy
  - GPU-direct support
  - Fault tolerance (automatic reconnection)
  - Benchmark vs. TCP and MPI over InfiniBand
  - Measure: throughput, latency, CPU overhead
- **Deliverable:** Working transport, performance comparison, congestion control analysis, integration with NCCL or MPI

---

## Module 11: Verification, Testing, and Correctness in Production

**Duration:** 20 hours  
**Level:** Expert → Distinguished

### 11.1 Model Checking Distributed Systems
- **TLA+ for distributed systems:** Specifying consensus, replication, transactions
- **Property specification:** Safety (invariants), liveness (eventually), fairness
- **State space exploration:** Explicit state, symbolic, bounded model checking
- **Counterexample analysis:** Understanding failures, fixing bugs, refining specs
- **Production connection:** Amazon's use of TLA+ for AWS; Microsoft use for Azure; why model checking finds bugs testing cannot

### 11.2 Jepsen Testing
- **Jepsen framework:** Linearizability checking, operation history analysis, Knossos
- **Test design:** Workload generation, failure injection, consistency verification
- **Consistency models:** Linearizability, serializability, snapshot isolation, causal consistency
- **Production connection:** Jepsen testing for database releases; why every distributed database needs Jepsen; interpreting Jepsen reports

### 11.3 Lineage-Driven Fault Injection
- **Lineage:** Data provenance, why questions, fault explanation
- **Fault injection based on lineage:** Targeted failures, minimal bug reproduction
- **Molly:** Lineage-driven fault injection tool, counterexamples, explanations
- **Production connection:** Lineage for debugging complex failures; targeted fault injection for rare bugs; explaining "why" not just "what"

### 11.4 Runtime Verification and Monitoring
- **Invariant monitoring:** Runtime assertion checking, temporal logic monitoring
- **Distributed tracing for verification:** Trace analysis, anomaly detection, consistency checking
- **Self-verifying systems:** Systems that check their own correctness properties
- **Production connection:** Runtime verification for critical invariants; trace-based consistency checking; self-healing systems

### 11.5 Lab: Verifying a Distributed System
- **Task:** Apply multiple verification techniques to a distributed system
- **Requirements:**
  - Write TLA+ specification for a component (consensus, replication, or transactions)
  - Model check with TLC and analyze counterexamples
  - Design Jepsen test suite with workload and failure injection
  - Run Jepsen tests and analyze results
  - Implement runtime invariant checking
  - Document verification coverage and remaining risks
- **Deliverable:** TLA+ spec, model checking results, Jepsen test suite, runtime verification code, verification report

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Planet-Scale Distributed Database
- **Scope:** Build a CockroachDB/Spanner-class distributed SQL database
- **Components:**
  - Multi-Raft consensus for range replication
  - Distributed transaction support (Percolator-style or 2PC)
  - Cost-based query optimizer
  - Automatic range splitting and rebalancing
  - Follower reads and bounded staleness
  - Online schema changes
  - Global deployment with data residency
  - TLA+ specification for core protocols
  - Jepsen testing for consistency
- **Deliverables:** Working system, formal specifications, Jepsen report, performance benchmarks, architecture document

### Capstone B: Distributed ML Training Supercomputer
- **Scope:** Build a distributed training system for exascale models
- **Components:**
  - Custom collective communication (all-reduce, all-gather, all-to-all)
  - 3D parallelism (data + tensor + pipeline)
  - Elastic training with spot instance handling
  - Topology-aware scheduling
  - Checkpointing to distributed storage
  - Automatic fault recovery
  - Custom transport protocol optimized for AI workloads
  - Integration with PyTorch or JAX
  - Scale: 1000+ GPUs, 1T+ parameter model
- **Deliverables:** Working system, scaling analysis, fault tolerance tests, performance benchmarks (TFLOPS/GPU), cost analysis

### Capstone C: Verified Distributed System
- **Scope:** Build a distributed system with formal verification of core properties
- **Components:**
  - Complete TLA+ specification of the system
  - Model checking of all safety and liveness properties
  - Jepsen testing with comprehensive failure injection
  - Runtime invariant checking
  - Lineage-driven fault injection
  - Chaos engineering integration
  - Performance comparable to unverified systems
  - Documentation of verification coverage and trust boundaries
- **Deliverables:** Working system, formal proofs, Jepsen report, chaos engineering results, verification document

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 15% | Working distributed systems from scratch |
| Formal specifications | 15% | TLA+ specs, proof sketches, model checking |
| Peer review | 10% | Reviewing others' systems and proofs |

### Examinations (30%)
- **Midterm (15%):** Consensus theory, replication, transactions, clocks
- **Final (15%):** Distributed storage, ML infrastructure, verification, emerging topics

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 10% |
| Formal verification | 8% |
| Performance & scalability | 5% |
| Documentation & presentation | 4% |
| Novel contribution | 3% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel protocols, formally verified, production-ready
- **B (80-89):** Excellent understanding, minor gaps, strong implementation
- **C (70-79):** Good understanding, significant gaps in formal methods or advanced topics
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding for expert-level distributed systems engineering

---

## Recommended Tools, Libraries & Infrastructure

### Formal Methods
| Tool | Purpose |
|------|---------|
| **TLA+ / PlusCal** | Formal specification |
| **TLC** | Model checker |
| **Apalache** | Symbolic model checker |
| **Coq / Isabelle** | Theorem proving |

### Distributed Systems
| Tool | Purpose |
|------|---------|
| **etcd** | Distributed key-value store |
| **ZooKeeper** | Coordination service |
| **Consul** | Service discovery |
| **Kafka** | Event streaming |
| **CockroachDB** | Distributed SQL |
| **TiKV** | Distributed transactional KV |

### Networking
| Tool | Purpose |
|------|---------|
| **DPDK** | Kernel bypass |
| **RDMA / libibverbs** | Remote memory access |
| **eBPF / BCC** | Kernel programming |
| **QUIC / quiche** | Modern transport |

### ML Infrastructure
| Tool | Purpose |
|------|---------|
| **NCCL** | GPU collectives |
| **Ray** | Distributed computing |
| **DeepSpeed** | Microsoft training |
| **Megatron-LM** | NVIDIA large models |
| **vLLM** | LLM serving |

### Testing
| Tool | Purpose |
|------|---------|
| **Jepsen** | Distributed correctness |
| **Chaos Monkey** | Failure injection |
| **Gremlin** | Chaos engineering |
| **Litmus** | Kubernetes chaos |

---

## References & Further Reading

### Foundational Papers
1. **Fischer, Lynch, Paterson,** "Impossibility of Distributed Consensus with One Faulty Process" — FLP
2. **Lamport,** "The Part-Time Parliament" — Paxos
3. **Ongaro & Ousterhout,** "In Search of an Understandable Consensus Algorithm" — Raft
4. **Gilbert & Lynch,** "Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services" — CAP proof

### Consensus and Replication
1. **Castro & Liskov,** "Practical Byzantine Fault Tolerance" — PBFT
2. **Yin et al.,** "HotStuff: BFT Consensus in the Lens of Blockchain" — HotStuff
3. **Lamport,** "Fast Paxos" — Fast Paxos

### Clocks and Causality
1. **Lamport,** "Time, Clocks, and the Ordering of Events in a Distributed System" — Logical clocks
2. **Kulkarni et al.,** "Logical Physical Clocks and Consistent Snapshots in Distributed Systems" — HLC
3. **Corbett et al.,** "Spanner: Google's Globally-Distributed Database" — TrueTime

### Transactions
1. **Percolator paper** — Google's distributed transactions
2. **Thomson et al.,** "Calvin: Fast Distributed Transactions for Partitioned Database Systems" — Calvin
3. **Garcia-Molina & Salem,** "Sagas" — Saga pattern

### Distributed ML
1. **Li et al.,** "Parameter Server for Distributed Machine Learning" — Parameter servers
2. **Rabenseifner,** "Optimization of Collective Reduction Operations" — All-reduce
3. **Narayanan et al.,** "Efficient Large-Scale Language Model Training on GPU Clusters" — Megatron

### Verification
1. **Newcombe et al.,** "How Amazon Web Services Uses Formal Methods" — TLA+ at AWS
2. **Kingsbury,** Jepsen analyses — Distributed database testing
3. **Alvaro et al.,** "Lineage-Driven Fault Injection" — Molly

---

## Appendix A: System Model Taxonomy

| Property | Options |
|----------|---------|
| Timing | Synchronous / Asynchronous / Partially synchronous |
| Failure | Crash-stop / Crash-recovery / Byzantine / Omission |
| Network | Reliable / Fair-loss / Arbitrary / Partitionable |
| Clocks | Synchronized / Bounded drift / Unsynchronized |
| Message delay | Bounded / Unbounded / Unknown bound |

## Appendix B: Consensus Protocol Comparison

| Protocol | Messages per decision | Fault tolerance | Timing assumption | Complexity |
|----------|----------------------|-----------------|-------------------|------------|
| Paxos | O(n²) | 2f+1 | Partial sync | High |
| Raft | O(n) | 2f+1 | Partial sync | Medium |
| PBFT | O(n²) | 3f+1 | Partial sync | Very high |
| HotStuff | O(n) | 3f+1 | Partial sync | Medium |
| Ben-Or | O(2^n) expected | 2f+1 | Async | Medium |

## Appendix C: Verification Checklist

Before claiming a distributed system is correct, verify:

- [ ] **Specification:** TLA+ or equivalent specification exists
- [ ] **Safety:** All safety invariants stated and checked
- [ ] **Liveness:** All liveness properties stated and checked
- [ ] **Model checking:** TLC or equivalent has explored state space
- [ ] **Jepsen:** Linearizability or target consistency model verified
- [ ] **Chaos:** Failure injection tests pass
- [ ] **Lineage:** Can explain why any output was produced
- [ ] **Review:** Peer review by distributed systems expert

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: distributed-systems-engineering-syllabus.md