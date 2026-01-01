# Rebuilding the Systems Stack

## A Formal Syllabus for Systems Software, AI Systems, and Real-Time XR

**Audience:** Start-up founder · Research-adjacent builder  
**Mode:** Full immersion · Build-first  
**Target Platform:** Linux desktop + GPU  
**Focus Areas:**

- Systems Software
    
- Computer Systems
    
- AI Systems (Inference & Runtime)
    
- XR / Real-Time Systems
    
- Hardware, Energy, and Security Awareness
    

---

## 1. Program Philosophy

This syllabus reconstructs the computing stack **bottom-up**, emphasizing _physical reality_, _constraints_, and _measurable performance_.

> You are not learning tools.  
> You are learning what abstractions hide — and where they fail.

Core principles:

- Performance is physical
    
- Memory and time dominate all systems
    
- Abstractions leak
    
- Systems outlast frameworks
    
- Constraints create leverage
    

---

## 2. Required Environment & Toolchain

### Operating System

- Linux (Ubuntu 22.04 LTS recommended)
    

### Core Languages

- C (primary)
    
- C++
    
- Python (AI systems only)
    
- CUDA / GPU kernels
    
- Optional later: Rust
    

### Core Tools

- `clang`, `gcc`
    
- `gdb`
    
- `perf`
    
- `valgrind`
    
- `objdump`
    
- `strace`
    
- `cmake`, `ninja`
    
- `git`
    

### GPU Tooling

- NVIDIA GPU + CUDA Toolkit
    
- Nsight Systems / Nsight Compute
    
- cuBLAS, cuDNN
    
- Vulkan SDK
    

---

## 3. Mathematical & Physical Lens (Integrated)

Mathematics and hardware realities are **woven into each phase**, not taught separately.

### Mathematical focus (applied only):

- Discrete logic & invariants (correctness)
    
- Linear algebra (SIMD, GPU, ML)
    
- Probability & statistics (latency, queues, tails)
    
- Information theory (bandwidth, compression)
    
- Numerical methods (quantization, approximation)
    
- Optimization under constraints (scheduling, budgets)
    

### Hardware & energy awareness:

- Performance-per-watt
    
- DVFS and thermal throttling
    
- Power-aware scheduling
    
- Data-center vs edge constraints
    

---

# CORE CURRICULUM

---

## Phase 0 — Toolchain & Systems Mindset

**Goal:** Remove abstraction myths and build low-level intuition

**Topics**

- C memory model
    
- Pointers, stack vs heap
    
- Undefined behavior
    
- Assembly inspection
    
- Debugging reality
    

**Languages & Tools**

- C
    
- clang, gdb, objdump, perf, valgrind
    

**References**

- _Computer Systems: A Programmer’s Perspective_ (selected chapters)
    

**Mastery Projects**

- Manual memory allocator
    
- UB experiments and writeups
    
- Assembly inspection of compiled code
    

---

## Phase 1 — Computer Architecture & Memory

**Goal:** Understand the physics of computation

**Topics**

- Pipelines, ILP, OoO execution
    
- Branch prediction
    
- Cache hierarchy
    
- NUMA
    
- SIMD
    
- CPU vs GPU memory models
    

**Math Focus**

- Throughput vs latency
    
- Roofline model
    

**Languages & Tools**

- C
    
- perf, hwloc, numactl
    

**References**

- _Computer Architecture: A Quantitative Approach_ — Hennessy & Patterson
    

**Mastery Projects**

- CPU cache benchmark suite
    
- False-sharing demonstration
    
- SIMD vs scalar benchmarks
    
- CPU vs GPU memory bandwidth profiler
    

---

## Phase 2 — Instruction Sets & Memory Models

**Goal:** Understand concurrency at the hardware level

**Topics**

- x86-64 / ARM assembly
    
- Memory ordering
    
- Atomics
    
- Cache coherence (MESI)
    
- Happens-before
    

**Languages & Tools**

- C
    
- clang, objdump, perf
    

**References**

- _Computer Systems: A Programmer’s Perspective_
    

**Mastery Projects**

- Broken and fixed spinlocks
    
- Atomic counter benchmarks
    
- Instruction reordering experiments
    

---

## Phase 3 — Operating Systems

**Goal:** Understand OS illusions and boundaries

**Topics**

- Processes vs threads
    
- Scheduling
    
- Virtual memory
    
- Page faults
    
- Syscalls
    
- IO stacks
    
- Filesystems
    

**Languages & Tools**

- C
    
- strace, perf, vmstat
    

**References**

- _Operating Systems: Three Easy Pieces_
    

**Mastery Projects**

- User-space scheduler
    
- Custom memory allocator
    
- Simple filesystem
    
- `mmap` vs `read` performance analysis
    

---

## Phase 4 — Concurrency & Parallelism

**Goal:** Build correct and scalable systems

**Topics**

- Lock-free data structures
    
- ABA problem
    
- Memory reclamation
    
- Work stealing
    
- Backpressure
    
- Queueing theory (Little’s Law)
    

**Languages & Tools**

- C / C++
    
- perf, thread sanitizers
    

**References**

- _The Art of Multiprocessor Programming_
    

**Mastery Projects**

- Lock-free queue
    
- Bounded MPMC queue
    
- Work-stealing thread pool
    

---

## Phase 5 — Compilers & Runtimes

**Goal:** Understand abstraction collapse

**Topics**

- Compilation pipeline
    
- LLVM IR
    
- Optimization passes
    
- Vectorization
    
- Register allocation
    
- JIT vs AOT
    
- Garbage collection basics
    

**Languages & Tools**

- C / C++
    
- LLVM, clang, objdump
    

**References**

- _Engineering a Compiler_
    
- _Crafting Interpreters_
    

**Mastery Projects**

- Tiny compiler (expressions → assembly)
    
- LLVM optimization pass
    
- Vectorization failure analysis
    
- Mini JIT
    

---

## Phase 6 — Networking & Distributed Systems

**Goal:** Reason about time and failure at scale

**Topics**

- TCP vs QUIC
    
- Latency vs throughput
    
- Clocks and time
    
- Consensus (Raft)
    
- Replication
    
- Logs
    
- CAP & invariants
    

**Languages & Tools**

- C / C++
    
- tcpdump, wireshark
    

**References**

- _Designing Data-Intensive Applications_
    
- MIT 6.824 materials
    

**Mastery Projects**

- Reliable UDP protocol
    
- Replicated log
    
- Raft-based key-value store
    

---

## Phase 7 — Storage & Database Engines

**Goal:** Build durable data substrates

**Topics**

- WAL
    
- LSM trees
    
- B-trees
    
- MVCC
    
- Indexing
    
- Query planning
    
- Columnar storage
    

**Languages & Tools**

- C / C++
    
- fio, perf
    

**References**

- _Database Internals_ — Alex Petrov
    

**Mastery Projects**

- KV store with WAL
    
- LSM tree implementation
    
- B-tree
    
- Mini query engine
    

---

# SPECIALIZATION CORE

---

## Phase 8 — GPU Systems & Real-Time (AI + XR Core)

**Goal:** Make compute run under real-time constraints

**Topics**

- GPU architecture
    
- CUDA / Vulkan compute
    
- Async compute
    
- Frame budgets
    
- Scheduling graphics + ML
    
- Foveated rendering
    
- Motion-to-photon latency
    

**Math Focus**

- Matrix math intuition
    
- Latency budgets
    

**Languages & Tools**

- C++, CUDA
    
- Nsight, nvidia-smi, Vulkan SDK
    

**References**

- _Programming Massively Parallel Processors_
    
- NVIDIA CUDA Programming Guide
    

**Mastery Projects**

- GPU kernel benchmarks
    
- Mixed graphics + ML workload
    
- Real-time render loop with frame pacing
    

---

## Phase 9 — AI Systems Deep Dive

**Goal:** Become an AI systems engineer

**Topics**

- Transformer execution
    
- Attention memory complexity
    
- KV cache management
    
- Quantization (INT8 / INT4)
    
- Inference scheduling
    
- Edge inference
    
- Verifiable inference (conceptual)
    

**Languages & Tools**

- C++, CUDA, Python
    
- CUDA, TensorRT, GPU profilers
    

**References**

- Stanford CS329S (ML Systems)
    
- NVIDIA inference optimization documentation
    

**Mastery Projects**

- Inference engine prototype
    
- Quantized model runner
    
- Memory-efficient attention implementation
    
- Real-time inference under strict latency budgets
    

---

## Phase 10 — Capstone (Founder Mode)

**Goal:** Demonstrate end-to-end systems mastery

**Choose One**

- Real-time AI engine for XR
    
- Edge AI runtime
    
- Simulation engine for AI agents
    
- GPU scheduling platform
    

**Requirements**

- Real hardware
    
- Measured performance
    
- Clear constraints
    
- Written design document
    
- Failure and tradeoff analysis
    

**Outcome**

- Investor-credible
    
- Research-adjacent
    
- Systems-native product
    

---

## Optional Extension — Systems Security & Applied Cryptography

**Topics**

- Memory exploitation
    
- Fuzzing (AFL, libFuzzer)
    
- Sandboxing & seccomp
    
- TEEs and attestation
    
- Secure boot
    
- Cryptographic protocols in systems
    

**Outcome**

- Ability to audit and design secure systems
    
- Strong foundation for security-sensitive startups
    

---

## Final Outcome

You finish this syllabus as:

- A systems architect
    
- An AI infrastructure builder
    
- A real-time performance engineer
    
- A founder-grade technologist
    

You understand:

- Hardware
    
- Time
    
- Memory
    
- Concurrency
    
- Failure
    
- Energy
    
- Intelligence under constraint