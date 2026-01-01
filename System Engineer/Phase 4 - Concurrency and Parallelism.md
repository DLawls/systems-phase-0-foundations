**Purpose:** Build systems that scale without falling apart  
**Outcome:** You can design concurrent systems that are correct _and_ fast

---

## Phase 4 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand **why locks kill scalability**
    
- Know when locks are acceptable — and when they are not
    
- Build **lock-free data structures**
    
- Understand **contention, backpressure, and queues**
    
- Design **work-stealing schedulers**
    
- Reason about **throughput vs latency vs fairness**
    
- See why most concurrency bugs are _design bugs_, not syntax bugs
    

This phase is essential for:

- AI inference runtimes
    
- XR real-time pipelines
    
- High-throughput servers
    
- GPU scheduling
    
- Startup-grade systems
    

---

## Core Mental Model (Must Internalize)

> **Concurrency is about contention, not threads.**

Adding threads without reducing contention makes things worse.

---

## Core Topics to Master

### 1) Contention & Scalability

- Amdahl’s Law (practical)
    
- Contended vs uncontended paths
    
- Serialization points
    
- Critical sections
    
- False sharing (from Phase 1, now weaponized)
    

**Key question:**  
Why does performance flatten — or degrade — after N cores?

---

### 2) Locks: Costs & Failure Modes

- Mutexes
    
- Spinlocks
    
- Fair vs unfair locks
    
- Convoying
    
- Priority inversion (conceptual)
    

**Key question:**  
Why is a “correct” mutex still too slow?

---

### 3) Lock-Free Programming

- Atomic primitives
    
- Compare-and-swap (CAS)
    
- ABA problem
    
- Memory reclamation (hazard pointers, epochs — conceptually)
    
- Progress guarantees (wait-free vs lock-free)
    

**Key question:**  
Why is correctness harder — but scalability better?

---

### 4) Queues & Backpressure

- Producer–consumer patterns
    
- Bounded vs unbounded queues
    
- Backpressure propagation
    
- Load shedding
    

**Key question:**  
Why does removing queue bounds cause system collapse?

---

### 5) Work Stealing & Task Parallelism

- Thread pools
    
- Task queues
    
- Locality vs fairness
    
- Work stealing deques
    

**Key question:**  
Why do modern runtimes prefer tasks over threads?

---

## Mathematical Lens (Applied)

You will reason with:

- Little’s Law (L = λW)
    
- Throughput vs latency tradeoffs
    
- Queue depth vs tail latency
    
- Contention curves
    

No proofs — only measurements and predictions.

---

## Energy & Hardware Reality (Integrated)

You will explicitly observe:

- Contention increases cache coherence traffic
    
- Locks burn power while waiting
    
- Busy-waiting vs blocking tradeoffs
    
- Why oversubscription destroys perf-per-watt
    

---

## Primary References (Anchors)

- **The Art of Multiprocessor Programming** — correctness & lock-free reasoning
    
- Linux kernel / runtime articles (selectively, as references)
    

Use these to **check your reasoning**, not memorize APIs.

---

# Execution Work (What You Build)

## Project 4.1 — Lock Contention Benchmark

**Goal:** Feel contention viscerally

**Implement**

- Shared counter with:
    
    - mutex
        
    - spinlock
        
    - atomic increment
        

**Measure**

- Throughput vs number of threads
    
- Latency variance
    

**Mastery check**

- You can explain where scalability collapses and why
    

---

## Project 4.2 — False Sharing Revisited

**Goal:** Combine Phase 1 + concurrency

**Implement**

- Shared data with and without padding
    
- Multiple writers on adjacent cache lines
    

**Measure**

- Throughput differences
    
- Coherence traffic indicators
    

**Mastery check**

- You can spot false sharing instantly in designs
    

---

## Project 4.3 — Lock-Free Queue (MPMC)

**Goal:** Build a core concurrency primitive

**Implement**

- Bounded MPMC queue using atomics
    
- Correct memory ordering
    
- No locks
    

**Validate**

- Correctness under contention
    
- Performance vs mutex-based queue
    

**Mastery check**

- You can state the correctness invariants clearly
    

---

## Project 4.4 — Backpressure Lab

**Goal:** Understand system stability

**Implement**

- Producer–consumer pipeline
    
- Unbounded queue version
    
- Bounded queue version with backpressure
    

**Observe**

- Memory growth
    
- Latency explosion
    
- Throughput collapse
    

**Mastery check**

- You understand why backpressure is mandatory in real systems
    

---

## Project 4.5 — Work-Stealing Thread Pool

**Goal:** Build a modern parallel execution model

**Implement**

- Thread pool
    
- Per-thread task deques
    
- Work stealing logic
    

**Compare**

- Centralized queue vs work stealing
    
- Locality vs fairness
    

**Mastery check**

- You understand why work stealing scales better
    

---

## 🔥 Flagship Project — Concurrency Stress Harness

**Goal:** Tie correctness and performance together

### What you build

A reusable concurrency test harness that:

- Runs all your queues, locks, and pools
    
- Varies:
    
    - thread count
        
    - workload mix
        
    - contention
        
- Reports:
    
    - throughput
        
    - latency distribution
        
    - tail latency
        

### Required explanation

Your README must explain:

- Where contention dominated
    
- Why some structures scaled
    
- How backpressure stabilized the system
    
- Implications for:
    
    - AI inference pipelines
        
    - XR frame scheduling
        
    - High-throughput services
        

---

## Repo Plan (Phase 4)

**Repo name**

`systems-phase-4-concurrency-parallelism`

**Structure**

`systems-phase-4-concurrency-parallelism/ ├── README.md ├── notes/ │   ├── contention.md │   ├── locks_vs_lockfree.md │   ├── aba_problem.md │   ├── backpressure.md │   └── work_stealing.md ├── src/ │   ├── locks/ │   ├── lockfree/ │   ├── queues/ │   ├── backpressure/ │   └── thread_pool/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 4 README must answer:

- Where did contention appear first?
    
- Which locks failed to scale and why?
    
- Why did lock-free structures help?
    
- How did backpressure change system behavior?
    
- How would these lessons apply to:
    
    - AI inference scheduling?
        
    - XR render + compute overlap?
        
    - GPU task queues?
        

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You can predict contention bottlenecks in designs
    
- You understand when locks are acceptable
    
- You can build a correct lock-free queue
    
- You understand backpressure deeply
    
- You think in queues and pipelines, not threads
    

If anything feels fuzzy → rerun stress tests.

---

## Why Phase 4 Matters for What Comes Next

- **Compilers & runtimes:** task scheduling depends on this
    
- **AI systems:** inference pipelines are concurrent systems
    
- **XR:** frame pipelines need bounded latency
    
- **Distributed systems:** queues and backpressure reappear at scale
    
- **Security:** races are vulnerabilities