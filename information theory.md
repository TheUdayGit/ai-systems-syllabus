## File: information-theory-scientific-computing-syllabus.md

# Information Theory & Scientific Computing for AI Systems Engineering

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Proficiency in Python/C++; solid calculus, linear algebra, and probability; familiarity with numerical computing and optimization  
**Estimated Duration:** 6–12 months (full-time study + production implementation)  
**Philosophy:** Theory → Implementation → Systems → Infrastructure → Production Engineering

---

## Table of Contents

1. [Module 0: Mathematical Foundations & Discrete Structures](#module-0-mathematical-foundations--discrete-structures)
2. [Module 1: Entropy, Information Measures & Source Coding](#module-1-entropy-information-measures--source-coding)
3. [Module 2: Channel Capacity, Coding Theory & Error Correction](#module-2-channel-capacity-coding-theory--error-correction)
4. [Module 3: Rate-Distortion Theory & Lossy Compression](#module-3-rate-distortion-theory--lossy-compression)
5. [Module 4: Information Theory in Machine Learning](#module-4-information-theory-in-machine-learning)
6. [Module 5: Numerical Linear Algebra for Scientific Computing](#module-5-numerical-linear-algebra-for-scientific-computing)
7. [Module 6: Numerical Methods for Differential Equations](#module-6-numerical-methods-for-differential-equations)
8. [Module 7: Physics-Informed Machine Learning (SciML)](#module-7-physics-informed-machine-learning-sciml)
9. [Module 8: High-Performance Scientific Computing](#module-8-high-performance-scientific-computing)
10. [Module 9: Mixed-Precision, Stochastic & Randomized Algorithms](#module-9-mixed-precision-stochastic--randomized-algorithms)
11. [Module 10: Production Scientific Computing & Information Systems](#module-10-production-scientific-computing--information-systems)
12. [Capstone Projects](#capstone-projects)
13. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
14. [Recommended Resources & Bibliography](#recommended-resources--bibliography)

---

## Module 0: Mathematical Foundations & Discrete Structures

**Duration:** 2–3 weeks  
**Objective:** Establish rigorous mathematical foundations for information theory and scientific computing. This module builds the combinatorial, probabilistic, and analytical substrate required for all subsequent modules.

### 0.1 Combinatorics & Counting Arguments
- **Counting Principles:** Permutations, combinations, Stirling's approximation
- **Generating Functions:** Ordinary, exponential, probability generating functions
- **Asymptotic Analysis:** Growth rates, Landau notation, dominant balance
- *Production Context:* 
  - Combinatorial optimization in neural architecture search
  - Counting arguments in coding theory (codebook sizes, sphere packing)
  - Asymptotic analysis in algorithmic complexity of compression schemes

### 0.2 Probability on Discrete & Continuous Spaces
- **Probability Spaces:** Discrete, continuous, mixed distributions
- **Random Variables:** Expectation, variance, moments, cumulants
- **Convergence:** Law of large numbers, central limit theorem, large deviations
- *Production Context:* 
  - Probabilistic analysis of hashing and sketching algorithms
  - Large deviation bounds in streaming data processing
  - CLT in distributed gradient aggregation variance analysis

### 0.3 Convex Analysis & Optimization Foundations
- **Convex Functions:** Definition, epigraph, Jensen's inequality
- **Duality:** Lagrangian, Fenchel conjugate, saddle points
- **Information Geometry:** Fisher metric, natural gradient, exponential families
- *Production Context:* 
  - Convex optimization in rate-distortion problems
  - Information geometry in natural gradient descent
  - Duality in variational inference and channel capacity

### 0.4 Discrete Mathematics for Coding
- **Finite Fields:** GF(2), GF(p^m), field extensions, primitive elements
- **Polynomial Rings:** Irreducible polynomials, cyclotomic polynomials
- **Graph Theory:** Adjacency, Laplacian, expanders, coding graphs
- *Production Context:* 
  - Finite fields in Reed-Solomon and BCH error-correcting codes
  - Polynomial rings in algebraic coding theory
  - Expander graphs in LDPC code design

---

## Module 1: Entropy, Information Measures & Source Coding

**Duration:** 3–4 weeks  
**Objective:** Master Shannon's information theory from first principles, with explicit focus on production data compression, model compression, and communication-efficient distributed systems.

### 1.1 Entropy & Axiomatic Foundations
- **Shannon Entropy:** Axiomatic derivation, uniqueness theorem, binary entropy
- **Joint & Conditional Entropy:** Chain rule, subadditivity, conditioning reduces entropy
- **Relative Entropy (KL Divergence):** Definition, properties, Pinsker's inequality
- **Mutual Information:** Definition, chain rule, data processing inequality
- *Production Context:* 
  - Cross-entropy loss as the fundamental training objective in classification
  - KL divergence in variational autoencoders (VAEs) and Bayesian inference
  - Mutual information in InfoNCE contrastive learning and representation learning

### 1.2 Asymptotic Equipartition Property (AEP)
- **Typical Sequences:** Definition, probability, cardinality of typical set
- **Source Coding Theorem:** Achievability, converse, Shannon's first theorem
- **Entropy Rate:** Stationary processes, Markov sources, Lempel-Ziv universality
- *Production Context:* 
  - Typical set in large language model vocabulary analysis
  - Entropy rate in text compression and tokenization efficiency
  - AEP in analyzing long-context dependencies in transformers

### 1.3 Lossless Source Coding
- **Kraft-McMillan Inequality:** Prefix codes, uniquely decodable codes
- **Huffman Coding:** Optimal prefix codes, greedy algorithm, extensions
- **Arithmetic Coding:** Interval subdivision, precision, adaptive coding
- **Lempel-Ziv Algorithms:** LZ77, LZ78, sliding window, dictionary-based
- *Production Context:* 
  - Huffman coding in model weight quantization (INT8/INT4 compression)
  - Arithmetic coding in entropy-coded model checkpoints
  - Lempel-Ziv in log compression and data deduplication pipelines

### 1.4 Universal & Adaptive Coding
- **Universal Codes:** Elias codes, universal portfolios, online learning
- **Context Tree Weighting:** Bayesian mixing, redundancy bounds
- **Burrows-Wheeler Transform:** BWT, move-to-front, compression pipeline
- *Production Context:* 
  - Universal coding in adaptive model compression
  - BWT in bioinformatics sequence compression
  - Context mixing in high-entropy data compression

---

## Module 2: Channel Capacity, Coding Theory & Error Correction

**Duration:** 4–5 weeks  
**Objective:** Channel coding theory underlies reliable communication in distributed training, storage systems, and fault-tolerant AI infrastructure. This module covers theory and implementation.

### 2.1 Channel Models & Capacity
- **Discrete Memoryless Channels (DMC):** Transition matrices, symmetric channels
- **Channel Capacity:** Definition, computation, Blahut-Arimoto algorithm
- **Noisy Channel Coding Theorem:** Shannon's second theorem, random coding exponent
- **Gaussian Channel:** AWGN capacity, water-filling, power allocation
- *Production Context:* 
  - Channel capacity in distributed training bandwidth optimization
  - Water-filling in gradient compression bit allocation across layers
  - Gaussian channel models in analog gradient aggregation

### 2.2 Linear Block Codes
- **Generator & Parity-Check Matrices:** Systematic form, encoding, syndrome decoding
- **Hamming Codes:** Perfect codes, decoding, error correction capability
- **Cyclic Codes:** Generator polynomials, shift registers, BCH codes
- *Production Context:* 
  - Hamming codes in ECC memory for GPU HBM error correction
  - Cyclic codes in RAID storage systems for data protection
  - Syndrome decoding in hash-based data integrity verification

### 2.3 Reed-Solomon & Algebraic Codes
- **Reed-Solomon Codes:** MDS property, Berlekamp-Massey decoding, FFT-based encoding
- **List Decoding:** Sudan algorithm, Guruswami-Sudan, Johnson bound
- **Algebraic Geometry Codes:** Goppa codes, asymptotic bounds, Tsfasman-Vladut-Zink
- *Production Context:* 
  - Reed-Solomon in distributed storage (erasure coding in Ceph, HDFS)
  - List decoding in robust distributed gradient aggregation
  - AG codes in long-blocklength error correction for satellite communication

### 2.4 Convolutional & Turbo Codes
- **Convolutional Codes:** Trellis representation, Viterbi decoding, BCJR algorithm
- **Turbo Codes:** Parallel concatenation, iterative decoding, extrinsic information
- **LDPC Codes:** Tanner graphs, belief propagation, density evolution
- *Production Context:* 
  - Turbo codes in high-reliability communication links
  - LDPC in SSD controllers and flash memory error correction
  - Iterative decoding in belief propagation for graphical models

### 2.5 Polar Codes & Modern Coding
- **Polarization:** Channel polarization, Bhattacharyya parameter, synthetic channels
- **Successive Cancellation Decoding:** SC, SC-list, CRC-aided decoding
- **Fountain Codes:** LT codes, Raptor codes, rateless coding
- *Production Context:* 
  - Polar codes in 5G NR control channel encoding
  - Fountain codes in scalable video streaming
  - Rateless codes in distributed data repair and multicast

---

## Module 3: Rate-Distortion Theory & Lossy Compression

**Duration:** 3–4 weeks **Objective:** Rate-distortion theory provides the fundamental limits of lossy compression, directly applicable to model quantization, embedding compression, and neural network pruning.

### 3.1 Rate-Distortion Function
- **Definition & Properties:** Convexity, monotonicity, Shannon lower bound
- **Blahut-Arimoto Algorithm:** Computation for discrete sources, convergence
- **Gaussian Source:** R(D) = ½ log(σ²/D), reverse water-filling
- *Production Context:* 
  - Rate-distortion in neural network quantization (optimal bit allocation)
  - Reverse water-filling in per-layer quantization sensitivity analysis
  - R(D) computation in model compression budget allocation

### 3.2 Vector Quantization & Clustering
- **Lloyd-Max Quantization:** Optimal scalar quantizer, Lloyd's algorithm
- **K-Means as VQ:** Linde-Buzo-Gray (LBG) algorithm, splitting
- **Tree-Structured VQ:** Hierarchical clustering, fast search
- *Production Context:* 
  - Vector quantization in embedding table compression (product quantization)
  - K-means in model weight clustering for quantization
  - Tree-structured VQ in fast nearest neighbor search

### 3.3 Transform Coding
- **Karhunen-Loève Transform:** Optimal decorrelation, eigenvector basis
- **Discrete Cosine Transform (DCT):** JPEG, energy compaction, fast algorithms
- **Wavelet Transforms:** Multiresolution analysis, subband coding, JPEG 2000
- *Production Context:* 
  - DCT in image preprocessing for vision models
  - Wavelet transforms in multi-resolution model compression
  - KLT in PCA-based dimensionality reduction for embeddings

### 3.4 Model Compression via Information Theory
- **Weight Quantization:** Uniform, non-uniform, learned quantization
- **Pruning as Rate-Distortion:** Optimal pruning under distortion constraints
- **Knowledge Distillation:** Teacher-student as rate-distortion with side information
- *Production Context:* 
  - INT8/INT4 quantization in TensorRT and ONNX Runtime
  - Structured pruning in mobile model deployment
  - Knowledge distillation in model compression pipelines

---

## Module 4: Information Theory in Machine Learning

**Duration:** 4–5 weeks  
**Objective:** Information-theoretic principles increasingly drive ML algorithm design. This module covers the theoretical foundations and production implementations.

### 4.1 Information Bottleneck & Deep Learning
- **Information Bottleneck Principle:** Compression vs. prediction trade-off
- **IB in Neural Networks:** Tishby's analysis, phase transitions, representation compression
- **VIB (Variational Information Bottleneck):** Variational approximation, applications
- *Production Context:* 
  - Information bottleneck in understanding deep learning generalization
  - VIB in variational representation learning
  - Compression-prediction trade-off in autoencoder design

### 4.2 Minimum Description Length (MDL)
- **Two-Part Codes:** Model description + data given model
- **Normalized Maximum Likelihood:** NML, regret, stochastic complexity
- **MDL in Model Selection:** Architecture search, hyperparameter selection
- *Production Context:* 
  - MDL in neural architecture search (NAS)
  - Model selection based on description length complexity
  - MDL-based regularization in overparameterized models

### 4.3 PAC-Bayes & Information-Theoretic Generalization
- **PAC-Bayes Bounds:** KL divergence prior-posterior, McAllester's bound
- **Information-Theoretic Bounds:** Xu-Raginsky bounds, mutual information bounds
- **Flat Minima & Generalization:** PAC-Bayes interpretation of sharpness-aware minimization
- *Production Context:* 
  - PAC-Bayes bounds in neural network generalization theory
  - Information-theoretic bounds in algorithm stability analysis
  - SAM (Sharpness-Aware Minimization) via PAC-Bayes lens

### 4.4 Differential Privacy & Information Leakage
- **Differential Privacy:** Definition, mechanisms, composition
- **Privacy-Utility Trade-off:** Rate-distortion with privacy constraints
- **Federated Learning Privacy:** Secure aggregation, local DP, shuffled model
- *Production Context:* 
  - DP-SGD in privacy-preserving training
  - Privacy budget allocation across training iterations
  - Secure aggregation in cross-device federated learning

### 4.5 Coding Theory in Distributed Learning
- **Gradient Compression:** Top-K, signSGD, quantization as source coding
- **Error Feedback:** Coded computation, gradient coding, straggler mitigation
- **Communication-Efficient Optimization:** Coded gradient descent, federated averaging
- *Production Context:* 
  - Gradient compression via coding theory (1-bit Adam, QSGD)
  - Coded computation in distributed matrix multiplication
  - Straggler mitigation via MDS codes in distributed training

---

## Module 5: Numerical Linear Algebra for Scientific Computing

**Duration:** 4–5 weeks  
**Objective:** Numerical linear algebra is the computational backbone of scientific computing. This module covers algorithms, stability, and high-performance implementations.

### 5.1 Direct Methods for Linear Systems
- **Gaussian Elimination:** LU decomposition, pivoting strategies, stability analysis
- **Cholesky Decomposition:** SPD systems, incomplete Cholesky preconditioners
- **QR Decomposition:** Householder, Givens, Gram-Schmidt, least squares
- *Production Context:* 
  - LU in circuit simulation and PDE solvers
  - Cholesky in Gaussian process covariance matrices
  - QR in least squares regression and orthogonalization

### 5.2 Iterative Methods for Sparse Systems
- **Stationary Methods:** Jacobi, Gauss-Seidel, SOR, convergence analysis
- **Krylov Subspace Methods:** CG, GMRES, BiCGSTAB, preconditioning
- **Multigrid Methods:** Geometric, algebraic, V-cycles, W-cycles
- *Production Context:* 
  - CG in large-scale optimization and physics simulations
  - GMRES in non-symmetric PDE systems
  - Multigrid in high-resolution simulation preconditioning

### 5.3 Eigenvalue & Singular Value Problems
- **Power Iteration & QR Algorithm:** Basic methods, shifts, deflation
- **Lanczos & Arnoldi:** Krylov methods for eigenproblems, implicit restart
- **Randomized SVD:** Sketching, power iteration, streaming algorithms
- *Production Context:* 
  - Randomized SVD in large-scale PCA and model compression
  - Lanczos in spectral clustering and graph analysis
  - Eigenvalue computation in stability analysis of dynamical systems

### 5.4 Fast Transforms & Structured Matrices
- **FFT & DFT:** Cooley-Tukey, butterfly, convolution theorem
- **Toeplitz & Circulant:** Fast solvers, embedding, preconditioning
- **Hierarchical Matrices:** H-matrices, low-rank approximations, fast arithmetic
- *Production Context:* 
  - FFT in convolutional layer acceleration
  - Toeplitz solvers in time-series analysis
  - H-matrices in fast kernel methods and N-body problems

---

## Module 6: Numerical Methods for Differential Equations

**Duration:** 4–5 weeks  
**Objective:** Differential equations model physical systems, optimization dynamics, and generative processes. This module covers numerical solution methods with production implementations.

### 6.1 Ordinary Differential Equations (ODEs)
- **Initial Value Problems:** Existence, uniqueness, Lipschitz continuity
- **One-Step Methods:** Euler, Runge-Kutta, embedded pairs, adaptive step size
- **Stiff ODEs:** Implicit methods, BDF, stability regions, A-stability
- **Sensitivity Analysis:** Forward/adjoint sensitivity, automatic differentiation
- *Production Context:* 
  - ODE solvers in neural ODEs (torchdiffeq, torchdyn)
  - Stiff solvers in chemical kinetics and reaction networks
  - Sensitivity analysis in gradient-based parameter estimation

### 6.2 Partial Differential Equations (PDEs)
- **Finite Difference Methods:** Discretization, stability (CFL), convergence
- **Finite Element Methods:** Weak formulation, Galerkin, mesh generation
- **Spectral Methods:** Fourier-Galerkin, collocation, polynomial approximation
- *Production Context:* 
  - Finite difference in fluid dynamics and climate simulation
  - FEM in structural analysis and engineering simulation
  - Spectral methods in turbulence modeling and weather prediction

### 6.3 Numerical Optimization & Root Finding
- **Newton's Method:** Local convergence, globalization, line search
- **Quasi-Newton Methods:** BFGS, L-BFGS, SR1, limited-memory variants
- **Nonlinear Solvers:** Fixed-point iteration, Anderson acceleration, inexact Newton
- *Production Context:* 
  - Newton's method in nonlinear PDE solvers
  - L-BFGS in large-scale training (full-batch optimization)
  - Anderson acceleration in fixed-point neural network layers

### 6.4 Monte Carlo Methods & Integration
- **Random Sampling:** Inverse transform, rejection sampling, importance sampling
- **Quasi-Monte Carlo:** Low-discrepancy sequences, Halton, Sobol sequences
- **Markov Chain Monte Carlo:** Metropolis, Gibbs, Hamiltonian Monte Carlo
- *Production Context:* 
  - Monte Carlo in Bayesian inference and probabilistic programming
  - QMC in high-dimensional numerical integration
  - MCMC in posterior sampling for Bayesian neural networks

---

## Module 7: Physics-Informed Machine Learning (SciML)

**Duration:** 4–5 weeks  
**Objective:** Scientific machine learning integrates physical knowledge with data-driven models. This module covers physics-informed neural networks, operator learning, and differentiable programming.

### 7.1 Physics-Informed Neural Networks (PINNs)
- **PDE Residual Loss:** Automatic differentiation for derivatives, collocation points
- **Boundary & Initial Conditions:** Hard constraints, soft constraints, exact enforcement
- **Forward & Inverse Problems:** Simulation, parameter identification, discovery
- **Training Challenges:** Spectral bias, causality, adaptive sampling, curriculum learning
- *Production Context:* 
  - PINNs in digital twin modeling and simulation
  - Inverse PINNs for parameter estimation from sparse measurements
  - PINN limitations: high-frequency solutions, training instability

### 7.2 Neural Operators & Operator Learning
- **DeepONet:** Branch net, trunk net, operator approximation
- **Fourier Neural Operator (FNO):** FFT-based integral operator, resolution invariance
- **Convolutional Neural Operators:** Green's function approximation, wavelet transforms
- *Production Context:* 
  - FNO in surrogate modeling for PDEs (fluid dynamics, climate)
  - Neural operators in real-time simulation for control systems
  - Operator learning in multi-scale physics problems

### 7.3 Differentiable Physics & Neural ODEs
- **Neural ODEs:** Continuous-depth models, adjoint method, sensitivity
- **Differentiable Simulators:** Automatic differentiation through physics engines
- **Hamiltonian Neural Networks:** Structure-preserving learning, symplectic integrators
- *Production Context:* 
  - Neural ODEs in continuous-time generative models
  - Differentiable physics in robotics simulation and control
  - Hamiltonian networks in molecular dynamics simulation

### 7.4 Symbolic Regression & Equation Discovery
- **Sparse Identification (SINDy):** Sparse regression, library construction, cross-validation
- **Genetic Programming:** Symbolic regression, grammar-based search
- **AI Feynman:** Neural network-based symbolic discovery
- *Production Context:* 
  - SINDy in discovering governing equations from data
  - Symbolic regression in interpretable model discovery
  - Equation discovery in scientific knowledge extraction

### 7.5 Multi-Fidelity & Hybrid Modeling
- **Multi-Fidelity Methods:** Coarse/fine models, Gaussian process cokriging
- **Hybrid ML-Physics:** Residual modeling, correction terms, domain decomposition
- **Digital Twins:** Real-time simulation, state estimation, predictive maintenance
- *Production Context:* 
  - Multi-fidelity in expensive simulation optimization
  - Hybrid models in weather forecasting (physics + ML)
  - Digital twins in industrial IoT and predictive maintenance

---

## Module 8: High-Performance Scientific Computing

**Duration:** 4–5 weeks  
**Objective:** Scientific computing at scale requires careful attention to hardware, parallelism, and algorithm design. This module covers HPC principles for AI infrastructure.

### 8.1 Parallel Computing Paradigms
- **Shared Memory:** OpenMP, threading, race conditions, false sharing
- **Distributed Memory:** MPI, point-to-point, collectives, topology awareness
- **GPU Computing:** CUDA, thread hierarchy, memory coalescing, occupancy
- *Production Context:* 
  - MPI in distributed training and large-scale simulation
  - GPU computing in PINN training and PDE solvers
  - Shared memory parallelism in multi-core data preprocessing

### 8.2 Domain Decomposition & Load Balancing
- **Spatial Decomposition:** Overlapping/non-overlapping, Schwarz methods
- **Graph Partitioning:** METIS, ParMETIS, spectral partitioning
- **Dynamic Load Balancing:** Work stealing, task queues, adaptive mesh refinement
- *Production Context:* 
  - Domain decomposition in climate and fluid simulation
  - Graph partitioning in distributed GNN training
  - Dynamic load balancing in particle-based simulations

### 8.3 Communication-Avoiding Algorithms
- **Communication Lower Bounds:** Irony-Tiskin-Toledo, latency/bandwidth trade-offs
- **2.5D & 3D Algorithms:** Matrix multiplication, LU, QR with reduced communication
- **Tile Algorithms:** Tiled Cholesky, tiled QR, dynamic scheduling
- *Production Context:* 
  - Communication-avoiding in distributed deep learning (SUMMA, Cannon)
  - Tile algorithms in dense linear algebra libraries (PLASMA, DPLASMA)
  - Communication-optimal gradient aggregation strategies

### 8.4 I/O & Storage for Scientific Data
- **Parallel I/O:** HDF5, NetCDF, MPI-IO, collective buffering
- **Data Formats:** Columnar (Parquet, Arrow), tensor (Zarr, N5), mesh (VTK, XDMF)
- **In-Situ Processing:** Visualization, analysis during simulation, reduced I/O
- *Production Context:* 
  - HDF5 in large-scale checkpointing for training
  - Zarr in cloud-native scientific data storage
  - In-situ in real-time monitoring of distributed training

---

## Module 9: Mixed-Precision, Stochastic & Randomized Algorithms

**Duration:** 3–4 weeks  
**Objective:** Modern hardware demands algorithms that exploit mixed precision, stochasticity, and randomization for efficiency without sacrificing correctness.

### 9.1 Mixed-Precision Numerical Methods
- **Floating-Point Formats:** FP64, FP32, BF16, FP16, FP8, integer emulation
- **Iterative Refinement:** Mixed-precision linear solvers, error analysis
- **Stochastic Rounding:** Unbiased rounding, error compensation, probabilistic bounds
- *Production Context:* 
  - Mixed-precision in scientific computing (FP64/FP32/BF16/FP8)
  - Iterative refinement in mixed-precision matrix factorizations
  - Stochastic rounding in low-precision training and simulation

### 9.2 Randomized Numerical Linear Algebra
- **Randomized SVD:** Range finder, power iteration, streaming algorithms
- **Sketching Techniques:** Count-sketch, sparse JL, leverage score sampling
- **Randomized Preconditioning:** Blendenpik, LSRN, recursive sketching
- *Production Context:* 
  - Randomized SVD in large-scale PCA and low-rank approximation
  - Sketching in streaming regression and online learning
  - Randomized preconditioning in distributed least squares

### 9.3 Probabilistic Error Bounds & Verification
- **Probabilistic Roundoff Analysis:** Forward error, backward error, confidence intervals
- **Monte Carlo Arithmetic:** Randomized rounding, error detection, verification
- **Verification in Scientific Computing:** Interval arithmetic, Taylor models, rigorous numerics
- *Production Context:* 
  - Probabilistic error bounds in mixed-precision deep learning
  - Monte Carlo arithmetic in numerical debugging
  - Rigorous numerics in safety-critical simulation verification

### 9.4 Energy-Aware & Sustainable Computing
- **Energy-Performance Trade-offs:** DVFS, power capping, energy-proportional computing
- **Green AI:** Carbon footprint of training, efficiency metrics, sustainable practices
- **Algorithmic Energy Minimization:** Communication reduction, precision tuning, sparsity
- *Production Context:* 
  - Energy-aware scheduling in GPU clusters
  - Carbon footprint tracking in model training pipelines
  - Algorithmic energy minimization in large-scale simulation

---

## Module 10: Production Scientific Computing & Information Systems

**Duration:** 4–5 weeks  
**Objective:** Bridge the gap between theory and production deployment. This module focuses on operational aspects of scientific computing and information systems in AI infrastructure.

### 10.1 Model Compression & Quantization Systems
- **Quantization-Aware Training:** Differentiable quantization, straight-through estimator
- **Post-Training Quantization:** Calibration, range estimation, per-channel scaling
- **Compression Pipelines:** Pruning → quantization → encoding → deployment
- *Production Context:* 
  - TensorRT quantization in inference serving
  - ONNX Runtime quantization for cross-platform deployment
  - Compression pipelines in mobile and edge AI

### 10.2 Distributed Training Communication Optimization
- **Gradient Compression:** Top-K, signSGD, error feedback, 1-bit Adam
- **Communication Scheduling:** Overlap computation/communication, pipeline bubbles
- **Collective Optimization:** Ring-allreduce, tree-allreduce, hierarchical aggregation
- *Production Context:* 
  - Gradient compression in bandwidth-limited clusters
  - Communication scheduling in pipeline parallelism
  - Hierarchical collectives in multi-rack GPU clusters

### 10.3 Scientific Data Infrastructure
- **Data Lakes for Science:** Schema-on-read, metadata management, provenance
- **Feature Stores:** Online/offline consistency, versioning, point-in-time correctness
- **Experiment Tracking:** MLflow, Weights & Biases, reproducibility, lineage
- *Production Context:* 
  - Scientific data lakes in climate and genomics
  - Feature stores in production ML pipelines
  - Experiment tracking in large-scale hyperparameter search

### 10.4 Reliability & Fault Tolerance
- **Checkpointing Strategies:** Full, incremental, asynchronous, hierarchical
- **Error Correction in AI:** ECC memory, checksums, algorithm-based fault tolerance (ABFT)
- **Byzantine Fault Tolerance:** Robust aggregation, Krum, trimmed mean
- *Production Context:* 
  - Checkpointing in long-running training jobs
  - ABFT in large-scale matrix operations
  - Byzantine-robust aggregation in federated learning

### 10.5 Performance Monitoring & Benchmarking
- **Roofline Model:** Arithmetic intensity, memory bandwidth, compute bottlenecks
- **Scientific Benchmarks:** HPL, HPCG, MLPerf HPC, custom kernels
- **Profiling Tools:** NVIDIA Nsight, Intel VTune, TAU, HPCToolkit
- *Production Context:* 
  - Roofline analysis in kernel optimization
  - MLPerf HPC in benchmarking scientific ML workloads
  - Profiling in identifying bottlenecks in distributed training

---

## Capstone Projects

Each student must complete **two** capstone projects: one from Category A (Implementation) and one from Category B (Systems/Infrastructure).

### Category A: Deep Implementation Projects

**A1. Production-Grade Lossless Compression Library for Model Weights**
- Implement Huffman, arithmetic, and asymmetric numeral systems (ANS) coding
- Support adaptive compression for streaming model updates
- Integrate with PyTorch/TensorFlow for checkpoint compression
- Benchmark against gzip, zstd, lz4 on model checkpoints
- **Systems Requirements:** Streaming capability, GPU decompression, checksum verification

**A2. Error-Correcting Code System for Distributed Storage**
- Implement Reed-Solomon and locally repairable codes (LRC)
- Support erasure coding for distributed training checkpoints
- Implement efficient repair for single and multiple failures
- **Systems Requirements:** Repair bandwidth optimization, parallel encoding/decoding, metadata management

**A3. Physics-Informed Neural Network Framework for Production**
- Implement PINNs for elliptic, parabolic, and hyperbolic PDEs
- Support adaptive sampling, curriculum learning, and causal training
- Integrate with distributed training for large-scale simulation
- **Systems Requirements:** Multi-GPU support, checkpointing, residual monitoring, convergence diagnostics

**A4. Mixed-Precision Scientific Computing Library**
- Implement mixed-precision iterative solvers (GMRES, CG) with iterative refinement
- Support FP16/BF16/FP32/FP64 with automatic precision selection
- Benchmark against vendor libraries (cuSOLVER, MKL)
- **Systems Requirements:** Numerical stability monitoring, automatic fallback, performance profiling

### Category B: Systems & Infrastructure Projects

**B1. Communication-Efficient Distributed Training System**
- Build a training system with gradient compression (Top-K, signSGD, quantization)
- Implement error feedback and local steps for convergence
- Support heterogeneous networks (WAN, multi-cloud)
- **Information Theory Components:** Source coding of gradients, rate-distortion optimization, channel coding for reliable aggregation

**B2. Scientific Data Platform for AI Workloads**
- Build a data platform supporting multi-dimensional arrays, meshes, and tensors
- Implement parallel I/O, compression, and caching
- Support metadata, provenance, and versioning
- **Scientific Computing Components:** HDF5/Zarr integration, domain decomposition, in-situ processing

**B3. Probabilistic Performance Modeling for GPU Clusters**
- Implement a framework modeling training time as stochastic process
- Support variability-aware scheduling and resource allocation
- Provide p95 performance guarantees
- **Components:** Queueing models, Monte Carlo simulation, tail latency optimization

**B4. Model Compression Service for Inference**
- Build a service for automatic model quantization and compression
- Support INT8/INT4/FP8 with accuracy preservation
- Implement calibration, validation, and rollback
- **Components:** Rate-distortion optimization, entropy coding, accuracy monitoring

---

## Assessment & Evaluation Framework

### Formative Assessments (Continuous)
- **Weekly Problem Sets:** 3–5 theoretical and implementation problems
- **Implementation Reviews:** Code review sessions focusing on correctness, numerical stability, and performance
- **Reading Reviews:** Analysis of seminal papers with systems relevance

### Summative Assessments (Milestone)
- **Midterm Examination:** 
  - 4-hour closed-book exam
  - Theoretical proofs (30%), algorithm design (40%), systems analysis (30%)
  - Topics: Modules 0–5

- **Final Examination:**
  - 6-hour take-home exam
  - Open-systems (access to documentation, no human collaboration)
  - Design a complete information-theoretic or scientific computing system from theory to production deployment
  - Topics: Modules 6–10 + integration

### Capstone Evaluation Rubric
| Criterion | Weight | Description |
|-----------|--------|-------------|
| Theoretical Correctness | 20% | Mathematical rigor, coding theory correctness, numerical stability |
| Implementation Quality | 25% | Code efficiency, hardware utilization, scalability |
| Systems Integration | 20% | Production readiness, fault tolerance, observability |
| Architecture Reasoning | 20% | Design decisions, trade-off analysis, information-theoretic optimality |
| Documentation | 15% | Technical writing, operational runbooks, theoretical rigor |

---

## Recommended Resources & Bibliography

### Core Textbooks (Information Theory)
1. **Cover, Thomas M. & Thomas, Joy A.** *Elements of Information Theory* (2nd ed.). Wiley, 2006. — *The definitive information theory reference.*
2. **MacKay, David J. C.** *Information Theory, Inference, and Learning Algorithms.* Cambridge University Press, 2003. — *Accessible, comprehensive, with practical algorithms.*
3. **Richardson, Tom & Urbanke, Rüdiger.** *Modern Coding Theory.* Cambridge University Press, 2008. — *LDPC codes and iterative decoding.*
4. **Lin, Shu & Costello, Daniel J.** *Error Control Coding* (2nd ed.). Pearson, 2004. — *Comprehensive coding theory.*

### Core Textbooks (Scientific Computing)
5. **Trefethen, Lloyd N. & Bau, David III.** *Numerical Linear Algebra.* SIAM, 1997. — *Concise, rigorous numerical LA.*
6. **LeVeque, Randall J.** *Finite Difference Methods for Ordinary and Partial Differential Equations.* SIAM, 2007. — *Clear introduction to numerical PDEs.*
7. **Hairer, Ernst, Nørsett, Syvert P. & Wanner, Gerhard.** *Solving Ordinary Differential Equations I: Nonstiff Problems* (2nd ed.). Springer, 1993. — *The ODE bible.*
8. **Saad, Yousef.** *Iterative Methods for Sparse Linear Systems* (2nd ed.). SIAM, 2003. — *Sparse solvers canonical reference.*

### Scientific Machine Learning
9. **Karniadakis, George Em et al.** "Physics-Informed Machine Learning." *Nature Reviews Physics*, 2021. — *PINNs and SciML overview.*
10. **Chen, Ricky T. Q. et al.** "Neural Ordinary Differential Equations." *NeurIPS 2018.* — *Neural ODEs.*
11. **Li, Zongyi et al.** "Fourier Neural Operator for Parametric Partial Differential Equations." *ICLR 2021.* — *Neural operators.*
12. **Raissi, Maziar et al.** "Physics-Informed Neural Networks: A Deep Learning Framework for Solving Forward and Inverse Problems Involving Nonlinear Partial Differential Equations." *JCP*, 2019. — *Seminal PINN paper.*

### Systems & Infrastructure
13. **Golden, Alicia et al.** "Probabilistic Runtime Insights and Scalable Performance Modeling for Large-Scale Distributed Training." *arXiv:2510.15596, 2026.* — *PRISM framework.*
14. **Demmel, James et al.** "Communication-Optimal Parallel and Sequential QR and LU Factorizations." *SIAM J. Sci. Comput.*, 2012. — *Communication-avoiding algorithms.*
15. **Cloud4SciEng.** "Ride the Wave, Build the Future: Scientific Computing in an AI World." 2026. — *Future of scientific computing.*

### Online Resources
- **MIT 6.441:** Information Theory
- **Stanford EE376A:** Information Theory
- **ETH 401-4656-21L:** AI in the Sciences and Engineering (PINNs, Neural Operators)
- **Oxford CS:** Physics Informed Neural Networks Course
- **SciML.ai:** Scientific Machine Learning Community
- **Julia SciML:** DifferentialEquations.jl, NeuralOperators.jl

---

## Appendix: Production Checklist

Before deploying any information-theoretic or scientific computing component to production, verify:

- [ ] **Theoretical Correctness:** Coding theory bounds verified, numerical stability proven
- [ ] **Compression Efficiency:** Rate-distortion trade-off analyzed, benchmarked against baselines
- [ ] **Numerical Stability:** Convergence verified, error bounds computed, edge cases handled
- [ ] **Scalability Tested:** Strong/weak scaling, communication overhead quantified
- [ ] **Fault Tolerance:** Error correction verified, graceful degradation tested
- [ ] **Performance Benchmarked:** Roofline analysis, FLOPs utilization, memory bandwidth saturation
- [ ] **Observability:** Compression ratios, numerical residuals, convergence metrics logged
- [ ] **Documentation:** API docs, theoretical behavior specification, operational runbooks

---

**End of Syllabus**

*Information theory and scientific computing are the twin pillars of modern AI infrastructure: information theory provides the fundamental limits of what can be compressed, communicated, and learned; scientific computing provides the algorithms and systems to reach those limits in practice. Mastery of both at the systems level is the difference between building models that work in isolation and building infrastructure that compresses, computes, and communicates reliably, efficiently, and at planetary scale. The information-theoretic optimality and scientific rigor you deploy today determine the efficiency and trustworthiness of the intelligent systems that power tomorrow.*