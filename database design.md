  
 ## File: database-design-syllabus.md

# Database Design for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Distributed Systems & Backend Engineering (or equivalent), TypeScript & Node.js Backend Engineering (or equivalent), strong understanding of data structures, operating systems, and computer networks  
**Estimated Duration:** 260–320 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: Storage Hardware & Physical Data Organization](#module-0-storage-hardware--physical-data-organization)
4. [Module 1: Relational Model, Set Theory & Formal Foundations](#module-1-relational-model-set-theory--formal-foundations)
5. [Module 2: SQL — Semantics, Optimization, and Execution](#module-2-sql--semantics-optimization-and-execution)
6. [Module 3: Indexing — Theory, Structures, and Selection](#module-3-indexing--theory-structures-and-selection)
7. [Module 4: Transaction Processing & Concurrency Control](#module-4-transaction-processing--concurrency-control)
8. [Module 5: Query Planning, Cost Models & Execution Engines](#module-5-query-planning-cost-models--execution-engines)
9. [Module 6: Database Internals — From Filesystem to Tuple](#module-6-database-internals--from-filesystem-to-tuple)
10. [Module 7: Distributed Databases — Partitioning, Replication, and Consistency](#module-7-distributed-databases--partitioning-replication-and-consistency)
11. [Module 8: NoSQL, NewSQL, and Specialized Stores](#module-8-nosql-newsql-and-specialized-stores)
12. [Module 9: Vector Databases & AI-Native Storage](#module-9-vector-databases--ai-native-storage)
13. [Module 10: Schema Design, Data Modeling & Domain Engineering](#module-10-schema-design-data-modeling--domain-engineering)
14. [Module 11: Production Database Engineering — Operations, Observability, and SRE](#module-11-production-database-engineering--operations-observability-and-sre)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Database Design** not as a SQL syntax course, but as a **systems engineering discipline for reliable, high-performance data management at scale**. The pedagogical approach follows a **Physics → Theory → Algorithm → System → Production** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Physics** | Storage media, memory hierarchy, I/O characteristics | Hardware-grounded reasoning |
| **Theory** | Relational algebra, set theory, formal semantics, normal forms | Provable correctness |
| **Algorithm** | Index structures, query optimization, concurrency protocols | Efficient implementations |
| **System** | Storage engines, execution engines, distributed coordination | Working databases |
| **Production** | Monitoring, tuning, disaster recovery, capacity planning | Battle-tested infrastructure |

**Core Principles:**
- **Every design decision must be traceable to physical reality.** We do not teach "use an index" — we teach *why* B-trees minimize disk seeks, *why* LSM-trees optimize for write amplification, *why* vector indexes trade recall for latency.
- **The relational model is not obsolete — it is the foundation.** We study Codd's algebra, normalization theory, and ACID semantics as the bedrock upon which all modern data systems are built — including NoSQL, NewSQL, and vector databases.
- **Concurrency control is the hardest problem in systems.** We derive isolation levels from first principles, prove serializability theorems, and implement MVCC from scratch.
- **Distributed databases are distributed systems with persistent state.** Consensus, replication, and partitioning are not "database topics" — they are distributed systems problems with durability requirements.
- **AI workloads reshape database design.** Vector search, embedding storage, time-series features, and model metadata require specialized storage that inherits classical principles while innovating for new access patterns.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Database Theory Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Relational model, basic SQL, simple normalization | CRUD application schemas |
| **Intermediate** | Relational algebra, query optimization, index selection | Production schema design |
| **Advanced** | MVCC implementation, cost-based optimization, distributed consistency | Database internals engineering |
| **Expert** | Custom storage engines, distributed transaction protocols, formal verification | Database platform engineering |

### Schema Design Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Entity-relationship modeling, basic normalization | Simple application schemas |
| **Intermediate** | Dimensional modeling, slowly changing dimensions, graph schemas | Data warehouse design |
| **Advanced** | Domain-driven design aggregates, event sourcing, CQRS | Complex domain modeling |
| **Expert** | Multi-tenant schema isolation, sharding key design, cross-region consistency | Hyperscale platform design |

### Operational Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Basic backups, simple monitoring, connection pooling | Small production databases |
| **Intermediate** | Replication setup, query tuning, partition management | Medium-scale operations |
| **Advanced** | Online schema changes, distributed recovery, capacity planning | Large-scale operations |
| **Expert** | Custom replication topologies, disaster recovery automation, database platform design | Hyperscale SRE |

### AI/ML Data Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Basic feature storage, simple embeddings | Prototype ML pipelines |
| **Intermediate** | Vector search, time-series features, model metadata stores | Production ML systems |
| **Advanced** | Feature stores, embedding indexes, multi-modal storage | LLM/RAG platforms |
| **Expert** | Custom vector indexes, learned indexes, AI-native storage engines | AI infrastructure platforms |

### Cross-Cutting Competencies
- **Systems:** Design storage systems handling >1M QPS or >1PB data
- **Formal reasoning:** Prove normalization correctness, serializability, and consistency properties
- **Operational thinking:** Debug lock contention, replication lag, and query plan regressions
- **Economic reasoning:** Storage cost optimization, query cost modeling, TCO analysis

---

## Module 0: Storage Hardware & Physical Data Organization

**Duration:** 20 hours  
**Purpose:** Ground all database design in physical reality — the storage hierarchy is the primary constraint

### 0.1 The Memory Hierarchy
- **Registers → L1 → L2 → L3 → DRAM → SSD → HDD → Network → Tape:** Latency, bandwidth, capacity at each level
- **Cache lines:** 64-byte alignment, false sharing, prefetching
- **TLB (Translation Lookaside Buffer):** Page walks, huge pages (2MB, 1GB), TLB shootdowns
- **NUMA (Non-Uniform Memory Access):** Local vs. remote memory, affinity, interleaving
- **Production connection:** Why database buffer pools are sized to fit in DRAM; why huge pages matter for large memory databases; NUMA-aware allocation in PostgreSQL

### 0.2 Disk Storage Physics
- **HDD mechanics:** Platters, heads, tracks, sectors, cylinders, seek time, rotational latency, transfer time
- **SSD architecture:** NAND flash, pages, blocks, erase-before-write, wear leveling, over-provisioning
- **NVMe protocol:** PCIe lanes, queue pairs, parallelism, latency reduction vs. SATA
- **I/O patterns:** Sequential vs. random, read vs. write, synchronous vs. asynchronous, direct I/O
- **Production connection:** Why B-trees favor sequential I/O; why LSM-trees are SSD-friendly; why NVMe queue depth matters for parallel queries

### 0.3 File Systems and Block I/O
- **File system structures:** Inodes, direct/indirect blocks, extents, journaling (ext4, XFS, Btrfs)
- **Copy-on-write (COW):** Btrfs, ZFS — snapshotting, checksums, self-healing
- **Memory-mapped files:** `mmap`, page faults, `madvise`, `msync`
- **Direct I/O:** Bypassing page cache, `O_DIRECT`, alignment requirements
- **Production connection:** ZFS for database data integrity; `mmap` for read-only analytical workloads; direct I/O for write-heavy transactional workloads

### 0.4 Data Layout and Alignment
- **Row-oriented storage:** Tuple layout, header, null bitmap, variable-length fields, padding
- **Column-oriented storage:** Column chunks, compression, vectorized execution
- **Hybrid layouts:** PAX (Partition Attributes Across), Apache Arrow
- **Alignment and padding:** Cache line alignment, SIMD requirements, memory waste trade-offs
- **Production connection:** Row stores for OLTP (PostgreSQL); column stores for OLAP (ClickHouse); Arrow for zero-copy data exchange

### 0.5 Lab: Storage Benchmarking and Characterization
- **Task:** Characterize storage subsystem performance
- **Requirements:**
  - Measure sequential vs. random read/write throughput for HDD, SATA SSD, NVMe SSD
  - Measure latency distribution (P50, P99, P99.9) under varying queue depths
  - Test `mmap` vs. `read`/`write` for large file access
  - Test direct I/O vs. buffered I/O
  - Document block size effects (4KB, 16KB, 64KB, 1MB)
- **Deliverable:** Benchmark report with latency histograms, throughput curves, queue depth analysis, recommendations for database page sizes

---

## Module 1: Relational Model, Set Theory & Formal Foundations

**Duration:** 25 hours  
**Level:** Beginner → Intermediate

### 1.1 Set Theory and Logic
- **Sets, relations, and functions:** Cartesian product, power set, equivalence relations
- **First-order logic:** Predicates, quantifiers, logical connectives, satisfiability
- **Relational calculus:** Tuple relational calculus, domain relational calculus, safety
- **Production connection:** Why SQL is (approximately) relational calculus with bag semantics; why set semantics matter for query optimization

### 1.2 The Relational Model
- **Relations:** Schema, domain, attribute, tuple, degree, cardinality
- **Keys:** Superkey, candidate key, primary key, foreign key, surrogate keys
- **Relational algebra:** Selection (σ), projection (π), union (∪), difference (−), intersection (∩), Cartesian product (×), rename (ρ), join (⋈), division (÷)
- **Relational algebra equivalences:** Commutativity, associativity, selection pushdown, projection pushdown
- **Production connection:** Query optimizers transform SQL into relational algebra and apply equivalence rules; understanding these rules explains why indexes matter

### 1.3 SQL Semantics
- **Data definition:** `CREATE TABLE`, `ALTER TABLE`, constraints (`NOT NULL`, `UNIQUE`, `CHECK`, `FOREIGN KEY`), domains
- **Data manipulation:** `INSERT`, `UPDATE`, `DELETE`, `MERGE` (upsert)
- **Querying:** `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`/`OFFSET`, window functions (`OVER`, `PARTITION BY`, `ORDER BY`, frame specification)
- **Subqueries:** Correlated vs. non-correlated, `EXISTS`, `IN`, `ANY`/`ALL`, lateral joins
- **Common Table Expressions (CTEs):** Recursive CTEs, `WITH` clause, materialization hints
- **Production connection:** Window functions for running totals and rankings; recursive CTEs for hierarchical data; lateral joins for top-N per group

### 1.4 Normalization Theory
- **Functional dependencies:** Definition, Armstrong's axioms, closure computation
- **Normal forms:** 1NF (atomic values), 2NF (no partial dependencies), 3NF (no transitive dependencies), BCNF (every determinant is a superkey)
- **Decomposition algorithms:** 3NF synthesis, BCNF decomposition, lossless-join, dependency preservation
- **Higher normal forms:** 4NF (multivalued dependencies), 5NF (join dependencies), DKNF
- **Denormalization:** When and why, materialized views, redundancy trade-offs
- **Production connection:** Why 3NF/BCNF is the sweet spot; when to denormalize for read performance; materialized views for analytical queries

### 1.5 Lab: Formal Schema Design and Verification
- **Task:** Design a schema for a complex domain and verify normalization
- **Requirements:**
  - Choose domain: e-commerce, healthcare, financial trading, or ML experiment tracking
  - Identify all functional dependencies
  - Normalize to BCNF with proof of lossless-join and dependency preservation
  - Document denormalization decisions with justification
  - Write complex queries using window functions, CTEs, and lateral joins
- **Deliverable:** Schema design document, normalization proofs, query suite with execution plans

---

## Module 2: SQL — Semantics, Optimization, and Execution

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 2.1 SQL Execution Semantics
- **Logical query processing order:** `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY` → `LIMIT`
- **Bag vs. set semantics:** Duplicates, `DISTINCT`, `ALL`, `UNION` vs. `UNION ALL`
- **NULL handling:** Three-valued logic (`TRUE`, `FALSE`, `UNKNOWN`), `IS NULL`, `COALESCE`, `NULLIF`
- **Window function semantics:** Frame boundaries (`ROWS`, `RANGE`, `GROUPS`), `EXCLUDE`, `WINDOW` clause
- **Production connection:** Why `SELECT *` can be expensive; why `NULL` complicates indexing; window function frame specification affects performance

### 2.2 Advanced SQL Patterns
- **Pivot and unpivot:** `CASE` aggregation, `crosstab`, `UNPIVOT`
- **Gaps and islands:** Identifying contiguous ranges, sessionization
- **Running totals and moving averages:** Window frames, `ROWS BETWEEN`
- **Top-N per group:** `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, lateral joins
- **Graph queries in SQL:** Recursive CTEs for tree/graph traversal, path enumeration
- **Time-series patterns:** Lead/lag, delta computation, sessionization, bucketing
- **Production connection:** Sessionization for web analytics; time-series bucketing for feature engineering; graph CTEs for hierarchical ML features

### 2.3 Query Optimization from First Principles
- **Cost-based optimization:** Statistics, selectivity, cardinality estimation, histograms
- **Join ordering:** Dynamic programming (System R, Selinger), greedy heuristics, left-deep vs. bushy trees
- **Join algorithms:** Nested loop, hash join, merge join, semi-join, anti-join
- **Access path selection:** Full table scan, index scan, index-only scan, bitmap scan
- **Production connection:** Why join order matters more than join algorithm; why statistics must be up-to-date; why `ANALYZE` is critical

### 2.4 SQL for ML Workloads
- **Feature engineering in SQL:** Aggregations, window functions, time-based features
- **Sampling:** Random sampling, stratified sampling, reservoir sampling
- **Embedding storage:** Array types, JSONB for sparse vectors, binary storage for dense vectors
- **Model inference in SQL:** PostgreSQL `plpython3u`, BigQuery ML, in-database prediction
- **Production connection:** SQL-based feature pipelines; in-database inference for low latency; sampling for training data generation

### 2.5 Lab: Query Optimization Challenge
- **Task:** Optimize a suite of slow queries on a large dataset
- **Requirements:**
  - Given 10 queries with execution times >10 seconds each
  - Analyze execution plans (`EXPLAIN ANALYZE`)
  - Identify missing indexes, suboptimal joins, statistics issues
  - Implement optimizations and measure improvement
  - Document root cause and solution for each
  - Target: all queries <100ms
- **Deliverable:** Optimization report with before/after execution plans, index design rationale, statistics analysis

---

## Module 3: Indexing — Theory, Structures, and Selection

**Duration:** 30 hours  
**Level:** Intermediate → Advanced

### 3.1 B-Trees and B+ Trees
- **B-tree properties:** Order, balance, fanout, minimum occupancy
- **B+ tree specifics:** Leaf-level linked list, non-leaf keys as separators, range scan optimization
- **Insertion and deletion:** Splitting, merging, redistribution, underflow handling
- **Concurrency:** B-link trees, lock coupling, latch crabbing, optimistic vs. pessimistic
- **Production connection:** PostgreSQL B-tree implementation; why clustered indexes matter for range queries; why index fragmentation occurs

### 3.2 Hash Indexes
- **Static hashing:** Bucket arrays, hash functions, collision resolution (chaining, open addressing)
- **Extendible hashing:** Directory, global depth, local depth, splitting
- **Linear hashing:** Incremental expansion, split pointer, overflow chains
- **Production connection:** PostgreSQL hash indexes (limited use); why hash indexes are rare in production; when they beat B-trees (equality-only lookups)

### 3.3 Bitmap and Inverted Indexes
- **Bitmap indexes:** Bit vectors, compression (BBC, WAH, EWAH, Roaring), boolean operations
- **Inverted indexes:** Term-document matrix, posting lists, skip lists, compression (PForDelta, Simple9)
- **Production connection:** Bitmap indexes for low-cardinality columns (data warehousing); inverted indexes for full-text search (PostgreSQL tsvector, Elasticsearch)

### 3.4 Multi-Dimensional and Spatial Indexes
- **R-trees:** Minimum bounding rectangles, insertion, splitting (quadratic, linear), search
- **k-d trees:** Axis-aligned splitting, nearest neighbor, balanced construction
- **Quad trees and octrees:** Space partitioning, point and region queries
- **Geohashes and S2:** Spatial indexing on B-trees, Hilbert curves
- **Production connection:** PostGIS for geospatial queries; geohash for location-based features; S2 for spherical geometry

### 3.5 Index Selection and Maintenance
- **Index selection problem:** NP-hard, heuristic approaches, what-if analysis
- **Covering indexes:** Index-only scans, include columns, index intersection
- **Partial indexes:** Conditional indexing, filtered indexes, selective indexing
- **Expression indexes:** Functional indexes, computed columns, JSON path indexes
- **Index maintenance:** Rebuild vs. reorganize, fill factor, vacuum, analyze
- **Production connection:** Covering indexes for read-heavy workloads; partial indexes for soft-deleted data; expression indexes for JSON queries; index bloat detection

### 3.6 Lab: Index Design for a Production Workload
- **Task:** Design optimal indexes for a complex application
- **Requirements:**
  - Given workload trace (read/write ratio, query patterns, access frequencies)
  - Design index set minimizing total cost (query + maintenance + storage)
  - Implement in PostgreSQL with `EXPLAIN ANALYZE` validation
  - Measure write amplification from indexes
  - Test partial indexes, expression indexes, covering indexes
  - Document trade-offs and recommendations
- **Deliverable:** Index design document, cost model, performance validation, maintenance plan

---

## Module 4: Transaction Processing & Concurrency Control

**Duration:** 35 hours  
**Level:** Advanced → Expert

### 4.1 ACID Properties
- **Atomicity:** All-or-nothing, WAL (Write-Ahead Logging), undo/redo logging
- **Consistency:** Integrity constraints, triggers, cascades, deferred constraints
- **Isolation:** Concurrent execution equivalence to serial execution
- **Durability:** Force vs. no-force, steal vs. no-steal, checkpointing
- **Production connection:** Why WAL is the foundation of durability; why `fsync` latency matters; checkpoint tuning for write throughput

### 4.2 Serializability Theory
- **Schedules:** Serial, serializable, conflict-serializable, view-serializable
- **Precedence graph:** Testing conflict serializability, cycle detection
- **Two-Phase Locking (2PL):** Growing phase, shrinking phase, strict 2PL, rigorous 2PL
- **Deadlock detection and prevention:** Wait-for graph, timeout, wound-wait, wait-die
- **Production connection:** Why strict 2PL is standard; deadlock handling in PostgreSQL; lock timeout configuration

### 4.3 Isolation Levels and Anomalies
- **ANSI SQL isolation levels:** READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE
- **Anomalies:** Dirty read, non-repeatable read, phantom read, write skew, lost update
- **Critique of ANSI levels:** Adya et al.'s formalization, phenomena vs. anomalies
- **Snapshot isolation:** First-committer-wins, write skew, serializable snapshot isolation (SSI)
- **Production connection:** PostgreSQL's default READ COMMITTED; why REPEATABLE READ prevents phantoms in PostgreSQL but not in MySQL; SSI in PostgreSQL 9.1+

### 4.4 Multi-Version Concurrency Control (MVCC)
- **Version storage:** Tuple versioning, delta storage, time-travel storage
- **Visibility rules:** Transaction ID comparison, snapshot, xmin/xmax (PostgreSQL)
- **Garbage collection:** Vacuum, autovacuum, tuple freezing, transaction ID wraparound
- **Index MVCC:** Index-only scans, HOT (Heap-Only Tuple) updates, index cleanup
- **Production connection:** PostgreSQL MVCC internals; why vacuum is critical; transaction ID wraparound prevention; HOT updates for index efficiency

### 4.5 Optimistic Concurrency Control
- **Validation-based protocols:** Read phase, validation phase, write phase
- **Timestamp ordering:** Thomas Write Rule, basic timestamp ordering
- **Multi-version timestamp ordering:** Read timestamps, write timestamps
- **Production connection:** OCC for low-contention workloads; timestamp ordering in distributed systems; why OCC is rare in traditional databases

### 4.6 Lab: Implementing MVCC from Scratch
- **Task:** Build a minimal MVCC storage engine
- **Requirements:**
  - Tuple storage with version chains
  - Transaction IDs and snapshot isolation
  - Read and write operations with visibility checking
  - Garbage collection (old version removal)
  - Deadlock-free design (no locking, pure MVCC)
  - Correctness validation: no dirty reads, no lost updates, no phantoms
  - Benchmark: 10K concurrent transactions, measure throughput and version chain length
- **Deliverable:** Working storage engine, formal correctness argument, performance analysis

---

## Module 5: Query Planning, Cost Models & Execution Engines

**Duration:** 30 hours  
**Level:** Advanced → Expert

### 5.1 Query Parsing and Semantic Analysis
- **Lexical analysis:** Tokenization, keyword recognition, literal handling
- **Parsing:** Recursive descent, LR parsing, AST construction
- **Semantic analysis:** Name resolution, type checking, privilege verification, view expansion
- **Production connection:** Why prepared statements skip parse/semantic phases; why query plan caching matters

### 5.2 Logical Query Optimization
- **Rule-based optimization:** Predicate pushdown, projection pushdown, join reordering, subquery unnesting, decorrelation
- **View merging:** Expanding views, materialized view matching
- **Constant folding and propagation:** Compile-time evaluation, constraint propagation
- **Production connection:** Why `WHERE` clause order doesn't matter (optimizer reorders); why correlated subqueries are slow (lack of unnesting)

### 5.3 Cost-Based Optimization
- **Statistics collection:** Table cardinality, column histograms, most common values, correlation statistics
- **Selectivity estimation:** Equality, range, join selectivity, independence assumptions, correlated predicates
- **Cost model:** I/O cost, CPU cost, memory cost, network cost, parallel cost
- **Plan enumeration:** Dynamic programming (System R style), genetic algorithms (PostgreSQL GEQO), top-k pruning
- **Production connection:** Why statistics must be current; why `ANALYZE` is not optional; why genetic algorithms are used for complex joins

### 5.4 Physical Query Execution
- **Iterator model (Volcano):** Open-next-close, pipelining, materialization
- **Vectorized execution:** Batch processing, SIMD, columnar iteration (MonetDB, DuckDB, ClickHouse)
- **Compilation:** LLVM JIT (PostgreSQL, Umbra), code generation, adaptive execution
- **Parallel execution:** Intra-query parallelism, exchange operators, partition-wise joins
- **Production connection:** Why vectorized execution is 10-100x faster for analytics; why JIT matters for complex queries; parallel query limits for OLTP

### 5.5 Query Plan Analysis and Hinting
- **Reading execution plans:** Node types, cost estimates, actual vs. estimated rows, buffer usage
- **Plan hints:** PostgreSQL `SET` parameters, Oracle hints, SQL Server hints, when to use (rarely)
- **Plan stability:** Plan baselines, query plan management, forced plans
- **Production connection:** Why hints are a last resort; why plan regression happens after statistics updates; plan management for critical queries

### 5.6 Lab: Building a Query Optimizer
- **Task:** Implement a cost-based query optimizer for a subset of SQL
- **Requirements:**
  - Parse simple SELECT-FROM-WHERE-JOIN queries
  - Generate candidate plans (different join orders, access paths)
  - Cost model based on cardinality estimates and I/O costs
  - Choose lowest-cost plan
  - Execute plan and compare estimated vs. actual costs
  - Implement at least 3 logical optimization rules
- **Deliverable:** Working optimizer, plan comparison visualization, correctness tests

---

## Module 6: Database Internals — From Filesystem to Tuple

**Duration:** 30 hours  
**Level:** Advanced → Expert

### 6.1 Storage Engine Architecture
- **Page structure:** Header, line pointers, tuple data, free space, special space
- **Page formats:** Heap page, index page, TOAST (The Oversized-Attribute Storage Technique)
- **File organization:** Tablespaces, relation files, fork files (main, FSM, VM), segments
- **WAL (Write-Ahead Log):** XLOG records, LSN (Log Sequence Number), full page writes, checkpoints
- **Production connection:** PostgreSQL page layout (`pageinspect` extension); why 8KB page size; WAL archiving for PITR

### 6.2 Buffer Pool Management
- **Buffer pool structure:** Hash table, clock sweep, LRU variants
- **Page replacement:** Clock, LRU, 2Q, ARC, custom policies
- **Dirty page management:** Write-back, checkpoint, background writer, double-write buffer
- **Production connection:** PostgreSQL shared_buffers tuning; why 25% of RAM is a starting point; checkpoint spike prevention

### 6.3 Logging and Recovery
- **ARIES protocol:** Analysis, redo, undo phases, compensation log records (CLRs), nested top actions
- **Checkpoint types:** Sharp, fuzzy, incremental, log sequence numbers
- **Media recovery:** Full backups, incremental backups, WAL archiving, PITR (Point-in-Time Recovery)
- **Replication recovery:** Streaming replication, log shipping, cascading replication
- **Production connection:** ARIES in PostgreSQL, MySQL InnoDB, SQL Server; backup strategies (full + incremental + WAL); RTO/RPO planning

### 6.4 Locking and Latching
- **Lock types:** Shared, exclusive, intention locks, predicate locks, advisory locks
- **Lock granularity:** Row-level, page-level, table-level, deadlock detection
- **Latches:** Lightweight locks, spinlocks, mutexes, read-write locks
- **Lock-free structures:** Lock-free lists, RCU (Read-Copy-Update), optimistic concurrency
- **Production connection:** PostgreSQL lock modes; row-level vs. table-level locking trade-offs; advisory locks for application-level coordination

### 6.5 Lab: Building a Minimal Storage Engine
- **Task:** Implement a B+ tree storage engine with WAL
- **Requirements:**
  - B+ tree with insertion, deletion, search, range scan
  - Slotted page format for tuple storage
  - WAL with redo logging
  - Buffer pool with clock replacement
  - Crash recovery (restart and replay WAL)
  - ACID transactions (at least atomicity and durability)
  - Benchmark: 100K operations/sec, crash recovery <1 second
- **Deliverable:** Working storage engine, recovery tests, performance analysis

---

## Module 7: Distributed Databases — Partitioning, Replication, and Consistency

**Duration:** 35 hours  
**Level:** Advanced → Expert

### 7.1 Data Partitioning (Sharding)
- **Partitioning strategies:** Hash, range, list, composite, consistent hashing
- **Partition key selection:** Access patterns, hotspot avoidance, rebalancing
- **Cross-partition operations:** Distributed transactions, two-phase commit, sagas
- **Rebalancing:** Online resharding, split/merge, double-write migration
- **Production connection:** Hash partitioning for even distribution; range partitioning for time-series; consistent hashing for elastic scaling

### 7.2 Replication Models
- **Synchronous vs. asynchronous:** Trade-offs, latency, durability
- **Primary-backup:** Single primary, multi-primary, conflict resolution
- **Quorum replication:** R + W > N, tunable consistency, read repair
- **State machine replication:** Log replication, deterministic execution
- **Production connection:** PostgreSQL synchronous replication; MySQL semi-sync; Dynamo-style quorum; why R=1, W=N is CP

### 7.3 Distributed Consensus for Databases
- **Raft for metadata:** etcd, TiKV, CockroachDB — leader election, log replication
- **Paxos variants:** Multi-Paxos, Fast Paxos, EPaxos — latency optimizations
- **Byzantine fault tolerance:** PBFT for adversarial environments
- **Production connection:** etcd for Kubernetes metadata; CockroachDB's Raft for range leases; why consensus is only for metadata, not data

### 7.4 Distributed Transactions
- **Two-Phase Commit (2PC):** Coordinator, participants, blocking problem
- **Three-Phase Commit (3PC):** Non-blocking recovery, complexity, liveness
- **Percolator:** Timestamp oracle, prewrite, commit, lazy cleanup (Google Bigtable)
- **Spanner:** TrueTime, two-phase commit with timestamps, external consistency
- **Saga pattern:** Compensating transactions, choreography vs. orchestration
- **Production connection:** 2PC for distributed SQL (CockroachDB, YugabyteDB); Percolator for TiDB; Spanner for globally consistent transactions; sagas for microservices

### 7.5 Consistency Models
- **Linearizability:** Single-copy semantics, real-time ordering, testable with Jepsen
- **Sequential consistency:** Program order preserved, no real-time guarantee
- **Causal consistency:** Causally related operations ordered
- **Eventual consistency:** Convergence via anti-entropy, read repair, hinted handoff
- **Session guarantees:** Read-your-writes, monotonic reads, monotonic writes, writes-follow-reads
- **Production connection:** Spanner (linearizable); CockroachDB (serializable default); Cassandra (eventual + tunable); choosing based on application requirements

### 7.6 Lab: Building a Distributed Key-Value Store
- **Task:** Build a Dynamo-style distributed database
- **Requirements:**
  - Consistent hashing with virtual nodes
  - Tunable quorum replication (R + W > N)
  - Hinted handoff and read repair
  - Vector clocks for conflict resolution
  - Gossip protocol for membership
  - Benchmark: 100K ops/sec, <10ms P99 latency
  - Jepsen-style partition testing
- **Deliverable:** Working system, consistency analysis under partitions, performance report

---

## Module 8: NoSQL, NewSQL, and Specialized Stores

**Duration:** 25 hours  
**Level:** Advanced

### 8.1 Key-Value Stores
- **Design principles:** Simple API (get/put/delete), hash-based lookup, high throughput
- **Redis:** In-memory, data structures, persistence options, replication, cluster
- **RocksDB:** Embedded, LSM-tree, column families, snapshots, transactions
- **DynamoDB:** Partition key, sort key, GSIs, LSIs, on-demand vs. provisioned
- **Production connection:** Redis for caching and real-time; RocksDB as storage engine foundation; DynamoDB for serverless applications

### 8.2 Document Stores
- **Document model:** Flexible schema, nested documents, arrays, references
- **MongoDB:** BSON, replication, sharding, aggregation pipeline, transactions
- **Couchbase:** Memory-first, SQL++ (N1QL), XDCR (cross-datacenter replication)
- **Production connection:** MongoDB for rapid prototyping; schema validation for production; aggregation for analytics

### 8.3 Wide-Column Stores
- **Column family model:** Rows, column families, sparse storage, timestamped cells
- **Cassandra:** Partition key, clustering columns, CQL, gossip, repair, compaction
- **HBase:** Region servers, ZooKeeper coordination, block cache, memstore
- **ScyllaDB:** C++ Cassandra clone, shard-per-core, auto-tuning
- **Production connection:** Cassandra for time-series and messaging; HBase for large-scale analytics; ScyllaDB for low-latency Cassandra workloads

### 8.4 Graph Databases
- **Graph models:** Property graph, RDF triple store, hypergraph
- **Neo4j:** Cypher query language, ACID transactions, causal clustering
- **JanusGraph:** Backend storage (Cassandra, HBase), index backend (Elasticsearch, Solr)
- **TigerGraph:** GSQL (Turing-complete), native parallel graph computation
- **Production connection:** Neo4j for knowledge graphs; TigerGraph for large-scale graph analytics; graph databases for recommendation systems

### 8.5 NewSQL and Distributed SQL
- **CockroachDB:** Raft ranges, serializable default, cost-based optimizer, follower reads
- **YugabyteDB:** DocDB storage (RocksDB-based), YSQL (PostgreSQL-compatible), YCQL (Cassandra-compatible)
- **TiDB:** TiKV (Raft), TiFlash (columnar), HTAP (Hybrid Transactional/Analytical Processing)
- **Google Spanner:** TrueTime, external consistency, global distribution
- **Production connection:** CockroachDB for PostgreSQL-compatible distributed SQL; TiDB for MySQL-compatible HTAP; Spanner for globally consistent applications

### 8.6 Lab: Multi-Store Architecture Design
- **Task:** Design a polyglot persistence architecture for a complex application
- **Requirements:**
  - Choose 3+ database types based on access patterns
  - Document data flow between stores
  - Design consistency model (eventual, causal, strong)
  - Implement data synchronization (CDC, event sourcing, dual-write)
  - Handle failure scenarios (network partition, store unavailability)
  - Benchmark each store for its intended workload
- **Deliverable:** Architecture document, working prototype, consistency analysis, failure mode matrix

---

## Module 9: Vector Databases & AI-Native Storage

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 9.1 Vector Search Fundamentals
- **Embeddings:** Dense vectors, sparse vectors, dimensionality, similarity metrics (cosine, Euclidean, dot product, Hamming)
- **Exact nearest neighbor:** Brute force, dimensionality reduction (PCA, t-SNE, UMAP — not for search)
- **Curse of dimensionality:** Why exact search fails in high dimensions, concentration of measure
- **Production connection:** Embedding models (OpenAI, sentence-transformers); choosing similarity metrics; why 768-dim vectors are standard

### 9.2 Approximate Nearest Neighbor (ANN) Algorithms
- **Tree-based:** k-d tree, ball tree, Annoy (random projection trees) — limited to low dimensions
- **Hashing-based:** Locality Sensitive Hashing (LSH), random projections, minhash
- **Quantization-based:** Product Quantization (PQ), Optimized PQ, Scalar Quantization
- **Graph-based:** HNSW (Hierarchical Navigable Small World), NSW, NSG, Vamana, DiskANN
- **Clustering-based:** IVF (Inverted File Index), IVF-PQ, IVF-HNSW
- **Production connection:** HNSW for high-recall, low-latency search; IVF for memory-constrained scenarios; DiskANN for billion-scale on-disk search

### 9.3 Vector Database Systems
- **Pinecone:** Managed, metadata filtering, hybrid search, no index tuning
- **Weaviate:** GraphQL interface, modular AI integrations, vector + BM25 hybrid
- **Milvus/Zilliz:** GPU index building, distributed architecture, tiered storage
- **pgvector:** PostgreSQL extension, ivfflat, hnsw, sparsevec, halfvec
- **Redis Vector:** In-memory vector search, hybrid queries
- **Chroma:** Embedded, simple API, local-first
- **Production connection:** Pinecone for managed simplicity; pgvector for SQL-native vectors; Milvus for billion-scale; Redis for real-time caching + vectors

### 9.4 Multi-Modal and AI-Native Storage
- **Multi-modal embeddings:** Text, image, audio, video in shared vector space
- **Learned indexes:** The Case for Learned Index Structures, recursive model indexes, PGM index
- **AI-native storage:** Vector + structured + graph in unified systems, AI-generated schemas
- **Production connection:** CLIP for image-text embeddings; learned indexes for key-value stores; unified storage for RAG systems

### 9.5 Lab: Building a Production RAG Vector Store
- **Task:** Build a vector database backend for RAG
- **Requirements:**
  - Support 10M+ vectors (768-dim) with <50ms P99 search latency
  - Metadata filtering (text, numeric, categorical)
  - Hybrid search (dense vector + sparse BM25)
  - Incremental index updates (add/delete vectors without full rebuild)
  - Persistence and crash recovery
  - Benchmark against Pinecone and pgvector
  - Evaluate recall@k vs. latency trade-offs
- **Deliverable:** Working vector store, performance benchmarks, recall analysis, architecture document

---

## Module 10: Schema Design, Data Modeling & Domain Engineering

**Duration:** 25 hours  
**Level:** Advanced

### 10.1 Domain-Driven Design (DDD) and Data Modeling
- **Strategic DDD:** Bounded contexts, ubiquitous language, context mapping
- **Tactical DDD:** Entities, value objects, aggregates, repositories, domain events
- **Aggregates and transactions:** Aggregate boundaries as consistency boundaries, one transaction per aggregate
- **Production connection:** Designing bounded contexts for microservices; aggregate design for transaction boundaries; domain events for cross-context communication

### 10.2 Event Sourcing and CQRS
- **Event sourcing:** State as reduction of events, event store, snapshotting, event versioning
- **CQRS:** Separate read and write models, command handlers, query handlers
- **Event store design:** Stream ID, event type, event data, metadata, sequence number
- **Read model projections:** Materialized views, eventual consistency, view rebuilds
- **Production connection:** Event sourcing for audit trails; CQRS for high-read workloads; rebuilding read models from events

### 10.3 Data Warehouse and Dimensional Modeling
- **Star schema:** Fact tables, dimension tables, surrogate keys, slowly changing dimensions (SCD)
- **Snowflake schema:** Normalized dimensions, space savings, query complexity
- **Data vault:** Hubs, links, satellites, flexibility, auditability
- **Production connection:** Star schema for analytics; SCD Type 2 for historical tracking; data vault for enterprise data warehouses

### 10.4 Time-Series Data Modeling
- **Time-series characteristics:** High write volume, time-ordered queries, aggregation, retention
- **Schema patterns:** Wide table, narrow table, hypertables (TimescaleDB)
- **Compression:** Delta encoding, Gorilla, XOR-based, dictionary encoding
- **Retention and downsampling:** TTL policies, continuous aggregation, tiered storage
- **Production connection:** TimescaleDB for SQL time-series; InfluxDB for metric collection; tiered storage for cost optimization

### 10.5 Multi-Tenant Data Architecture
- **Isolation models:** Shared database/shared schema, shared database/separate schema, separate database
- **Tenant identification:** Tenant ID in every table, row-level security, schema search path
- **Resource allocation:** Per-tenant quotas, connection pooling, query routing
- **Production connection:** Shared schema for SaaS (Salesforce); separate schema for compliance (healthcare); row-level security for fine-grained isolation

### 10.6 Lab: Designing a Multi-Tenant ML Feature Store
- **Task:** Design schema and storage for a multi-tenant feature store
- **Requirements:**
  - Support 100+ tenants with data isolation
  - Real-time features (Redis) and batch features (PostgreSQL/warehouse)
  - Point-in-time correctness for training data
  - Feature versioning and lineage
  - Access control per tenant and per feature
  - Performance: <10ms for online features, <1min for batch feature backfill
- **Deliverable:** Schema design document, data flow diagrams, consistency model, performance projections

---

## Module 11: Production Database Engineering — Operations, Observability, and SRE

**Duration:** 20 hours  
**Level:** Expert

### 11.1 Monitoring and Alerting
- **Key metrics:** QPS, latency (P50, P99, P99.9), error rate, connection count, replication lag, lock waits, checkpoint frequency
- **PostgreSQL specifics:** `pg_stat_*` views, `pg_stat_statements`, `auto_explain`, `pg_buffercache`
- **MySQL specifics:** `PERFORMANCE_SCHEMA`, `INFORMATION_SCHEMA`, slow query log, `SHOW ENGINE INNODB STATUS`
- **Alerting:** SLO-based, anomaly detection, predictive alerts
- **Production connection:** Setting SLOs for database latency; anomaly detection for query plan regressions; predictive alerts for disk space

### 11.2 Backup and Recovery
- **Backup types:** Full, incremental, differential, WAL archiving, logical (pg_dump)
- **Point-in-Time Recovery (PITR):** WAL archiving, base backup + WAL replay, recovery targets
- **Disaster recovery:** RTO (Recovery Time Objective), RPO (Recovery Point Objective), cross-region replication
- **Testing backups:** Regular restore tests, automated validation
- **Production connection:** PITR for accidental deletion recovery; cross-region replication for DR; automated backup testing

### 11.3 Schema Changes and Migrations
- **Online schema changes:** `pg_repack`, `pt-online-schema-change`, native online DDL
- **Migration strategies:** Expand-contract pattern, blue-green deployment, feature flags
- **Backward compatibility:** Add-only migrations, nullable columns, dual-write periods
- **Production connection:** Zero-downtime schema changes; expand-contract for column renames; feature flags for risky migrations

### 11.4 Query Tuning and Index Maintenance
- **Slow query analysis:** `EXPLAIN ANALYZE`, `auto_explain`, `pg_stat_statements`
- **Index maintenance:** Reindex, vacuum analyze, bloat detection (`pgstattuple`)
- **Partition management:** Partition pruning, partition maintenance, archival
- **Production connection:** Weekly slow query review; monthly index maintenance; partition pruning for time-series

### 11.5 Capacity Planning and Scaling
- **Vertical scaling:** CPU, memory, IOPS, storage capacity
- **Horizontal scaling:** Read replicas, connection pooling (PgBouncer), sharding
- **Workload characterization:** Read-heavy, write-heavy, mixed, analytical
- **Cost optimization:** Reserved instances, storage tiering, query optimization
- **Production connection:** Read replicas for read scaling; connection pooling for connection limits; sharding when vertical scaling is exhausted

### 11.6 Lab: Database SRE Simulation
- **Task:** Manage a production database through a simulated incident
- **Requirements:**
  - Given a running PostgreSQL instance with synthetic workload
  - Detect and diagnose: replication lag, lock contention, query regression, disk space
  - Implement fixes: index addition, query rewrite, vacuum tuning, connection pool sizing
  - Perform online schema change with zero downtime
  - Execute point-in-time recovery after simulated data corruption
  - Document incident response and post-mortem
- **Deliverable:** Incident response log, diagnostic analysis, fix implementation, post-mortem document

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Distributed SQL Database
- **Scope:** Build a CockroachDB/TiDB-like distributed SQL database
- **Components:**
  - Raft-based consensus for metadata and data ranges
  - Distributed transaction support (2PC or Percolator-style)
  - Cost-based query optimizer
  - Range-based partitioning with automatic rebalancing
  - SQL parser and executor (subset)
  - Online schema changes
  - Jepsen-style consistency testing
- **Deliverables:** Working system, formal consistency analysis, performance benchmarks, architecture document

### Capstone B: Production Feature Store
- **Scope:** Build a multi-tenant feature store for ML pipelines
- **Components:**
  - Online store (Redis) for low-latency serving
  - Offline store (PostgreSQL/data warehouse) for training
  - Feature registry with versioning and lineage
  - Point-in-time correct joins for training data
  - Real-time feature computation pipeline
  - Access control and multi-tenant isolation
  - Monitoring and drift detection
- **Deliverables:** Working platform, performance benchmarks, data quality report, cost analysis

### Capstone C: Vector Database Engine
- **Scope:** Build a high-performance vector search engine
- **Components:**
  - HNSW or IVF index implementation
  - Metadata filtering with bitmap indexes
  - Hybrid search (dense + sparse)
  - Incremental index updates
  - Persistence and crash recovery
  - Distributed sharding for scale-out
  - Benchmark against FAISS and pgvector
- **Deliverables:** Working engine, recall/latency benchmarks, scalability analysis, architecture document

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 20% | Code quality, correctness, performance |
| Lab reports | 10% | Design decisions, profiling, formal proofs |
| Peer review | 10% | Reviewing others' designs and code |

### Examinations (30%)
- **Midterm (15%):** Relational algebra, indexing, transaction theory
- **Final (15%):** Distributed databases, vector search, production operations

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 10% |
| System design & architecture | 10% |
| Performance & scalability | 5% |
| Operations & reliability | 3% |
| Documentation & presentation | 2% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel algorithms, production-ready, formal proofs
- **B (80-89):** Solid understanding, minor gaps, good engineering
- **C (70-79):** Adequate understanding, significant gaps, needs improvement
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding

---

## Recommended Tools, Libraries & Infrastructure

### Relational Databases
| Tool | Purpose |
|------|---------|
| **PostgreSQL 16+** | Primary relational database |
| **MySQL 8+ / MariaDB** | Alternative relational |
| **SQLite** | Embedded, testing, local-first |
| **CockroachDB** | Distributed SQL |
| **YugabyteDB** | Distributed SQL (PostgreSQL-compatible) |
| **TiDB** | HTAP distributed SQL |

### NoSQL
| Tool | Purpose |
|------|---------|
| **Redis** | In-memory data structures, caching |
| **MongoDB** | Document store |
| **Cassandra** | Wide-column, time-series |
| **ScyllaDB** | High-performance Cassandra |
| **Neo4j** | Graph database |
| **TigerGraph** | Native parallel graph |

### Vector Databases
| Tool | Purpose |
|------|---------|
| **Pinecone** | Managed vector search |
| **Weaviate** | Vector + semantic |
| **Milvus** | Open vector database |
| **pgvector** | PostgreSQL extension |
| **Chroma** | Embedded vector store |
| **Redis Vector** | In-memory vector search |

### Analytics
| Tool | Purpose |
|------|---------|
| **ClickHouse** | Columnar OLAP |
| **DuckDB** | Embedded analytical |
| **Apache Druid** | Real-time analytics |
| **TimescaleDB** | Time-series on PostgreSQL |
| **InfluxDB** | Time-series metrics |

### Tools
| Tool | Purpose |
|------|---------|
| **pgAdmin / DBeaver** | Database administration |
| **psql / mysql** | Command-line clients |
| **pgbench / sysbench** | Benchmarking |
| **Jepsen** | Distributed correctness testing |
| **Liquibase / Flyway** | Schema migrations |
| **Debezium** | Change Data Capture |

---

## References & Further Reading

### Relational Theory
1. **Codd,** "A Relational Model of Data for Large Shared Data Banks" — The original paper
2. **Date,** *An Introduction to Database Systems* (8th Ed.) — Comprehensive theory
3. **Garcia-Molina, Ullman, Widom,** *Database Systems: The Complete Book* — Modern comprehensive text
4. **Abiteboul, Hull, Vianu,** *Foundations of Databases* — Formal foundations

### Transaction Processing
1. **Gray & Reuter,** *Transaction Processing: Concepts and Techniques* — The classic
2. **Mohan et al.,** "ARIES: A Transaction Recovery Method Supporting Fine-Granularity Locking and Partial Rollbacks" — ARIES paper
3. **Berenson et al.,** "A Critique of ANSI SQL Isolation Levels" — Isolation levels critique

### Query Optimization
1. **Selinger et al.,** "Access Path Selection in a Relational Database Management System" — System R paper
2. **Graefe,** "The Cascades Framework for Query Optimization" — Cascades optimizer

### Distributed Databases
1. **DeCandia et al.,** "Dynamo: Amazon's Highly Available Key-value Store" — Dynamo paper
2. **Corbett et al.,** "Spanner: Google's Globally-Distributed Database" — Spanner paper
3. **Lakshman & Malik,** "Cassandra: A Decentralized Structured Storage System" — Cassandra paper
4. **Taft et al.,** "CockroachDB: The Resilient Geo-Distributed SQL Database" — CockroachDB paper

### Vector Databases
1. **Malkov & Yashunin,** "Efficient and Robust Approximate Nearest Neighbor Search Using Hierarchical Navigable Small World Graphs" — HNSW paper
2. **Jégou et al.,** "Product Quantization for Nearest Neighbor Search" — PQ paper
3. **Subramanya et al.,** "DiskANN: Fast Accurate Billion-point Nearest Neighbor Search on a Single Node" — DiskANN paper

### Production Operations
1. **Beyer et al.,** *Site Reliability Engineering* — Google SRE book
2. **PostgreSQL documentation** — The gold standard for open-source docs
3. **MySQL Internals Manual** — Storage engine details

---

## Appendix A: PostgreSQL Configuration for Production

```ini
# Memory
shared_buffers = 25% of RAM
effective_cache_size = 75% of RAM
work_mem = 256MB (per operation)
maintenance_work_mem = 1GB

# WAL
wal_buffers = 16MB
checkpoint_completion_target = 0.9
max_wal_size = 4GB
min_wal_size = 1GB

# Connections
max_connections = 200 (use PgBouncer for more)

# Query planning
random_page_cost = 1.1 (for SSD)
effective_io_concurrency = 200 (for SSD)

# Logging
log_min_duration_statement = 1000
log_checkpoints = on
log_connections = on
log_disconnections = on
```

## Appendix B: Isolation Level Anomaly Matrix

| Isolation Level | Dirty Read | Non-Repeatable | Phantom | Write Skew |
|-----------------|------------|----------------|---------|------------|
| READ UNCOMMITTED | ✗ | ✓ | ✓ | ✓ |
| READ COMMITTED | ✓ | ✓ | ✓ | ✓ |
| REPEATABLE READ | ✓ | ✗ | ✗* | ✓ |
| SERIALIZABLE | ✓ | ✗ | ✗ | ✗ |

*PostgreSQL REPEATABLE READ prevents phantoms; MySQL/InnoDB does not

## Appendix C: Consistency Model Hierarchy

```
Linearizability → Sequential Consistency → Causal Consistency → Eventual Consistency
     ↑                    ↑                      ↑
  Strongest           Program order           Causal order
```

## Appendix D: Production Checklist

Before deploying any database to production, verify:

- [ ] **Schema:** Normalized to appropriate level, indexes designed for workload, constraints enforced
- [ ] **Performance:** Query plans reviewed, slow queries optimized, connection pool sized
- [ ] **Reliability:** Backups configured and tested, PITR enabled, replication verified
- [ ] **Monitoring:** Key metrics instrumented, alerts configured, dashboards ready
- [ ] **Security:** Access control, encryption at rest and in transit, audit logging
- [ ] **Scalability:** Partitioning strategy, read replicas, sharding plan documented
- [ ] **Operations:** Runbooks written, on-call rotation, incident response tested
- [ ] **Recovery:** RTO/RPO defined, DR tested, cross-region replication verified

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: database-design-syllabus.md