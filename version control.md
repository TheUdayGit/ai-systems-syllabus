  ## File: version-control-syllabus.md

# Version Control for AI/ML Infrastructure Systems

## A Comprehensive Syllabus for Staff+ Engineers Building Production AI Systems

---

## Table of Contents

1. [Course Overview](#1-course-overview)
2. [Learning Objectives](#2-learning-objectives)
3. [Prerequisites](#3-prerequisites)
4. [Curriculum Structure](#4-curriculum-structure)
5. [Module 0: Foundations & Philosophy](#module-0-foundations--philosophy)
6. [Module 1: Git Internals & Object Model](#module-1-git-internals--object-model)
7. [Module 2: Branching Strategies & Workflow Design](#module-2-branching-strategies--workflow-design)
8. [Module 3: Merge Strategies & Conflict Resolution](#module-3-merge-strategies--conflict-resolution)
9. [Module 4: History Manipulation & Rewriting](#module-4-history-manipulation--rewriting)
10. [Module 5: Collaboration at Scale](#module-5-collaboration-at-scale)
11. [Module 6: Monorepos & Large Repository Management](#module-6-monorepos--large-repository-management)
12. [Module 7: Hooks, Automation & CI/CD Integration](#module-7-hooks-automation--cicd-integration)
13. [Module 8: Security, Compliance & Audit](#module-8-security-compliance--audit)
14. [Module 9: Advanced Topics & Emerging Patterns](#module-9-advanced-topics--emerging-patterns)
15. [Capstone Projects](#capstone-projects)
16. [Assessment & Evaluation](#assessment--evaluation)
17. [Recommended Resources](#recommended-resources)
18. [Study Schedule](#study-schedule)

---

## 1. Course Overview

This syllabus provides a rigorous, production-oriented deep dive into Version Control as practiced at the intersection of AI/ML infrastructure, distributed systems, and large-scale backend engineering. It is designed for engineers who manage the source of truth for code, models, data, and infrastructure configurations that power modern AI systems.

Unlike generic Git tutorials, this curriculum explicitly connects every version control concept to AI/ML systems: from managing terabyte-scale datasets with Git LFS to versioning model artifacts in registries, from designing branching strategies for research-to-production pipelines to implementing cryptographic provenance for regulatory compliance. The focus is on systems that must be correct, auditable, scalable, and operable under extreme complexity.

**Target Audience:**
- ML Infrastructure Engineers managing multi-terabyte repositories
- MLOps Engineers designing experiment-to-production workflows
- Platform Engineers building internal developer platforms
- Distributed Systems Engineers implementing reproducible builds
- Staff+ candidates architecting version control strategy for AI organizations

**Duration:** 12-16 weeks (self-paced or intensive)
**Format:** Theory → Deep Implementation → Systems Architecture → Production Operations → Security & Compliance

---

## 2. Learning Objectives

By the end of this syllabus, you will be able to:

### Technical Mastery
- Understand Git at the object-model level and extend it for specialized workflows
- Design branching strategies that balance research velocity with production stability
- Manage repositories at scale: monorepos, large files, shallow clones, partial checkouts
- Implement hooks and automation that enforce quality without blocking innovation
- Secure version control systems against supply chain attacks and insider threats

### Architectural Reasoning
- Choose between monorepo and polyrepo architectures based on quantitative analysis
- Design version control workflows for heterogeneous teams (researchers, engineers, operators)
- Architect for reproducibility: code, data, model, and environment versioning
- Implement audit trails and provenance tracking for regulatory compliance

### Production Operations
- Operate version control infrastructure with SLOs and disaster recovery procedures
- Troubleshoot complex repository states and history corruption
- Optimize repository performance for CI/CD throughput
- Manage repository migrations and organizational restructuring

---

## 3. Prerequisites

### Required
- **Programming:** Fluent in Python and shell scripting; familiarity with C for Git internals
- **Git:** Daily use experience: clone, commit, branch, merge, rebase, push, pull
- **Systems:** Understanding of file systems, hashing, compression, networking basics
- **AI/ML:** Familiarity with model training workflows, experiment tracking, and deployment pipelines

### Recommended
- Experience with GitHub/GitLab/Bitbucket at organizational scale
- Exposure to CI/CD systems and their integration with version control
- Understanding of cryptography basics (hashing, signatures, certificates)
- Familiarity with distributed systems concepts (consistency, consensus, CAP)

---

## 4. Curriculum Structure

The syllabus follows a **deep-to-wide** progression—mastering fundamentals before scaling to organizational systems:

| Phase | Focus | Weeks | Key Outcome |
|-------|-------|-------|-------------|
| **Internals** | Object model, storage, plumbing | 1-3 | Git-level mastery |
| **Workflows** | Branching, merging, collaboration | 4-6 | Production workflow design |
| **Scale** | Monorepos, large files, performance | 7-9 | Repository architecture for AI/ML |
| **Automation** | Hooks, CI/CD, quality gates | 10-11 | Automated quality enforcement |
| **Security** | Cryptography, audit, compliance | 12-13 | Secure, compliant version control |
| **Advanced** | Emerging patterns, research frontiers | 14-16 | Staff-level system design |

---

## Module 0: Foundations & Philosophy

### 0.1 The Role of Version Control in AI Systems
- **Version control as the backbone of reproducible AI**
- The "it works on my machine" problem at scale
- Reproducibility crisis: code, data, model, environment, hardware
- **AI/ML context:** Why DALL-E 3 training requires versioning 100TB datasets, 10,000 commits, and exact dependency snapshots
- The cost of version control failures: lost experiments, irreproducible results, regulatory violations

### 0.2 Version Control Beyond Code
- Versioning data: datasets, feature stores, embeddings
- Versioning models: checkpoints, configurations, architectures
- Versioning environments: Docker images, conda environments, system packages
- Versioning infrastructure: Terraform, Kubernetes manifests, network configs
- **Pattern:** The "everything as versioned" philosophy

### 0.3 The History of Version Control
- Local VCS: RCS, SCCS
- Centralized VCS: CVS, Subversion
- Distributed VCS: BitKeeper, Git, Mercurial, Darcs, Pijul
- **Why Git won:** technical merits, network effects, GitHub ecosystem
- Emerging alternatives: Jujutsu (jj), Sapling (Meta), Gitless

### 0.4 Mental Models for Version Control
- DAG (Directed Acyclic Graph) of commits
- Content-addressable storage
- Distributed vs. centralized mental models
- **Exercise:** Draw the DAG for a complex merge scenario

### 0.5 Version Control as a System Component
- VCS in the system architecture: not just a tool, but infrastructure
- SLOs for version control: availability, latency, throughput
- Disaster recovery: repository corruption, accidental deletion, ransomware
- **AI/ML context:** Version control as part of the ML platform, not an afterthought

---

## Module 1: Git Internals & Object Model

### 1.1 The Git Object Model
- **The four object types:** blob, tree, commit, tag
- Content-addressable storage: SHA-1 (and transition to SHA-256)
- Object storage: loose objects vs. packfiles
- The object graph and reachability
- **Implementation:** Reading raw Git objects with `git cat-file`, building a simple object browser

### 1.2 The Git Directory Structure
- `.git/` anatomy: `objects/`, `refs/`, `HEAD`, `index`, `config`, `hooks/`
- Refs: branches, tags, remote tracking branches, symbolic refs
- The index (staging area): structure, conflict entries, sparse index
- **Implementation:** Parsing `.git/index` binary format in Python

### 1.3 Commit Graph & History Traversal
- Parent pointers and the commit DAG
- `git log` algorithms: commit graph v2, generation numbers, topological sort
- Reachability analysis: `git merge-base`, `git branch --contains`
- **Performance:** Commit graph file (`commit-graph`), bloom filters for changed paths
- **AI/ML context:** Tracing model lineage through commit history

### 1.4 Refs & Reflogs
- Refs as mutable pointers to commits
- Reflog: the safety net, expiration policies
- Detached HEAD state: what it means and how to recover
- Symbolic refs: `HEAD`, `ORIG_HEAD`, `FETCH_HEAD`
- **Recovery techniques:** Using reflog to recover from `git reset --hard`, filter-branch disasters

### 1.5 The Index & Staging Area Deep Dive
- Index format: mode, SHA, stage number, path
- Three-way merge index entries: stage 1 (base), 2 (ours), 3 (theirs)
- Sparse index and sparse checkout for monorepos
- **Implementation:** Building a minimal index parser and manipulation tool

### 1.6 Packfiles & Delta Compression
- Packfile format: header, objects, delta chains
- Delta compression: copy/insert instructions, sliding window
- Packfile indexing: `.idx` and `.pack` files
- Garbage collection: `git gc`, repack strategies
- **Performance:** Packfile optimization for large repositories
- **AI/ML context:** Efficient storage for model checkpoints and binary artifacts

### 1.7 Plumbing vs. Porcelain
- Git's layered architecture: plumbing commands vs. porcelain
- Building custom workflows with plumbing: `git hash-object`, `git mktree`, `git commit-tree`
- **Implementation:** Building a minimal Git client using only plumbing commands
- **Pattern:** Using plumbing for automation and custom tools

---

## Module 2: Branching Strategies & Workflow Design

### 2.1 Branch Semantics & Mechanics
- Branches as lightweight refs: implementation details
- Branch namespaces: local, remote, tracking
- Branch lifecycle: creation, evolution, merging, deletion
- **Best practice:** Semantic branch naming conventions

### 2.2 GitFlow & Its Discontents
- GitFlow: master, develop, feature, release, hotfix branches
- Critique: complexity, merge hell, release branch overhead
- When GitFlow still makes sense: scheduled releases, regulated industries
- **AI/ML context:** GitFlow adapted for model release cycles

### 2.3 GitHub Flow & Trunk-Based Development
- GitHub Flow: main branch, feature branches, pull requests
- Trunk-based development: short-lived branches, feature flags
- Comparison: velocity, risk, cognitive load, tooling requirements
- **Quantitative analysis:** Branch lifetime, merge frequency, conflict rates
- **AI/ML context:** Rapid experiment iteration vs. production stability

### 2.4 Feature Flags vs. Feature Branches
- Feature flag architecture: client-side, server-side, hybrid
- Flag lifecycle: creation, rollout, monitoring, cleanup
- Trade-offs: deployment complexity vs. branch management complexity
- **Implementation:** Feature flag system design for ML model variants
- **Pattern:** The "branch by abstraction" technique

### 2.5 Branch Protection & Quality Gates
- Required status checks, required reviews, required signatures
- Merge strategies: merge, squash, rebase, fast-forward
- Merge queues: GitHub Merge Queue, GitLab Merge Trains, Mergify
- **AI/ML context:** Protecting model configuration branches, experiment reproducibility gates

### 2.6 Release Branching & Versioning
- Semantic Versioning (SemVer): MAJOR.MINOR.PATCH
- Calendar Versioning (CalVer): YYYY.MM.MICRO
- Release branch management: creation, cherry-picks, EOL
- **AI/ML context:** Model versioning strategies aligned with code versioning
- **Pattern:** The "release train" for continuous model deployment

### 2.7 Long-Running Branches & Divergence Management
- The problem of long-lived feature branches
- Strategies for managing divergence: regular merges, rebasing, patch queues
- Subtree merges and submodule alternatives
- **AI/ML context:** Long-running research branches, model architecture experiments

---

## Module 3: Merge Strategies & Conflict Resolution

### 3.1 Three-Way Merge Algorithm
- Common ancestor, ours, theirs: the three snapshots
- Diff3 format and conflict markers
- Merge algorithm: recursive, resolve, octopus
- **Implementation:** Building a minimal three-way merge tool

### 3.2 Recursive Merge & Merge Bases
- Finding merge bases: recursive merge base calculation
- Criss-cross merges and the recursive strategy
- Virtual common ancestor construction
- **Edge cases:** Multiple merge bases, degenerate cases

### 3.3 Merge Conflict Resolution Strategies
- Manual resolution: understanding conflict markers
- Merge tools: vimdiff, meld, VS Code, IntelliJ
- Rerere (Reuse Recorded Resolution): automatic resolution learning
- **Best practice:** Resolution discipline and testing merged code

### 3.4 Structural Merge & Semantic Merge
- Limitations of line-based merging
- Semantic merge tools: IntelliJ, SemanticMerge, GitHub Copilot
- Language-aware merging: AST-based, graph-based
- **AI/ML context:** Merging Jupyter notebooks, model configuration files (YAML, JSON)
- **Tools:** `nbdime` for notebooks, custom merge drivers

### 3.5 Rebase vs. Merge: The Eternal Debate
- Rebase mechanics: replaying commits, rewriting history
- Golden rule of rebasing: never rebase public history
- Interactive rebase: editing, squashing, reordering, splitting commits
- **Trade-off analysis:** History linearity vs. historical accuracy
- **AI/ML context:** Clean history for experiment reproducibility vs. audit trail preservation

### 3.6 Cherry-Pick & Selective History
- Cherry-pick mechanics: applying commits to different branches
- Cherry-pick vs. rebase: when to use each
- Range cherry-picks and patch series management
- **AI/ML context:** Selectively applying model improvements across experiment branches

### 3.7 Merge Queues & Batch Merging
- The merge queue problem: conflicting parallel PRs
- GitHub Merge Queue: how it works, configuration, monitoring
- GitLab Merge Trains: pipeline-driven merging
- **Implementation:** Building a custom merge queue for specialized workflows
- **Performance:** Queue depth, batch size, timeout strategies

---

## Module 4: History Manipulation & Rewriting

### 4.1 Commit Rewriting Fundamentals
- Amending commits: `git commit --amend`
- Squashing commits: interactive rebase, fixup commits
- Splitting commits: `git reset`, selective staging, `git add -p`
- **Best practice:** When to rewrite history vs. preserve it

### 4.2 Filter-Branch & Filter-Repo
- `git filter-branch`: rewriting entire history
- `git filter-repo`: the modern, faster replacement
- Use cases: removing secrets, splitting repositories, rewriting paths
- **Caution:** Filter-branch is destructive and slow; always backup
- **AI/ML context:** Removing large model files accidentally committed, cleaning dataset history

### 4.3 BFG Repo-Cleaner
- BFG vs. filter-repo: performance and usability comparison
- Removing large files, replacing text, removing sensitive data
- **Performance:** BFG's speed advantage for massive repositories
- **Security:** Ensuring secrets are fully purged from history

### 4.4 Git Submodules & Subtree
- Submodules: separate repositories within repositories
- Submodule mechanics: `.gitmodules`, `git submodule update`, `--recursive`
- Subtree merge strategy: alternative to submodules
- **Trade-offs:** Submodule complexity vs. monorepo simplicity
- **AI/ML context:** Managing shared model architectures, common datasets

### 4.5 Git Worktree
- Multiple working trees from a single repository
- Worktree mechanics: `.git/worktrees`, `git worktree add`
- Use cases: simultaneous branch work, CI/CD isolation
- **Performance:** Avoiding clone overhead for parallel operations

### 4.6 Partial Clone & Sparse Checkout
- Partial clone: `--filter=blob:none`, `--filter=tree:0`
- Sparse checkout: cone mode, sparse index
- **Performance:** Dramatic reduction in clone time and disk usage
- **AI/ML context:** Working with repositories containing terabytes of model artifacts
- **Implementation:** Configuring sparse checkout for ML monorepos

### 4.7 Shallow Clone & Unshallowing
- Shallow clones: `--depth`, `--shallow-since`, `--shallow-exclude`
- Unshallowing: fetching missing history
- **Trade-offs:** Speed vs. completeness, merge limitations
- **AI/ML context:** CI/CD optimization with shallow clones for large repos

---

## Module 5: Collaboration at Scale

### 5.1 Fork-Based Collaboration
- Forks: server-side clones with independent history
- Fork workflows: personal fork, shared fork, fork-and-branch
- **Comparison:** Fork-based vs. shared repository workflows
- **AI/ML context:** Open source ML project collaboration (Hugging Face, PyTorch)

### 5.2 Code Review as a Collaborative Process
- Pull request mechanics: creation, review, approval, merge
- Review types: code review, design review, security review
- Review tools: GitHub, GitLab, Gerrit, Phabricator
- **Best practice:** Constructive review culture, review checklists
- **AI/ML context:** Reviewing model configuration changes, data pipeline modifications

### 5.3 Signed Commits & Verified History
- GPG signing: `git commit -S`, `git verify-commit`
- SSH signing: modern alternative to GPG
- Verified commits in GitHub/GitLab UI
- **Security:** Ensuring commit authenticity, preventing impersonation
- **Compliance:** Regulatory requirements for signed code

### 5.4 Attribution & Authorship
- Git author vs. committer: the distinction
- `Co-authored-by` trailers for pair programming
- Mailmap for canonicalizing identities
- **AI/ML context:** Attribution in collaborative research, DCO (Developer Certificate of Origin)

### 5.5 Communication in Commits
- Commit message anatomy: subject, body, trailers
- Conventional Commits: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- Commit message driven development: writing messages first
- **Automation:** Changelog generation, semantic versioning from commits
- **AI/ML context:** Tracking experiment changes through commit messages

### 5.6 Handling Large Teams & Merge Conflicts
- Conflict prediction and prevention
- Communication protocols for touching shared code
- Locking strategies for binary files (Git LFS locking)
- **AI/ML context:** Coordinating model file changes, dataset updates

### 5.7 Cross-Repository Dependencies
- Git submodules for cross-repo dependencies
- Package managers: npm, pip, cargo, poetry
- Monorepo tools: Bazel, Nx, Rush, Pants
- **Trade-off analysis:** Submodule vs. package vs. monorepo for ML dependencies

---

## Module 6: Monorepos & Large Repository Management

### 6.1 Monorepo Philosophy & Architecture
- **Why monorepos:** atomic changes, shared dependencies, unified versioning
- **Why not monorepos:** scale, build times, access control, cognitive load
- **Quantitative analysis:** Google's monorepo (2 billion lines, 95,000 commits/day)
- **AI/ML context:** Monorepo for ML platform: models, training code, serving infrastructure

### 6.2 Scaling Git for Monorepos
- Virtual file system: VFS for Git (Microsoft), GitFS
- Sparse checkout and sparse index optimization
- Partial clone strategies: treeless, blobless, shallow
- **Performance:** Clone time, checkout time, status time, log time

### 6.3 Large File Management
- Git LFS (Large File Storage): architecture, pointer files, smudge/clean filters
- LFS server implementations: GitHub, GitLab, custom
- LFS locking for binary file collaboration
- **Alternatives:** git-annex, DVC (Data Version Control), custom artifact stores
- **AI/ML context:** Versioning model checkpoints (GB-TB), datasets, embeddings

### 6.4 DVC: Data Version Control for AI/ML
- DVC architecture: `.dvc` files, remote storage, pipelines
- DVC vs. Git LFS: when to use each
- DVC pipelines: reproducible ML experiments
- **Implementation:** Setting up DVC for a complete ML project
- **Integration:** DVC with CI/CD, experiment tracking (MLflow, W&B)

### 6.5 Repository Splitting & Federation
- When to split a monorepo: quantitative criteria
- Repository federation: Git submodules, repo tool, custom solutions
- Codebase analysis tools: dependency graphs, change frequency
- **AI/ML context:** Splitting model repos from infrastructure repos

### 6.6 Performance Optimization
- Repository maintenance: `git gc`, `git repack`, `git prune`
- Packfile optimization: window size, depth, delta cache
- Index optimization: sparse index, split index
- **Monitoring:** Repository size metrics, clone time metrics, operation latency
- **AI/ML context:** Optimizing repos with large binary histories

### 6.7 Alternative VCS for Scale
- Sapling (Meta): virtualized working copy, transparent scaling
- Jujutsu (jj): conflict-free merges, operation log, working copy as commit
- Mercurial: evolution, changeset evolution, narrow clones
- **Evaluation criteria:** Scale, usability, ecosystem, migration cost
- **AI/ML context:** When to consider alternatives to Git

---

## Module 7: Hooks, Automation & CI/CD Integration

### 7.1 Git Hooks Architecture
- Client-side hooks: `pre-commit`, `prepare-commit-msg`, `commit-msg`, `post-commit`
- Server-side hooks: `pre-receive`, `update`, `post-receive`
- Hook execution environment: PATH, working directory, stdin/stdout
- **Implementation:** Building a comprehensive hook framework

### 7.2 Pre-Commit Hooks & Quality Gates
- Linting: `flake8`, `black`, `eslint`, `prettier`
- Type checking: `mypy`, `pyright`, `tsc`
- Security scanning: `detect-secrets`, `git-secrets`, `truffleHog`
- **Performance:** Fast hooks vs. thorough hooks, staged files only
- **AI/ML context:** Validating model configs, checking for data leaks

### 7.3 Commit Message Automation
- `prepare-commit-msg`: templating, issue linking
- `commit-msg`: validation (conventional commits, length, format)
- **Implementation:** Enforcing commit message standards across teams

### 7.4 Server-Side Hooks & Policy Enforcement
- `pre-receive`: blocking pushes based on policy
- `update`: per-ref policies
- `post-receive`: triggering CI/CD, notifications
- **Implementation:** Building a server-side policy engine

### 7.5 GitHub Actions & GitLab CI Integration
- Triggering workflows on push, pull request, merge
- Workflow design: jobs, steps, artifacts, caching
- Matrix builds and parallelization
- **AI/ML context:** Triggering model training, evaluation, and deployment from commits

### 7.6 GitOps: Version Control as Infrastructure
- GitOps principles: declarative desired state, Git as single source of truth
- Pull-based vs. push-based deployment
- Tools: ArgoCD, Flux, Jenkins X
- **AI/ML context:** GitOps for model deployments, training job specifications

### 7.7 Automated Changelog & Release Management
- Conventional commits → changelog generation
- Semantic release: automated versioning from commits
- Release note generation: PR descriptions, commit summaries
- **Implementation:** Building an automated release pipeline
- **AI/ML context:** Automated model release notes with performance metrics

---

## Module 8: Security, Compliance & Audit

### 8.1 Supply Chain Security
- The software supply chain attack surface
- Notable incidents: SolarWinds, Codecov, PyTorch nightly compromise
- Threat model for version control: insider threats, compromised accounts, malicious commits
- **Defense in depth:** Multiple security layers

### 8.2 Commit Signing & Verification
- GPG signing: setup, key management, verification
- SSH signing: simpler alternative, key rotation
- S/MIME signing: enterprise PKI integration
- **Implementation:** Organization-wide commit signing policy
- **Compliance:** Regulatory requirements (FDA, SOX, FedRAMP)

### 8.3 Secret Detection & Prevention
- Pre-commit secret scanning: `detect-secrets`, `git-secrets`
- Server-side secret scanning: GitHub secret scanning, GitLab secret detection
- Historical secret scanning: `truffleHog`, `gitLeaks`
- **Response:** Secret rotation, incident response, post-mortem
- **AI/ML context:** Preventing API keys, model access tokens, cloud credentials in commits

### 8.4 Access Control & Permissions
- Repository access levels: read, write, maintain, admin
- Branch protection rules: who can push, who can merge
- Code owners: `CODEOWNERS` file for review requirements
- **Implementation:** Least-privilege access model for ML repos
- **AI/ML context:** Protecting model weights, proprietary architectures

### 8.5 Audit Trails & Provenance
- Git's audit capabilities: reflog, `git log`, `git blame`
- Enhanced audit: server-side logging, webhook logging
- Provenance tracking: SLSA (Supply-chain Levels for Software Artifacts)
- **Implementation:** Building audit dashboards for compliance
- **AI/ML context:** Model provenance for regulatory approval (FDA, EMA)

### 8.6 Repository Backup & Disaster Recovery
- Backup strategies: mirroring, bundling, server replication
- Recovery procedures: repository corruption, accidental deletion, ransomware
- High availability: primary-replica, multi-region
- **RTO/RPO:** Recovery Time Objective, Recovery Point Objective
- **AI/ML context:** Protecting irreplaceable training data and model histories

### 8.7 Compliance & Regulatory Requirements
- SOC 2: change management, access controls, audit trails
- GDPR: data lineage, right to deletion in version history
- FDA 21 CFR Part 11: electronic records, electronic signatures
- **Implementation:** Compliance controls as code, automated evidence collection
- **AI/ML context:** Medical AI, financial AI, autonomous systems compliance

---

## Module 9: Advanced Topics & Emerging Patterns

### 9.1 CRDTs & Collaborative Editing
- Conflict-free Replicated Data Types: theory and applications
- Real-time collaborative editing: operational transform vs. CRDTs
- Git meets CRDTs: projects like GitHub Codespaces, GitDoc
- **AI/ML context:** Collaborative notebook editing, real-time experiment annotation

### 9.2 Content-Defined Chunking & Deduplication
- Rabin fingerprinting for content-defined chunking
- Deduplication strategies in version control
- BorgBackup, Restic, and modern backup systems
- **AI/ML context:** Deduplicating similar model checkpoints, incremental dataset versioning

### 9.3 Merkle Trees & Cryptographic Verification
- Merkle tree structure and properties
- Git's use of Merkle trees for integrity
- Verifiable data structures: transparency logs, certificate transparency
- **AI/ML context:** Verifiable model provenance, tamper-evident experiment logs

### 9.4 Pijul & Patch-Based Version Control
- Patch-based vs. snapshot-based version control
- Pijul's patch algebra: commutative patches, conflict handling
- **Comparison:** Pijul vs. Git for specific workflows
- **Research:** Theoretical advantages of patch-based systems

### 9.5 Version Control for Machine Learning
- ML-specific versioning: models, datasets, experiments, environments
- Integration with MLflow, W&B, Neptune, DVC
- Reproducibility: code + data + model + environment + hardware
- **Emerging:** ML-native version control systems (ModelStore, LakeFS)

### 9.6 Version Control at Hyperscale
- Google's Piper: trunk-based, sparse workflows, CitC (Clients in the Cloud)
- Meta's Sapling: virtualized working copies, transparent scaling
- Microsoft's GVFS: virtual file system for massive repos
- **Lessons learned:** What works at 10,000+ engineer scale
- **AI/ML context:** Applying hyperscale lessons to ML platform teams

### 9.7 Future of Version Control
- AI-assisted version control: commit message generation, conflict resolution
- Semantic version control: AST-aware diff, code understanding
- Decentralized version control: IPFS, blockchain-based provenance
- **Critical analysis:** Hype vs. reality in emerging VCS technologies

---

## Capstone Projects

### Project 1: Monorepo Architecture for ML Platform
Design and implement a version control strategy for an ML platform with:
- Monorepo structure: models, training code, serving infrastructure, datasets
- Git LFS or DVC integration for large files
- Sparse checkout configuration for different team workflows
- Branch protection and quality gates
- Performance optimization for 100+ engineers
- Documentation and migration plan

### Project 2: Secure, Compliant Version Control System
Implement a hardened version control workflow with:
- Mandatory commit signing (GPG or SSH)
- Server-side secret scanning and blocking
- Audit trail collection and dashboard
- Compliance controls for regulated industry (medical/financial AI)
- Incident response procedures
- Security documentation and threat model

### Project 3: Automated ML Experiment Reproducibility System
Build a system that ensures experiment reproducibility through version control:
- Integration of code, data, model, and environment versioning
- Automated experiment tracking linked to commits
- Reproducibility verification: re-run and compare
- Dashboard for experiment lineage and comparison
- Integration with CI/CD for automated experiment pipelines

### Project 4: Version Control Performance Optimization
Take a large, slow repository and optimize it:
- Analyze bottlenecks: clone time, status time, log time
- Implement partial clone, sparse checkout, sparse index
- Optimize packfiles and repository maintenance
- Measure and document improvements
- Create runbook for ongoing maintenance

---

## Assessment & Evaluation

### Knowledge Checks
- **Module quizzes:** Git internals, workflow design, security principles
- **Practical exercises:** Repository manipulation, conflict resolution, history rewriting
- **Architecture reviews:** Design version control strategies for given scenarios

### Practical Assessments
- **Implementation exercises:** Build hooks, automation, custom tools
- **Troubleshooting:** Diagnose and fix complex repository states
- **Security audit:** Review repository configuration for vulnerabilities

### Capstone Evaluation
- **Design document:** Architecture and trade-off analysis
- **Implementation:** Working system with documentation
- **Presentation:** Technical communication and defense
- **Operations:** Demonstrate monitoring, maintenance, and incident response

---

## Recommended Resources

### Books
- "Pro Git" — Scott Chacon, Ben Straub (free online, definitive reference)
- "Git Internals" — Scott Chacon (Plumbing commands deep dive)
- "Building Git" — James Coglan (implementing Git from scratch)
- "Version Control with Git" — Jon Loeliger, Matthew McCullough
- "Monorepo.tools" — Various authors (monorepo patterns and tools)

### Official Documentation
- Git official documentation: git-scm.com
- GitHub Docs: docs.github.com
- GitLab Docs: docs.gitlab.com
- DVC documentation: dvc.org

### Papers & Articles
- "The Git Parable" — Tom Preston-Werner
- "Git from the Bottom Up" — John Wiegley
- Google's monorepo papers (2016, 2020)
- "Sapling: Source Control at Scale" — Meta Engineering
- SLSA framework documentation (supply chain security)

### Tools & Technologies
- **Git:** Core tool, git-scm.com
- **Git LFS:** git-lfs.github.com
- **DVC:** dvc.org
- **Pre-commit:** pre-commit.com
- **GitHub/GitLab/Bitbucket:** Hosting platforms
- **Gerrit:** Code review system
- **BFG Repo-Cleaner:** rtyley.github.io/bfg-repo-cleaner
- **git-filter-repo:** github.com/newren/git-filter-repo

---

## Study Schedule

### Intensive Track (12 weeks, 20-25 hrs/week)

| Week | Modules | Focus |
|------|---------|-------|
| 1 | 0, 1.1-1.3 | Philosophy, object model, directory structure |
| 2 | 1.4-1.7 | Refs, index, packfiles, plumbing |
| 3 | 2.1-2.4 | Branch semantics, GitFlow, GitHub Flow, trunk-based |
| 4 | 2.5-2.7 | Branch protection, release branching, long-running branches |
| 5 | 3.1-3.4 | Three-way merge, recursive merge, conflict resolution, structural merge |
| 6 | 3.5-3.7 | Rebase, cherry-pick, merge queues |
| 7 | 4.1-4.4 | Commit rewriting, filter-branch, BFG, submodules |
| 8 | 4.5-4.7 | Worktree, partial clone, sparse checkout, shallow clone |
| 9 | 5.1-5.4 | Forks, code review, signed commits, attribution |
| 10 | 5.5-5.7, 6.1-6.3 | Commit communication, large teams, monorepo philosophy, Git scaling |
| 11 | 6.4-6.7 | DVC, repo splitting, performance, alternative VCS |
| 12 | 7-9 | Hooks, CI/CD, security, advanced topics, capstone |

### Self-Paced Track (16 weeks, 15-20 hrs/week)

Follow the same module sequence with additional time for:
- Deep implementation exercises (building Git plumbing tools)
- Experimentation with alternative VCS (Sapling, Jujutsu)
- Performance benchmarking and optimization
- Extended capstone development

---

## Meta-Learning: How to Use This Syllabus

1. **Build Git from Understanding:** Don't just use Git—understand why it works. Read the object model, parse the index, build tools.
2. **Practice Recovery:** Deliberately break repositories and recover them. The best Git users are those who've survived disasters.
3. **Measure Everything:** Track clone times, repo sizes, operation latencies. Optimization requires measurement.
4. **Think in Systems:** Version control is infrastructure, not just a tool. Design for scale, security, and operability from day one.
5. **Connect to ML Workflows:** Every concept should be applied to the unique challenges of AI/ML: large files, experiments, reproducibility.

---

## Conclusion

Version control is the invisible backbone of every modern engineering organization. In AI/ML systems, where reproducibility is not merely desirable but scientifically and regulatorily mandatory, the quality of version control practices directly determines the trustworthiness of results.

The best ML infrastructure engineers don't just "use Git"—they design version control systems that scale to terabytes of model artifacts, enforce security and compliance without blocking research velocity, and provide complete provenance trails from data ingestion through model deployment. They understand Git at the object level, design workflows for organizational dynamics, and treat version control as a first-class system component with SLOs and runbooks.

This syllabus provides the rigorous, systems-level training needed to reach that level of engineering excellence.

---

*Last Updated: 2026-05-20*
*Version: 1.0*
*Target Level: Staff+ Engineer / Principal Engineer*