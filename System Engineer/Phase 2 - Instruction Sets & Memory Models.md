
**Purpose:** Understand what the CPU is _allowed_ to do (and why your code breaks)  
**Outcome:** You can reason about concurrency correctly and read machine-level behavior

---

## Phase 2 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Read and reason about **assembly-level effects** of C/C++ code
    
- Understand **calling conventions** and stack frames at a practical level
    
- Understand **memory ordering** and why “it works on my machine” is meaningless
    
- Use **atomics correctly** (acquire/release/seq-cst)
    
- Know what **data races** actually mean (not vibes)
    
- Build synchronization that works under optimization and reordering
    

This phase is the **bridge** between “software” and “computer”.

---

## Core Topics to Master

### 1) Minimal ISA & ABI Literacy (Practical)

- Registers vs stack
    
- Function prologue/epilogue
    
- Calling convention basics
    
- Parameter passing
    
- Return values
    
- Stack alignment
    

**You don’t need to become an assembly programmer — you need to stop being blind.**

---

### 2) The Optimizer Is an Adversary

- Reordering within a thread
    
- Dead-store elimination
    
- Common subexpression elimination
    
- “As-if rule” mindset
    
- UB interacts with optimization
    

---

### 3) Memory Models & Reordering

- Compiler reordering vs CPU reordering
    
- Happens-before
    
- Visibility vs ordering
    
- Why `volatile` is not synchronization
    
- Acquire/release intuition
    
- Sequential consistency (and why it’s expensive)
    

---

### 4) Cache Coherence (High-Level but Real)

- What coherence guarantees
    
- What it does _not_ guarantee
    
- Store buffers and invalidations (conceptual)
    
- Coherence traffic costs (preview for Phase 4)
    

---

## Mathematical Lens (Light but Essential)

- Partial orders (happens-before)
    
- Invariants for correctness
    
- Simple reasoning about causality
    

You’ll write _correctness claims_ as invariants, not prose.

---

## Energy & Hardware Reality (Integrated)

You will observe:

- Atomics and fences can be expensive
    
- Contention increases coherence traffic (power + latency)
    
- “Correct” synchronization can still be too slow for real-time XR
    

---

## References (Anchor Texts)

- **Computer Systems: A Programmer’s Perspective** (machine-level + linking concepts)
    
- **The Art of Multiprocessor Programming** (memory ordering and atomic reasoning; we’ll go deep later)
    
- C++ atomics reference (as needed; use as a manual, not reading)
    

---

# Execution Work (What You Build)

## Project 2.1 — Assembly & ABI Microscope

**Goal:** See how your code becomes machine behavior

**Implement**

- Simple functions with:
    
    - locals
        
    - loops
        
    - structs
        
    - function calls
        
- Compile with `-O0` and `-O2`
    
- Disassemble and compare
    

**Deliverables**

- Notes: stack frames, calling convention observations
    
- A small “pattern cheat sheet” you build yourself
    

**Mastery check**

- You can look at a function and describe where variables live (stack/register)
    

---

## Project 2.2 — Reordering Reality Lab (Single-thread)

**Goal:** Prove to yourself that the compiler is not your friend

**Implement**

- Programs where compiler reordering changes outcomes (without UB if possible; otherwise controlled UB + sanitizers)
    
- Demonstrate dead-store elimination
    
- Demonstrate load hoisting
    

**Deliverables**

- Minimal repro cases with explanation
    
- Output differences across `-O0` vs `-O2`
    

**Mastery check**

- You can explain why the output changed in optimizer terms
    

---

## Project 2.3 — The “Volatile Trap” Demo

**Goal:** Destroy the most common low-level misconception

**Implement**

- A “flag” used for thread synchronization with `volatile`
    
- Run under contention
    
- Show broken behavior
    
- Replace with correct atomics
    

**Deliverables**

- Broken example + corrected example
    
- Explanation: “volatile provides visibility but not ordering/synchronization”
    

**Mastery check**

- You can explain why volatile is insufficient without handwaving
    

---

## Project 2.4 — Litmus Tests (Memory Model Lab)

**Goal:** Internalize acquire/release/seq-cst

**Implement**  
Classic litmus tests:

- Store buffering
    
- Message passing
    
- Load buffering
    

Implement each with:

- plain loads/stores (intentionally racy)
    
- atomics relaxed
    
- acquire/release
    
- seq-cst
    

**Deliverables**

- A small harness that runs tests many times and reports observed outcomes
    
- Notes that map outcomes → ordering rules
    

**Mastery check**

- You can predict which outcomes are possible under each ordering
    

---

## Project 2.5 — Build a Correct Spinlock (and prove it)

**Goal:** Write and validate a fundamental synchronization primitive

**Implement**

- naive spinlock (broken)
    
- correct spinlock using:
    
    - `atomic_flag`
        
    - acquire/release semantics
        

**Bench**

- under low contention
    
- under high contention
    

**Deliverables**

- lock correctness notes (invariants)
    
- performance notes and observed costs
    

**Mastery check**

- You can state the lock’s correctness argument + why ordering matters
    

---

## Flagship Project — “Happens-Before Visualizer”

**Goal:** Turn invisible ordering into something you can reason about

**What you build**  
A small tool/program that:

- runs litmus tests
    
- logs event traces (thread A write, thread B read, etc.)
    
- outputs a simple textual “graph” of happens-before relationships
    
- highlights outcomes that violate naive assumptions
    

**Deliverable**

- README with:
    
    - your mental model of ordering
        
    - rules of thumb for picking atomic orderings
        
    - implications for real-time systems and AI runtimes
        

This becomes a reference you’ll reuse in Phase 4+.

---

# Repo Plan (Phase 2)

**Repo name**

`systems-phase-2-isa-memory-models`

**Structure**

`systems-phase-2-isa-memory-models/ ├── README.md ├── notes/ │   ├── abi_and_calling_conventions.md │   ├── optimizer_reordering.md │   ├── memory_ordering.md │   ├── volatile_is_not_sync.md │   └── litmus_results.md ├── src/ │   ├── abi/ │   ├── optimizer/ │   ├── volatile_trap/ │   ├── litmus/ │   ├── atomics/ │   └── locks/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

# Required Documentation (Mandatory)

Your Phase 2 README must answer:

- What reorderings did you observe and why?
    
- What’s the difference between compiler vs CPU reordering?
    
- What does acquire/release guarantee?
    
- What does seq-cst guarantee and what does it cost?
    
- When is relaxed acceptable?
    
- Why does this matter for:
    
    - real-time frame loops
        
    - GPU scheduling
        
    - AI inference runtimes
        

---

# Mastery Checklist (All Must Be True)

You may proceed only when:

- You can read disassembly for simple C functions
    
- You can explain at least 3 optimizer transformations you saw
    
- You understand why racy code “works” until it doesn’t
    
- You can correctly choose between relaxed vs acq/rel vs seq-cst
    
- You can implement a correct spinlock and justify it
    
- Litmus tests no longer feel like magic