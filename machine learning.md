  
  
  ## File: machine-learning-syllabus.md

# Machine Learning

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Mathematical Foundations](#module-0-mathematical-foundations)
5. [Module 1: The Machine Learning Lifecycle & Production Mindset](#module-1-the-machine-learning-lifecycle--production-mindset)
6. [Module 2: Data Engineering for ML — Ingestion, Validation & Feature Stores](#module-2-data-engineering-for-ml)
7. [Module 3: Supervised Learning — Theory, Algorithms & Implementation](#module-3-supervised-learning)
8. [Module 4: Unsupervised Learning & Representation Learning](#module-4-unsupervised-learning--representation-learning)
9. [Module 5: Deep Learning — Neural Networks, Backpropagation & Optimization](#module-5-deep-learning)
10. [Module 6: Computer Vision & Multimodal Learning](#module-6-computer-vision--multimodal-learning)
11. [Module 7: Natural Language Processing & Large Language Models](#module-7-natural-language-processing--large-language-models)
12. [Module 8: Recommender Systems & Ranking](#module-8-recommender-systems--ranking)
13. [Module 9: Distributed Training & Scaling](#module-9-distributed-training--scaling)
14. [Module 10: Model Serving, Inference Optimization & Edge Deployment](#module-10-model-serving--inference-optimization--edge-deployment)
15. [Module 11: MLOps — Pipelines, Experiment Tracking & Model Registry](#module-11-mlops)
16. [Module 12: Monitoring, Observability & Drift Detection](#module-12-monitoring--observability--drift-detection)
17. [Module 13: Responsible AI, Fairness & Ethics](#module-13-responsible-ai--fairness--ethics)
18. [Module 14: Advanced Topics — Reinforcement Learning, Causal Inference, AutoML](#module-14-advanced-topics)
19. [Capstone Project](#capstone-project)
20. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
21. [Appendix B: Tooling Matrix](#appendix-b-tooling-matrix)
22. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

Machine Learning is not about training models in Jupyter notebooks. It is a **systems engineering discipline** at the intersection of:

- **Applied Mathematics**: linear algebra, multivariate calculus, probability theory, optimization, information theory
- **Computer Science**: algorithms, data structures, distributed systems, software engineering
- **Statistics**: hypothesis testing, experimental design, Bayesian inference, causal inference
- **Systems Engineering**: data pipelines, distributed training, model serving, monitoring, fault tolerance
- **Domain Expertise**: understanding the problem space, feature engineering, business metrics

The modern ML production stack must handle:
- **Billion-parameter models** trained across thousands of GPUs with fault tolerance
- **Real-time inference** at p99 < 100ms latency with 99.99% availability
- **Continuous retraining** pipelines that detect drift and auto-deploy validated models
- **Multi-modal data** — text, images, audio, video, tabular, time-series — in unified pipelines
- **Regulatory compliance** — explainability, fairness, audit trails, data governance

This course progresses from **mathematical foundations** → **classical ML** → **deep learning** → **production systems** → **MLOps & responsible AI**, with each module building a complete mental model connecting theory to implementation to infrastructure.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building and deploying ML models at scale
- ML Infrastructure Engineers designing training and serving platforms
- MLOps Engineers creating CI/CD pipelines for ML
- Data Engineers transitioning to ML systems
- Distributed Systems Engineers extending into ML infrastructure
- Staff-level candidates preparing for ML system design interviews

### Prerequisites
- **Solid Python**: NumPy, Pandas, object-oriented design, type hints
- **Mathematics**: linear algebra, multivariate calculus, probability & statistics
- **Computer Science**: algorithms, data structures, complexity analysis
- **Software Engineering**: version control, testing, CI/CD, containerization
- **Distributed Systems**: basics of parallel computing, message passing

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Derive** core ML algorithms from first principles (gradient descent, backpropagation, EM algorithm)
2. **Implement** production-grade training pipelines with distributed data/model parallelism
3. **Architect** real-time inference systems with feature stores, caching, and load balancing
4. **Design** monitoring systems that detect data drift, concept drift, and model degradation
5. **Optimize** models for inference through quantization, pruning, distillation, and compilation
6. **Build** MLOps pipelines with experiment tracking, model registry, and automated deployment
7. **Evaluate** models beyond accuracy — precision, recall, calibration, fairness, robustness
8. **Deploy** LLMs and multi-modal models with efficient serving strategies
9. **Ensure** responsible AI through bias detection, explainability, and governance frameworks
10. **Debug** production ML systems using distributed tracing, model introspection, and causal analysis

---

## Module 0: Mathematical Foundations

### 0.1 Linear Algebra for ML
- **Vector spaces**: basis, dimension, linear independence, span
- **Matrix operations**: multiplication, inversion, eigendecomposition, SVD
- **Positive definite matrices**: covariance matrices, kernel matrices
- **Tensor operations**: rank, contraction, Einstein summation notation
- **Application**: feature representations, weight matrices, attention mechanisms

### 0.2 Multivariate Calculus & Optimization
- **Gradients, Jacobians, Hessians**: partial derivatives, chain rule, Taylor expansion
- **Convex optimization**: convex sets, convex functions, Lagrange duality, KKT conditions
- **Gradient descent**: batch, stochastic, mini-batch, momentum, Nesterov acceleration
- **Adaptive optimizers**: AdaGrad, RMSprop, Adam, AdamW — derivation and convergence analysis
- **Second-order methods**: L-BFGS, Newton's method, natural gradient
- **Constrained optimization**: projected gradient, penalty methods, barrier methods

### 0.3 Probability & Statistics
- **Probability spaces**: random variables, distributions, expectation, variance
- **Common distributions**: Gaussian, Bernoulli, Binomial, Poisson, Beta, Dirichlet
- **Maximum Likelihood Estimation (MLE)**: likelihood function, log-likelihood, Fisher information
- **Maximum A Posteriori (MAP)**: Bayesian perspective, conjugate priors
- **Bayesian inference**: posterior computation, MCMC, variational inference
- **Information theory**: entropy, cross-entropy, KL divergence, mutual information
- **Hypothesis testing**: p-values, confidence intervals, Type I/II errors, power analysis

### 0.4 Numerical Methods
- **Floating-point arithmetic**: IEEE 754, catastrophic cancellation, numerical stability
- **Matrix factorization**: LU, Cholesky, QR — stability and complexity
- **Eigenvalue computation**: power iteration, QR algorithm, Lanczos method
- **Randomized algorithms**: randomized SVD, sketching, Johnson-Lindenstrauss lemma

### 0.5 Reading
- *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong
- *Convex Optimization* — Boyd & Vandenberghe
- *Pattern Recognition and Machine Learning* — Bishop, Ch. 1-4

---

## Module 1: The Machine Learning Lifecycle & Production Mindset

### 1.1 The ML Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│                    ML System Lifecycle                          │
│                                                                 │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐  │
│  │  Problem │──▶│   Data   │──▶│  Feature │──▶│  Model   │  │
│  │ Definition│   │ Collection│   │ Engineering│   │ Training │  │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘  │
│       ▲                                              │         │
│       │                                              ▼         │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐  │
│  │  Monitor │◀──│  Evaluate │◀──│  Deploy  │◀──│ Validate │  │
│  │ & Retrain│   │  & Test   │   │  & Serve │   │  & Test  │  │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 1.2 ML vs Traditional Software

| Aspect | Traditional Software | ML System |
|--------|---------------------|-----------|
| Core logic | Handwritten rules / Business logic | Learned probabilistic models |
| Data | Structured, transactional | High volume, variable, evolving distributions |
| Failure modes | Predictable (bugs, crashes) | Silent failures (drift, bias, overfitting) |
| Testing | Unit / Integration tests | A/B testing, offline evaluation, shadow mode |
| Maintenance | Code updates | Continuous retraining, monitoring, data freshness |
| Requirements | Functional specs | Statistical performance, latency, fairness |

### 1.3 Problem Formulation
- **Supervised learning**: regression, classification, ranking, sequence prediction
- **Unsupervised learning**: clustering, dimensionality reduction, density estimation
- **Reinforcement learning**: Markov decision processes, policy optimization
- **Self-supervised learning**: contrastive learning, masked prediction
- **Business metric translation**: from "increase revenue" to "optimize click-through rate"

### 1.4 Data Strategy
- **Data collection**: active learning, weak supervision, synthetic data
- **Data labeling**: crowdsourcing, expert annotation, programmatic labeling
- **Data versioning**: DVC, LakeFS, Delta Lake for reproducibility
- **Data lineage**: tracking transformations from raw to model input

### 1.5 Evaluation Framework
- **Offline metrics**: accuracy, precision, recall, F1, AUC-ROC, AUC-PR, RMSE, MAE
- **Online metrics**: CTR, conversion rate, revenue, user engagement
- **Statistical rigor**: confidence intervals, power analysis, sample size calculation
- **Counterfactual evaluation**: inverse propensity weighting, doubly robust estimators

---

## Module 2: Data Engineering for ML — Ingestion, Validation & Feature Stores

### 2.1 Data Ingestion Patterns
- **Batch ingestion**: scheduled ETL, incremental loads, full refreshes
- **Streaming ingestion**: Kafka, Kinesis, Pulsar, Pub/Sub
- **Change Data Capture (CDC)**: Debezium, Maxwell, database binlog parsing
- **API ingestion**: REST, GraphQL, gRPC with rate limiting and backoff
- **Data lakes**: S3, GCS, ADLS — raw, bronze, silver, gold medallion architecture

### 2.2 Data Validation & Quality
- **Great Expectations**: declarative data validation, automated profiling
- **Deequ**: Spark-based data quality (Amazon)
- **Pandera**: Pandas DataFrame validation with schemas
- **Data quality dimensions**: completeness, uniqueness, validity, consistency, timeliness, accuracy
- **Anomaly detection in data**: statistical tests, isolation forest for data drift

### 2.3 Feature Engineering
- **Numerical features**: scaling (standard, min-max, robust), binning, transforms (log, sqrt)
- **Categorical features**: one-hot encoding, target encoding, embeddings, hash encoding
- **Temporal features**: cyclical encoding, time since event, rolling windows
- **Text features**: TF-IDF, word embeddings, sentence embeddings
- **Feature crosses**: manual crosses, factorization machines, deep crosses

### 2.4 Feature Stores
- **Offline store**: batch-computed features, training data generation, point-in-time correctness
- **Online store**: low-latency feature serving, Redis, DynamoDB, Cassandra
- **Feature registry**: metadata, lineage, versioning, documentation
- **Training-serving skew**: ensuring consistency between training and inference features
- **Feature monitoring**: drift detection, freshness, null rate tracking

### 2.5 Lab: Build a Feature Store Pipeline
- Ingest streaming events into Kafka
- Compute batch features with Spark
- Serve online features via Redis
- Implement point-in-time joins for training data
- Monitor feature drift with Great Expectations

---

## Module 3: Supervised Learning — Theory, Algorithms & Implementation

### 3.1 Linear Models
- **Linear regression**: normal equation, gradient descent, geometric interpretation
- **Ridge & Lasso**: L2/L1 regularization, elastic net, coordinate descent
- **Logistic regression**: sigmoid, cross-entropy loss, Newton-Raphson, IRLS
- **Generalized Linear Models (GLM)**: exponential family, link functions
- **Probabilistic interpretation**: MLE, MAP, Bayesian linear regression

### 3.2 Tree-Based Models
- **Decision trees**: CART, ID3, C4.5 — entropy, Gini impurity, information gain
- **Random Forests**: bagging, feature subsampling, out-of-bag error
- **Gradient Boosting**: additive models, gradient descent in function space
- **XGBoost/LightGBM/CatBoost**: histogram-based splits, leaf-wise growth, categorical handling
- **Monotonic constraints**: enforcing business logic in tree models

### 3.3 Support Vector Machines
- **Hard-margin SVM**: maximum margin hyperplane, quadratic programming
- **Soft-margin SVM**: hinge loss, slack variables, C parameter
- **Kernel trick**: polynomial, RBF, sigmoid kernels — Mercer's condition
- **SMO algorithm**: sequential minimal optimization, Lagrange multipliers
- **SVM for regression**: epsilon-insensitive loss

### 3.4 Probabilistic Graphical Models
- **Naive Bayes**: conditional independence, Laplace smoothing
- **Bayesian Networks**: DAG structure, conditional probability tables, d-separation
- **Hidden Markov Models**: forward-backward, Viterbi, Baum-Welch (EM)
- **Conditional Random Fields**: undirected graphs, feature functions, inference

### 3.5 Ensemble Methods
- **Bagging**: bootstrap aggregating, variance reduction
- **Boosting**: AdaBoost, gradient boosting — bias reduction
- **Stacking**: meta-learner, heterogeneous base models
- **Voting**: hard voting, soft voting, weighted voting

### 3.6 Model Evaluation & Selection
- **Cross-validation**: k-fold, stratified, time-series split, group k-fold
- **Bias-variance decomposition**: underfitting vs overfitting, learning curves
- **Hyperparameter tuning**: grid search, random search, Bayesian optimization (Optuna, Hyperopt)
- **Model calibration**: Platt scaling, isotonic regression, expected calibration error
- **Threshold selection**: ROC analysis, precision-recall curves, cost-sensitive thresholds

### 3.7 Lab: Build a Production-Grade Classifier
- Implement logistic regression from scratch with NumPy
- Train XGBoost and LightGBM models on a real dataset
- Perform Bayesian hyperparameter optimization
- Calibrate probabilities and optimize decision threshold
- Deploy with ONNX for cross-platform inference

---

## Module 4: Unsupervised Learning & Representation Learning

### 4.1 Clustering
- **K-means**: Lloyd's algorithm, k-means++, initialization, convergence
- **Hierarchical clustering**: agglomerative, divisive, linkage criteria
- **DBSCAN**: density-based, epsilon, minPts, noise points
- **Gaussian Mixture Models**: EM algorithm, soft clustering, BIC/AIC model selection
- **Spectral clustering**: graph Laplacian, eigenvectors, normalized cuts

### 4.2 Dimensionality Reduction
- **PCA**: eigendecomposition of covariance matrix, explained variance, kernel PCA
- **t-SNE**: perplexity, KL divergence, crowding problem
- **UMAP**: topological data analysis, fuzzy simplicial sets, cross-entropy
- **Autoencoders**: encoder-decoder architecture, bottleneck, reconstruction loss
- **Factor analysis**: latent variable models, probabilistic PCA

### 4.3 Density Estimation
- **Kernel Density Estimation (KDE)**: bandwidth selection, kernel functions
- **Gaussian Mixture Models**: soft clustering, density estimation
- **Normalizing Flows**: invertible transformations, change of variables, RealNVP, Glow

### 4.4 Self-Supervised Learning
- **Contrastive learning**: SimCLR, MoCo, InfoNCE loss, data augmentation
- **Masked prediction**: BERT-style masking, MAE for vision
- **Bootstrap your own latent (BYOL)**: online-offline networks, stop-gradient
- **DINO**: self-distillation with no labels, vision transformers

### 4.5 Lab: Build a Representation Learning Pipeline
- Implement PCA and t-SNE from scratch
- Train a contrastive learning model (SimCLR) on image data
- Evaluate learned representations with linear probing
- Visualize embeddings with UMAP and analyze cluster quality

---

## Module 5: Deep Learning — Neural Networks, Backpropagation & Optimization

### 5.1 Neural Network Foundations
- **Perceptron**: biological inspiration, linear separability, XOR problem
- **Multi-layer perceptron (MLP)**: universal approximation theorem
- **Activation functions**: sigmoid, tanh, ReLU, Leaky ReLU, GELU, Swish — derivatives, saturation
- **Weight initialization**: Xavier/Glorot, He initialization, orthogonal initialization
- **Normalization**: batch norm, layer norm, group norm, instance norm — forward, backward

### 5.2 Backpropagation
- **Computational graphs**: nodes, edges, forward pass, backward pass
- **Chain rule**: vector-Jacobian products, automatic differentiation
- **Vanishing/exploding gradients**: causes, detection, mitigation
- **Gradient clipping**: value clipping, norm clipping
- **Mixed precision training**: FP16/BF16 forward/backward, FP32 master weights, loss scaling

### 5.3 Convolutional Neural Networks
- **Convolution operation**: kernels, strides, padding, dilation
- **Pooling**: max pooling, average pooling, global pooling
- **Modern architectures**: ResNet (skip connections), DenseNet, EfficientNet, ConvNeXt
- **Transfer learning**: ImageNet pretraining, fine-tuning strategies, feature extraction
- **Object detection**: R-CNN family, YOLO, SSD, anchor boxes, NMS
- **Segmentation**: U-Net, Mask R-CNN, semantic vs instance segmentation

### 5.4 Recurrent Neural Networks & Sequence Models
- **RNN**: Elman, Jordan, BPTT, truncated BPTT
- **LSTM/GRU**: gating mechanisms, forget/input/output gates, peephole connections
- **Bidirectional RNNs**: forward + backward processing
- **Attention mechanism**: query-key-value, scaled dot-product, multi-head attention
- **Transformers**: self-attention, positional encoding, encoder-decoder, feed-forward networks

### 5.5 Training Deep Networks
- **Learning rate scheduling**: step decay, cosine annealing, warm restarts, one-cycle policy
- **Regularization**: dropout, dropconnect, data augmentation, cutout, mixup, cutmix
- **Early stopping**: validation loss monitoring, patience, checkpointing
- **Ensemble deep learning**: snapshot ensembles, SWA (stochastic weight averaging)
- **Neural architecture search (NAS)**: DARTS, ENAS, evolutionary methods

### 5.6 Lab: Build a Deep Learning Framework from Scratch
- Implement automatic differentiation with computational graphs
- Build MLP, CNN, and RNN layers with NumPy
- Train on MNIST and CIFAR-10
- Compare with PyTorch implementation
- Profile memory usage and computation graph

---

## Module 6: Computer Vision & Multimodal Learning

### 6.1 Modern Vision Architectures
- **Vision Transformers (ViT)**: patch embedding, global attention, inductive bias tradeoff
- **Swin Transformer**: shifted window attention, hierarchical features
- **ConvNeXt**: modernizing ConvNets with Transformer design choices
- **EfficientNet**: compound scaling, depth/width/resolution balance
- **Self-supervised vision**: MAE, DINO, iBOT, data-efficient training

### 6.2 Object Detection & Segmentation
- **Two-stage detectors**: Faster R-CNN, Mask R-CNN, Feature Pyramid Networks
- **One-stage detectors**: YOLOv8/v9, SSD, RetinaNet, focal loss
- **Transformer detectors**: DETR, Deformable DETR, DINO (Detection Transformer)
- **Segmentation**: SAM (Segment Anything), SAM 2, interactive segmentation
- **Panoptic segmentation**: unified semantic + instance segmentation

### 6.3 Generative Models for Vision
- **VAE**: encoder-decoder, reparameterization trick, ELBO
- **GANs**: generator, discriminator, minimax game, WGAN, StyleGAN
- **Diffusion models**: forward diffusion, reverse diffusion, DDPM, DDIM, latent diffusion
- **Flow-based models**: normalizing flows, invertible networks

### 6.4 Multimodal Learning
- **Vision-Language models**: CLIP, ALIGN, BLIP — contrastive learning, image-text alignment
- **Multimodal transformers**: Flamingo, GPT-4V, Gemini — interleaved modalities
- **Cross-modal retrieval**: text-to-image, image-to-text, zero-shot classification
- **Multimodal fusion**: early fusion, late fusion, intermediate fusion, attention-based fusion

### 6.5 Lab: Build a Multimodal Search System
- Fine-tune CLIP on domain-specific image-text pairs
- Build a vector index with FAISS for image retrieval
- Implement text-to-image and image-to-text search
- Evaluate zero-shot classification performance
- Deploy with ONNX Runtime for efficient inference

---

## Module 7: Natural Language Processing & Large Language Models

### 7.1 NLP Foundations
- **Tokenization**: BPE, WordPiece, SentencePiece, Unigram — vocabulary construction
- **Word embeddings**: Word2Vec (CBOW, Skip-gram), GloVe, FastText — subword information
- **Contextual embeddings**: ELMo, CoVe — bidirectional LSTM-based
- **Language modeling**: n-gram, neural LM, perplexity, cross-entropy

### 7.2 Transformer Architecture Deep Dive
- **Self-attention**: query-key-value, scaled dot-product, O(n²) complexity
- **Multi-head attention**: parallel attention heads, concatenation, linear projection
- **Positional encoding**: sinusoidal, learned, rotary (RoPE), ALiBi
- **Feed-forward networks**: GELU activation, expansion factor, dropout
- **Layer normalization**: pre-norm vs post-norm, RMSNorm
- **Encoder-decoder**: cross-attention, teacher forcing, autoregressive generation

### 7.3 Large Language Models
- **GPT family**: decoder-only, autoregressive, next-token prediction
- **BERT family**: encoder-only, masked language modeling, fine-tuning
- **T5/BART**: encoder-decoder, span corruption, denoising
- **Scaling laws**: Kaplan, Chinchilla — compute-optimal training
- **Instruction tuning**: FLAN, InstructGPT, supervised fine-tuning (SFT)
- **RLHF**: reward modeling, PPO, DPO, constitutional AI

### 7.4 LLM Training & Fine-Tuning
- **Pre-training**: data curation, deduplication, filtering, mixture of sources
- **Continual pre-training**: domain adaptation, catastrophic forgetting mitigation
- **Parameter-efficient fine-tuning**: LoRA, QLoRA, prefix tuning, prompt tuning, adapters
- **Alignment**: SFT → RLHF/DPO → iterative refinement
- **Tool use**: function calling, retrieval augmentation, agent frameworks

### 7.5 LLM Serving & Inference
- **KV caching**: storing key-value pairs for autoregressive generation
- **Quantization**: INT8, INT4, GPTQ, AWQ, GGUF — memory reduction, speedup
- **Speculative decoding**: draft model + target model, acceptance sampling
- **Continuous batching**: vLLM, TensorRT-LLM, TGI — throughput optimization
- **PagedAttention**: vLLM's memory management for efficient serving
- **Model parallelism**: tensor parallelism, pipeline parallelism, sequence parallelism

### 7.6 Lab: Build an LLM Fine-Tuning & Serving Pipeline
- Fine-tune Llama 3 with LoRA on a domain-specific dataset
- Evaluate with perplexity, BLEU, and human evaluation
- Quantize to 4-bit with GPTQ for inference
- Serve with vLLM for high-throughput generation
- Implement retrieval-augmented generation (RAG) with vector DB

---

## Module 8: Recommender Systems & Ranking

### 8.1 Recommendation Problem Formulation
- **Explicit vs implicit feedback**: ratings vs clicks, views, purchases
- **User-item matrix**: sparsity, cold start, long tail
- **Evaluation metrics**: precision@k, recall@k, NDCG, MRR, MAP, coverage, diversity
- **Business metrics**: CTR, conversion rate, revenue, engagement time

### 8.2 Classical Methods
- **Collaborative filtering**: user-based, item-based, matrix factorization (SVD, NMF)
- **Content-based filtering**: TF-IDF, item attributes, user profiles
- **Hybrid methods**: weighted, switching, mixed, feature combination
- **Association rules**: Apriori, FP-Growth, market basket analysis

### 8.3 Deep Learning for Recommendations
- **Neural collaborative filtering**: MLP for user-item interaction
- **Two-tower models**: separate encoders for users and items, dot product similarity
- **Sequential recommenders**: GRU4Rec, SASRec, BERT4Rec — session-based
- **Graph neural networks**: PinSage, LightGCN — leveraging interaction graphs

### 8.4 Production Recommendation Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              Production Recommendation System                │
├──────────────────────────────────────────────────────────────┤
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │
│  │   Request   │───▶│  Candidate  │───▶│   Ranking   │   │
│  │   (User)    │    │ Generation  │    │   Model     │   │
│  └─────────────┘    └─────────────┘    └──────┬──────┘   │
│       │                                         │          │
│       │    ┌─────────────┐    ┌─────────────┐  │          │
│       └───▶│  Feature    │◀──│  Feature    │◀─┘          │
│            │   Store     │    │   Cache     │             │
│            └─────────────┘    └─────────────┘             │
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │
│  │   Re-rank   │───▶│   Filter    │───▶│   Response  │   │
│  │  (Business) │    │  (Diversity)│    │   (Top-K)   │   │
│  └─────────────┘    └─────────────┘    └─────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

- **Candidate generation**: approximate nearest neighbor (ANN), FAISS, ScaNN, HNSW
- **Ranking model**: deep neural network, feature crosses, wide & deep
- **Re-ranking**: diversity, freshness, business rules, exploration/exploitation
- **A/B testing**: interleaving, counterfactual evaluation, guardrail metrics

### 8.5 Lab: Build a Two-Stage Recommender
- Implement matrix factorization with alternating least squares
- Build a two-tower neural network for candidate generation
- Index embeddings with FAISS for fast retrieval
- Train a ranking model with wide & deep architecture
- Deploy with real-time feature serving

---

## Module 9: Distributed Training & Scaling

### 9.1 Data Parallelism
- **Synchronous SGD**: all-reduce, gradient averaging, batch size scaling
- **Asynchronous SGD**: parameter server, stale gradients, convergence analysis
- **Ring AllReduce**: Horovod, PyTorch DDP — bandwidth-optimal collective
- **ZeRO (Zero Redundancy Optimizer)**: optimizer state partitioning, gradient partitioning, parameter partitioning
- **Fully Sharded Data Parallel (FSDP)**: PyTorch's ZeRO implementation

### 9.2 Model Parallelism
- **Tensor parallelism**: splitting layers across devices, Megatron-LM
- **Pipeline parallelism**: GPipe, PipeDream — micro-batching, bubble reduction
- **Sequence parallelism**: splitting along sequence dimension for long contexts
- **3D parallelism**: combining data, tensor, and pipeline parallelism

### 9.3 Mixed Precision & Memory Optimization
- **FP16/BF16 training**: automatic loss scaling, gradient scaling
- **Gradient checkpointing**: trading compute for memory
- **Activation checkpointing**: recomputing activations in backward pass
- **CPU offloading**: ZeRO-Offload, DeepSpeed — offloading to host memory

### 9.4 Fault Tolerance & Elasticity
- **Checkpointing**: frequency, async checkpointing, distributed checkpointing
- **Elastic training**: adding/removing workers, spot instance preemption handling
- **Determinism**: seed management, deterministic algorithms, reproducibility
- **Health monitoring**: GPU memory, temperature, NCCL errors, node failures

### 9.5 Frameworks
- **PyTorch Distributed**: DDP, FSDP, RPC, TorchElastic
- **TensorFlow Distributed**: MirroredStrategy, MultiWorkerMirroredStrategy, TPUStrategy
- **DeepSpeed**: ZeRO, 3D parallelism, inference optimization
- **Megatron-LM**: NVIDIA's large model training framework
- **JAX/Flax**: XLA compilation, pmap, pjit, mesh transformations

### 9.6 Lab: Train a Model with Distributed Data Parallelism
- Set up multi-GPU training with PyTorch DDP
- Implement gradient accumulation for large effective batch sizes
- Profile memory usage and optimize with gradient checkpointing
- Compare throughput: single GPU vs DDP vs FSDP
- Implement checkpointing and resume from preemption

---

## Module 10: Model Serving, Inference Optimization & Edge Deployment

### 10.1 Serving Patterns

| Pattern | Latency | Throughput | Complexity | Use Case |
|---------|---------|-----------|------------|----------|
| **Batch prediction** | High (minutes) | Very High | Low | Daily recommendations, reports |
| **Real-time API** | Low (<100ms) | Medium | Medium | Fraud detection, search ranking |
| **Streaming** | Very Low (<10ms) | High | High | IoT, real-time bidding |
| **Edge/On-device** | Ultra Low (<5ms) | Low | High | Mobile, autonomous vehicles |

### 10.2 Model Servers
- **TensorFlow Serving**: REST/gRPC, versioning, batching, A/B testing
- **TorchServe**: model archiving, custom handlers, metrics, profiling
- **Triton Inference Server**: multi-framework, dynamic batching, ensemble models
- **vLLM**: PagedAttention, continuous batching, high-throughput LLM serving
- **BentoML**: model packaging, deployment abstraction

### 10.3 Inference Optimization
- **Quantization**: post-training (PTQ), quantization-aware training (QAT), GPTQ, AWQ
- **Pruning**: magnitude pruning, structured pruning, movement pruning
- **Knowledge distillation**: teacher-student, hint learning, attention transfer
- **Compilation**: ONNX Runtime, TensorRT, OpenVINO, TVM, XLA — graph optimization, kernel fusion
- **Kernel optimization**: FlashAttention, FlashDecoding, fused operations

### 10.4 Edge & Mobile Deployment
- **TensorFlow Lite**: quantization, delegates (GPU, NPU), model optimization
- **Core ML**: Apple's ecosystem, ANE (Apple Neural Engine) utilization
- **ONNX Runtime Mobile**: cross-platform, optimized kernels
- **Model compression**: pruning, quantization, knowledge distillation for mobile

### 10.5 Lab: Optimize and Deploy a Model
- Convert a PyTorch model to ONNX
- Quantize to INT8 with TensorRT
- Benchmark latency and throughput before/after optimization
- Deploy on Triton Inference Server with dynamic batching
- Compare with edge deployment on mobile device

---

## Module 11: MLOps — Pipelines, Experiment Tracking & Model Registry

### 11.1 ML Pipelines
- **Workflow orchestration**: Airflow, Prefect, Dagster, Kubeflow Pipelines, Metaflow
- **Pipeline components**: data extraction, validation, transformation, training, evaluation, deployment
- **Pipeline versioning**: code, data, model, configuration versioning together
- **Reproducibility**: deterministic execution, containerization, dependency pinning

### 11.2 Experiment Tracking
- **MLflow**: logging metrics, parameters, artifacts, model registry
- **Weights & Biases**: experiment tracking, visualization, collaboration
- **TensorBoard**: metrics visualization, model graph, profiling
- **Sacred**: experiment configuration, observer pattern
- **Best practices**: systematic naming, hyperparameter logging, artifact versioning

### 11.3 Model Registry
- **Versioning**: semantic versioning for models, artifact storage
- **Staging**: development, staging, production, archived
- **Metadata**: training data, metrics, hyperparameters, dependencies, lineage
- **Approval workflows**: manual review, automated gates, compliance checks
- **Rollback**: instant rollback to previous version, traffic shifting

### 11.4 CI/CD for ML
- **GitOps**: Git as single source of truth, automated deployments
- **Testing**: unit tests (data transforms), integration tests (pipeline), model tests (performance)
- **Canary deployment**: gradual traffic shifting, automated rollback
- **Blue-green deployment**: zero-downtime updates, instant switchover
- **Feature flags**: toggling model versions, A/B test configuration

### 11.5 Lab: Build an End-to-End MLOps Pipeline
- Create a Kubeflow Pipeline with data validation, training, evaluation
- Track experiments with MLflow, log metrics and artifacts
- Register models with staging/production promotion workflow
- Implement automated testing: data validation, model performance, integration
- Deploy with canary rollout and automated rollback

---

## Module 12: Monitoring, Observability & Drift Detection

### 12.1 ML Monitoring Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    ML Monitoring Stack                       │
├──────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │   Data      │  │   Model     │  │   Business          │ │
│  │   Drift     │  │   Performance│  │   Metrics           │ │
│  │   (PSI/KS)  │  │   (AUC/RMSE)│  │   (CTR/Revenue)     │ │
│  └──────┬──────┘  └──────┬──────┘  └──────────┬────────────┘ │
│         │                │                    │              │
│         └────────────────┼────────────────────┘              │
│                          ▼                                   │
│                   ┌─────────────┐                            │
│                   │   Alerting  │                            │
│                   │  (PagerDuty)│                            │
│                   └──────┬──────┘                            │
│                          ▼                                   │
│                   ┌─────────────┐                            │
│                   │  Automated  │                            │
│                   │  Retraining │                            │
│                   │   Trigger   │                            │
│                   └─────────────┘                            │
└─────────────────────────────────────────────────────────────┘
```

### 12.2 Data Drift Detection
- **Population Stability Index (PSI)**: threshold-based drift quantification
- **Kolmogorov-Smirnov test**: distribution comparison, non-parametric
- **Wasserstein distance**: optimal transport-based drift measurement
- **Maximum Mean Discrepancy (MMD)**: kernel-based distribution comparison
- **Feature drift**: per-feature monitoring, correlation drift, covariate shift

### 12.3 Concept Drift & Model Degradation
- **Concept drift types**: sudden, gradual, incremental, recurring
- **Performance monitoring**: accuracy degradation, calibration drift, error analysis
- **Prediction drift**: output distribution changes, confidence score drift
- **Updatability**: model freshness, retraining frequency, incremental learning

### 12.4 Observability for ML
- **Structured logging**: prediction logs, feature logs, model version tracking
- **Distributed tracing**: request flow through feature store, model, post-processing
- **Metrics**: latency (p50, p95, p99), throughput, error rates, resource utilization
- **Dashboards**: Grafana, Datadog, custom ML monitoring dashboards

### 12.5 Automated Response
- **Alerting thresholds**: PSI > 0.25, accuracy drop > 5%, latency p99 > SLA
- **Auto-retraining**: triggered by drift detection, scheduled, or manual
- **Shadow mode**: new model runs in parallel, predictions logged but not served
- **Champion-challenger**: continuous A/B testing of model versions

### 12.6 Lab: Build an ML Monitoring System
- Deploy Evidently AI for drift detection
- Set up Prometheus + Grafana for model metrics
- Implement automated retraining pipeline triggered by drift
- Create alerting for performance degradation
- Build a dashboard showing model health over time

---

## Module 13: Responsible AI, Fairness & Ethics

### 13.1 Fairness in ML
- **Fairness definitions**: demographic parity, equalized odds, equal opportunity, calibration
- **Bias sources**: historical bias, representation bias, measurement bias, aggregation bias
- **Bias mitigation**: pre-processing (reweighting, resampling), in-processing (adversarial debiasing, constrained optimization), post-processing (threshold adjustment, calibration)
- **Fairness metrics**: disparate impact, equal opportunity difference, average odds difference

### 13.2 Explainability & Interpretability
- **Intrinsic interpretability**: linear models, decision trees, rule-based systems
- **Post-hoc explanation**: SHAP, LIME, attention visualization, saliency maps
- **Model-agnostic methods**: permutation importance, partial dependence plots, ICE curves
- **Causal interpretability**: counterfactual explanations, causal graphs
- **Regulatory requirements**: GDPR "right to explanation", EU AI Act

### 13.3 Privacy & Security
- **Differential privacy**: epsilon, delta, mechanisms (Laplace, Gaussian), composition
- **Federated learning**: horizontal, vertical, secure aggregation
- **Model inversion attacks**: reconstructing training data from model outputs
- **Membership inference**: determining if a sample was in training data
- **Adversarial robustness**: FGSM, PGD, adversarial training, certified defenses

### 13.4 Governance & Ethics
- **AI governance frameworks**: NIST AI RMF, EU AI Act, IEEE standards
- **Model cards**: documentation standard for model behavior, limitations, intended use
- **Datasheets for datasets**: documenting dataset creation, biases, limitations
- **Human-in-the-loop**: active learning, human review, feedback integration
- **Red teaming**: adversarial testing, stress testing, edge case evaluation

### 13.5 Lab: Build a Responsible AI Pipeline
- Audit a model for demographic parity and equalized odds
- Generate SHAP explanations for model predictions
- Implement differential privacy in training (DP-SGD)
- Create a model card with performance across subgroups
- Conduct red team testing for adversarial inputs

---

## Module 14: Advanced Topics — Reinforcement Learning, Causal Inference, AutoML

### 14.1 Reinforcement Learning
- **Markov Decision Processes (MDP)**: states, actions, rewards, transition probabilities
- **Value-based methods**: Q-learning, SARSA, DQN, Double DQN, Dueling DQN
- **Policy gradient methods**: REINFORCE, Actor-Critic, A2C, A3C, PPO
- **Model-based RL**: Dyna-Q, MuZero, world models
- **Applications**: recommendation systems, robotics, game playing, resource allocation

### 14.2 Causal Inference
- **Potential outcomes framework**: Rubin causal model, treatment effects
- **Causal graphs**: DAGs, d-separation, backdoor criterion, front-door criterion
- **Estimation methods**: propensity score matching, inverse probability weighting, doubly robust
- **Causal ML**: causal forests, meta-learners (S-Learner, T-Learner, X-Learner)
- **Applications**: A/B test analysis, uplift modeling, policy evaluation

### 14.3 AutoML & Neural Architecture Search
- **Hyperparameter optimization**: Bayesian optimization, Hyperband, BOHB
- **Neural Architecture Search (NAS)**: DARTS, ENAS, evolutionary algorithms
- **AutoML frameworks**: AutoGluon, H2O, TPOT, Auto-sklearn
- **Feature engineering automation**: Featuretools, AutoFeat
- **Cost-aware AutoML**: multi-objective optimization (accuracy vs latency vs cost)

### 14.4 Lab: Build an Advanced ML System
- Implement PPO for a custom environment
- Estimate causal treatment effects from observational data
- Run AutoML with AutoGluon and compare with hand-tuned models
- Deploy the best model with optimized inference

---

## Capstone Project

### Project: Production-Grade ML Platform for E-Commerce

Build a comprehensive ML platform for a large e-commerce company:

**Requirements:**
1. **Data pipeline**: Ingest clickstream, transaction, and product data from Kafka
2. **Feature store**: Real-time and batch features for users, products, and interactions
3. **Recommendation system**: Two-stage (candidate generation + ranking) with deep learning
4. **Search ranking**: Learning-to-rank model with query understanding
5. **Fraud detection**: Real-time transaction scoring with XGBoost
6. **Price optimization**: Dynamic pricing with demand forecasting
7. **LLM integration**: Product description generation, review summarization, customer support
8. **MLOps**: Full CI/CD with Kubeflow, MLflow, automated retraining
9. **Monitoring**: Drift detection, performance tracking, business metric correlation
10. **Responsible AI**: Fairness auditing, explainability, differential privacy

**Architecture:**
- Kafka + Spark Streaming for real-time data
- Redis + Feast for feature store
- PyTorch + DeepSpeed for model training
- Triton Inference Server for model serving
- FAISS for vector search
- Kubeflow + MLflow for MLOps
- Prometheus + Grafana for monitoring
- Evidently AI for drift detection

---

## Appendix A: Reading List & References

### Mathematics & Theory
- *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong
- *Pattern Recognition and Machine Learning* — Christopher Bishop
- *The Elements of Statistical Learning* — Hastie, Tibshirani, Friedman
- *Convex Optimization* — Boyd & Vandenberghe
- *Probabilistic Graphical Models* — Koller & Friedman

### Deep Learning
- *Deep Learning* — Goodfellow, Bengio, Courville
- *Dive into Deep Learning* — Zhang et al. (interactive, with code)
- *Natural Language Processing with Transformers* — Tunstall, von Werra, Wolf

### Production ML & MLOps
- *Designing Machine Learning Systems* — Chip Huyen
- *Building Machine Learning Pipelines* — Hannes Hapke, Catherine Nelson
- *Machine Learning Engineering* — Andriy Burkov
- *Reliable Machine Learning* — Sculley et al.

### Distributed Systems & Scaling
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Distributed Systems* — Tanenbaum & Van Steen
- *Programming Massively Parallel Processors* — Kirk & Hwu

### Responsible AI
- *Fairness and Machine Learning* — Barocas, Hardt, Narayanan
- *Interpretable Machine Learning* — Christoph Molnar
- *Weapons of Math Destruction* — Cathy O'Neil

---

## Appendix B: Tooling Matrix

### ML Frameworks
| Framework | Best For | Ecosystem |
|-----------|----------|-----------|
| **PyTorch** | Research, flexibility | TorchVision, TorchAudio, HuggingFace |
| **TensorFlow** | Production, deployment | Keras, TF Serving, TFX |
| **JAX** | High-performance research | Flax, Haiku, Optax |
| **XGBoost** | Tabular data, competitions | Native, sklearn API |
| **LightGBM** | Large tabular datasets | Fast training, categorical support |
| **scikit-learn** | Classical ML, prototyping | Comprehensive, well-documented |

### MLOps & Experiment Tracking
| Tool | Type | Best For |
|------|------|----------|
| **MLflow** | Open source | Experiment tracking, model registry |
| **Weights & Biases** | Managed | Visualization, collaboration |
| **Kubeflow** | Open source | Kubernetes-native ML pipelines |
| **Airflow** | Open source | Workflow orchestration |
| **Prefect** | Open source | Modern Pythonic workflows |

### Model Serving
| Tool | Type | Best For |
|------|------|----------|
| **Triton** | NVIDIA | Multi-framework, GPU optimization |
| **TorchServe** | PyTorch | PyTorch model serving |
| **TensorFlow Serving** | TensorFlow | TF model deployment |
| **vLLM** | Open source | High-throughput LLM serving |
| **BentoML** | Framework-agnostic | Model packaging, deployment |

### Feature Stores
| Tool | Type | Best For |
|------|------|----------|
| **Feast** | Open source | Real-time + batch features |
| **Tecton** | Managed | Enterprise feature platform |
| **Redis** | In-memory | Low-latency online serving |

### Monitoring
| Tool | Type | Best For |
|------|------|----------|
| **Evidently AI** | Open source | ML-specific drift detection |
| **WhyLabs** | Managed | Data-centric observability |
| **Arize** | Managed | ML observability platform |
| **Fiddler** | Managed | Model performance monitoring |

---

## Appendix C: Interview Preparation

### System Design: ML Systems
- Design a recommendation system for a streaming platform (Netflix)
- Design a fraud detection system for a payment processor
- Design a search ranking system for e-commerce
- Design an LLM serving infrastructure for a chat application
- Design a real-time bidding system for digital advertising

### ML Theory Deep Dives
- Derive backpropagation for a multi-layer neural network
- Explain bias-variance decomposition and its implications
- Compare gradient boosting vs random forests vs neural networks
- How would you handle class imbalance in a fraud detection model?
- Design a causal inference study for a new product feature

### Production ML
- How do you prevent training-serving skew?
- Design a drift detection system for a production model
- How do you scale model training from 1 GPU to 100 GPUs?
- Compare batch prediction vs real-time inference architectures
- How do you ensure model fairness across demographic groups?

### Coding Challenges
- Implement logistic regression with gradient descent from scratch
- Build a k-means clustering algorithm
- Implement matrix factorization for collaborative filtering
- Write a custom PyTorch Dataset and DataLoader
- Implement attention mechanism from scratch

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 2 weeks | 0-1 | Mathematics, ML lifecycle |
| **Classical ML** | 3 weeks | 2-4 | Data engineering, supervised, unsupervised |
| **Deep Learning** | 3 weeks | 5-7 | Neural networks, CV, NLP, LLMs |
| **Production Systems** | 3 weeks | 8-10 | Recommendations, distributed training, serving |
| **MLOps & Operations** | 2 weeks | 11-12 | Pipelines, monitoring, drift detection |
| **Responsible AI** | 1 week | 13 | Fairness, explainability, privacy |
| **Advanced Topics** | 1 week | 14 | RL, causal inference, AutoML |
| **Capstone** | 2 weeks | — | Production-grade platform |

**Total Duration: 17 weeks (4 months) full-time, or 8 months part-time**

---

*This syllabus treats machine learning as a systems engineering discipline. The models, frameworks, and infrastructure evolve rapidly, but the mathematical foundations, statistical principles, and systems thinking remain constant. Master the fundamentals, and you can adapt to any technology stack or research breakthrough.*

---

Download this file: [machine-learning-syllabus.md](sandbox:///mnt/agents/output/machine-learning-syllabus.md)