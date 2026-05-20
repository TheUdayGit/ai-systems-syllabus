## File: cloud-computing-devops-syllabus.md

# Cloud Computing and DevOps for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Distributed Systems Engineering (or equivalent), System Design Advanced (or equivalent), Database Design (or equivalent), strong Linux systems administration, networking fundamentals, and infrastructure-as-code experience  
**Estimated Duration:** 260–320 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: Cloud-Native Foundations — Economics, Physics, and Organizational Transformation](#module-0-cloud-native-foundations--economics-physics-and-organizational-transformation)
4. [Module 1: Compute Infrastructure — VMs, Containers, Serverless, and Beyond](#module-1-compute-infrastructure--vms-containers-serverless-and-beyond)
5. [Module 2: Kubernetes — The Control Plane of Modern Infrastructure](#module-2-kubernetes--the-control-plane-of-modern-infrastructure)
6. [Module 3: Networking in the Cloud — VPCs, Service Mesh, and Zero-Trust](#module-3-networking-in-the-cloud--vpcs-service-mesh-and-zero-trust)
7. [Module 4: Storage and Data Services in the Cloud](#module-4-storage-and-data-services-in-the-cloud)
8. [Module 5: Infrastructure as Code, GitOps, and Configuration Management](#module-5-infrastructure-as-code-gitops-and-configuration-management)
9. [Module 6: CI/CD, Deployment Strategies, and Release Engineering](#module-6-cicd-deployment-strategies-and-release-engineering)
10. [Module 7: Observability, SRE, and Incident Management](#module-7-observability-sre-and-incident-management)
11. [Module 8: Security, Compliance, and Governance in the Cloud](#module-8-security-compliance-and-governance-in-the-cloud)
12. [Module 9: Cost Optimization, FinOps, and Capacity Management](#module-9-cost-optimization-finops-and-capacity-management)
13. [Module 10: AI/ML Infrastructure on Cloud — MLOps, LLMOps, and GenAI Platforms](#module-10-aiml-infrastructure-on-cloud--mlops-llmops-and-genai-platforms)
14. [Module 11: Multi-Cloud, Hybrid Cloud, and Edge Infrastructure](#module-11-multi-cloud-hybrid-cloud-and-edge-infrastructure)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
17. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
18. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Cloud Computing and DevOps** not as a certification track, but as a **systems engineering discipline for operating reliable, cost-effective, and secure infrastructure at planetary scale**. The pedagogical approach follows a **Economics → Abstraction → Automation → Observability → Optimization** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Economics** | TCO, unit economics, cloud financial management, CapEx vs. OpEx | Financially rational infrastructure |
| **Abstraction** | VMs, containers, serverless, managed services, control planes | Appropriate abstraction selection |
| **Automation** | IaC, CI/CD, GitOps, self-healing, auto-scaling | Zero-touch operations |
| **Observability** | Metrics, logs, traces, SLOs, error budgets, incident response | Data-driven reliability |
| **Optimization** | Right-sizing, spot instances, reserved capacity, FinOps | Cost-efficient performance |

**Core Principles:**
- **The cloud is not a data center you rent — it is a programmable utility.** We teach API-driven infrastructure, not console-clicking. Every resource is provisioned, configured, and destroyed through code.
- **DevOps is not a team — it is a set of practices and a culture of shared ownership.** We study platform engineering, SRE, and developer experience as organizational capabilities, not job titles.
- **Cost is a first-class engineering constraint.** We teach FinOps, unit economics, and TCO analysis as core skills. A system that performs beautifully but bankrupts the company is not a success.
- **Security is not a gate — it is a continuous property of the system.** We integrate security into every phase: shift-left, zero-trust, policy-as-code, and automated compliance.
- **AI infrastructure is cloud infrastructure with GPU-shaped workloads.** We apply the same rigor to ML training clusters, model serving endpoints, and vector databases as we do to web services and databases.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Cloud Infrastructure Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | Provision and manage cloud resources via IaC, basic networking, cost monitoring | Single-cloud operations |
| **Advanced** | Design multi-region architectures, custom Kubernetes operators, service meshes | Production platforms |
| **Expert** | Design cloud-native platforms, FinOps programs, multi-cloud strategies | Hyperscale infrastructure |
| **Distinguished** | Define cloud strategy, negotiate enterprise agreements, shape vendor roadmaps | Technical leadership |

### DevOps/SRE Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | CI/CD pipelines, basic monitoring, incident response, configuration management | Team-level DevOps |
| **Advanced** | GitOps, SLO-based operations, chaos engineering, platform engineering | Organization-wide SRE |
| **Expert** | Custom platform tooling, automated remediation, reliability frameworks | Platform engineering |
| **Distinguished** | Define SRE culture, shape incident management practices, drive operational excellence | Technical leadership |

### AI/ML Cloud Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Intermediate** | GPU instance provisioning, basic ML pipeline orchestration, model serving | Production ML |
| **Advanced** | Distributed training on cloud, custom AMIs for ML, vector database deployment | ML platforms |
| **Expert** | Multi-region AI inference, LLM serving infrastructure, cost-optimized training | AI supercomputing |
| **Distinguished** | Design AI-native cloud platforms, negotiate GPU allocations, shape ML infrastructure strategy | AI infrastructure leadership |

### Cross-Cutting Competencies
- **Economic reasoning:** TCO analysis, unit cost modeling, cloud financial management
- **Security reasoning:** Zero-trust architecture, policy-as-code, automated compliance
- **Operational reasoning:** SLO design, error budgets, incident command, post-mortem culture
- **Organizational reasoning:** Platform team design, developer experience, RFC culture

---

## Module 0: Cloud-Native Foundations — Economics, Physics, and Organizational Transformation

**Duration:** 20 hours  
**Purpose:** Establish the strategic, economic, and organizational foundations of cloud-native engineering

### 0.1 The Economics of Cloud Computing
- **CapEx vs. OpEx:** Capital expenditure, operational expenditure, cash flow implications, accounting treatment
- **Unit economics:** Cost per request, cost per user, cost per transaction, marginal cost analysis
- **Cloud pricing models:** On-demand, reserved instances, spot/preemptible, savings plans, committed use discounts
- **TCO analysis:** Cloud vs. on-premise, hidden costs (data transfer, egress, API calls), break-even analysis
- **Production connection:** Why Dropbox moved off AWS; why Netflix stayed; when cloud is more expensive than on-premise; FinOps as a discipline

### 0.2 The Physics of Cloud Infrastructure
- **Global infrastructure:** Regions, availability zones, edge locations, points of presence, submarine cables
- **Latency and bandwidth:** Speed of light constraints, cross-region latency, data transfer costs
- **Power and sustainability:** PUE (Power Usage Effectiveness), carbon footprint, renewable energy, water usage
- **Production connection:** Why region selection matters for latency; why data transfer is the hidden cloud cost; sustainability as a design constraint

### 0.3 Cloud Service Models and Abstractions
- **IaaS:** Compute, storage, networking — maximum control, maximum responsibility
- **PaaS:** Managed platforms, databases, message queues — balanced control and convenience
- **SaaS:** Fully managed applications — minimum control, maximum convenience
- **FaaS (Serverless):** Functions, event-driven, pay-per-invocation — extreme abstraction
- **CaaS (Containers as a Service):** Kubernetes, managed container orchestration
- **Production connection:** Choosing between EC2 and Lambda; when managed databases beat self-hosted; why Kubernetes is the dominant abstraction

### 0.4 Organizational Transformation and DevOps Culture
- **DevOps principles:** Flow, feedback, continual learning — CAMS (Culture, Automation, Measurement, Sharing)
- **Team topologies:** Stream-aligned, platform, enabling, complicated subsystem teams
- **Platform engineering:** Internal developer platforms, golden paths, self-service, developer experience
- **SRE culture:** Error budgets, blameless post-mortems, toil reduction, service level objectives
- **Production connection:** Why DevOps transformations fail (culture, not tools); why platform engineering is the evolution of DevOps; SRE at Google and beyond

### 0.5 Lab: Cloud Economics Analysis
- **Task:** Perform TCO analysis for a hypothetical workload on AWS, GCP, and Azure
- **Requirements:**
  - Define workload: compute, storage, networking, data transfer
  - Calculate costs for 3 pricing models: on-demand, reserved, spot
  - Include hidden costs: data egress, API calls, support, training
  - Compare with equivalent on-premise deployment
  - Model 3-year TCO with growth projections
  - Document assumptions and sensitivity analysis
- **Deliverable:** TCO comparison report, pricing model recommendation, risk analysis

---

## Module 1: Compute Infrastructure — VMs, Containers, Serverless, and Beyond

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 1.1 Virtual Machines and Instance Types
- **Hypervisor types:** Type 1 (bare metal), Type 2 (hosted), paravirtualization, hardware-assisted virtualization
- **Instance families:** General purpose, compute optimized, memory optimized, GPU, FPGA, burstable
- **Bare metal:** No hypervisor overhead, direct hardware access, licensing benefits
- **Production connection:** Choosing instance types for ML training (GPU instances); burstable for dev/test; bare metal for high-performance databases

### 1.2 Container Technology Deeply
- **Container internals:** Namespaces (PID, net, mount, user, IPC, UTS, cgroup), cgroups v1/v2, union filesystems (overlayfs, aufs)
- **Container runtime:** runc, crun, containerd, CRI-O, OCI specs
- **Container security:** Seccomp, AppArmor/SELinux, capabilities, rootless containers, gVisor, Kata Containers
- **Image optimization:** Multi-stage builds, distroless images, image scanning, SBOMs
- **Production connection:** Why container startup time matters for serverless; rootless containers for security; distroless for minimal attack surface

### 1.3 Serverless and Function-as-a-Service
- **Function lifecycle:** Cold start, warm start, provisioned concurrency, snapstart
- **Event sources:** API Gateway, S3, DynamoDB, Kafka, schedule, custom events
- **Limitations:** Timeout, memory, package size, statelessness, execution time
- **Serverless containers:** AWS Fargate, Google Cloud Run, Knative — bridge between containers and serverless
- **Production connection:** Lambda for lightweight ML inference; Cloud Run for containerized serving; cold start optimization strategies

### 1.4 GPU and Accelerated Computing
- **GPU instances:** NVIDIA A100, H100, V100, T4, L4 — use cases and pricing
- **GPU scheduling:** Kubernetes device plugins, NVIDIA GPU Operator, time-slicing, MIG (Multi-Instance GPU)
- **Custom accelerators:** AWS Inferentia, Trainium, Google TPU, Azure Maia — custom silicon economics
- **Production connection:** GPU scheduling for multi-tenant ML platforms; MIG for cost sharing; custom accelerators for cost-performance optimization

### 1.5 Lab: Building a Multi-Tenant Compute Platform
- **Task:** Build a platform supporting VMs, containers, and serverless workloads
- **Requirements:**
  - Terraform/Pulumi for infrastructure provisioning
  - Kubernetes cluster with GPU support
  - Serverless functions for event processing
  - Auto-scaling based on CPU, memory, and custom metrics
  - Cost allocation per tenant
  - Security: network isolation, IAM, secrets management
  - Benchmark: startup time, scaling latency, cost per workload type
- **Deliverable:** Working platform, architecture document, cost analysis, security audit

---

## Module 2: Kubernetes — The Control Plane of Modern Infrastructure

**Duration:** 35 hours  
**Level:** Advanced → Expert

### 2.1 Kubernetes Architecture Deeply
- **Control plane:** API server, etcd, scheduler, controller manager, cloud controller manager
- **Node components:** Kubelet, kube-proxy, container runtime, CNI plugin, CSI driver
- **API server internals:** REST API, admission controllers, webhooks, aggregation layer, API priority and fairness
- **etcd:** Raft consensus, watch mechanism, compaction, defragmentation, backup strategies
- **Production connection:** Why etcd is the brain of Kubernetes; API server performance tuning; admission controller latency impact

### 2.2 Scheduling and Resource Management
- **Scheduler algorithm:** Predicates and priorities, scheduling framework, custom schedulers
- **Resource requests and limits:** CPU (compressible), memory (incompressible), QoS classes (Guaranteed, Burstable, BestEffort)
- **Advanced scheduling:** Affinity/anti-affinity, taints/tolerations, node selectors, topology spread constraints, pod topology spread
- **GPU scheduling:** Device plugins, extended resources, GPU sharing (time-slicing, MIG)
- **Production connection:** Scheduling for high availability (topology spread); GPU sharing for cost efficiency; why resource limits prevent OOM kills

### 2.3 Networking and Service Discovery
- **CNI plugins:** Calico, Cilium, Flannel, Weave, AWS VPC CNI — comparison and selection
- **Service types:** ClusterIP, NodePort, LoadBalancer, ExternalName, Headless
- **Ingress and Gateway API:** NGINX, Traefik, Istio Gateway, AWS ALB Ingress Controller
- **DNS:** CoreDNS, cluster DNS, external DNS, service discovery patterns
- **Network policies:** L3/L4 policies, Cilium L7 policies, zero-trust networking
- **Production connection:** Cilium for eBPF-based networking; Gateway API for advanced traffic management; network policies for microsegmentation

### 2.4 Storage and Stateful Workloads
- **Storage classes:** Provisioner, parameters, reclaim policy, volume binding mode
- **PV/PVC lifecycle:** Provisioning, binding, mounting, resizing, snapshotting
- **StatefulSets:** Ordered deployment, stable network identity, persistent storage per pod
- **Operators:** CRDs, controllers, Helm vs. Operators, Operator SDK, lifecycle management
- **Production connection:** StatefulSets for databases; Operators for complex stateful applications (Kafka, PostgreSQL); storage class selection for performance

### 2.5 Custom Resource Definitions and Operators
- **CRD design:** Schema, validation, versioning, conversion webhooks
- **Controller pattern:** Reconcile loop, work queues, informers, rate limiting
- **Operator patterns:** Level-based vs. edge-based triggering, idempotency, finalizers
- **Production connection:** Writing custom operators for ML platforms; CRDs for feature store resources; operator patterns for GitOps

### 2.6 Lab: Building a Kubernetes-Based ML Platform
- **Task:** Build a complete ML platform on Kubernetes
- **Requirements:**
  - Custom operator for training job lifecycle
  - CRDs for models, experiments, datasets
  - GPU scheduling with device plugin
  - Distributed training with MPI Operator or Kubeflow
  - Model serving with KServe or Seldon Core
  - Auto-scaling with KEDA
  - Multi-tenancy with namespaces and RBAC
  - Observability: metrics, logs, traces
  - GitOps deployment with ArgoCD
- **Deliverable:** Working platform, operator code, architecture document, scaling tests

---

## Module 3: Networking in the Cloud — VPCs, Service Mesh, and Zero-Trust

**Duration:** 25 hours  
**Level:** Advanced

### 3.1 Virtual Private Cloud (VPC) Architecture
- **VPC fundamentals:** Subnets, route tables, internet gateways, NAT gateways, VPC peering
- **Network segmentation:** Public subnets, private subnets, database subnets, DMZ
- **Hybrid connectivity:** VPN, Direct Connect, ExpressRoute, Transit Gateway, Cloud Interconnect
- **Multi-region networking:** Global VPC, inter-region peering, traffic routing, data residency
- **Production connection:** VPC design for multi-tier applications; Transit Gateway for hub-and-spoke; hybrid cloud connectivity

### 3.2 Load Balancing and Traffic Management
- **Layer 4 load balancers:** NLB, pass-through, TCP/UDP, connection tracking, health checks
- **Layer 7 load balancers:** ALB, path-based routing, host-based routing, SSL termination, WAF integration
- **Global load balancing:** GeoDNS, latency-based routing, health-aware failover
- **Production connection:** NLB for database connections; ALB for web applications; global load balancing for multi-region failover

### 3.3 Service Mesh
- **Istio architecture:** Control plane (istiod), data plane (Envoy), xDS APIs, sidecar injection
- **Traffic management:** Virtual services, destination rules, traffic splitting, canary, mirroring
- **Security:** mTLS automatic, certificate rotation, authorization policies, peer authentication
- **Observability:** Automatic metrics, distributed tracing, access logs
- **Sidecar-less service mesh:** Cilium Service Mesh, Istio ambient mesh, eBPF-based
- **Production connection:** Istio for microservices security; ambient mesh for reduced overhead; eBPF for performance

### 3.4 Zero-Trust Networking
- **BeyondCorp model:** Identity-aware proxy, context-aware access, device trust
- **Micro-segmentation:** Network policies, service mesh policies, identity-based segmentation
- **mTLS everywhere:** Service-to-service authentication, certificate management, SPIFFE/SPIRE
- **Production connection:** Google's BeyondCorp; zero-trust for Kubernetes; SPIFFE for workload identity

### 3.5 Lab: Designing a Zero-Trust Multi-Region Network
- **Task:** Design network architecture for a global SaaS platform
- **Requirements:**
  - VPCs in 3+ regions with peering/transit gateway
  - Private subnets for databases and internal services
  - Public subnets for load balancers and bastion hosts
  - Service mesh with mTLS (Istio or Cilium)
  - Zero-trust policies: identity-based access, micro-segmentation
  - Global load balancing with health-aware failover
  - Hybrid connectivity for on-premise integration
  - Network monitoring and flow logging
- **Deliverable:** Network architecture document, Terraform code, security policies, failover test results

---

## Module 4: Storage and Data Services in the Cloud

**Duration:** 20 hours  
**Level:** Advanced

### 4.1 Object Storage
- **S3 architecture:** Buckets, objects, keys, consistency model, multipart upload, versioning, lifecycle
- **S3 features:** Glacier, Intelligent-Tiering, Object Lock, replication, event notifications
- **S3 performance:** Request rate limits, prefix parallelism, transfer acceleration, batch operations
- **Production connection:** S3 as data lake foundation; Intelligent-Tiering for cost optimization; S3 event notifications for pipeline triggers

### 4.2 Block Storage
- **EBS volumes:** gp3, io2, st1, sc1 — performance characteristics, IOPS, throughput, latency
- **Volume types:** SSD-backed, HDD-backed, provisioned IOPS, throughput optimized
- **Multi-attach:** Read-write on multiple instances, cluster filesystems, limitations
- **Snapshots:** Incremental, cross-region copy, fast snapshot restore, lifecycle
- **Production connection:** gp3 for general workloads; io2 for databases; snapshot strategies for backup

### 4.3 File Storage
- **EFS:** NFS-based, elastic, multi-AZ, performance modes, throughput modes
- **FSx:** Lustre, Windows File Server, ONTAP, OpenZFS — specialized file systems
- **Cloud Filestore / Azure Files:** Managed NFS/SMB, integration with Kubernetes
- **Production connection:** EFS for shared storage; FSx Lustre for HPC; file storage for legacy applications

### 4.4 Managed Database Services
- **RDS / Cloud SQL / Azure Database:** PostgreSQL, MySQL, SQL Server — managed backups, patching, scaling
- **Aurora:** Storage architecture, read replicas, serverless, global databases
- **DynamoDB / Bigtable / Cosmos DB:** NoSQL managed services, consistency models, capacity modes
- **ElastiCache / Memorystore:** Managed Redis/Memcached, cluster mode, replication
- **Production connection:** Aurora for PostgreSQL-compatible high performance; DynamoDB for key-value at scale; choosing managed vs. self-hosted

### 4.5 Lab: Designing a Multi-Tier Storage Architecture
- **Task:** Design storage for a data-intensive application
- **Requirements:**
  - Hot storage: EBS/io2 for transactional database
  - Warm storage: S3 Standard for analytics data
  - Cold storage: S3 Glacier for archival
  - Cache layer: ElastiCache Redis for session and query cache
  - Data lifecycle policies: automated tiering, retention, compliance
  - Backup strategy: cross-region replication, point-in-time recovery
  - Performance: <10ms for hot, <100ms for warm, hours acceptable for cold
  - Cost optimization: storage class analysis, retrieval cost modeling
- **Deliverable:** Storage architecture document, lifecycle policies, cost model, performance validation

---

## Module 5: Infrastructure as Code, GitOps, and Configuration Management

**Duration:** 25 hours  
**Level:** Advanced

### 5.1 Infrastructure as Code (IaC)
- **Declarative vs. imperative:** Desired state vs. procedural execution, idempotency, convergence
- **Terraform:** HCL, state management, modules, workspaces, remote backends, provider ecosystem
- **Pulumi:** General-purpose languages (TypeScript, Python, Go), strong typing, policy as code
- **CloudFormation / ARM / Deployment Manager:** Native IaC, drift detection, stack sets
- **Production connection:** Terraform for multi-cloud; Pulumi for type-safe infrastructure; CloudFormation for AWS-native integration

### 5.2 GitOps
- **GitOps principles:** Git as single source of truth, declarative configuration, automated convergence, closed loop
- **ArgoCD:** Application definitions, sync policies, hooks, resource health, multi-source
- **Flux:** GitOps toolkit, sources, kustomize, helm, image automation, notification
- **Rancher Fleet:** Cluster management, GitOps at scale, bundle deployment
- **Production connection:** ArgoCD for Kubernetes GitOps; Flux for progressive delivery; GitOps for disaster recovery

### 5.3 Configuration Management
- **Ansible:** Agentless, YAML playbooks, idempotency, roles, collections, vault
- **Chef / Puppet:** Agent-based, resource abstraction, cookbook/module ecosystem
- **Cloud-init:** VM initialization, user data, first-boot configuration
- **Production connection:** Ansible for VM configuration; cloud-init for auto-scaling groups; choosing based on fleet size and dynamism

### 5.4 Secret Management
- **HashiCorp Vault:** Dynamic secrets, PKI, encryption as a service, identity integration
- **AWS Secrets Manager / Azure Key Vault / GCP Secret Manager:** Native secret management, rotation, replication
- **External Secrets Operator:** Kubernetes integration, multi-backend, automatic synchronization
- **SOPS / Sealed Secrets:** Git-encrypted secrets, age/GPG, transparent decryption
- **Production connection:** Vault for multi-cloud; native secret managers for simplicity; SOPS for GitOps secrets

### 5.5 Policy as Code and Compliance
- **Open Policy Agent (OPA):** Rego language, policy decisions, admission control, authorization
- **Terraform Sentinel / AWS Config / Azure Policy:** Cloud-native policy enforcement
- **Compliance frameworks:** CIS benchmarks, SOC2, PCI-DSS, HIPAA, GDPR — automated validation
- **Production connection:** OPA for Kubernetes admission control; Sentinel for Terraform governance; automated compliance scanning

### 5.6 Lab: Building a GitOps Platform
- **Task:** Build a complete GitOps-based deployment platform
- **Requirements:**
  - Terraform/Pulumi for infrastructure provisioning
  - ArgoCD or Flux for application deployment
  - Vault or native secret manager for secrets
  - OPA for policy enforcement
  - Multi-environment promotion (dev → staging → prod)
  - Drift detection and automated remediation
  - Rollback capability
  - Audit trail for all changes
  - Developer self-service via pull requests
- **Deliverable:** Working GitOps platform, architecture document, policy definitions, demo workflow

---

## Module 6: CI/CD, Deployment Strategies, and Release Engineering

**Duration:** 25 hours  
**Level:** Advanced

### 6.1 CI/CD Pipeline Design
- **Continuous Integration:** Build, test, lint, security scan, artifact creation
- **Continuous Delivery:** Automated deployment to staging, manual promotion to production
- **Continuous Deployment:** Fully automated to production, feature flags, progressive delivery
- **Pipeline patterns:** Fan-out/fan-in, matrix builds, parameterized pipelines, artifact promotion
- **Tools:** GitHub Actions, GitLab CI, Jenkins, CircleCI, Azure DevOps, Buildkite, Tekton
- **Production connection:** GitHub Actions for GitHub-native; GitLab CI for integrated DevOps; Tekton for Kubernetes-native; Buildkite for agent-based scaling

### 6.2 Deployment Strategies
- **Rolling deployment:** Gradual replacement, health checks, automatic rollback
- **Blue-green deployment:** Parallel environments, instant switch, easy rollback, double capacity
- **Canary deployment:** Percentage-based traffic shift, metric-based promotion, automated rollback
- **A/B testing:** Feature comparison, statistical significance, user segmentation
- **Feature flags:** LaunchDarkly, Unleash, custom — gradual rollout, kill switches, targeting
- **Production connection:** Canary for low-risk deployment; blue-green for database migrations; feature flags for decoupling deployment from release

### 6.3 Artifact Management and Supply Chain Security
- **Container registries:** Docker Hub, ECR, GCR, ACR, Harbor — scanning, signing, replication
- **Artifact repositories:** Nexus, Artifactory, GitHub Packages, PyPI, npm — caching, promotion
- **SBOM (Software Bill of Materials):** SPDX, CycloneDX, generation, validation, vulnerability tracking
- **Supply chain security:** SLSA framework, signed artifacts, reproducible builds, dependency verification
- **Production connection:** Harbor for self-hosted registry; SLSA for supply chain integrity; SBOM for vulnerability management

### 6.4 Release Engineering and Feature Management
- **Release trains:** Scheduled releases, batching, coordination, release notes
- **Feature gates:** Percentage rollout, user targeting, metric-gated promotion
- **Dark launches:** Production testing without user impact, shadow traffic, comparison
- **Rollback strategies:** Automatic rollback on error rate, manual rollback, database rollback complexity
- **Production connection:** Release trains for predictable cadence; feature gates for safe experimentation; dark launches for confidence building

### 6.5 Lab: Building a Production CI/CD Pipeline
- **Task:** Build a complete CI/CD pipeline for a microservices application
- **Requirements:**
  - Source control with branch protection and required checks
  - Build stage: compilation, unit tests, linting, security scan (SAST, DAST, dependency)
  - Artifact creation: container images with SBOM, signed with cosign
  - Deployment to staging: automated, integration tests, performance tests
  - Promotion to production: canary deployment with metric-based promotion
  - Feature flags for gradual rollout
  - Rollback on error rate threshold
  - Audit trail and compliance reporting
  - GitOps integration for Kubernetes manifests
- **Deliverable:** Working pipeline, deployment strategy document, rollback procedures, security scan results

---

## Module 7: Observability, SRE, and Incident Management

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 7.1 The Three Pillars of Observability
- **Metrics:** Counters, gauges, histograms, summaries, exemplars, cardinality management
- **Logs:** Structured logging, correlation IDs, log levels, aggregation, sampling
- **Traces:** Spans, traces, context propagation, sampling strategies, tail-based sampling
- **OpenTelemetry:** Standardization, instrumentation, collectors, exporters, semantic conventions
- **Production connection:** Metrics for alerting; logs for debugging; traces for latency analysis; OpenTelemetry for vendor neutrality

### 7.2 SLOs, SLIs, and Error Budgets
- **Service Level Indicators (SLIs):** Quantitative measure of service quality (availability, latency, throughput, error rate)
- **Service Level Objectives (SLOs):** Target values for SLIs, aspirational but achievable
- **Service Level Agreements (SLAs):** Contractual commitments, penalties, customer-facing
- **Error budgets:** SLO-based budget for unreliability, balancing velocity and stability
- **Error budget policies:** Burn rate alerts, freeze policies, escalation procedures
- **Production connection:** Defining SLOs for ML serving; error budgets for safe deployment velocity; burn rate alerts for fast detection

### 7.3 Incident Management
- **Incident lifecycle:** Detection, triage, mitigation, resolution, post-incident review
- **Incident command system:** Roles (IC, scribe, communications, operations), clear authority, structured process
- **On-call engineering:** Rotation design, alert quality, fatigue management, escalation policies
- **Post-mortems:** Blameless culture, five whys, action items, follow-up, published learning
- **Production connection:** PagerDuty/Opsgenie for incident management; structured post-mortems at Google; on-call health metrics

### 7.4 Chaos Engineering and Reliability Testing
- **Principles:** Hypothesis-driven, blast radius control, production experimentation, automated rollback
- **Failure injection:** Network latency, partition, CPU pressure, memory pressure, disk failure, zone failure, DNS failure
- **Game days:** Planned experiments, team response validation, scenario design
- **Tools:** Chaos Monkey, Gremlin, Litmus, AWS Fault Injection Simulator, ChaoSlingr, PowerfulSeal
- **Production connection:** Netflix's Simian Army; chaos engineering for ML serving resilience; automated chaos in CI/CD pipelines

### 7.5 Lab: Building an SRE Practice
- **Task:** Establish SLOs, error budgets, and incident management for a service
- **Requirements:**
  - Define 3-5 SLIs with measurement methodology
  - Set SLOs with stakeholder agreement
  - Implement error budget tracking and burn rate alerts
  - Design on-call rotation with escalation
  - Run chaos experiment with hypothesis and measurement
  - Conduct post-mortem for simulated incident
  - Document runbooks for common alerts
  - Create observability dashboard (RED/USE methods)
- **Deliverable:** SLO document, error budget policy, on-call rotation, chaos experiment report, post-mortem, runbook library, dashboard

---

## Module 8: Security, Compliance, and Governance in the Cloud

**Duration:** 25 hours  
**Level:** Advanced → Expert

### 8.1 Identity and Access Management (IAM)
- **IAM fundamentals:** Users, groups, roles, policies, permissions, resource hierarchy
- **Federated identity:** SAML, OIDC, SSO, identity providers (Okta, Azure AD, Google Workspace)
- **Service accounts and workload identity:** Managed identities, service account keys, workload identity federation, SPIFFE/SPIRE
- **Least privilege:** Policy design, permission boundaries, attribute-based access control (ABAC)
- **Production connection:** AWS IAM policies; workload identity for Kubernetes; least privilege for ML pipelines; SPIFFE for zero-trust

### 8.2 Network Security
- **VPC security:** Security groups, NACLs, flow logs, VPC endpoints, PrivateLink
- **WAF and DDoS protection:** AWS WAF, Cloudflare, AWS Shield, rate limiting, bot management
- **Encryption in transit:** TLS 1.3, certificate management, mutual TLS, perfect forward secrecy
- **Encryption at rest:** KMS, envelope encryption, HSM, customer-managed keys, automatic rotation
- **Production connection:** Security groups as stateful firewalls; WAF for OWASP protection; KMS for data encryption; mTLS for service mesh

### 8.3 Data Protection and Privacy
- **Data classification:** Public, internal, confidential, restricted — handling requirements
- **Data masking and tokenization:** Static masking, dynamic masking, format-preserving encryption, token vaults
- **Privacy regulations:** GDPR (right to erasure, data portability, consent), CCPA, HIPAA, PCI-DSS
- **Production connection:** Data classification for access control; tokenization for PCI compliance; GDPR right to erasure implementation

### 8.4 Compliance and Audit
- **Compliance frameworks:** SOC2, ISO 27001, PCI-DSS, HIPAA, FedRAMP, NIST
- **Continuous compliance:** AWS Config, Azure Policy, GCP Security Command Center, automated remediation
- **Audit logging:** CloudTrail, Azure Activity Log, GCP Audit Logs, immutable storage, analysis
- **Production connection:** SOC2 for SaaS; PCI-DSS for payment processing; continuous compliance automation; audit log analysis for threat detection

### 8.5 Lab: Designing a Compliant Multi-Tenant Platform
- **Task:** Design security and compliance for a multi-tenant SaaS platform
- **Requirements:**
  - IAM design with role-based and attribute-based access control
  - Network segmentation with zero-trust policies
  - Data encryption at rest and in transit with customer-managed keys
  - WAF and DDoS protection
  - Compliance automation for SOC2 Type II
  - Audit logging with immutable storage
  - Privacy controls for GDPR (right to erasure, data portability)
  - Penetration testing plan
  - Security incident response plan
- **Deliverable:** Security architecture document, IAM policies, compliance roadmap, audit strategy, incident response plan

---

## Module 9: Cost Optimization, FinOps, and Capacity Management

**Duration:** 20 hours  
**Level:** Advanced → Expert

### 9.1 Cloud Financial Management (FinOps)
- **FinOps principles:** Inform, optimize, operate — team collaboration, shared accountability
- **Cost allocation:** Tagging strategies, cost centers, showback/chargeback, unit economics
- **Cost visibility:** Billing dashboards, anomaly detection, budget alerts, forecasting
- **Production connection:** FinOps Foundation framework; tagging as the foundation of cost visibility; unit economics for SaaS products

### 9.2 Compute Cost Optimization
- **Right-sizing:** Instance type selection, vertical scaling, horizontal scaling, auto-scaling
- **Reserved capacity:** Reserved instances, savings plans, committed use discounts, break-even analysis
- **Spot/preemptible instances:** Bidding strategies, interruption handling, spot fleets, checkpointing
- **Serverless economics:** Pay-per-invocation, cold start trade-offs, provisioned concurrency cost
- **Production connection:** Spot instances for batch ML training; savings plans for baseline compute; serverless for variable workloads

### 9.3 Storage and Data Transfer Optimization
- **Storage tiering:** Hot, warm, cold, archive — automated lifecycle policies
- **Data transfer:** Egress costs, CDN for edge caching, VPC endpoints, Direct Connect for bulk transfer
- **Deduplication and compression:** Data reduction, compression algorithms, delta encoding
- **Production connection:** S3 Intelligent-Tiering; CloudFront for egress reduction; compression for log storage

### 9.4 Capacity Planning and Auto-Scaling
- **Predictive scaling:** Machine learning-based forecasting, scheduled scaling, proactive capacity
- **Reactive scaling:** Target tracking, step scaling, simple scaling, cooldown periods
- **Custom metrics:** Application-specific metrics, queue depth, custom CloudWatch/Prometheus metrics
- **Production connection:** Predictive scaling for known events; custom metrics for ML serving; cooldown tuning for stability

### 9.5 Lab: FinOps Program Implementation
- **Task:** Implement a FinOps program for a cloud-native organization
- **Requirements:**
  - Tagging strategy and enforcement
  - Cost allocation model (showback/chargeback)
  - Right-sizing analysis and recommendations
  - Reserved capacity purchase recommendations
  - Spot instance strategy for appropriate workloads
  - Storage lifecycle optimization
  - Anomaly detection and alerting
  - Monthly cost review process
  - Target: 20% cost reduction without performance impact
- **Deliverable:** FinOps program document, cost analysis, optimization recommendations, implemented changes, savings report

---

## Module 10: AI/ML Infrastructure on Cloud — MLOps, LLMOps, and GenAI Platforms

**Duration:** 30 hours  
**Level:** Expert

### 10.1 ML Training Infrastructure on Cloud
- **Distributed training:** Multi-node, multi-GPU, all-reduce, parameter servers, ring-allreduce
- **Managed training services:** SageMaker Training, Vertex AI Training, Azure Machine Learning
- **Custom training clusters:** Kubernetes with GPU nodes, MPI operator, Kubeflow Training
- **Spot instance training:** Checkpointing, fault tolerance, elastic training, cost optimization
- **Production connection:** SageMaker for managed training; Kubernetes for custom workflows; spot instances for 70% cost reduction

### 10.2 Model Serving and Inference
- **Real-time serving:** SageMaker Endpoints, Vertex AI Prediction, KServe, Seldon Core
- **Batch inference:** SageMaker Batch Transform, Apache Spark, Ray, distributed batch processing
- **Edge inference:** AWS IoT Greengrass, Azure IoT Edge, custom edge deployment
- **Model optimization:** Quantization, pruning, compilation (ONNX, TensorRT), container optimization
- **Production connection:** KServe for Kubernetes-native serving; batch inference for large-scale predictions; edge inference for latency-sensitive applications

### 10.3 Feature Stores and Data Management
- **Feature store architecture:** Online store, offline store, feature registry, point-in-time correctness
- **Managed feature stores:** SageMaker Feature Store, Tecton, Feast on Kubernetes
- **Data versioning:** DVC, LakeFS, Delta Lake — reproducibility, lineage, rollback
- **Production connection:** Tecton for enterprise feature management; DVC for experiment reproducibility; Delta Lake for time travel

### 10.4 LLM and GenAI Infrastructure
- **LLM serving platforms:** vLLM on Kubernetes, SageMaker JumpStart, Vertex AI Model Garden
- **Vector databases on cloud:** Pinecone, Weaviate on EKS/GKE, pgvector on RDS
- **RAG pipelines:** Document ingestion, embedding generation, vector search, LLM integration
- **Agent frameworks:** LangChain on cloud, function calling, tool use, multi-agent orchestration
- **Production connection:** vLLM on EKS for custom LLM serving; managed vector databases for RAG; agent frameworks for autonomous workflows

### 10.5 Lab: Building a Cloud-Native GenAI Platform
- **Task:** Build a complete GenAI platform on Kubernetes
- **Requirements:**
  - LLM serving with vLLM or TensorRT-LLM on GPU nodes
  - Vector database (Weaviate or pgvector) for RAG
  - Document ingestion pipeline with embedding generation
  - API gateway with rate limiting and authentication
  - Auto-scaling based on request queue depth
  - Cost tracking per request and per user
  - Monitoring: latency, throughput, GPU utilization, token count
  - GitOps deployment with ArgoCD
  - Multi-tenancy with resource isolation
- **Deliverable:** Working platform, architecture document, cost analysis, performance benchmarks, scaling tests

---

## Module 11: Multi-Cloud, Hybrid Cloud, and Edge Infrastructure

**Duration:** 20 hours  
**Level:** Expert

### 11.1 Multi-Cloud Strategy and Architecture
- **Multi-cloud drivers:** Avoiding vendor lock-in, best-of-breed services, disaster recovery, compliance
- **Multi-cloud challenges:** Data gravity, egress costs, skill fragmentation, operational complexity
- **Abstraction layers:** Terraform for multi-cloud IaC, Kubernetes as the common runtime, Crossplane
- **Service portability:** Container images, Helm charts, OpenAPI specs, polyglot persistence
- **Production connection:** When multi-cloud is rational (regulatory, negotiation leverage); when it's irrational (complexity cost); Kubernetes as the abstraction layer

### 11.2 Hybrid Cloud and On-Premise Integration
- **Hybrid patterns:** Cloud bursting, backup and DR, dev/test in cloud, production on-premise
- **Connectivity:** VPN, Direct Connect, ExpressRoute, SD-WAN, Transit Gateway
- **Unified management:** Anthos, Azure Arc, AWS Outposts, Azure Stack, consistent tooling
- **Production connection:** Hybrid for regulated workloads; cloud bursting for peak loads; Outposts for low-latency edge

### 11.3 Edge Computing and IoT
- **Edge hierarchy:** Cloud → regional → metro → access → device
- **Edge platforms:** AWS Greengrass, Azure IoT Edge, Google Distributed Cloud Edge
- **Container orchestration at edge:** K3s, MicroK8s, lightweight Kubernetes
- **Data synchronization:** Edge-to-cloud sync, conflict resolution, offline operation
- **Production connection:** Edge inference for autonomous vehicles; K3s for factory automation; data synchronization for remote operations

### 11.4 Cloud-Native Networking Evolution
- **Cilium and eBPF:** Service mesh without sidecars, network policies, observability, load balancing
- **Service mesh convergence:** Istio ambient mesh, Cilium service mesh, sidecar-less future
- **API gateways:** Envoy Gateway, Kubernetes Gateway API, unified ingress and mesh
- **Production connection:** Cilium for eBPF-based networking; ambient mesh for reduced overhead; Gateway API for standardized ingress

### 11.5 Lab: Designing a Multi-Cloud AI Platform
- **Task:** Design an AI platform spanning AWS and GCP
- **Requirements:**
  - Training on AWS (SageMaker or custom EKS with GPU nodes)
  - Inference on GCP (Vertex AI or custom GKE)
  - Shared model registry (MLflow or custom)
  - Data synchronization between clouds
  - Unified monitoring and logging
  - Cost tracking per cloud and per workload
  - Failover strategy for cloud outage
  - Security: consistent IAM, encryption, network policies
  - Compliance: data residency, audit logging
- **Deliverable:** Architecture document, Terraform/Pulumi code, data flow diagrams, cost model, failover test plan

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Cloud-Native Platform Engineering Organization
- **Scope:** Build an internal developer platform for a 500+ engineer organization
- **Components:**
  - Self-service infrastructure provisioning (Terraform/Backstage)
  - Golden path templates for common services
  - CI/CD pipeline with security scanning and compliance gates
  - Kubernetes platform with multi-tenancy
  - Observability stack with SLOs and error budgets
  - FinOps integration with cost visibility
  - Security: zero-trust, policy-as-code, secret management
  - Documentation and developer experience
  - On-call rotation and incident management
- **Deliverables:** Working platform, developer satisfaction metrics, cost savings report, security audit, operational runbooks

### Capstone B: Production MLOps Platform
- **Scope:** Build a complete MLOps platform on cloud Kubernetes
- **Components:**
  - Data ingestion and validation pipelines
  - Feature store with online and offline stores
  - Distributed training with experiment tracking
  - Model registry with versioning and lineage
  - Real-time serving with A/B testing
  - Batch inference for large-scale processing
  - Model monitoring: drift, latency, throughput
  - Auto-scaling and cost optimization
  - GitOps deployment with ArgoCD
  - Security: model access control, data privacy
- **Deliverables:** Working platform, performance benchmarks, cost analysis, scaling tests, security assessment

### Capstone C: Multi-Cloud GenAI Infrastructure
- **Scope:** Design and implement GenAI infrastructure across AWS and Azure
- **Components:**
  - LLM serving with vLLM on GPU clusters in both clouds
  - Vector databases with hybrid search
  - RAG pipeline with document ingestion and embedding
  - Multi-cloud model registry and artifact storage
  - Unified API gateway with intelligent routing
  - Cost optimization: spot instances, reserved capacity, model distillation
  - Security: consistent IAM, encryption, network policies
  - Observability: unified metrics, logs, traces
  - Disaster recovery: cross-cloud failover
- **Deliverables:** Working infrastructure, architecture document, cost comparison, failover test results, performance benchmarks

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 15% | Working infrastructure code, pipelines, platforms |
| Architecture documents | 15% | Design docs, ADRs, RFCs, cost analyses |
| Peer review | 10% | Reviewing others' infrastructure designs |

### Examinations (30%)
- **Midterm (15%):** Kubernetes, networking, security, CI/CD
- **Final (15%):** AI/ML infrastructure, multi-cloud, FinOps, SRE

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 8% |
| Architecture and design | 8% |
| Cost optimization | 5% |
| Security and compliance | 4% |
| Documentation and presentation | 3% |
| Operational excellence | 2% |

### Grading Rubric
- **A (90-100):** Publication-quality work, production-ready platform, significant cost optimization, comprehensive security
- **B (80-89):** Excellent understanding, minor gaps, strong implementation
- **C (70-79):** Good understanding, significant gaps in advanced topics
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding for expert-level cloud engineering

---

## Recommended Tools, Libraries & Infrastructure

### Cloud Platforms
| Tool | Purpose |
|------|---------|
| **AWS** | Primary cloud platform |
| **GCP** | AI/ML services, Kubernetes |
| **Azure** | Enterprise, hybrid cloud |
| **Terraform** | Multi-cloud IaC |
| **Pulumi** | Type-safe IaC |
| **Crossplane** | Kubernetes-based IaC |

### Kubernetes
| Tool | Purpose |
|------|---------|
| **EKS / GKE / AKS** | Managed Kubernetes |
| **K3s / MicroK8s** | Lightweight Kubernetes |
| **Helm** | Package management |
| **ArgoCD / Flux** | GitOps |
| **Istio / Cilium** | Service mesh |
| **KEDA** | Event-driven auto-scaling |

### CI/CD
| Tool | Purpose |
|------|---------|
| **GitHub Actions** | CI/CD |
| **GitLab CI** | Integrated DevOps |
| **Tekton** | Kubernetes-native CI/CD |
| **Buildkite** | Scalable CI/CD |
| **Jenkins** | Self-hosted CI/CD |

### Observability
| Tool | Purpose |
|------|---------|
| **Prometheus** | Metrics |
| **Grafana** | Visualization |
| **Jaeger** | Tracing |
| **Loki** | Logs |
| **OpenTelemetry** | Instrumentation |
| **PagerDuty / Opsgenie** | Incident management |

### Security
| Tool | Purpose |
|------|---------|
| **Vault** | Secrets management |
| **OPA** | Policy as code |
| **Falco** | Runtime security |
| **Trivy** | Container scanning |
| **Cosign** | Artifact signing |

### AI/ML
| Tool | Purpose |
|------|---------|
| **Kubeflow** | ML pipelines |
| **KServe / Seldon** | Model serving |
| **MLflow** | Experiment tracking |
| **Feast** | Feature store |
| **vLLM** | LLM serving |
| **Ray** | Distributed computing |

---

## References & Further Reading

### Cloud Architecture
1. **Vogels,** "Eventually Consistent" — Amazon CTO on distributed systems
2. **Barr et al.,** *AWS Well-Architected Framework* — Official AWS guidance
3. **Beyer et al.,** *The Site Reliability Workbook* — Google SRE practices

### Kubernetes
1. **Hightower et al.,** *Kubernetes Up & Running* — Practical Kubernetes
2. **Burns et al.,** *Designing Distributed Systems* — Kubernetes patterns
3. **Kubernetes documentation** — The definitive reference

### DevOps and SRE
1. **Kim et al.,** *The DevOps Handbook* — DevOps principles
2. **Beyer et al.,** *Site Reliability Engineering* — Google SRE book
3. **Forsgren et al.,** *Accelerate* — DevOps metrics and performance

### FinOps
1. **FinOps Foundation,** *Cloud FinOps* — Official FinOps book
2. **AWS Cost Optimization** — Official AWS guidance

### AI/ML Infrastructure
1. **Huyen,** *Designing Machine Learning Systems* — MLOps from first principles
2. **Kubeflow documentation** — ML on Kubernetes
3. **SageMaker / Vertex AI documentation** — Managed ML services

### Security
1. **Stallings & Brown,** *Computer Security: Principles and Practice*
2. **NIST Cloud Security** — Official NIST guidance

---

## Appendix A: Cloud Service Comparison Matrix

| Service | AWS | GCP | Azure |
|---------|-----|-----|-------|
| Compute | EC2 | Compute Engine | VMs |
| Kubernetes | EKS | GKE | AKS |
| Object Storage | S3 | Cloud Storage | Blob Storage |
| Managed DB | RDS | Cloud SQL | Azure SQL |
| Serverless | Lambda | Cloud Functions | Functions |
| ML Training | SageMaker | Vertex AI | ML Studio |
| Vector DB | OpenSearch | Vertex AI Vector Search | Cognitive Search |

## Appendix B: Kubernetes Resource Model

```
Pod → smallest deployable unit
  ↓
ReplicaSet → ensures desired replica count
  ↓
Deployment → declarative updates, rollback
  ↓
StatefulSet → ordered deployment, stable identity
  ↓
DaemonSet → one per node
  ↓
Job / CronJob → batch / scheduled
  ↓
Service → network abstraction
  ↓
Ingress / Gateway → external access
  ↓
ConfigMap / Secret → configuration
  ↓
PersistentVolumeClaim → storage request
```

## Appendix C: SLO Template

| Service | SLI | SLO | Measurement |
|---------|-----|-----|-------------|
| API | Availability | 99.9% | Successful requests / total requests |
| API | Latency | P99 < 200ms | Request duration |
| Database | Availability | 99.99% | Connection success rate |
| Database | Replication lag | < 1 second | Seconds behind primary |
| Model serving | Latency | P99 < 100ms | Inference duration |
| Model serving | Error rate | < 0.1% | Failed inferences / total |

## Appendix D: Production Checklist

Before any cloud infrastructure is production-ready, verify:

- [ ] **IaC:** All resources provisioned via code, state managed, drift detected
- [ ] **Security:** IAM least privilege, encryption at rest and in transit, network policies
- [ ] **Compliance:** Required frameworks met, audit logging enabled, automated checks
- [ ] **Observability:** Metrics, logs, traces, SLOs defined, alerts configured
- [ ] **Reliability:** Auto-scaling, health checks, graceful shutdown, circuit breakers
- [ ] **Cost:** Tagged, budgeted, right-sized, reserved capacity where appropriate
- [ ] **Backup:** Automated backups, tested recovery, cross-region replication
- [ ] **Documentation:** Runbooks, architecture docs, ADRs, onboarding guide
- [ ] **On-call:** Rotation defined, escalation paths, incident response plan

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: cloud-computing-devops-syllabus.md