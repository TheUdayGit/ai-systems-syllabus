  
 ## File: llm-engineering-syllabus.md

# Large Language Model (LLM) Engineering: From First Principles to Production Systems

## A University-Level, Industry-Grade Technical Syllabus

**Version:** 2026.05  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Solid Python, linear algebra, probability, deep learning fundamentals, distributed systems basics, and systems programming comfort  
**Estimated Duration:** 400–500 hours of focused study + 200 hours of capstone projects  
**Last Updated:** May 2026

---

## Table of Contents

1. [Meta: How to Use This Syllabus](#meta-how-to-use-this-syllabus)
2. [Phase 0: Mathematical & Systems Prerequisites](#phase-0-mathematical--systems-prerequisites)
3. [Phase 1: Foundational Theory — The Transformer Architecture](#phase-1-foundational-theory--the-transformer-architecture)
4. [Phase 2: Pretraining at Scale — Data, Compute, and Optimization](#phase-2-pretraining-at-scale--data-compute-and-optimization)
5. [Phase 3: Alignment — SFT, RLHF, DPO, and Beyond](#phase-3-alignment--sft-rlhf-dpo-and-beyond)
6. [Phase 4: Inference Engineering — Serving LLMs in Production](#phase-4-inference-engineering--serving-llms-in-production)
7. [Phase 5: Retrieval-Augmented Generation (RAG) & Context Engineering](#phase-5-retrieval-augmented-generation-rag--context-engineering)
8. [Phase 6: Agentic Systems, Tool Use, and Multi-Agent Orchestration](#phase-6-agentic-systems-tool-use-and-multi-agent-orchestration)
9. [Phase 7: Production MLOps, Observability, and Governance](#phase-7-production-mlops-observability-and-governance)
10. [Phase 8: Security, Evaluation, and Red Teaming](#phase-8-security-evaluation-and-red-teaming)
11. [Phase 9: Advanced Topics & Research Frontiers](#phase-9-advanced-topics--research-frontiers)
12. [Capstone Projects](#capstone-projects)
13. [Assessment & Certification Rubric](#assessment--certification-rubric)
14. [Recommended Reading & Reference Library](#recommended-reading--reference-library)

---

## Meta: How to Use This Syllabus

This syllabus is designed as a **self-contained, progressive curriculum** that transforms a strong software engineer into a production-grade LLM systems engineer. Each phase builds upon the previous, with explicit dependency chains.

**Study Protocol:**
- **Theory → Implementation → Systems → Production:** Every concept must be understood mathematically, implemented from scratch (where feasible), integrated into a system, and operationalized.
- **Spaced Reinforcement:** Concepts from earlier phases reappear in later phases at increasing depth.
- **Build-Measure-Learn:** Every module includes explicit debugging, profiling, and benchmarking exercises.
- **Architecture Reasoning:** Each phase includes design exercises requiring trade-off analysis (latency vs. throughput, accuracy vs. cost, consistency vs. availability).

**Required Tools & Environment:**
- Python 3.11+, PyTorch 2.3+, CUDA 12.x
- Access to GPU instances (A100/H100/B200 or cloud equivalents)
- Kubernetes cluster access for distributed training experiments
- vLLM, Ray, DeepSpeed, and HuggingFace Transformers installed

---

## Phase 0: Mathematical & Systems Prerequisites

> **Objective:** Establish the mathematical language and systems intuition required for rigorous LLM engineering. Skip only if you can derive backpropagation through attention, explain why matrix multiplication is memory-bound, and debug a distributed deadlock.

### 0.1 Linear Algebra for Deep Learning
- **Vector Spaces & Subspaces:** Bases, linear independence, rank, null space
- **Matrix Decompositions:** SVD, eigendecomposition, QR, Cholesky — computational complexity and numerical stability
- **Tensor Operations:** Einstein summation, tensor contractions, batched matrix operations
- **Numerical Linear Algebra:** Condition numbers, floating-point arithmetic (IEEE 754), mixed-precision training implications
- **Key Exercise:** Implement a numerically stable softmax and layer normalization from scratch. Profile memory access patterns.

### 0.2 Probability & Information Theory
- **Probability Distributions:** Gaussian mixtures, categorical distributions, KL divergence, JS divergence
- **Information Theory:** Entropy, cross-entropy, mutual information, perplexity as an information-theoretic measure
- **Maximum Likelihood Estimation:** Derivation, properties, connection to cross-entropy loss
- **Bayesian Inference:** Priors, posteriors, variational inference basics (relevant for uncertainty quantification)
- **Key Exercise:** Compute the perplexity of a trained model on a held-out set. Explain why lower perplexity doesn't always mean better generation.

### 0.3 Optimization Theory
- **Convex & Non-Convex Optimization:** Gradient descent convergence, saddle points, local minima in high dimensions
- **Stochastic Gradient Descent:** Mini-batch statistics, learning rate schedules, momentum, Nesterov acceleration
- **Adaptive Optimizers:** Adam, AdamW (decoupled weight decay), Lion, Adafactor — mathematical derivation and hyperparameter sensitivity
- **Second-Order Methods:** L-BFGS basics, Hessian-vector products, why they don't scale to LLMs
- **Distributed Optimization:** Data parallelism, model parallelism, pipeline parallelism — convergence guarantees and staleness analysis
- **Key Exercise:** Implement AdamW from scratch. Train a small transformer and compare convergence with different β₁, β₂ configurations.

### 0.4 Systems Fundamentals
- **Computer Architecture:** CPU vs. GPU memory hierarchy, cache lines, coalesced memory access, warp scheduling
- **CUDA Programming Model:** Kernels, threads, blocks, grids, shared memory, constant memory, texture memory
- **GPU Profiling:** Nsight Compute, Nsight Systems, roofline model analysis
- **Distributed Systems Basics:** CAP theorem, consensus (Raft/Paxos), message passing vs. shared memory, backpressure
- **Networking for ML:** RDMA, InfiniBand, NCCL collectives (all-reduce, all-gather, reduce-scatter), bandwidth vs. latency bottlenecks
- **Key Exercise:** Write a CUDA kernel for vector addition. Profile memory bandwidth utilization. Implement a ring-allreduce in Python using MPI.

### 0.5 Deep Learning Foundations
- **Neural Network Basics:** MLPs, activation functions (ReLU, GELU, SwiGLU), initialization schemes (Xavier, Kaiming)
- **Convolutional & Recurrent Networks:** Brief review — why they fail for long sequences
- **Autodifferentiation:** Computational graphs, forward-mode vs. reverse-mode AD, memory complexity of backprop
- **PyTorch Internals:** ATen, TorchScript, `torch.compile`, Dynamo, Inductor, Triton kernels
- **Key Exercise:** Implement a computational graph framework supporting automatic differentiation. Build a simple MLP and verify gradients against finite differences.

---

## Phase 1: Foundational Theory — The Transformer Architecture

> **Objective:** Understand the transformer at the level of matrix operations, memory access patterns, and numerical stability. Build intuition for why attention works, when it fails, and how to optimize it.

### 1.1 The Attention Mechanism
- **Scaled Dot-Product Attention:** Query-Key-Value formulation, mathematical derivation, O(n²) complexity analysis
- **Self-Attention vs. Cross-Attention:** Bidirectional encoding, causal masking for autoregressive generation
- **Multi-Head Attention:** Parallel attention heads, concatenation and projection, head dimension trade-offs
- **Attention as Soft Dictionary Lookup:** Information retrieval interpretation, attention weights as importance scores
- **Numerical Stability:** Softmax temperature scaling, attention score clipping, mixed-precision considerations
- **Key Exercise:** Implement attention from scratch in NumPy. Verify outputs match PyTorch. Profile FLOPs and memory for sequence lengths 512, 2048, 8192.

### 1.2 Positional Encoding
- **Sinusoidal Encodings:** Mathematical formulation, relative position bias, wavelength analysis
- **Learned Positional Embeddings:** Trade-offs vs. sinusoidal, extrapolation challenges
- **Rotary Position Embeddings (RoPE):** Complex number formulation, rotation matrices, long-sequence extrapolation (NTK-aware scaling, YaRN)
- **ALiBi & Other Alternatives:** Linear biases, extrapolation without fine-tuning
- **Key Exercise:** Implement RoPE. Test interpolation vs. extrapolation on sequences longer than training length.

### 1.3 The Transformer Block
- **Layer Normalization:** Pre-norm vs. post-norm, RMSNorm, numerical stability in mixed precision
- **Feed-Forward Networks:** GELU, SwiGLU activation, up-projection and down-projection dimensions, MoE routing basics
- **Residual Connections:** Gradient flow, vanishing gradients, deep network trainability
- **The Complete Block:** Forward pass data flow, backward pass gradient flow, activation checkpointing
- **Key Exercise:** Implement a full transformer block. Compare pre-norm vs. post-norm training stability on a small dataset.

### 1.4 Architecture Variants
- **Encoder-Only (BERT-style):** Masked language modeling, bidirectional context, downstream fine-tuning
- **Decoder-Only (GPT-style):** Autoregressive generation, causal masking, next-token prediction
- **Encoder-Decoder (T5-style):** Cross-attention, sequence-to-sequence modeling, denoising objectives
- **Mixture of Experts (MoE):** Sparse activation, routing algorithms (Top-K, expert choice), load balancing, capacity factor
- **State Space Models (Mamba, RWKV):** Linear attention approximations, selective state spaces, hardware-aware algorithms
- **Key Exercise:** Implement a GPT-2 scale model (124M parameters) from scratch. Train on OpenWebText. Evaluate perplexity and generation quality.

### 1.5 Tokenization
- **Byte-Pair Encoding (BPE):** Algorithm, vocabulary construction, merge rules, subword segmentation
- **SentencePiece & Unigram:** Unigram language modeling, subword regularization
- **Byte-Level BPE (BBPE):** Handling of rare characters, UTF-8 encoding, vocabulary size trade-offs
- **Tokenization Pitfalls:** Pre-tokenizer inconsistencies, whitespace handling, multilingual challenges, prompt injection via token boundaries
- **Key Exercise:** Train a BPE tokenizer on a multilingual corpus. Analyze merge operations. Test adversarial inputs that exploit token boundaries.

---

## Phase 2: Pretraining at Scale — Data, Compute, and Optimization

> **Objective:** Understand how billion-parameter models are trained. Master distributed training strategies, data pipeline engineering, and the economics of large-scale compute.

### 2.1 Data Engineering for Pretraining
- **Data Sources:** Common Crawl, C4, The Pile, GitHub code, synthetic data generation
- **Quality Filtering:** Deduplication (MinHash, SimHash), toxicity filtering, PII removal, language identification
- **Data Mixing:** Domain weighting, curriculum learning, data composition laws (Chinchilla scaling)
- **Tokenization at Scale:** Parallel processing, memory-mapped datasets, streaming vs. materialized data
- **Data Pipeline Architecture:** Apache Beam, Dataflow, Ray Data, webdataset format
- **Key Exercise:** Build a data pipeline that processes 100GB of raw text into tokenized sequences. Implement deduplication and quality filtering. Benchmark throughput.

### 2.2 Scaling Laws & Compute Budgeting
- **Chinchilla Scaling Laws:** Optimal model size vs. data size for fixed compute, over/under-training analysis
- **Kaplan vs. Chinchilla:** Revised scaling laws, empirical vs. theoretical predictions
- **Emergent Abilities:** Definition, controversy, measurement, and predictability
- **Compute Estimation:** FLOPs per token, total training FLOPs, GPU-hours, cost modeling
- **Key Exercise:** Given a $1M compute budget, design a training run. Specify model size, data size, batch size, and training duration. Justify every choice.

### 2.3 Distributed Training Fundamentals
- **Data Parallelism (DP):** Gradient accumulation, synchronous vs. asynchronous updates, batch size scaling
- **Distributed Data Parallel (DDP):** `torch.nn.parallel.DistributedDataParallel`, gradient bucketing, overlap computation and communication
- **Fully Sharded Data Parallel (FSDP):** ZeRO-1/2/3, parameter sharding, gradient sharding, optimizer state sharding, auto-wrapping policies
- **FSDP2 (2026):** 2D parallelism, hybrid sharding, reduced communication overhead
- **Key Exercise:** Train a 1B parameter model using FSDP on 8 GPUs. Profile communication overhead. Experiment with different sharding strategies.

### 2.4 Model & Pipeline Parallelism
- **Tensor Parallelism (TP):** Column-wise and row-wise splitting, all-reduce communication, Megatron-LM implementation
- **Pipeline Parallelism (PP):** GPipe, PipeDream, bubble time analysis, micro-batching, activation checkpointing
- **3D Parallelism:** Combining DP, TP, and PP, communication topology design
- **Sequence Parallelism:** Reducing activation memory for long sequences, context parallelism
- **Key Exercise:** Implement tensor parallelism for a transformer layer. Measure throughput vs. baseline. Analyze communication patterns.

### 2.5 Advanced Training Techniques
- **Mixed Precision Training:** FP16/BF16/FP8, loss scaling, gradient scaling, automatic mixed precision (AMP)
- **Gradient Clipping & Accumulation:** Norm-based clipping, value-based clipping, large batch stability
- **Learning Rate Schedules:** Warmup, cosine decay, linear decay, inv_sqrt, schedule-free optimizers
- **Regularization:** Dropout (attention and residual), weight decay, label smoothing, MixUp/CutMix for NLP
- **Checkpointing & Fault Tolerance:** Synchronous checkpointing, asynchronous checkpointing, checkpoint sharding, resume from failure
- **Key Exercise:** Implement mixed-precision training with automatic loss scaling. Train to convergence and compare wall-clock time vs. full FP32.

### 2.6 Training Frameworks & Infrastructure
- **PyTorch Distributed:** `torchrun`, process groups, NCCL backend, environment configuration
- **DeepSpeed:** ZeRO stages, CPU offloading, NVMe offloading, 1-bit Adam, pipeline parallelism integration
- **Megatron-LM:** NVIDIA's framework for large-scale training, tensor and pipeline parallelism, distributed optimizer
- **JAX/Flax:** XLA compilation, `pmap`, `vmap`, `pjit`, TPU training, functional programming paradigm
- **Ray Train:** Distributed training orchestration, hyperparameter tuning integration, fault tolerance
- **Key Exercise:** Set up a multi-node training job using DeepSpeed ZeRO-3. Train a 7B parameter model. Monitor GPU memory utilization and communication bandwidth.

### 2.7 Training Stability & Debugging
- **Loss Spikes:** Causes (bad data points, gradient explosions, learning rate too high), detection, mitigation
- **Dead ReLU & Vanishing Gradients:** Detection via activation histograms, mitigation strategies
- **Numerical Instability:** NaN/Inf detection, mixed-precision pitfalls, gradient scaling debugging
- **Distributed Debugging:** Deadlocks, race conditions, NCCL timeouts, collective operation mismatches
- **Observability:** TensorBoard, Weights & Biases, logging strategies, gradient norm tracking, activation statistics
- **Key Exercise:** Intentionally introduce a bug (e.g., misconfigured learning rate) and debug it using gradient norm tracking and activation histograms.

---

## Phase 3: Alignment — SFT, RLHF, DPO, and Beyond

> **Objective:** Master the techniques that transform a pretrained base model into a helpful, harmless, and honest assistant. Understand the infrastructure, algorithms, and failure modes of alignment.

### 3.1 Supervised Fine-Tuning (SFT)
- **Instruction Tuning:** Dataset curation (Alpaca, ShareGPT, UltraChat), prompt templates, multi-turn conversations
- **Multi-Turn Conversation Modeling:** Loss masking (only compute loss on assistant tokens), conversation formatting
- **Chat Templates:** System prompts, user/assistant roles, special tokens, template injection risks
- **SFT Hyperparameters:** Learning rate (typically 1e-5 to 5e-5), batch size, epochs, overfitting detection
- **Key Exercise:** Fine-tune a 7B model on an instruction dataset. Evaluate on MT-Bench. Analyze failure modes.

### 3.2 Reward Modeling
- **Preference Data Collection:** Pairwise comparisons, Likert scales, Elo ratings, human vs. synthetic labels
- **Bradley-Terry Model:** Probability formulation, maximum likelihood estimation, connection to reward modeling
- **Reward Model Architecture:** Initialize from SFT model, regression head, loss function (pairwise ranking loss)
- **Reward Hacking:** Specification gaming, reward model overoptimization, length bias, style bias
- **Key Exercise:** Train a reward model on a preference dataset. Evaluate ranking accuracy. Analyze reward distribution for different response lengths.

### 3.3 Reinforcement Learning from Human Feedback (RLHF)
- **PPO for Language Models:** Policy gradient, clipped surrogate objective, value function estimation, advantage computation (GAE)
- **The Four Models in PPO:** Actor, critic, reference, reward — memory requirements, update frequencies
- **KL Divergence Penalty:** Controlling deviation from the reference policy, β tuning, theoretical justification
- **Training Instability:** Reward spikes, entropy collapse, value function divergence, gradient clipping strategies
- **Key Exercise:** Implement PPO for a small language model (e.g., 1B parameters). Train on a simple task (e.g., sentiment control). Monitor KL divergence and reward curves.

### 3.4 RLHF Infrastructure & Frameworks (2026)
- **verl (ByteDance):** HybridEngine, in-place weight swapping between FSDP and vLLM, Megatron-LM integration, YAML configuration
- **OpenRLHF:** Ray-based actor pools, heterogeneous cluster support, vLLM rollout workers, parallel training and generation
- **TRL (HuggingFace):** Standard `Trainer` API, Accelerate integration, FSDP/DeepSpeed backends, ease of use for <30B models
- **Framework Selection Criteria:** Scale (7B vs. 70B+), cluster homogeneity, team expertise, integration with existing stack
- **Key Exercise:** Set up a PPO run using OpenRLHF on a multi-node cluster. Configure actor, critic, reference, and reward model placement. Monitor VRAM utilization per role.

### 3.5 Direct Preference Optimization (DPO) & Alternatives
- **DPO Derivation:** Closed-form policy extraction, no reward model needed, implicit reward modeling
- **DPO vs. PPO:** Computational efficiency, stability, performance trade-offs, when to use which
- **IPO (Identity Preference Optimization):** Handling preference noise, theoretical improvements
- **KTO (Kahneman-Tversky Optimization):** Binary feedback, avoiding pairwise comparisons
- **RLAIF (AI Feedback):** Constitutional AI, self-critique and revision, scalable oversight
- **Key Exercise:** Implement DPO from scratch. Compare with PPO on the same preference dataset. Analyze training stability and final policy quality.

### 3.6 GRPO & Reasoning-Time Scaling
- **Group Relative Policy Optimization (GRPO):** Eliminating the critic model, group-relative advantage estimates, verifiable rewards
- **Reasoning-Time Compute:** Test-time scaling, chain-of-thought prompting, self-consistency, majority voting
- **Process Reward Models:** Step-by-step reward modeling, credit assignment in reasoning
- **Key Exercise:** Implement GRPO for a mathematical reasoning task. Compare sample efficiency with PPO.

### 3.7 Alignment Failure Modes & Safety
- **Reward Hacking:** Examples (length exploitation, keyword stuffing), detection, mitigation
- **Jailbreaking:** Prompt injection, roleplay attacks, encoding attacks, defense mechanisms
- **Alignment Faking:** Deceptive alignment, situational awareness, evaluation gaming
- **Constitutional AI:** Principles-based training, self-critique, revision loops
- **Key Exercise:** Red-team a fine-tuned model. Document 5 distinct jailbreak techniques and their success rates. Implement a defense mechanism.

---

## Phase 4: Inference Engineering — Serving LLMs in Production

> **Objective:** Master the art and science of serving LLMs at scale. Optimize for latency, throughput, cost, and reliability. This is where theory meets the economics of production AI.

### 4.1 Inference Basics
- **Autoregressive Generation:** Token-by-token decoding, temperature sampling, top-k, top-p (nucleus sampling), beam search
- **KV Cache Management:** Cache allocation, preallocation strategies, memory fragmentation, prefix caching
- **Batching:** Static batching vs. dynamic batching, padding and packing, batch size trade-offs
- **Quantization:** INT8, INT4, FP8, GPTQ, AWQ, GGUF, smooth quantization — accuracy vs. speed vs. memory
- **Key Exercise:** Implement greedy decoding and top-p sampling from scratch. Measure generation time vs. sequence length.

### 4.2 High-Throughput Serving
- **Continuous Batching (In-Flight Batching):** Iteration-level scheduling, preemption, recomputation, chunked prefill
- **PagedAttention (vLLM):** Block-based KV cache management, memory sharing (copy-on-write), throughput improvements
- **vLLM Architecture:** Scheduler, worker processes, tensor parallelism, pipeline parallelism, OpenAI-compatible API
- **SGLang:** Structured generation, RadixAttention for prefix caching, speculative execution
- **TensorRT-LLM:** NVIDIA's optimized inference engine, plugin system, multi-GPU support
- **Key Exercise:** Deploy a 70B model with vLLM. Benchmark throughput at batch sizes 1, 8, 32, 64. Analyze latency percentiles (p50, p95, p99).

### 4.3 Latency Optimization
- **Speculative Decoding:** Draft model, token tree verification, acceptance rates, speedup analysis
- **Medusa & Lookahead Decoding:** Multiple draft heads, n-gram-based speculation
- **Prompt Caching:** Prefix matching, RadixAttention, common prefix exploitation
- **Disaggregated Serving:** Separating prefill and decode phases, phase-specific optimization
- **Key Exercise:** Implement speculative decoding with a small draft model. Measure speedup on different prompt lengths.

### 4.4 Model Compression & Quantization
- **Post-Training Quantization (PTQ):** GPTQ (layer-wise quantization, optimal brain quantization), AWQ (activation-aware), SmoothQuant
- **Quantization-Aware Training (QAT):** Simulated quantization, straight-through estimators, accuracy recovery
- **FP8 Inference:** Hardware support (H100/B200), mixed FP8/FP16 computation, dynamic scaling
- **Pruning:** Structured vs. unstructured, magnitude pruning, movement pruning, sparse inference
- **Key Exercise:** Quantize a 7B model to INT4 using GPTQ. Deploy with vLLM. Measure perplexity degradation and throughput improvement.

### 4.5 Multi-Model & Multi-LoRA Serving
- **Multi-LoRA Inference:** Adapter swapping, base model sharing, memory-efficient serving
- **Model Ensemble:** Router models, mixture of agents, cascade serving (small → large)
- **A/B Testing:** Shadow traffic, canary deployments, statistical significance testing
- **Key Exercise:** Build a serving system that hosts 10 LoRA adapters on a single 70B base model. Measure cold-start latency and concurrent request handling.

### 4.6 Inference Infrastructure & Observability
- **Load Balancing:** Request routing, least-loaded, token-based routing, session affinity
- **Auto-scaling:** GPU cluster autoscaling, queue-depth-based scaling, predictive scaling
- **Circuit Breakers & Fallbacks:** Degradation strategies, cached responses, smaller model fallback
- **Observability:** Token throughput, time-to-first-token (TTFT), time-per-output-token (TPOT), queue depth, GPU utilization
- **Key Exercise:** Build a production-ready inference service with Kubernetes. Implement auto-scaling, circuit breakers, and comprehensive metrics dashboards.

---

## Phase 5: Retrieval-Augmented Generation (RAG) & Context Engineering

> **Objective:** Build systems that ground LLM outputs in external knowledge. Master retrieval, context management, and the production patterns that separate working RAG from demo RAG.

### 5.1 Embedding Models & Dense Retrieval
- **Embedding Architecture:** Bi-encoders, sentence transformers, contrastive training, in-batch negatives
- **Training Embeddings:** NLI datasets, hard negative mining, InfoNCE loss, temperature scaling
- **Vector Databases:** FAISS, Milvus, Pinecone, Weaviate, pgvector — indexing (IVF, HNSW), quantization, filtering
- **Dense Passage Retrieval (DPR):** End-to-end training, passage encoding, query encoding
- **Key Exercise:** Fine-tune an embedding model for a domain-specific retrieval task. Build a FAISS index. Evaluate recall@k.

### 5.2 RAG Pipeline Architecture
- **Indexing Pipeline:** Document parsing, chunking strategies (fixed, semantic, hierarchical), metadata extraction
- **Retrieval Strategies:** Dense, sparse (BM25), hybrid, reranking (cross-encoders, ColBERT)
- **Context Assembly:** Top-k selection, context window management, relevance scoring, deduplication
- **Generation with Retrieval:** Retrieval-augmented prompt construction, citation generation, faithfulness constraints
- **Key Exercise:** Build an end-to-end RAG system for technical documentation. Implement hybrid retrieval with reranking. Evaluate answer accuracy and citation correctness.

### 5.3 Advanced RAG Patterns
- **Query Rewriting:** Hypothetical document embeddings (HyDE), query expansion, decomposition
- **Multi-Step RAG:** Iterative retrieval, chain-of-thought retrieval, self-ask
- **Agentic RAG:** Tool use for retrieval, dynamic query formulation, source verification
- **GraphRAG:** Knowledge graph construction, community detection, global vs. local search
- **Key Exercise:** Implement a multi-step RAG system that handles complex multi-hop questions. Compare with baseline single-step RAG.

### 5.4 Context Engineering & Memory Systems
- **Context Window Management:** Sliding window, hierarchical attention, compression techniques
- **Long-Context Models:** RoPE scaling, YaRN, positional interpolation, attention sink patterns
- **Memory Architectures:** Short-term (conversation history), medium-term (session summaries), long-term (user profiles, knowledge bases)
- **Context Protocols:** Model Context Protocol (MCP), structured context boundaries, tool schemas
- **Key Exercise:** Design a memory system for a personal assistant that maintains user preferences across sessions. Implement context summarization and retrieval.

### 5.5 RAG Evaluation & Production Hardening
- **Retrieval Metrics:** Recall@k, MRR, NDCG, latency percentiles
- **Generation Metrics:** Faithfulness, answer relevance, context precision, hallucination detection
- **RAGAS Framework:** Automated evaluation pipeline, component-wise metrics
- **Production Challenges:** Index freshness, version management, schema evolution, cost optimization
- **Key Exercise:** Build an evaluation pipeline for your RAG system. Measure retrieval and generation metrics. Implement A/B testing for different chunking strategies.

---

## Phase 6: Agentic Systems, Tool Use, and Multi-Agent Orchestration

> **Objective:** Design and implement autonomous AI systems that interact with the world through tools, reasoning, and collaboration. Focus on reliability, observability, and production-grade orchestration.

### 6.1 Tool Use & Function Calling
- **Function Calling Architecture:** Schema definition, JSON mode, constrained decoding, tool selection
- **Tool Implementation:** Idempotency, error handling, timeouts, rate limiting, retry logic
- **Tool-Augmented LLMs:** ReAct pattern, chain-of-thought tool use, observation integration
- **Key Exercise:** Build a calculator tool and a web search tool. Implement a ReAct agent that solves math problems using these tools.

### 6.2 Agent Architectures
- **ReAct:** Reasoning and acting interleaved, thought-action-observation loops
- **Plan-and-Solve:** Decomposition, subgoal generation, execution monitoring
- **Reflexion:** Self-evaluation, error detection, retry with correction
- **Tree of Thoughts:** BFS/DFS over reasoning paths, evaluation pruning, backtracking
- **Key Exercise:** Implement a Tree of Thoughts solver for a planning problem. Compare node expansion strategies.

### 6.3 Multi-Agent Systems
- **Agent Roles & Specialization:** Router agents, worker agents, critic agents, verifier agents
- **Communication Patterns:** Direct messaging, broadcast, shared memory, blackboard architecture
- **Coordination Mechanisms:** Consensus, voting, hierarchy, market-based allocation
- **Failure Modes:** Deadlocks, livelocks, conflicting actions, shared context corruption
- **Key Exercise:** Build a multi-agent system where one agent researches a topic, another writes a summary, and a third verifies accuracy. Implement conflict resolution.

### 6.4 Model Context Protocol (MCP) & Standards
- **MCP Architecture:** Hosts, clients, servers, tools, resources, prompts
- **MCP Server Implementation:** Schema definition, capability negotiation, transport (stdio, SSE)
- **Integration Patterns:** Connecting agents to databases, APIs, file systems via MCP
- **Observability in MCP:** Request tracing, tool call logging, context boundary enforcement
- **Key Exercise:** Implement an MCP server for a custom API. Connect it to an agent using the MCP client. Trace all tool calls.

### 6.5 Production Agent Engineering
- **Reliability Patterns:** Idempotency, determinism, state persistence, checkpointing
- **Observability:** Agent trajectory logging, decision tracing, tool call auditing
- **Safety Guardrails:** Output validation, sandboxing, permission systems, human-in-the-loop
- **Testing:** Mock tool responses, golden trajectory tests, property-based testing for agent behavior
- **Key Exercise:** Build a production-grade agent with comprehensive logging, error handling, and safety guardrails. Write unit and integration tests.

---

## Phase 7: Production MLOps, Observability, and Governance

> **Objective:** Operationalize LLM systems with the rigor of production software engineering. Implement CI/CD, monitoring, cost governance, and compliance.

### 7.1 LLM Infrastructure as Code
- **Containerization:** Docker for training and serving, multi-stage builds, layer caching
- **Orchestration:** Kubernetes for GPU workloads, device plugins, resource quotas, node affinity
- **Infrastructure Provisioning:** Terraform, Pulumi, cloud-specific GPU instance management
- **Key Exercise:** Write Terraform configurations for a multi-zone GPU cluster. Implement node pools for training and inference.

### 7.2 CI/CD for LLMs
- **Model Versioning:** DVC, MLflow Model Registry, HuggingFace Hub, Git LFS for checkpoints
- **Training Pipelines:** Kubeflow, Airflow, Prefect — pipeline definition, dependency management, artifact tracking
- **Evaluation Gates:** Automated benchmarking, regression detection, quality thresholds
- **Deployment Strategies:** Blue-green, canary, shadow deployments for model updates
- **Key Exercise:** Build a CI/CD pipeline that trains a model, runs evaluation benchmarks, and deploys to production if quality thresholds are met.

### 7.3 Observability & Monitoring
- **Metrics:** Token throughput, latency percentiles, error rates, GPU utilization, memory pressure
- **Logging:** Structured logging, request tracing, correlation IDs, distributed tracing (Jaeger, Zipkin)
- **Alerting:** SLO definition, alert thresholds, on-call runbooks, incident response
- **Cost Tracking:** Per-request cost attribution, budget alerts, chargeback mechanisms
- **Key Exercise:** Set up a monitoring stack (Prometheus + Grafana) for an inference service. Define SLOs and create alerting rules.

### 7.4 Cost Governance & Optimization
- **Compute Cost Modeling:** GPU pricing, spot vs. on-demand, reserved instances, autoscaling economics
- **Request Routing:** Model routing based on complexity, cost-aware load balancing, caching strategies
- **Token Budgeting:** Rate limiting, quota management, token-based billing, prompt optimization
- **Key Exercise:** Implement a cost-aware request router that selects between a small and large model based on query complexity. Track cost savings.

### 7.5 Compliance & Governance
- **Data Privacy:** GDPR, CCPA, data retention, anonymization, consent management
- **Model Governance:** Bias detection, fairness metrics, explainability requirements, audit trails
- **Content Safety:** Toxicity filtering, PII detection, output moderation, compliance reporting
- **Key Exercise:** Implement a PII detection and redaction pipeline. Build an audit log for all model interactions.

---

## Phase 8: Security, Evaluation, and Red Teaming

> **Objective:** Ensure LLM systems are robust, safe, and trustworthy. Master systematic evaluation, adversarial testing, and security hardening.

### 8.1 LLM Evaluation Frameworks
- **Benchmarks:** MMLU, HellaSwag, TruthfulQA, HumanEval, MT-Bench, Arena Elo
- **Custom Evaluation:** Task-specific metrics, human evaluation protocols, inter-annotator agreement
- **Automated Evaluation:** LLM-as-a-judge, rubric-based scoring, consistency checks
- **DeepEval & RAGAS:** Framework implementation, metric customization, CI integration
- **Key Exercise:** Build an evaluation suite for a domain-specific task. Implement both automated and human evaluation protocols.

### 8.2 Adversarial Testing & Red Teaming
- **Prompt Injection:** Direct injection, indirect injection, jailbreak techniques, defense mechanisms
- **Data Poisoning:** Training data attacks, backdoor insertion, mitigation strategies
- **Model Extraction:** API-based extraction, distillation attacks, watermarking
- **PyRIT Framework:** Microsoft's red-teaming framework, attack orchestration, multi-modal attacks
- **Key Exercise:** Conduct a red-teaming exercise on a production LLM system. Document vulnerabilities and remediation steps.

### 8.3 Safety & Alignment Evaluation
- **Toxicity Detection:** Perspective API, custom classifiers, multi-language challenges
- **Bias Evaluation:** Gender bias, racial bias, stereotype detection, fairness metrics
- **Robustness:** Out-of-distribution detection, adversarial robustness, stress testing
- **Key Exercise:** Evaluate a model for gender bias in professional role generation. Implement debiasing techniques.

### 8.4 OWASP Top 10 for LLM Applications
- **LLM01: Prompt Injection** — Input validation, output encoding, privilege separation
- **LLM02: Insecure Output Handling** — Sanitization, encoding, secure parsing
- **LLM03: Training Data Poisoning** — Data provenance, anomaly detection, sandboxing
- **LLM04: Model Denial of Service** — Rate limiting, resource management, input size constraints
- **LLM05: Supply Chain Vulnerabilities** — Model provenance, dependency scanning, SBOMs
- **LLM06: Sensitive Information Disclosure** — PII detection, data masking, access controls
- **LLM07: Insecure Plugin Design** — Input validation, least privilege, sandboxing
- **LLM08: Excessive Agency** — Permission boundaries, human approval, action constraints
- **LLM09: Overreliance** — Confidence calibration, uncertainty quantification, human oversight
- **LLM10: Model Theft** — API security, watermarking, access logging
- **Key Exercise:** Audit an LLM application against the OWASP Top 10. Implement mitigations for the top 3 risks.

---

## Phase 9: Advanced Topics & Research Frontiers

> **Objective:** Explore cutting-edge research and emerging paradigms. Develop the ability to read, implement, and critique research papers.

### 9.1 Multimodal LLMs
- **Vision-Language Models:** CLIP, LLaVA, GPT-4V architecture, visual tokenization, cross-modal attention
- **Audio & Speech:** Whisper, audio tokenization, speech-to-text integration
- **Unified Multimodal Architectures:** Any-to-any models, modality-agnostic transformers
- **Key Exercise:** Fine-tune a vision-language model on a custom dataset. Evaluate cross-modal retrieval.

### 9.2 Efficient Architectures & Long Context
- **Linear Attention:** Performer, Linformer, RWKV, state space models (Mamba, Mamba-2)
- **Ring Attention & Sequence Parallelism:** Distributed attention for million-token contexts
- **Memory-Augmented Models:** External memory, differentiable neural computers, retrieval-augmented architectures
- **Key Exercise:** Implement ring attention for a transformer. Benchmark memory usage vs. standard attention at 128K context length.

### 9.3 Model Merging & Composition
- **Model Soups:** Weight averaging, task vector arithmetic
- **SLERP & TIES:** Spherical interpolation, trimming, electing sign, merging
- **Mixture of Experts (MoE):** Sparse upcycling, expert routing, load balancing
- **Key Exercise:** Merge two fine-tuned models using TIES-Merging. Evaluate performance on both tasks.

### 9.4 Synthetic Data & Self-Improvement
- **Self-Instruct:** Synthetic instruction generation, bootstrapping, quality filtering
- **Constitutional AI:** Self-critique, revision, RL from AI feedback
- **Iterative Distillation:** Teacher-student training, capability transfer, compression
- **Key Exercise:** Generate a synthetic instruction dataset using self-instruct. Fine-tune a model and evaluate against human-curated data.

### 9.5 Interpretability & Mechanistic Understanding
- **Attention Visualization:** Attention rollout, attention flow, token attribution
- **Probing & Representation Analysis:** Linear probes, concept-based explanations, logit lens
- **Mechanistic Interpretability:** Circuit tracing, superposition, feature visualization
- **Key Exercise:** Use attention visualization to identify factual recall mechanisms in a trained model. Trace the "circuit" for a specific fact.

### 9.6 Future Directions
- **Test-Time Training:** Dynamic adaptation during inference, in-context learning theory
- **Neurosymbolic AI:** Combining neural networks with symbolic reasoning, program synthesis
- **World Models:** Internal simulation, planning, causal reasoning
- **Key Exercise:** Write a research proposal for a novel LLM architecture or training paradigm. Include theoretical justification and experimental design.

---

## Capstone Projects

> **Objective:** Demonstrate mastery by building production-grade systems from scratch. Each project should be portfolio-ready and include architecture diagrams, performance benchmarks, and operational documentation.

### Capstone 1: Distributed Pretraining System
**Scope:** Pretrain a 1B-parameter transformer from scratch on a multi-node GPU cluster.
**Requirements:**
- Implement data pipeline with quality filtering and deduplication
- Configure 3D parallelism (DP + TP + PP)
- Achieve >50% GPU utilization (measured via DCGM)
- Implement fault-tolerant checkpointing with automatic resume
- Document scaling efficiency (weak and strong scaling)

### Capstone 2: Production RAG Platform
**Scope:** Build a RAG system serving 10K+ documents with sub-second retrieval.
**Requirements:**
- Hybrid dense + sparse retrieval with reranking
- Real-time index updates and versioning
- Comprehensive evaluation pipeline (RAGAS metrics)
- A/B testing framework for chunking and retrieval strategies
- Cost tracking and optimization dashboard

### Capstone 3: RLHF Training Pipeline
**Scope:** Align a 7B parameter model using full RLHF (SFT → Reward Model → PPO).
**Requirements:**
- Train reward model with >85% ranking accuracy
- Implement PPO with KL divergence monitoring
- Compare PPO vs. DPO vs. GRPO on the same task
- Productionize with checkpointing and rollback capabilities
- Evaluate on MT-Bench or equivalent

### Capstone 4: High-Throughput Inference Service
**Scope:** Deploy a 70B parameter model serving 1000+ concurrent users.
**Requirements:**
- vLLM or TensorRT-LLM deployment with continuous batching
- Speculative decoding integration
- Multi-LoRA serving with <100ms cold-start
- Auto-scaling based on queue depth
- Comprehensive observability (TTFT, TPOT, error rates, cost per 1K tokens)

### Capstone 5: Multi-Agent Orchestration System
**Scope:** Build a multi-agent system for complex task automation.
**Requirements:**
- 3+ specialized agents with defined roles
- MCP integration for tool use
- State persistence and failure recovery
- Human-in-the-loop approval for critical actions
- Comprehensive audit logging and security guardrails

---

## Assessment & Certification Rubric

### Knowledge Assessment
- **Theory Exams:** Closed-book exams on transformer math, distributed training algorithms, and optimization theory
- **Code Reviews:** Review of implementation quality, efficiency, and correctness
- **Architecture Reviews:** Design reviews of capstone projects focusing on trade-off analysis

### Practical Assessment
- **Debugging Challenges:** Intentionally broken systems that candidates must diagnose and fix
- **Performance Optimization:** Given a slow system, achieve target latency/throughput with cost constraints
- **Incident Response:** Simulated production incidents requiring rapid diagnosis and mitigation

### Certification Levels
- **Level 1 — Practitioner:** Completes Phases 1–5, passes theory exams, completes Capstone 1
- **Level 2 — Specialist:** Completes Phases 1–7, passes practical assessments, completes Capstones 1–3
- **Level 3 — Expert:** Completes all phases, leads architecture reviews, completes all capstones with production deployment

---

## Recommended Reading & Reference Library

### Foundational Papers
1. **"Attention Is All You Need"** — Vaswani et al. (2017) [Transformer architecture]
2. **"Language Models are Few-Shot Learners"** — Brown et al. (2020) [GPT-3]
3. **"Training Language Models to Follow Instructions with Human Feedback"** — Ouyang et al. (2022) [InstructGPT/RLHF]
4. **"Llama 2: Open Foundation and Fine-Tuned Chat Models"** — Touvron et al. (2023)
5. **"Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM"** — Narayanan et al. (2021)
6. **"ZeRO: Memory Optimizations Toward Training Trillion Parameter Models"** — Rajbhandari et al. (2020)
7. **"PagedAttention: Efficient Memory Management for LLM Serving"** — Kwon et al. (2023) [vLLM]
8. **"Direct Preference Optimization: Your Language Model is Secretly a Reward Model"** — Rafailov et al. (2023)
9. **"Mamba: Linear-Time Sequence Modeling with Selective State Spaces"** — Gu & Dao (2023)
10. **"Chain-of-Thought Prompting Elicits Reasoning in Large Language Models"** — Wei et al. (2022)

### Books
- **"Hands-On Large Language Models"** — Alammar & Grootendorst (2024)
- **"LLMs from Scratch"** — Raschka (2024)
- **"Designing Machine Learning Systems"** — Huyen (2022)
- **"Building Machine Learning Pipelines"** — Hannes Hapke & Catherine Nelson (2020)

### Courses & Tutorials
- **CS224N: Natural Language Processing with Deep Learning** (Stanford)
- **CS25: Transformers United** (Stanford)
- **Full Stack LLM Bootcamp** (Full Stack Deep Learning)
- **LLM Engineering Course** — Maven/Chip Huyen

### Tools & Frameworks Reference
- **PyTorch Distributed:** https://pytorch.org/tutorials/beginner/dist_overview.html
- **DeepSpeed:** https://www.deepspeed.ai/
- **vLLM:** https://docs.vllm.ai/
- **HuggingFace TRL:** https://huggingface.co/docs/trl/
- **OpenRLHF:** https://github.com/OpenRLHF/OpenRLHF
- **verl:** https://github.com/volcengine/verl
- **RAGAS:** https://docs.ragas.io/
- **DeepEval:** https://docs.confident-ai.com/

### Community & Research
- **arXiv cs.CL:** Daily paper tracking
- **Papers with Code:** Implementation references
- **HuggingFace Blog:** Model releases and tutorials
- **Lilian Weng's Blog:** Technical deep-dives
- **The Gradient:** AI research and industry perspectives

---

## Appendix: Glossary of Terms

| Term | Definition |
|------|------------|
| **Attention** | Mechanism allowing models to focus on relevant input parts |
| **BF16** | Brain floating-point format (16-bit) |
| **Continual Batching** | Dynamic batching of requests at iteration level |
| **DPO** | Direct Preference Optimization |
| **FSDP** | Fully Sharded Data Parallel |
| **GRPO** | Group Relative Policy Optimization |
| **KV Cache** | Key-Value cache for autoregressive generation |
| **LoRA** | Low-Rank Adaptation |
| **MCP** | Model Context Protocol |
| **MoE** | Mixture of Experts |
| **NCCL** | NVIDIA Collective Communications Library |
| **PPO** | Proximal Policy Optimization |
| **RAG** | Retrieval-Augmented Generation |
| **RLHF** | Reinforcement Learning from Human Feedback |
| **RoPE** | Rotary Position Embedding |
| **SFT** | Supervised Fine-Tuning |
| **Speculative Decoding** | Using draft model to accelerate generation |
| **TP** | Tensor Parallelism |
| **vLLM** | High-throughput LLM serving engine |

---

## Final Notes

This syllabus represents a comprehensive, production-focused curriculum for LLM engineering. It is designed to be iterative — revisit earlier phases as you advance, as deeper understanding reveals new connections. The field evolves rapidly; maintain a habit of reading papers, tracking framework updates, and experimenting with new techniques.

**The ultimate goal is not just to use LLMs, but to understand them deeply enough to build, optimize, debug, and operate them at scale.**

---

*Document Version: 2026.05.17*  
*Maintained by: Senior Curriculum Designer — AI/ML Infrastructure Track*  
*Next Review Date: 2026.08.17*