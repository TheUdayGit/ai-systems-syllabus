## File: linear-algebra-syllabus.md

# Linear Algebra for AI Systems Engineering

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Proficiency in Python/C++; basic calculus and probability; familiarity with computer architecture and memory hierarchies  
**Estimated Duration:** 6–12 months (full-time study + production implementation)  
**Philosophy:** Theory → Implementation → Systems → Infrastructure → Production Engineering

---

## Table of Contents

1. [Module 0: Mathematical Foundations & Computational Reasoning](#module-0-mathematical-foundations--computational-reasoning)
2. [Module 1: Vector Spaces, Bases & Linear Mappings](#module-1-vector-spaces-bases--linear-mappings)
3. [Module 2: Matrix Theory & Decompositions](#module-2-matrix-theory--decompositions)
4. [Module 3: Numerical Linear Algebra & Stability](#module-3-numerical-linear-algebra--stability)
5. [Module 4: Eigenvalue Problems & Spectral Theory](#module-4-eigenvalue-problems--spectral-theory)
6. [Module 5: Optimization & Least Squares](#module-5-optimization--least-squares)
7. [Module 6: Tensor Algebra & Multilinear Maps](#module-6-tensor-algebra--multilinear-maps)
8. [Module 7: Sparse Linear Algebra & Structured Matrices](#module-7-sparse-linear-algebra--structured-matrices)
9. [Module 8: Distributed & Parallel Linear Algebra](#module-8-distributed--parallel-linear-algebra)
10. [Module 9: GPU-Accelerated Linear Algebra](#module-9-gpu-accelerated-linear-algebra)
11. [Module 10: Linear Algebra in Production AI Systems](#module-10-linear-algebra-in-production-ai-systems)
12. [Capstone Projects](#capstone-projects)
13. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
14. [Recommended Resources & Bibliography](#recommended-resources--bibliography)

---

## Module 0: Mathematical Foundations & Computational Reasoning

**Duration:** 2–3 weeks  
**Objective:** Establish the mathematical maturity and computational reasoning required for rigorous linear algebra in production AI systems. This is not a remedial math module—it is a systems-oriented treatment of the foundations that directly enable algorithmic and architectural reasoning.

### 0.1 Fields, Vector Spaces & Subspaces
- **Fields:** ℝ, ℂ, finite fields (GF(2), GF(p))—why finite fields matter in quantization and error correction
- **Vector Space Axioms:** Closure, associativity, distributivity—proving properties algorithmically
- **Subspaces:** Column space, row space, null space, left null space—the four fundamental subspaces
- **Quotient Spaces:** Abstract but essential for understanding tensor products and parallel decompositions
- *Production Context:* 
  - Embedding spaces as vector spaces over ℝ
  - Binary embeddings over GF(2) for memory efficiency
  - Subspace methods in dimensionality reduction (PCA, ICA)

### 0.2 Linear Independence, Span & Basis
- **Linear Independence:** Definition, testing via Gaussian elimination, geometric intuition
- **Span & Basis:** Minimal generating sets, dimension theorem, change of basis matrices
- **Orthogonal & Orthonormal Bases:** Gram-Schmidt process, QR factorization connection
- **Dual Spaces & Dual Bases:** Linear functionals, row vectors as covectors
- *Production Context:* 
  - Basis selection in adaptive mesh refinement for simulation
  - Feature selection as basis selection in model compression
  - Dual space interpretation of attention mechanisms

### 0.3 Linear Transformations & Matrix Representations
- **Linear Maps:** Kernel, image, rank-nullity theorem
- **Matrix Representation:** Change of basis, similarity transformations
- **Projections:** Orthogonal projections, oblique projections, projection matrices
- **Affine Transformations:** Homogeneous coordinates, translation as linear map in higher dimension
- *Production Context:* 
  - Layer transformations in neural networks as affine maps
  - Projection heads in contrastive learning (SimCLR, CLIP)
  - Attention as learned projection operators
  - Coordinate transformations in computer vision (homography)

### 0.4 Inner Product Spaces & Norms
- **Inner Products:** Definition, induced norms, Cauchy-Schwarz, triangle inequality
- **Norms:** L1, L2, L∞, Frobenius, spectral, nuclear norms
- **Orthogonality:** Orthogonal complements, orthogonal projections, Pythagorean theorem
- **Hilbert Spaces:** Completeness, infinite-dimensional spaces (brief)
- *Production Context:* 
  - L2 normalization in embeddings and retrieval
  - Spectral normalization in GANs for training stability
  - Nuclear norm regularization for low-rank matrix recovery
  - Cosine similarity as normalized inner product

### 0.5 Computational Complexity of Linear Algebra
- **Big-O for Matrix Operations:** O(n³) for naive multiplication, Strassen O(n^2.807), theoretical bounds
- **Memory Complexity:** In-place vs. out-of-place, workspace requirements
- **Flops vs. Memory Bandwidth:** Arithmetic intensity, roofline model introduction
- **Conditioning:** Well-conditioned vs. ill-conditioned problems
- *Production Context:* 
  - Choosing between dense and sparse representations based on arithmetic intensity
  - Understanding why transformers are memory-bound, not compute-bound
  - Roofline analysis for kernel optimization

---

## Module 1: Vector Spaces, Bases & Linear Mappings

**Duration:** 3–4 weeks  
**Objective:** Deep understanding of vector spaces as the foundational abstraction for all AI computation, with explicit focus on computational representation and systems implications.

### 1.1 Vector Space Axioms & Examples
- Formal definition over arbitrary fields
- Examples: ℝⁿ, function spaces, polynomial spaces, sequence spaces
- Subspace criteria and intersection/sum of subspaces
- Direct sums and complements
- *Production Context:* 
  - Function approximation in neural networks (universal approximation theorem)
  - Polynomial feature spaces in kernel methods
  - Direct sum decomposition in model parallelism

### 1.2 Bases, Dimension & Coordinates
- Existence of bases (via Zorn's lemma for infinite-dimensional)
- Dimension invariance, rank-nullity theorem
- Coordinate vectors, change of basis matrices
- Dual bases and coordinate functionals
- *Production Context:* 
  - Coordinate transformations in distributed training (data parallelism)
  - Basis adaptation in transfer learning (feature space alignment)
  - Dimensionality reduction as change of basis (PCA, SVD)

### 1.3 Linear Maps & Their Matrix Representations
- Hom(V,W) as vector space
- Composition as matrix multiplication
- Isomorphisms, automorphisms, GL(n)
- Rank, nullity, and the fundamental theorem of linear maps
- *Production Context:* 
  - Neural network layers as compositions of linear maps + nonlinearities
  - Invertibility conditions for normalizing flows
  - Automorphism groups in equivariant neural networks

### 1.4 Projections & Idempotent Operators
- Projection matrices: P² = P
- Orthogonal vs. oblique projections
- Projection onto subspaces, least squares projection
- Complementary projections and direct sum decompositions
- *Production Context:* 
  - Dropout as random projection in training
  - Projection layers in transformer architectures
  - Subspace clustering in representation learning
  - Model compression via projection onto low-rank manifolds

### 1.5 Quotient Spaces & Exact Sequences
- Quotient space construction, canonical projection
- First isomorphism theorem
- Short exact sequences, split exact sequences
- *Production Context:* 
  - Understanding distributed representations as quotient spaces
  - Exact sequences in persistent homology for topological data analysis
  - Quotient constructions in symmetry-reduced neural networks

---

## Module 2: Matrix Theory & Decompositions

**Duration:** 4–5 weeks  
**Objective:** Master matrix decompositions as the computational primitives of AI systems. Every decomposition is taught with its algorithmic implementation, numerical properties, and systems implications.

### 2.1 Gaussian Elimination & LU Decomposition
- Gaussian elimination with partial and complete pivoting
- LU decomposition: Doolittle, Crout, Cholesky variants
- Block LU decomposition for cache efficiency
- Numerical stability and growth factors
- *Production Context:* 
  - Solving linear systems in optimization (Newton's method)
  - Cholesky decomposition for covariance matrices in Gaussian processes
  - Block LU in distributed linear algebra (ScaLAPACK)
  - LU in circuit simulation and constraint solvers

### 2.2 QR Decomposition
- Gram-Schmidt (classical and modified)
- Householder reflections, Givens rotations
- Thin QR, full QR, rank-revealing QR
- Communication-avoiding QR (CAQR) for distributed systems
- *Production Context:* 
  - Orthogonalization in iterative solvers (GMRES, Arnoldi)
  - QR for least squares problems in regression
  - Householder reflections in Hessenberg reduction for eigenvalue problems
  - CAQR in large-scale distributed linear algebra on TPU pods citeweb_search:2#3

### 2.3 Singular Value Decomposition (SVD)
- Existence and uniqueness proofs
- Truncated SVD, randomized SVD
- Relationship to PCA, latent semantic analysis
- SVD for low-rank approximation (Eckart-Young-Mirsky theorem)
- *Production Context:* 
  - Model compression via low-rank factorization (LoRA, SVD-based pruning)
  - Recommendation systems (collaborative filtering)
  - Image compression and denoising
  - Latent semantic indexing in search and RAG

### 2.4 Cholesky Decomposition & Positive Definite Matrices
- Positive definite criteria: eigenvalues, principal minors, quadratic forms
- Cholesky algorithm and its stability
- Incomplete Cholesky preconditioners
- Block Cholesky for parallel execution
- *Production Context:* 
  - Gaussian process covariance matrices
  - Kalman filter implementations
  - Preconditioning in conjugate gradient methods
  - Portfolio optimization in financial AI

### 2.5 Schur Complement & Block Matrix Operations
- Schur complement formula and applications
- Block matrix inversion, Woodbury matrix identity
- Sherman-Morrison formula for rank-1 updates
- *Production Context:* 
  - Efficient Gaussian process updates with new data
  - Recursive least squares in online learning
  - Block matrix operations in distributed training
  - Low-rank updates in quasi-Newton methods (BFGS, L-BFGS)

### 2.6 Matrix Functions & Operator Theory
- Matrix exponential, logarithm, square root
- Functions via diagonalization, Jordan form, Cauchy integral
- Matrix sign function, polar decomposition
- *Production Context:* 
  - Matrix exponential in continuous-time neural networks (Neural ODEs)
  - Polar decomposition in orthogonal initialization
  - Matrix square root in whitening transformations
  - Matrix functions in quantum machine learning simulations

---

## Module 3: Numerical Linear Algebra & Stability

**Duration:** 4–5 weeks  
**Objective:** Production AI systems fail silently when numerical linear algebra is treated as a black box. This module builds the rigor to debug, optimize, and design numerically robust systems.

### 3.1 Floating-Point Arithmetic & Rounding Error Analysis
- IEEE 754 standard: formats, special values, rounding modes
- Machine epsilon, unit roundoff
- Forward error, backward error, mixed stability
- *Production Context:* 
  - Mixed-precision training (FP16/BF16/FP32)
  - Numerical stability in softmax and cross-entropy computations
  - Gradual underflow and its impact on training dynamics
  - Custom floating-point formats in quantization (INT8, INT4)

### 3.2 Conditioning & Stability of Linear Systems
- Condition number: κ(A) = ||A|| ||A⁻¹||
- Ill-conditioned systems and their geometric interpretation
- Perturbation theory: Bauer-Fike, Weyl's inequalities
- *Production Context:* 
  - Diagnosing training instability via condition number monitoring
  - Preconditioning to improve conditioning in optimization
  - Sensitivity analysis in model interpretability
  - Numerical stability in attention mechanisms (softmax scaling)

### 3.3 Direct Methods for Linear Systems
- Gaussian elimination with pivoting strategies
- LU with iterative refinement
- Cholesky for symmetric positive definite systems
- Banded, tridiagonal, and structured solvers
- *Production Context:* 
  - Sparse direct solvers in circuit simulation
  - Tridiagonal solvers in 1D diffusion models
  - Banded solvers in finite difference methods for PDEs
  - Direct solvers in real-time control systems

### 3.4 Iterative Methods for Linear Systems
- Stationary methods: Jacobi, Gauss-Seidel, SOR
- Krylov subspace methods: CG, GMRES, BiCGSTAB
- Preconditioning: Jacobi, ILU, multigrid
- Convergence analysis and stopping criteria
- *Production Context:* 
  - Large-scale optimization in deep learning (preconditioned SGD)
  - Iterative solvers in physics-informed neural networks
  - Conjugate gradient in trust-region methods
  - Preconditioned iterative methods in graph neural networks

### 3.5 Least Squares Problems
- Normal equations vs. QR approach vs. SVD approach
- Regularized least squares: Tikhonov, LASSO
- Weighted and generalized least squares
- Total least squares (errors-in-variables)
- *Production Context:* 
  - Linear regression at scale (distributed least squares)
  - Ridge regression and LASSO in feature selection
  - Robust regression via iteratively reweighted least squares
  - Total least squares in errors-in-variables models

### 3.6 Numerical Rank & Rank-Revealing Decompositions
- Numerical rank vs. algebraic rank
- Rank-revealing QR, URV decomposition
- Interpolative decomposition, CUR decomposition
- *Production Context:* 
  - Rank determination in model compression
  - CUR for interpretable matrix approximation
  - Rank-revealing decompositions in randomized algorithms
  - Numerical rank in noisy data recovery

---

## Module 4: Eigenvalue Problems & Spectral Theory

**Duration:** 4–5 weeks  
**Objective:** Spectral theory underlies PCA, spectral clustering, graph neural networks, and stability analysis. This module treats eigenvalue computation as a systems problem with numerical and distributed dimensions.

### 4.1 Eigenvalues, Eigenvectors & Eigenspaces
- Characteristic polynomial, algebraic multiplicity
- Geometric multiplicity, defective matrices
- Eigenspace decomposition, diagonalizability
- Spectral mapping theorem
- *Production Context:* 
  - Spectral analysis of attention matrices
  - Eigendecomposition in principal component analysis
  - Spectral clustering for community detection
  - Stability analysis via eigenvalue spectra

### 4.2 Similarity Transformations & Canonical Forms
- Jordan canonical form (theoretical)
- Schur decomposition, real Schur form
- Hessenberg reduction via Householder reflections
- *Production Context:* 
  - Schur form in matrix function computation
  - Hessenberg reduction as preprocessing for eigenvalue algorithms
  - Canonical forms in control theory and system identification

### 4.3 Symmetric Eigenvalue Problems
- Spectral theorem for Hermitian matrices
- Rayleigh quotient, Courant-Fischer min-max theorem
- Divide-and-conquer, MRRR algorithm
- *Production Context:* 
  - Spectral decomposition of covariance matrices
  - Rayleigh quotient iteration for refined eigenvalue estimates
  - Divide-and-conquer in parallel eigenvalue computation

### 4.4 Iterative Eigenvalue Algorithms
- Power iteration, inverse iteration, Rayleigh quotient iteration
- Subspace iteration, simultaneous iteration
- Lanczos algorithm, Arnoldi iteration
- Implicitly restarted Arnoldi/Lanczos
- *Production Context:* 
  - Power iteration in PageRank computation
  - Lanczos in large-scale PCA and spectral clustering
  - Arnoldi in eigenvalue analysis of large graphs
  - Implicit restarts for memory-constrained eigenvalue solvers

### 4.5 Generalized Eigenvalue Problems & SVD Extensions
- Generalized eigenvalue problem Ax = λBx
- Generalized SVD (GSVD)
- Polar decomposition, CS decomposition
- *Production Context:* 
  - Generalized eigenvalue problems in discriminant analysis (LDA)
  - GSVD in regularized regression
  - Polar decomposition in orthogonal Procrustes problems
  - CS decomposition in subspace intersection problems

### 4.6 Spectral Graph Theory
- Graph Laplacian: combinatorial, normalized, random walk
- Spectral clustering algorithm and analysis
- Cheeger inequality and graph conductance
- *Production Context:* 
  - Spectral clustering in community detection
  - Graph Laplacian in graph neural networks (GNNs)
  - Spectral analysis of neural network weight matrices
  - Conductance-based graph partitioning for distributed training

---

## Module 5: Optimization & Least Squares

**Duration:** 4–5 weeks  
**Objective:** Linear algebra is the engine of optimization. This module connects matrix theory to the optimization algorithms that power training, inference, and systems design.

### 5.1 Convex Sets & Convex Functions
- Convex sets, convex hulls, extreme points
- Convex functions, epigraphs, subgradients
- Strong convexity, smoothness, Lipschitz continuity
- *Production Context:* 
  - Convex optimization in training linear models
  - Strong convexity and convergence rates in SGD
  - Lipschitz constraints in Wasserstein GANs
  - Convex relaxations in combinatorial optimization

### 5.2 Gradient Descent & Its Variants
- Gradient descent: convergence analysis for convex and strongly convex
- Momentum, Nesterov acceleration
- Stochastic gradient descent (SGD): variance analysis, mini-batch trade-offs
- *Production Context:* 
  - SGD with momentum in PyTorch/TensorFlow
  - Nesterov acceleration in training large language models
  - Mini-batch size selection for memory-compute trade-offs
  - Variance reduction techniques (SVRG, SAGA)

### 5.3 Second-Order Methods
- Newton's method, convergence analysis
- Quasi-Newton methods: BFGS, L-BFGS, SR1
- Trust-region methods, dogleg method
- Gauss-Newton, Levenberg-Marquardt
- *Production Context:* 
  - L-BFGS in full-batch training of small models
  - Gauss-Newton in neural network training (natural gradient)
  - Trust-region methods in reinforcement learning policy optimization
  - Second-order methods in meta-learning

### 5.4 Constrained Optimization
- Lagrange multipliers, KKT conditions
- Duality: weak and strong, Slater's condition
- Primal-dual methods, barrier methods, penalty methods
- Projected gradient descent, Frank-Wolfe algorithm
- *Production Context:* 
  - Constrained optimization in resource allocation
  - Duality in adversarial training (GANs)
  - Projected gradient descent for norm constraints
  - Frank-Wolfe for structured sparsity in model pruning

### 5.5 Linear Programming & Simplex Method
- Standard form, basic feasible solutions
- Simplex algorithm, tableau method
- Interior point methods, barrier methods
- Duality in linear programming
- *Production Context:* 
  - Linear programming in optimal transport
  - Simplex method in assignment problems
  - Interior point methods in portfolio optimization
  - LP relaxations in integer programming for neural architecture search

### 5.6 Matrix Manifolds & Optimization on Manifolds
- Stiefel manifold, Grassmann manifold
- Riemannian gradient, exponential map, retraction
- Optimization algorithms on manifolds
- *Production Context:* 
  - Orthogonal constraints in recurrent networks
  - Low-rank optimization on Grassmann manifold
  - Riemannian optimization in metric learning
  - Manifold optimization in subspace tracking

---

## Module 6: Tensor Algebra & Multilinear Maps

**Duration:** 4–5 weeks  
**Objective:** Tensors are the native data structures of deep learning. This module treats tensor algebra rigorously, from multilinear maps to tensor decompositions and their implementation on modern hardware.

### 6.1 Tensor Products & Multilinear Maps
- Multilinear maps, universal property of tensor product
- Tensor product of vector spaces, bases for tensor products
- Tensor product of linear maps (Kronecker product)
- Tensor contractions, Einstein summation convention
- *Production Context:* 
  - Tensor contractions in einsum operations (PyTorch/TensorFlow)
  - Kronecker products in separable convolutions
  - Multilinear maps in higher-order neural networks
  - Tensor network contractions in quantum computing simulations

### 6.2 Tensor Decompositions
- CP decomposition (CANDECOMP/PARAFAC)
- Tucker decomposition, higher-order SVD (HOSVD)
- Tensor train (TT) decomposition, matrix product states
- Hierarchical Tucker decomposition
- *Production Context:* 
  - Tensor decomposition for neural network compression
  - TT decomposition for efficient attention computation
  - Tucker decomposition in tensor completion problems
  - Tensor train in quantum chemistry simulations

### 6.3 Tensor Contractions & Einstein Summation
- Einstein notation, index raising/lowering
- Contraction optimization, optimal contraction order
- Tensor network diagrams
- *Production Context:* 
  - Optimal einsum path finding in NumPy/PyTorch
  - Tensor network contractions in transformer layers
  - Contraction order optimization in automatic differentiation
  - Tensor networks in quantum machine learning

### 6.4 Tensor Operations on Modern Hardware
- Blocked tensor operations, loop tiling
- Tensor cores and mixed-precision computation
- Distributed tensor contractions (SUMMA for tensors)
- *Production Context:* 
  - Tensor core utilization in NVIDIA GPUs (WMMA, MMA)
  - Blocked tensor operations in CUTLASS
  - Distributed tensor contractions in TPU pods citeweb_search:2#3
  - Tensor parallelism in large model training (Megatron-LM)

### 6.5 Symmetric & Antisymmetric Tensors
- Symmetric tensors, symmetric tensor decomposition
- Antisymmetric tensors, exterior algebra, wedge product
- Applications in invariant theory
- *Production Context:* 
  - Symmetric tensors in moment-based methods
  - Antisymmetric tensors in fermionic neural networks
  - Exterior algebra in differential geometry for robotics
  - Symmetric tensor decomposition in blind source separation

---

## Module 7: Sparse Linear Algebra & Structured Matrices

**Duration:** 3–4 weeks  
**Objective:** Production AI systems routinely encounter sparsity—sparse gradients, sparse attention, sparse features. This module covers the algorithms and data structures for exploiting sparsity.

### 7.1 Sparse Matrix Representations
- Coordinate (COO), Compressed Sparse Row (CSR), Compressed Sparse Column (CSC)
- Block sparse formats, diagonal formats (DIA), ELLPACK
- Hybrid formats (HYB), specialized formats for GPUs
- *Production Context:* 
  - CSR/CSC in scipy.sparse, cuSPARSE
  - Block sparse formats in sparse attention (Longformer, BigBird)
  - ELLPACK in GPU graph neural networks
  - Sparse embedding tables in recommendation systems

### 7.2 Sparse Matrix-Vector & Matrix-Matrix Operations
- SpMV, SpMM algorithms and their complexity
- Cache-friendly SpMV implementations
- Sparse-dense matrix multiplication (SpMM)
- *Production Context:* 
  - SpMV in graph neural network message passing
  - SpMM in sparse transformer layers
  - Sparse-dense multiplication in pruned neural networks
  - Sparse operations in cuSPARSE and cuSPARSELt citeweb_search:2#5

### 7.3 Sparse Direct Solvers
- Sparse LU, Cholesky with fill-reducing orderings
- Minimum degree, nested dissection, METIS
- Supernodal and multifrontal methods
- *Production Context:* 
  - Sparse Cholesky in Gaussian process regression
  - Nested dissection in finite element analysis
  - Sparse solvers in circuit simulation
  - Fill-reducing orderings in sparse matrix factorization

### 7.4 Structured Matrices & Fast Transforms
- Toeplitz, Hankel, circulant matrices
- Fast Fourier Transform (FFT) and its matrix interpretation
- Fast multipole method (FMM) overview
- *Production Context:* 
  - Circulant matrices in convolutional layers
  - FFT-based convolution acceleration
  - Toeplitz structure in time-series analysis
  - FMM in N-body problems for physics-informed ML

### 7.5 Randomized Numerical Linear Algebra
- Randomized SVD, randomized range finder
- Sketching techniques, Count-Sketch, sparse Johnson-Lindenstrauss
- Randomized least squares, preconditioning
- *Production Context:* 
  - Randomized SVD for large-scale PCA
  - Sketching in streaming data analysis
  - Randomized preconditioning in distributed optimization
  - Approximate matrix multiplication in federated learning

---

## Module 8: Distributed & Parallel Linear Algebra

**Duration:** 4–5 weeks  
**Objective:** Modern AI models exceed single-device memory. This module covers the linear algebra of distributed systems—how to decompose, communicate, and synchronize matrix operations across clusters.

### 8.1 Data Distribution & Layout
- 1D block, 1D cyclic, 2D block-cyclic distributions
- ScaLAPACK conventions, processor grids
- Memory mapping and alignment for NUMA systems
- *Production Context:* 
  - Data parallelism in distributed training
  - 2D block-cyclic distribution in ScaLAPACK
  - Tensor sharding in model parallelism (Megatron, DeepSpeed)
  - NUMA-aware data placement in multi-socket servers

### 8.2 Distributed Matrix Multiplication
- Cannon's algorithm, SUMMA algorithm
- 2.5D and 3D algorithms for memory-compute trade-offs
- Communication lower bounds (Irony-Tiskin-Toledo)
- *Production Context:* 
  - SUMMA in TPU pod matrix multiplication citeweb_search:2#3
  - Cannon's algorithm in GPU all-reduce implementations
  - Communication-avoiding algorithms in large-scale training
  - 2.5D algorithms for memory-limited clusters

### 8.3 Collective Communication Patterns
- Broadcast, reduce, all-reduce, all-gather, reduce-scatter
- Ring all-reduce, tree all-reduce, butterfly mixing
- Bandwidth-optimal algorithms, latency hiding
- *Production Context:* 
  - Ring all-reduce in Horovod, DeepSpeed
  - Tree all-reduce in NCCL
  - Collective communication in parameter servers
  - Bandwidth optimization in multi-node training

### 8.4 Distributed Factorizations
- Distributed LU, QR, Cholesky
- TSQR (Tall-Skinny QR) for distributed QR
- CAQR (Communication-Avoiding QR)
- *Production Context:* 
  - TSQR in distributed orthogonalization
  - CAQR in large-scale least squares problems
  - Distributed Cholesky in Gaussian process training
  - QR factorization in TPU pods citeweb_search:2#3

### 8.5 Fault Tolerance & Checkpointing
- Algorithm-based fault tolerance (ABFT)
- Checkpointing strategies for long-running factorizations
- Recomputation vs. checkpoint trade-offs
- *Production Context:* 
  - ABFT in large-scale matrix operations
  - Checkpointing in distributed training jobs
  - Fault-tolerant gradient aggregation
  - Recovery protocols in MPI-based linear algebra

### 8.6 Mixed-Precision & Approximate Distributed Algorithms
- Mixed-precision iterative refinement
- Stochastic rounding in distributed aggregation
- Lossy compression for gradient communication
- *Production Context:* 
  - Mixed-precision training (FP16/BF16 master weights)
  - Gradient compression (Top-K, signSGD, quantization)
  - Stochastic rounding in low-precision communication
  - Approximate algorithms for bandwidth-limited clusters

---

## Module 9: GPU-Accelerated Linear Algebra

**Duration:** 4–5 weeks  
**Objective:** GPUs are the dominant compute substrate for AI. This module covers the architecture, programming models, and optimization techniques for GPU linear algebra, from BLAS kernels to custom CUDA implementations.

### 9.1 GPU Architecture & Memory Hierarchy
- CUDA core architecture, warp scheduling, SIMT execution
- Memory hierarchy: registers, shared memory, L1/L2 cache, global memory, HBM
- Memory coalescing, bank conflicts, occupancy
- *Production Context:* 
  - Understanding GPU memory bandwidth (A100: 2 TB/s) vs. CPU bandwidth citeweb_search:2#1
  - Memory coalescing in matrix multiplication kernels
  - Shared memory optimization in convolution implementations
  - Occupancy tuning for kernel performance

### 9.2 CUDA Programming for Linear Algebra
- Kernel launch, grid/block/thread hierarchy
- Shared memory programming, tiling, thread coarsening
- Warp shuffle operations, cooperative groups
- CUDA streams, asynchronous execution
- *Production Context:* 
  - Custom CUDA kernels for attention mechanisms
  - Shared memory tiling in matrix multiplication
  - Warp-level primitives in reduction operations
  - Stream parallelism in multi-GPU training

### 9.3 cuBLAS, cuSPARSE & CUTLASS
- cuBLAS levels 1, 2, 3: API design, performance characteristics
- cuSPARSE: sparse matrix operations on GPU
- CUTLASS: customizable GEMM templates, warp-level GEMM
- *Production Context:* 
  - cuBLAS GEMM optimization in deep learning frameworks
  - cuSPARSE for sparse attention and GNNs citeweb_search:2#5
  - CUTLASS for custom fused kernels (flash attention)
  - Mixed-precision GEMM in tensor cores

### 9.4 Tensor Cores & Mixed-Precision
- Tensor core architecture: WMMA, MMA PTX instructions
- FP16, BF16, TF32, INT8 precision modes
- Automatic mixed precision (AMP) training
- *Production Context:* 
  - Tensor core utilization in transformer training
  - AMP in PyTorch/TensorFlow
  - INT8 tensor core inference acceleration
  - Numerical stability in mixed-precision training

### 9.5 Multi-GPU & Distributed GPU Linear Algebra
- NVLink, NVSwitch topology
- NCCL library design and performance
- GPU-aware MPI, CUDA-aware communication
- *Production Context:* 
  - NVLink topology-aware job scheduling
  - NCCL all-reduce in distributed training
  - GPU-aware MPI in scientific computing
  - Multi-GPU linear algebra in large model training

### 9.6 Profiling & Optimization
- NVIDIA Nsight Compute, Nsight Systems
- Roofline analysis on GPU
- Memory bandwidth vs. compute bottlenecks
- *Production Context:* 
  - Profiling custom kernels with Nsight Compute
  - Roofline analysis for kernel optimization
  - Identifying memory bandwidth bottlenecks in attention
  - Compute vs. memory-bound operation classification

---

## Module 10: Linear Algebra in Production AI Systems

**Duration:** 4–5 weeks  
**Objective:** Bridge the gap between linear algebra theory and production AI infrastructure. This module focuses on the operational aspects of linear algebra systems.

### 10.1 Matrix Operations in Deep Learning Frameworks
- Computation graph representation of linear algebra
- Automatic differentiation via Jacobian-vector products
- Memory planning and buffer reuse
- *Production Context:* 
  - PyTorch autograd engine internals
  - TensorFlow/XLA compilation of linear algebra
  - Memory optimization in transformer training
  - Gradient checkpointing and recomputation

### 10.2 Linear Algebra in Model Serving
- Batch matrix operations in inference
- Dynamic batching and padding strategies
- Kernel fusion and operator optimization
- *Production Context:* 
  - Batched GEMM in inference servers
  - Dynamic batching in Triton Inference Server
  - Kernel fusion in ONNX Runtime/TensorRT
  - Operator optimization in TVM/MLIR

### 10.3 Numerical Stability in Production
- Detecting and mitigating numerical instability
- Gradient clipping, loss scaling
- Condition number monitoring
- *Production Context:* 
  - Loss scaling in mixed-precision training
  - Gradient clipping in transformer training
  - Numerical stability in attention softmax
  - Monitoring condition numbers in production pipelines

### 10.4 Performance Engineering & Benchmarking
- Microbenchmarking matrix operations
- End-to-end pipeline profiling
- Bottleneck identification and mitigation
- *Production Context:* 
  - Benchmarking GEMM performance across hardware
  - Profiling end-to-end training steps
  - Identifying communication bottlenecks in distributed training
  - Performance regression detection in CI/CD

### 10.5 Debugging Linear Algebra Systems
- Reproducibility in parallel linear algebra
- Debugging non-deterministic reductions
- Numerical debugging tools and techniques
- *Production Context:* 
  - Deterministic reductions in distributed training
  - Debugging NaN/Inf in training
  - Numerical debugging with finite difference checks
  - Reproducibility in model training pipelines

### 10.6 Scalability & Efficiency Analysis
- Strong scaling vs. weak scaling for linear algebra operations
- Communication-computation ratios
- Roofline model for distributed systems
- *Production Context:* 
  - Scaling analysis for data parallelism
  - Pipeline parallelism efficiency bounds
  - Communication overhead in model parallelism
  - Optimal cluster sizing for training workloads

---

## Capstone Projects

Each student must complete **two** capstone projects: one from Category A (Implementation) and one from Category B (Systems/Infrastructure).

### Category A: Deep Implementation Projects

**A1. Production-Grade Distributed Matrix Multiplication Framework**
- Implement SUMMA, Cannon's, and 3D matrix multiplication algorithms
- Support 2D block-cyclic data distribution
- Integrate with MPI for multi-node execution
- Benchmark against ScaLAPACK, analyze communication-computation trade-offs
- **Systems Requirements:** Fault tolerance, dynamic grid resizing, mixed-precision support

**A2. GPU-Accelerated Sparse Linear Algebra Library**
- Implement CSR/COO SpMV and SpMM kernels in CUDA
- Support mixed-precision computation (FP16/FP32)
- Integrate with cuSPARSE for validation
- Optimize for memory coalescing and shared memory usage
- **Systems Requirements:** Multi-GPU support, stream parallelism, memory pool management

**A3. Randomized SVD for Large-Scale Model Compression**
- Implement randomized range finder with power iteration
- Support streaming updates for online compression
- Integrate with PyTorch for layer-wise compression
- Benchmark compression ratio vs. accuracy trade-offs on LLMs
- **Systems Requirements:** Memory-efficient implementation, checkpointing, distributed execution

**A4. Numerical Optimization Solver for Deep Learning**
- Implement L-BFGS with line search and trust-region variants
- Support constrained optimization (projected gradient, Frank-Wolfe)
- Integrate with PyTorch autograd
- Benchmark against Adam/AdamW on standard tasks
- **Systems Requirements:** Distributed support, checkpointing, convergence monitoring

### Category B: Systems & Infrastructure Projects

**B1. Mixed-Precision Training Infrastructure**
- Design and implement a mixed-precision training framework
- Support FP16/BF16/FP32 with automatic loss scaling
- Integrate gradient compression (Top-K, signSGD)
- Implement numerical stability monitoring and alerting
- **Linear Algebra Components:** Condition number tracking, iterative refinement, error analysis

**B2. Distributed Eigenvalue Solver for Graph Neural Networks**
- Build a distributed Lanczos/Arnoldi solver for large graph Laplacians
- Support spectral clustering at billion-node scale
- Implement checkpointing and fault tolerance
- Integrate with PyTorch Geometric Distributed
- **Linear Algebra Components:** Sparse matrix operations, orthogonalization, convergence criteria

**B3. Linear Algebra Backend for Inference Serving**
- Design a high-performance linear algebra backend for model serving
- Support batched operations, dynamic shapes, kernel fusion
- Implement operator scheduling and memory planning
- Integrate with ONNX Runtime or custom serving framework
- **Linear Algebra Components:** Batched GEMM, tensor contractions, memory optimization

**B4. Numerical Stability Monitoring System**
- Build a production monitoring system for numerical health of training runs
- Track gradient norms, condition numbers, eigenvalue spectra
- Implement automated alerting for instability detection
- Provide debugging recommendations based on linear algebra diagnostics
- **Linear Algebra Components:** Spectral analysis, condition estimation, perturbation theory

---

## Assessment & Evaluation Framework

### Formative Assessments (Continuous)
- **Weekly Problem Sets:** 3–5 theoretical and implementation problems
- **Implementation Reviews:** Code review sessions focusing on numerical stability, performance, and correctness
- **Reading Reviews:** Analysis of seminal papers with systems relevance

### Summative Assessments (Milestone)
- **Midterm Examination:** 
  - 4-hour closed-book exam
  - Theoretical proofs (30%), algorithm design (40%), systems analysis (30%)
  - Topics: Modules 0–5

- **Final Examination:**
  - 6-hour take-home exam
  - Open-systems (access to documentation, no human collaboration)
  - Design a complete linear algebra system from theory to production deployment
  - Topics: Modules 6–10 + integration

### Capstone Evaluation Rubric
| Criterion | Weight | Description |
|-----------|--------|-------------|
| Correctness | 20% | Mathematical correctness, numerical stability, edge case handling |
| Performance | 25% | Asymptotic and empirical efficiency, hardware utilization |
| Systems Integration | 20% | Production readiness, fault tolerance, observability |
| Architecture Reasoning | 20% | Design decisions, trade-off analysis, scalability considerations |
| Documentation | 15% | Technical writing, operational runbooks, mathematical rigor |

---

## Recommended Resources & Bibliography

### Core Textbooks
1. **Strang, Gilbert.** *Linear Algebra and Learning from Data.* Wellesley-Cambridge Press, 2019. — *The essential bridge between linear algebra and machine learning.*
2. **Golub, Gene H. & Van Loan, Charles F.** *Matrix Computations* (4th ed.). Johns Hopkins University Press, 2013. — *The definitive reference for numerical linear algebra.*
3. **Trefethen, Lloyd N. & Bau, David III.** *Numerical Linear Algebra.* SIAM, 1997. — *Concise, rigorous, and focused on algorithms.*
4. **Horn, Roger A. & Johnson, Charles R.** *Matrix Analysis* (2nd ed.). Cambridge University Press, 2012. — *Comprehensive theoretical treatment.*
5. **Axler, Sheldon.** *Linear Algebra Done Right* (3rd ed.). Springer, 2015. — *Rigorous foundation with minimal determinant dependence.*

### Specialized Resources
6. **Saad, Yousef.** *Iterative Methods for Sparse Linear Systems* (2nd ed.). SIAM, 2003. — *The canonical text for sparse solvers.*
7. **Hackbusch, Wolfgang.** *Tensor Spaces and Numerical Tensor Calculus.* Springer, 2012. — *Rigorous treatment of tensor algebra.*
8. **Demmel, James W.** *Applied Numerical Linear Algebra.* SIAM, 1997. — *Parallel and high-performance linear algebra.*
9. **Ballard, Grey et al.** "Communication lower bounds and optimal algorithms for numerical linear algebra." *Acta Numerica*, 2014. — *Essential for distributed linear algebra.*

### Systems & AI Infrastructure
10. **NVIDIA CUDA Documentation.** *CUDA C++ Programming Guide, cuBLAS Library, cuSPARSE Library.* — *Essential for GPU linear algebra implementation.*
11. **Rajbhandari, Samyam et al.** "ZeRO: Memory Optimizations Toward Training Trillion Parameter Models." *SC 2020.* — *Memory-efficient distributed training.*
12. **Narayanan, Deepak et al.** "Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM." *SC 2021.* — *Tensor parallelism and distributed linear algebra.*
13. **FAMLIES Working Group.** "A Proposed Framework for Advanced (Multi)Linear Infrastructure in Engineering and Science." *arXiv:2604.07311, 2026.* — *Modern tensor infrastructure framework.* citeweb_search:2#4

### Online Resources
- **MIT 18.06, 18.065:** Linear Algebra, Matrix Methods in Data Analysis
- **Stanford EE263, EE364A:** Introduction to Linear Dynamical Systems, Convex Optimization
- **CMU 10-701, 15-712:** Machine Learning, Distributed Systems
- **NVIDIA Deep Learning Institute:** GPU-accelerated computing courses

---

## Appendix: Production Checklist

Before deploying any linear algebra component to production, verify:

- [ ] **Numerical Correctness:** Verified against reference implementations, property-based tests for algebraic laws
- [ ] **Stability:** Condition number analysis, backward error analysis, mixed-precision validation
- [ ] **Performance:** Benchmarked against vendor libraries (MKL, cuBLAS), roofline analysis completed
- [ ] **Memory Safety:** No unbounded allocations, workspace size validation, OOM handling
- [ ] **Scalability:** Tested on target hardware configuration, strong/weak scaling analysis
- [ ] **Fault Tolerance:** Checkpointing for long-running operations, graceful degradation
- [ ] **Observability:** Numerical health metrics, performance counters, error tracking
- [ ] **Documentation:** API documentation, numerical behavior specification, operational runbooks

---

**End of Syllabus**

*Linear algebra is not merely the language of AI—it is the computational fabric upon which all intelligent systems are woven. Mastery of linear algebra at the systems level is the difference between building models that work in notebooks and building infrastructure that powers intelligent systems at planetary scale.*