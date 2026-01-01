**Purpose:** Understand how high-level code becomes machine behavior  
**Outcome:** You can predict abstraction cost, guide the compiler, and design runtimes

---

## Phase 5 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand the **full compilation pipeline**
    
- Read and reason about **IR and generated assembly**
    
- Know **why optimizations succeed or fail**
    
- Understand **vectorization limits**
    
- Understand **runtime systems** (stack, heap, GC basics)
    
- Design code that the compiler _can_ optimize
    
- Predict **performance and energy impact** of abstractions
    

This phase is critical for:

- AI inference engines
    
- XR real-time loops
    
- GPU + CPU mixed workloads
    
- Language/runtime design
    
- High-performance startup codebases
    

---

## Core Mental Model (Must Internalize)

> **The compiler is a proof engine, not a mind reader.**

If it can’t _prove_ something is safe, it won’t optimize it.

---

## Core Topics to Master

### 1) Compilation Pipeline (End-to-End)

- Frontend (parsing, AST)
    
- Intermediate Representation (IR)
    
- Optimization passes
    
- Code generation
    
- Linking
    
- Static vs dynamic linking
    

**Key question:**  
Where exactly does your source code stop existing?

---

### 2) Optimization Passes & Cost Models

- Dead code elimination
    
- Common subexpression elimination
    
- Inlining
    
- Loop unrolling
    
- Strength reduction
    
- Instruction selection
    

**Key question:**  
Why did the compiler _refuse_ to optimize this?

---

### 3) Vectorization (Deeper Than Phase 1)

- Loop vectorization
    
- Reduction patterns
    
- Alias analysis
    
- Alignment requirements
    
- Scalar vs vector cost tradeoffs
    

**Key question:**  
Why does adding one pointer break vectorization?

---

### 4) Register Allocation & Spills

- Register pressure
    
- Spilling to stack
    
- Impact on cache & power
    

**Key question:**  
Why did “simpler” code get slower?

---

### 5) Runtimes & Memory Management

- Stack vs heap (runtime perspective)
    
- Calling conventions revisited
    
- Memory allocation strategies
    
- Garbage collection basics:
    
    - Stop-the-world
        
    - Generational GC (conceptual)
        
- Why real-time systems avoid GC
    

**Key question:**  
Why do runtimes exist at all?

---

## Mathematical Lens (Applied)

You will reason about:

- Cost models (instruction counts, memory ops)
    
- Tradeoffs between code size and speed
    
- Throughput vs latency in runtime behavior
    
- Amortized allocation costs
    

---

## Energy & Hardware Reality (Integrated)

You will explicitly observe:

- Inlining increases instruction cache pressure
    
- Register spills increase memory traffic
    
- GC pauses violate real-time guarantees
    
- Optimization choices affect power draw
    

---

## Primary References (Anchors)

- **Engineering a Compiler** — optimization & IR truth
    
- **Crafting Interpreters** — runtime intuition
    
- LLVM documentation (as reference manual)
    

---

# Execution Work (What You Build)

## Project 5.1 — Tiny Compiler (Source → Assembly)

**Goal:** Demystify compilation

**Implement**

- Expression language:
    
    - arithmetic
        
    - variables
        
    - control flow (if/while)
        
- Generate simple IR
    
- Emit assembly
    

**Deliverables**

- Clear mapping: source → IR → asm
    
- Notes on lost abstractions
    

**Mastery check**

- You can point to where each source construct disappears
    

---

## Project 5.2 — Optimization Pass Playground

**Goal:** See optimization rules in action

**Implement**

- Small kernels designed to:
    
    - inline well
        
    - inline poorly
        
    - vectorize
        
    - fail vectorization
        
- Compare `-O0`, `-O2`, `-O3`
    

**Inspect**

- IR
    
- Assembly
    
- Vectorization reports
    

**Mastery check**

- You can explain _why_ each optimization happened or didn’t
    

---

## Project 5.3 — Vectorization Failure Lab

**Goal:** Learn how to help the compiler

**Implement**

- Loops with:
    
    - aliasing pointers
        
    - unknown bounds
        
    - misaligned memory
        
- Fix each issue deliberately
    

**Deliverables**

- Before/after code
    
- Performance measurements
    
- Explanation of required proofs
    

**Mastery check**

- You know how to _write vectorizable code_
    

---

## Project 5.4 — Register Pressure & Spills

**Goal:** Understand low-level performance cliffs

**Implement**

- Functions with increasing live variables
    
- Measure spill behavior
    
- Inspect stack usage
    

**Deliverables**

- Correlation between spills and performance
    
- Notes on register allocation tradeoffs
    

**Mastery check**

- You can spot register pressure by reading code
    

---

## Project 5.5 — Runtime & Allocation Lab

**Goal:** Understand runtime costs

**Implement**

- Custom allocators:
    
    - naive
        
    - pool-based
        
- Compare allocation patterns
    
- (Optional) simple GC simulation
    

**Observe**

- Allocation cost
    
- Cache effects
    
- Latency spikes
    

**Mastery check**

- You know why real-time systems avoid GC
    

---

## 🔥 Flagship Project — Abstraction Cost Atlas

**Goal:** Create a personal reference for performance decisions

### What you build

A documented set of experiments showing:

- Abstraction → IR → machine code
    
- Performance cost of:
    
    - function calls
        
    - virtual dispatch
        
    - allocations
        
    - bounds checks
        
    - runtime helpers
        

### Required explanation

Your README must explain:

- When abstractions are “free”
    
- When they are catastrophically expensive
    
- How this applies to:
    
    - AI inference loops
        
    - XR frame pipelines
        
    - Hot paths in startups
        

---

## Repo Plan (Phase 5)

**Repo name**

`systems-phase-5-compilers-runtimes`

**Structure**

`systems-phase-5-compilers-runtimes/ ├── README.md ├── notes/ │   ├── compilation_pipeline.md │   ├── optimization_passes.md │   ├── vectorization.md │   ├── register_allocation.md │   └── runtime_systems.md ├── src/ │   ├── compiler/ │   ├── optimizations/ │   ├── vectorization/ │   ├── registers/ │   └── runtime/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 5 README must answer:

- Where do abstractions disappear?
    
- Why did the compiler reject certain optimizations?
    
- What caused register spills?
    
- Which runtime behaviors violate real-time constraints?
    
- How would you design code differently for:
    
    - AI inference kernels?
        
    - XR render loops?
        
    - Low-latency systems?
        

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You can read IR and assembly with confidence
    
- You understand why optimizations succeed or fail
    
- You can write vectorizable code deliberately
    
- You can spot abstraction costs
    
- You understand runtime tradeoffs
    
- GC pauses no longer feel mysterious
    

If anything feels fuzzy → repeat the experiments.

---

## Why Phase 5 Matters for What Comes Next

- **Distributed systems:** serialization & runtime costs
    
- **Databases:** query compilation & execution
    
- **AI systems:** kernel fusion, codegen, JITs
    
- **XR:** frame-critical hot paths
    
- **Energy:** instruction count = power