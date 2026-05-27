## File: mathematics-for-ml-dl-syllabus.md

# Mathematics for Machine Learning and Deep Learning

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Proficiency in Python/C++; solid calculus, linear algebra, probability, and optimization; familiarity with basic machine learning concepts  
**Estimated Duration:** 6–12 months (full-time study + production implementation)  
**Philosophy:** Theory → Implementation → Systems → Infrastructure → Production Engineering

---

## Table of Contents

1. [Module 0: Mathematical Foundations for ML/DL](#module-0-mathematical-foundations-for-mldl)
2. [Module 1: Linear Algebra for Representation Learning](#module-1-linear-algebra-for-representation-learning)
3. [Module 2: Calculus & Optimization for Deep Learning](#module-2-calculus--optimization-for-deep-learning)
4. [Module 3: Probability & Statistics for Learning](#module-3-probability--statistics-for-learning)
5. [Module 4: Approximation Theory & Function Spaces](#module-4-approximation-theory--function-spaces)
6. [Module 5: Geometric Deep Learning & Symmetry](#module-5-geometric-deep-learning--symmetry)
7. [Module 6: Graph Theory & Spectral Methods](#module-6-graph-theory--spectral-methods)
8. [Module 7: Information Geometry & Manifold Learning](#module-7-information-geometry--manifold-learning)
9. [Module 8: Dynamical Systems & Neural ODEs](#module-8-dynamical-systems--neural-odes)
10. [Module 9: Statistical Learning Theory & Generalization](#module-9-statistical-learning-theory--generalization)
11. [Module 10: Mathematics in Production Deep Learning](#module-10-mathematics-in-production-deep-learning)
12. [Capstone Projects](#capstone-projects)
13. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
14. [Recommended Resources & Bibliography](#recommended-resources--bibliography)

---

## Module 0: Mathematical Foundations for ML/DL

**Duration:** 2–3 weeks  
**Objective:** Establish the unified mathematical language for machine learning and deep learning. This module synthesizes prerequisite knowledge into a coherent framework for understanding modern AI architectures.

### 0.1 The Mathematical Landscape of ML/DL
- **The Five Pillars:** Linear algebra, calculus, probability, optimization, information theory
- **Function Spaces:** From finite-dimensional vector spaces to infinite-dimensional Hilbert/Banach spaces
- **Approximation Paradigms:** Universal approximation, representer theorem, kernel methods
- **Statistical Framework:** Empirical risk minimization, Bayesian inference, PAC learning
- *Production Context:* 
  - Understanding which mathematical tools apply to which ML problems
  - Mapping theoretical guarantees to production system requirements
  - Mathematical maturity for reading research papers and implementing novel architectures

### 0.2 Tensors & Multi-Dimensional Arrays
- **Tensor Algebra:** Tensor product, contraction, Einstein summation convention
- **Tensor Decompositions:** CP, Tucker, tensor train (TT), hierarchical Tucker
- **Tensor Operations in Deep Learning:** Einsum, batch operations, broadcasting
- *Production Context:* 
  - Tensor contractions in transformer attention mechanisms
  - Tensor decompositions in model compression and efficient attention
  - Einsum optimization in PyTorch/TensorFlow computation graphs

### 0.3 Computational Complexity & Scaling Laws
- **Big-O for ML Operations:** Matrix multiplication, convolution, attention complexity
- **Arithmetic Intensity:** Roofline model, memory-bound vs. compute-bound operations
- **Scaling Laws:** Kaplan et al. scaling, compute-optimal training, emergent abilities
- *Production Context:* 
  - Complexity analysis of transformer architectures (O(n²) attention)
  - Scaling law predictions for model training budgets
  - Arithmetic intensity optimization for GPU kernel design

---

## Module 1: Linear Algebra for Representation Learning

**Duration:** 3–4 weeks  
**Objective:** Linear algebra is the language of representation learning. This module covers the matrix methods that power embeddings, transformations, and dimensionality reduction in production systems.

### 1.1 Vector Spaces & Linear Maps in ML
- **Feature Spaces:** Input space, hidden representations, output space
- **Linear Transformations:** Layers as linear maps, weight matrices, bias as translation
- **Change of Basis:** PCA, ICA, whitening, normalization
- *Production Context:* 
  - Weight matrices as learned linear transformations between feature spaces
  - Batch normalization as adaptive whitening
  - Change of basis in transfer learning and domain adaptation

### 1.2 Matrix Decompositions for ML
- **Eigendecomposition:** Spectral analysis, power iteration, deflation
- **SVD & Low-Rank Approximation:** Truncated SVD, randomized SVD, streaming SVD
- **QR & Cholesky:** Orthogonalization, least squares, covariance structures
- *Production Context:* 
  - Low-rank SVD in model compression (LoRA, adapters)
  - Randomized SVD in large-scale recommendation systems
  - Cholesky in Gaussian process covariance computation

### 1.3 Spectral Methods & Graph Analysis
- **Graph Laplacian:** Combinatorial, normalized, random walk variants
- **Spectral Clustering:** Eigenvector embedding, k-means in spectral space
- **Spectral Graph Convolutions:** Graph Fourier transform, Chebyshev polynomials
- *Production Context:* 
  - Spectral clustering in community detection and graph partitioning
  - Graph Laplacian in GNN message passing
  - Spectral convolutions in graph neural networks (GraphSAGE, GCN)

### 1.4 Structured Matrices & Fast Transforms
- **Toeplitz & Circulant:** Convolution as matrix multiplication, FFT acceleration
- **Sparse & Banded:** Sparse attention patterns, structured sparsity
- **Kronecker Products:** Separable convolutions, tensor network contractions
- *Production Context:* 
  - Circulant matrices in fast convolution implementations
  - Sparse attention in Longformer, BigBird, sparse transformers
  - Kronecker products in separable convolutions and tensor operations

---

## Module 2: Calculus & Optimization for Deep Learning

**Duration:** 4–5 weeks  
**Objective:** Calculus and optimization power the training of deep neural networks. This module covers the theory and practice of gradient-based learning at scale.

### 2.1 Gradients & Backpropagation
- **Chain Rule on Computational Graphs:** Forward pass, backward pass, gradient flow
- **Jacobian-Vector Products:** Efficient gradient computation, automatic differentiation
- **Hessian-Vector Products:** Second-order information without full Hessian
- *Production Context:* 
  - Backpropagation in PyTorch autograd and TensorFlow gradient tape
  - Hessian-vector products in second-order optimization (K-FAC, Shampoo)
  - Custom gradients for non-differentiable operations (quantization, sampling)

### 2.2 Optimization Landscapes
- **Critical Points:** Local minima, saddle points, plateaus, flat minima
- **Hessian Spectral Analysis:** Eigenvalue distribution, condition number, rank
- **Landscape Geometry:** Connectedness, mode connectivity, linear mode connectivity
- *Production Context:* 
  - Saddle point escape in non-convex optimization
  - Flat minima and generalization (Sharpness-Aware Minimization)
  - Landscape visualization for debugging training instability

### 2.3 Stochastic Optimization
- **SGD & Mini-Batch:** Variance analysis, learning rate schedules, momentum
- **Adaptive Methods:** AdaGrad, RMSProp, Adam, AdamW, convergence properties
- **Large-Batch Optimization:** LARS, LAMB, layer-wise adaptive rates
- *Production Context:* 
  - AdamW as standard optimizer for LLM training
  - LAMB for large-batch BERT pretraining
  - Learning rate scheduling (warmup, cosine annealing, decay)

### 2.4 Constrained & Structured Optimization
- **Projected Gradient Descent:** Norm constraints, simplex constraints
- **Proximal Methods:** L1 regularization, group LASSO, structured sparsity
- **Riemannian Optimization:** Optimization on manifolds (Stiefel, Grassmann)
- *Production Context:* 
  - Weight decay and L2 regularization in training
  - Structured pruning via proximal methods
  - Orthogonal constraints in recurrent networks via Riemannian optimization

---

## Module 3: Probability & Statistics for Learning

**Duration:** 4–5 weeks  
**Objective:** Probability and statistics provide the language for uncertainty, generalization, and decision-making in machine learning systems.

### 3.1 Probabilistic Models & Maximum Likelihood
- **Exponential Families:** Sufficient statistics, conjugate priors, maximum entropy
- **MLE & MAP:** Likelihood maximization, regularization as prior
- **Probabilistic Graphical Models:** Bayesian networks, Markov random fields, factor graphs
- *Production Context:* 
  - Cross-entropy loss as negative log-likelihood
  - Regularization as MAP with Gaussian/Laplacian priors
  - Graphical models in structured prediction and causal inference

### 3.2 Bayesian Deep Learning
- **Variational Inference:** ELBO, reparameterization trick, amortized inference
- **MCMC for Neural Networks:** Stochastic gradient Langevin dynamics (SGLD)
- **Laplace Approximation:** Local Gaussian approximation, Hessian computation
- *Production Context:* 
  - Variational dropout as Bayesian approximation
  - SGLD in Bayesian neural network training
  - Laplace approximation for uncertainty quantification in production

### 3.3 Gaussian Processes & Kernel Methods
- **GP Regression & Classification:** Kernel design, posterior computation, hyperparameters
- **Neural Tangent Kernel (NTK):** Infinite-width limit, kernel regime, training dynamics
- **Kernel Approximation:** Random features, Nyström method, sparse GPs
- *Production Context:* 
  - GPs in Bayesian optimization for hyperparameter tuning
  - NTK analysis of neural network training dynamics
  - Sparse GPs in large-scale regression tasks

### 3.4 Sampling & Monte Carlo Methods
- **Importance Sampling:** Proposal design, self-normalization, variance reduction
- **MCMC:** Metropolis-Hastings, Gibbs sampling, Hamiltonian Monte Carlo
- **Variational Autoencoders:** Encoder-decoder, latent space, generative modeling
- *Production Context:* 
  - Importance sampling in off-policy reinforcement learning
  - MCMC in posterior inference for Bayesian models
  - VAEs in generative modeling and representation learning

---

## Module 4: Approximation Theory & Function Spaces

**Duration:** 4–5 weeks  
**Objective:** Approximation theory explains why neural networks work. This module covers the mathematical foundations of universal approximation, depth efficiency, and function space embeddings.

### 4.1 Universal Approximation Theorems
- **Cybenko's Theorem:** Single hidden layer, sigmoid activation, dense approximation
- **Hornik's Extension:** Bounded measurable functions, non-polynomial activation
- **Leshno et al.:** Necessary and sufficient conditions for universal approximation
- *Production Context:* 
  - Understanding expressivity of MLPs vs. CNNs vs. Transformers
  - Activation function selection based on approximation properties
  - Depth-width trade-offs in architecture design

### 4.2 Depth & Expressivity
- **Depth Efficiency:** Exponential advantage of depth over width (Telgarsky, Eldan-Shamir)
- **VC Dimension of Neural Networks:** Bounds, activation-dependent complexity
- **Rademacher Complexity:** Data-dependent generalization bounds for deep networks
- *Production Context:* 
  - Depth efficiency in choosing architecture depth for vision vs. NLP tasks
  - VC dimension in understanding overparameterization benefits
  - Rademacher complexity in generalization analysis

### 4.3 Sobolev Spaces & Smooth Approximation
- **Sobolev Embeddings:** Regularity, approximation rates, Barron spaces
- **Spectral Bias:** Neural networks learn low frequencies first
- **Fourier Analysis of NNs:** Frequency principle, initialization effects
- *Production Context:* 
  - Spectral bias in understanding training dynamics (PINNs, GANs)
  - Barron spaces in analyzing approximation rates for ReLU networks
  - Fourier features in positional encoding and neural radiance fields

### 4.4 Kernel Methods & Neural Networks
- **Neural Tangent Kernel:** Infinite-width limit, kernel gradient descent, convergence
- **Mean-Field Analysis:** Wasserstein gradient flow, McKean-Vlasov equations
- **Feature Learning:** Beyond kernel regime, adaptive representations
- *Production Context:* 
  - NTK in understanding wide network training
  - Mean-field analysis in neural network training dynamics
  - Feature learning in finite-width networks vs. kernel regime

---

## Module 5: Geometric Deep Learning & Symmetry

**Duration:** 4–5 weeks  
**Objective:** Geometric deep learning leverages symmetry and geometry to design principled architectures. This module covers group theory, representation theory, and equivariant networks.

### 5.1 Group Theory for Deep Learning
- **Groups & Group Actions:** Definition, examples (translation, rotation, permutation)
- **Subgroups & Quotients:** Stabilizers, orbits, homogeneous spaces
- **Lie Groups:** Matrix Lie groups (SO(n), SE(n)), Lie algebras, exponential map
- *Production Context:* 
  - Translation equivariance in CNNs (group = ℤ²)
  - Rotation equivariance in medical imaging and robotics
  - Permutation equivariance in graph neural networks (Sₙ)

### 5.2 Representation Theory
- **Linear Representations:** Irreducible representations, Schur's lemma, character theory
- **Induced Representations:** Frobenius reciprocity, Mackey theory
- **Peter-Weyl Theorem:** Fourier analysis on compact groups, spherical harmonics
- *Production Context:* 
  - Irreducible representations in steerable CNNs
  - Spherical harmonics in 3D shape analysis and molecular modeling
  - Fourier analysis on groups for equivariant convolutions

### 5.3 Equivariant Neural Networks
- **G-Equivariant Layers:** Intertwiners, kernel constraints, steerable filters
- **Group Convolutions:** Lifting, group correlation, pooling
- **Gauge Equivariance:** Local symmetries, principal bundles, connection fields
- *Production Context:* 
  - E(n)-equivariant networks in 3D vision and point cloud processing
  - SE(3)-equivariant networks in robotics and molecular dynamics
  - Gauge equivariant CNNs on manifolds and meshes

### 5.4 Geometric Deep Learning Blueprint
- **The 5 G's:** Graphs, grids, groups, geodesics, gauges
- **Domain-Specific Architectures:** CNNs (grids), GNNs (graphs), spherical CNNs
- **Symmetry-Preserving Design:** Invariance vs. equivariance, quotient spaces
- *Production Context:* 
  - Geometric deep learning blueprint for novel architecture design
  - Domain-specific equivariant architectures for scientific computing
  - Symmetry-preserving constraints in physics-informed neural networks

---

## Module 6: Graph Theory & Spectral Methods

**Duration:** 3–4 weeks  
**Objective:** Graphs model relational data. This module covers graph theory, spectral graph theory, and graph neural networks with mathematical rigor.

### 6.1 Graph Theory Foundations
- **Graphs & Matrices:** Adjacency, Laplacian, incidence, transition matrices
- **Spectral Graph Theory:** Eigenvalues, Cheeger inequality, expanders
- **Random Graphs:** Erdős-Rényi, preferential attachment, stochastic block models
- *Production Context:* 
  - Graph Laplacian in spectral clustering and community detection
  - Expander graphs in network design and LDPC codes
  - Random graph models in social network analysis

### 6.2 Graph Neural Networks: Mathematical Foundations
- **Message Passing:** Spatial domain, aggregation functions, over-smoothing
- **Spectral GNNs:** Graph Fourier transform, ChebNet, CayleyNet
- **Weisfeiler-Lehman Test:** Graph isomorphism, expressivity limits, GNN power
- *Production Context:* 
  - Message passing in PyTorch Geometric and DGL
  - Spectral GNNs in molecular property prediction
  - WL test in analyzing GNN expressivity limits

### 6.3 Graph Signal Processing
- **Graph Filters:** Polynomial filters, rational filters, ARMA filters
- **Graph Wavelets:** Spectral wavelets, diffusion wavelets, frame theory
- **Sampling on Graphs:** Bandlimited signals, reconstruction, uncertainty principle
- *Production Context:* 
  - Graph filters in graph convolutional networks
  - Graph wavelets in multi-scale graph analysis
  - Graph sampling in large-scale graph neural network training

---

## Module 7: Information Geometry & Manifold Learning

**Duration:** 3–4 weeks  
**Objective:** Information geometry provides the differential-geometric structure of statistical models. Manifold learning discovers low-dimensional structure in high-dimensional data.

### 7.1 Information Geometry
- **Statistical Manifolds:** Fisher metric, exponential families, natural gradient
- **Amari-Chentsov Tensor:** α-connections, dual flatness, divergence functions
- **Natural Gradient Descent:** Fisher-Rao metric, adaptive learning rates
- *Production Context:* 
  - Natural gradient in second-order optimization (K-FAC)
  - Information geometry in variational inference
  - Fisher metric in understanding parameter space geometry

### 7.2 Manifold Learning & Dimensionality Reduction
- **Classical Methods:** PCA, MDS, Isomap, LLE, t-SNE, UMAP
- **Riemannian Manifold Learning:** Metric learning, geodesic computation, embeddings
- **Diffusion Maps:** Spectral embedding, diffusion distances, multiscale analysis
- *Production Context:* 
  - UMAP in visualization and representation learning
  - Metric learning in similarity search and retrieval
  - Diffusion maps in single-cell analysis and genomics

### 7.3 Hyperbolic & Non-Euclidean Embeddings
- **Hyperbolic Geometry:** Poincaré ball, Lorentz model, gyrovector spaces
- **Tree-Like Data:** Hierarchical embeddings, distortion trade-offs
- **Product Manifolds:** Mixed-curvature spaces, spherical, Euclidean, hyperbolic
- *Production Context:* 
  - Hyperbolic embeddings in hierarchical data (WordNet, taxonomies)
  - Mixed-curvature spaces in multi-relational graph embeddings
  - Non-Euclidean geometry in recommender systems

---

## Module 8: Dynamical Systems & Neural ODEs

**Duration:** 3–4 weeks  
**Objective:** Viewing neural networks as dynamical systems provides insights into training, architecture design, and continuous-time models.

### 8.1 Neural ODEs & Continuous Models
- **Neural ODEs:** Continuous-depth networks, adjoint method, sensitivity
- **Stability Analysis:** Lyapunov stability, equilibrium points, bifurcations
- **Discretization as Architecture:** Euler → ResNet, Runge-Kutta → DenseNet
- *Production Context:* 
  - Neural ODEs in continuous-time generative models
  - Stability analysis in training deep ResNets
  - ODE-inspired architectures (RevNet, i-RevNet)

### 8.2 Optimization as Dynamical Systems
- **Gradient Flow:** ODE interpretation, convergence rates, energy dissipation
- **Momentum as Physics:** Heavy ball, Nesterov as discretized ODEs
- **Stochastic Gradient Flow:** SDE limits, noise injection, escape from saddle points
- *Production Context:* 
  - Gradient flow analysis in understanding optimization dynamics
  - Momentum methods as physical system discretization
  - SDE limits in analyzing SGD noise and generalization

### 8.3 Hamiltonian & Symplectic Neural Networks
- **Hamiltonian Systems:** Phase space, symplectic structure, conservation laws
- **Symplectic Integrators:** Leapfrog, Verlet, structure-preserving learning
- **Conservation Laws:** Noether's theorem, equivariant dynamics
- *Production Context:* 
  - Hamiltonian networks in physics simulation and molecular dynamics
  - Symplectic integrators in long-term stability of learned dynamics
  - Conservation-aware neural networks in scientific computing

---

## Module 9: Statistical Learning Theory & Generalization

**Duration:** 4–5 weeks  
**Objective:** Statistical learning theory explains when and why deep learning models generalize. This module covers PAC learning, uniform convergence, and modern generalization theory.

### 9.1 PAC Learning & Complexity Bounds
- **PAC Framework:** Probably approximately correct, sample complexity, VC dimension
- **Rademacher Complexity:** Data-dependent bounds, contraction, Dudley integral
- **Covering Numbers:** Metric entropy, bracketing, chaining arguments
- *Production Context:* 
  - VC dimension in architecture capacity control
  - Rademacher bounds in generalization analysis
  - Metric entropy in understanding function class complexity

### 9.2 Uniform Convergence & Stability
- **Uniform Law of Large Numbers:** Glivenko-Cantelli, Donsker classes
- **Algorithmic Stability:** Uniform stability, hypothesis stability, pointwise stability
- **Stability-Generalization:** Bousquet-Elisseeff bounds, regularization connection
- *Production Context:* 
  - Uniform convergence in validation set design
  - Stability in differential privacy and federated learning
  - Algorithmic stability in understanding SGD generalization

### 9.3 Modern Generalization Theory
- **Double Descent:** Classical U-curve, interpolation threshold, over-parameterization
- **Benign Overfitting:** Minimum norm interpolants, RKHS, implicit regularization
- **PAC-Bayes & Information Bounds:** KL-regularization, flat minima, compression bounds
- *Production Context:* 
  - Double descent in large model scaling decisions
  - Benign overfitting in understanding over-parameterized networks
  - PAC-Bayes in sharpness-aware minimization (SAM)

### 9.4 Implicit Regularization & Inductive Bias
- **Implicit Bias of SGD:** Norm minimization, margin maximization
- **Architecture Bias:** Depth, width, skip connections, convolutional structure
- **Initialization Bias:** Neural tangent kernel, lazy training, rich regime
- *Production Context:* 
  - Implicit regularization in understanding training dynamics
  - Architecture bias in choosing CNN vs. Transformer vs. MLP
  - Initialization schemes (Xavier, He) and their theoretical foundations

---

## Module 10: Mathematics in Production Deep Learning

**Duration:** 4–5 weeks  
**Objective:** Bridge mathematical theory to production deep learning infrastructure. This module focuses on the operational aspects of mathematical methods in AI systems.

### 10.1 Numerical Stability in Deep Learning
- **Floating-Point Arithmetic:** IEEE 754, subnormal numbers, rounding modes
- **Gradient Underflow/Overflow:** Loss scaling, gradient clipping, log-space computation
- **Conditioning of Layers:** Spectral normalization, weight initialization, batch normalization
- *Production Context:* 
  - Mixed-precision training (FP16/BF16/FP32/FP8)
  - Numerical stability in attention mechanisms (softmax scaling)
  - Spectral normalization in GAN training stability

### 10.2 Efficient Mathematical Kernels
- **BLAS & LAPACK:** Level 1/2/3 operations, vendor libraries (MKL, cuBLAS)
- **Custom CUDA Kernels:** Shared memory, coalescing, warp primitives
- **Kernel Fusion:** XLA, TVM, MLIR for operator optimization
- *Production Context:* 
  - cuBLAS GEMM optimization in transformer training
  - Custom CUDA kernels for attention mechanisms (Flash Attention)
  - Kernel fusion in inference optimization (TensorRT, ONNX Runtime)

### 10.3 Distributed Mathematical Operations
- **Matrix Multiplication:** SUMMA, Cannon, 2.5D/3D algorithms
- **Eigenvalue Computation:** Distributed Lanczos, LOBPCG
- **All-Reduce & Collectives:** Ring, tree, butterfly topologies
- *Production Context:* 
  - Distributed matrix operations in large model training
  - Collective communication in gradient synchronization
  - Topology-aware all-reduce in GPU cluster optimization

### 10.4 Mathematical Debugging & Profiling
- **Gradient Checking:** Finite difference verification, relative error thresholds
- **Hessian Spectrum Analysis:** Eigenvalue histograms, condition number monitoring
- **Spectral Analysis of Weights:** SVD of weight matrices, rank collapse detection
- *Production Context:* 
  - Gradient checking in CI/CD for model correctness
  - Hessian spectrum in training diagnostics and instability detection
  - Weight matrix SVD in analyzing representation collapse

---

## Capstone Projects

Each student must complete **two** capstone projects: one from Category A (Implementation) and one from Category B (Systems/Infrastructure).

### Category A: Deep Implementation Projects

**A1. Geometric Deep Learning Framework**
- Implement E(n)-equivariant and SE(3)-equivariant neural network layers
- Support steerable convolutions, spherical harmonics, and Clebsch-Gordan coefficients
- Benchmark on molecular dynamics and 3D vision tasks
- **Systems Requirements:** GPU acceleration, batching, numerical stability

**A2. Neural Tangent Kernel Analysis Toolkit**
- Implement NTK computation for various architectures (MLP, CNN, Transformer)
- Support infinite-width limit analysis and finite-width corrections
- Visualize kernel spectra and training dynamics
- **Systems Requirements:** Distributed computation, memory-efficient kernel computation, visualization

**A3. Information Geometry Optimization Library**
- Implement natural gradient descent with Fisher information matrix approximation
- Support K-FAC, Shampoo, and diagonal Fisher preconditioners
- Integrate with PyTorch for large-scale training
- **Systems Requirements:** Multi-GPU support, mixed-precision, checkpointing

**A4. Spectral Graph Neural Network Framework**
- Implement spectral GNNs with Chebyshev, Cayley, and rational filters
- Support graph coarsening, pooling, and hierarchical processing
- Benchmark on molecular property prediction and social network tasks
- **Systems Requirements:** Sparse matrix operations, graph batching, GPU acceleration

### Category B: Systems & Infrastructure Projects

**B1. Mathematical Debugging Service for Deep Learning**
- Build a service for real-time numerical health monitoring of training jobs
- Implement gradient checking, Hessian spectrum analysis, and spectral monitoring
- Provide automated alerting and remediation recommendations
- **Components:** Numerical analysis, spectral methods, automated diagnostics

**B2. Equivariant Model Serving Infrastructure**
- Design serving infrastructure for equivariant neural networks
- Support group-averaged inference, symmetry-constrained outputs
- Optimize for latency and throughput in production
- **Components:** Group theory, caching, batching, optimization

**B3. Distributed NTK Computation Service**
- Build a service for computing neural tangent kernels at scale
- Support distributed kernel matrix construction and eigenvalue analysis
- Integrate with training pipelines for architecture analysis
- **Components:** Distributed linear algebra, kernel methods, spectral analysis

**B4. Mathematical Optimization Backend for AutoML**
- Design a backend for automated architecture search with theoretical guarantees
- Implement complexity-aware search (VC dimension, Rademacher bounds)
- Support multi-objective optimization (accuracy, efficiency, robustness)
- **Components:** Approximation theory, statistical learning theory, optimization

---

## Assessment & Evaluation Framework

### Formative Assessments (Continuous)
- **Weekly Problem Sets:** 3–5 theoretical and implementation problems
- **Implementation Reviews:** Code review sessions focusing on mathematical correctness and performance
- **Reading Reviews:** Analysis of seminal papers with systems relevance

### Summative Assessments (Milestone)
- **Midterm Examination:** 
  - 4-hour closed-book exam
  - Theoretical proofs (30%), algorithm design (40%), systems analysis (30%)
  - Topics: Modules 0–5

- **Final Examination:**
  - 6-hour take-home exam
  - Open-systems (access to documentation, no human collaboration)
  - Design a complete mathematical ML system from theory to production deployment
  - Topics: Modules 6–10 + integration

### Capstone Evaluation Rubric
| Criterion | Weight | Description |
|-----------|--------|-------------|
| Mathematical Rigor | 20% | Theoretical correctness, proof quality, mathematical depth |
| Implementation Quality | 25% | Code efficiency, numerical accuracy, hardware utilization |
| Systems Integration | 20% | Production readiness, fault tolerance, observability |
| Architecture Reasoning | 20% | Design decisions, trade-off analysis, theoretical grounding |
| Documentation | 15% | Technical writing, operational runbooks, mathematical exposition |

---

## Recommended Resources & Bibliography

### Core Textbooks
1. **Goodfellow, Ian, Bengio, Yoshua & Courville, Aaron.** *Deep Learning.* MIT Press, 2016. — *The canonical deep learning reference with mathematical foundations.*
2. **Bishop, Christopher M.** *Pattern Recognition and Machine Learning.* Springer, 2006. — *Comprehensive ML from probabilistic perspective.*
3. **Bronstein, Michael M. et al.** *Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, Gauges.* 2021. — *The geometric deep learning blueprint.*
4. **Mohri, Mehryar, Rostamizadeh, Afshin & Talwalkar, Ameet.** *Foundations of Machine Learning* (2nd ed.). MIT Press, 2018. — *Rigorous learning theory.*
5. **Petersen, Philipp et al.** *Mathematical Foundations of Deep Learning.* 2024. — *Modern approximation theory for neural networks.*

### Specialized Resources
6. **Ghosh, Sourangshu.** *Mathematical Foundations of Deep Learning.* IISc Bangalore, 2024. — *Rigorous treatment of NTK, approximation, optimization.*
7. **Amari, Shun-ichi.** *Information Geometry and Its Applications.* Springer, 2016. — *Information geometry foundations.*
8. **Weiler, Maurice et al.** "Equivariant and Steerable CNNs." *ICLR 2019.* — *Steerable convolutions and representation theory.*
9. **Cohen, Taco & Welling, Max.** "Group Equivariant Convolutional Networks." *ICML 2016.* — *Group CNNs foundational paper.*

### Geometric Deep Learning
10. **Cohen, Taco et al.** "Gauge Equivariant Convolutional Networks and the Icosahedral CNN." *ICML 2019.* — *Gauge equivariance on manifolds.*
11. **Fuchs, Fabian et al.** "SE(3)-Transformers: 3D Roto-Translation Equivariant Attention Networks." *NeurIPS 2020.* — *SE(3) equivariant transformers.*
12. **Bogatskiy, Alexander et al.** "Symmetry Group Equivariant Architectures for Physics." *2020.* — *Physics-inspired equivariant networks.*

### Online Resources
- **Geometric Deep Learning Book:** https://geometricdeeplearning.com/book/
- **Stanford CS229T:** Statistical Learning Theory (Percy Liang)
- **CMU 10-701/10-702:** Machine Learning, Deep Learning
- **MIT 6.036:** Introduction to Machine Learning
- **Northeastern CS7180:** Geometric Deep Learning (Robin Walters)

---

## Appendix: Production Checklist

Before deploying any mathematical ML component to production, verify:

- [ ] **Mathematical Correctness:** Proofs verified, approximations justified, edge cases handled
- [ ] **Numerical Stability:** Finite difference checks, gradient norm monitoring, NaN/Inf detection
- [ ] **Performance Benchmarked:** Roofline analysis, FLOPs utilization, memory bandwidth saturation
- [ ] **Scalability Tested:** Strong/weak scaling, communication overhead quantified
- [ ] **Generalization Verified:** Validation on held-out data, cross-domain evaluation
- [ ] **Uncertainty Quantified:** Aleatoric/epistemic uncertainty reported where relevant
- [ ] **Observability:** Mathematical health metrics, spectral monitoring, convergence tracking
- [ ] **Documentation:** API docs, theoretical behavior specification, operational runbooks

---

**End of Syllabus**

*Mathematics is not merely the language of machine learning—it is the very fabric from which intelligent systems are woven. From the linear algebra of representations to the differential geometry of manifolds, from the approximation theory of neural networks to the information geometry of optimization, mathematical depth is what separates practitioners who use tools from engineers who understand them. The mathematics you deploy today determines the capabilities, reliability, and trustworthiness of the intelligent systems that power tomorrow.*