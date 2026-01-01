

**Purpose:** Understand the _physical limits_ of computation  
**Outcome:** You can predict performance before running code

---

## Phase 1 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Think in **cache lines, bandwidth, and stalls**
    
- Understand **why memory dominates AI and XR**
    
- Know when CPUs win and when GPUs win
    
- Predict performance regressions _before profiling_
    
- Stop trusting Big-O in isolation
    

This phase is the **physics layer** of your entire roadmap.

---

## Core Mental Model (Must Internalize)

> **Modern systems are memory systems with compute attached.**

If you don’t believe that yet, this phase will convince you.

---

## Core Topics to Master

### 1. Instruction Execution & Throughput

- Pipelines
    
- Superscalar execution
    
- Instruction-level parallelism (ILP)
    
- Out-of-order execution
    
- Throughput vs latency
    

**Key question you must answer:**  
Why can _more instructions_ sometimes run faster?

---

### 2. Branch Prediction & Speculation

- Branch predictors
    
- Speculative execution
    
- Misprediction penalties
    
- Branchless programming patterns
    

**Key question:**  
Why does “clean” control flow often perform worse?

---

### 3. Cache Hierarchy & Locality

- Cache lines
    
- L1 / L2 / L3
    
- Spatial vs temporal locality
    
- TLBs
    
- Working sets
    

**Key question:**  
Why does changing loop order change performance by 10×?

---

### 4. Multicore Reality & NUMA

- Cache coherence (high-level)
    
- False sharing
    
- Core-to-core traffic
    
- NUMA memory placement
    
- Thread pinning
    

**Key question:**  
Why does adding threads sometimes make code slower?

---

### 5. SIMD & Vectorization

- SIMD width
    
- Alignment
    
- Auto-vectorization
    
- Reduction patterns
    
- Vectorization failures
    

**Key question:**  
Why did the compiler refuse to vectorize this loop?

---

### 6. GPU Mental Model (Conceptual, Not Deep CUDA Yet)

- GPUs as throughput machines
    
- SMs vs CPU cores
    
- Warps / wavefronts
    
- Latency hiding
    
- Memory hierarchy (global / shared / registers)
    

**Key question:**  
Why are GPUs bad at latency but amazing at bandwidth?

---

## Mathematical Lens (Applied)

You must be comfortable with:

- Throughput = work / time
    
- Latency vs bandwidth curves
    
- Roofline model intuition
    
- Back-of-the-envelope performance estimates
    

No proofs. Only _predictive reasoning_.

---

## Energy & Hardware Reality (Integrated)

You will explicitly observe:

- Power draw vs performance
    
- Cache vs DRAM energy cost
    
- Why sustained performance drops (thermal limits)
    
- Why “peak FLOPs” are marketing numbers
    

---

## Primary References (Use as Anchors)

- **Computer Architecture: A Quantitative Approach**  
    (Primary reference for truth)
    
- **Computer Systems: A Programmer’s Perspective**  
    (Execution & memory reinforcement)
    

Use these as **reference manuals**, not linear textbooks.

---

## Execution Work (What You Build)

### Project 1.1 — Instruction Throughput Lab

**Goal:** Observe ILP and OoO execution

**Implement**

- Dependent vs independent instruction loops
    
- Arithmetic-heavy kernels
    
- Instruction mixes
    

**Measure**

- IPC (instructions per cycle)
    
- Execution time
    

**Required insight**

- Explain why OoO helps in one case and not another
    

---

### Project 1.2 — Branch Prediction Lab

**Goal:** Measure speculation costs

**Implement**

- Predictable branches
    
- Unpredictable branches
    
- Branchless equivalents
    

**Measure**

- Branch misses
    
- Execution time
    

**Required insight**

- Quantify misprediction penalty
    

---

### Project 1.3 — Cache & Memory Wall Lab

**Goal:** Make cache behavior visible

**Implement**

- Stride-based memory access
    
- Working-set sweeps
    
- Pointer chasing vs array traversal
    

**Measure**

- Cache misses
    
- Latency curves
    

**Required insight**

- Identify L1/L2/L3 boundaries on _your_ machine
    

---

### Project 1.4 — False Sharing & NUMA Lab

**Goal:** Feel multicore pain

**Implement**

- Shared counters (broken)
    
- Padded counters (fixed)
    
- NUMA-aware allocation
    
- Thread pinning
    

**Measure**

- Throughput before/after padding
    
- NUMA penalties
    

**Required insight**

- Explain coherence traffic cost
    

---

### Project 1.5 — SIMD & Vectorization Lab

**Goal:** Understand data-parallel execution

**Implement**

- Scalar vs SIMD loops
    
- Aligned vs misaligned memory
    
- Reduction patterns
    

**Inspect**

- Compiler vectorization reports
    
- Generated assembly
    

**Required insight**

- Explain why vectorization failed or succeeded
    

---

### Project 1.6 — CPU vs GPU Memory Bandwidth

**Goal:** Establish GPU intuition early

**Implement**

- CPU memory bandwidth benchmark
    
- GPU memory bandwidth benchmark
    

**Measure**

- Sustained bandwidth
    
- Power draw (via `nvidia-smi`)
    

**Required insight**

- Explain why GPUs dominate bandwidth-bound workloads
    

---

## 🔥 Flagship Project — The Memory Wall Profiler

**This project ties everything together.**

### What You Build

A **CPU + GPU memory performance profiler** that:

- Measures:
    
    - Latency
        
    - Bandwidth
        
    - Cache effects
        
    - NUMA effects
        
    - CPU vs GPU behavior
        
- Produces plots or tables
    
- Annotates explanations
    

### Required Explanation

Your README must clearly explain:

- Why AI attention is memory-bound
    
- Why XR rendering is memory-bound
    
- Why more compute does not fix memory stalls
    

This project becomes **foundational IP** for later phases.

---

## GitHub Repository Structure (Phase 1)

**Repo name**

`systems-phase-1-architecture-memory`

**Structure**

`systems-phase-1-architecture-memory/ ├── README.md ├── notes/ │   ├── pipelines_and_ilp.md │   ├── branch_prediction.md │   ├── cache_hierarchy.md │   ├── numa_and_false_sharing.md │   ├── simd_vectorization.md │   └── cpu_vs_gpu.md ├── src/ │   ├── ilp/ │   ├── branches/ │   ├── cache/ │   ├── numa/ │   ├── simd/ │   └── gpu/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your `README.md` must answer:

- What surprised you most?
    
- Which assumptions failed?
    
- Where did memory dominate?
    
- Where did compute dominate?
    
- How did power/thermal behavior show up?
    
- How would this affect AI inference or XR frame timing?
    

If you can’t answer these clearly, you’re not done.

---

## Mastery Checklist (All Must Be True)

You may proceed **only if**:

- You can identify cache bottlenecks by inspection
    
- You understand false sharing instinctively
    
- You can explain SIMD alignment issues
    
- You understand CPU vs GPU tradeoffs
    
- You think in bandwidth and latency
    
- You no longer trust peak FLOPs claims
    

If any item is fuzzy → rerun experiments.

---

## Why Phase 1 Matters for Everything Later

- **AI Systems:** attention = memory traffic
    
- **XR:** frame pacing = cache + branch behavior
    
- **Security:** side-channels start here
    
- **Concurrency:** coherence costs dominate
    
- **Energy:** memory is expensive
    

This phase makes all future optimization _honest_.