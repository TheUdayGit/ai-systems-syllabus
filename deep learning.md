  
  
    ## File: deep-learning-syllabus.md

# Deep Learning

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Mathematical Foundations](#module-0-mathematical-foundations)
5. [Module 1: Neural Network Foundations — From Perceptrons to Universal Approximators](#module-1-neural-network-foundations)
6. [Module 2: Backpropagation & Automatic Differentiation — The Engine of Deep Learning](#module-2-backpropagation--automatic-differentiation)
7. [Module 3: Optimization — Gradient Descent, Adaptive Methods & Second-Order Techniques](#module-3-optimization)
8. [Module 4: Convolutional Neural Networks — The Visual Cortex of AI](#module-4-convolutional-neural-networks)
9. [Module 5: Recurrent Neural Networks & Sequence Modeling](#module-5-recurrent-neural-networks--sequence-modeling)
10. [Module 6: The Transformer Revolution — Attention Is All You Need](#module-6-the-transformer-revolution)
11. [Module 7: Generative Models — VAEs, GANs, Diffusion & Flows](#module-7-generative-models)
12. [Module 8: Self-Supervised & Contrastive Learning](#module-8-self-supervised--contrastive-learning)
13. [Module 9: Distributed Training at Scale — Data, Model & Pipeline Parallelism](#module-9-distributed-training-at-scale)
14. [Module 10: Training Stability — Mixed Precision, Normalization & Regularization](#module-10-training-stability)
15. [Module 11: Neural Architecture Search & Automated Deep Learning](#module-11-neural-architecture-search)
16. [Module 12: Deep Learning for Computer Vision — Object Detection, Segmentation & Generation](#module-12-deep-learning-for-computer-vision)
17. [Module 13: Deep Learning for NLP — From Word Embeddings to LLMs](#module-13-deep-learning-for-nlp)
18. [Module 14: Production Deep Learning — Serving, Optimization & MLOps](#module-14-production-deep-learning)
19. [Capstone Project](#capstone-project)
20. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
21. [Appendix B: Tooling Matrix](#appendix-b-tooling-matrix)
22. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

Deep Learning is not about stacking layers and hoping for convergence. It is a **systems engineering discipline** at the intersection of:

- **Applied Mathematics**: differential geometry of loss landscapes, spectral analysis of Hessians, information geometry
- **Computer Science**: automatic differentiation, memory hierarchies, parallel algorithms, compiler optimization
- **Signal Processing**: convolution, filtering, spectral analysis, time-frequency representations
- **Systems Engineering**: distributed GPU clusters, InfiniBand topology, NCCL collectives, checkpointing strategies
- **Cognitive Science**: inductive biases, representation learning, emergent capabilities, neural coding

The modern deep learning production stack must handle:
- **Billion-parameter models** trained across thousands of GPUs with 3D parallelism and fault tolerance
- **Mixed precision training** (FP16/BF16/FP8) achieving 3× speedup on Tensor Cores while maintaining numerical stability
- **Attention mechanisms** processing sequences of 1M+ tokens with sub-quadratic complexity
- **Generative models** producing photorealistic images, coherent video, and structured 3D scenes
- **Self-supervised learning** extracting representations from unlabeled data at scale
- **Real-time inference** at p99 < 10ms with quantization, pruning, and kernel fusion

This course progresses from **mathematical foundations** → **core architectures** → **training at scale** → **generative models** → **production systems**, with each module building a complete mental model connecting first principles to GPU kernel-level implementation.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building production deep learning systems
- ML Infrastructure Engineers designing distributed training platforms
- Computer Vision Engineers developing perception systems
- NLP Engineers building language understanding pipelines
- Staff-level candidates preparing for deep learning architecture interviews

### Prerequisites
- **Solid Python**: NumPy, PyTorch/TensorFlow, data structures, OOP
- **Mathematics**: linear algebra, multivariate calculus, probability & statistics
- **Machine Learning**: supervised learning, bias-variance, cross-validation, regularization
- **Computer Systems**: memory hierarchies, parallel computing basics
- **Software Engineering**: Git, debugging, profiling, testing

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Derive** backpropagation from first principles and implement automatic differentiation engines
2. **Architect** distributed training systems using data, tensor, and pipeline parallelism across GPU clusters
3. **Design** CNN, RNN, and Transformer architectures with proper inductive biases for specific domains
4. **Train** generative models (VAEs, GANs, diffusion) with stable convergence
5. **Implement** self-supervised learning algorithms that learn representations without labels
6. **Optimize** training with mixed precision, gradient checkpointing, and memory-efficient attention
7. **Debug** training failures using gradient flow analysis, loss landscape visualization, and distributed tracing
8. **Deploy** models with quantization, pruning, knowledge distillation, and optimized inference kernels
9. **Evaluate** models beyond accuracy using robustness, fairness, and interpretability metrics
10. **Build** production pipelines with experiment tracking, model versioning, and automated deployment

---

## Module 0: Mathematical Foundations

### 0.1 Differential Geometry of Loss Landscapes
- **Loss surfaces**: visualization, critical points, saddle points, local minima
- **Hessian analysis**: eigenvalue spectrum, condition number, flat vs sharp minima
- **Gradient flow**: gradient descent as gradient flow on Riemannian manifold
- **Information geometry**: Fisher information metric, natural gradient descent
- **Sharpness-aware minimization (SAM)**: minimizing loss + sharpness for better generalization

### 0.2 Spectral Analysis & Fourier Methods
- **Discrete Fourier Transform (DFT)**: convolution theorem, fast convolution
- **Spectral analysis of weights**: singular value decomposition of weight matrices
- **Frequency-domain training**: Fourier features, implicit neural representations
- **Wavelet transforms**: multi-resolution analysis, sparse representations

### 0.3 Probability & Information Theory
- **Entropy, cross-entropy, KL divergence**: connections to maximum likelihood
- **Mutual information**: measuring dependence between representations
- **Variational bounds**: ELBO, InfoNCE, contrastive predictive coding
- **Maximum entropy**: principle and applications in regularization

### 0.4 Optimization Theory
- **Convexity**: convex sets, convex functions, Jensen's inequality
- **Lipschitz continuity**: L-smoothness, strong convexity, convergence rates
- **Stochastic approximation**: Robbins-Monro conditions, Polyak averaging
- **Momentum as ODE**: continuous-time interpretation of optimization dynamics

### 0.5 Reading
- *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong, Ch. 5-7
- *Information Theory and Statistical Learning* — Principe et al.
- *Optimization Methods for Large-Scale Machine Learning* — Bottou, Curtis, Nocedal

---

## Module 1: Neural Network Foundations — From Perceptrons to Universal Approximators

### 1.1 The Perceptron & Biological Inspiration
- **McCulloch-Pitts neuron**: threshold logic, boolean function implementation
- **Rosenblatt's perceptron**: learning rule, convergence proof, linear separability
- **Biological neurons**: dendrites, axons, synapses, action potentials, Hebbian learning
- **The XOR problem**: why single-layer perceptrons fail, need for nonlinearity

### 1.2 Multi-Layer Perceptrons (MLPs)
- **Universal approximation theorem**: Cybenko (1989), Hornik (1991) — proof sketch
- **Forward propagation**: layer-wise computation, activation functions
- **Activation functions**:
  - **Sigmoid**: σ(x) = 1/(1+e^(-x)), vanishing gradient problem
  - **Tanh**: centered at zero, still suffers vanishing gradients
  - **ReLU**: max(0,x), dying ReLU problem, biological plausibility
  - **Leaky ReLU**: αx for x<0, parametric ReLU (PReLU)
  - **GELU**: x·Φ(x), smooth approximation to ReLU, used in Transformers
  - **Swish/SiLU**: x·σ(x), self-gated, discovered by NAS
  - **Mish**: x·tanh(softplus(x)), smooth, non-monotonic
- **Output activations**: softmax (classification), linear (regression), sigmoid (binary)

### 1.3 Weight Initialization
- **Xavier/Glorot initialization**: uniform/normal, based on fan-in + fan-out
  - `W ~ U[-√(6/(fan_in+fan_out)), √(6/(fan_in+fan_out))]`
- **He initialization**: for ReLU, `W ~ N(0, √(2/fan_in))`
- **Orthogonal initialization**: QR decomposition, preserves norms through layers
- **Fixup initialization**: no normalization needed, scale residual branches

### 1.4 Loss Functions
- **Regression**: MSE, MAE, Huber loss, quantile loss
- **Classification**: cross-entropy, focal loss, label smoothing
- **Ranking**: pairwise, listwise, NDCG-based losses
- **Multi-task**: weighted sum, uncertainty weighting, gradient surgery

### 1.5 Lab: Build an MLP from Scratch
- Implement forward and backward pass with NumPy
- Compare different activation functions on gradient flow
- Experiment with weight initialization strategies
- Visualize loss landscape with random 2D projections

---

## Module 2: Backpropagation & Automatic Differentiation — The Engine of Deep Learning

### 2.1 The Chain Rule & Computational Graphs
- **Computational graphs**: nodes (operations), edges (data flow), DAG structure
- **Forward mode AD**: Jacobian-vector products, efficient for n << m
- **Reverse mode AD**: vector-Jacobian products (VJP), efficient for n >> m
- **Backpropagation**: reverse mode AD applied to neural networks
- **Complexity**: O(network size) for both forward and backward passes

### 2.2 Implementing Autograd
- **Tape/Wengert list**: recording operations during forward pass
- **Gradient accumulation**: ∂L/∂x = Σ (∂L/∂y_i · ∂y_i/∂x) for multiple consumers
- **In-place operations**: breaking the computation graph, memory aliasing
- **Control flow**: handling loops, conditionals, recursion in AD

### 2.3 Modern Autograd Systems
- **PyTorch Autograd**: dynamic graphs, `torch.autograd.Function`, custom backward
- **TensorFlow GradientTape**: eager execution, tape watching, nested tapes
- **JAX**: XLA compilation, `jax.grad`, `jax.vmap`, `jax.pmap`, function transformation
- **Functors**: `vmap` (vectorization), `grad` (differentiation), `jit` (compilation)

### 2.4 Advanced Differentiation
- **Higher-order derivatives**: Hessian-vector products, Fisher information
- **Jacobian computation**: `torch.autograd.functional.jacobian`
- **Hessian computation**: `torch.autograd.functional.hessian`
- **Mixed partial derivatives**: cross-derivatives for optimization analysis

### 2.5 Lab: Build an Autograd Engine
- Implement a minimal autograd system supporting:
  - Tensor operations: add, mul, matmul, pow, exp, log
  - Activation functions: relu, sigmoid, tanh
  - Loss functions: MSE, cross-entropy
- Train a 3-layer MLP on MNIST
- Compare with PyTorch's autograd
- Profile memory usage during backpropagation

---

## Module 3: Optimization — Gradient Descent, Adaptive Methods & Second-Order Techniques

### 3.1 Gradient Descent Variants
- **Batch gradient descent**: full dataset, stable but slow
- **Stochastic gradient descent (SGD)**: single sample, noisy but fast
- **Mini-batch SGD**: compromise, typical batch sizes 32-512
- **Convergence analysis**: O(1/√T) for convex, O(1/T) for strongly convex
- **Learning rate schedules**: step decay, exponential decay, polynomial decay

### 3.2 Momentum Methods
- **Polyak momentum**: v_t = βv_{t-1} + ∇L, θ_t = θ_{t-1} - αv_t
- **Nesterov accelerated gradient**: look-ahead gradient, O(1/T²) for convex
- **Momentum as averaging**: exponential moving average of gradients
- **Quasi-hyperbolic momentum (QHM)**: interpolating between SGD and momentum

### 3.3 Adaptive Optimizers
- **AdaGrad**: per-parameter learning rates, accumulates squared gradients
  - Problem: learning rate decays to zero
- **RMSprop**: exponential moving average of squared gradients
  - `v_t = βv_{t-1} + (1-β)(∇L)²`, `θ_t = θ_{t-1} - α·∇L/√(v_t+ε)`
- **Adam**: momentum + RMSprop, bias correction
  - `m_t = β₁m_{t-1} + (1-β₁)∇L` (first moment)
  - `v_t = β₂v_{t-1} + (1-β₂)(∇L)²` (second moment)
  - `m̂_t = m_t/(1-β₁^t)`, `v̂_t = v_t/(1-β₂^t)` (bias correction)
  - `θ_t = θ_{t-1} - α·m̂_t/(√v̂_t+ε)`
- **AdamW**: decoupled weight decay, `θ_t = θ_{t-1} - α·m̂_t/(√v̂_t+ε) - λθ_{t-1}`
- **LARS/LAMB**: layer-wise adaptive rates for large batch training

### 3.4 Second-Order Methods
- **Newton's method**: θ_t = θ_{t-1} - H⁻¹∇L, quadratic convergence
- **L-BFGS**: limited-memory BFGS, approximates inverse Hessian
- **Natural gradient**: Fisher information matrix as Riemannian metric
- **K-FAC**: Kronecker-factored approximate curvature, block-diagonal Fisher
- **When to use**: small models, full-batch, convex-like landscapes

### 3.5 Learning Rate Scheduling
- **Warmup**: linear increase from 0 to peak, prevents early instability
- **Cosine annealing**: `lr_t = lr_min + 0.5(lr_max-lr_min)(1+cos(πT_cur/T_max))`
- **Warm restarts**: periodic resets, snapshot ensembles
- **One-cycle policy**: increase then decrease, super-convergence
- **Plateau scheduling**: reduce LR when validation loss plateaus

### 3.6 Lab: Optimize a Deep Network
- Implement SGD, Momentum, RMSprop, Adam, AdamW from scratch
- Train ResNet-18 on CIFAR-10 with each optimizer
- Compare convergence speed, final accuracy, generalization
- Implement cosine annealing with warm restarts
- Profile optimizer state memory usage

---

## Module 4: Convolutional Neural Networks — The Visual Cortex of AI

### 4.1 The Convolution Operation
- **1D convolution**: sliding window, kernel, stride, padding, dilation
- **2D convolution**: `Y[i,j] = Σ_m Σ_n X[i+m,j+n]·K[m,n]`
- **Properties**: translation equivariance, local connectivity, weight sharing
- **Stride**: downsampling factor, reduces spatial dimensions
- **Padding**: same (preserve size), valid (reduce size), causal (for sequences)
- **Dilation**: atrous convolution, enlarged receptive field without pooling

### 4.2 CNN Architectures — Historical Progression
- **LeNet-5 (1998)**: 5 layers, MNIST, foundational
- **AlexNet (2012)**: 8 layers, ReLU, dropout, data augmentation, GPU training
- **VGGNet (2014)**: 16-19 layers, 3×3 convolutions, simplicity
- **ResNet (2015)**: skip connections, residual learning, 152+ layers
  - `F(x) + x` instead of `F(x)`, solves vanishing gradient
  - Bottleneck design: 1×1 → 3×3 → 1×1
- **DenseNet (2017)**: dense connections, feature reuse, parameter efficiency
- **EfficientNet (2019)**: compound scaling (depth, width, resolution)
- **ConvNeXt (2022)**: modernizing ConvNets with Transformer design choices

### 4.3 Modern CNN Components
- **Batch Normalization**: `y = γ(x-μ)/√(σ²+ε) + β`
  - Training: batch statistics; Inference: running statistics
  - Benefits: faster training, higher LR, regularization
- **Group Normalization**: alternative when batch size is small
- **Layer Normalization**: used in Transformers, per-sample normalization
- **Instance Normalization**: style transfer, per-sample per-channel
- **Squeeze-and-Excitation**: channel attention, recalibration
- **Stochastic Depth**: randomly drop residual blocks during training

### 4.4 Object Detection & Segmentation
- **R-CNN family**: region proposals, feature extraction, classification
  - R-CNN → Fast R-CNN → Faster R-CNN (end-to-end)
- **YOLO**: single-shot detection, real-time, anchor boxes
  - YOLOv1 → YOLOv8/v9: improved architecture, anchor-free
- **SSD**: multi-scale feature maps, aspect ratio priors
- **Anchor-free**: CenterNet, FCOS, DETR
  - Center points, corner points, keypoints
- **Transformer-based**: DETR, Deformable DETR, DINO
  - Bipartite matching, set prediction

### 4.5 Segmentation
- **Semantic**: pixel-level class labels
  - FCN, U-Net, DeepLab, PSPNet
  - Atrous spatial pyramid pooling (ASPP)
- **Instance**: individual object masks
  - Mask R-CNN: add mask head to Faster R-CNN
  - Panoptic FPN: unified semantic + instance
- **Panoptic**: both semantic and instance
- **Interactive**: SAM (Segment Anything), click-based prompts

### 4.6 Lab: Build a Modern CNN
- Implement ResNet-50 from scratch with batch normalization
- Train on ImageNet subset or CIFAR-100
- Implement data augmentation: random crop, horizontal flip, color jitter
- Compare with pre-trained torchvision model
- Visualize feature maps and filter responses

---

## Module 5: Recurrent Neural Networks & Sequence Modeling

### 5.1 RNN Fundamentals
- **Elman RNN**: `h_t = tanh(W_{hh}h_{t-1} + W_{xh}x_t + b)`
- **Jordan RNN**: output feedback instead of hidden state feedback
- **Bidirectional RNN**: forward + backward processing, concatenated states
- **Deep RNNs**: stacking multiple RNN layers
- **Backpropagation Through Time (BPTT)**: unrolling, truncated BPTT

### 5.2 LSTM & GRU
- **Vanishing gradients in RNNs**: why long-term dependencies are hard
- **LSTM (Long Short-Term Memory)**:
  - Forget gate: `f_t = σ(W_f·[h_{t-1}, x_t] + b_f)`
  - Input gate: `i_t = σ(W_i·[h_{t-1}, x_t] + b_i)`
  - Candidate: `c̃_t = tanh(W_c·[h_{t-1}, x_t] + b_c)`
  - Cell state: `c_t = f_t ⊙ c_{t-1} + i_t ⊙ c̃_t`
  - Output gate: `o_t = σ(W_o·[h_{t-1}, x_t] + b_o)`
  - Hidden state: `h_t = o_t ⊙ tanh(c_t)`
- **GRU (Gated Recurrent Unit)**: simplified, merge forget and input gates
  - Update gate: `z_t = σ(W_z·[h_{t-1}, x_t])`
  - Reset gate: `r_t = σ(W_r·[h_{t-1}, x_t])`
  - Candidate: `h̃_t = tanh(W·[r_t ⊙ h_{t-1}, x_t])`
  - Hidden state: `h_t = (1-z_t) ⊙ h_{t-1} + z_t ⊙ h̃_t`
- **Peephole connections**: gates see cell state directly

### 5.3 Sequence-to-Sequence Models
- **Encoder-decoder**: encoder compresses input, decoder generates output
- **Attention mechanism**: Bahdanau attention, content-based addressing
- **Teacher forcing**: using ground truth as decoder input during training
- **Scheduled sampling**: gradually reducing teacher forcing ratio
- **Copy mechanism**: copying rare words from input

### 5.4 Modern Sequence Models
- **Transformer-XL**: segment-level recurrence, relative positional encoding
- **XLNet**: permutation language modeling, autoregressive denoising
- **Mamba/State Space Models**: linear complexity, long sequences, hardware-efficient
  - Selective state spaces: input-dependent transitions
  - Hardware-aware parallel scan algorithm

### 5.5 Lab: Build a Sequence Model
- Implement LSTM from scratch with NumPy
- Train character-level language model on Shakespeare
- Implement attention mechanism for machine translation
- Compare LSTM vs Transformer on sequence length scaling
- Visualize attention weights for interpretability

---

## Module 6: The Transformer Revolution — Attention Is All You Need

### 6.1 Self-Attention Mechanism
- **Scaled dot-product attention**: `Attention(Q,K,V) = softmax(QK^T/√d_k)V`
  - Q, K, V projections from input
  - Scaling factor √d_k prevents softmax saturation
  - O(n²) complexity in sequence length
- **Multi-head attention**: h parallel attention heads, concatenated, projected
  - `MultiHead(Q,K,V) = Concat(head_1,...,head_h)W^O`
  - Each head learns different attention patterns
- **Positional encoding**: sinusoidal, learned, rotary (RoPE), ALiBi
  - Sinusoidal: `PE(pos,2i) = sin(pos/10000^(2i/d))`
  - RoPE: rotate query/key by position-dependent angles
  - ALiBi: add position-based bias to attention scores

### 6.2 Transformer Architecture
- **Encoder**: self-attention + feed-forward, stack of N layers
- **Decoder**: masked self-attention + cross-attention + feed-forward
- **Feed-forward network**: two linear layers with activation, typically 4× expansion
- **Layer normalization**: Pre-LN (before attention) vs Post-LN (after attention)
  - Pre-LN: more stable training, used in modern models
  - RMSNorm: simplified, removes mean centering
- **Residual connections**: `x + Sublayer(LayerNorm(x))` or `LayerNorm(x + Sublayer(x))`

### 6.3 Efficiency Improvements
- **Sparse attention**: Longformer, BigBird, local + global + random attention
- **Linear attention**: kernel feature maps, O(n) complexity
- **FlashAttention**: IO-aware algorithm, tiling, recomputation
  - Tiling: split Q,K,V into blocks that fit in SRAM
  - Recomputation: don't store large attention matrices
  - 2-4× speedup, memory-proportional to sequence length
- **FlashDecoding**: split long KV cache for parallel decoding
- **Sliding window attention**: local attention with global tokens

### 6.4 Vision Transformers (ViT)
- **Patch embedding**: split image into patches, linear projection
- **Global attention**: all patches attend to all patches
- **Inductive bias tradeoff**: less bias than CNNs, more data needed
- **Hierarchical ViTs**: Swin Transformer, shifted window attention
- **Hybrid approaches**: CNN + Transformer, early convolutions

### 6.5 Lab: Implement a Transformer from Scratch
- Build complete encoder-decoder Transformer with PyTorch
- Train on WMT14 English-German translation
- Implement FlashAttention-style memory-efficient attention
- Compare with HuggingFace implementation
- Analyze attention patterns for different heads

---

## Module 7: Generative Models — VAEs, GANs, Diffusion & Flows

### 7.1 Variational Autoencoders (VAE)
- **Latent variable model**: `p(x) = ∫ p(x|z)p(z)dz`
- **Evidence Lower Bound (ELBO)**: `log p(x) ≥ E_q[log p(x|z)] - KL(q(z|x)||p(z))`
- **Reparameterization trick**: `z = μ + σ·ε`, ε ~ N(0,I)
- **Encoder**: inference network q(z|x), outputs μ and log(σ²)
- **Decoder**: generative network p(x|z), reconstructs input
- **β-VAE**: weighted KL term for disentanglement
- **VAE limitations**: blurry reconstructions, posterior collapse

### 7.2 Generative Adversarial Networks (GAN)
- **Minimax game**: `min_G max_D V(D,G) = E[log D(x)] + E[log(1-D(G(z)))]`
- **Generator**: maps noise to data space
- **Discriminator**: classifies real vs fake
- **Training challenges**: mode collapse, vanishing gradients, non-convergence
- **Improvements**:
  - **DCGAN**: convolutional architecture, batch norm, strided convolutions
  - **WGAN**: Wasserstein distance, Lipschitz constraint, weight clipping
  - **WGAN-GP**: gradient penalty instead of clipping
  - **StyleGAN**: progressive growing, style-based generator, AdaIN
  - **StyleGAN2/3**: improved regularization, better quality

### 7.3 Diffusion Models
- **Forward diffusion**: gradually add Gaussian noise, `q(x_t|x_{t-1}) = N(x_t; √(1-β_t)x_{t-1}, β_tI)`
- **Reverse diffusion**: learn to denoise, `p_θ(x_{t-1}|x_t) = N(x_{t-1}; μ_θ(x_t,t), Σ_θ(x_t,t))`
- **DDPM**: simplified objective, predict noise, `L = E_t[||ε - ε_θ(x_t,t)||²]`
- **DDIM**: deterministic sampling, fewer steps
- **Classifier-free guidance**: `ε_θ = ε_uncond + w(ε_cond - ε_uncond)`
- **Latent diffusion**: operate in latent space (VAE encoder), Stable Diffusion
- **Flow matching**: direct path between distributions, continuous normalizing flows

### 7.4 Normalizing Flows
- **Change of variables**: `log p(x) = log p(z) + log|det(∂f/∂z)|`
- **Invertible transformations**: coupling layers, autoregressive flows
- **RealNVP**: affine coupling, easy Jacobian determinant
- **Glow**: 1×1 convolutions, actnorm, multi-scale architecture
- **Continuous normalizing flows**: neural ODEs, FFJORD

### 7.5 Lab: Build Generative Models
- Implement VAE with reparameterization trick
- Train DCGAN on CelebA or CIFAR-10
- Implement DDPM diffusion model
- Compare sample quality: VAE vs GAN vs Diffusion
- Interpolate in latent space and visualize

---

## Module 8: Self-Supervised & Contrastive Learning

### 8.1 Pretext Tasks
- **Rotation prediction**: predict image rotation angle
- **Jigsaw puzzles**: predict permutation of image patches
- **Colorization**: predict color channels from grayscale
- **Inpainting**: predict missing image regions
- **Relative patch location**: predict spatial relationship between patches

### 8.2 Contrastive Learning
- **InfoNCE loss**: `L = -log(exp(sim(z_i,z_j^+)/τ) / Σ_k exp(sim(z_i,z_k)/τ))`
- **SimCLR**: data augmentation, projection head, large batch size
  - Two views of same image are positive pair
  - All other images in batch are negatives
- **MoCo**: momentum encoder, dynamic dictionary, queue of negatives
  - Momentum update: `θ_k ← m·θ_k + (1-m)·θ_q`
- **SwAV**: online clustering, prototypes, swapped assignment
- **BYOL**: no negatives, online-offline networks, stop-gradient
- **DINO**: self-distillation with no labels, centering, sharpening

### 8.3 Masked Prediction
- **BERT**: masked language modeling, next sentence prediction
- **MAE (Masked Autoencoder)**: high masking ratio (75%), pixel reconstruction
- **BEiT**: discrete visual tokens from VAE, BERT-style pretraining
- **Data2Vec**: unified self-supervised learning across modalities

### 8.4 Representation Quality
- **Linear probing**: freeze encoder, train linear classifier
- **Fine-tuning**: end-to-end adaptation to downstream task
- **k-NN evaluation**: nearest neighbor classifier in feature space
- **Transfer learning**: cross-domain, cross-task evaluation

### 8.5 Lab: Implement Self-Supervised Learning
- Implement SimCLR with custom data augmentation pipeline
- Train on unlabeled ImageNet subset
- Evaluate with linear probing on ImageNet-1k
- Compare with supervised baseline
- Visualize learned representations with t-SNE

---

## Module 9: Distributed Training at Scale — Data, Model & Pipeline Parallelism

### 9.1 Data Parallelism
- **Synchronous SGD**: all-reduce gradients, identical model copies
- **Ring AllReduce**: bandwidth-optimal, O(2(N-1)/N) per node
  - Scatter-reduce: each node accumulates chunk
  - All-gather: broadcast final result
- **PyTorch DDP**: `DistributedDataParallel`, bucketing, overlap computation/communication
- **Horovod**: MPI-based, `hvd.DistributedOptimizer`
- **Batch size scaling**: linear scaling rule, LARS/LAMB for large batches

### 9.2 Model Parallelism
- **Tensor parallelism**: split individual layers across GPUs
  - Column-wise: split output dimension
  - Row-wise: split input dimension
  - Megatron-LM: clever partitioning to minimize communication
- **Pipeline parallelism**: split model into stages
  - GPipe: micro-batches, all forward then all backward
  - PipeDream: interleaved forward/backward, weight stashing
  - Bubble reduction: more micro-batches, less idle time

### 9.3 3D Parallelism & ZeRO
- **DeepSpeed ZeRO**: Zero Redundancy Optimizer
  - ZeRO-1: partition optimizer states
  - ZeRO-2: partition gradients
  - ZeRO-3: partition parameters
  - ZeRO-Offload: offload to CPU/NVMe
- **FSDP (Fully Sharded Data Parallel)**: PyTorch's ZeRO implementation
- **3D parallelism**: DP × TP × PP, optimal configuration depends on cluster topology

### 9.4 Communication & Topology
- **NCCL**: NVIDIA Collective Communications Library
- **InfiniBand**: high-speed interconnect, RDMA, 400-800 Gbps
- **NVLink**: GPU-to-GPU, 900 GB/s, within-node
- **Hierarchical topology**: node-level (NVLink) + rack-level + datacenter-level (InfiniBand)
- **Llama 3.1 405B**: 16K H100s, TP=8, PP=16, DP=8-128, 54 days training

### 9.5 Lab: Distributed Training
- Set up multi-GPU training with PyTorch DDP
- Implement ring all-reduce from scratch
- Train ResNet-50 with data parallelism, measure scaling efficiency
- Profile communication overhead with NVIDIA Nsight
- Compare DDP vs FSDP memory usage

---

## Module 10: Training Stability — Mixed Precision, Normalization & Regularization

### 10.1 Mixed Precision Training
- **FP16/BF16**: 16-bit floating point, 2× memory, faster Tensor Cores
- **Automatic Mixed Precision (AMP)**: `torch.cuda.amp`, automatic casting
- **Loss scaling**: prevent gradient underflow in FP16
  - Dynamic scaling: increase until Inf/NaN, then decrease
  - `GradScaler`: `scale(loss).backward()`, `step()`, `update()`
- **Master weights**: FP32 copy for optimizer state, FP16 for forward/backward
- **BF16 vs FP16**: BF16 has wider range (same exponent as FP32), no loss scaling needed
- **FP8**: H100/B200, even lower precision, requires careful scaling

### 10.2 Normalization Techniques
- **Batch Normalization**: `BN(x) = γ·(x-μ_B)/√(σ²_B+ε) + β`
  - Training: batch statistics; Inference: running mean/variance
  - Benefits: faster convergence, higher learning rates, regularization
- **Layer Normalization**: per-sample, per-layer normalization
- **Group Normalization**: divide channels into groups, normalize per group
- **Instance Normalization**: per-sample, per-channel
- **RMSNorm**: `RMSNorm(x) = x/√(mean(x²))·γ`, simpler, used in LLaMA

### 10.3 Regularization
- **Dropout**: randomly zero neurons during training, p=0.2-0.5
  - Inverted dropout: scale by 1/(1-p) during training
  - DropConnect: randomly zero weights
- **DropBlock**: structured dropout for convolutions
- **Stochastic Depth**: randomly skip residual blocks
- **Label smoothing**: `y_smooth = (1-α)·y + α/K`, prevents overconfidence
- **Mixup**: `x' = λx₁ + (1-λ)x₂`, `y' = λy₁ + (1-λ)y₂`, linear interpolation
- **CutMix**: cut and paste patches between images
- **Cutout**: random square masks

### 10.4 Training Diagnostics
- **Gradient norm monitoring**: exploding/vanishing gradients
- **Weight norm monitoring**: weight collapse, dead neurons
- **Activation statistics**: mean, std, saturation percentage
- **Learning rate finder**: find optimal LR range
- **Loss landscape visualization**: random directions, filter-normalized

### 10.5 Lab: Stabilize Training
- Implement mixed precision training with AMP
- Compare BN, LN, GN on small batch sizes
- Implement dropout, label smoothing, mixup
- Monitor gradient norms and activation statistics
- Use learning rate finder to optimize training

---

## Module 11: Neural Architecture Search & Automated Deep Learning

### 11.1 Search Spaces
- **Macro search**: entire architecture topology
- **Micro search**: cell/block structure, repeated
- **Primitive operations**: convolutions, pooling, skip connections, attention
- **Constraints**: FLOPs, memory, latency, energy

### 11.2 Search Strategies
- **Random search**: surprisingly strong baseline
- **Evolutionary algorithms**: mutation, crossover, selection
  - AmoebaNet, EfficientNet evolution
- **Reinforcement learning**: controller RNN, policy gradient
  - NASNet, ENAS (efficient NAS with parameter sharing)
- **Gradient-based (DARTS)**: continuous relaxation, differentiable
  - Softmax over operations: `ō(x) = Σ_i α_i·o_i(x)`
  - Bi-level optimization: train weights, then architecture
  - Limitations: memory overhead, discretization gap
- **Bayesian optimization**: Gaussian processes, acquisition functions

### 11.3 Hardware-Aware NAS
- **Latency prediction**: lookup tables, learned predictors
- **Multi-objective**: accuracy vs latency, Pareto frontier
- **ProxylessNAS**: direct search on target hardware
- **Once-for-All (OFA)**: train supernet, then specialize
- **BigNAS**: train one model, extract subnets of any size

### 11.4 Lab: Implement NAS
- Implement DARTS with PyTorch
- Search for optimal cell on CIFAR-10
- Evaluate searched architecture on ImageNet
- Compare with hand-designed ResNet
- Analyze architecture choices

---

## Module 12: Deep Learning for Computer Vision — Object Detection, Segmentation & Generation

### 12.1 Object Detection
- **Two-stage**: R-CNN, Fast R-CNN, Faster R-CNN
  - Region Proposal Network (RPN)
  - ROI pooling, ROI align
- **One-stage**: YOLO, SSD, RetinaNet
  - Anchor boxes, aspect ratios, scales
  - Focal loss for class imbalance
- **Anchor-free**: CenterNet, FCOS, DETR
  - Center points, corner points, keypoints
- **Transformer-based**: DETR, Deformable DETR, DINO
  - Bipartite matching, set prediction

### 12.2 Segmentation
- **Semantic**: pixel-level class labels
  - FCN, U-Net, DeepLab, PSPNet
  - Atrous spatial pyramid pooling (ASPP)
- **Instance**: individual object masks
  - Mask R-CNN: add mask head to Faster R-CNN
  - Panoptic FPN: unified semantic + instance
- **Panoptic**: both semantic and instance
- **Interactive**: SAM (Segment Anything), click-based prompts

### 12.3 Image Generation & Editing
- **StyleGAN**: style-based generator, progressive growing
  - Mapping network, synthesis network, AdaIN
  - Style mixing, truncation trick
- **Stable Diffusion**: latent diffusion, text conditioning
  - CLIP text encoder, U-Net denoiser, VAE decoder
- **ControlNet**: conditional control with locked base model
- **Inpainting**: masked diffusion, context-aware filling

### 12.4 Video Understanding
- **3D convolutions**: spatiotemporal filters, C3D, I3D
- **Two-stream networks**: RGB + optical flow
- **Transformer-based**: TimeSformer, Video Swin Transformer
- **Self-supervised**: masked video modeling, contrastive learning

### 12.5 Lab: Build a Vision System
- Implement Faster R-CNN or YOLOv8 for object detection
- Train U-Net for medical image segmentation
- Fine-tune Stable Diffusion for domain-specific generation
- Evaluate on COCO, PASCAL VOC, or custom dataset

---

## Module 13: Deep Learning for NLP — From Word Embeddings to LLMs

### 13.1 Word Representations
- **One-hot encoding**: sparse, high-dimensional, no semantics
- **Word2Vec**: CBOW (predict word from context), Skip-gram (predict context from word)
  - Negative sampling, hierarchical softmax
  - `L = log σ(v'_w·v_c) + Σ_k E[log σ(-v'_n·v_c)]`
- **GloVe**: global word-word co-occurrence statistics
  - `L = Σ_ij f(X_ij)(w_i^T w̃_j + b_i + b̃_j - log X_ij)²`
- **FastText**: subword information, character n-grams

### 13.2 Contextual Embeddings
- **ELMo**: bidirectional LSTM, deep contextualized representations
- **BERT**: masked language modeling, next sentence prediction
  - `[CLS]` token for classification, `[SEP]` for separation
  - Pre-training → fine-tuning paradigm
- **RoBERTa**: more data, longer training, no NSP, dynamic masking
- **ALBERT**: parameter sharing, factorized embeddings, SOP
- **DeBERTa**: disentangled attention, enhanced mask decoder

### 13.3 Large Language Models
- **GPT series**: decoder-only, autoregressive, next-token prediction
  - GPT-1 → GPT-4: scaling parameters, data, compute
- **T5**: encoder-decoder, text-to-text transfer transformer
- **BART**: denoising autoencoder, bidirectional + autoregressive
- **Scaling laws**: loss ∝ C^(-α), N^(-β), D^(-γ)
- **Instruction tuning**: FLAN, InstructGPT, ChatGPT
- **RLHF**: reward model, PPO, KL penalty

### 13.4 Modern LLM Techniques
- **Parameter-efficient fine-tuning**: LoRA, prefix tuning, prompt tuning
- **Quantization**: GPTQ, AWQ, GGUF for inference
- **Speculative decoding**: draft model + target model
- **Tool use**: function calling, retrieval augmentation
- **Chain-of-thought**: explicit reasoning, self-consistency

### 13.5 Lab: Build an NLP Pipeline
- Implement Word2Vec with negative sampling
- Fine-tune BERT for sentiment analysis
- Train a GPT-style model from scratch (small scale)
- Implement LoRA fine-tuning for domain adaptation
- Build a retrieval-augmented generation system

---

## Module 14: Production Deep Learning — Serving, Optimization & MLOps

### 14.1 Model Optimization
- **Quantization**: PTQ (post-training), QAT (quantization-aware training)
  - INT8, INT4, FP8, dynamic vs static quantization
- **Pruning**: unstructured (magnitude), structured (channels, heads)
  - Gradual pruning, lottery ticket hypothesis
- **Knowledge distillation**: teacher-student, soft targets, hint learning
- **Compilation**: ONNX Runtime, TensorRT, TVM, XLA
  - Graph optimization, operator fusion, kernel autotuning

### 14.2 Serving Infrastructure
- **Batch inference**: high throughput, high latency
- **Real-time inference**: low latency, streaming
- **Model servers**: TorchServe, TensorFlow Serving, Triton, vLLM
- **Dynamic batching**: batch requests at runtime
- **Model parallelism**: split large models across GPUs
- **Caching**: embedding cache, result cache, prompt cache

### 14.3 MLOps for Deep Learning
- **Experiment tracking**: MLflow, W&B, TensorBoard
- **Model registry**: versioning, staging, metadata
- **CI/CD**: automated testing, canary deployment, rollback
- **Monitoring**: drift detection, performance degradation, latency
- **Feature stores**: online/offline consistency, point-in-time correctness

### 14.4 Lab: Deploy a Production Model
- Convert PyTorch model to ONNX
- Quantize to INT8 with TensorRT
- Deploy on Triton Inference Server
- Implement dynamic batching
- Benchmark latency and throughput
- Set up monitoring with Prometheus/Grafana

---

## Capstone Project

### Project: Build a Production-Grade Deep Learning Platform

Build an end-to-end deep learning system for a complex real-world problem:

**Requirements:**
1. **Data pipeline**: Large-scale data ingestion, preprocessing, augmentation
2. **Model architecture**: Custom architecture with attention, convolutions, or both
3. **Distributed training**: Multi-GPU training with 3D parallelism
4. **Mixed precision**: FP16/BF16 training with loss scaling
5. **Generative component**: VAE, GAN, or diffusion model for data generation
6. **Self-supervised pretraining**: Representation learning on unlabeled data
7. **Fine-tuning**: Task-specific adaptation with LoRA or full fine-tuning
8. **Optimization**: Quantization, pruning, or distillation for deployment
9. **Serving**: Real-time inference with dynamic batching
10. **MLOps**: Full pipeline with experiment tracking, model registry, monitoring

**Suggested Domains:**
- Autonomous driving perception (detection + segmentation)
- Medical imaging (classification + segmentation + generation)
- Multimodal search (vision + language + retrieval)
- Scientific computing (PDE solving, molecular generation)

---

## Appendix A: Reading List & References

### Foundations
- *Deep Learning* — Goodfellow, Bengio, Courville
- *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong
- *Neural Networks and Deep Learning* — Michael Nielsen (free online)

### Architectures
- *An Image is Worth 16x16 Words* — Dosovitsky et al. (ViT)
- *Attention Is All You Need* — Vaswani et al. (Transformer)
- *Deep Residual Learning for Image Recognition* — He et al. (ResNet)

### Generative Models
- *Auto-Encoding Variational Bayes* — Kingma & Welling (VAE)
- *Generative Adversarial Networks* — Goodfellow et al. (GAN)
- *Denoising Diffusion Probabilistic Models* — Ho et al. (DDPM)

### Training at Scale
- *Megatron-LM: Training Multi-Billion Parameter Language Models* — Shoeybi et al.
- *ZeRO: Memory Optimizations Toward Training Trillion Parameter Models* — Rajbhandari et al.
- *Mixed Precision Training* — Micikevicius et al. (NVIDIA)

### Self-Supervised Learning
- *A Simple Framework for Contrastive Learning of Visual Representations* — Chen et al. (SimCLR)
- *Masked Autoencoders Are Scalable Vision Learners* — He et al. (MAE)

---

## Appendix B: Tooling Matrix

### Frameworks
| Framework | Best For | Ecosystem |
|-----------|----------|-----------|
| **PyTorch** | Research, flexibility | Dynamic graphs, Pythonic |
| **TensorFlow** | Production, deployment | Keras, TF Serving, TFX |
| **JAX** | High-performance research | XLA, functional, composable |
| **PyTorch Lightning** | Structured training | Boilerplate reduction |

### Distributed Training
| Tool | Best For | Scale |
|------|----------|-------|
| **PyTorch DDP** | Data parallelism | Single-node, multi-node |
| **DeepSpeed** | Large models | ZeRO, 3D parallelism |
| **Megatron-LM** | LLM pretraining | 1000s GPUs |
| **Horovod** | MPI-based training | Multi-node |
| **FSDP** | PyTorch sharding | Large models |

### Optimization & Serving
| Tool | Best For |
|------|----------|
| **TensorRT** | NVIDIA GPU inference |
| **ONNX Runtime** | Cross-platform inference |
| **vLLM** | LLM serving |
| **TVM** | Auto-scheduling, edge devices |
| **Apex** | Mixed precision, distributed |

---

## Appendix C: Interview Preparation

### System Design
- Design a distributed training system for a 100B parameter model
- Design a real-time image recognition service
- Design a video understanding pipeline
- Design a generative model serving infrastructure

### Deep Dives
- Derive backpropagation for a CNN with batch normalization
- Explain why transformers use layer norm instead of batch norm
- Compare LSTM vs Transformer for long sequences
- How does FlashAttention achieve memory efficiency?
- Design a diffusion model training pipeline

### Coding Challenges
- Implement a Transformer encoder from scratch
- Build a ResNet block with skip connections
- Implement attention mechanism with causal masking
- Write a VAE with reparameterization trick
- Implement distributed data parallel training loop

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 1 week | 0 | Math, optimization theory |
| **Core Architectures** | 3 weeks | 1-6 | MLP, CNN, RNN, Transformer |
| **Generative Models** | 2 weeks | 7-8 | VAE, GAN, Diffusion, Self-supervised |
| **Scale** | 2 weeks | 9-10 | Distributed training, stability |
| **Advanced** | 2 weeks | 11-13 | NAS, CV, NLP |
| **Production** | 1 week | 14 | Serving, optimization, MLOps |
| **Capstone** | 2 weeks | — | End-to-end system |

**Total Duration: 13 weeks (3 months) full-time, or 6 months part-time**

---

*This syllabus treats deep learning as a systems engineering discipline. The architectures, training techniques, and hardware evolve rapidly, but the mathematical foundations — differential geometry, optimization theory, and linear algebra — remain constant. Master the fundamentals, and you can adapt to any architecture or scale.*

---

Download this file: [deep-learning-syllabus.md](sandbox:///mnt/agents/output/deep-learning-syllabus.md)