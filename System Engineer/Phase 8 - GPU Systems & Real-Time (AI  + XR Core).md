## Phase 8 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand **GPU architecture** deeply enough to predict performance
    
- Write **GPU kernels** that are bandwidth-aware
    
- Schedule **graphics + ML compute together**
    
- Reason about **frame budgets** (not averages)
    
- Control **latency, jitter, and tail latency**
    
- Understand **why XR and real-time systems are unforgiving**
    
- Bridge **AI inference and rendering pipelines**
    

This phase is essential for:

- XR engines
    
- On-device AI
    
- Simulation systems
    
- Robotics
    
- Real-time inference platforms
    

---

## Core Mental Model (Must Internalize)

> **Real-time systems don’t care how fast you are on average —  
> they care how slow you are at your worst.**

Dropped frames and missed deadlines are _failures_.

---

## Core Topics to Master

### 1) GPU Architecture (Systems View)

- Streaming Multiprocessors (SMs)
    
- Warps / wavefronts
    
- Occupancy
    
- Registers vs shared vs global memory
    
- Latency hiding vs low latency
    

**Key question:**  
Why do GPUs hide latency instead of eliminating it?

---

### 2) GPU Memory Hierarchy

- Global memory
    
- Shared memory
    
- Registers
    
- Coalesced vs scattered access
    
- Memory bandwidth ceilings
    

**Key question:**  
Why does memory layout matter more than math?

---

### 3) GPU Kernel Design

- Thread/block decomposition
    
- Occupancy vs register pressure
    
- Memory-bound vs compute-bound kernels
    
- Synchronization costs
    

**Key question:**  
Why does “more threads” sometimes make kernels slower?

---

### 4) Real-Time Constraints

- Frame budgets (e.g. 11.1ms @ 90Hz)
    
- Motion-to-photon latency
    
- Jitter vs latency
    
- Deadline misses
    
- Deterministic execution
    

**Key question:**  
Why does one long frame ruin XR comfort?

---

### 5) Scheduling Graphics + ML Together

- Async compute
    
- Command queues
    
- GPU preemption limits
    
- Compute vs graphics contention
    
- Avoiding starvation
    

**Key question:**  
Why can ML inference break rendering — even if it’s fast?

---

### 6) Power & Thermal Reality

- Sustained vs burst performance
    
- Thermal throttling
    
- Perf-per-watt
    
- Mobile vs desktop constraints
    

**Key question:**  
Why does performance decay over time?

---

## Mathematical Lens (Applied)

You will reason with:

- Frame time budgets
    
- Throughput vs latency regimes
    
- Tail latency
    
- Bandwidth ceilings
    
- Scheduling windows
    

---

## Primary References (Anchors)

- _Programming Massively Parallel Processors_ — GPU fundamentals
    
- NVIDIA CUDA Programming Guide
    
- GPU vendor performance guides (as reference manuals)
    

---

# Execution Work (What You Build)

## Project 8.1 — GPU Architecture & Bandwidth Lab

**Goal:** Build correct GPU intuition

**Implement**

- Memory-bound kernel
    
- Compute-bound kernel
    
- Vary block sizes and occupancy
    

**Measure**

- Execution time
    
- Achieved bandwidth
    
- Occupancy
    

**Mastery check**

- You can identify the bottleneck without profiling
    

---

## Project 8.2 — Kernel Optimization Lab

**Goal:** Learn where performance comes from

**Implement**

- Naive kernel
    
- Optimized kernel using:
    
    - shared memory
        
    - coalesced access
        
- Compare results
    

**Measure**

- Speedup
    
- Power usage (`nvidia-smi`)
    

**Mastery check**

- You understand when shared memory helps — and when it hurts
    

---

## Project 8.3 — Frame Budget Simulator

**Goal:** Make real-time constraints concrete

**Implement**

- Fixed-rate “frame loop”
    
- Inject variable GPU workloads
    
- Detect deadline misses
    

**Measure**

- Frame time
    
- Jitter
    
- Tail latency
    

**Mastery check**

- You understand why average performance is meaningless
    

---

## Project 8.4 — Async Compute Scheduling Lab

**Goal:** Run compute and graphics together

**Implement**

- Simple graphics workload
    
- Concurrent compute workload
    
- Schedule using async queues
    

**Observe**

- Starvation
    
- Frame drops
    
- Latency spikes
    

**Mastery check**

- You understand why naive scheduling fails
    

---

## Project 8.5 — Power & Thermal Profiling

**Goal:** Understand sustained performance

**Implement**

- Long-running GPU workload
    
- Monitor:
    
    - clocks
        
    - temperature
        
    - power
        
- Observe throttling behavior
    

**Mastery check**

- You can explain performance decay over time
    

---

## 🔥 Flagship Project — Real-Time GPU Workload Manager

**Goal:** Integrate GPU + real-time thinking

### What you build

A small system that:

- Runs:
    
    - a graphics loop
        
    - an ML-like compute workload
        
- Enforces:
    
    - frame deadlines
        
    - compute budgets
        
- Dynamically:
    
    - reduces workload
        
    - defers compute
        
    - avoids missed frames
        

### Required explanation

Your README must explain:

- Scheduling decisions
    
- Why some work was deferred
    
- How tail latency was controlled
    
- Implications for:
    
    - XR engines
        
    - On-device AI
        
    - Simulation systems
        

This project becomes **foundational for Phase 9**.

---

## Repo Plan (Phase 8)

**Repo name**

`systems-phase-8-gpu-realtime`

**Structure**

`systems-phase-8-gpu-realtime/ ├── README.md ├── notes/ │   ├── gpu_architecture.md │   ├── memory_hierarchy.md │   ├── real_time_constraints.md │   ├── async_compute.md │   └── power_thermal.md ├── src/ │   ├── bandwidth/ │   ├── kernels/ │   ├── frame_loop/ │   ├── async_compute/ │   └── power/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 8 README must answer:

- Which workloads caused missed frames?
    
- What dominated latency?
    
- How did tail latency differ from average?
    
- How did power and thermal behavior affect performance?
    
- How would this design change for:
    
    - XR headsets?
        
    - Edge AI devices?
        
    - Desktop vs mobile GPUs?
        

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You think in frame budgets
    
- You understand GPU scheduling limits
    
- You can run compute without breaking rendering
    
- You can predict power throttling effects
    
- You treat tail latency as first-class
    

If anything feels fuzzy → rerun with stricter budgets.

---

## Why Phase 8 Matters for Everything Else

- **AI Systems:** inference must respect latency
    
- **XR:** dropped frames = sickness
    
- **Simulation:** determinism matters
    
- **Energy:** power limits dominate design
    
- **Startups:** real-time reliability creates defensibility