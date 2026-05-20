  
  
 ## File: data-engineering-syllabus.md

# Data Engineering for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** MLOps and AIOps (or equivalent), Database Design (or equivalent), Cloud Computing and DevOps (or equivalent), strong SQL proficiency, distributed systems fundamentals, Python/Scala/Java programming experience  
**Estimated Duration:** 260–320 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: The Data Engineering Paradigm — From Raw Data to Intelligence](#module-0-the-data-engineering-paradigm--from-raw-data-to-intelligence)
4. [Module 1: Data Ingestion — Batch, Streaming, and Change Data Capture](#module-1-data-ingestion--batch-streaming-and-change-data-capture)
5. [Module 2: Data Storage — Lakehouse, Warehouse, and Specialized Formats](#module-2-data-storage--lakehouse-warehouse-and-specialized-formats)
6. [Module 3: Data Processing — ETL, ELT, and Stream Processing at Scale](#module-3-data-processing--etl-elt-and-stream-processing-at-scale)
7. [Module 4: Data Quality, Validation, and Observability](#module-4-data-quality-validation-and-observability)
8. [Module 5: Data Modeling — Dimensional, Data Vault, and Graph](#module-5-data-modeling--dimensional-data-vault-and-graph)
9. [Module 6: Workflow Orchestration and Pipeline Engineering](#module-6-workflow-orchestration-and-pipeline-engineering)
10. [Module 7: Real-Time Data Systems — Streaming, Kappa, and Event-Driven Architecture](#module-7-real-time-data-systems--streaming-kappa-and-event-driven-architecture)
11. [Module 8: Data Governance, Lineage, and Metadata Management](#module-8-data-governance-lineage-and-metadata-management)
12. [Module 9: ML Data Engineering — Feature Pipelines, Training Data, and Data-Centric AI](#module-9-ml-data-engineering--feature-pipelines-training-data-and-data-centric-ai)
13. [Module 10: Performance Engineering, Cost Optimization, and SRE for Data](#module-10-performance-engineering-cost-optimization-and-sre-for-data)
14. [Module 11: Emerging Frontiers — Data Mesh, Data Contracts, and AI-Native Data Systems](#module-11-emerging-frontiers--data-mesh-data-contracts-and-ai-native-data-systems)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Data Engineering** not as a pipeline-building craft, but as a **systems engineering discipline for transforming raw data into trustworthy, accessible, and actionable assets at scale**. The pedagogical approach follows a **Ingest → Store → Process → Validate → Serve → Govern** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Ingest** | Batch, streaming, CDC, API extraction — reliability, ordering, exactly-once | Trustworthy data arrival |
| **Store** | Lakehouse, warehouse, object storage, specialized formats — cost, performance, evolution | Accessible data assets |
| **Process** | ETL/ELT, stream processing, transformation logic — correctness, idempotency, scale | Clean, transformed data |
| **Validate** | Quality checks, schema enforcement, anomaly detection, lineage | Verified data integrity |
| **Serve** | Query optimization, API exposure, feature extraction, caching | Consumable data products |
| **Govern** | Cataloging, lineage, access control, compliance, lifecycle management | Governed data estate |

**Core Principles:**
- **Data is not oil — it is a liability until proven otherwise.** We teach data engineering as risk management: every byte ingested carries storage cost, compliance burden, and quality risk. The engineer's job is to maximize value while minimizing liability.
- **Schema is a contract, not a suggestion.** We enforce schema at ingestion, validate at transformation, and monitor at serving. Schema evolution is a first-class engineering concern with backward/forward compatibility guarantees.
- **Batch and streaming are not separate worlds — they are unified by time.** We study the Kappa architecture, unified batch/stream processing, and event time semantics as the modern paradigm, not as theoretical ideals.
- **Data quality is not a step — it is a continuous property.** We embed quality checks at every stage, from source to sink, with automated remediation and human escalation paths.
- **ML data engineering is data engineering with statistical requirements.** Feature pipelines, training data generation, and data-centric AI require all classical data engineering skills plus statistical rigor, point-in-time correctness, and leakage prevention.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Data Engineering Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | Build ETL pipelines, design star schemas, basic Spark, simple orchestration | Team data engineering |
| **Advanced** | Design lakehouse architectures, stream processing, CDC, data quality frameworks | Platform data engineering |
| **Expert** | Design data platforms, custom storage formats, real-time systems, cost optimization | Data infrastructure leadership |
| **Distinguished** | Define organizational data strategy, shape industry standards, invent new abstractions | Technical leadership |

### Streaming and Real-Time Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | Kafka consumers, basic Flink, windowed aggregations | Simple stream processing |
| **Advanced** | Exactly-once processing, stateful operations, event time semantics, backpressure | Production streaming |
| **Expert** | Custom stream processors, watermark design, late data handling, streaming SQL | Streaming platform engineering |
| **Distinguished** | Design next-generation stream processing systems, challenge batch assumptions | Research engineering |

### ML Data Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | Feature extraction, training data pipelines, basic feature stores | ML data pipelines |
| **Advanced** | Point-in-time correctness, data leakage prevention, training-serving skew detection | ML platform engineering |
| **Expert** | Custom feature computation, data-centric AI, synthetic data generation, data valuation | AI data infrastructure |
| **Distinguished** | Design data systems for foundation models, multi-modal data, AI-native storage | AI research engineering |

### Cross-Cutting Competencies
- **Systems:** Design pipelines processing 1PB+/day with <1 hour latency
- **Economic reasoning:** Storage tiering, compute optimization, TCO analysis for data estates
- **Operational reasoning:** Pipeline SLOs, data freshness monitoring, incident response for data outages
- **Governance reasoning:** Data contracts, lineage, compliance, privacy-preserving engineering

---

## Module 0: The Data Engineering Paradigm — From Raw Data to Intelligence

**Duration:** 15 hours  
**Purpose:** Establish the foundational mindset and map the modern data landscape

### 0.1 The Data Engineering Lifecycle
- **Generation → Ingestion → Storage → Processing → Serving → Analytics → Archival:** The complete flow
- **Data maturity model:** Ad-hoc → warehouse → lake → lakehouse → data mesh → data product
- **The data engineer's role:** Not "plumber" but "architect of trust" — ensuring data is correct, timely, accessible, and governed
- **Production connection:** Why data engineering is the bottleneck for most AI initiatives; why "data is the new oil" is dangerously wrong

### 0.2 Data Systems vs. Software Systems
- **Immutability:** Append-only logs, immutable data, versioned datasets — why mutation is the enemy
- **Time as a first-class dimension:** Event time, processing time, ingestion time, effective time — why event time is the only true time
- **Schema evolution:** Backward compatibility, forward compatibility, full compatibility, breaking changes
- **Idempotency and determinism:** Why data pipelines must be replayable, why non-determinism destroys trust
- **Production connection:** Why immutable data lakes enable time travel; why schema evolution is harder than API versioning; why idempotency is non-negotiable

### 0.3 The Modern Data Stack
- **Ingestion:** Fivetran, Airbyte, Debezium, Kafka, Kinesis
- **Storage:** S3, Delta Lake, Iceberg, Hudi, Snowflake, BigQuery
- **Transformation:** dbt, Spark, Flink, dbt + Spark
- **Orchestration:** Airflow, Prefect, Dagster, Temporal
- **Serving:** Feature stores, reverse ETL, APIs, BI tools
- **Governance:** DataHub, Collibra, Monte Carlo, Great Expectations
- **Production connection:** Evaluating the modern data stack; when managed services beat self-hosted; when to build vs. buy

### 0.4 Data Engineering for AI/ML
- **Training data requirements:** Volume, variety, velocity, veracity, valuation
- **Feature engineering pipelines:** Batch, real-time, on-demand — consistency challenges
- **Data leakage:** Temporal contamination, target leakage, lookahead bias — prevention strategies
- **Data-centric AI:** Data quality > model complexity, data valuation, active learning, synthetic data
- **Production connection:** Why 80% of ML effort is data preparation; why data leakage is the silent killer; why data-centric AI is the future

### 0.5 Lab: Data Engineering Maturity Assessment
- **Task:** Assess an organization's data engineering maturity
- **Requirements:**
  - Evaluate across dimensions: ingestion, storage, processing, quality, serving, governance
  - Interview data consumers (analysts, data scientists, product managers)
  - Identify data debt and technical debt
  - Create prioritized roadmap with business case
  - Define metrics for maturity progression
- **Deliverable:** Maturity assessment report, gap analysis, roadmap, business case

---

## Module 1: Data Ingestion — Batch, Streaming, and Change Data Capture

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 1.1 Batch Ingestion Patterns
- **Extract patterns:** Full extract, incremental extract (timestamp, auto-increment, checksum), delta extract
- **Load patterns:** Truncate-and-load, merge/upsert, SCD Type 1/2/3, partition swap
- **File-based ingestion:** CSV, JSON, Parquet, Avro — parsing, validation, schema inference
- **API ingestion:** REST, GraphQL, webhooks — rate limiting, pagination, backoff, idempotency
- **Production connection:** Why incremental extract beats full extract; why SCD Type 2 is essential for analytics; why API ingestion needs circuit breakers

### 1.2 Streaming Ingestion
- **Kafka producers:** Batching, compression, acks, idempotency, transactional producers
- **Kafka consumers:** Consumer groups, partition assignment, offset management, rebalancing
- **Exactly-once semantics:** Idempotent producers, transactions, EOS, two-phase commit
- **Backpressure and flow control:** Consumer prefetch, rate limiting, credit-based flow control
- **Production connection:** Kafka as the central nervous system; exactly-once as "exactly-once processing"; backpressure for preventing consumer overload

### 1.3 Change Data Capture (CDC)
- **CDC patterns:** Query-based (timestamp polling), trigger-based, log-based (binlog, WAL, redo log)
- **Debezium:** Kafka Connect source, database connectors, snapshotting, streaming changes
- **CDC challenges:** Schema changes, DDL events, large transactions, initial snapshots, ordering guarantees
- **Production connection:** Debezium for real-time CDC; why log-based CDC is the only correct approach; handling schema changes in CDC streams

### 1.4 Data Ingestion at Scale
- **Parallel ingestion:** Partitioning, sharding, multi-threaded extract, batch sizing
- **Error handling:** Dead letter queues, retry policies, quarantine, alerting
- **Schema on read vs. schema on write:** Trade-offs, evolution strategies, enforcement points
- **Production connection:** Parallel ingestion for large tables; dead letter queues for poison pills; schema enforcement points for data contracts

### 1.5 Lab: Building a Resilient Data Ingestion Platform
- **Task:** Build a platform ingesting from 10+ sources with varying reliability
- **Requirements:**
  - Batch ingestion from databases (full and incremental)
  - Streaming ingestion from Kafka
  - CDC from PostgreSQL with Debezium
  - API ingestion with rate limiting and backoff
  - Schema validation at ingestion
  - Dead letter queue for bad records
  - Exactly-once processing guarantees
  - Monitoring: ingestion lag, error rate, throughput
  - Benchmark: 1M records/minute with <0.1% loss
- **Deliverable:** Working platform, architecture document, failure mode analysis, performance benchmarks

---

## Module 2: Data Storage — Lakehouse, Warehouse, and Specialized Formats

**Duration:** 30 hours  
**Level:** Advanced

### 2.1 Object Storage as the Foundation
- **S3 architecture:** Buckets, keys, consistency model, multipart upload, versioning, lifecycle
- **Performance characteristics:** Request rate limits, prefix parallelism, transfer acceleration
- **Cost optimization:** Storage classes (Standard, IA, Glacier), Intelligent-Tiering, lifecycle policies
- **Production connection:** S3 as the universal storage layer; prefix design for parallelism; Intelligent-Tiering for cost optimization

### 2.2 Columnar File Formats
- **Parquet:** Row groups, column chunks, page headers, dictionary encoding, predicate pushdown
- **ORC:** Stripe, row group, index, bloom filter, ACID transactions (Hive ACID)
- **Avro:** Row-based, schema evolution, RPC, serialization — when and why
- **Arrow:** In-memory columnar, zero-copy, language-agnostic, IPC format
- **Production connection:** Parquet for analytics (universal standard); Arrow for in-memory processing; Avro for streaming serialization

### 2.3 Lakehouse Architectures
- **Delta Lake:** ACID transactions, time travel, schema enforcement, Z-ordering, liquid clustering, predictive I/O
- **Apache Iceberg:** Hidden partitioning, partition evolution, time travel, schema evolution, table branching
- **Apache Hudi:** Copy-on-write vs. merge-on-read, incremental processing, compaction, clustering
- **Comparison:** Write performance, read performance, ecosystem, vendor support, community
- **Production connection:** Delta Lake for Databricks ecosystem; Iceberg for open multi-engine; Hudi for incremental processing; choosing based on query patterns

### 2.4 Data Warehouses and Query Engines
- **Snowflake:** Separation of storage and compute, virtual warehouses, zero-copy cloning, time travel, data sharing
- **BigQuery:** Serverless, columnar storage, Dremel execution, materialized views, BI Engine
- **Databricks SQL:** Photon engine, liquid clustering, predictive I/O, serverless
- **ClickHouse / DuckDB:** Columnar OLAP, embedded analytics, high-performance single-node
- **Production connection:** Snowflake for enterprise analytics; BigQuery for GCP-native; ClickHouse for real-time analytics; DuckDB for local/embedded

### 2.5 Specialized Storage for AI/ML
- **Training datasets:** WebDataset, TFRecord, HDF5, LMDB — format selection for throughput
- **Embedding storage:** Vector databases, pgvector, FAISS, approximate nearest neighbor indexes
- **Graph storage:** RDF stores, property graph databases, adjacency formats for GNN training
- **Time-series storage:** TimescaleDB, InfluxDB, Prometheus — retention, downsampling, aggregation
- **Production connection:** WebDataset for high-throughput training; vector databases for RAG; time-series for feature engineering

### 2.6 Lab: Designing a Lakehouse Architecture
- **Task:** Design a lakehouse for a data-intensive organization
- **Requirements:**
  - Raw zone (bronze), cleaned zone (silver), curated zone (gold)
  - Delta Lake or Iceberg for ACID and time travel
  - Parquet as the standard format
  - Z-ordering or liquid clustering for query optimization
  - Partitioning strategy (time-based, category-based)
  - Schema evolution handling
  - Cost optimization: storage tiering, compaction, vacuum
  - Integration with Spark, Trino/Presto, and Python
  - Benchmark: query 1TB in <10 seconds
- **Deliverable:** Architecture document, table designs, performance benchmarks, cost analysis

---

## Module 3: Data Processing — ETL, ELT, and Stream Processing at Scale

**Duration:** 30 hours  
**Level:** Advanced

### 3.1 ETL vs. ELT and Modern Transformations
- **ETL:** Extract-Transform-Load — traditional, schema-on-write, heavy transformation before storage
- **ELT:** Extract-Load-Transform — modern, schema-on-read, transform in warehouse/lakehouse
- **EtLT:** Extract, minor Transform, Load, major Transform — hybrid for streaming
- **Transformation frameworks:** dbt (SQL-based), Spark (code-based), Flink (stream-based), Trino (SQL-based)
- **Production connection:** dbt for warehouse transformations; Spark for complex data processing; why ELT dominates modern architectures

### 3.2 Apache Spark Deeply
- **Spark architecture:** Driver, executors, tasks, stages, DAG, lineage
- **RDDs vs. DataFrames vs. Datasets:** Type safety, optimization, API evolution
- **Catalyst optimizer:** Logical plan, physical plan, cost-based optimization, adaptive query execution
- **Tungsten:** Code generation, off-heap memory, cache-friendly binary format
- **Spark SQL:** Hive integration, UDFs, window functions, joins, bucketing
- **Structured Streaming:** Micro-batch, continuous processing, event time, watermarks, output modes
- **Production connection:** Catalyst for query optimization; Tungsten for performance; Structured Streaming for unified batch/stream; why Spark remains the workhorse

### 3.3 Apache Flink for Stream Processing
- **Flink architecture:** JobManager, TaskManager, slots, checkpointing, savepoints
- **DataStream API:** Sources, transformations, sinks, stateful operations, keyed streams
- **Table API and SQL:** Unified batch/stream SQL, temporal tables, window aggregations
- **Checkpointing and exactly-once:** Barriers, state snapshots, incremental checkpoints, asynchronous snapshots
- **Production connection:** Flink for complex event processing; exactly-once for financial streams; why Flink beats Spark Streaming for low latency

### 3.4 dbt and SQL-Based Transformation
- **dbt models:** SQL files, materialization (table, view, incremental, ephemeral), refs, sources
- **dbt tests:** Schema tests, custom tests, singular tests, severity, store failures
- **dbt snapshots:** SCD Type 2, timestamp strategy, check strategy, invalidate hard deletes
- **dbt macros and packages:** Jinja templating, reusable logic, package ecosystem
- **Production connection:** dbt for analytics engineering; tests as data quality gates; snapshots for slowly changing dimensions

### 3.5 Lab: Building a Unified Batch-Stream Processing Platform
- **Task:** Build a platform supporting both batch and real-time transformations
- **Requirements:**
  - Spark for batch processing (daily, hourly)
  - Flink for stream processing (real-time)
  - dbt for warehouse transformations
  - Unified data model across batch and stream
  - Exactly-once processing for both
  - Schema enforcement and evolution
  - Data quality checks at each stage
  - Monitoring: throughput, latency, error rate, data freshness
  - Benchmark: batch 10TB/hour, stream 100K events/sec
- **Deliverable:** Working platform, architecture document, performance benchmarks, quality report

---

## Module 4: Data Quality, Validation, and Observability

**Duration:** 25 hours  
**Level:** Advanced

### 4.1 Data Quality Dimensions
- **Completeness:** Missing values, null rates, coverage, expected volume
- **Uniqueness:** Duplicate detection, primary key violations, fuzzy matching
- **Validity:** Format checks, range checks, regex, referential integrity, business rules
- **Timeliness:** Freshness, latency, staleness, SLA compliance
- **Consistency:** Cross-field, cross-table, cross-system, temporal consistency
- **Accuracy:** Ground truth comparison, statistical validation, business impact
- **Production connection:** Why data quality is multi-dimensional; why accuracy is the hardest to measure; why timeliness has direct business impact

### 4.2 Data Validation Frameworks
- **Great Expectations:** Expectation suites, batch validation, checkpoint, documentation, profiling
- **Deequ:** Constraint suggestion, metrics computation, anomaly detection, incremental validation
- **Soda Core:** Checks as code, self-serve data quality, anomaly detection, incident management
- **Custom validation:** Schema validation, statistical tests, business rule engines, ML-based anomaly detection
- **Production connection:** Great Expectations for pipeline gates; Deequ for large-scale data quality; Soda for self-serve; custom for domain-specific rules

### 4.3 Data Observability
- **Pillars:** Freshness, volume, schema, distribution, lineage, quality
- **Tools:** Monte Carlo, Bigeye, Metaplane, Anomalo, custom solutions
- **Anomaly detection:** Statistical methods, ML methods, baseline learning, seasonality
- **Root cause analysis:** Lineage-driven, correlation analysis, impact assessment
- **Production connection:** Monte Carlo for managed observability; custom for specific domains; why data observability is the new data quality

### 4.4 Data Testing and CI/CD for Data
- **Unit tests for data:** Row counts, null rates, distribution checks, relationship tests
- **Integration tests:** End-to-end pipeline tests, sample data tests, staging environment tests
- **Data diffing:** Comparing datasets across environments, regression testing for transformations
- **Production connection:** Data testing in CI/CD; why data pipelines need the same rigor as software; data diffing for migration validation

### 4.5 Lab: Building a Data Quality Platform
- **Task:** Build a comprehensive data quality and observability system
- **Requirements:**
  - Great Expectations or Deequ for validation
  - Custom anomaly detection for metrics
  - Data freshness monitoring with SLAs
  - Schema drift detection and alerting
  - Volume anomaly detection
  - Distribution drift monitoring
  - Lineage-driven root cause analysis
  - Integration with Slack/PagerDuty for alerting
  - Dashboard: quality score, anomaly timeline, impact analysis
  - Benchmark: detect quality issues within 5 minutes
- **Deliverable:** Working platform, quality dashboard, anomaly detection accuracy, incident response demo

---

## Module 5: Data Modeling — Dimensional, Data Vault, and Graph

**Duration:** 20 hours  
**Level:** Advanced

### 5.1 Dimensional Modeling
- **Star schema:** Fact tables, dimension tables, surrogate keys, degenerate dimensions
- **Snowflake schema:** Normalized dimensions, space savings, query complexity
- **Slowly Changing Dimensions (SCD):** Type 0 (fixed), Type 1 (overwrite), Type 2 (history), Type 3 (previous value), Type 4 (mini-dimension), Type 6 (hybrid)
- **Fact table types:** Transaction, periodic snapshot, accumulating snapshot, factless fact
- **Production connection:** Star schema for BI performance; SCD Type 2 for historical tracking; accumulating snapshot for order fulfillment

### 5.2 Data Vault 2.0
- **Hubs:** Business keys, hash keys, load dates, record sources
- **Links:** Relationships, link hashes, hub references, effectivity satellites
- **Satellites:** Descriptive data, hash differences, load dates, expiration dates
- **Point-in-time (PIT) tables:** Pre-joined views for performance, bridge tables for many-to-many
- **Production connection:** Data Vault for enterprise data warehouses; agility for schema changes; auditability for compliance

### 5.3 Graph Data Modeling
- **Property graph model:** Nodes, relationships, properties, labels, direction
- **RDF and triple stores:** Subject-predicate-object, ontologies, SPARQL, linked data
- **Graph schema design:** Node types, relationship types, property modeling, supernodes
- **Production connection:** Property graphs for recommendations; RDF for knowledge graphs; graph modeling for GNN training data

### 5.4 Lab: Designing a Multi-Model Data Warehouse
- **Task:** Design a warehouse supporting dimensional, Data Vault, and graph queries
- **Requirements:**
  - Star schema for BI reporting
  - Data Vault for raw data integration and audit
  - Graph model for relationship analytics
  - ETL/ELT pipelines between models
  - Point-in-time correctness for all models
  - Performance: BI queries <5s, graph queries <2s
  - Documentation: entity-relationship, Data Vault diagram, graph schema
- **Deliverable:** Design document, schema definitions, ETL logic, performance projections

---

## Module 6: Workflow Orchestration and Pipeline Engineering

**Duration:** 25 hours  
**Level:** Advanced

### 6.1 Apache Airflow
- **Architecture:** Scheduler, webserver, metadata database, executor (Local, Celery, Kubernetes), workers
- **DAG design:** Tasks, operators, sensors, hooks, XComs, task groups, dynamic task mapping
- **Best practices:** Idempotency, atomicity, retries, timeouts, SLA misses, backfill, catchup
- **Production connection:** Airflow as the industry standard; why KubernetesExecutor beats Celery for scaling; why DAG design matters for maintainability

### 6.2 Modern Orchestrators
- **Prefect:** Modern Python-native, dynamic workflows, hybrid execution, flow-based
- **Dagster:** Software-defined assets, data-aware orchestration, type safety, observability-first
- **Temporal:** Durable execution, workflow-as-code, fault tolerance, long-running workflows
- **Mage:** Data pipeline tool, integrated transformation, real-time and batch
- **Production connection:** Prefect for modern Python teams; Dagster for data-aware pipelines; Temporal for long-running, fault-tolerant workflows

### 6.3 Pipeline Patterns and Anti-Patterns
- **Patterns:** Fan-out/fan-in, branching, conditional execution, dynamic generation, sensor-based triggering
- **Anti-patterns:** Monolithic DAGs, hardcoded dates, untested transformations, missing idempotency, XCom abuse
- **Data lineage in orchestration:** Task-level lineage, dataset-level lineage, impact analysis
- **Production connection:** Why small, focused DAGs beat monolithic ones; why idempotency is non-negotiable; why lineage must be automatic

### 6.4 Lab: Building a Production Orchestration Platform
- **Task:** Build a platform orchestrating 100+ data pipelines
- **Requirements:**
  - Airflow or Dagster for orchestration
  - Dynamic task generation for variable workloads
  - Sensor-based triggering (file arrival, API callback)
  - Retry policies with exponential backoff
  - SLA monitoring and alerting
  - Backfill capability
  - Data lineage integration
  - Cost tracking per pipeline
  - Multi-environment promotion (dev → staging → prod)
  - Benchmark: 1000+ tasks/day, 99.9% success rate
- **Deliverable:** Working platform, DAG examples, lineage visualization, cost report, SLA dashboard

---

## Module 7: Real-Time Data Systems — Streaming, Kappa, and Event-Driven Architecture

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 7.1 The Kappa Architecture
- **Unified processing:** Single stream processing layer for both real-time and batch
- **Event log as source of truth:** Immutable, ordered, replayable, the "data lake" for streaming
- **Reprocessing:** Replaying historical events, schema evolution during replay, backfilling
- **Production connection:** Why Kappa beats Lambda for simplicity; why event logs are the true source of truth; reprocessing for schema migration

### 7.2 Stream-Table Duality
- **Tables as materialized views of streams:** Aggregation, projection, join, windowing
- **Streams as changelog of tables:** CDC, event sourcing, state changes
- **Materialized views:** Incremental maintenance, refresh strategies, consistency
- **Production connection:** Kafka Streams for stream-table duality; Flink for complex materialized views; why this duality simplifies architecture

### 7.3 Event Time and Watermarks
- **Event time vs. processing time:** Why processing time is a lie, why event time is the truth
- **Watermarks:** Bounded lateness, punctuated watermarks, periodic watermarks, idle timeouts
- **Late data handling:** Side outputs, allowed lateness, retraction, updating results
- **Production connection:** Watermarks for bounded out-of-orderness; why late data is inevitable; side outputs for analytics

### 7.4 Stateful Stream Processing
- **State backends:** Memory, filesystem, RocksDB, incremental checkpoints
- **State types:** Value state, list state, map state, reducing state, aggregating state
- **State TTL:** Time-to-live, cleanup strategies, state size management
- **Production connection:** RocksDB for large state; incremental checkpoints for fast recovery; TTL for state cleanup

### 7.5 Lab: Building a Real-Time Analytics Platform
- **Task:** Build a Kappa architecture platform for real-time analytics
- **Requirements:**
  - Kafka as the event log (source of truth)
  - Flink for stream processing
  - Stream-table duality with materialized views
  - Event time processing with watermarks
  - Stateful operations with RocksDB
  - Exactly-once processing
  - Real-time dashboard (Grafana or custom)
  - Reprocessing capability for backfilling
  - Benchmark: 1M events/sec, <5s end-to-end latency
- **Deliverable:** Working platform, architecture document, watermark analysis, state management report, performance benchmarks

---

## Module 8: Data Governance, Lineage, and Metadata Management

**Duration:** 20 hours  
**Level:** Advanced

### 8.1 Data Governance Framework
- **Policies:** Data quality, access control, retention, privacy, classification
- **Roles:** Data owners, stewards, custodians, consumers, governance committee
- **Processes:** Approval workflows, impact assessment, change management, audit
- **Production connection:** Data governance as enabler, not blocker; why roles matter more than tools; why governance fails without executive sponsorship

### 8.2 Data Catalogs and Metadata Management
- **DataHub:** LinkedIn's metadata platform, ingestion, search, lineage, impact analysis
- **Apache Atlas:** Hadoop ecosystem, classification, lineage, security, governance
- **Collibra / Alation:** Enterprise data catalogs, business glossary, data marketplace
- **OpenMetadata:** Unified metadata platform, data quality, profiling, collaboration
- **Production connection:** DataHub for open-source metadata; Collibra for enterprise governance; why searchability is the killer feature

### 8.3 Data Lineage
- **Lineage types:** Table-level, column-level, transformation-level, end-to-end, business lineage
- **Automated lineage:** SQL parsing, Spark lineage, Airflow lineage, OpenLineage standard
- **Impact analysis:** Upstream changes, downstream consumers, blast radius, change notification
- **Production connection:** OpenLineage for pipeline lineage; column-level lineage for GDPR; impact analysis for safe schema changes

### 8.4 Data Privacy and Compliance
- **GDPR:** Right to erasure, data portability, consent, privacy by design
- **CCPA/CPRA:** Consumer rights, opt-out, data sale, sensitive data
- **HIPAA:** PHI, minimum necessary, access controls, audit trails
- **Data masking:** Static masking, dynamic masking, format-preserving encryption, tokenization
- **Production connection:** Privacy by design for data pipelines; dynamic masking for analytics; tokenization for PCI compliance

### 8.5 Lab: Building a Data Governance Platform
- **Task:** Build a governance platform with catalog, lineage, and compliance
- **Requirements:**
  - Data catalog with search and discovery
  - Automated lineage collection (OpenLineage)
  - Data classification (PII, sensitive, public)
  - Access control policies
  - Data quality scorecards
  - Retention policies and automated enforcement
  - Privacy compliance reporting
  - Integration with data pipelines
  - Dashboard: governance metrics, compliance status, lineage map
- **Deliverable:** Working platform, catalog demo, lineage visualization, compliance report

---

## Module 9: ML Data Engineering — Feature Pipelines, Training Data, and Data-Centric AI

**Duration:** 30 hours  
**Level:** Expert

### 9.1 Feature Engineering Pipelines
- **Feature types:** Raw, derived, aggregated, embedded, temporal, geospatial
- **Computation patterns:** Batch (scheduled), real-time (stream), on-demand (request-time)
- **Frameworks:** TFX Transform, Spark MLlib, Feast, custom pipelines
- **Consistency:** Training-serving skew detection, feature validation, backtesting
- **Production connection:** TFX for TensorFlow feature engineering; Feast for feature store integration; why consistency is harder than computation

### 9.2 Point-in-Time Correctness
- **The problem:** Preventing data leakage, using only data available at prediction time
- **Temporal joins:** AS OF joins, event time alignment, lookback windows, rolling windows
- **Feature stores:** Point-in-time correct retrieval, event time indexing, backfilling
- **Production connection:** Why point-in-time correctness is the hardest problem in ML data engineering; why feature stores are essential; backfilling for historical training

### 9.3 Training Data Generation and Management
- **Dataset versioning:** DVC, LakeFS, Delta Lake time travel, dataset registries
- **Sampling strategies:** Random, stratified, time-based, importance sampling, active learning
- **Data augmentation:** Synthetic data, SMOTE, GANs, diffusion models, domain randomization
- **Data valuation:** Shapley values, influence functions, data maps, coreset selection
- **Production connection:** DVC for dataset versioning; active learning for label efficiency; data valuation for cleaning

### 9.4 Data-Centric AI and Data Quality for ML
- **Data-centric vs. model-centric:** Why data quality beats model complexity
- **Data cleaning:** Error detection, outlier removal, label correction, consensus methods
- **Data labeling:** Active learning, weak supervision, programmatic labeling, quality estimation
- **Synthetic data generation:** GANs, VAEs, diffusion models, domain-specific generators, privacy guarantees
- **Production connection:** Why data-centric AI reduces costs; weak supervision for large-scale labeling; synthetic data for rare events

### 9.5 Lab: Building a ML Data Platform
- **Task:** Build a platform for generating, versioning, and serving ML training data
- **Requirements:**
  - Feature engineering pipelines (batch and real-time)
  - Point-in-time correct training set generation
  - Dataset versioning with DVC or LakeFS
  - Training-serving skew detection
  - Data quality validation for ML
  - Synthetic data generation pipeline
  - Integration with feature store
  - Monitoring: feature drift, null rate, distribution changes
  - Benchmark: generate 1M-row training set in <10 minutes
- **Deliverable:** Working platform, point-in-time correctness tests, quality report, skew detection demo

---

## Module 10: Performance Engineering, Cost Optimization, and SRE for Data

**Duration:** 20 hours  
**Level:** Expert

### 10.1 Query Optimization and Performance Tuning
- **Query planning:** EXPLAIN ANALYZE, cost models, join optimization, partition pruning
- **Indexing strategies:** B-tree, bitmap, BRIN, partial, expression indexes
- **Partitioning:** Range, list, hash, composite, partition elimination
- **Clustering:** Z-ordering, liquid clustering, sort keys, distribution keys
- **Production connection:** Partition pruning for time-series; Z-ordering for multi-column filtering; why query optimization is data engineering

### 10.2 Storage Optimization
- **Compaction:** Small file problem, Delta Lake optimize, Iceberg rewrite, Hudi clustering
- **Compression:** Snappy, Zstd, Gzip, LZ4 — speed vs. ratio trade-offs
- **File sizing:** Target file size, coalesce, repartition, adaptive query execution
- **Tiered storage:** Hot, warm, cold, archive — automated policies, retrieval costs
- **Production connection:** Compaction for query performance; Zstd for balanced compression; tiered storage for cost optimization

### 10.3 Compute Optimization
- **Auto-scaling:** Target tracking, step scaling, scheduled scaling, predictive scaling
- **Spot instances:** Bidding strategies, interruption handling, checkpointing, mixed fleets
- **Right-sizing:** Instance type selection, vertical scaling, horizontal scaling, container resource tuning
- **Production connection:** Spot instances for batch processing; auto-scaling for variable workloads; right-sizing for steady-state

### 10.4 Data Pipeline SLOs and Reliability
- **Pipeline SLOs:** Freshness, completeness, latency, quality, cost
- **Error budgets:** Allowable failure rate, burn rate alerts, freeze policies
- **Incident response:** Data pipeline failures, data corruption, schema changes, backfill procedures
- **Production connection:** Data freshness SLOs for real-time pipelines; error budgets for safe deployment; incident response for data corruption

### 10.5 Lab: Optimizing a Data Platform for Cost and Performance
- **Task:** Optimize an existing data platform for 50% cost reduction
- **Requirements:**
  - Analyze current spend by component (storage, compute, transfer)
  - Identify optimization opportunities: compaction, partitioning, right-sizing, spot instances
  - Implement storage tiering and lifecycle policies
  - Optimize query performance with indexing and clustering
  - Implement auto-scaling policies
  - Benchmark before/after: query time, pipeline duration, total cost
  - Document trade-offs and risks
  - Target: 50% cost reduction with <10% performance degradation
- **Deliverable:** Optimization report, implementation details, before/after benchmarks, cost savings analysis

---

## Module 11: Emerging Frontiers — Data Mesh, Data Contracts, and AI-Native Data Systems

**Duration:** 20 hours  
**Level:** Expert

### 11.1 Data Mesh
- **Domain-oriented decentralized data ownership:** Domain teams as data product owners
- **Data as a product:** Discoverable, addressable, trustworthy, self-describing, interoperable
- **Self-serve data infrastructure:** Platform team provides infrastructure, domains provide data
- **Federated computational governance:** Global policies, local autonomy, automated enforcement
- **Production connection:** Zhamak Dehghani's original vision; why Data Mesh fails without platform engineering; why federated governance is the hardest part

### 11.2 Data Contracts
- **Contract definition:** Schema, semantics, SLAs, quality guarantees, ownership, lifecycle
- **Contract enforcement:** Schema registries, CI/CD gates, automated testing, breaking change detection
- **Contract evolution:** Versioning, deprecation, migration, compatibility guarantees
- **Production connection:** Data contracts for API-like data interfaces; schema registries for streaming; why contracts prevent data quality disasters

### 11.3 AI-Native Data Systems
- **Vector-native storage:** Native vector indexes, hybrid search, embedding pipelines
- **Learned query optimization:** Neural cost models, learned indexes, query rewriting
- **Data synthesis:** Synthetic data generation, differential privacy, federated data access
- **Autonomous data management:** Self-tuning, self-healing, self-optimizing data systems
- **Production connection:** Vector-native databases for RAG; learned optimizers for complex queries; synthetic data for privacy-preserving ML

### 11.4 Lab: Designing a Data Mesh Architecture
- **Task:** Design a Data Mesh for a 500+ engineer organization
- **Requirements:**
  - Domain identification and ownership model
  - Data product definition template
  - Self-serve infrastructure platform
  - Federated governance framework
  - Data contracts between domains
  - Discovery and catalog integration
  - Quality and SLA monitoring per domain
  - Cost allocation model
  - Organizational design: platform team, domain teams, governance committee
  - Migration strategy from current centralized model
- **Deliverable:** Architecture document, organizational design, migration roadmap, governance framework, data contract template

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Petabyte-Scale Data Platform
- **Scope:** Build a data platform processing 1PB+/day
- **Components:**
  - Multi-source ingestion (batch, streaming, CDC)
  - Lakehouse storage (Delta Lake or Iceberg)
  - Batch and stream processing (Spark + Flink)
  - Data quality framework with automated remediation
  - Feature store integration
  - Data catalog with automated lineage
  - Cost optimization: tiered storage, spot instances, compaction
  - Governance: data contracts, access control, compliance
  - Monitoring: freshness, quality, cost, lineage
- **Deliverables:** Working platform, architecture document, performance benchmarks, cost analysis, governance framework

### Capstone B: Real-Time ML Feature Platform
- **Scope:** Build a platform for real-time feature computation and serving
- **Components:**
  - Stream ingestion from Kafka
  - Real-time feature computation with Flink
  - Feature store with online and offline stores
  - Point-in-time correct training data generation
  - Training-serving skew detection
  - Feature monitoring: drift, null rate, distribution
  - Integration with model training and serving
  - Latency: <10ms for online features, <1min for batch backfill
- **Deliverables:** Working platform, point-in-time correctness tests, performance benchmarks, quality dashboard

### Capstone C: Data Mesh Implementation
- **Scope:** Design and pilot a Data Mesh for a complex organization
- **Components:**
  - Domain analysis and ownership model
  - 3+ data products with contracts
  - Self-serve infrastructure platform
  - Federated governance with automated enforcement
  - Data catalog with domain-specific views
  - Quality monitoring per domain
  - Cost allocation and showback
  - Organizational change management plan
  - Migration from centralized warehouse
- **Deliverables:** Architecture document, data product specifications, platform design, governance framework, organizational plan, pilot results

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 15% | Working pipelines, platforms, quality systems |
| Architecture documents | 15% | Design docs, data models, governance frameworks |
| Peer review | 10% | Reviewing others' data engineering designs |

### Examinations (30%)
- **Midterm (15%):** Ingestion, storage, processing, data modeling
- **Final (15%):** Streaming, governance, ML data engineering, emerging topics

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 8% |
| Architecture and design | 8% |
| Performance and cost optimization | 5% |
| Governance and compliance | 4% |
| Documentation and presentation | 3% |
| Innovation | 2% |

### Grading Rubric
- **A (90-100):** Publication-quality work, production-ready platform, comprehensive governance, novel contributions
- **B (80-89):** Excellent understanding, minor gaps, strong implementation
- **C (70-79):** Good understanding, significant gaps in advanced topics
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding for expert-level data engineering

---

## Recommended Tools, Libraries & Infrastructure

### Ingestion
| Tool | Purpose |
|------|---------|
| **Apache Kafka** | Event streaming |
| **Debezium** | Change data capture |
| **Apache Flink** | Stream processing |
| **Airbyte / Fivetran** | Managed ingestion |
| **Apache Spark** | Batch processing |

### Storage
| Tool | Purpose |
|------|---------|
| **Delta Lake** | Lakehouse transactions |
| **Apache Iceberg** | Open table format |
| **Apache Hudi** | Incremental processing |
| **Snowflake** | Cloud data warehouse |
| **BigQuery** | Serverless analytics |

### Processing
| Tool | Purpose |
|------|---------|
| **Apache Spark** | Distributed processing |
| **dbt** | SQL transformations |
| **Apache Flink** | Stream processing |
| **Trino / Presto** | Federated query engine |
| **DuckDB** | Embedded analytics |

### Orchestration
| Tool | Purpose |
|------|---------|
| **Apache Airflow** | Workflow orchestration |
| **Prefect** | Modern orchestration |
| **Dagster** | Data-aware orchestration |
| **Temporal** | Durable execution |

### Quality
| Tool | Purpose |
|------|---------|
| **Great Expectations** | Data validation |
| **Deequ** | Data quality at scale |
| **Soda Core** | Checks as code |
| **Monte Carlo** | Data observability |

### Governance
| Tool | Purpose |
|------|---------|
| **DataHub** | Metadata platform |
| **Apache Atlas** | Hadoop governance |
| **OpenMetadata** | Unified metadata |
| **Collibra** | Enterprise catalog |

### ML Data
| Tool | Purpose |
|------|---------|
| **Feast** | Feature store |
| **DVC** | Data versioning |
| **TFX** | TensorFlow extended |
| **LakeFS** | Data lake versioning |

---

## References & Further Reading

### Data Engineering Fundamentals
1. **Reis & Housley,** *Fundamentals of Data Engineering* — Comprehensive modern guide
2. **Kleppmann,** *Designing Data-Intensive Applications* — The definitive systems book
3. **Gorton & Klein,** *Data Engineering with Python* — Practical Python-based DE

### Lakehouse and Modern Storage
1. **Armbrust et al.,** "Lakehouse: A New Generation of Open Platforms that Unify Data Warehousing and Advanced Analytics" — Databricks paper
2. **Delta Lake documentation** — Transactional storage layer
3. **Apache Iceberg documentation** — Open table format

### Streaming
1. **Kreps,** "Questioning the Lambda Architecture" — Kappa architecture
2. **Akidau et al.,** "The Dataflow Model" — Streaming semantics
3. **Flink documentation** — Stream processing

### Data Mesh
1. **Dehghani,** *Data Mesh* — The original book
2. **Dehghani,** "How to Move Beyond a Monolithic Data Lake to a Distributed Data Mesh" — Original article

### Data Quality
1. **Great Expectations documentation** — Data validation
2. **Schelter et al.,** "Unit Testing Data with Deequ" — Amazon paper

### ML Data Engineering
1. **Polyzotis et al.,** "Data Management Challenges in Production Machine Learning" — Google paper
2. **Huyen,** *Designing Machine Learning Systems* — MLOps from first principles

---

## Appendix A: Data Pipeline Checklist

Before any data pipeline goes to production, verify:

- [ ] **Idempotency:** Re-running produces identical results
- [ ] **Schema enforcement:** Input and output schemas validated
- [ ] **Quality checks:** At least 3 quality checks per pipeline
- [ ] **Error handling:** Dead letter queue, retry policy, alerting
- [ ] **Monitoring:** Freshness, volume, error rate, latency
- [ ] **Lineage:** Source to sink tracked
- [ ] **Documentation:** Purpose, schema, dependencies, owner
- [ ] **Cost:** Estimated and budgeted
- [ ] **Security:** Access controls, encryption, PII handling
- [ ] **Rollback:** Procedure documented and tested

## Appendix B: Data Quality Scorecard

| Dimension | Metric | Target | Current | Status |
|-----------|--------|--------|---------|--------|
| Completeness | Null rate | <1% | _____ | _____ |
| Uniqueness | Duplicate rate | <0.1% | _____ | _____ |
| Validity | Schema violation rate | 0% | _____ | _____ |
| Timeliness | Freshness | <1 hour | _____ | _____ |
| Consistency | Cross-system match rate | >99% | _____ | _____ |
| **Overall** | **Quality score** | **>95%** | **_____** | **_____** |

## Appendix C: Data Contract Template

```yaml
contract:
  name: user_events
  version: 1.2.0
  owner: analytics-team@company.com
  
  schema:
    - name: user_id
      type: string
      nullable: false
      description: Unique user identifier
    - name: event_type
      type: string
      nullable: false
      enum: [click, purchase, login, logout]
    - name: timestamp
      type: timestamp
      nullable: false
      description: Event occurrence time (UTC)
    - name: amount
      type: decimal(10,2)
      nullable: true
      description: Purchase amount (null for non-purchase events)
  
  quality:
    - freshness: < 5 minutes
    - completeness: > 99.9%
    - uniqueness: user_id + timestamp + event_type
  
  sla:
    - availability: 99.9%
    - latency_p99: < 100ms
  
  lifecycle:
    created: 2024-01-15
    deprecated: null
    retired: null
```

## Appendix D: Storage Cost Optimization Matrix

| Access Pattern | Storage Class | Compression | Lifecycle |
|----------------|---------------|-------------|-----------|
| Hot, frequent | Standard | Snappy | 30 days |
| Warm, occasional | Infrequent Access | Zstd | 90 days |
| Cold, rare | Glacier | Gzip | 1 year |
| Archive, compliance | Deep Archive | Gzip | 7 years |

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: data-engineering-syllabus.md