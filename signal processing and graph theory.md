## File: signal-processing-graph-theory-syllabus.md

# Signal Processing & Graph Theory for AI/ML Infrastructure Engineers

**Version:** 1.0  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, Retrieval/Search Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level infrastructure candidates  
**Prerequisites:** Linear Algebra, Calculus, Probability & Statistics, Data Structures & Algorithms, Python/C++ proficiency, basic systems programming  
**Estimated Duration:** 200–250 hours (lecture + lab + project)  
**Format:** Self-contained, publication-quality, GitHub-ready Markdown  

---

## Table of Contents

1. [Course Philosophy & Pedagogical Approach](#1-course-philosophy--pedagogical-approach)
2. [Learning Objectives & Competency Matrix](#2-learning-objectives--competency-matrix)
3. [Module 0: Mathematical & Systems Foundations Review](#module-0-mathematical--systems-foundations-review)
4. [Module 1: Discrete-Time Signal Processing Foundations](#module-1-discrete-time-signal-processing-foundations)
5. [Module 2: Spectral Analysis & Frequency-Domain Methods](#module-2-spectral-analysis--frequency-domain-methods)
6. [Module 3: Filter Design & Digital Filtering Systems](#module-3-filter-design--digital-filtering-systems)
7. [Module 4: Multirate Signal Processing & Resampling](#module-4-multirate-signal-processing--resampling)
8. [Module 5: Graph Theory Foundations for AI Systems](#module-5-graph-theory-foundations-for-ai-systems)
9. [Module 6: Spectral Graph Theory & Graph Signal Processing](#module-6-spectral-graph-theory--graph-signal-processing)
10. [Module 7: Graph Neural Networks & Message Passing](#module-7-graph-neural-networks--message-passing)
11. [Module 8: Large-Scale Graph Systems & Distributed Graph Processing](#module-8-large-scale-graph-systems--distributed-graph-processing)
12. [Module 9: Production Integration — Signal & Graph Pipelines](#module-9-production-integration--signal--graph-pipelines)
13. [Module 10: Advanced Topics & Research Frontiers](#module-10-advanced-topics--research-frontiers)
14. [Capstone Projects](#capstone-projects)
15. [Assessment & Evaluation Framework](#assessment--evaluation-framework)
16. [Recommended Tools, Libraries & Infrastructure](#recommended-tools-libraries--infrastructure)
17. [References & Further Reading](#references--further-reading)

---

## 1. Course Philosophy & Pedagogical Approach

This syllabus treats **Signal Processing** and **Graph Theory** not as separate mathematical disciplines, but as **unified mathematical machinery for representing, transforming, and reasoning about structured data in AI systems**. The pedagogical approach follows a **Theory → Implementation → Systems → Infrastructure → Production** pipeline:

| Phase | Focus | Output |
|-------|-------|--------|
| **Theory** | Mathematical definitions, theorems, proofs | Intuition + rigor |
| **Implementation** | Algorithmic realization, numerical methods | Working code |
| **Systems** | Data structures, memory layouts, I/O patterns | Efficient implementations |
| **Infrastructure** | Distributed execution, resource management | Scalable services |
| **Production** | Monitoring, debugging, SLOs, reliability | Battle-tested pipelines |

**Core Principles:**
- **Every concept must have a production AI system analog.** FFT → LLM attention optimization; Graph Laplacian → recommendation system embeddings; Spectral clustering → document retrieval.
- **Performance is a first-class concern.** We analyze FLOPs, memory bandwidth, cache behavior, and distributed communication patterns.
- **Debugging is a skill.** Each module includes "failure modes and diagnostics" sections.
- **Architecture reasoning over API memorization.** We teach *why* PyTorch Geometric or DGL is designed the way it is, not just *how* to use it.

---

## 2. Learning Objectives & Competency Matrix

Upon completion, engineers will demonstrate:

### Signal Processing Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Sample, quantize, reconstruct signals without aliasing | Audio preprocessing for ASR pipelines |
| **Intermediate** | Design FIR/IIR filters, implement FFT/DFT, analyze spectra | Feature extraction for time-series models |
| **Advanced** | Multirate processing, windowing, spectral estimation, STFT | Real-time audio streaming, speech enhancement |
| **Expert** | Custom CUDA kernels for FFT, polyphase implementations, streaming algorithms | GPU-accelerated inference preprocessing |

### Graph Theory Competencies
| Level | Competency | Production Context |
|-------|-----------|-------------------|
| **Beginner** | Represent graphs (adjacency, incidence, Laplacian), traverse (BFS/DFS) | Knowledge graph storage, social graph queries |
| **Intermediate** | Compute centrality, community detection, shortest paths at scale | Fraud detection, recommendation ranking |
| **Advanced** | Spectral graph theory, graph Fourier transform, GNN message passing | Graph-based retrieval, molecular property prediction |
| **Expert** | Distributed graph partitioning, sampling, sparsification, GNN system design | Billion-node graph serving, Pinterest/LinkedIn-scale systems |

### Cross-Cutting Competencies
- **Systems:** Design pipelines that process >1M signals/sec or graphs with >1B edges
- **Mathematical:** Derive and prove correctness of spectral algorithms
- **Operational:** Debug numerical instability, distributed deadlocks, memory pressure
- **Architectural:** Choose between signal-based vs. graph-based representations for a given AI problem

---

## Module 0: Mathematical & Systems Foundations Review

**Duration:** 15 hours  
**Purpose:** Ensure all learners share prerequisite fluency; identify gaps early

### 0.1 Linear Algebra Refresher for Signal/Graph Processing
- **Vector spaces over ℝ and ℂ:** Inner products, norms, orthogonality
- **Matrix decompositions:** Eigendecomposition, SVD, QR, Cholesky — computational complexity and numerical stability
- **Toeplitz, Circulant, and Hankel matrices:** Structure-exploiting algorithms (O(n log n) vs O(n³))
- **Tensor contractions:** Einstein notation, n-mode products (preparation for multivariate signals)
- **Sparse matrix formats:** CSR, CSC, COO — memory access patterns, cache efficiency
- **Production connection:** Why SVD is the backbone of latent semantic indexing; why sparse formats matter for billion-edge graphs

### 0.2 Complex Analysis & Fourier Series Primer
- **Complex numbers in polar form:** Magnitude, phase, Euler's formula
- **Fourier series convergence:** Dirichlet conditions, Gibbs phenomenon
- **L² space completeness:** Parseval's theorem, energy conservation
- **Production connection:** Phase information in audio signals; why magnitude-only STFT loses critical information

### 0.3 Probability & Stochastic Processes
- **Random variables, expectation, variance:** Moment-generating functions
- **Wide-sense stationary (WSS) processes:** Autocorrelation, power spectral density
- **Gaussian processes, white noise:** Filtering stochastic signals
- **Production connection:** Modeling sensor noise in IoT pipelines; understanding why "spectral whitening" improves convergence

### 0.4 Systems Programming Foundations
- **Memory hierarchy:** Registers → L1/L2/L3 → DRAM → SSD → Network. Bandwidth and latency at each level
- **SIMD/vectorization:** AVX-512, NEON. Data layout for SoA vs AoS
- **Concurrency primitives:** Locks, atomics, lock-free queues, memory ordering
- **GPU architecture:** Warps, shared memory, coalesced access, occupancy
- **Production connection:** Why FFTW beats naive FFT; why graph traversal is memory-bound, not compute-bound

### 0.5 Lab: Benchmarking Baseline
- Implement naive matrix-vector multiply, naive DFT, naive BFS
- Profile with `perf`, `nvprof`, `Intel VTune`
- Document cache misses, branch mispredictions, memory bandwidth utilization
- **Deliverable:** Baseline performance report establishing "naive" vs "optimized" gap

---

## Module 1: Discrete-Time Signal Processing Foundations

**Duration:** 20 hours  
**Level:** Beginner → Intermediate

### 1.1 Sampling, Quantization, and Reconstruction
- **Nyquist-Shannon sampling theorem:** Bandlimited signals, critical sampling, oversampling
- **Aliasing:** Frequency folding, anti-aliasing filters, practical considerations
- **Quantization:** Uniform, non-uniform (μ-law, A-law), dithering, quantization noise power
- **Reconstruction:** Ideal sinc interpolation, zero-order hold, first-order hold, practical DACs
- **Sampling in multiple dimensions:** Image sampling, hexagonal grids, quincunx sampling
- **Production context:** 
  - Audio pipelines: 16kHz vs 44.1kHz for speech recognition
  - Video pipelines: Chroma subsampling (4:2:0, 4:2:2)
  - LLM tokenization as a form of "semantic sampling"

### 1.2 Discrete-Time Signals and Systems
- **Signal classes:** Finite/infinite energy, causal, anti-causal, periodic, aperiodic
- **Basic operations:** Time shifting, reversal, scaling, decimation, interpolation
- **LTI systems:** Impulse response, convolution sum, frequency response, BIBO stability
- **Difference equations:** IIR/FIR classification, direct form structures, cascade/parallel realizations
- **z-Transform:** Region of convergence, pole-zero analysis, inverse z-transform (partial fractions, power series, contour integration)
- **System properties:** Causality, stability, minimum-phase, all-pass, linear phase
- **Production context:**
  - Why FIR filters are preferred in production (guaranteed stability, linear phase)
  - Implementing convolution as matrix multiplication for GPU batching

### 1.3 Convolution: Theory, Algorithms, and Systems
- **Mathematical definition:** Discrete convolution as polynomial multiplication
- **Computational complexity:** Naive O(n²), FFT-based O(n log n), overlap-add, overlap-save
- **Circular vs. linear convolution:** Zero-padding, DFT properties
- **Fast convolution on GPUs:** cuFFT, cuDNN convolution algorithms (implicit GEMM, Winograd, FFT)
- **Memory layouts:** NCHW vs NHWC, implications for cache locality
- **Production context:**
  - Audio effect pipelines: real-time convolution reverb
  - Image processing: Gaussian blur, Sobel edge detection
  - Deep learning: 1D convolutions in WaveNet, 2D convolutions in ResNet

### 1.4 Lab: Building a Production-Grade Audio Preprocessing Pipeline
- **Task:** Implement end-to-end audio preprocessing for an ASR system
- **Components:**
  1. Resampling (polyphase implementation): 44.1kHz → 16kHz
  2. Pre-emphasis filter (first-order FIR)
  3. Framing and windowing (Hamming, Hann, Blackman — compare)
  4. Power normalization, dithering for quantization to int16
- **Performance requirements:** Process 100 hours of audio in <10 minutes on a single GPU
- **Deliverable:** Python/C++ pipeline with benchmarking, documented design decisions, performance analysis

---

## Module 2: Spectral Analysis & Frequency-Domain Methods

**Duration:** 25 hours  
**Level:** Intermediate → Advanced

### 2.1 Discrete Fourier Transform (DFT) — Deep Dive
- **Definition and properties:** Linearity, shift, convolution, correlation, Parseval's theorem
- **Matrix formulation:** DFT matrix, unitary scaling, circulant matrix diagonalization
- **Computational complexity:** Why O(N²) is unacceptable at scale
- **Number-theoretic transform (NTT):** DFT over finite fields, application in cryptography and ML
- **Production context:** 
  - DFT as the workhorse of spectral feature extraction
  - Why DFT size matters: power-of-2 vs. prime-factor vs. Bluestein algorithm

### 2.2 Fast Fourier Transform (FFT) Algorithms
- **Cooley-Tukey radix-2:** Decimation-in-time, decimation-in-frequency, butterfly diagrams
- **Mixed-radix, split-radix:** Optimizing for non-power-of-2 sizes
- **Rader's algorithm, Bluestein's algorithm:** Prime-length DFTs
- **FFT on modern hardware:**
  - SIMD vectorization: FFTW's "codelets"
  - GPU implementation: cuFFT, rocFFT — thread coarsening, shared memory tiling
  - Distributed FFT: Pencil decomposition for 3D FFTs (climate simulation, molecular dynamics)
- **Numerical stability:** Round-off error analysis, twiddle factor accuracy
- **Production context:**
  - Real-time spectrogram computation for voice activity detection
  - FFT in LLM attention approximations (e.g., FlashAttention-2 block-sparse patterns)
  - FFT-based convolution in depthwise separable convolutions (MobileNet efficiency)

### 2.3 Windowing and Spectral Leakage
- **Spectral leakage mechanism:** Finite observation of infinite signals
- **Window functions:** Rectangular, Hann, Hamming, Blackman, Kaiser, Gaussian, flat-top
- **Window metrics:** Main lobe width, side lobe level, side lobe roll-off, coherent gain, equivalent noise bandwidth
- **Choosing windows:** Trade-offs for tone detection vs. broadband analysis
- **Production context:** 
  - STFT window choice in music information retrieval
  - Overlap-add constraints: 50%, 75%, 87.5% — compute vs. temporal resolution trade-off

### 2.4 Short-Time Fourier Transform (STFT) and Spectrograms
- **STFT definition:** Time-frequency tiling, uncertainty principle
- **Spectrogram:** Power, magnitude, log-magnitude, Mel-scale warping
- **Inverse STFT:** Perfect reconstruction conditions, Griffin-Lim algorithm
- **Constant-Q transform:** Log-frequency resolution for musical signals
- **Production context:**
  - Mel-spectrogram → CNN for sound classification
  - STFT as frontend for neural audio codecs (SoundStream, EnCodec)
  - Real-time STFT on edge devices: fixed-point arithmetic, lookup tables

### 2.5 Power Spectral Density Estimation
- **Periodogram:** Definition, bias, variance, inconsistency
- **Bartlett's method:** Averaging periodograms
- **Welch's method:** Overlapped segments, windowed periodograms
- **Parametric methods:** AR, MA, ARMA models, Yule-Walker equations, Burg's method
- **Modern spectral estimation:** MUSIC, ESPRIT — subspace methods
- **Production context:**
  - Anomaly detection in time-series via spectral change
  - Channel estimation in wireless communication for federated learning
  - Vibration analysis for predictive maintenance in industrial IoT

### 2.6 Lab: GPU-Accelerated Spectral Feature Extraction
- **Task:** Build a spectral feature extractor that processes 10,000 audio streams concurrently
- **Requirements:**
  - Implement STFT with configurable window/overlap on GPU
  - Compute Mel-spectrogram with learnable Mel filterbank
  - Benchmark against librosa (CPU) and torchaudio (GPU)
  - Profile memory bandwidth, occupancy, kernel fusion opportunities
- **Deliverable:** CUDA/C++ extension with Python bindings, performance comparison report, optimization recommendations

---

## Module 3: Filter Design & Digital Filtering Systems

**Duration:** 20 hours  
**Level:** Intermediate → Advanced

### 3.1 FIR Filter Design
- **Linear phase FIR:** Types I-IV, symmetry constraints, zero locations
- **Window method:** Design by windowing ideal impulse responses
- **Frequency sampling method:** Sampling desired response, IDFT
- **Optimal equiripple design:** Parks-McClellan algorithm, Remez exchange, Chebyshev approximation
- **Least-squares design:** FIR design as convex optimization
- **Multiband, Hilbert transformer, differentiator:** Specialized designs
- **Production context:**
  - Anti-aliasing filters in audio resampling (SoX, ffmpeg)
  - Matched filters in radar/sonar signal processing
  - FIR approximation of IIR for parallel GPU execution

### 3.2 IIR Filter Design
- **Classical analog prototypes:** Butterworth, Chebyshev (Type I/II), Elliptic, Bessel
- **Bilinear transform:** s-plane to z-plane mapping, frequency warping, prewarping
- **Impulse invariance:** Aliasing issues, applicability
- **Direct form structures:** I, II, transposed — numerical stability comparison
- **Lattice, wave digital filters:** Alternative structures for fixed-point
- **Production context:**
  - IIR for equalization in audio production (low compute, steep roll-off)
  - Stability concerns: why IIR is avoided in some ML pipelines
  - State-space implementations for better numerical properties

### 3.3 Adaptive Filtering & Online Learning
- **Wiener filter:** Optimal linear estimation, orthogonality principle
- **LMS algorithm:** Derivation, convergence analysis, step-size selection
- **NLMS, sign-LMS, leaky LMS:** Variants for robustness
- **RLS algorithm:** Newton's method interpretation, fast RLS, numerical issues
- **Kalman filtering:** State-space model, prediction-correction, extended Kalman filter
- **Production context:**
  - Echo cancellation in VoIP systems
  - Noise suppression in real-time communication (RNNoise, WebRTC)
  - Adaptive beamforming for microphone arrays
  - Online gradient estimation in distributed learning

### 3.4 Filter Banks & Subband Processing
- **Two-channel filter bank:** Perfect reconstruction conditions, alias cancellation
- **QMF, CQF, orthogonal, biorthogonal:** Design families
- **M-channel filter banks:** Polyphase representation, noble identities
- **Cosine-modulated filter banks:** Pseudo-QMF, paraunitary
- **Wavelets from filter banks:** Multiresolution analysis, scaling functions, wavelet functions
- **Production context:**
  - JPEG 2000 wavelet compression
  - Subband coding in audio compression (MP3, AAC)
  - Multiresolution analysis in computer vision (Laplacian pyramids)

### 3.5 Lab: Real-Time Adaptive Noise Cancellation System
- **Task:** Build a real-time noise cancellation pipeline
- **Components:**
  1. Adaptive LMS filter with configurable filter length
  2. Double-talk detection (Geigel algorithm, cross-correlation)
  3. Comfort noise injection during suppression
  4. Fixed-point implementation for ARM Cortex-M4 target
- **Performance:** <10ms latency, <5% CPU on target
- **Deliverable:** C implementation with unit tests, latency measurements, comparison with SpeexDSP

---

## Module 4: Multirate Signal Processing & Resampling

**Duration:** 15 hours  
**Level:** Advanced

### 4.1 Decimation and Interpolation
- **Decimation by M:** Anti-aliasing requirement, polyphase decomposition
- **Interpolation by L:** Anti-imaging requirement, polyphase implementation
- **Rational sampling rate conversion:** L/M conversion, polyphase efficiency
- **Arbitrary resampling:** Farrow structure, polynomial interpolation, cubic splines
- **Production context:**
  - Audio resampling: 44.1kHz ↔ 48kHz (SRC problem)
  - Image scaling: bicubic, Lanczos, polyphase for video
  - Feature map resizing in CNNs: bilinear vs. learned upsampling

### 4.2 Polyphase Filter Structures
- **Polyphase decomposition:** Type I, II, III, IV
- **Efficient implementations:** Commutator model, parallel processing
- **Noble identities:** Moving decimators/interpolators past filters
- **Cascaded integrator-comb (CIC) filters:** Multiplier-free decimation/interpolation
- **Production context:**
  - Software-defined radio (SDR) frontends
  - Video processing pipelines (deinterlacing, frame rate conversion)
  - Efficient attention downsampling in hierarchical transformers

### 4.3 Multiresolution Analysis & Wavelets
- **Continuous wavelet transform (CWT):** Mother wavelets, scale, translation
- **Discrete wavelet transform (DWT):** Mallat's algorithm, filter bank implementation
- **Wavelet packets:** Adaptive time-frequency tiling
- **Lifting scheme:** In-place computation, integer-to-integer transforms
- **Production context:**
  - Image denoising (wavelet thresholding)
  - Time-series anomaly detection (multi-scale analysis)
  - JPEG 2000, ICER ( Mars rover image compression)

### 4.4 Lab: High-Performance Video Resampling Pipeline
- **Task:** Build a GPU-accelerated video resampling system
- **Requirements:**
  - Support arbitrary input/output resolutions and frame rates
  - Polyphase Lanczos resampling with antialiasing
  - Handle YUV 4:2:0, 4:2:2, 4:4:4 formats
  - Process 4K@60fps on single GPU with <1 frame latency
- **Deliverable:** CUDA implementation, quality metrics (SSIM, PSNR), performance profiling

---

## Module 5: Graph Theory Foundations for AI Systems

**Duration:** 20 hours  
**Level:** Beginner → Intermediate

### 5.1 Graph Representations & Data Structures
- **Formal definitions:** Graph G=(V,E), directed/undirected, weighted, bipartite, multipartite
- **Adjacency matrix:** Dense vs. sparse, properties (symmetric, irreducible)
- **Adjacency list:** CSR, CSC, COO — memory footprints, traversal efficiency
- **Incidence matrix:** Node-edge relationships, circuit theory connections
- **Laplacian matrix:** Combinatorial Laplacian L = D - A, normalized versions
- **Edge list formats:** CSV, Parquet, binary edge list, property graph models
- **Production context:**
  - Storage formats for billion-edge graphs (Adjacency list in RocksDB, TigerGraph format)
  - Graph serialization: Protocol Buffers, FlatBuffers for zero-copy deserialization
  - Memory-mapped graph storage for out-of-core processing

### 5.2 Graph Traversal Algorithms & Systems
- **Breadth-first search (BFS):** Level-synchronous, queue-based, parallelization strategies
- **Depth-first search (DFS):** Recursive, iterative, applications in cycle detection
- **Topological sort:** Kahn's algorithm, DFS-based, applications in DAGs
- **Shortest paths:** Dijkstra, Bellman-Ford, Floyd-Warshall, Johnson's algorithm
- **All-pairs shortest paths:** Hierarchical methods, landmark-based approximation
- **Production context:**
  - Neo4j, Amazon Neptune query execution plans
  - Graph traversal in recommendation systems (Pinterest, LinkedIn)
  - Dependency resolution in build systems and package managers

### 5.3 Connectivity & Structure
- **Connected components:** Undirected (union-find), directed (strongly connected components — Kosaraju, Tarjan)
- **Bridges and articulation points:** Critical infrastructure identification
- **Biconnected components:** Block-cut tree, reliability analysis
- **Graph minors, treewidth:** Structural parameters for algorithm design
- **Production context:**
  - Identifying single points of failure in distributed systems
  - Community boundary detection in social networks
  - Compiler optimization (control flow graph analysis)

### 5.4 Centrality & Importance Measures
- **Degree centrality:** Local importance, weighted variants
- **Closeness centrality:** Average shortest path, harmonic centrality
- **Betweenness centrality:** Brandes' algorithm, approximation for large graphs
- **Eigenvector centrality, PageRank:** Power iteration, random walk interpretation, damping factor
- **Katz centrality, HITS:** Hub and authority scores
- **Production context:**
  - PageRank for web search (Google, Bing)
  - Identifying influencers in social networks
  - Critical node identification in infrastructure networks
  - Node importance in graph neural network explainability

### 5.5 Lab: Building a Graph Query Engine
- **Task:** Implement an in-memory graph database supporting basic queries
- **Requirements:**
  - CSR-based storage with dynamic updates
  - BFS, DFS, shortest path, PageRank queries
  - Cypher-like query parser (subset)
  - Handle 10M nodes, 100M edges in <32GB RAM
- **Deliverable:** C++ implementation with benchmarks against NetworkX, igraph

---

## Module 6: Spectral Graph Theory & Graph Signal Processing

**Duration:** 25 hours  
**Level:** Advanced

### 6.1 Graph Laplacian & Spectral Properties
- **Combinatorial Laplacian:** L = D - A, properties (positive semi-definite, null space)
- **Normalized Laplacians:** L_sym = D^(-1/2) L D^(-1/2), L_rw = D^(-1) L
- **Eigenvalues and eigenvectors:** Fiedler value, spectral gap, algebraic connectivity
- **Courant-Fischer theorem:** Variational characterization of eigenvalues
- **Cheeger inequality:** Isoperimetric number, graph partitioning
- **Production context:**
  - Spectral clustering for document/topic organization
  - Fiedler vector for graph bisection (METIS, Scotch)
  - Algebraic connectivity as a network robustness metric

### 6.2 Spectral Clustering & Graph Cuts
- **Graph cuts:** Min-cut, ratio cut, normalized cut, conductance
- **Spectral clustering algorithm:** Laplacian embedding, k-means in spectral space
- **Multilevel methods:** Coarsening, partitioning, uncoarsening (METIS, KaHIP)
- **Streaming and dynamic clustering:** Incremental spectral updates
- **Production context:**
  - Image segmentation (Shi-Malik normalized cuts)
  - Document clustering in RAG systems
  - Customer segmentation in fraud detection
  - Load balancing in distributed graph processing

### 6.3 Graph Fourier Transform (GFT)
- **Definition:** Projection onto Laplacian eigenvectors
- **Graph frequency:** Variation of eigenvectors (smooth vs. oscillatory)
- **Graph convolution theorem:** Spectral filtering via eigenvalue modulation
- **Computational challenges:** O(n³) eigendecomposition, polynomial approximations
- **Production context:**
  - Graph signal smoothing for denoising
  - Graph convolutional layers as spectral filters
  - Heat kernel smoothing on meshes (computer graphics)

### 6.4 Graph Filtering & Signal Recovery
- **Graph filters:** FIR and IIR on graphs, polynomial of Laplacian
- **Chebyshev polynomial approximation:** Efficient spectral filtering without full eigendecomposition
- **Graph Wiener filtering:** Optimal denoising on graphs
- **Semi-supervised learning:** Label propagation, graph regularization
- **Production context:**
  - Denoising node features in knowledge graphs
  - Recommender systems as graph signal recovery
  - Semi-supervised node classification (Cora, Citeseer, Pubmed)

### 6.5 Lab: Spectral Clustering at Scale
- **Task:** Implement spectral clustering for a 1M-node graph
- **Requirements:**
  - Use randomized SVD or Lanczos method for partial eigendecomposition
  - Implement multilevel coarsening for acceleration
  - Compare with k-means++ on raw features
  - Evaluate on benchmark: Amazon product co-purchasing graph
- **Deliverable:** Python/C++ implementation with scalability analysis, quality metrics (conductance, modularity)

---

## Module 7: Graph Neural Networks & Message Passing

**Duration:** 30 hours  
**Level:** Advanced → Expert

### 7.1 Message Passing Neural Networks (MPNN)
- **General MPNN framework:** Message, aggregate, update functions
- **Graph Convolutional Network (GCN):** Spectral motivation, first-order approximation
- **GraphSAGE:** Sampling, aggregation (mean, LSTM, pooling), inductive learning
- **Graph Attention Network (GAT):** Attention mechanisms, multi-head attention
- **GIN (Graph Isomorphism Network):** Weisfeiler-Lehman test, expressiveness
- **Production context:**
  - Node classification: fraud detection, protein function prediction
  - Graph classification: molecular property prediction (MPNN in drug discovery)
  - Link prediction: recommendation systems, knowledge graph completion

### 7.2 Spectral GNNs & Polynomial Filters
- **ChebNet:** Chebyshev polynomial of Laplacian, K-localized filters
- **CayleyNet:** Rational spectral filters via Cayley transform
- **ARMA filters:** Autoregressive moving average on graphs
- **Graph heat kernel:** Diffusion-based smoothing
- **Production context:**
  - Why ChebNet matters: avoids O(n³) eigendecomposition
  - Spectral filters for mesh processing in computer graphics
  - ARMA filters for long-range dependencies

### 7.3 Spatial GNNs & Neighborhood Aggregation
- **MPNN instantiations:** NNConv, EdgeConv, GatedGraphConv
- **Jumping Knowledge networks:** Addressing oversmoothing
- **Deep Graph Library (DGL) abstractions:** Message passing on edges, node updates
- **PyTorch Geometric (PyG):** Sparse tensor operations, neighborhood sampling
- **Production context:**
  - DGL vs. PyG: memory layout trade-offs, when to choose which
  - Implementing custom message passing for heterogeneous graphs
  - GPU memory management: neighbor sampling, subgraph extraction

### 7.4 Scalable GNN Training
- **Neighbor sampling:** GraphSAGE-style, layer-wise sampling, importance sampling
- **Cluster-GCN:** Subgraph-based training, METIS partitioning
- **GraphSAINT:** Random walk sampling, importance sampling
- **SIGN, SGC:** Precomputing graph diffusion, removing neighborhood expansion
- **Production context:**
  - Training on billion-edge graphs (Pinterest, Alibaba)
  - Mini-batch training vs. full-graph training trade-offs
  - Feature caching, graph partitioning for distributed training

### 7.5 Heterogeneous Graphs & Relational Learning
- **Relational GCN (R-GCN):** Relation-specific weights, basis decomposition
- **Heterogeneous Graph Transformer (HGT):** Node-type, edge-type aware attention
- **Knowledge graph embeddings:** TransE, RotatE, ComplEx, DistMult
- **Reasoning on knowledge graphs:** Path-based, embedding-based, neural-symbolic
- **Production context:**
  - Amazon product graph: items, customers, reviews, brands
  - Medical knowledge graphs: diseases, symptoms, drugs, genes
  - Enterprise knowledge graphs: documents, entities, relationships

### 7.6 Temporal Graphs & Dynamic GNNs
- **Discrete-time dynamic graphs:** Snapshots, time-aware aggregation
- **Continuous-time dynamic graphs:** Temporal point processes, TGAT, TGN
- **Streaming graph updates:** Incremental embeddings, temporal random walks
- **Production context:**
  - Real-time fraud detection on transaction graphs
  - Social network evolution prediction
  - Temporal recommendation systems

### 7.7 Lab: Production GNN Inference System
- **Task:** Build a GNN inference service for a recommendation system
- **Requirements:**
  - Support GraphSAGE with neighbor sampling (k=2, fanout=[10, 10])
  - Handle 10M users, 100M items, 1B interactions
  - P99 latency <50ms for single-node inference
  - Batch inference with dynamic batching
  - Model versioning, A/B testing infrastructure
- **Deliverable:** Full system with gRPC API, Redis for feature cache, DGL/PyG backend, load testing with Locust, monitoring with Prometheus/Grafana

---

## Module 8: Large-Scale Graph Systems & Distributed Graph Processing

**Duration:** 25 hours  
**Level:** Expert

### 8.1 Graph Partitioning & Distribution
- **Edge-cut partitioning:** METIS, KaHIP, spectral partitioning
- **Vertex-cut partitioning:** PowerLyra, Ginger, streaming partitioning
- **Balanced partitioning:** Load balancing, communication minimization
- **Dynamic repartitioning:** Workload-aware, elasticity
- **Production context:**
  - PowerGraph (GraphLab): vertex-cut for power-law graphs
  - Facebook's social graph partitioning
  - Graph partitioning in GNN training (DistDGL)

### 8.2 Distributed Graph Processing Frameworks
- **Pregel model:** Bulk Synchronous Parallel (BSP), vertex-centric programming
- **Giraph, GraphX:** Apache ecosystem implementations
- **PowerGraph:** Gather-Apply-Scatter (GAS), vertex-cut, asynchronous execution
- **GraphLab, Dato:** Shared-memory, asynchronous, consistency models
- **Modern systems:** DGL-KE, DistDGL, AliGraph, Euler
- **Production context:**
  - PageRank at Google scale (Pregel paper)
  - Triangle counting in social networks
  - Distributed GNN training on GPU clusters

### 8.3 Graph Storage & Retrieval Systems
- **Graph databases:** Neo4j, Amazon Neptune, JanusGraph, ArangoDB
- **RDF stores:** Apache Jena, Virtuoso, GraphDB
- **Key-value adaptations:** TitanDB (Cassandra/HBase), RedisGraph
- **Graph query languages:** Cypher, Gremlin, SPARQL, GSQL
- **Production context:**
  - Query optimization in graph databases
  - Index-free adjacency vs. index-based traversal
  - Graph storage for RAG systems (knowledge graph retrieval)

### 8.4 Graph Sampling & Approximation
- **Random walk sampling:** Uniform, Metropolis-Hastings, rejection sampling
- **Forest fire, snowball sampling:** Bias analysis
- **Graph sparsification:** Spectral sparsification, effective resistance sampling
- **Sketching:** Count-Min, HyperLogLog for graph statistics
- **Production context:**
  - Representative subgraph extraction for visualization
  - Approximate centrality for billion-node graphs
  - Streaming graph algorithms (counting triangles, connected components)

### 8.5 Lab: Distributed Graph Analytics Platform
- **Task:** Build a distributed PageRank and connected components system
- **Requirements:**
  - Process 1B-edge graph on 4-node cluster
  - Implement Pregel-style BSP and asynchronous modes
  - Handle dynamic edge insertions/deletions
  - Fault tolerance: checkpointing, recovery
  - Performance: PageRank convergence in <5 minutes
- **Deliverable:** C++/Rust system with MPI or gRPC communication, benchmarking against Giraph/GraphX, failure injection tests

---

## Module 9: Production Integration — Signal & Graph Pipelines

**Duration:** 20 hours  
**Level:** Expert

### 9.1 End-to-End Signal Processing Pipelines
- **Pipeline architecture:** Ingestion → preprocessing → feature extraction → model input
- **Stream processing:** Apache Kafka, Flink, Spark Streaming for signal data
- **Real-time constraints:** Latency budgets, jitter analysis, deadline scheduling
- **Quality of Service:** Admission control, backpressure, graceful degradation
- **Production context:**
  - Real-time audio processing pipeline (Zoom, Discord)
  - Sensor data fusion in autonomous vehicles
  - Video preprocessing for computer vision models

### 9.2 Graph-Based Retrieval & RAG Systems
- **Knowledge graphs for RAG:** Entity linking, relation extraction, graph traversal
- **Graph-enhanced retrieval:** Hybrid dense-sparse retrieval, graph-based reranking
- **Multi-hop reasoning:** Path retrieval, subgraph extraction for LLM context
- **Graph vector databases:** Combining graph traversal with vector similarity (Neo4j + Pinecone)
- **Production context:**
  - Microsoft GraphRAG, Google's Knowledge Graph Search
  - Enterprise RAG with domain knowledge graphs
  - Legal/medical document retrieval with citation graphs

### 9.3 Monitoring, Debugging & Observability
- **Signal pipeline monitoring:** SNR tracking, drift detection, spectral change alerts
- **Graph system monitoring:** Query latency, cache hit rates, partition balance
- **Numerical debugging:** Identifying instability in IIR filters, Laplacian conditioning
- **Distributed debugging:** Tracing message passing, identifying stragglers
- **Production context:**
  - Setting SLOs for audio quality in production
  - Detecting graph query performance regression
  - Root-causing GNN training divergence

### 9.4 Performance Engineering & Optimization
- **Signal processing:** SIMD vectorization, fixed-point arithmetic, lookup tables
- **Graph processing:** Cache-friendly layouts, prefetching, compression
- **GPU optimization:** Kernel fusion, memory coalescing, stream parallelism
- **Distributed optimization:** Communication compression, asynchronous updates
- **Production context:**
  - Optimizing STFT for mobile deployment (CoreML, TFLite)
  - Graph compression for edge caching (WebGraph framework)
  - Mixed-precision GNN training

### 9.5 Lab: Production-Grade Multimodal Pipeline
- **Task:** Build a system that processes audio + knowledge graph for a voice assistant
- **Components:**
  1. Real-time audio stream → STFT → Mel-spectrogram → CNN feature extractor
  2. ASR output → entity linking → knowledge graph query
  3. Graph traversal for context expansion → LLM prompt augmentation
  4. Response generation with latency <200ms end-to-end
- **Deliverable:** Full microservices architecture, Kubernetes deployment, load testing, monitoring dashboard, incident response runbook

---

## Module 10: Advanced Topics & Research Frontiers

**Duration:** 15 hours  
**Level:** Expert → Research

### 10.1 Advanced Spectral Methods
- **Nonlinear dimensionality reduction:** Laplacian eigenmaps, diffusion maps
- **Manifold learning:** Isomap, LLE, t-SNE, UMAP — spectral connections
- **Spectral graph theory in ML theory:** Generalization bounds for GNNs
- **Random matrix theory:** Eigenvalue distributions of random graphs

### 10.2 Neural Signal Processing
- **Differentiable digital signal processing (DDSP):** Neural audio synthesis
- **Neural operators:** Fourier Neural Operator (FNO), learning solution operators
- **Implicit neural representations:** SIREN, Fourier features for signals
- **Production context:** 
  - Real-time neural audio synthesis (NSynth, DDSP)
  - Physics-informed neural networks for PDE solving
  - Neural radiance fields (NeRF) as signal representations

### 10.3 Graph Transformers & Beyond
- **Graph Transformer architectures:** SAN, Graphormer, TokenGT
- **Graph prompting:** Pre-training, fine-tuning, zero-shot transfer
- **Large graph models:** Scaling laws for GNNs, graph foundation models
- **Production context:**
  - Molecular foundation models (GraphGPT, Uni-Mol)
  - Social network foundation models
  - Graph-based multimodal learning

### 10.4 Quantum Graph Signal Processing
- **Quantum walks on graphs:** Continuous-time quantum walks
- **Quantum graph algorithms:** Quantum speedups for graph problems
- **Production context:** Near-term quantum advantage in graph optimization

### 10.5 Lab: Research Replication Project
- **Task:** Replicate a recent NeurIPS/ICML paper at the intersection of signal processing and graph theory
- **Examples:**
  - "Graph Signal Processing for Directed Graphs" (recent advances)
  - "Fourier Neural Operator for Parametric PDEs"
  - "Scalable Graph Neural Networks via Spectral Sparsification"
- **Deliverable:** Reproduced results, code repository, critical analysis, extension proposal

---

## Capstone Projects

Students choose ONE project to demonstrate mastery:

### Capstone A: Real-Time Audio Intelligence Platform
- **Scope:** End-to-end system for real-time audio analysis
- **Components:**
  - Multi-channel audio acquisition (microphone array)
  - GPU-accelerated STFT + source separation (ICA, beamforming)
  - ASR with custom language model
  - Speaker diarization via graph clustering
  - Knowledge graph query for domain-specific responses
- **Deliverables:** Working system, performance benchmarks, demo video, architecture document

### Capstone B: Billion-Scale Recommendation Graph
- **Scope:** Production-grade recommendation system using graph neural networks
- **Components:**
  - Graph construction from user-item interactions (1B+ edges)
  - Distributed GNN training (GraphSAGE + Cluster-GCN)
  - Real-time inference service (<50ms P99)
  - A/B testing framework, online evaluation
- **Deliverables:** System in production-like environment, evaluation report, business metrics analysis

### Capstone C: Scientific Computing Pipeline
- **Scope:** Signal/graph processing for scientific simulation
- **Components:**
  - PDE solver using spectral methods (FFT-based)
  - Mesh generation and graph-based domain decomposition
  - Neural operator surrogate model
  - Distributed training on simulation data
- **Deliverables:** Published-quality code, convergence analysis, scaling study

---

## Assessment & Evaluation Framework

### Continuous Assessment (40%)
| Component | Weight | Description |
|-----------|--------|-------------|
| Lab implementations | 20% | Code quality, correctness, performance |
| Lab reports | 10% | Design decisions, profiling analysis |
| Peer review | 10% | Reviewing others' code and architecture docs |

### Examinations (30%)
- **Midterm (15%):** Signal processing theory, graph algorithms, systems design
- **Final (15%):** Advanced spectral methods, distributed systems, production engineering

### Capstone Project (30%)
| Criterion | Weight |
|-----------|--------|
| Technical correctness | 10% |
| System design & architecture | 10% |
| Performance & scalability | 5% |
| Documentation & presentation | 5% |

### Grading Rubric
- **A (90-100):** Publication-quality work, novel insights, production-ready
- **B (80-89):** Solid understanding, minor gaps, good engineering
- **C (70-79):** Adequate understanding, significant gaps, needs improvement
- **D (60-69):** Partial understanding, major gaps
- **F (<60):** Insufficient understanding

---

## Recommended Tools, Libraries & Infrastructure

### Signal Processing
| Tool | Purpose | Production Relevance |
|------|---------|---------------------|
| **NumPy/SciPy** | Baseline implementations | Reference implementations |
| **PyTorch/torchaudio** | GPU-accelerated audio | Deep learning integration |
| **librosa** | Music/audio analysis | Feature extraction |
| **FFTW** | High-performance FFT | Gold standard for CPU FFT |
| **cuFFT/rocFFT** | GPU FFT | NVIDIA/AMD GPU acceleration |
| **SoX/ffmpeg** | Audio conversion | Production audio pipelines |
| **JACK/PortAudio** | Real-time audio I/O | Low-latency audio systems |
| **MATLAB (optional)** | Prototyping | Academic reference |

### Graph Processing
| Tool | Purpose | Production Relevance |
|------|---------|---------------------|
| **NetworkX** | Algorithm prototyping | Education, small graphs |
| **igraph** | High-performance graph algorithms | Medium-scale analysis |
| **Graph-tool** | Parallel graph algorithms | CPU-intensive workloads |
| **Neo4j** | Graph database | Production graph storage |
| **DGL** | Deep graph learning | GNN research & production |
| **PyTorch Geometric** | GNN implementations | Active research, production |
| **GraphX/Giraph** | Distributed graph processing | Apache ecosystem |
| **TigerGraph** | Native parallel graph DB | Enterprise graph analytics |

### Systems & Infrastructure
| Tool | Purpose |
|------|---------|
| **Docker/Kubernetes** | Containerization, orchestration |
| **gRPC/Apache Thrift** | Service communication |
| **Redis/Memcached** | Feature caching |
| **Apache Kafka** | Stream ingestion |
| **Prometheus/Grafana** | Monitoring, observability |
| **MLflow/Weights & Biases** | Experiment tracking |
| **CUDA/ROCm** | GPU programming |
| **MPI/OpenMP** | Distributed/parallel computing |

---

## References & Further Reading

### Signal Processing Classics
1. **Oppenheim & Schafer,** *Discrete-Time Signal Processing* (3rd Ed.) — The canonical reference
2. **Proakis & Manolakis,** *Digital Signal Processing* — Comprehensive, mathematically rigorous
3. **Mallat,** *A Wavelet Tour of Signal Processing* — Wavelets and multiresolution
4. **Vetterli, Kovačević, & Goyal,** *Foundations of Signal Processing* — Modern, Fourier-free approach
5. **Lyons,** *Understanding Digital Signal Processing* — Intuitive, practical

### Graph Theory & Algorithms
1. **Bondy & Murty,** *Graph Theory* — Classic, rigorous
2. **Diestel,** *Graph Theory* (5th Ed.) — Modern, concise
3. **Newman,** *Networks* — Network science perspective
4. **Easley & Kleinberg,** *Networks, Crowds, and Markets* — Interdisciplinary
5. **Leskovec, Rajaraman, & Ullman,** *Mining of Massive Datasets* — Large-scale algorithms

### Spectral Graph Theory & Graph Signal Processing
1. **Chung,** *Spectral Graph Theory* — The definitive mathematical reference
2. **Shuman et al.,** "The Emerging Field of Signal Processing on Graphs" — Foundational survey
3. **Ortega,** *Introduction to Graph Signal Processing* — Comprehensive textbook
4. **Stanković et al.,** *Graph Signal Processing* — Recent advances

### Graph Neural Networks
1. **Hamilton,** *Graph Representation Learning* — Excellent introduction
2. **Wu et al.,** "A Comprehensive Survey on Graph Neural Networks" — Broad overview
3. **Zhou et al.,** "Graph Neural Networks: A Review of Methods and Applications" — Applications focus
4. **Kipf & Welling,** "Semi-Supervised Classification with Graph Convolutional Networks" — GCN paper
5. **Veličković et al.,** "Graph Attention Networks" — GAT paper
6. **Hamilton et al.,** "Inductive Representation Learning on Large Graphs" — GraphSAGE paper

### Systems & Production
1. **Gonzalez et al.,** "PowerGraph: Distributed Graph-Parallel Computation on Natural Graphs" — PowerGraph
2. **Ma et al.,** "Deep Graph Library: A Graph-Centric, Highly-Performant Package for Graph Neural Networks" — DGL
3. **Fey & Lenssen,** "Fast Graph Representation Learning with PyTorch Geometric" — PyG
4. **Zheng et al.,** "DistDGL: Distributed Graph Neural Network Training for Billion-Scale Graphs" — Distributed GNN
5. **Zhang et al.,** "GraphSAINT: Graph Sampling Based Inductive Learning Method" — Scalable training

### Research Papers (Selected)
- **Shi & Malik,** "Normalized Cuts and Image Segmentation" — Spectral clustering
- **Defferrard et al.,** "Convolutional Neural Networks on Graphs with Fast Localized Spectral Filtering" — ChebNet
- **Klicpera et al.,** "Predict then Propagate: Graph Neural Networks meet Personalized PageRank" — APPNP
- **Chiang et al.,** "Cluster-GCN: An Efficient Algorithm for Training Deep and Large Graph Convolutional Networks" — Cluster-GCN
- **Hu et al.,** "OGB-LSC: A Large-Scale Challenge for Machine Learning on Graphs" — Benchmarks

---

## Appendix A: Mathematical Notation Reference

| Symbol | Meaning |
|--------|---------|
| $x[n]$ | Discrete-time signal |
| $X(e^{j\omega})$ | DTFT |
| $X[k]$ | DFT |
| $h[n]$ | Impulse response |
| $H(z)$ | Transfer function |
| $G = (V, E)$ | Graph with vertices $V$ and edges $E$ |
| $A$ | Adjacency matrix |
| $D$ | Degree matrix |
| $L$ | Graph Laplacian |
| $\lambda_i$ | Eigenvalue of Laplacian |
| $\mathbf{u}_i$ | Eigenvector of Laplacian |
| $\hat{x}$ | Graph Fourier transform of signal $x$ |

## Appendix B: Complexity Cheat Sheet

| Operation | Naive | Optimized | Hardware |
|-----------|-------|-----------|----------|
| DFT | $O(N^2)$ | $O(N \log N)$ FFT | CPU/GPU |
| Convolution | $O(N^2)$ | $O(N \log N)$ FFT-based | CPU/GPU |
| Matrix-vector multiply | $O(N^2)$ | $O(N^2)$ (memory-bound) | GPU |
| BFS | $O(V + E)$ | $O(V + E)$ | CPU |
| PageRank | $O(T \cdot E)$ | $O(T \cdot E)$, parallel | CPU/GPU |
| GCN forward | $O(L \cdot E \cdot d^2)$ | $O(L \cdot E \cdot d^2)$ | GPU |
| Spectral clustering | $O(N^3)$ | $O(N \cdot k^2)$ randomized | CPU/GPU |

## Appendix C: Production Checklist

Before deploying any signal processing or graph system to production, verify:

- [ ] **Correctness:** Unit tests pass, property-based tests pass, golden reference comparisons pass
- [ ] **Performance:** Benchmarked against SOTA, latency/throughput SLOs met
- [ ] **Scalability:** Tested at 10x expected peak load, horizontal scaling validated
- [ ] **Reliability:** Fault injection tested, graceful degradation verified
- [ ] **Observability:** Metrics, logs, traces instrumented, alerts configured
- [ ] **Security:** Input validation, access control, data encryption verified
- [ ] **Maintainability:** Documentation complete, runbooks written, onboarding guide ready
- [ ] **Cost:** Resource utilization optimized, auto-scaling configured, cost projections reviewed

---

**End of Syllabus**

*This document is designed to be self-contained, publication-quality, and ready for deployment as a GitHub repository or internal technical curriculum. Each module can be expanded into a full course with lecture notes, lab assignments, and assessment rubrics.*

---

## File: signal-processing-graph-theory-syllabus.md