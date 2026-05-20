## File: computer-architecture-low-level-systems-syllabus.md

# Computer Architecture & Low-Level Systems: From Silicon to Production Software

## A University-Level, Industry-Grade Technical Syllabus

**Version:** 2026.05  
**Target Audience:** AI Systems Engineers, ML Infrastructure Engineers, LLM Engineers, MLOps Engineers, Distributed Systems Engineers, Backend Engineers, GPU/Inference Engineers, Production AI Engineers, Staff-level Infrastructure Candidates  
**Prerequisites:** Solid C/C++, basic assembly, digital logic fundamentals, operating systems basics, and comfort with binary/hex arithmetic  
**Estimated Duration:** 350–450 hours of focused study + 150 hours of capstone projects  
**Last Updated:** May 2026

---

## Table of Contents

1. [Meta: How to Use This Syllabus](#meta-how-to-use-this-syllabus)
2. [Phase 0: Mathematical & Digital Foundations](#phase-0-mathematical--digital-foundations)
3. [Phase 1: Digital Logic & Computer Organization](#phase-1-digital-logic--computer-organization)
4. [Phase 2: Computer Architecture — The Processor](#phase-2-computer-architecture--the-processor)
5. [Phase 3: Memory Hierarchy & Caching](#phase-3-memory-hierarchy--caching)
6. [Phase 4: Instruction Set Architecture & Assembly](#phase-4-instruction-set-architecture--assembly)
7. [Phase 5: Operating Systems & System Programming](#phase-5-operating-systems--system-programming)
8. [Phase 6: Compiler Design & Code Generation](#phase-6-compiler-design--code-generation)
9. [Phase 7: Performance Engineering & Optimization](#phase-7-performance-engineering--optimization)
10. [Phase 8: Modern CPU Microarchitecture](#phase-8-modern-cpu-microarchitecture)
11. [Phase 9: GPU Architecture & Heterogeneous Computing](#phase-9-gpu-architecture--heterogeneous-computing)
12. [Phase 10: Systems Security & Hardware Hardening](#phase-10-systems-security--hardware-hardening)
13. [Capstone Projects](#capstone-projects)
14. [Assessment & Certification Rubric](#assessment--certification-rubric)
15. [Recommended Reading & Reference Library](#recommended-reading--reference-library)

---

## Meta: How to Use This Syllabus

This syllabus is designed as a **bottom-up, progressive curriculum** that builds intuition from the transistor level to production systems engineering. Each phase constructs abstractions upon the previous, with explicit dependency chains.

**Study Protocol:**
- **Theory → Implementation → Systems → Production:** Every concept must be understood at the gate level, implemented in HDL/assembly/C, integrated into a system, and operationalized in production contexts.
- **Spaced Reinforcement:** Concepts from earlier phases reappear in later phases at increasing depth.
- **Build-Measure-Learn:** Every module includes explicit simulation, profiling, and benchmarking exercises.
- **Architecture Reasoning:** Each phase includes design exercises requiring trade-off analysis (area vs. delay, power vs. performance, latency vs. throughput).

**Required Tools & Environment:**
- Verilog/VHDL simulator (Icarus Verilog, Vivado, or Verilator)
- C/C++ compiler (GCC/Clang) with `-O0` through `-O3`, `-march=native`
- GDB, LLDB, perf, valgrind, cachegrind, callgrind
- QEMU for architecture emulation
- Intel VTune, AMD uProf, or Linux perf for microarchitectural profiling
- CUDA toolkit (12.x+) for GPU architecture sections

---

## Phase 0: Mathematical & Digital Foundations

> **Objective:** Establish the mathematical language and abstraction discipline required for rigorous computer architecture. Skip only if you can derive Boolean algebra laws from first principles, analyze timing in a sequential circuit, and explain why binary is used.

### 0.1 Boolean Algebra & Logic Design
- **Boolean Axioms:** Commutativity, associativity, distributivity, identity, complement, De Morgan's laws
- **Canonical Forms:** Sum-of-products (SOP), product-of-sums (POS), minterms, maxterms
- **Logic Minimization:** Karnaugh maps (2-6 variables), Quine-McCluskey algorithm, prime implicants, essential prime implicants
- **Functional Completeness:** NAND/NAND universality, NOR/NOR universality, Reed-Muller expansion
- **Key Exercise:** Minimize a 4-variable Boolean function using K-maps. Verify with algebraic manipulation. Implement using only NAND gates.

### 0.2 Number Systems & Arithmetic
- **Positional Number Systems:** Binary, octal, hexadecimal, radix conversion, fractional representation
- **Fixed-Point Arithmetic:** Q-format, scaling factors, overflow/underflow, rounding modes
- **Floating-Point (IEEE 754):** Single/double precision, sign-exponent-mantissa, subnormals, NaN, infinity, rounding modes (RN, RZ, RP, RM)
- **Floating-Point Pitfalls:** Catastrophic cancellation, non-associativity, precision loss in summation (Kahan summation)
- **Key Exercise:** Implement a 16-bit floating-point adder in C. Test edge cases: subnormal + normal, overflow, NaN propagation.

### 0.3 Combinational Circuit Analysis
- **Logic Gates:** CMOS transistor-level implementation (NOT, NAND, NOR, AND, OR, XOR, XNOR), propagation delay, fan-in/fan-out
- **Timing Analysis:** Gate delay, critical path, slack, setup/hold time concepts (preview)
- **Hazards:** Static-0, static-1, dynamic hazards, hazard elimination via redundant terms
- **Key Exercise:** Design a 4-bit carry-lookahead adder (CLA). Calculate gate count and critical path delay. Compare with ripple-carry adder.

### 0.4 Sequential Logic Foundations
- **Flip-Flops & Latches:** SR, D, JK, T flip-flops, level-sensitive vs. edge-triggered, metastability
- **Registers & Counters:** Shift registers, ring counters, Johnson counters, binary counters
- **Finite State Machines (FSM):** Moore vs. Mealy machines, state minimization, state encoding (binary, one-hot, gray)
- **Timing Constraints:** Setup time (t_su), hold time (t_h), clock-to-Q delay (t_cq), maximum clock frequency
- **Clock Distribution:** Clock skew, clock jitter, clock gating, clock domain crossing (CDC) basics
- **Key Exercise:** Design a vending machine FSM (Mealy). Implement in Verilog. Simulate with testbench. Analyze timing for 100 MHz operation.

### 0.5 Discrete Mathematics for Systems
- **Set Theory & Relations:** Equivalence relations, partial orders, lattices (relevant for memory consistency models)
- **Graph Theory:** Directed acyclic graphs (DAGs) for dataflow, topological sorting, critical path method
- **Modular Arithmetic:** Two's complement as modular arithmetic, residue number systems
- **Probability:** Random variables, expectation, variance, Markov chains (for cache modeling, branch prediction)
- **Key Exercise:** Model a simple cache as a Markov chain. Calculate hit rate given access patterns.

---

## Phase 1: Digital Logic & Computer Organization

> **Objective:** Build a complete mental model of how digital systems are constructed from transistors to functional units. Design and simulate real hardware.

### 1.1 CMOS Transistor-Level Design
- **MOSFET Physics:** nMOS vs. pMOS, threshold voltage, inversion layer, saturation vs. linear region
- **CMOS Logic:** Pull-up network (pMOS), pull-down network (nMOS), complementary design, power consumption (dynamic, static, short-circuit)
- **Pass Transistor Logic:** Transmission gates, multiplexers, advantages and limitations
- **Layout & Area:** Design rules, lambda-based design, stick diagrams, standard cells
- **Key Exercise:** Draw the transistor-level schematic of a full adder. Calculate worst-case delay using RC model.

### 1.2 Arithmetic Logic Units (ALU)
- **Adder Architectures:** Ripple-carry, carry-lookahead (CLA), carry-select, carry-skip, prefix adders (Kogge-Stone, Brent-Kung)
- **Multipliers:** Array multiplier, Wallace tree, Dadda tree, Booth encoding, pipelined multipliers
- **Dividers:** Restoring division, non-restoring division, SRT division, Newton-Raphson iteration
- **Floating-Point Units:** Fused multiply-add (FMA), pipelining, exception handling, denormal support
- **Key Exercise:** Implement a 32-bit Kogge-Stone adder in Verilog. Synthesize and report area/delay/power.

### 1.3 Memory Circuits
- **SRAM:** 6T cell, read/write operation, sense amplifiers, column multiplexing, word-line/bit-line design
- **DRAM:** 1T1C cell, refresh cycles, row/column decoding, sense amplifiers, RAS/CAS timing
- **ROM & Flash:** NOR/NAND flash, page/block structure, wear leveling, ECC
- **Memory Organization:** Bit-interleaving, bank interleaving, burst modes, DDR timing (tRCD, tRP, tCAS)
- **Key Exercise:** Design a 1KB SRAM array (32 words × 32 bits). Write Verilog model. Simulate read/write with timing checks.

### 1.4 Bus Architecture & Interconnect
- **System Buses:** Address bus, data bus, control bus, bus arbitration, synchronous vs. asynchronous
- **Bus Protocols:** AXI4, AHB, Wishbone — handshaking, burst transfers, out-of-order completion
- **On-Chip Interconnect:** Crossbar, shared bus, ring, mesh, torus — latency, bandwidth, scalability
- **NoC (Network-on-Chip):** Router microarchitecture, virtual channels, wormhole switching, deadlock-free routing
- **Key Exercise:** Design a 4-master, 4-slave AXI crossbar in Verilog. Simulate concurrent transfers. Measure throughput.

### 1.5 I/O & Peripheral Interfacing
- **Programmed I/O:** Memory-mapped I/O, port-mapped I/O, polling
- **Interrupts:** Vectored interrupts, interrupt priority, nested interrupts, interrupt latency
- **DMA:** DMA controller architecture, burst mode, cycle stealing, scatter-gather, cache coherence issues
- **Storage Interfaces:** SATA, NVMe, AHCI — command queues, parallelism, protocol overhead
- **Key Exercise:** Design a DMA controller with scatter-gather support. Integrate with a simple CPU model.

---

## Phase 2: Computer Architecture — The Processor

> **Objective:** Understand processor design from single-cycle to superscalar out-of-order execution. Build intuition for the instruction lifecycle.

### 2.1 Single-Cycle Processor Design
- **Datapath Components:** Program counter, instruction memory, register file, ALU, data memory, control unit
- **Instruction Execution:** Fetch → Decode → Execute → Memory → Writeback, single-cycle timing
- **Control Logic:** Main decoder, ALU control, control signal generation, truth tables
- **Performance Analysis:** Clock cycle time = critical path delay, CPI = 1, performance equation
- **Key Exercise:** Design a single-cycle RISC-V RV32I processor in Verilog. Implement all base instructions. Verify with RISC-V tests.

### 2.2 Multi-Cycle & Pipelined Processors
- **Multi-Cycle Design:** Resource sharing, state machine control, CPI > 1, reduced clock cycle time
- **5-Stage Pipeline:** IF → ID → EX → MEM → WB, pipeline registers, throughput improvement
- **Pipeline Hazards:** Structural hazards (resource conflicts), data hazards (RAW, WAR, WAW), control hazards (branches, jumps)
- **Hazard Resolution:** Forwarding/bypassing, stall insertion, branch prediction (static: not-taken, taken, delayed branch)
- **Key Exercise:** Convert the single-cycle RISC-V to a 5-stage pipeline. Implement forwarding and hazard detection. Benchmark CPI on test programs.

### 2.3 Advanced Pipelining
- **Superpipelining:** Increasing pipeline depth, clock frequency vs. CPI trade-off, branch misprediction penalty
- **Superscalar Execution:** Multiple issue slots, dynamic scheduling, register renaming, reservation stations
- **Out-of-Order Execution (OoO):** Tomasulo's algorithm, reorder buffer (ROB), speculative execution, precise exceptions
- **Branch Prediction:** 1-bit/2-bit saturating counters, correlating predictors (gshare), tournament predictors, TAGE, perceptron predictors
- **Key Exercise:** Implement a 2-wide superscalar pipeline with Tomasulo's algorithm in a cycle-accurate simulator. Measure IPC on SPEC-like benchmarks.

### 2.4 Instruction Set Architecture (ISA) Design
- **RISC vs. CISC:** Philosophy, code density, compiler complexity, hardware complexity, x86 vs. ARM vs. RISC-V
- **ISA Encoding:** Fixed-length vs. variable-length, opcode fields, register specifiers, immediate formats
- **Addressing Modes:** Immediate, register, direct, indirect, indexed, PC-relative, base+offset
- **Calling Conventions:** Stack frames, parameter passing, callee-saved vs. caller-saved registers, alignment
- **Key Exercise:** Design a minimal ISA for a domain-specific accelerator (e.g., matrix multiplication). Define encoding, implement assembler, write programs.

### 2.5 Virtual Memory & Protection
- **Address Translation:** Virtual → Physical, page tables, multi-level page tables, TLB (Translation Lookaside Buffer)
- **TLB Design:** Fully associative, set-associative, split TLB (instruction/data), TLB shootdown
- **Page Table Walks:** Hardware vs. software, page table entry format, dirty/accessed bits
- **Memory Protection:** Rings/privilege levels, system calls, traps, segmentation vs. paging
- **Key Exercise:** Simulate a two-level page table with TLB. Measure TLB hit rate vs. page size and working set.

---

## Phase 3: Memory Hierarchy & Caching

> **Objective:** Master the memory hierarchy from registers to distributed storage. Understand cache design, coherence, and consistency as a systems engineer.

### 3.1 Cache Fundamentals
- **Cache Organization:** Direct-mapped, fully associative, set-associative (N-way), tag/store/compare logic
- **Cache Performance:** Hit rate, miss rate, miss penalty, average memory access time (AMAT), 3C model (compulsory, capacity, conflict)
- **Block Placement & Replacement:** LRU, FIFO, random, pseudo-LRU, NRU, clock algorithm
- **Write Policies:** Write-through vs. write-back, write-allocate vs. no-write-allocate, dirty bit management
- **Key Exercise:** Implement a configurable cache simulator (direct-mapped to 16-way set-associative). Test with SPEC CPU traces. Analyze miss rates.

### 3.2 Advanced Cache Design
- **Multi-Level Caches:** L1 (split I/D), L2 (unified), L3 (shared), inclusion policies (inclusive, exclusive, non-inclusive)
- **Cache Optimizations:** Victim caches, stream buffers, prefetching (stride, stream, correlation), critical word first, early restart
- **Non-Blocking Caches:** Miss status handling registers (MSHR), hit-under-miss, miss-under-miss
- **Cache Compression:** Frequent pattern compression, base-delta-immediate, compressed cache lines
- **Key Exercise:** Add prefetching (stride detection) to your cache simulator. Measure coverage and accuracy on memory-intensive benchmarks.

### 3.3 Cache Coherence
- **The Coherence Problem:** Multiple caches, shared memory, write propagation, write serialization
- **Snooping Protocols:** MSI, MESI, MOSI, MOESI — state transitions, snoop requests, bus transactions
- **Directory Protocols:** Full directory, limited directory (Dir_iB), chained directory, memory overhead
- **False Sharing:** Definition, detection, mitigation (cache line padding, data structure redesign)
- **Key Exercise:** Implement a MESI snooping cache coherence simulator with 4 cores. Test with shared variable increments. Demonstrate false sharing.

### 3.4 Memory Consistency Models
- **Sequential Consistency:** Definition, implementation cost, memory fence requirements
- **Relaxed Models:** Total Store Order (TSO), Partial Store Order (PSO), Weak Ordering, Release Consistency
- **ARM & x86 Models:** ARMv8 memory model, x86-TSO, load/store reordering rules
- **Synchronization Primitives:** Test-and-set, compare-and-swap (CAS), load-linked/store-conditional (LL/SC), memory barriers
- **Key Exercise:** Write a program that demonstrates a memory reordering bug under TSO. Fix it with proper fencing. Verify with memory model checker (e.g., herd7).

### 3.5 Main Memory & Storage Systems
- **DRAM Architecture:** Banks, ranks, channels, DIMM organization, burst length, refresh overhead
- **Memory Controllers:** Scheduling policies (FR-FCFS, PAR-BS), row buffer locality, bank parallelism
- **Non-Volatile Memory:** NAND flash (SLC/MLC/TLC/QLC), wear leveling, garbage collection, FTL (Flash Translation Layer)
- **Storage Stack:** File systems (ext4, XFS, ZFS), block layer, I/O scheduling (CFQ, deadline, noop, mq-deadline)
- **Key Exercise:** Profile memory bandwidth and latency under different access patterns (sequential, random, strided). Correlate with DRAM row buffer behavior.

---

## Phase 4: Instruction Set Architecture & Assembly

> **Objective:** Develop fluency in low-level programming. Understand how high-level code maps to machine instructions and how to optimize at the assembly level.

### 4.1 x86-64 Architecture
- **Registers:** General-purpose (RAX, RBX, etc.), segment registers, RFLAGS, XMM/YMM/ZMM (AVX/AVX-512)
- **Addressing Modes:** Register, immediate, direct, indirect, indexed, scaled index, RIP-relative
- **Instruction Encoding:** Opcode, ModR/M, SIB, displacement, immediate, prefix bytes, instruction length
- **System Instructions:** SYSCALL/SYSRET, interrupts, I/O instructions, privileged operations
- **Key Exercise:** Write a function in x86-64 assembly implementing a linked list traversal. Call it from C. Profile with perf.

### 4.2 ARM64 (AArch64) Architecture
- **Registers:** X0-X30, SP, PC (implicit), V0-V31 (SIMD), system registers
- **Instruction Encoding:** Fixed 32-bit, opcode fields, conditional execution (removed in AArch64), compare-and-branch
- **Load/Store Architecture:** Only LDR/STR access memory, addressing modes (pre-indexed, post-indexed, signed offset)
- **SIMD/NEON & SVE:** Vector registers, predication, scatter-gather, SVE variable vector length
- **Key Exercise:** Implement a dot product kernel in ARM64 assembly using NEON. Compare performance with compiler-generated code.

### 4.3 RISC-V Assembly
- **Base Integer ISA (RV32I/RV64I):** Register conventions, immediate types (I, S, B, U, J), instruction formats
- **Standard Extensions:** M (multiply/divide), A (atomic), F/D (float/double), C (compressed)
- **Privilege Architecture:** M-mode, S-mode, U-mode, CSR registers, exception handling, interrupts
- **Calling Convention:** Integer argument registers (a0-a7), return values, stack alignment, frame pointers
- **Key Exercise:** Write a context switch routine in RISC-V assembly. Save/restore registers. Implement a minimal cooperative scheduler.

### 4.4 Calling Conventions & ABI
- **System V AMD64 ABI:** Register usage, stack frame layout, red zone, argument passing (integer, float, struct), varargs
- **ARM64 AAPCS:** Parameter passing (X0-X7, V0-V7), stack alignment (16-byte), homogenous aggregates
- **Stack Management:** Stack frames, frame pointers (rbp/x29), stack canaries, stack unwinding (DWARF)
- **Key Exercise:** Manually generate stack frames for a recursive function. Trace with GDB. Examine DWARF unwind info.

### 4.5 Inline Assembly & Intrinsics
- **GCC Inline Assembly:** Extended asm syntax, input/output operands, clobbers, constraints, memory barriers
- **Compiler Intrinsics:** SSE/AVX intrinsics (`_mm_add_ps`), NEON intrinsics, RISC-V vector intrinsics
- **When to Use:** Compiler limitations, specific instruction needs, cycle-accurate control
- **Key Exercise:** Implement a memcpy using AVX-512 intrinsics. Compare with libc memcpy across sizes. Analyze with IACA/LLVM-MCA.

---

## Phase 5: Operating Systems & System Programming

> **Objective:** Master the operating system as a hardware abstraction layer. Understand kernel internals, system calls, and the production implications of OS design decisions.

### 5.1 Process Management
- **Process Abstraction:** PCB, states (new, ready, running, waiting, terminated), context switching
- **Scheduling Algorithms:** FCFS, SJF, SRTF, priority, round-robin, multilevel feedback queue, CFS (Completely Fair Scheduler)
- **Real-Time Scheduling:** Rate-monotonic, earliest-deadline-first, priority inheritance, priority ceiling
- **Kernel Threads vs. User Threads:** 1:1, N:1, M:N models, pthreads, green threads, goroutines
- **Key Exercise:** Implement a minimal round-robin scheduler in a kernel module or userspace simulation. Measure context switch overhead.

### 5.2 Memory Management
- **Virtual Memory:** Paging, segmentation, page tables, TLB, demand paging, copy-on-write
- **Page Replacement:** FIFO, LRU (clock algorithm), NRU, working set model, thrashing detection
- **Memory Allocation:** Buddy system, slab allocator, jemalloc, tcmalloc, ptmalloc — fragmentation, locality
- **Huge Pages:** Standard (4KB) vs. huge (2MB, 1GB), TLB pressure, transparent huge pages (THP), madvise
- **Key Exercise:** Profile memory allocation patterns of a real application. Switch allocators. Measure fragmentation and performance.

### 5.3 Concurrency & Synchronization
- **Concurrency Primitives:** Mutexes, semaphores, condition variables, read-write locks, barriers
- **Lock-Free Programming:** Lock-free vs. wait-free, ABA problem, hazard pointers, epoch-based reclamation
- **Memory Ordering:** Acquire-release semantics, sequential consistency, compiler barriers, hardware fences
- **Classic Problems:** Producer-consumer, readers-writers, dining philosophers, sleeping barber
- **Key Exercise:** Implement a lock-free queue (Michael-Scott). Prove correctness. Benchmark against mutex-based queue.

### 5.4 File Systems & I/O
- **File System Internals:** Inodes, directories, hard links, symbolic links, journaling, copy-on-write (Btrfs, ZFS)
- **Block I/O:** Buffer cache, page cache, direct I/O, async I/O (io_uring, libaio), vectored I/O
- **I/O Scheduling:** Elevator algorithms, deadline, CFQ, BFQ, mq-deadline, hardware queues
- **Network I/O:** Synchronous vs. asynchronous, epoll/kqueue/IOCP, zero-copy (sendfile, splice), DPDK
- **Key Exercise:** Implement a minimal log-structured file system (LFS) in userspace. Measure write amplification and read performance.

### 5.5 System Calls & Kernel Internals
- **System Call Interface:** Trap instructions, syscall numbers, parameter passing, return values, errno
- **Kernel Architecture:** Monolithic (Linux), microkernel (seL4, QNX), hybrid, exokernel
- **Kernel Modules:** Loadable kernel modules (LKM), device drivers, character vs. block devices
- **eBPF:** Extended Berkeley Packet Filter, verifier, maps, kprobes/uprobes, performance implications
- **Key Exercise:** Write a Linux kernel module that intercepts a system call. Log arguments. Measure overhead.

---

## Phase 6: Compiler Design & Code Generation

> **Objective:** Understand how high-level code becomes executable. Master compiler internals to reason about optimization, debugging, and performance.

### 6.1 Lexical Analysis & Parsing
- **Regular Expressions & Finite Automata:** NFA to DFA conversion, minimal DFA, lexer generators (flex)
- **Context-Free Grammars:** Productions, derivations, parse trees, ambiguity, left recursion elimination
- **Parsing Algorithms:** LL(1) recursive descent, LR(0), SLR, LR(1), LALR(1), GLR, parser generators (bison, ANTLR)
- **Abstract Syntax Trees (AST):** Design, traversal, semantic analysis, symbol tables
- **Key Exercise:** Write a recursive descent parser for a subset of C. Generate AST. Implement pretty-printer.

### 6.2 Semantic Analysis & Intermediate Representation
- **Type Checking:** Static vs. dynamic typing, type inference (Hindley-Milner), polymorphism
- **Symbol Tables:** Scoping (lexical vs. dynamic), name resolution, overloading resolution
- **Intermediate Representations:** Three-address code, SSA (Static Single Assignment), CFG (Control Flow Graph)
- **Key Exercise:** Convert AST to SSA form. Implement a simple constant propagation pass.

### 6.3 Code Generation & Optimization
- **Instruction Selection:** Tree pattern matching, tiling, maximal munch, dynamic programming approach
- **Register Allocation:** Graph coloring, live variable analysis, interference graphs, spilling, coalescing
- **Optimization Passes:** Constant folding, dead code elimination, common subexpression elimination, loop optimizations (invariant code motion, strength reduction, unrolling, vectorization)
- **Alias Analysis:** Type-based, flow-sensitive, context-sensitive, restrict keyword
- **Key Exercise:** Implement a register allocator using graph coloring for a simple IR. Handle spilling.

### 6.4 Linking & Loading
- **Object File Formats:** ELF structure, sections (.text, .data, .bss, .symtab, .rel.*), symbol tables, relocation entries
- **Static Linking:** Symbol resolution, relocation, archive libraries (.a), symbol precedence, common blocks
- **Dynamic Linking:** Shared libraries (.so), PLT/GOT, lazy binding, position-independent code (PIC), prelinking
- **Loading:** Program headers, memory mapping, dynamic linker (ld-linux.so), RTLD_NEXT, LD_PRELOAD
- **Key Exercise:** Write a minimal dynamic linker. Load a simple ELF executable. Resolve symbols. Handle relocations.

### 6.5 Modern Compiler Infrastructure
- **LLVM Architecture:** IR, passes, PassManager, LLVM IR syntax, optimization levels (-O0 to -O3, -Os, -Oz)
- **Clang Frontend:** AST matchers, libTooling, refactoring, static analysis (Clang Static Analyzer)
- **GCC Internals:** GIMPLE, RTL, optimization passes, profile-guided optimization (PGO), link-time optimization (LTO)
- **JIT Compilation:** LLVM ORC, libgccjit, tracing JIT (LuaJIT), method-at-a-time JIT
- **Key Exercise:** Write an LLVM pass that instruments every function entry/exit with timing calls. Compile and test on a real program.

---

## Phase 7: Performance Engineering & Optimization

> **Objective:** Develop the ability to make software fast. Master profiling, optimization, and the art of performance reasoning.

### 7.1 Performance Measurement
- **Metrics:** Latency, throughput, bandwidth, IOPS, CPI, IPC, cache miss rate, branch misprediction rate
- **Profiling Tools:** perf (Linux), VTune (Intel), uProf (AMD), gprof, callgrind, flame graphs
- **Microbenchmarking:** Google Benchmark, Catch2, pitfalls (warmup, noise, statistical significance)
- **Roofline Model:** Operational intensity, memory bandwidth bound vs. compute bound, identifying bottlenecks
- **Key Exercise:** Profile a matrix multiplication kernel. Generate roofline plot. Identify if memory-bound or compute-bound.

### 7.2 CPU Microarchitecture-Aware Optimization
- **Instruction-Level Parallelism:** Superscalar execution, dependency chains, out-of-order window, register renaming
- **SIMD Vectorization:** SSE/AVX/AVX-512, NEON, SVE, auto-vectorization hints, manual intrinsics, alignment
- **Branch Prediction:** Branchless programming, likely/unlikely hints, branch target buffers, indirect branch prediction
- **Loop Optimizations:** Unrolling, software pipelining, loop interchange, loop tiling/blocking for cache
- **Key Exercise:** Optimize a hot loop in a real application. Achieve 10x speedup through vectorization + tiling.

### 7.3 Memory Hierarchy Optimization
- **Cache-Aware Algorithms:** Blocking/tiling, cache-oblivious algorithms (Funnel sort, cache-oblivious B-trees)
- **Prefetching:** Software prefetch intrinsics (`_mm_prefetch`), hardware stride detection, prefetch distance tuning
- **Data Layout:** Structure of Arrays (SoA) vs. Array of Structures (AoS), padding, alignment, false sharing avoidance
- **NUMA Awareness:** Local memory allocation (`numactl`), thread pinning, first-touch policy, interleaved allocation
- **Key Exercise:** Optimize a graph algorithm (BFS/DFS) for cache efficiency. Compare AoS vs. SoA. Measure L1/L2/L3 miss rates.

### 7.4 I/O & Network Optimization
- **Zero-Copy:** `sendfile`, `splice`, `mmap`, DPDK, kernel bypass
- **Async I/O:** io_uring (Linux 5.1+), libaio, epoll, io_uring performance characteristics
- **Memory-Mapped Files:** `mmap`/`munmap`, page fault overhead, madvise hints, huge page backing
- **Network Stack Optimization:** TCP tuning (window scaling, timestamps, fast open), kernel bypass (DPDK, RDMA)
- **Key Exercise:** Build a high-throughput file server using io_uring. Benchmark against epoll-based implementation.

### 7.5 Lock-Free & Wait-Free Algorithms
- **Atomic Operations:** C11/C++11 `std::atomic`, memory_order variants, compare-and-swap loops
- **Lock-Free Data Structures:** Stacks, queues, lists, hash tables — design patterns and correctness arguments
- **RCU (Read-Copy-Update):** Linux RCU, quiescent states, grace periods, performance characteristics
- **Hazard Pointers & Epoch-Based Reclamation:** Safe memory reclamation in lock-free structures
- **Key Exercise:** Implement a lock-free hash table with RCU-style updates. Benchmark read-heavy workload.

---

## Phase 8: Modern CPU Microarchitecture

> **Objective:** Understand contemporary processors at the RTL/microarchitecture level. Reason about speculative execution, security implications, and performance characteristics.

### 8.1 Out-of-Order Execution Deep Dive
- **Reservation Stations:** Dispatch, issue, execution, writeback — Tomasulo's algorithm revisited
- **Reorder Buffer (ROB):** In-order commit, precise exceptions, branch misprediction recovery
- **Register Renaming:** Architectural vs. physical registers, register alias table (RAT), free list
- **Load-Store Queue:** Memory disambiguation, store-to-load forwarding, speculative loads
- **Key Exercise:** Simulate a 4-wide OoO processor with ROB, RS, and LSQ. Measure IPC on traces.

### 8.2 Speculative Execution & Security
- **Branch Prediction Deep Dive:** TAGE, perceptron, loop predictors, indirect branch prediction, return address stack
- **Speculative Execution:** Speculative loads, memory dependence prediction, value prediction
- **Side-Channel Attacks:** Cache timing (Flush+Reload, Prime+Probe), Spectre (v1, v2, v4), Meltdown, Foreshadow
- **Mitigations:** Retpoline, IBPB, IBRS, STIBP, L1TF mitigations, hardware fixes (e.g., Intel CET)
- **Key Exercise:** Implement a Spectre v1 proof-of-concept. Measure cache side channel. Apply mitigations and verify elimination.

### 8.3 Simultaneous Multithreading (SMT) & Multi-Core
- **SMT/Hyper-Threading:** Shared resources (frontend, execution units, caches), thread scheduling, throughput vs. single-thread latency
- **Cache Hierarchy in Multi-Core:** Private L1/L2, shared L3, inclusive vs. exclusive, cache slicing
- **Inter-Core Communication:** Cache coherence traffic, snoop filters, directory protocols, on-chip networks
- **Core Pinning & Affinity:** `sched_setaffinity`, NUMA topology, thread placement strategies
- **Key Exercise:** Measure performance of a shared-data workload with/without SMT. Analyze cache coherence traffic with perf c2c.

### 8.4 Hardware Performance Counters
- **PMU (Performance Monitoring Unit):** Architectural vs. model-specific events, event multiplexing
- **Key Events:** Cycles, instructions, cache references/misses, branch instructions/misses, stall cycles
- **Top-Down Analysis:** Frontend bound, backend bound, bad speculation, retiring — Intel's top-down microarchitecture analysis
- **Linux perf:** `perf stat`, `perf record`, `perf report`, `perf annotate`, PEBS, LBR (Last Branch Record)
- **Key Exercise:** Perform top-down analysis of a production workload. Identify the primary bottleneck category. Propose and validate optimization.

### 8.5 Emerging CPU Architectures (2026)
- **ARM Neoverse:** V1/N2/N3 microarchitecture, SVE2, CMN-700 mesh interconnect, cloud-native design
- **Intel P-Core/E-Core:** Hybrid architecture (Alder Lake/Raptor Lake/Meteor Lake), thread director, scheduler challenges
- **AMD Zen 5:** Core architecture, cache hierarchy, chiplet design, Infinity Fabric
- **RISC-V Implementations:** SiFive P550/P650, BOOM (Berkeley Out-of-Order Machine), CVA6
- **Key Exercise:** Benchmark the same workload on Intel P-core vs. E-core. Analyze scheduler decisions. Measure power efficiency.

---

## Phase 9: GPU Architecture & Heterogeneous Computing

> **Objective:** Master GPU architecture for AI/ML workloads. Understand CUDA programming, memory hierarchies, and the implications for distributed training and inference.

### 9.1 GPU Architecture Fundamentals
- **GPU vs. CPU Design Philosophy:** Throughput-oriented vs. latency-oriented, SIMT (Single Instruction, Multiple Threads), warps/wavefronts
- **NVIDIA GPU Architecture:** Streaming Multiprocessors (SM), CUDA cores, Tensor Cores, RT Cores, memory hierarchy
- **AMD GPU Architecture:** Compute Units (CU), Wavefronts, RDNA/CDNA architecture differences
- **Memory Hierarchy:** Registers, shared memory/L1, L2 cache, global memory (GDDR/HBM), unified memory
- **Key Exercise:** Draw the memory hierarchy of an A100/H100. Calculate bandwidth and latency at each level.

### 9.2 CUDA Programming Model
- **Kernel Execution:** Grid, blocks, threads, warps, thread divergence, occupancy
- **Memory Management:** `cudaMalloc`, `cudaMemcpy`, unified memory, pinned memory, zero-copy
- **Synchronization:** `__syncthreads()`, block-level, grid-level (`cudaDeviceSynchronize`), stream semantics
- **Streams & Concurrency:** Default stream, explicit streams, stream priorities, overlapping compute and transfer
- **Key Exercise:** Implement matrix multiplication in CUDA. Optimize for shared memory tiling. Profile with Nsight Compute.

### 9.3 GPU Memory Optimization
- **Coalesced Memory Access:** Thread memory access patterns, warp coalescing, strided access penalties
- **Shared Memory:** Bank conflicts, padding strategies, dynamic shared memory, `__shared__` qualifier
- **Constant & Texture Memory:** Read-only caches, caching behavior, use cases
- **Global Memory Throughput:** Memory transactions, cache line utilization, L2 cache optimization
- **Key Exercise:** Optimize a reduction kernel. Achieve >80% of peak memory bandwidth. Document optimization steps.

### 9.4 Advanced CUDA & Tensor Cores
- **Warp-Level Primitives:** `__shfl_sync`, `__ballot`, `__activemask`, warp-level reductions
- **Tensor Cores:** WMMA API, MMA instructions, mixed-precision (FP16/BF16/INT8/FP8), accumulator precision
- **CUDA Graphs:** Capture and replay, reducing CPU launch overhead, stream capture
- **Multi-GPU Programming:** Peer-to-peer access, NVLink, NVSwitch, unified virtual addressing (UVA)
- **Key Exercise:** Implement a GEMM using Tensor Cores (WMMA). Compare performance with cuBLAS. Analyze numerical accuracy.

### 9.5 GPU Profiling & Optimization
- **Nsight Compute:** Kernel-level profiling, memory throughput analysis, instruction mix, stall reasons
- **Nsight Systems:** Timeline analysis, CPU-GPU synchronization, stream visualization, bottleneck identification
- **Roofline for GPUs:** Operational intensity, memory bandwidth bound vs. compute bound (FP32, FP16, Tensor Core)
- **Occupancy Calculator:** Register pressure, shared memory usage, block size tuning
- **Key Exercise:** Profile a production deep learning training step. Identify the limiting factor (memory bandwidth, compute, or synchronization). Optimize and remeasure.

### 9.6 Distributed GPU Computing
- **NCCL:** Collective operations (all-reduce, all-gather, reduce-scatter, broadcast), ring/tree algorithms
- **NVLink & NVSwitch:** Topology, bandwidth, multi-node scaling, DGX/HGX systems
- **GPUDirect RDMA:** Direct GPU-to-GPU communication across nodes, bypassing CPU memory
- **Multi-Node Training:** Data parallelism, model parallelism (tensor + pipeline), 3D parallelism, ZeRO
- **Key Exercise:** Implement a ring all-reduce using NCCL. Measure bandwidth efficiency on 8 GPUs. Analyze scaling efficiency.

---

## Phase 10: Systems Security & Hardware Hardening

> **Objective:** Understand security from the hardware up. Build systems that are resilient to attacks at every layer.

### 10.1 Hardware Security Primitives
- **Trusted Execution Environments (TEE):** Intel SGX, AMD SEV, ARM TrustZone, Apple Secure Enclave
- **Memory Encryption:** TME (Total Memory Encryption), SME, SEV-ES, SEV-SNP
- **Secure Boot:** UEFI Secure Boot, measured boot, TPM (Trusted Platform Module), PCR registers
- **Hardware Roots of Trust:** Root of trust for measurement (RTM), root of trust for storage (RTS), root of trust for reporting (RTR)
- **Key Exercise:** Enable AMD SEV on a VM. Verify memory encryption. Measure performance overhead.

### 10.2 Side-Channel & Speculative Attack Mitigations
- **Cache-Based Attacks:** Flush+Reload, Prime+Probe, Evict+Time, cache occupancy channels
- **Transient Execution Attacks:** Spectre variants, Meltdown, MDS (Microarchitectural Data Sampling), L1TF
- **Hardware Mitigations:** CET (Control-flow Enforcement Technology), IBT (Indirect Branch Tracking), HFI (Hardware-enforced Fine-grained Isolation)
- **Software Mitigations:** Site isolation, retpoline, lfence insertion, constant-time programming
- **Key Exercise:** Implement a constant-time string comparison. Verify with cache timing measurements.

### 10.3 Memory Safety & Exploitation
- **Buffer Overflows:** Stack smashing, heap overflows, format string bugs, integer overflows
- **Modern Exploitation:** ASLR, NX/DEP, stack canaries, RELRO, CFI (Control-Flow Integrity), PAC (Pointer Authentication)
- **Memory-Safe Languages:** Rust ownership model, borrow checker, lifetimes, zero-cost abstractions
- **Sandboxing:** seccomp-bpf, namespaces, cgroups, gVisor, WebAssembly sandboxing
- **Key Exercise:** Write a buffer overflow exploit (controlled environment). Apply mitigations one by one. Measure effectiveness.

### 10.4 Cryptographic Hardware Acceleration
- **AES-NI:** Intel/AMD AES instructions, performance vs. software implementation
- **SHA Extensions:** SHA-1/SHA-256 acceleration, ARMv8 Cryptographic Extensions
- **Post-Quantum Cryptography:** Lattice-based algorithms, NIST standards, hardware implications
- **Random Number Generation:** RDRAND/RDSEED, hardware RNG, entropy pools, `/dev/random` vs. `/dev/urandom`
- **Key Exercise:** Implement AES-GCM using AES-NI intrinsics. Compare throughput with OpenSSL. Verify constant-time properties.

---

## Capstone Projects

> **Objective:** Demonstrate mastery by building production-grade systems from first principles. Each project should be portfolio-ready and include architecture diagrams, performance benchmarks, and operational documentation.

### Capstone 1: RISC-V Processor Implementation
**Scope:** Implement a complete 5-stage pipelined RISC-V RV32IM processor in Verilog.
**Requirements:**
- Implement all base integer and multiply/divide instructions
- Include forwarding, hazard detection, and branch prediction (2-bit saturating counter)
- Pass RISC-V ISA tests (riscv-tests)
- Synthesize to FPGA (e.g., Xilinx Artix-7). Report maximum clock frequency and resource utilization
- Write an assembler in Python/C that generates machine code from assembly

### Capstone 2: High-Performance Memory Allocator
**Scope:** Build a production-quality memory allocator for multi-threaded applications.
**Requirements:**
- Implement per-thread caches, size classes, and central heap
- Support scalable allocation/deallocation with low fragmentation
- Include debugging features (double-free detection, use-after-free detection in debug mode)
- Benchmark against jemalloc and tcmalloc on real workloads (e.g., RocksDB, Redis)
- Document thread scaling and fragmentation behavior

### Capstone 3: Optimized BLAS Kernel
**Scope:** Implement a DGEMM (double-precision matrix multiply) kernel achieving >80% of peak CPU performance.
**Requirements:**
- Implement in C with SIMD intrinsics (AVX-512 or NEON)
- Use cache blocking/tiling for L1, L2, and L3
- Include micro-kernel with optimal register usage
- Benchmark against OpenBLAS/MKL. Generate roofline plot
- Document optimization decisions and performance analysis

### Capstone 4: GPU-Accelerated Training Kernel
**Scope:** Implement a fused optimizer kernel for deep learning training.
**Requirements:**
- Fuse AdamW update into a single CUDA kernel (avoiding separate kernels for each operation)
- Support mixed precision (FP16/FP32 master weights)
- Optimize for coalesced access and shared memory usage
- Integrate with PyTorch via custom C++/CUDA extension
- Benchmark against PyTorch native AdamW. Measure memory bandwidth and compute utilization

### Capstone 5: Secure System Call Monitor
**Scope:** Build an eBPF-based system call monitoring and enforcement system.
**Requirements:**
- Trace all system calls with arguments using kprobes/tracepoints
- Implement a policy engine in userspace (allowlist/blocklist)
- Enforce policies in-kernel via eBPF LSM hooks or kprobes with `bpf_override_return`
- Include performance overhead analysis (<5% overhead target)
- Write comprehensive tests and documentation for production deployment

---

## Assessment & Certification Rubric

### Knowledge Assessment
- **Theory Exams:** Closed-book exams on digital logic, computer architecture, operating systems, and compiler theory
- **Code Reviews:** Review of HDL, assembly, C, and CUDA code for correctness, efficiency, and style
- **Architecture Reviews:** Design reviews of capstone projects focusing on trade-off analysis and correctness arguments

### Practical Assessment
- **Debugging Challenges:** Intentionally broken systems (simulator hangs, memory leaks, race conditions) that candidates must diagnose
- **Performance Optimization:** Given a slow system, achieve target performance with profiling evidence
- **Security Audit:** Simulated security assessment requiring vulnerability identification and mitigation

### Certification Levels
- **Level 1 — Practitioner:** Completes Phases 1–5, passes theory exams, completes Capstone 1
- **Level 2 — Specialist:** Completes Phases 1–8, passes practical assessments, completes Capstones 1–3
- **Level 3 — Expert:** Completes all phases, leads architecture reviews, completes all capstones with production deployment evidence

---

## Recommended Reading & Reference Library

### Foundational Textbooks
1. **"Computer Organization and Design"** — Patterson & Hennessy (RISC-V edition)
2. **"Computer Architecture: A Quantitative Approach"** — Hennessy & Patterson
3. **"Modern Operating Systems"** — Tanenbaum & Bos
4. **"Compilers: Principles, Techniques, and Tools"** — Aho, Lam, Sethi, Ullman (Dragon Book)
5. **"Computer Systems: A Programmer's Perspective"** — Bryant & O'Hallaron (CS:APP)
6. **"The Art of Computer Systems Performance Analysis"** — Jain
7. **"What Every Programmer Should Know About Memory"** — Ulrich Drepper (free)

### Hardware & Architecture Papers
- **"The RISC-V Instruction Set Manual"** — Waterman, Asanovic, et al.
- **"Zen 2: The AMD Next-Generation Core"** — AMD HotChips presentation
- **"A New Golden Age for Computer Architecture"** — Hennessy & Patterson (Turing Lecture)
- **"Efficient Memory Disambiguation"** — Moshovos et al.

### GPU & CUDA Resources
- **"Programming Massively Parallel Processors"** — Kirk & Hwu
- **NVIDIA CUDA C Programming Guide**
- **CUDA Best Practices Guide**
- **Nsight Compute/Systems Documentation**

### Security & Systems
- **"The Shellcoder's Handbook"** — Anley et al.
- **"Hacking: The Art of Exploitation"** — Erickson
- **"Security Engineering"** — Ross Anderson (free online)
- **Intel 64 and IA-32 Architectures Software Developer's Manual** (volumes 1-4)

### Tools & References
- **RISC-V ISA Simulator (Spike):** https://github.com/riscv-software-src/riscv-isa-sim
- **Chisel/Firrtl:** Hardware construction language
- **LLVM Documentation:** https://llvm.org/docs/
- **Linux Kernel Documentation:** https://www.kernel.org/doc/html/latest/
- **perf wiki:** https://perf.wiki.kernel.org/

### Courses
- **6.004: Computation Structures** (MIT) — Digital logic to processor design
- **6.823: Computer System Architecture** (MIT) — Advanced architecture
- **CS110: Principles of Computer Systems** (Stanford) — Systems programming
- **CS143: Compilers** (Stanford) — Full compiler construction
- **ECE 598: GPU Programming** (UIUC/Various) — CUDA and optimization

---

## Appendix: Glossary of Terms

| Term | Definition |
|------|------------|
| **ALU** | Arithmetic Logic Unit |
| **AMAT** | Average Memory Access Time |
| **CPI** | Cycles Per Instruction |
| **CMOS** | Complementary Metal-Oxide-Semiconductor |
| **D$ / I$** | Data Cache / Instruction Cache |
| **DMA** | Direct Memory Access |
| **DRAM** | Dynamic Random Access Memory |
| **ELF** | Executable and Linkable Format |
| **FPGA** | Field-Programmable Gate Array |
| **HBM** | High Bandwidth Memory |
| **IPC** | Instructions Per Cycle |
| **ISA** | Instruction Set Architecture |
| **MESI** | Cache coherence protocol (Modified, Exclusive, Shared, Invalid) |
| **MMU** | Memory Management Unit |
| **MSHR** | Miss Status Handling Register |
| **NCCL** | NVIDIA Collective Communications Library |
| **NUMA** | Non-Uniform Memory Access |
| **OoO** | Out-of-Order execution |
| **PCB** | Process Control Block |
| **PLT/GOT** | Procedure Linkage Table / Global Offset Table |
| **RISC-V** | Open ISA standard |
| **ROB** | Reorder Buffer |
| **SIMD** | Single Instruction, Multiple Data |
| **SIMT** | Single Instruction, Multiple Threads |
| **SoC** | System on Chip |
| **SRAM** | Static Random Access Memory |
| **SSA** | Static Single Assignment |
| **TEE** | Trusted Execution Environment |
| **TLB** | Translation Lookaside Buffer |
| **VTune** | Intel performance profiler |
| **Warp** | Group of threads executed together in SIMT |

---

## Final Notes

This syllabus represents a comprehensive, bottom-up curriculum for computer architecture and low-level systems engineering. It is designed to be iterative — revisit earlier phases as you advance, as deeper understanding reveals new connections between layers of abstraction.

**The ultimate goal is not just to write code, but to understand the entire stack from silicon to software deeply enough to build, optimize, debug, and secure systems at any scale.**

---

*Document Version: 2026.05.17*  
*Maintained by: Senior Curriculum Designer — Systems & Architecture Track*  
*Next Review Date: 2026.08.17*