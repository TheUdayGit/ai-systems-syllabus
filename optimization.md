## File: optimization-syllabus.md

# Optimization for AI Systems Engineering

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Proficiency in Python/C++; solid linear algebra and multivariate calculus; familiarity with probability theory and numerical computing  
**Estimated Duration:** 6–12 months (full-time study + production implementation)  
**Philosophy:** Theory → Implementation → Systems → Infrastructure → Production Engineering

---

## Table of Contents

1. [Module 0: Mathematical Foundations & Computational Reasoning](#module-0-mathematical-foundations--computational-reasoning)
2. [Module 1: Convex Analysis & Optimization Fundamentals](#module-1-convex-analysis--optimization-fundamentals)
3. [Module 2: First-Order Methods: Theory & Practice](#module-2-first-order-methods-theory--practice)
4. [Module 3: Second-Order & Curvature-Aware Methods](#module-3-second-order--curvature-aware-methods)
5. [Module 4: Stochastic Optimization & Mini-Batch Methods](#module-4-stochastic-optimization--mini-batch-methods)
6. [Module 5: Distributed & Parallel Optimization](#module-5-distributed--parallel-optimization)
7. [Module 6: Constrained & Composite Optimization](#module-6-constrained--composite-optimization)
8. [Module 7: Non-Convex Optimization in Deep Learning](#module-7-non-convex-optimization-in-deep-learning)
9. [Module 8: Hyperparameter Optimization & AutoML](#module-8-hyperparameter-optimization--automl)
10. [Module 9: Optimization for Production AI Systems](#module-9-optimization-for-production-ai-systems)
11. [Module 10: Advanced Topics & Emerging Methods](#module-10-advanced-topics--emerging-methods)
12. [Capstone Projects](#capstone-projects)
13. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
14. [Recommended Resources & Bibliography](#recommended-resources--bibliography)

---

## Module 0: Mathematical Foundations & Computational Reasoning

**Duration:** 2–3 weeks  
**Objective:** Establish the mathematical maturity and computational reasoning required for rigorous optimization in production AI systems. This module treats optimization not as a collection of recipes, but as a principled discipline grounded in analysis, linear algebra, and probability.

### 0.1 Multivariate Calculus for Optimization
- **Gradients, Jacobians, Hessians:** Definition, computation, and geometric interpretation
- **Taylor Expansion:** First-order and second-order approximations, remainder terms
- **Directional Derivatives & Gâteaux Derivatives:** Generalization to infinite-dimensional spaces
- **Chain Rule for Compositions:** Backpropagation as a special case of reverse-mode automatic differentiation
- *Production Context:* 
  - Computing gradients in computation graphs (PyTorch autograd, TensorFlow XLA)
  - Hessian-vector products without forming the full Hessian (Pearlmutter's method)
  - Jacobian-vector products in normalizing flows and Neural ODEs

### 0.2 Linear Algebra in Optimization
- **Positive Definite & Semidefinite Matrices:** Characterizations, Cholesky decomposition
- **Eigenvalue & Singular Value Decompositions:** Spectral analysis of curvature
- **Matrix Norms & Condition Numbers:** Sensitivity of optimization problems
- **Quadratic Forms:** Definiteness, level sets, ellipsoids
- *Production Context:* 
  - Condition number analysis for training stability
  - Spectral analysis of Hessian in neural network landscapes
  - Preconditioning via matrix factorizations

### 0.3 Probability & Measure-Theoretic Foundations
- **Random Variables & Expectations:** Law of large numbers, central limit theorem
- **Convergence Modes:** Almost sure, in probability, in mean square, in distribution
- **Stochastic Processes:** Martingales, Markov chains, filtrations
- *Production Context:* 
  - Stochastic gradient descent as a stochastic approximation algorithm
  - Convergence analysis of randomized algorithms
  - Noise models in mini-batch gradients

### 0.4 Topology & Analysis on Manifolds
- **Open/Closed Sets, Compactness, Continuity**
- **Lipschitz Continuity & Smoothness:** L-smoothness, μ-strong convexity
- **Manifolds & Tangent Spaces:** Optimization on matrix manifolds (Stiefel, Grassmann)
- *Production Context:* 
  - Orthogonal constraints in recurrent networks
  - Low-rank optimization on Grassmann manifold
  - Riemannian optimization in metric learning

### 0.5 Computational Complexity & Information Theory
- **Oracle Complexity:** Query lower bounds for first-order and second-order methods
- **Arithmetic Intensity:** Flops vs. memory bandwidth in optimization algorithms
- *Production Context:* 
  - Understanding why SGD is communication-bound in distributed settings
  - Choosing between first-order and second-order methods based on problem structure
  - Roofline analysis for optimization kernel performance

---

## Module 1: Convex Analysis & Optimization Fundamentals

**Duration:** 3–4 weeks  
**Objective:** Master convex optimization as the foundational language of AI systems. While deep learning problems are non-convex, convex analysis provides the tools to understand convergence, design algorithms, and reason about approximations.

### 1.1 Convex Sets & Functions
- **Convex Sets:** Definition, examples, operations preserving convexity (intersection, affine images, perspective)
- **Convex Functions:** Epigraph characterization, Jensen's inequality
- **Strict & Strong Convexity:** Geometric interpretation, uniqueness of minimizers
- **Quasi-Convex & Log-Convex Functions:** Generalizations and applications
- *Production Context:* 
  - Convex relaxations in combinatorial optimization (neural architecture search)
  - Log-convex loss functions in probabilistic modeling
  - Convex constraints in resource allocation

### 1.2 Subgradients & Subdifferential Calculus
- **Subgradients:** Definition, existence for convex functions, subdifferential
- **Subgradient Calculus:** Sum rule, chain rule, pointwise maximum
- **ε-Subgradients:** Approximate subgradients for non-smooth optimization
- *Production Context:* 
  - Subgradient methods for L1 regularization (LASSO)
  - Non-smooth activation functions (ReLU) in backpropagation
  - Subgradient computation in max-margin losses

### 1.3 Duality Theory
- **Lagrangian & Dual Function:** Construction, weak duality
- **Strong Duality:** Slater's condition, constraint qualifications
- **KKT Conditions:** Necessary and sufficient conditions for optimality
- **Fenchel Conjugate & Biconjugate:** Fenchel-Young inequality, infimal convolution
- *Production Context:* 
  - Duality in adversarial training (GANs)
  - Dual decomposition in distributed optimization
  - KKT conditions for constrained neural network training
  - Fenchel duality in Wasserstein distance computation

### 1.4 Conic Optimization
- **Linear Programming:** Simplex method, interior-point methods, duality
- **Second-Order Cone Programming (SOCP):** Formulations, applications
- **Semidefinite Programming (SDP):** Matrix variables, relaxations
- **Exponential Cone & Relative Entropy Cone:** Modern conic programming
- *Production Context:* 
  - LP relaxations in integer programming for NAS
  - SDP relaxations in max-cut and community detection
  - SOCP in robust optimization and portfolio selection
  - Conic programming in optimal transport

### 1.5 Convex Optimization Software & Solvers
- **CVXPY, CVXOPT, MOSEK, Gurobi:** Modeling languages and commercial solvers
- **Interior-Point Methods:** Barrier functions, path-following, predictor-corrector
- **First-Order Methods for Large-Scale Convex Problems:** Proximal methods, ADMM
- *Production Context:* 
  - CVXPY for prototyping convex optimization layers in neural networks
  - MOSEK/Gurobi for production convex optimization
  - Interior-point methods in portfolio optimization
  - ADMM in distributed consensus optimization

---

## Module 2: First-Order Methods: Theory & Practice

**Duration:** 4–5 weeks  
**Objective:** First-order methods are the workhorse of modern AI. This module builds deep understanding of their theoretical properties, practical implementation, and systems implications.

### 2.1 Gradient Descent & Convergence Analysis
- **Exact Line Search vs. Fixed Step Size:** Convergence rates for L-smooth convex functions
- **Gradient Descent on Strongly Convex Functions:** Linear convergence, condition number dependence
- **Polyak-Lojasiewicz (PL) Condition:** Convergence without convexity
- **Nesterov's Lower Bounds:** Oracle complexity limits for first-order methods
- *Production Context:* 
  - Step size selection in full-batch training
  - Convergence monitoring in training pipelines
  - PL condition in overparameterized neural networks
  - Lower bound awareness for algorithm selection

### 2.2 Accelerated Gradient Methods
- **Nesterov Acceleration:** Momentum interpretation, optimal convergence rates
- **Heavy-Ball Method:** Polyak's momentum, dynamical systems perspective
- **Accelerated Proximal Methods:** FISTA, Nesterov's universal accelerated methods
- *Production Context:* 
  - Nesterov momentum in PyTorch/TensorFlow SGD
  - Heavy-ball momentum in large-scale vision training
  - FISTA for sparse coding and compressed sensing
  - Acceleration in convex optimization layers

### 2.3 Stochastic Gradient Descent (SGD)
- **SGD Convergence:** Robbins-Monro conditions, asymptotic normality
- **Mini-Batch SGD:** Variance reduction, batch size scaling laws
- **Learning Rate Schedules:** Step decay, exponential decay, cosine annealing, warmup
- *Production Context:* 
  - Mini-batch size selection for memory-compute trade-offs
  - Learning rate warmup in transformer training (BERT, GPT)
  - Cosine annealing in computer vision training
  - Step decay schedules and their theoretical justification

### 2.4 Adaptive Gradient Methods
- **AdaGrad:** Per-parameter learning rates, regret analysis
- **RMSProp:** Exponential moving average of squared gradients
- **Adam/AdamW:** Bias correction, decoupled weight decay, convergence analysis
- **Adam Variants:** AdaBound, Yogi, AdaBelief, RAdam, NAdam
- *Production Context:* 
  - Adam as default optimizer in NLP and transformers
  - AdamW replacing L2 penalty with decoupled weight decay
  - AdaBelief for improved generalization in vision tasks
  - Adaptive methods in sparse gradient settings (embeddings)

### 2.5 Variance Reduction Methods
- **SVRG (Stochastic Variance Reduced Gradient):** Snapshot gradients, variance reduction
- **SAGA:** Incremental gradient method with unbiased updates
- **Katyusha:** Accelerated variance reduction, optimal rates
- *Production Context:* 
  - SVRG for finite-sum optimization in ML
  - Variance reduction in federated learning
  - Katyusha for large-scale convex optimization
  - Trade-offs between variance reduction and implementation complexity

### 2.6 Coordinate Descent & Proximal Methods
- **Coordinate Descent:** Cyclic, randomized, greedy selection rules
- **Proximal Gradient Descent:** Soft-thresholding, proximal operators
- **Accelerated Proximal Methods:** APG, FISTA for composite objectives
- *Production Context:* 
  - Coordinate descent in LASSO and elastic net
  - Proximal methods for structured sparsity (group LASSO)
  - Proximal operators in constrained optimization layers
  - Coordinate descent in large-scale matrix factorization

---

## Module 3: Second-Order & Curvature-Aware Methods

**Duration:** 4–5 weeks  
**Objective:** Second-order methods offer superior convergence rates but face computational challenges. This module covers the theory, approximations, and distributed implementations that make them viable in production AI systems.

### 3.1 Newton's Method & Convergence
- **Classical Newton's Method:** Quadratic convergence, affine invariance
- **Damped Newton:** Line search, trust-region variants
- **Newton's Method for Non-Convex Problems:** Saddle point avoidance, local minima
- *Production Context:* 
  - Newton's method in small-scale optimization
  - Trust-region methods in reinforcement learning
  - Damped Newton in Gaussian process hyperparameter optimization

### 3.2 Quasi-Newton Methods
- **BFGS:** Secant equation, curvature condition, update formulas
- **L-BFGS:** Limited-memory approximation, two-loop recursion
- **SR1, DFP:** Alternative quasi-Newton updates
- *Production Context:* 
  - L-BFGS in full-batch training of small models
  - BFGS in hyperparameter optimization
  - L-BFGS in scientific computing and PDE-constrained optimization
  - Memory-efficient quasi-Newton for large models

### 3.3 Natural Gradient & Information Geometry
- **Fisher Information Matrix:** Definition, properties, relationship to Hessian
- **Natural Gradient Descent:** Parameterization-invariant optimization
- **Gauss-Newton Method:** Hessian approximation for least squares
- *Production Context:* 
  - Natural gradient in policy gradient methods (TRPO, PPO)
  - Gauss-Newton in neural network training
  - Fisher information in variational inference
  - Information geometry in probabilistic modeling

### 3.4 Kronecker-Factored Approximate Curvature (K-FAC)
- **Kronecker Factorization:** Fisher block approximation for neural networks
- **Distributed K-FAC:** Asynchronous computation, dedicated stats workers
- **Doubly-Factored K-FAC:** Scaling to wide layers
- *Production Context:* 
  - K-FAC for large-scale ImageNet training (2x speedup over SGD+BN)
  - Distributed K-FAC across multiple GPUs with asynchronous inversion
  - Kronecker factorization in transformer training
  - Trade-offs between curvature quality and computational cost citeweb_search:5#1web_search:5#4

### 3.5 Shampoo & Tensor Preconditioning
- **Shampoo Algorithm:** Preconditioner per tensor mode, Kronecker product structure
- **Distributed Shampoo:** CPU preconditioner computation, pipelined training
- **MLCommons AlgoPerf Winner:** 28% faster training than baseline
- *Production Context:* 
  - Shampoo in large-scale Transformer training (45% wall-time reduction)
  - Distributed Shampoo on TPU/GPU clusters with CPU offloading
  - Tensor preconditioning for embedding layers
  - Mixed-precision Shampoo with FP16/FP32 citeweb_search:5#0web_search:5#7

### 3.6 Hessian-Free & Inexact Newton Methods
- **Hessian-Vector Products:** Pearlmutter's method, finite differences
- **Conjugate Gradient Inner Loop:** Solving Newton systems iteratively
- **Truncated Newton:** Early stopping, trust-region integration
- *Production Context:* 
  - Hessian-free optimization in deep learning
  - Hessian-vector products in meta-learning
  - Truncated Newton in large-scale PDE-constrained optimization
  - CG-based Newton in physics-informed neural networks

---

## Module 4: Stochastic Optimization & Mini-Batch Methods

**Duration:** 4–5 weeks  
**Objective:** Stochastic optimization is the algorithmic heart of deep learning. This module covers the theory, variance analysis, and practical design of stochastic methods at scale.

### 4.1 Stochastic Approximation Theory
- **Robbins-Monro Algorithm:** Convergence conditions, asymptotic behavior
- **Kiefer-Wolfowitz:** Finite-difference gradient estimation
- **Stochastic Approximation with Constraints:** Projected algorithms, mirror descent
- *Production Context:* 
  - SGD as stochastic approximation
  - Finite-difference methods in black-box optimization
  - Projected SGD for constrained neural network training

### 4.2 Mini-Batch Scaling Laws
- **Linear Scaling Rule:** Learning rate proportional to batch size (up to a point)
- **Critical Batch Size:** Transition from linear to constant scaling
- **Gradient Noise Scale:** Measuring and utilizing noise in gradients
- *Production Context:* 
  - Batch size scaling in ImageNet training (linear up to ~8k)
  - Critical batch size estimation for efficient training
  - Gradient noise scale in large language model training
  - Optimal batch size for time-to-target accuracy

### 4.3 Momentum & Acceleration in Stochastic Settings
- **SGD with Momentum:** Convergence analysis, equivalence to accelerated methods
- **Nesterov Momentum in Stochastic Case:** Bias correction, variance effects
- **Quasi-Hyperbolic Momentum (QHM):** Interpolating between SGD and momentum
- *Production Context:* 
  - Momentum tuning in production training pipelines
  - Nesterov momentum in transformer training
  - QHM for improved convergence in vision tasks
  - Momentum scheduling across training phases

### 4.4 Adaptive Methods: Theory & Criticism
- **Adam Convergence Issues:** Non-convergence on convex problems, counterexamples
- **Decoupled Weight Decay (AdamW):** Separation of optimization and regularization
- **Adaptive Gradient Clipping:** Norm-based clipping, per-layer clipping
- *Production Context:* 
  - AdamW as standard for language model training
  - Gradient clipping in RNNs and transformers (norm thresholds)
  - Adaptive clipping in mixed-precision training
  - Convergence debugging in production training

### 4.5 Large-Batch Optimization
- **LARS (Layer-wise Adaptive Rate Scaling):** Scaling learning rates per layer
- **LAMB (Layer-wise Adaptive Moments):** Adam-like large-batch training
- **LARC:** Momentum-based layer-wise scaling
- *Production Context:* 
  - LARS in ImageNet training in minutes (batch size 32k+)
  - LAMB in BERT pretraining (batch size 64k+)
  - Layer-wise scaling for training stability at scale
  - Large-batch training in TPU pods

### 4.6 Noise Injection & Regularization
- **Gaussian Noise Injection:** Adding noise to gradients for regularization
- **Label Smoothing:** Soft targets for improved generalization
- **Mixup & CutMix:** Data augmentation as implicit regularization
- *Production Context:* 
  - Noise injection for improved generalization
  - Label smoothing in classification training
  - Mixup in vision model training pipelines
  - Implicit regularization from SGD noise

---

## Module 5: Distributed & Parallel Optimization

**Duration:** 4–5 weeks  
**Objective:** Modern AI training is inherently distributed. This module covers the optimization algorithms and systems design for training at scale, from data parallelism to federated learning.

### 5.1 Data Parallelism & Synchronization
- **Synchronous SGD:** All-reduce gradients, identical model replicas
- **Asynchronous SGD:** Parameter servers, stale gradients, convergence analysis
- **Semi-Synchronous Methods:** Bounded staleness, local updates
- *Production Context:* 
  - Synchronous SGD in Horovod, PyTorch DDP
  - Asynchronous SGD in parameter server architectures
  - Bounded staleness in large-scale training systems
  - Synchronization overhead analysis citeweb_search:6#2web_search:6#5

### 5.2 Gradient Compression & Communication Efficiency
- **Quantization:** 1-bit SGD, signSGD, QSGD
- **Sparsification:** Top-K gradient sparsification, random sparsification
- **Error Compensation:** Local error accumulation, convergence guarantees
- *Production Context:* 
  - Gradient compression in bandwidth-limited clusters
  - SignSGD for 32x communication reduction
  - Error compensation in DeepSpeed ZeRO
  - Communication-efficient federated learning

### 5.3 Model Parallelism & Pipeline Parallelism
- **Tensor Parallelism:** Splitting layers across devices, all-reduce communication
- **Pipeline Parallelism:** Micro-batching, bubble time, scheduling
- **3D Parallelism:** Combining data, tensor, and pipeline parallelism
- *Production Context:* 
  - Tensor parallelism in Megatron-LM
  - Pipeline parallelism in GPipe, PipeDream
  - 3D parallelism in large model training (GPT-3, PaLM)
  - Bubble time optimization and scheduling

### 5.4 Federated & Decentralized Optimization
- **FedAvg:** Local SGD, periodic averaging, convergence analysis
- **FedProx:** Proximal regularization for heterogeneous clients
- **Decentralized SGD:** Gossip averaging, network topology effects
- *Production Context:* 
  - Federated learning in mobile devices
  - FedAvg in cross-silo federated learning
  - Decentralized training in peer-to-peer networks
  - Heterogeneity handling in production federated systems

### 5.5 Asynchronous Optimization with Delays
- **Delay Models:** Bounded delays, unbounded delays, polynomial growth
- **Convergence Under Delays:** Step-size tuning, delay compensation
- **Rescaled ASGD:** Correcting for heterogeneous worker speeds
- *Production Context:* 
  - Asynchronous training in volunteer computing grids
  - Delay compensation in distributed parameter servers
  - Rescaled ASGD for heterogeneous GPU clusters citeweb_search:6#0web_search:6#1

### 5.6 Elastic & Fault-Tolerant Training
- **Checkpointing Strategies:** Synchronous, asynchronous, incremental
- **Elastic SGD:** Dynamic membership, shrinking/expanding clusters
- **Byzantine-Robust Optimization:** Krum, trimmed mean, coordinate-wise median
- *Production Context:* 
  - Elastic training in Kubernetes-orchestrated clusters
  - Byzantine-robust aggregation in federated learning
  - Fault tolerance in long-running training jobs
  - Dynamic resource allocation in cloud training

---

## Module 6: Constrained & Composite Optimization

**Duration:** 3–4 weeks  
**Objective:** Production AI systems routinely encounter constraints—resource budgets, latency requirements, regulatory limits. This module covers optimization with explicit constraints and non-smooth objectives.

### 6.1 Projected Gradient Methods
- **Projection Operators:** Euclidean projection, Bregman projection
- **Projected SGD:** Convergence rates, feasibility maintenance
- **Frank-Wolfe Algorithm:** Conditional gradient, linear minimization oracle
- *Production Context:* 
  - Projection onto norm balls for regularization
  - Frank-Wolfe for structured sparsity in model pruning
  - Projected methods for simplex constraints
  - Projection in adversarial example generation

### 6.2 Proximal Methods & Splitting Algorithms
- **Proximal Operators:** Definition, properties, examples (soft-thresholding, projection)
- **Proximal Gradient Descent:** Forward-backward splitting
- **ADMM (Alternating Direction Method of Multipliers):** Augmented Lagrangian, dual ascent
- **Douglas-Rachford Splitting:** Primal-dual methods
- *Production Context:* 
  - ADMM in distributed consensus optimization
  - Proximal methods for total variation denoising
  - Splitting algorithms in multi-objective optimization
  - ADMM in model parallel training

### 6.3 Conic & Semidefinite Constraints
- **Conic Programming:** LP, SOCP, SDP hierarchies
- **Semidefinite Relaxations:** Max-cut, community detection, neural network verification
- **Interior-Point Methods for Cones:** Barrier functions, central path
- *Production Context:* 
  - SDP relaxations in neural network robustness certification
  - Conic programming in optimal transport
  - Interior-point methods in portfolio optimization
  - Conic constraints in safe reinforcement learning

### 6.4 Non-Smooth & Subgradient Methods
- **Subgradient Descent:** Convergence rates, diminishing step sizes
- **Bundle Methods:** Cutting plane models, aggregation
- **ε-Subgradient Methods:** Approximate subgradients for large-scale problems
- *Production Context:* 
  - Subgradient methods for L1 regularization
  - Bundle methods in non-smooth risk minimization
  - Hinge loss optimization in SVMs
  - Non-smooth losses in adversarial training

### 6.5 Composite Objective Optimization
- **Composite Structure:** Smooth + non-smooth terms
- **Proximal Newton:** Second-order proximal methods
- **Catalyst Acceleration:** Generic acceleration for composite problems
- *Production Context:* 
  - Composite objectives in regularized risk minimization
  - Proximal Newton in group LASSO
  - Catalyst acceleration for generic optimization
  - Composite structure in training with regularization

---

## Module 7: Non-Convex Optimization in Deep Learning

**Duration:** 4–5 weeks  
**Objective:** Deep learning optimization is fundamentally non-convex. This module covers the landscape analysis, algorithm design, and practical techniques for navigating complex loss surfaces.

### 7.1 Loss Landscape Geometry
- **Critical Points:** Local minima, saddle points, plateaus
- **Hessian Spectral Analysis:** Bulk distribution, outliers, rank
- **Flat vs. Sharp Minima:** Generalization implications, sharpness-aware minimization
- *Production Context:* 
  - Hessian eigenvalue analysis for training diagnostics
  - Flat minima and generalization in large batch training
  - Sharpness-aware minimization (SAM) for improved generalization
  - Landscape visualization in training debugging

### 7.2 Saddle Point Escape & Second-Order Information
- **Saddle Point Problems:** Negative curvature exploitation
- **Trust Region Methods:** Cauchy point, dogleg method
- **Cubic Regularization:** Nesterov-Polyak cubic regularization
- *Production Context:* 
  - Trust region methods in policy optimization
  - Cubic regularization in non-convex optimization
  - Saddle point avoidance in GAN training
  - Second-order information in optimization debugging

### 7.3 Sharpness-Aware Minimization (SAM)
- **SAM Algorithm:** Adversarial weight perturbation, bi-level optimization
- **Efficient Variants:** Lookahead SAM, ESAM, memory-efficient SAM
- **Generalization Theory:** PAC-Bayes bounds, uniform stability
- *Production Context:* 
  - SAM for improved ImageNet generalization
  - Efficient SAM variants for large model training
  - Sharpness regularization in production pipelines
  - Memory-efficient implementations

### 7.4 Optimization for Specific Architectures
- **Transformers:** Learning rate warmup, attention-specific optimization
- **CNNs:** Batch normalization interaction, weight decay tuning
- **RNNs/LSTMs:** Gradient clipping, orthogonal initialization
- **GNNs:** Graph-level batching, neighborhood sampling
- *Production Context:* 
  - Transformer-specific optimization (AdamW, warmup, decay)
  - Batch normalization and optimization interaction
  - Gradient clipping in recurrent networks
  - Graph sampling in large-scale GNN training

### 7.5 Meta-Optimization & Learning to Optimize
- **L2L (Learning to Learn):** RNN optimizers, meta-gradient descent
- **Hypergradient Descent:** Learning learning rates online
- **Neural Architecture Search (NAS):** Differentiable NAS, RL-based NAS
- *Production Context:* 
  - Meta-optimization for automated hyperparameter tuning
  - Differentiable NAS in production model design
  - Learning to optimize for few-shot learning
  - Hypergradient methods for adaptive training

### 7.6 Optimization for Generative Models
- **GAN Training:** Minimax optimization, alternating updates, mode collapse
- **Diffusion Models:** Score matching, stochastic differential equations
- **Flow Matching:** Continuous normalizing flows, optimal transport
- *Production Context:* 
  - GAN training stabilization techniques
  - Diffusion model training at scale
  - Flow matching for high-resolution image generation
  - Minimax optimization in adversarial training

---

## Module 8: Hyperparameter Optimization & AutoML

**Duration:** 3–4 weeks  
**Objective:** Hyperparameter optimization is a critical systems problem in production AI. This module covers the algorithms and infrastructure for efficient hyperparameter search.

### 8.1 Bayesian Optimization
- **Gaussian Processes:** Kernels, acquisition functions, posterior updates
- **Acquisition Functions:** Expected Improvement, UCB, Thompson Sampling
- **Multi-Fidelity Methods:** Successive halving, Hyperband, BOHB
- *Production Context:* 
  - Bayesian optimization for learning rate tuning
  - Multi-fidelity BO for large-scale model training
  - Gaussian process surrogates for expensive evaluations
  - BO in neural architecture search citeweb_search:6#4web_search:6#6

### 8.2 Population-Based & Evolutionary Methods
- **Population-Based Training (PBT):** Online hyperparameter adaptation
- **Evolutionary Strategies:** CMA-ES, NEAT for architecture search
- **Genetic Algorithms:** Crossover, mutation, selection for NAS
- *Production Context:* 
  - PBT in reinforcement learning training
  - CMA-ES for black-box optimization
  - Evolutionary NAS in production model design
  - Population-based methods in AutoML systems

### 8.3 Hyperparameter Optimization at Scale
- **Distributed Search:** Parallel evaluations, asynchronous BO
- **Transfer Learning for HPO:** Meta-learning across datasets
- **Vizier, Optuna, Ray Tune:** Production HPO systems
- *Production Context:* 
  - Distributed HPO in Google Vizier
  - Optuna for production hyperparameter search
  - Ray Tune for distributed HPO at scale
  - Transfer HPO for rapid model development

### 8.4 Neural Architecture Search (NAS)
- **Differentiable NAS (DARTS):** Continuous relaxation, bi-level optimization
- **One-Shot NAS:** Weight sharing, supernets
- **Hardware-Aware NAS:** Latency constraints, FLOPS constraints
- *Production Context:* 
  - DARTS for efficient architecture search
  - One-shot NAS for mobile model deployment
  - Hardware-aware NAS for edge deployment
  - NAS in production model design pipelines

### 8.5 Automated Feature Engineering & Pipeline Optimization
- **AutoML Pipelines:** TPOT, Auto-sklearn
- **Feature Engineering Automation:** Deep Feature Synthesis, genetic programming
- **End-to-End Optimization:** Joint optimization of preprocessing and model
- *Production Context:* 
  - Automated feature engineering in production pipelines
  - End-to-end pipeline optimization
  - AutoML for tabular data processing
  - Pipeline optimization in MLOps systems

---

## Module 9: Optimization for Production AI Systems

**Duration:** 4–5 weeks  
**Objective:** Bridge the gap between optimization theory and production AI infrastructure. This module focuses on the operational aspects of optimization systems.

### 9.1 Mixed-Precision Training
- **FP16/BF16 Training:** Loss scaling, master weights, gradient scaling
- **FP8 Training:** Sub-8-bit formats, micro-scaling, precision decoupling
- **Automatic Mixed Precision (AMP):** Framework integration, op casting
- *Production Context:* 
  - Mixed-precision training in PyTorch AMP
  - FP8 training on NVIDIA H100 (Transformer Engine)
  - Loss scaling for gradient underflow prevention
  - Precision decoupling in FP8 LLM training citeweb_search:3#0

### 9.2 Memory Optimization Techniques
- **Gradient Checkpointing:** Trade compute for memory
- **Activation Compression:** Sparse attention, activation quantization
- **Optimizer State Sharding:** ZeRO, FSDP, parameter/gradient/optimizer partitioning
- *Production Context:* 
  - Gradient checkpointing in transformer training
  - ZeRO-Infinity for trillion-parameter models
  - FSDP in PyTorch for large model training
  - Memory-optimal training pipeline design

### 9.3 Compilation & Kernel Optimization
- **XLA, TVM, MLIR:** Compiler frameworks for optimization fusion
- **Operator Fusion:** Combining ops to reduce memory traffic
- **Custom CUDA Kernels:** Hand-optimized kernels for critical ops
- *Production Context:* 
  - XLA compilation for TPU training
  - Operator fusion in inference serving
  - Custom CUDA kernels for attention mechanisms
  - Compiler optimization in production training

### 9.4 Profiling & Performance Engineering
- **Training Step Profiling:** Forward pass, backward pass, optimizer step
- **Communication Profiling:** All-reduce, all-gather, point-to-point
- **Memory Profiling:** Allocation patterns, fragmentation, peak usage
- *Production Context:* 
  - PyTorch Profiler for training bottleneck identification
  - NCCL profiling for communication optimization
  - Memory profiling for OOM prevention
  - End-to-end training pipeline optimization

### 9.5 Numerical Stability & Debugging
- **NaN/Inf Detection:** Gradient norm monitoring, loss scaling
- **Gradient Accumulation:** Simulating large batches with limited memory
- **Reproducibility:** Deterministic algorithms, seeding, debugging
- *Production Context:* 
  - NaN detection and automatic recovery
  - Gradient accumulation for large effective batch sizes
  - Reproducible training for debugging and compliance
  - Numerical stability monitoring in production

### 9.6 Scaling Laws & Efficiency Analysis
- **Compute-Optimal Training:** Chinchilla scaling laws, optimal model/data ratios
- **Training Efficiency:** FLOPs utilization, model FLOPs utilization (MFU)
- **Cost Optimization:** Spot instances, preemptible training, budget constraints
- *Production Context:* 
  - Chinchilla-optimal training for LLMs
  - MFU measurement and optimization
  - Cost-efficient training on spot instances
  - Budget-constrained model development

---

## Module 10: Advanced Topics & Emerging Methods

**Duration:** 3–4 weeks  
**Objective:** Cover cutting-edge optimization methods that are shaping the future of AI systems.

### 10.1 Continuous-Time Optimization & Neural ODEs
- **Gradient Flow:** ODE interpretation of gradient descent
- **Neural ODEs:** Continuous-depth models, adjoint method
- **Hamiltonian Descent:** Momentum as physical system
- *Production Context:* 
  - Neural ODEs for memory-efficient deep learning
  - Continuous-time analysis of optimization algorithms
  - Hamiltonian dynamics in optimization design
  - Adjoint method for efficient backpropagation

### 10.2 Optimization on Manifolds & Geometric Methods
- **Riemannian Optimization:** Exponential map, parallel transport
- **Stiefel & Grassmann Manifolds:** Orthogonal constraints, subspace tracking
- **Natural Gradient Revisited:** Information geometry, Fisher metric
- *Production Context:* 
  - Riemannian optimization in metric learning
  - Orthogonal constraints in recurrent networks
  - Natural gradient in policy optimization
  - Geometric methods in representation learning

### 10.3 Quantum & Analog Optimization
- **Quantum Annealing:** Ising models, QUBO formulations
- **Variational Quantum Algorithms:** VQE, QAOA for optimization
- **Analog Computing:** Physical systems for optimization
- *Production Context:* 
  - Quantum optimization for combinatorial problems
  - Variational quantum algorithms for chemistry
  - Analog methods in specialized hardware
  - Quantum-classical hybrid optimization

### 10.4 Bi-Level & Multi-Objective Optimization
- **Bi-Level Optimization:** Hyperparameter optimization, meta-learning
- **Multi-Objective Pareto Optimization:** Trade-off surfaces, scalarization
- **Stackelberg Games:** Leader-follower dynamics in adversarial training
- *Production Context:* 
  - Bi-level optimization in neural architecture search
  - Multi-objective optimization in fair ML
  - Adversarial training as Stackelberg game
  - Pareto fronts in model compression

### 10.5 Optimization for Edge & Resource-Constrained Devices
- **Quantization-Aware Training:** Differentiable quantization, straight-through estimator
- **Pruning-Aware Training:** Structured/unstructured pruning, lottery ticket hypothesis
- **Knowledge Distillation:** Teacher-student training, soft targets
- *Production Context:* 
  - QAT for INT8/INT4 deployment
  - Structured pruning for mobile deployment
  - Knowledge distillation for model compression
  - Edge-optimized training pipelines

---

## Capstone Projects

Each student must complete **two** capstone projects: one from Category A (Implementation) and one from Category B (Systems/Infrastructure).

### Category A: Deep Implementation Projects

**A1. Production-Grade Distributed Second-Order Optimizer**
- Implement distributed K-FAC or Shampoo from scratch
- Support asynchronous preconditioner computation on CPU
- Integrate with PyTorch for large-scale transformer training
- Benchmark against Adam/AdamW on standard tasks
- **Systems Requirements:** Multi-node multi-GPU support, mixed-precision training, checkpointing, fault tolerance citeweb_search:5#0web_search:5#7

**A2. Asynchronous SGD with Delay Compensation**
- Implement Rescaled ASGD or similar delay-compensated method
- Support heterogeneous worker speeds and data heterogeneity
- Prove convergence under polynomial delay growth
- Benchmark against synchronous baselines
- **Systems Requirements:** Dynamic worker management, staleness tracking, convergence monitoring citeweb_search:6#1

**A3. Mixed-Precision Training Framework with Numerical Stability Monitoring**
- Implement FP16/BF16/FP8 training with automatic loss scaling
- Integrate gradient compression (Top-K, signSGD)
- Build real-time numerical stability dashboard
- **Systems Requirements:** Automatic precision selection, stability alerting, reproducibility guarantees

**A4. Bayesian Optimization Service for Hyperparameter Tuning**
- Implement Gaussian process-based Bayesian optimization
- Support multi-fidelity evaluation (successive halving)
- Integrate with distributed training infrastructure
- **Systems Requirements:** Scalable surrogate modeling, parallel evaluation, transfer learning across experiments citeweb_search:6#4web_search:6#6

### Category B: Systems & Infrastructure Projects

**B1. Optimization Backend for Large-Scale Training**
- Design a training backend supporting multiple optimizers (SGD, Adam, LAMB, Shampoo)
- Implement automatic optimizer selection based on model architecture
- Support elastic scaling and fault tolerance
- **Optimization Components:** Second-order methods, large-batch scaling, memory optimization

**B2. Distributed Federated Learning Platform**
- Build a federated learning system with FedAvg/FedProx
- Implement differential privacy and secure aggregation
- Support heterogeneous clients and unreliable networks
- **Optimization Components:** Decentralized optimization, compression, Byzantine robustness

**B3. Production Training Pipeline with Auto-Optimization**
- Design an end-to-end training pipeline with automatic hyperparameter tuning
- Integrate profiling, bottleneck detection, and automatic optimization
- Support A/B testing of optimization configurations
- **Optimization Components:** AutoML, profiling, cost optimization, reproducibility

**B4. Memory-Efficient Training System for LLMs**
- Build a training system supporting ZeRO-1/2/3, FSDP, and gradient checkpointing
- Implement automatic memory planning and offloading
- Support trillion-parameter model training
- **Optimization Components:** Memory optimization, pipeline parallelism, communication optimization

---

## Assessment & Evaluation Framework

### Formative Assessments (Continuous)
- **Weekly Problem Sets:** 3–5 theoretical and implementation problems
- **Implementation Reviews:** Code review sessions focusing on correctness, performance, and numerical stability
- **Reading Reviews:** Analysis of seminal papers with systems relevance

### Summative Assessments (Milestone)
- **Midterm Examination:** 
  - 4-hour closed-book exam
  - Theoretical proofs (30%), algorithm design (40%), systems analysis (30%)
  - Topics: Modules 0–5

- **Final Examination:**
  - 6-hour take-home exam
  - Open-systems (access to documentation, no human collaboration)
  - Design a complete optimization system from theory to production deployment
  - Topics: Modules 6–10 + integration

### Capstone Evaluation Rubric
| Criterion | Weight | Description |
|-----------|--------|-------------|
| Correctness | 20% | Mathematical correctness, convergence guarantees, numerical stability |
| Performance | 25% | Convergence speed, wall-clock time, hardware utilization |
| Systems Integration | 20% | Production readiness, fault tolerance, observability |
| Architecture Reasoning | 20% | Design decisions, trade-off analysis, scalability considerations |
| Documentation | 15% | Technical writing, operational runbooks, theoretical rigor |

---

## Recommended Resources & Bibliography

### Core Textbooks
1. **Boyd, Stephen & Vandenberghe, Lieven.** *Convex Optimization.* Cambridge University Press, 2004. — *The definitive reference for convex optimization foundations.*
2. **Nocedal, Jorge & Wright, Stephen J.** *Numerical Optimization* (2nd ed.). Springer, 2006. — *Comprehensive treatment of numerical optimization methods.*
3. **Bubeck, Sébastien.** *Convex Optimization: Algorithms and Complexity.* Foundations and Trends in Machine Learning, 2015. — *Concise, modern treatment with complexity focus.*
4. **Bottou, Léon, Curtis, Frank E. & Nocedal, Jorge.** "Optimization Methods for Large-Scale Machine Learning." *SIAM Review*, 60(2), 2018. — *Essential survey for ML optimization.* citeweb_search:4#5
5. **Beck, Amir.** *First-Order Methods in Optimization.* SIAM, 2017. — *Rigorous treatment of first-order methods.*

### Specialized Resources
6. **Martens, James & Grosse, Roger.** "Optimizing Neural Networks with Kronecker-factored Approximate Curvature." *ICML 2015.* — *K-FAC foundational paper.*
7. **Anil, Rohan et al.** "Scalable Second Order Optimization for Deep Learning." *arXiv:2002.09018, 2020.* — *Distributed Shampoo implementation.* citeweb_search:5#0
8. **Wang, Jing et al.** "A Survey of Optimization Methods for Training DL Models." *arXiv:2501.14458, 2025.* — *Comprehensive theoretical survey.* citeweb_search:4#11
9. **Zhou, Zhengyuan et al.** "Distributed Stochastic Optimization with Large Delays." *Mathematics of Operations Research, 2021.* — *Asynchronous optimization theory.* citeweb_search:6#2web_search:6#5

### Systems & AI Infrastructure
10. **Rajbhandari, Samyam et al.** "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models." *SC 2020.* — *Memory-efficient distributed training.*
11. **Narayanan, Deepak et al.** "Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM." *SC 2021.* — *Distributed training at scale.*
12. **Meta AI.** "Distributed Shampoo." *GitHub: facebookresearch/optimizers.* — *Production second-order optimizer.* citeweb_search:5#7
13. **Mahran, Ammar et al.** "Rescaled Asynchronous SGD: Optimal Distributed Optimization under Data and System Heterogeneity." *arXiv:2605.13434, 2026.* — *Latest async optimization theory.* citeweb_search:6#1

### Online Resources
- **Stanford EE364A/B:** Convex Optimization I & II
- **CMU 10-701/15-712:** Machine Learning, Distributed Systems
- **MIT 6.036:** Introduction to Machine Learning (Optimization Focus)
- **MLSys Conference Proceedings:** Systems for ML optimization

---

## Appendix: Production Checklist

Before deploying any optimization component to production, verify:

- [ ] **Convergence Correctness:** Verified on synthetic problems with known solutions
- [ ] **Numerical Stability:** Gradient norm monitoring, loss scaling validation, NaN/Inf detection
- [ ] **Scalability Tested:** Strong/weak scaling analysis, communication overhead quantified
- [ ] **Memory Safety:** No unbounded growth, workspace validation, OOM handling
- [ ] **Fault Tolerance:** Checkpointing, recovery, graceful degradation on worker failure
- [ ] **Reproducibility:** Deterministic execution, seeding, identical results across runs
- [ ] **Observability:** Loss curves, gradient norms, learning rate schedules, throughput metrics
- [ ] **Cost Efficiency:** FLOPs utilization, wall-clock time per epoch, cloud cost analysis
- [ ] **Documentation:** API docs, convergence guarantees, hyperparameter tuning guides

---

**End of Syllabus**

*Optimization is the engine of intelligent systems. Mastery of optimization at the systems level is the difference between training models that converge in theory and building infrastructure that trains models reliably, efficiently, and at planetary scale. The optimization algorithms you deploy today determine the capabilities of the AI systems that power tomorrow.*