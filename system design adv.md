  
   ## File: system-design-advanced-syllabus.md

# System Design Advanced for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** System Design Foundations (or equivalent), Distributed Systems & Backend Engineering (or equivalent), Database Design (or equivalent), 5+ years production engineering experience  
**Estimated Duration:** 280–350 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: First Principles at Scale — Formal Methods, Economics, and Organizational Architecture](#module-0-first-principles-at-scale--formal-methods-economics-and-organizational-architecture)
4. [Module 1: Planet-Scale Distributed Systems](#module-1-planet-scale-distributed-systems)
5. [Module 2: Custom Protocol Design and Kernel Bypass](#module-2-custom-protocol-design-and-kernel-bypass)
6. [Module 3: Advanced Consensus, Replication, and Byzantine Fault Tolerance](#module-3-advanced-consensus-replication-and-byzantine-fault-tolerance)
7. [Module 4: Custom Storage Engines and Learned Indexes](#module-4-custom-storage-engines-and-learned-indexes)
8. [Module 5: Advanced Caching — Coherence, Consistency, and Custom Eviction](#module-5-advanced-caching--coherence-consistency-and-custom-eviction)
9. [Module 6: Custom Load Balancers, Proxies, and Traffic Engineering](#module-6-custom-load-balancers-proxies-and-traffic-engineering)
10. [Module 7: AI/ML Platform Architecture — Training Supercomputers and Inference at Scale](#module-7-aiml-platform-architecture--training-supercomputers-and-inference-at-scale)
11. [Module 8: LLM Infrastructure — Distributed Serving, Speculative Decoding, and Multi-Modal Pipelines](#module-8-llm-infrastructure--distributed-serving-speculative-decoding-and-multi-modal-pipelines)
12. [Module 9: Security Architecture — Formal Verification, Zero-Knowledge, and Post-Quantum](#module-9-security-architecture--formal-verification-zero-knowledge-and-post-quantum)
13. [Module 10: Organizational Scaling — Platform Engineering, RFC Culture, and Technical Strategy](#module-10-organizational-scaling--platform-engineering-rfc-culture-and-technical-strategy)
14. [Module 11: Emerging Frontiers — Photonic Computing, Neuromorphic Systems, and Beyond](#module-11-emerging-frontiers--photonic-computing-neuromorphic-systems-and-beyond)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Advanced System Design** as a **discipline of engineering judgment at the limits of physics, economics, and organizational complexity**. The pedagogical approach follows a **Formal → Physical → Economic → Organizational → Evolutionary** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Formal** | Proof sketches, model checking, TLA+, invariants | Provable correctness |
| **Physical** | Speed of light, thermodynamics, quantum limits | Physics-grounded constraints |
| **Economic** | Marginal cost, TCO, opportunity cost, technical debt valuation | Rational investment |
| **Organizational** | Conway's Law, platform teams, RFC culture, technical strategy | Sustainable scaling |
| **Evolutionary** | Deprecation, migration, technical debt amortization, succession planning | Long-term viability |

**Core Principles:**
- **At staff+ level, correctness is not enough — you must prove it.** We use TLA+ to model consensus protocols, model checking to verify cache coherence, and formal invariants to reason about distributed state machines.
- **Physics is the ultimate constraint.** Speed of light limits cross-region latency. Landauer's principle limits computation energy. Quantum tunneling limits transistor scaling. Every design must account for these hard boundaries.
- **Economics is the ultimate arbiter.** A technically superior design that costs 10x more is not superior. We teach marginal analysis, TCO modeling, and technical debt valuation as core engineering skills.
- **Organizations are systems too.** A perfect architecture fails if the organization cannot operate it. We study platform engineering, team topologies, and technical strategy as first-class design inputs.
- **The future is not an extrapolation of the present.** We study emerging technologies — photonic interconnects, neuromorphic computing, quantum-safe cryptography — not as curiosities, but as potential disruptions that reshape architectural assumptions.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Formal Methods Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | Write TLA+ specs for simple protocols, understand invariants | Design review validation |
| **Advanced** | Model check distributed algorithms, prove safety and liveness | Protocol design |
| **Expert** | Design custom formal methods, verify production systems, teach formal reasoning | Platform engineering |

### Planet-Scale System Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Design multi-region systems with sub-100ms latency, handle 1B+ users | Hyperscale platforms |
| **Expert** | Design systems for 10B+ users, custom hardware, planetary scale | Infrastructure platforms |

### AI/ML Infrastructure Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Design distributed training for 1000+ GPUs, inference at 1M+ QPS | Production ML platforms |
| **Expert** | Design training supercomputers, custom inference accelerators, AI-native systems | AI supercomputing |

### Organizational Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Advanced** | Lead platform engineering teams, define technical strategy, mentor staff engineers | Staff+ engineering |
| **Expert** | Define organizational architecture, shape engineering culture, drive technical vision | Principal/Distinguished |

### Cross-Cutting Competencies
- **Formal reasoning:** Prove correctness of distributed protocols using TLA+ or equivalent
- **Physical reasoning:** Derive latency and energy bounds from first principles
- **Economic reasoning:** Model TCO, ROI, and technical debt for architectural decisions
- **Strategic reasoning:** Align technical architecture with business strategy over 5-year horizons

---

## Module 0: First Principles at Scale — Formal Methods, Economics, and Organizational Architecture

**Duration:** 25 hours  
**Purpose:** Establish the advanced reasoning frameworks that distinguish staff+ engineers from senior engineers

### 0.1 Formal Methods for System Design
- **TLA+ (Temporal Logic of Actions):** States, actions, invariants, liveness properties, fairness
- **Model checking:** State space exploration, counterexamples, state explosion problem
- **PlusCal:** Algorithm language for TLA+, processes, atomic blocks, await
- **Practical TLA+:** Specifying consensus, cache coherence, distributed transactions
- **Production connection:** Using TLA+ to verify Raft implementation; specifying cache invalidation protocols; Amazon's use of TLA+ for AWS services

### 0.2 The Physics of Planet-Scale Systems
- **Speed of light constraints:** Minimum latency between datacenters, why sub-100ms global consistency is physically impossible without approximation
- **Thermodynamic limits:** Landauer's principle, reversible computing, energy per bit
- **Quantum limits:** Heisenberg uncertainty in timing, quantum tunneling in transistors, why 1nm is approaching physical limits
- **Optical interconnects:** Silicon photonics, co-packaged optics, why electrical signaling fails at high bandwidth-distance products
- **Production connection:** Why global databases use clocks and causality tracking rather than synchronous replication; why data center energy is the new constraint; why photonic interconnects are the future of AI clusters

### 0.3 Economic Analysis of System Design
- **Total Cost of Ownership (TCO):** CapEx, OpEx, personnel, opportunity cost
- **Marginal analysis:** Cost of the next user, next request, next byte
- **Technical debt valuation:** Interest rate, principal, amortization, bankruptcy risk
- **Build vs. buy vs. partner:** Decision framework, vendor lock-in, strategic control
- **Production connection:** TCO analysis for cloud vs. on-premise; marginal cost of a new feature; valuing technical debt in sprint planning

### 0.4 Organizational Architecture and Conway's Law
- **Team topologies:** Stream-aligned, platform, enabling, complicated subsystem teams
- **Conway's Law:** System structure mirrors organizational communication structure; designing systems requires designing organizations
- **Platform engineering:** Internal developer platforms, golden paths, self-service infrastructure
- **Technical strategy:** Vision, bets, no-gos, investment horizons, portfolio management
- **Production connection:** Why microservices fail without platform teams; why platform engineering is essential at scale; how technical strategy shapes architecture over 5 years

### 0.5 Evolutionary Architecture and Technical Debt
- **Architecture fitness functions:** Automated validation of architectural constraints
- **Evolutionary patterns:** Strangler fig, branch by abstraction, parallel run
- **Deprecation strategies:** Sunset policies, migration incentives, compatibility layers
- **Succession planning:** Knowledge transfer, bus factor, documentation as architecture
- **Production connection:** Fitness functions for API compatibility; strangler fig for legacy migration; deprecation as a product feature

### 0.6 Lab: Formal Specification of a Distributed Protocol
- **Task:** Specify and model-check a distributed cache invalidation protocol
- **Requirements:**
  - Write TLA+ spec for cache coherence across 3+ nodes
  - Define safety invariants (no stale reads) and liveness properties (eventual consistency)
  - Model check with TLC for various configurations
  - Find and fix a bug using counterexample
  - Document the spec and its relationship to implementation
- **Deliverable:** TLA+ spec, model checking results, bug report, implementation guide

---

## Module 1: Planet-Scale Distributed Systems

**Duration:** 30 hours  
**Level:** Expert

### 1.1 Global Data Placement and Consistency
- **Data sovereignty:** GDPR, CCPA, data residency requirements, jurisdictional boundaries
- **Consistency models at global scale:** Causal+ consistency, parallel snapshot isolation, session guarantees
- **CRDTs at scale:** State-based vs. operation-based, delta-state CRDTs, bounded growth
- **Clock synchronization:** HLC (Hybrid Logical Clocks), CockroachDB timestamps, TrueTime
- **Production connection:** Designing for GDPR data residency; CRDTs for collaborative editing at scale; why CockroachDB's HLC enables serializable transactions globally

### 1.2 Multi-Region Architecture Patterns
- **Active-active:** Conflict resolution, vector clocks, last-write-wins, custom merge functions
- **Active-passive:** RTO/RPO, failover automation, split-brain prevention
- **Follower reads:** Stale reads for latency, bounded staleness, read replicas
- **Global databases:** Spanner, CockroachDB, YugabyteDB — trade-offs and limitations
- **Production connection:** Active-active for latency-sensitive reads; active-passive for compliance; follower reads for cost optimization

### 1.3 Edge Computing and Fog Architecture
- **Edge hierarchy:** Cloud → regional → metro → access → device
- **Edge orchestration:** Kubernetes at the edge, lightweight control planes, autonomous operation
- **Data synchronization:** Edge-to-cloud sync, conflict resolution, offline-first
- **Production connection:** CDN edge for inference; autonomous vehicles; IoT data processing; why edge computing is not "cloud but smaller"

### 1.4 Custom Networking and SDN
- **Software-defined networking:** OpenFlow, P4, programmable data planes
- **Custom routing:** Anycast, BGP manipulation, traffic engineering, MPLS
- **Network function virtualization:** Load balancers, firewalls, NAT as software
- **Production connection:** Google's Jupiter network; Facebook's Express Backbone; custom SDN for AI cluster topology

### 1.5 Lab: Designing a Global AI Inference Network
- **Task:** Design a system for serving AI models from 50+ edge locations
- **Requirements:**
  - Model deployment to edge with versioning and rollback
  - Consistent model serving across regions
  - Edge-to-cloud feedback loop for model updates
  - Data residency compliance
  - <50ms inference latency from any major city
  - Automatic failover between regions
  - Cost optimization: edge caching vs. cloud inference
- **Deliverable:** Architecture document, latency analysis, cost model, compliance matrix, failover test plan

---

## Module 2: Custom Protocol Design and Kernel Bypass

**Duration:** 25 hours  
**Level:** Expert

### 2.1 Custom Application Protocols
- **Protocol design principles:** Simplicity, extensibility, efficiency, debuggability
- **Binary protocols:** TLV (Type-Length-Value), fixed headers, variable-length fields, endianness
- **Framing:** Length-prefix framing, delimiter-based framing, chunked transfer
- **Versioning:** In-band vs. out-of-band, capability negotiation, graceful degradation
- **Production connection:** Designing custom protocols for AI training collectives; why gRPC is not always sufficient; protocol design for high-frequency trading

### 2.2 Kernel Bypass Networking
- **DPDK (Data Plane Development Kit):** Poll-mode drivers, huge pages, NUMA awareness, core pinning
- **AF_XDP:** Express Data Path, zero-copy from NIC to userspace, BPF program for packet steering
- **RDMA (Remote Direct Memory Access):** InfiniBand, RoCE, one-sided operations, memory registration
- **Production connection:** DPDK for custom load balancers; AF_XDP for high-throughput packet processing; RDMA for distributed training collectives

### 2.3 Userspace TCP Stacks
- **mTCP:** Multi-core TCP stack, batch processing, lock-free data structures
- **F-Stack:** DPDK-based TCP/IP stack, POSIX compatibility, high performance
- **Custom transport protocols:** QUIC variants, reliable UDP, congestion control customization
- **Production connection:** Userspace TCP for 10M+ connections; custom congestion control for data center networks; QUIC for mobile optimization

### 2.4 eBPF for Custom Data Planes
- **eBPF architecture:** Verifier, JIT compiler, maps, helper functions, program types
- **XDP (eXpress Data Path):** Packet processing at NIC driver level, drop/redirect/pass
- **TC (Traffic Control) eBPF:** Qdisc integration, traffic shaping, custom scheduling
- **Production connection:** eBPF for DDoS mitigation; custom load balancing at XDP; traffic shaping for QoS

### 2.5 Lab: Building a Kernel-Bypass Load Balancer
- **Task:** Build an L4 load balancer using DPDK or AF_XDP
- **Requirements:**
  - Packet processing at >10M packets/sec per core
  - Consistent hashing for backend selection
  - Health checking and automatic backend removal
  - Connection tracking and NAT
  - Metrics export via eBPF maps or shared memory
  - Comparison with IPVS and Nginx
- **Deliverable:** Working implementation, performance benchmarks, packet capture analysis, architecture document

---

## Module 3: Advanced Consensus, Replication, and Byzantine Fault Tolerance

**Duration:** 30 hours  
**Level:** Expert

### 3.1 Advanced Consensus Protocols
- **Multi-Paxos optimizations:** Leader leasing, batching, pipelining, witness nodes
- **Raft variants:** Pre-vote, checkquorum, joint consensus, single-server membership changes
- **EPaxos / Multi-Paxos:** Leaderless consensus, dependency tracking, commit without leader
- **Flexible Paxos:** Quorum intersection relaxation, flexible quorums
- **Production connection:** etcd's Raft implementation; CockroachDB's Multi-Raft; why leaderless consensus matters for geo-distributed systems

### 3.2 Byzantine Fault Tolerance at Scale
- **PBFT optimizations:** Fast path, speculative execution, view change optimization
- **HotStuff:** Linear communication, chained consensus, responsiveness
- **Tendermint / Cosmos:** BFT consensus for blockchains, bonded validators, slashing
- **Production connection:** Blockchain consensus (Ethereum 2.0, Cosmos); BFT for federated learning; why BFT is expensive and when it's worth it

### 3.3 State Machine Replication with Reconfiguration
- **Dynamic membership:** Adding/removing nodes without downtime, joint consensus
- **Snapshotting and recovery:** Incremental snapshots, log compaction, catch-up
- **Byzantine fault-tolerant SMR:** BFT-Smart, RBFT, Scalable BFT
- **Production connection:** Dynamic reconfiguration in etcd; snapshotting in Raft; why reconfiguration is harder than it appears

### 3.4 Clocks, Causality, and Consistency
- **Vector clocks:** Version vectors, dotted version vectors, scalability limits
- **Hybrid Logical Clocks (HLC):** Physical clock + logical counter, causality tracking without coordination
- **Causal broadcast:** Deliver messages in causal order, implementation strategies
- **Production connection:** HLC in CockroachDB; vector clocks in Riak; causal consistency in collaborative systems

### 3.5 Lab: Implementing an Advanced Consensus Protocol
- **Task:** Implement EPaxos or HotStuff
- **Requirements:**
  - Leaderless or responsive consensus
  - Dependency tracking and commit optimization
  - Dynamic membership changes
  - Byzantine fault tolerance (optional)
  - Formal safety argument
  - Jepsen-style testing with network partitions
  - Benchmark: latency under varying conflict rates
- **Deliverable:** Working implementation, formal proof sketch, test results, performance analysis

---

## Module 4: Custom Storage Engines and Learned Indexes

**Duration:** 30 hours  
**Level:** Expert

### 4.1 B-Tree Variants and Optimizations
- **Bw-Tree:** Lock-free B-trees, delta records, mapping table, garbage collection
- **Masstree:** Trie of B+-trees, cache-line-friendly, optimistic concurrency
- **BzTree:** PMEM-optimized B-tree, persistent memory, crash consistency
- **Production connection:** Bw-Tree in SQL Server Hekaton; Masstree for in-memory databases; BzTree for persistent memory systems

### 4.2 LSM-Tree Optimizations
- **Tiered compaction:** Size-tiered, leveled, hybrid, time-windowed
- **Bloom filter optimization:** Monotonic filters, prefix filters, SuRF (Succinct Range Filter)
- **Range filtering:** Prefix Bloom filters, Rosetta range filter, learned filters
- **Production connection:** RocksDB tuning for workloads; SuRF for range query optimization; why LSM-trees dominate write-heavy workloads

### 4.3 Learned Indexes
- **The Case for Learned Index Structures:** Recursive model index (RMI), CDF modeling, error bounds
- **Learned index variants:** PGM index, RadixSpline, ALEX (Adaptive Learned Index)
- **Integration challenges:** Update handling, concurrency, model training overhead
- **Production connection:** When learned indexes beat B-trees (read-heavy, static data); when they fail (write-heavy, dynamic data); research frontiers

### 4.4 Persistent Memory and Storage Class Memory
- **Intel Optane / 3D XPoint:** Byte-addressable persistence, PMEM programming model
- **Programming models:** App Direct, Memory Mode, libpmem, PMDK
- **Crash consistency:** Cache line flush, memory fences, transactional persistence
- **Production connection:** PMEM for high-performance databases; why Optane's discontinuation reshaped the market; CXL as the successor

### 4.5 Lab: Building a Learned Index Storage Engine
- **Task:** Build a storage engine using learned indexes
- **Requirements:**
  - Recursive model index for point lookups
  - PGM index for range queries
  - Integration with LSM-tree or B-tree for writes
  - Benchmark against standard B-tree and LSM-tree
  - Measure: lookup latency, range scan performance, build time, memory overhead
  - Handle updates without full rebuild
- **Deliverable:** Working engine, performance comparison, analysis of when learned indexes win/lose

---

## Module 5: Advanced Caching — Coherence, Consistency, and Custom Eviction

**Duration:** 20 hours  
**Level:** Expert

### 5.1 Cache Coherence Protocols
- **MESI and variants:** Modified, Exclusive, Shared, Invalid, MOESI, MESIF
- **Directory-based coherence:** Directory organization, pointer chains, broadcast vs. unicast
- **Timestamp-based coherence:** Lazy release consistency, TreadMarks, software distributed shared memory
- **Production connection:** Hardware cache coherence in CPUs; software coherence in distributed caches; why coherence is expensive

### 5.2 Strongly Consistent Distributed Caches
- **Linearizable caching:** Read-through linearizability, write-through consistency
- **Lease-based consistency:** Cache leases, invalidation leases, timeout-based consistency
- **Transactional caching:** Cache-as-SoR (System of Record), two-phase commit integration
- **Production connection:** Linearizable caching for financial data; lease-based for session state; transactional for inventory management

### 5.3 Custom Eviction Policies
- **W-TinyLFU:** Window-TinyLFU, admission filter, frequency sketch
- **ARC (Adaptive Replacement Cache):** Ghost entries, recency vs. frequency adaptation
- **Custom policies:** ML-based eviction, workload-aware eviction, cost-aware eviction
- **Production connection:** Caffeine's W-TinyLFU; ARC in IBM storage systems; ML-based eviction for CDN optimization

### 5.4 Lab: Designing a Linearizable Distributed Cache
- **Task:** Build a distributed cache with linearizable operations
- **Requirements:**
  - Linearizable read, write, and compare-and-swap
  - Lease-based expiration with automatic renewal
  - Multi-key atomic operations
  - Partition tolerance with configurable consistency
  - Benchmark against Redis Cluster
  - Measure: latency, throughput, consistency violations under partition
- **Deliverable:** Working cache, consistency tests, performance benchmarks, formal invariant documentation

---

## Module 6: Custom Load Balancers, Proxies, and Traffic Engineering

**Duration:** 20 hours  
**Level:** Expert

### 6.1 Custom L4/L7 Load Balancers
- **Maglev:** Consistent hashing with minimal disruption, connection tracking, backend health
- **Katran:** XDP-based load balancer, BPF program for packet processing, high performance
- **Envoy architecture:** Threading model, hot restart, filter chain, xDS APIs
- **Production connection:** Google's Maglev for L4; Facebook's Katran for DDoS resistance; Envoy as the universal proxy

### 6.2 Traffic Engineering and Anycast
- **BGP traffic engineering:** Path prepending, communities, local preference, MED
- **Anycast routing:** Same IP from multiple locations, health-aware withdrawal, latency optimization
- **Software-defined WAN (SD-WAN):** Path selection, application-aware routing, zero-touch provisioning
- **Production connection:** Google's anycast for DNS and search; Cloudflare's anycast for DDoS protection; SD-WAN for enterprise connectivity

### 6.3 Custom Congestion Control
- **BBR (Bottleneck Bandwidth and RTT):** Model-based congestion control, bandwidth probing, RTT fairness
- **COPA:** Delay-based congestion control, competitive equilibrium, fairness
- **HPCC (High Precision Congestion Control):** In-network telemetry, precise rate control
- **Production connection:** BBR for YouTube and Google Cloud; HPCC for data center networks; custom congestion control for RDMA

### 6.4 Lab: Building a Custom Anycast Load Balancer
- **Task:** Design and simulate an anycast-based global load balancing system
- **Requirements:**
  - BGP anycast announcement from multiple PoPs
  - Health-aware route withdrawal
  - Latency-based backend selection
  - DDoS mitigation with rate limiting and blackholing
  - Simulation with Mininet or real BGP testbed
  - Benchmark: <50ms failover, <1% packet loss during failure
- **Deliverable:** Architecture document, simulation results, failover test report, BGP configuration

---

## Module 7: AI/ML Platform Architecture — Training Supercomputers and Inference at Scale

**Duration:** 35 hours  
**Level:** Expert

### 7.1 AI Supercomputer Design
- **Cluster topology:** Fat-tree, dragonfly, torus, fully connected (DGX SuperPOD)
- **Interconnect technologies:** InfiniBand, NVLink, NVSwitch, CXL, photonic interconnects
- **Memory hierarchy:** HBM, DDR, CXL-attached memory, disaggregated memory
- **Power and cooling:** PUE, liquid cooling, immersion cooling, power density limits
- **Production connection:** NVIDIA DGX SuperPOD; Google's TPU pods; Meta's RSC; why topology-aware scheduling matters

### 7.2 Distributed Training at Exascale
- **3D parallelism:** Data + tensor + pipeline parallelism, communication scheduling
- **ZeRO-Infinity:** Offloading to CPU and NVMe, infinity offload engine
- **FSDP (Fully Sharded Data Parallel):** Sharding optimizer states, gradients, parameters
- **Communication optimization:** Overlapping communication and computation, bucket sizes, gradient compression
- **Production connection:** Training GPT-4 scale models; memory optimization for 1T+ parameter models; communication scheduling for topology-aware performance

### 7.3 Model Serving at Scale
- **Batching strategies:** Dynamic batching, continuous batching, in-flight batching, iteration-level scheduling
- **Quantization and compilation:** INT8, FP16, GPTQ, AWQ, SmoothQuant, TensorRT, ONNX Runtime
- **Model parallelism for serving:** Tensor parallelism, pipeline parallelism, expert parallelism (MoE)
- **Speculative decoding:** Draft model, acceptance criteria, speedup analysis, tree-based speculation
- **Production connection:** vLLM for LLM serving; continuous batching for throughput; speculative decoding for latency reduction; MoE for cost-efficient serving

### 7.4 Feature Platforms and Real-Time AI
- **Feature store architecture:** Online store, offline store, feature registry, point-in-time correctness
- **Real-time feature computation:** Stream processing, windowed aggregations, feature freshness
- **Model freshness:** Online learning, continual learning, model update strategies
- **Production connection:** Tecton for feature management; real-time fraud detection; online learning for recommendation systems

### 7.5 Lab: Designing an Exascale Training Cluster
- **Task:** Design a distributed training system for a 1T parameter model
- **Requirements:**
  - Cluster topology design (10,000+ GPUs)
  - 3D parallelism strategy with communication scheduling
  - Checkpointing strategy (frequency, storage, recovery time)
  - Fault tolerance (automatic restart, elastic training)
  - Power and cooling requirements
  - Network bandwidth calculations
  - Cost model (CapEx and OpEx)
  - Performance projection (TFLOPS/GPU, time to train)
- **Deliverable:** Architecture document, topology diagram, performance model, cost analysis, risk assessment

---

## Module 8: LLM Infrastructure — Distributed Serving, Speculative Decoding, and Multi-Modal Pipelines

**Duration:** 30 hours  
**Level:** Expert

### 8.1 LLM Serving Architecture
- **vLLM deep dive:** PagedAttention, continuous batching, prefix caching, speculative decoding integration
- **TensorRT-LLM:** Tensor parallelism, pipeline parallelism, in-flight batching, plugins
- **Text Generation Inference (TGI):** Safetensors, flash attention, quantization support
- **Distributed serving:** Tensor parallelism across GPUs, pipeline parallelism across nodes, expert parallelism for MoE
- **Production connection:** vLLM for open-source serving; TensorRT-LLM for NVIDIA-optimized inference; choosing based on model size and latency requirements

### 8.2 Advanced Decoding Strategies
- **Speculative decoding:** Draft model selection, acceptance rate, tree-based speculation, lookahead decoding
- **Medusa:** Multiple future tokens prediction, tree attention, draft heads
- **Lookahead decoding:** N-gram-based speculation, Jacobi iteration, parallel token verification
- **Production connection:** Speculative decoding for 2-3x latency reduction; Medusa for single-model speculation; lookahead for memory-constrained scenarios

### 8.3 Multi-Modal and Agent Infrastructure
- **Multi-modal pipelines:** Text, image, audio, video — unified embedding space, cross-modal retrieval
- **Agent orchestration:** Tool use, planning, memory, multi-agent communication, state management
- **Long-context handling:** Ring attention, streaming attention, Hierarchical Navigable Attention
- **Production connection:** GPT-4V for vision-language tasks; agent frameworks for autonomous workflows; long-context for document analysis

### 8.4 Cost Optimization and Efficiency
- **Token economics:** Input vs. output token pricing, context window costs, batching economics
- **Model distillation:** Teacher-student training, logit matching, layer pruning
- **Caching strategies:** Prefix caching, semantic caching, response caching
- **Production connection:** Token budgeting for user tiers; distillation for cost reduction; semantic caching for repeated queries

### 8.5 Lab: Designing a Production LLM Serving Platform
- **Task:** Design a platform serving 100+ LLM models with diverse requirements
- **Requirements:**
  - Multi-model serving with resource isolation
  - Speculative decoding for latency-sensitive models
  - Continuous batching for throughput-sensitive models
  - Multi-modal pipeline support
  - Agent orchestration with tool use
  - Cost tracking per request and per user
  - A/B testing for model versions
  - Automatic scaling based on queue depth
  - <100ms P99 for small models, <2s for large models
- **Deliverable:** Architecture document, resource allocation model, cost analysis, latency breakdown, scaling policy

---

## Module 9: Security Architecture — Formal Verification, Zero-Knowledge, and Post-Quantum

**Duration:** 20 hours  
**Level:** Expert

### 9.1 Formal Verification of Security Properties
- **Model checking security:** NuSMV, SPIN, TLA+ for security protocols
- **Theorem proving:** Coq, Isabelle/HOL, proof assistants for cryptographic protocols
- **Symbolic execution:** KLEE, angr, finding vulnerabilities in protocol implementations
- **Production connection:** Verifying TLS implementations; formally proving consensus safety; symbolic execution for smart contract auditing

### 9.2 Zero-Knowledge Proofs
- **zk-SNARKs:** Succinct non-interactive arguments of knowledge, trusted setup, circuit design
- **zk-STARKs:** Scalable transparent arguments, no trusted setup, post-quantum security
- **Applications:** Private transactions, verifiable computation, identity proofs
- **Production connection:** Zcash for private payments; zk-rollups for blockchain scaling; verifiable ML inference

### 9.3 Post-Quantum Cryptography
- **NIST standards:** CRYSTALS-Kyber (key encapsulation), CRYSTALS-Dilithium (signatures), SPHINCS+
- **Migration strategies:** Hybrid classical/post-quantum, cryptographic agility, inventory
- **Performance implications:** Larger key sizes, slower operations, bandwidth overhead
- **Production connection:** Preparing for quantum threats; hybrid encryption for long-term secrets; cryptographic agility for future-proofing

### 9.4 Confidential Computing
- **Trusted Execution Environments (TEEs):** Intel SGX, AMD SEV, ARM TrustZone, AWS Nitro Enclaves
- **Attestation:** Remote attestation, measurement, verification
- **Applications:** Secure multi-party computation, private ML training, key management
- **Production connection:** Nitro Enclaves for AWS key management; SGX for private analytics; TEEs for federated learning

### 9.5 Lab: Designing a Zero-Knowledge Verification System
- **Task:** Design a system for verifiable computation of ML inference
- **Requirements:**
  - Client submits input, receives output + proof
  - Proof verifies that inference was performed correctly
  - No leakage of model weights or intermediate activations
  - Choose zk-SNARK or zk-STARK based on requirements
  - Performance analysis: proof generation time, verification time, proof size
  - Security argument for zero-knowledge property
- **Deliverable:** Architecture document, circuit design, performance analysis, security proof sketch

---

## Module 10: Organizational Scaling — Platform Engineering, RFC Culture, and Technical Strategy

**Duration:** 20 hours  
**Level:** Expert

### 10.1 Platform Engineering
- **Internal Developer Platforms (IDPs):** Self-service infrastructure, golden paths, developer experience
- **Platform team topology:** Platform as a product, platform engineering vs. DevOps vs. SRE
- **Platform capabilities:** CI/CD, observability, security, cost management, data infrastructure
- **Production connection:** Spotify's Backstage; Netflix's platform; why platform engineering is essential at scale

### 10.2 RFC Culture and Decision Making
- **RFC process:** Problem, proposal, alternatives, risks, timeline, stakeholders
- **Decision records:** ADRs, architecture review boards, escalation paths
- **Disagree and commit:** Handling dissent, recording dissent, revisiting decisions
- **Production connection:** Google's design docs; Amazon's 6-pagers; why written communication scales better than meetings

### 10.3 Technical Strategy and Portfolio Management
- **Technical vision:** 3-5 year horizon, bets, no-gos, investment themes
- **Portfolio management:** Horizon 1 (optimize), Horizon 2 (extend), Horizon 3 (transform)
- **Technical debt strategy:** Amortization, consolidation, strategic debt vs. reckless debt
- **Production connection:** AWS's three-pillar strategy; Google's technical bets; why technical strategy must align with business strategy

### 10.4 Mentoring and Staff+ Engineering
- **Staff engineer archetypes:** Tech lead, architect, solver, right hand
- **Mentoring frameworks:** Socratic questioning, code review as teaching, career coaching
- **Influence without authority:** Building consensus, driving change, managing up
- **Production connection:** Staff engineer expectations at Google, Meta, Netflix; why influence > authority at senior levels

### 10.5 Lab: Writing a Technical Strategy Document
- **Task:** Write a 5-year technical strategy for an AI infrastructure platform
- **Requirements:**
  - Current state assessment
  - Vision and principles
  - Key bets (Horizon 1/2/3)
  - Investment priorities
  - Risk assessment and mitigation
  - Organizational implications
  - Metrics for success
  - Peer review and revision
- **Deliverable:** Strategy document, presentation to peers, feedback incorporation, final version

---

## Module 11: Emerging Frontiers — Photonic Computing, Neuromorphic Systems, and Beyond

**Duration:** 15 hours  
**Level:** Expert → Research

### 11.1 Photonic Interconnects and Computing
- **Silicon photonics:** Optical transceivers, co-packaged optics, wavelength division multiplexing
- **Photonic computing:** Matrix-vector multiplication in optics, Mach-Zehnder interferometers, photonic accelerators
- **Challenges:** Thermal stability, crosstalk, packaging, electronic-photonic integration
- **Production connection:** Co-packaged optics in AI clusters; Lightmatter's photonic accelerators; why photonics matters for exascale

### 11.2 Neuromorphic Computing
- **Spiking neural networks (SNNs):** Leaky integrate-and-fire, temporal coding, event-driven computation
- **Neuromorphic hardware:** Intel Loihi, IBM TrueNorth, BrainChip Akida
- **Applications:** Low-power inference, event-based vision, always-on sensing
- **Production connection:** Loihi for robotics; neuromorphic sensors for autonomous vehicles; when SNNs beat DNNs

### 11.3 Quantum Computing and Quantum-Safe Systems
- **Quantum algorithms:** Shor's algorithm, Grover's algorithm, quantum machine learning
- **Quantum hardware:** Superconducting qubits, trapped ions, photonic qubits
- **Quantum-classical hybrid:** Variational quantum algorithms, quantum annealing
- **Production connection:** Quantum-safe cryptography migration; quantum annealing for optimization; timeline for quantum threat

### 11.4 Biological and DNA Storage
- **DNA data storage:** Encoding, synthesis, sequencing, density, durability
- **Challenges:** Cost, speed, error rates, random access
- **Production connection:** Microsoft's DNA storage research; when DNA storage becomes practical; archival storage applications

### 11.5 Lab: Research Replication — Emerging Technology Assessment
- **Task:** Assess an emerging technology for production viability
- **Requirements:**
  - Choose technology: photonic computing, neuromorphic, quantum, DNA storage, or other
  - Literature review: key papers, current state, key players
  - Technical assessment: capabilities, limitations, maturity
  - Economic assessment: cost trajectory, market timing
  - Architectural implications: how would it change system design?
  - Timeline: when (if ever) will it be production-relevant?
  - Recommendation: invest, monitor, or ignore
- **Deliverable:** Assessment report, presentation, peer critique, final recommendation

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Planet-Scale AI Platform
- **Scope:** Design a global AI infrastructure platform serving 1B+ users
- **Components:**
  - Multi-region training clusters (10,000+ GPUs)
  - Global inference network with edge serving
  - Feature platform with real-time and batch features
  - Model registry with versioning and lineage
  - Multi-modal pipeline (text, image, video, audio)
  - Security: zero-trust, confidential computing, audit trails
  - Observability: distributed tracing, custom metrics, SLOs
  - Cost optimization: dynamic scaling, spot instances, model distillation
  - Organizational: platform teams, RFC process, technical strategy
- **Deliverables:** Architecture document, TLA+ specs for critical protocols, cost model, security analysis, organizational design, 5-year technical strategy

### Capstone B: Post-Quantum Secure Distributed System
- **Scope:** Design a distributed system resistant to quantum attacks
- **Components:**
  - Post-quantum cryptography (Kyber, Dilithium)
  - Zero-knowledge proofs for verifiable computation
  - Byzantine fault-tolerant consensus
  - Confidential computing with TEEs
  - Formal verification of security properties
  - Migration strategy from classical to post-quantum
  - Performance analysis: overhead vs. classical cryptography
- **Deliverables:** Architecture document, formal security proof, implementation of core protocols, performance benchmarks, migration plan

### Capstone C: Custom AI Accelerator and Serving Stack
- **Scope:** Design a custom hardware-software stack for AI inference
- **Components:**
  - Custom accelerator architecture (ASIC, FPGA, or photonic)
  - Compiler and runtime for the accelerator
  - Distributed serving infrastructure
  - Integration with existing ML frameworks
  - Performance projection vs. NVIDIA/TPU
  - Cost analysis: NRE, unit cost, TCO
  - Power and cooling requirements
  - Software ecosystem: drivers, libraries, tools
- **Deliverables:** Architecture document, hardware specification, software stack design, performance model, cost analysis, ecosystem plan

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Design exercises | 15% | Architecture documents, TLA+ specs, formal proofs |
| Lab implementations | 15% | Working prototypes of advanced systems |
| Peer review & mentoring | 10% | Reviewing others' designs, providing structured feedback |

### Examinations (30%)
- **Midterm (15%):** Formal methods, advanced consensus, custom protocols
- **Final (15%):** AI infrastructure, security, organizational scaling, emerging technologies

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical depth and correctness | 10% |
| Architectural reasoning and trade-offs | 8% |
| Formal analysis (TLA+, proofs, models) | 5% |
| Economic and organizational analysis | 4% |
| Documentation and presentation | 3% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel contributions, production-ready, persuasive strategic reasoning
- **B (80-89):** Excellent understanding, minor gaps, strong engineering judgment
- **C (70-79):** Good understanding, significant gaps in formal methods or advanced topics
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding for staff+ level

---

## Recommended Tools, Libraries & Infrastructure

### Formal Methods
| Tool | Purpose |
|------|---------|
| **TLA+ / PlusCal** | Formal specification and model checking |
| **TLC** | TLA+ model checker |
| **Apalache** | Symbolic model checker for TLA+ |
| **Coq / Isabelle** | Theorem proving |
| **Alloy** | Lightweight formal modeling |

### Systems Programming
| Tool | Purpose |
|------|---------|
| **DPDK** | Kernel bypass networking |
| **AF_XDP** | Express Data Path |
| **eBPF / BCC** | Kernel programming |
| **RDMA / libibverbs** | Remote direct memory access |
| **SPDK** | Storage performance development kit |

### AI/ML Infrastructure
| Tool | Purpose |
|------|---------|
| **vLLM** | LLM serving |
| **TensorRT-LLM** | NVIDIA optimized inference |
| **DeepSpeed** | Microsoft distributed training |
| **Megatron-LM** | NVIDIA large model training |
| **Ray** | Distributed computing |
| **Kubeflow** | ML pipelines |

### Security
| Tool | Purpose |
|------|---------|
| **libsnark / bellman** | zk-SNARK implementations |
| **STARKWare** | zk-STARK infrastructure |
| **OpenSSL 3.x** | Post-quantum cryptography |
| **AWS Nitro Enclaves** | Confidential computing |

### Platform Engineering
| Tool | Purpose |
|------|---------|
| **Backstage** | Internal developer platform |
| **Terraform / Pulumi** | Infrastructure as code |
| **Crossplane** | Kubernetes-based infrastructure |
| **ArgoCD** | GitOps continuous delivery |

---

## References & Further Reading

### Formal Methods
1. **Lamport,** *Specifying Systems* — The TLA+ book
2. **Newcombe et al.,** "How Amazon Web Services Uses Formal Methods" — CACM article
3. **Lamport,** "The Temporal Logic of Actions" — Original TLA paper

### Advanced Distributed Systems
1. **Lynch,** *Distributed Algorithms* — The definitive formal treatment
2. **Attiya & Welch,** *Distributed Computing* — Formal approach
3. **Guerraoui & Kapalka,** *Principles of Transactional Memory* — Advanced concurrency

### AI Infrastructure
1. **Narayanan et al.,** "Efficient Large-Scale Language Model Training on GPU Clusters" — Megatron paper
2. **Kwon et al.,** "Efficient Memory Management for Large Language Model Serving with PagedAttention" — vLLM paper
3. **Pope et al.,** "Efficiently Scaling Transformer Inference" — PaLM inference paper

### Emerging Technologies
1. **Lightmatter** research papers — Photonic computing
2. **Davies et al.,** "Advancing Neuromorphic Computing with Loihi" — Intel Loihi
3. **NIST Post-Quantum Cryptography Standardization** — Official standards

### Organizational Scaling
1. **Will Larson,** *Staff Engineer* — Staff+ engineering guide
2. **Team Topologies** by Matthew Skelton and Manuel Pais — Organizational design
3. **Platform Engineering** by Luca Galante and team — Platform engineering practices

---

## Appendix A: TLA+ Specification Template

```tla
---- MODULE SystemName ----
EXTENDS Integers, Sequences, FiniteSets

CONSTANTS Nodes, MaxRequests

VARIABLES state, requests

Init ==
  /\ state = [n \in Nodes |-> "idle"]
  /\ requests = 0

Next ==
  \/ \E n \in Nodes : Request(n)
  \/ \E n \in Nodes : Process(n)
  \/ \E n \in Nodes : Fail(n)

Safety == 
  \A n \in Nodes : state[n] = "processing" => requests > 0

Liveness ==
  \A n \in Nodes : state[n] = "requesting" ~> state[n] = "completed"

====
```

## Appendix B: Economic Analysis Template

```
1. Current State
   - Annual infrastructure cost: $_____
   - Engineering cost: $_____
   - Incident cost: $_____
   - Technical debt interest: $_____

2. Proposed Change
   - Implementation cost: $_____
   - Annual savings: $_____
   - Risk reduction value: $_____
   - New capability value: $_____

3. Financial Metrics
   - NPV (5 years): $_____
   - IRR: _____%
   - Payback period: _____ months
   - Sensitivity: ±20% on key assumptions

4. Non-Financial Factors
   - Strategic alignment: _____
   - Team morale impact: _____
   - Competitive advantage: _____
   - Risk profile: _____
```

## Appendix C: Staff+ Engineering Review Checklist

Before any design is approved at staff+ level, verify:

- [ ] **Formal correctness:** Safety and liveness properties stated, ideally verified
- [ ] **Physical feasibility:** Latency, bandwidth, energy constraints validated
- [ ] **Economic viability:** TCO analysis, ROI, marginal cost documented
- [ ] **Organizational fit:** Conway's Law considered, team structure aligned
- [ ] **Evolutionary path:** Migration, deprecation, succession planned
- [ ] **Security:** Threat model, formal security argument, quantum readiness
- [ ] **Observability:** SLOs defined, failure modes instrumented, runbooks written
- [ ] **Review:** Peer review by at least two staff+ engineers, dissent recorded

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: system-design-advanced-syllabus.md