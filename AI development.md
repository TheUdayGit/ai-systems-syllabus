  
  
     
   ## File: ai-development-and-fine-tuning-syllabus.md

# AI Development and Fine-Tuning

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Mathematical & Computational Foundations](#module-0-mathematical--computational-foundations)
5. [Module 1: The AI Development Lifecycle — From Pre-training to Production](#module-1-the-ai-development-lifecycle)
6. [Module 2: Data Curation & Preparation for AI Training](#module-2-data-curation--preparation-for-ai-training)
7. [Module 3: Pre-training Foundations — Language Modeling at Scale](#module-3-pre-training-foundations)
8. [Module 4: Supervised Fine-Tuning (SFT) — Instruction Following & Domain Adaptation](#module-4-supervised-fine-tuning-sft)
9. [Module 5: Parameter-Efficient Fine-Tuning (PEFT) — LoRA, QLoRA, Adapters](#module-5-parameter-efficient-fine-tuning-peft)
10. [Module 6: Preference Alignment — RLHF, DPO, ORPO, KTO](#module-6-preference-alignment)
11. [Module 7: Reinforcement Learning for Reasoning — GRPO, DAPO, RLVR](#module-7-reinforcement-learning-for-reasoning)
12. [Module 8: Continual Pre-training & Domain Adaptation](#module-8-continual-pre-training--domain-adaptation)
13. [Module 9: Model Compression & Inference Optimization](#module-9-model-compression--inference-optimization)
14. [Module 10: AI Agents — Tool Use, Function Calling & Multi-Agent Systems](#module-10-ai-agents)
15. [Module 11: Evaluation, Benchmarking & Red Teaming](#module-11-evaluation-benchmarking--red-teaming)
16. [Module 12: Production Deployment & Serving](#module-12-production-deployment--serving)
17. [Module 13: MLOps for AI — Pipelines, Experiment Tracking & Model Registry](#module-13-mlops-for-ai)
18. [Module 14: Responsible AI Development & Governance](#module-14-responsible-ai-development--governance)
19. [Capstone Project](#capstone-project)
20. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
21. [Appendix B: Tooling Matrix](#appendix-b-tooling-matrix)
22. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

AI Development and Fine-Tuning is not about running `trainer.train()` in a notebook. It is a **systems engineering discipline** at the intersection of:

- **Applied Mathematics**: optimization theory, probability, information theory, game theory
- **Computer Science**: distributed systems, algorithms, memory hierarchies, compiler optimization
- **Data Engineering**: large-scale data curation, deduplication, quality filtering, tokenization
- **Systems Engineering**: GPU clusters, InfiniBand, NCCL, checkpointing, fault tolerance
- **Cognitive Science**: instruction following, reasoning, tool use, multi-turn dialogue
- **Ethics & Governance**: alignment, safety, fairness, transparency, regulatory compliance

The modern AI development stack must handle:
- **Trillion-token pre-training runs** across thousands of GPUs with <0.1% downtime
- **Parameter-efficient fine-tuning** that adapts 70B models on single consumer GPUs
- **Multi-stage alignment pipelines** (SFT → DPO → RL) that transform base models into helpful, harmless assistants
- **Reasoning models** that use reinforcement learning with verifiable rewards to solve complex problems
- **AI agents** that autonomously use tools, browse the web, and collaborate with other agents
- **Production serving** at p99 < 100ms with quantization, speculative decoding, and continuous batching

This course progresses from **mathematical foundations** → **pre-training** → **fine-tuning & alignment** → **reasoning & agents** → **production systems**, with each module building a complete mental model connecting theory to implementation to infrastructure.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building and fine-tuning production LLMs
- ML Infrastructure Engineers designing training platforms for foundation models
- MLOps Engineers creating CI/CD pipelines for AI model development
- Research Engineers transitioning from academia to production AI
- Staff-level candidates preparing for AI development and system design interviews

### Prerequisites
- **Solid Python**: PyTorch/TensorFlow, data structures, OOP, type hints
- **Mathematics**: linear algebra, multivariate calculus, probability, optimization
- **Deep Learning**: neural networks, backpropagation, transformers, attention
- **Distributed Systems**: basics of parallel computing, MPI, NCCL
- **Software Engineering**: Git, Docker, CI/CD, testing, debugging

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Architect** full AI development pipelines from data curation through pre-training to deployment
2. **Implement** parameter-efficient fine-tuning (LoRA/QLoRA) that achieves 95%+ of full fine-tuning quality
3. **Design** multi-stage alignment pipelines (SFT → DPO → RLHF) with proper evaluation gates
4. **Train** reasoning models using GRPO and verifiable rewards for math, code, and logic tasks
5. **Build** AI agents with tool use, function calling, and multi-agent orchestration
6. **Optimize** models for inference through quantization, pruning, distillation, and compilation
7. **Evaluate** models comprehensively with benchmarks, human evaluation, and red teaming
8. **Deploy** models at scale with vLLM, TensorRT-LLM, and continuous batching
9. **Ensure** responsible AI through alignment, safety testing, and governance frameworks
10. **Debug** training failures using distributed tracing, gradient monitoring, and checkpoint analysis

---

## Module 0: Mathematical & Computational Foundations

### 0.1 Optimization Theory for AI Training
- **Convex vs non-convex optimization**: local minima, saddle points, plateaus
- **Stochastic Gradient Descent (SGD)**: convergence rates, mini-batch variance, learning rate schedules
- **Momentum methods**: Polyak momentum, Nesterov accelerated gradient
- **Adaptive optimizers**: AdaGrad, RMSprop, Adam, AdamW — derivation, bias correction, weight decay decoupling
- **Second-order methods**: L-BFGS, natural gradient, Fisher information matrix
- **Distributed optimization**: local SGD, federated averaging, gradient compression

### 0.2 Probability & Information Theory
- **Maximum Likelihood Estimation**: log-likelihood, score function, Fisher information
- **Maximum A Posteriori**: conjugate priors, Laplace approximation
- **Variational Inference**: ELBO, KL divergence, reparameterization trick
- **Information theory**: entropy, cross-entropy, KL divergence, mutual information
- **Rate-distortion theory**: compression limits, VAE objective derivation

### 0.3 Game Theory for RLHF
- **Normal-form games**: Nash equilibrium, dominated strategies, best responses
- **Extensive-form games**: sequential decisions, subgame perfect equilibrium
- **Stackelberg games**: leader-follower dynamics, commitment strategies
- **Mechanism design**: incentive compatibility, revelation principle
- **Application**: RLHF as a Stackelberg game where the model is the leader and human is the follower

### 0.4 Numerical Linear Algebra at Scale
- **Matrix factorizations**: LU, Cholesky, QR, SVD — stability and complexity
- **Eigenvalue problems**: power iteration, Lanczos, Arnoldi
- **Sparse matrices**: CSR, CSC formats, sparse solvers
- **Tensor contractions**: einsum, tensor network contractions
- **GPU memory hierarchies**: HBM, shared memory, registers, coalesced access

### 0.5 Reading
- *Optimization Methods for Large-Scale Machine Learning* — Bottou, Curtis, Nocedal
- *Information Theory and Reliable Communication* — Gallager
- *Game Theory* — Fudenberg & Tirole
- *Numerical Linear Algebra* — Trefethen & Bau

---

## Module 1: The AI Development Lifecycle — From Pre-training to Production

### 1.1 The Four-Stage AI Development Pipeline

```
┌─────────────────────────────────────────────────────────────────┐
│              AI Development Lifecycle (2026)                     │
│                                                                 │
│  Stage 1: Pre-training        Stage 2: Post-training            │
│  ┌──────────────┐             ┌──────────────┐                 │
│  │  Next-token   │             │  SFT: Teach   │                 │
│  │  prediction   │────────────▶│  instruction  │                 │
│  │  on web data  │             │  following    │                 │
│  └──────────────┘             └──────┬───────┘                 │
│       Base Model                      │                         │
│                                       ▼                         │
│  Stage 3: Preference Alignment  Stage 4: Reasoning/Agents       │
│  ┌──────────────┐             ┌──────────────┐                 │
│  │  DPO/RLHF    │             │  GRPO/RLVR   │                 │
│  │  Align with  │────────────▶│  Verifiable  │                 │
│  │  preferences │             │  rewards     │                 │
│  └──────────────┘             └──────────────┘                 │
│       Instruct Model                Reasoning Model             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 1.2 Pre-training vs Post-training vs Fine-tuning

| Phase | What Changes | Scale | Compute | Goal |
|-------|-------------|-------|---------|------|
| **Pre-training** | All weights, next-token prediction | 1T-10T tokens | 1000s GPUs, weeks | General knowledge, language understanding |
| **Continual Pre-training** | All weights, domain data | 1B-500B tokens | 100s GPUs, days | Domain vocabulary, specialized knowledge |
| **SFT (Post-training)** | All or adapter weights, instruction data | 1M-100M examples | 10s GPUs, hours | Instruction following, output format |
| **Preference Alignment** | All or adapter weights, preference pairs | 50K-500K pairs | 10s GPUs, hours | Helpfulness, harmlessness, honesty |
| **RL for Reasoning** | All weights, verifiable rewards | 10K-100K problems | 100s GPUs, days | Math, code, logic reasoning |
| **Fine-tuning (User)** | Adapter weights, task data | 500-50K examples | 1-4 GPUs, minutes | Task-specific adaptation |

### 1.3 The 2026 Production Default: Fine-tune the Interface, Retrieve the Content
- **What to fine-tune**: query rewriter, grounded-answer format, refusal behavior, reranker
- **What to retrieve**: dynamic knowledge, customer-specific data, frequently updated content
- **Pattern**: LoRA adapter for tone/format + RAG pipeline for knowledge
- **When to break**: highly specialized domains (legal, biomedical) where base vocabulary is inadequate

### 1.4 Compute Planning & Cost Estimation
- **GPU-hour estimation**: tokens/sec × total tokens × epochs / (3600 × GPUs)
- **Memory requirements**: model params × bytes/param × parallelism factor
- **Cost optimization**: spot instances, checkpointing, early stopping, mixed precision
- **ROI analysis**: when full fine-tuning justifies cost vs LoRA/QLoRA

---

## Module 2: Data Curation & Preparation for AI Training

### 2.1 Data Collection at Scale
- **Web crawling**: Common Crawl, refined-web, deduplication pipelines
- **Synthetic data**: self-instruct, evol-instruct, constitutional AI, agent-generated data
- **Proprietary data**: enterprise documents, logs, conversations, codebases
- **Multimodal data**: image-text pairs (LAION), video-text (InternVid), audio-text

### 2.2 Data Quality & Filtering
- **Quality heuristics**: perplexity filtering, language identification, length filtering
- **Deduplication**: exact dedup (MinHash), near-dedup (SimHash), fuzzy dedup
- **Toxicity filtering**: perspective API, custom classifiers, blocklist filtering
- **Privacy scrubbing**: PII detection, entity recognition, anonymization
- **Data mixing**: domain proportions, temperature sampling, curriculum learning

### 2.3 Tokenization
- **BPE (Byte-Pair Encoding)**: merge rules, vocabulary construction, subword units
- **WordPiece**: Google variant, likelihood-based merging
- **SentencePiece**: unigram language model, language-agnostic
- **BPE dropout**: regularization through stochastic tokenization
- **Special tokens**: `<|endoftext|>`, `<|user|>`, `<|assistant|>`, `<|tool|>`, `<|think|>`

### 2.4 Dataset Formats & Tools
- **JSONL**: line-delimited JSON for streaming
- **Parquet**: columnar format for analytics, predicate pushdown
- **Arrow**: in-memory format for zero-copy reads
- **HuggingFace Datasets**: `load_dataset`, `map`, `filter`, `interleave_datasets`
- **WebDataset**: tar-based streaming for large-scale training
- **MosaicML Streaming**: efficient streaming with shard-based prefetching

### 2.5 Lab: Build a Data Curation Pipeline
- Download and process Common Crawl subset
- Implement MinHash deduplication
- Filter by quality score and language
- Create balanced data mix with curriculum learning
- Tokenize with SentencePiece and analyze vocabulary coverage

---

## Module 3: Pre-training Foundations — Language Modeling at Scale

### 3.1 Causal Language Modeling
- **Objective**: maximize log-likelihood of next token given context
- **Loss function**: cross-entropy over vocabulary, label smoothing
- **Attention masking**: causal (lower triangular) mask for autoregressive generation
- **Position encoding**: absolute (sinusoidal), relative (RoPE, ALiBi), rotary embeddings

### 3.2 Transformer Architecture at Scale
- **Multi-head self-attention**: QKV projections, scaled dot-product, O(n²) complexity
- **Feed-forward networks**: SwiGLU, GELU, expansion ratios (4×, 8/3×)
- **Normalization**: Pre-LN vs Post-LN, RMSNorm, deepnorm for stability
- **Activation checkpointing**: trading compute for memory
- **FlashAttention**: IO-aware attention algorithm, tiling, recomputation

### 3.3 Distributed Pre-training
- **Data parallelism**: replicate model, shard data, all-reduce gradients
- **Tensor parallelism**: shard layers across GPUs (Megatron-LM)
- **Pipeline parallelism**: micro-batching, bubble reduction (GPipe, PipeDream)
- **3D parallelism**: combining DP, TP, PP (DeepSpeed, Megatron)
- **Sequence parallelism**: splitting along sequence dimension for long contexts
- **ZeRO**: optimizer state partitioning, gradient partitioning, parameter partitioning

### 3.4 Training Stability
- **Loss spikes**: gradient clipping, learning rate warmup, stableAdamW
- **Numerical precision**: BF16 vs FP16 vs FP8, mixed precision training
- **Checkpointing**: frequency, async checkpointing, distributed checkpointing
- **Fault tolerance**: spot instance handling, automatic restart, checkpoint resumption

### 3.5 Scaling Laws
- **Kaplan scaling**: loss ∝ C^(-α), N^(-β), D^(-γ) — power laws for compute, params, data
- **Chinchilla scaling**: compute-optimal training (20 tokens per parameter)
- **Over-training**: training beyond Chinchilla for inference efficiency
- **Emergence**: capabilities that appear suddenly at scale

### 3.6 Lab: Pre-train a Small LLM
- Implement GPT-2 architecture from scratch
- Train on OpenWebText with distributed data parallelism
- Implement gradient clipping, learning rate scheduling, checkpointing
- Evaluate perplexity and downstream task performance
- Analyze scaling behavior with different model sizes

---

## Module 4: Supervised Fine-Tuning (SFT) — Instruction Following & Domain Adaptation

### 4.1 SFT Fundamentals
- **Objective**: maximize likelihood of instruction-response pairs
- **Data formats**: Alpaca, ShareGPT, OpenAI format, ChatML, custom formats
- **Loss masking**: compute loss only on assistant tokens, not user tokens
- **Sequence packing**: multiple examples per sequence for efficiency

### 4.2 Dataset Quality & Curation
- **The Accuracy-Diversity-Complexity Triad**: three pillars of dataset quality
- **LIMA principle**: 1,000 carefully curated examples can match GPT-4 quality
- **Synthetic data generation**: self-instruct, evol-instruct, agent trajectories
- **Data mixing**: instruction data + general data ratio, domain proportions
- **Data validation**: format checking, length distribution, tokenization verification

### 4.3 Training Configuration
- **Learning rate**: 1e-5 to 2e-4 for LoRA, lower for full fine-tuning
- **Batch size**: 64-512 global batch size, gradient accumulation
- **Epochs**: 1-3 epochs (overfitting is common with multiple epochs)
- **Warmup**: linear warmup to peak LR, cosine decay
- **Regularization**: dropout, weight decay, label smoothing

### 4.4 Full Fine-Tuning vs PEFT
- **Full fine-tuning**: update all parameters, maximum quality, highest compute cost
- **LoRA**: low-rank adapters, 0.1-1% trainable params, near-full quality
- **QLoRA**: 4-bit base + LoRA adapters, single-GPU for 70B models
- **DoRA**: weight decomposition, magnitude + direction adaptation
- **Decision framework**: accuracy requirements, compute budget, iteration speed

### 4.5 Lab: SFT a Production Model
- Prepare high-quality instruction dataset (1K-10K examples)
- Fine-tune Llama 3 with LoRA (rank 16, alpha 32)
- Evaluate on held-out instruction following benchmark
- Compare full fine-tuning vs LoRA vs QLoRA
- Analyze catastrophic forgetting on general knowledge tasks

---

## Module 5: Parameter-Efficient Fine-Tuning (PEFT) — LoRA, QLoRA, Adapters

### 5.1 LoRA (Low-Rank Adaptation)
- **Mathematical formulation**: W = W₀ + BA, where B ∈ R^(d×r), A ∈ R^(r×k), r << min(d,k)
- **Initialization**: A with random Gaussian, B with zeros (zero at start)
- **Where to apply**: attention Q/V projections, MLP layers, all linear layers
- **Rank selection**: 8-64 typical, higher rank for complex tasks, diminishing returns
- **Alpha scaling**: α/r scaling factor for adapter contribution
- **Merging adapters**: W_merged = W₀ + BA, enabling inference without adapter overhead

### 5.2 QLoRA (Quantized LoRA)
- **4-bit quantization**: NormalFloat4, double quantization, page optimizer
- **Memory savings**: 70B model fits in 48GB GPU (vs 140GB+ for FP16)
- **Dequantization**: on-the-fly dequantization for forward/backward passes
- **Performance**: 80-90% of full fine-tuning quality, slight degradation vs LoRA
- **When to use**: limited VRAM, large models, rapid experimentation

### 5.3 Advanced PEFT Methods
- **DoRA**: decompose weight into magnitude (m) and direction (V), adapt separately
- **IA³**: learn scaling vectors for key, value, and feed-forward activations
- **Prefix tuning**: prepend trainable tokens to keys and values
- **Prompt tuning**: soft prompts as trainable embeddings
- **Adapter fusion**: combining multiple adapters for multi-task inference
- **Multi-adapter serving**: one base model, many task-specific adapters, dynamic routing

### 5.4 PEFT Training Best Practices
- **Learning rate**: 2e-4 to 5e-4 for LoRA (higher than full fine-tuning)
- **Target modules**: `q_proj`, `v_proj` minimum; `all_linear` for best results
- **Dropout**: 0.05-0.1 for regularization
- **Gradient checkpointing**: trade compute for memory
- **DeepSpeed integration**: ZeRO-3 for large models with PEFT

### 5.5 Lab: Master PEFT Techniques
- Implement LoRA from scratch with PyTorch
- Fine-tune 70B model with QLoRA on single A100
- Compare LoRA, DoRA, IA³ on same task
- Implement multi-adapter serving with vLLM
- Measure memory, throughput, and quality tradeoffs

---

## Module 6: Preference Alignment — RLHF, DPO, ORPO, KTO

### 6.1 The Alignment Problem
- **Helpful, Harmless, Honest (HHH)**: the three pillars of aligned AI
- **Reward hacking**: models optimizing proxy metrics instead of true objectives
- **Distribution shift**: training on static data, deploying to open-ended interactions
- **Alignment tax**: capability reduction from safety training

### 6.2 RLHF (Reinforcement Learning from Human Feedback)
- **Three-stage pipeline**: SFT → Reward Model → RL (PPO)
- **Reward modeling**: Bradley-Terry model, preference pairs, cross-entropy loss
- **PPO (Proximal Policy Optimization)**: clipped surrogate objective, value function, advantage estimation
- **KL divergence penalty**: preventing policy drift from reference model
- **Challenges**: reward hacking, mode collapse, training instability

### 6.3 DPO (Direct Preference Optimization)
- **Insight**: derive optimal policy in closed form, eliminate reward model
- **Objective**: maximize likelihood of preferred response, minimize likelihood of rejected
- **Mathematical derivation**: from Bradley-Terry to DPO loss
- **Advantages**: simpler, more stable, no reward model needed
- **Reference model**: frozen SFT model for KL regularization
- **β parameter**: controlling divergence from reference (typical: 0.1-0.5)

### 6.4 ORPO (Odds Ratio Preference Optimization)
- **Single-stage**: combine SFT and preference alignment in one training run
- **Odds ratio**: ratio of preferred to rejected response likelihoods
- **Advantage**: no reference model, simpler pipeline, competitive results

### 6.5 KTO (Kahneman-Tversky Optimization)
- **Binary feedback**: learns from "good" / "bad" labels instead of pairs
- **Prospect theory**: asymmetric loss for desirable vs undesirable outputs
- **Advantage**: easier data collection, no preference pairs needed

### 6.6 RLAIF & Constitutional AI
- **AI feedback**: using strong model to judge outputs instead of humans
- **Constitutional AI**: self-critique and revision based on principles
- **Scalability**: cheaper than human labeling, consistent criteria
- **Limitations**: bias amplification, capability ceiling of judge model

### 6.7 Lab: Build an Alignment Pipeline
- Collect preference pairs from human annotators or synthetic generation
- Train reward model with Bradley-Terry objective
- Implement PPO training with KL penalty
- Compare DPO vs PPO on same dataset
- Evaluate with MT-bench, AlpacaEval, safety benchmarks

---

## Module 7: Reinforcement Learning for Reasoning — GRPO, DAPO, RLVR

### 7.1 The Reasoning Revolution
- **Chain-of-thought (CoT)**: explicit reasoning steps improve performance
- **Test-time compute**: more inference compute for harder problems
- **Verifiable rewards**: math proofs, code execution, logic puzzles have objective correctness
- **DeepSeek-R1**: GRPO enables reasoning without human-labeled CoT data

### 7.2 GRPO (Group Relative Policy Optimization)
- **No critic model**: uses group baseline instead of learned value function
- **Group sampling**: sample N responses per prompt, score each
- **Relative advantage**: advantage = (individual reward - group mean) / group std
- **KL penalty**: prevents policy from diverging too far
- **Efficiency**: eliminates critic training, reduces memory by ~50%

### 7.3 DAPO (Decoupled Clip and Dynamic Sampling Policy Optimization)
- **Decoupled clipping**: separate clip ratios for policy and reference
- **Dynamic sampling**: filter out prompts where all responses are correct/incorrect
- **Token-level loss**: per-token policy gradient instead of sequence-level
- **Advantage**: better credit assignment, faster convergence

### 7.4 RLVR (Reinforcement Learning with Verifiable Rewards)
- **Reward functions**: code execution (unit tests), math (sympy verification), logic (SAT solver)
- **Sparse rewards**: binary correct/incorrect, reward shaping for intermediate steps
- **Process reward models**: reward each reasoning step, not just final answer
- **Outcome reward models**: reward only final correctness, simpler but less informative

### 7.5 Training Recipe for Reasoning Models
1. **SFT on CoT data**: seed model with reasoning examples (optional but helps)
2. **GRPO training**: sample multiple responses, reward correct ones
3. **Rejection sampling**: generate high-quality responses from trained model
4. **SFT on best responses**: distill reasoning patterns
5. **Iterate**: repeat GRPO → rejection sampling → SFT

### 7.6 Lab: Train a Reasoning Model
- Implement GRPO from scratch
- Train on GSM8K (math word problems) with verifiable rewards
- Compare GRPO vs PPO vs supervised CoT fine-tuning
- Evaluate reasoning depth with step-by-step analysis
- Test generalization to out-of-distribution problems

---

## Module 8: Continual Pre-training & Domain Adaptation

### 8.1 When to Use Continual Pre-training (CPT)
- **Diagnostic**: high perplexity on domain text → base model lacks vocabulary
- **vs SFT**: CPT changes what model knows; SFT changes how model responds
- **vs RAG**: CPT for static knowledge, RAG for dynamic knowledge
- **Typical domains**: legal, medical, scientific, financial, code

### 8.2 CPT Implementation
- **Data composition**: 80% domain + 20% general replay buffer
- **Learning rate**: 10-100× lower than original pretraining LR
- **Token budget**: 1B-500B tokens depending on domain size
- **Checkpointing**: frequent saves, regression testing every 1K steps

### 8.3 Catastrophic Forgetting Prevention
- **Replay buffer**: mix general-domain data into every batch (most effective)
- **Elastic Weight Consolidation (EWC)**: penalize changes to important weights
  - `L_EWC = λ × Σ(F_i × (θ_i - θ*_i)²)` — Fisher information matrix
  - Practical for 7B-13B models; memory-prohibitive for 70B+
- **Progressive networks**: freeze old layers, add new ones
- **Adapter-based CPT**: train adapters instead of full weights

### 8.4 Regression Testing
- **Benchmark suite**: MMLU, HellaSwag, ARC, GSM8K, HumanEval
- **Alert threshold**: >3 percentage point drop on any benchmark
- **Frequency**: every 5K training steps
- **Action**: checkpoint restart with adjusted hyperparameters

### 8.5 Lab: Domain-Adapt a Model with CPT
- Select domain corpus (legal contracts, medical papers, code repos)
- Implement replay buffer with general-domain data
- Run CPT with regression monitoring
- Compare domain perplexity before/after
- Evaluate on domain-specific benchmarks

---

## Module 9: Model Compression & Inference Optimization

### 9.1 Quantization
- **Post-Training Quantization (PTQ)**: fastest path, small calibration set
  - INT8, INT4, FP8, NVFP4 — precision formats
  - GPTQ: layer-wise quantization with Hessian information
  - AWQ: activation-aware weight quantization
  - GGUF: llama.cpp format for CPU inference
- **Quantization-Aware Training (QAT)**: train with fake quantization
- **Tradeoffs**: 4-bit can cause 10-15% drop on complex reasoning tasks

### 9.2 Pruning
- **Magnitude pruning**: remove smallest weights
- **Structured pruning**: remove entire heads, layers, or channels
- **Semi-structured sparsity**: 2:4 pattern (NVIDIA hardware support)
- **Movement pruning**: learn which weights to remove during training
- **P-KD-Q sequence**: Prune → Distill → Quantize for best compression

### 9.3 Knowledge Distillation
- **Teacher-student**: large model teaches smaller model
- **Soft targets**: probability distributions contain richer information than hard labels
- **Hint learning**: intermediate layer distillation
- **Self-distillation**: model teaches itself (DINO, BYOL)
- **DistilBERT**: 40% smaller, 60% faster, 97% accuracy retention

### 9.4 Inference Optimization
- **KV caching**: store key-value pairs for autoregressive generation
- **PagedAttention**: vLLM's memory management, eliminate memory waste
- **Continuous batching**: batch new requests with ongoing ones
- **Speculative decoding**: draft model + target model, acceptance sampling
- **FlashAttention**: IO-aware attention, 2-4× speedup
- **FlashDecoding**: split long sequences for parallel decoding

### 9.5 Compilation & Kernel Fusion
- **ONNX Runtime**: cross-platform inference engine
- **TensorRT-LLM**: NVIDIA-optimized kernels, FP8, inflight batching
- **TVM**: auto-scheduling, hardware-specific optimization
- **XLA**: JIT compilation for JAX/TensorFlow
- **Kernel fusion**: combine operations to reduce memory bandwidth

### 9.6 Lab: Optimize a Model for Production Inference
- Quantize Llama 3 to 4-bit with GPTQ and AWQ
- Compare accuracy on reasoning benchmarks
- Deploy with vLLM and measure throughput (tokens/sec)
- Implement speculative decoding with smaller draft model
- Benchmark latency: p50, p95, p99

---

## Module 10: AI Agents — Tool Use, Function Calling & Multi-Agent Systems

### 10.1 Tool Use & Function Calling
- **Native function calling**: OpenAI, Anthropic, Google models support structured tool use
- **JSON schema**: defining tool signatures, parameters, descriptions
- **Execution loop**: model generates tool call → system executes → model processes result
- **Parallel tool calls**: multiple independent tools in single turn
- **Error handling**: tool failures, timeouts, malformed responses

### 10.2 Agent Architecture Patterns
- **ReAct**: Reasoning + Acting loop, interleaving thought and action
- **Plan-and-execute**: generate plan first, then execute steps
- **Reflection**: self-critique and revision loops
- **Tree of Thoughts**: explore multiple reasoning paths, backtrack
- **Reflexion**: verbal reinforcement learning through self-feedback

### 10.3 Multi-Agent Systems
- **Role-based agents**: specialized agents with distinct roles (planner, executor, critic)
- **Communication protocols**: MCP (Model Context Protocol), A2A (Agent-to-Agent)
- **Orchestration**: LangGraph, CrewAI, AutoGen for multi-agent workflows
- **Consensus mechanisms**: voting, debate, hierarchical decision making
- **Emergent behavior**: swarm intelligence, collective problem solving

### 10.4 Agent Frameworks (2026)
- **LangGraph**: stateful, controllable orchestration, graph-based workflows
- **CrewAI**: human-readable multi-agent crews with roles and tasks
- **AutoGen**: event-driven multi-agent with robust recipes
- **OpenAI Agents SDK**: native OpenAI integration, first-party tools
- **Anthropic Agent SDK**: accuracy-first, extended thinking, MCP ecosystem
- **PydanticAI**: type-safe tool contracts, structured I/O

### 10.5 Production Agent Challenges
- **Reliability**: ensuring consistent tool calls, handling edge cases
- **Latency**: multi-turn interactions, tool execution overhead
- **Cost**: token usage scales with conversation length
- **Safety**: preventing harmful tool use, sandboxing execution
- **Observability**: tracing agent decisions, debugging failures

### 10.6 Lab: Build a Production AI Agent
- Implement ReAct agent with 5+ tools (search, calculator, API calls)
- Add reflection loop for self-correction
- Build multi-agent system with planner + executor + critic
- Integrate with LangGraph for stateful orchestration
- Add observability with decision tracing and logging

---

## Module 11: Evaluation, Benchmarking & Red Teaming

### 11.1 Automatic Benchmarks
- **Knowledge**: MMLU, MMLU-Pro, ARC, HellaSwag, TruthfulQA
- **Reasoning**: GSM8K, MATH, HumanEval, MBPP, SWE-Bench
- **Instruction following**: IFEval, MT-Bench, AlpacaEval
- **Safety**: BBQ, BOLD, RealToxicityPrompts, XSTest
- **Long context**: Needle in a Haystack, RULER, InfiniteBench

### 11.2 Human Evaluation
- **Pairwise comparison**: judge prefers response A or B
- **ELO ratings**: Bradley-Terry model for ranking
- **Likert scales**: 1-5 ratings on specific dimensions
- **Inter-annotator agreement**: Cohen's kappa, Krippendorff's alpha
- **Crowdsourcing**: Amazon Mechanical Turk, Scale AI, custom platforms

### 11.3 Model-Based Evaluation
- **LLM-as-a-judge**: GPT-4, Claude judge other models' outputs
- **Self-evaluation**: model critiques its own responses
- **Constitutional evaluation**: evaluate against principles
- **Bias**: judge model may favor its own style, length, or position

### 11.4 Red Teaming
- **Adversarial prompting**: jailbreaks, prompt injection, roleplay attacks
- **Capability elicitation**: extracting harmful knowledge, bypassing refusals
- **Automated red teaming**: generate adversarial prompts at scale
- **Harm categories**: violence, hate speech, self-harm, misinformation, malware
- **Mitigation**: robust training, input filtering, output filtering, monitoring

### 11.5 A/B Testing & Online Evaluation
- **Shadow mode**: new model runs in parallel, no user impact
- **Canary deployment**: 1% traffic, gradually increase
- **Counterfactual evaluation**: inverse propensity weighting
- **Business metrics**: engagement, satisfaction, task completion

### 11.6 Lab: Build an Evaluation Suite
- Run automatic benchmarks on fine-tuned model
- Conduct human evaluation with pairwise comparisons
- Implement LLM-as-a-judge pipeline
- Perform red teaming with 100+ adversarial prompts
- Analyze failure modes and iterate on training

---

## Module 12: Production Deployment & Serving

### 12.1 Serving Architectures

| Pattern | Latency | Throughput | Use Case |
|---------|---------|-----------|----------|
| **Synchronous API** | <100ms p99 | Medium | Chat, search, real-time |
| **Asynchronous Batch** | Minutes | Very High | Offline inference, reports |
| **Streaming** | <50ms TTFB | High | Long-form generation, CoT |
| **Edge** | <10ms | Low | Mobile, IoT, on-device |

### 12.2 Model Serving Engines
- **vLLM**: PagedAttention, continuous batching, high throughput
  - LoRA support for multi-adapter serving
  - Tensor parallelism, pipeline parallelism
  - OpenAI-compatible API
- **TensorRT-LLM**: NVIDIA-optimized, FP8, inflight batching
- **TGI (Text Generation Inference)**: HuggingFace production server
- **llama.cpp**: CPU inference, GGUF format, quantization
- **Ollama**: local model management, simple API

### 12.3 Scaling Strategies
- **Horizontal scaling**: multiple replicas behind load balancer
- **Auto-scaling**: CPU/GPU utilization, queue depth, request rate
- **Model parallelism**: split large models across multiple GPUs
- **Request routing**: route by model size, task type, priority
- **Caching**: semantic caching, prompt caching, response caching

### 12.4 Multi-Adapter Serving
- **Architecture**: one base model in memory, many LoRA adapters
- **Routing**: request → select adapter → load adapter → generate
- **Tools**: vLLM LoRA support, LoRAX, SGLang
- **Use case**: multi-tenant SaaS with per-customer specialization
- **Cost**: 1 base model + N small adapters vs N full models

### 12.5 Lab: Deploy a Production Model
- Set up vLLM with TensorRT-LLM backend
- Configure continuous batching and paged attention
- Implement multi-adapter serving with 5+ task adapters
- Add load balancing and auto-scaling
- Benchmark throughput and latency under load

---

## Module 13: MLOps for AI — Pipelines, Experiment Tracking & Model Registry

### 13.1 Experiment Tracking
- **MLflow**: metrics, parameters, artifacts, model registry
- **Weights & Biases**: visualization, collaboration, hyperparameter sweeps
- **TensorBoard**: metrics, model graphs, profiling
- **Best practices**: systematic naming, version control integration, artifact logging

### 13.2 Training Pipelines
- **Kubeflow Pipelines**: Kubernetes-native ML workflows
- **Airflow**: general orchestration, ML-specific operators
- **Metaflow**: Netflix's framework for ML workflows
- **Components**: data validation, training, evaluation, model validation, deployment

### 13.3 Model Registry & Versioning
- **Staging**: development, staging, production, archived
- **Metadata**: training config, dataset version, metrics, dependencies
- **Lineage**: tracking from data to model to deployment
- **Approval workflows**: manual review, automated gates

### 13.4 CI/CD for AI Models
- **GitOps**: Git as single source of truth
- **Automated testing**: unit tests, integration tests, model performance tests
- **Canary deployment**: gradual traffic shifting
- **Rollback**: instant revert to previous version
- **Feature flags**: toggle model versions, A/B test configuration

### 13.5 Lab: Build an MLOps Pipeline
- Create Kubeflow pipeline for SFT → DPO → evaluation
- Track experiments with W&B, log all hyperparameters
- Register models with staging/production promotion
- Implement automated testing and canary deployment
- Set up monitoring and alerting

---

## Module 14: Responsible AI Development & Governance

### 14.1 Alignment & Safety
- **RLHF limitations**: reward hacking, mode collapse, over-optimization
- **Constitutional AI**: self-improvement through principles
- **Debate**: AI systems debate solutions, human judges
- **Interpretability**: mechanistic interpretability, probing, attribution
- **Emergent risks**: deceptive alignment, gradient hacking, power-seeking

### 14.2 Fairness & Bias
- **Bias sources**: training data, annotation, model architecture
- **Fairness metrics**: demographic parity, equalized odds, calibration
- **Mitigation**: pre-processing, in-processing, post-processing
- **Evaluation**: intersectional fairness, subgroup analysis

### 14.3 Transparency & Explainability
- **Model cards**: documenting capabilities, limitations, intended use
- **Datasheets**: documenting dataset creation, biases, limitations
- **Explainability**: SHAP, LIME, attention visualization
- **Regulatory**: EU AI Act, GDPR right to explanation

### 14.4 Governance Frameworks
- **NIST AI RMF**: risk management framework
- **EU AI Act**: risk-based regulation, prohibited practices
- **IEEE standards**: ethical design, transparency
- **Internal governance**: review boards, red teams, audit trails

### 14.5 Lab: Implement Responsible AI Practices
- Conduct bias audit on fine-tuned model
- Generate model card with comprehensive documentation
- Implement explainability pipeline for predictions
- Design governance workflow for model approval
- Create red team protocol for safety testing

---

## Capstone Project

### Project: Build a Domain-Specific AI Assistant with Reasoning Capabilities

Build a production-grade AI system for a specialized domain (e.g., legal, medical, scientific):

**Requirements:**
1. **Data curation**: Collect and process 10M+ tokens of domain-specific data
2. **Continual pre-training**: Domain-adapt base model with CPT, prevent catastrophic forgetting
3. **SFT**: Fine-tune with 5K high-quality instruction-response pairs
4. **Alignment**: DPO training with human/AI preference pairs
5. **Reasoning**: GRPO training on verifiable domain problems
6. **Agent capabilities**: Tool use for external APIs, databases, calculators
7. **Optimization**: Quantize to 4-bit, deploy with vLLM
8. **Evaluation**: Automatic benchmarks, human evaluation, red teaming
9. **MLOps**: Full pipeline with experiment tracking, model registry, CI/CD
10. **Governance**: Model card, bias audit, safety testing

**Architecture:**
- Base model: Llama 3.1 70B or equivalent
- Training: Multi-node GPU cluster with DeepSpeed/Megatron
- PEFT: LoRA/QLoRA for efficient fine-tuning
- Alignment: DPO with reference model
- Reasoning: GRPO with verifiable rewards
- Serving: vLLM with multi-adapter support
- Monitoring: W&B, Prometheus, custom dashboards

---

## Appendix A: Reading List & References

### Foundations
- *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong
- *Deep Learning* — Goodfellow, Bengio, Courville
- *Natural Language Processing with Transformers* — Tunstall, von Werra, Wolf

### Pre-training & Scaling
- *Scaling Laws for Neural Language Models* — Kaplan et al. (OpenAI)
- *Training Compute-Optimal Large Language Models* — Hoffmann et al. (DeepMind)
- *Llama 2: Open Foundation and Fine-Tuned Chat Models* — Touvron et al. (Meta)

### Fine-Tuning & Alignment
- *LoRA: Low-Rank Adaptation of Large Language Models* — Hu et al. (Microsoft)
- *QLoRA: Efficient Finetuning of Quantized LLMs* — Dettmers et al.
- *Direct Preference Optimization* — Rafailov et al.
- *Constitutional AI: Harmlessness from AI Feedback* — Bai et al. (Anthropic)

### Reasoning
- *DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning* — DeepSeek
- *Training Verifiers to Solve Math Word Problems* — Cobbe et al. (OpenAI)
- *Let's Verify Step by Step* — Lightman et al. (OpenAI)

### Systems & Production
- *Efficient Large-Scale Language Model Training on GPU Clusters* — Narayanan et al. (NVIDIA)
- *vLLM: Easy, Fast, and Cheap LLM Serving with PagedAttention* — Kwon et al.
- *Designing Machine Learning Systems* — Chip Huyen

---

## Appendix B: Tooling Matrix

### Training Frameworks
| Tool | Best For | Scale |
|------|----------|-------|
| **HuggingFace TRL** | SFT, DPO, PPO | Single to multi-GPU |
| **Unsloth** | Fast QLoRA training | Single GPU |
| **Axolotl** | Config-driven pipelines | Multi-GPU |
| **Torchtune** | PyTorch-native training | Multi-node |
| **DeepSpeed** | Large model training | 100s GPUs |
| **Megatron-LM** | NVIDIA-optimized pretraining | 1000s GPUs |
| **JAX/Flax** | Research flexibility | TPU/GPU |

### Alignment & RL
| Tool | Methods | Best For |
|------|---------|----------|
| **TRL** | SFT, DPO, PPO, ORPO | HuggingFace ecosystem |
| **OpenRLHF** | RLHF at scale | Large-scale alignment |
| **verl** | GRPO, PPO | Verifiable rewards |
| **LLaMA-Factory** | Comprehensive PEFT | Easy fine-tuning |

### Serving & Inference
| Tool | Best For | Throughput |
|------|----------|------------|
| **vLLM** | High-throughput serving | Very High |
| **TensorRT-LLM** | NVIDIA GPU optimization | Very High |
| **TGI** | HuggingFace integration | High |
| **llama.cpp** | CPU/edge inference | Low |
| **Ollama** | Local development | Low |

### Agent Frameworks
| Tool | Best For | Complexity |
|------|----------|------------|
| **LangGraph** | Stateful orchestration | Medium |
| **CrewAI** | Multi-agent crews | Low |
| **AutoGen** | Event-driven agents | Medium |
| **OpenAI Agents SDK** | OpenAI ecosystem | Low |
| **PydanticAI** | Type-safe agents | Low |

---

## Appendix C: Interview Preparation

### System Design: AI Development
- Design a system for continual pre-training of a 70B model
- Design a multi-tenant LoRA serving architecture
- Design an RLHF pipeline with human feedback collection
- Design a reasoning model training system with verifiable rewards
- Design an AI agent platform with tool use and multi-agent collaboration

### Deep Dives
- Derive DPO objective from Bradley-Terry model
- Explain GRPO and why it eliminates the critic model
- Compare LoRA, QLoRA, DoRA — when to use each
- How do you prevent catastrophic forgetting during continual pre-training?
- Design a red teaming protocol for a production LLM

### Production Challenges
- How do you debug a training run with loss spikes?
- Design a cost-effective serving architecture for 1000+ LoRA adapters
- How do you evaluate alignment without human evaluators?
- Implement speculative decoding and analyze speedup
- Design a safety filter that doesn't harm helpfulness

### Coding Challenges
- Implement LoRA forward pass from scratch
- Write a GRPO training loop with verifiable rewards
- Build a ReAct agent with tool use
- Implement KV cache for autoregressive generation
- Write a data curation pipeline with deduplication

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 1 week | 0 | Mathematics, optimization, game theory |
| **Pre-training** | 2 weeks | 1-3 | Data curation, pre-training, scaling laws |
| **Fine-Tuning** | 2 weeks | 4-5 | SFT, LoRA, QLoRA, PEFT |
| **Alignment** | 2 weeks | 6-7 | DPO, RLHF, GRPO, reasoning |
| **Domain Adaptation** | 1 week | 8 | CPT, catastrophic forgetting |
| **Optimization** | 1 week | 9 | Quantization, pruning, distillation |
| **Agents** | 1 week | 10 | Tool use, multi-agent, frameworks |
| **Production** | 2 weeks | 11-13 | Evaluation, serving, MLOps |
| **Governance** | 1 week | 14 | Safety, fairness, compliance |
| **Capstone** | 2 weeks | — | End-to-end AI system |

**Total Duration: 15 weeks (3.5 months) full-time, or 7 months part-time**

---

*This syllabus treats AI development and fine-tuning as a systems engineering discipline. The models, frameworks, and techniques evolve rapidly — new alignment methods, agent architectures, and optimization techniques emerge monthly. Master the fundamentals of optimization theory, distributed systems, and data engineering, and you can adapt to any breakthrough in the field.*

---

Download this file: [ai-development-and-fine-tuning-syllabus.md](sandbox:///mnt/agents/output/ai-development-and-fine-tuning-syllabus.md)