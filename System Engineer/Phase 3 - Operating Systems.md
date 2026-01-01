**Purpose:** Understand how the OS virtualizes CPU, memory, and IO  
**Outcome:** You know exactly what the OS is lying to you about — and what it costs

---

## Phase 3 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand **processes vs threads** mechanically
    
- Know exactly what happens during a **system call**
    
- Understand **virtual memory** intuitively (not just definitions)
    
- Know why **page faults stall everything**
    
- Understand **scheduling tradeoffs**
    
- Measure **context switch and syscall overhead**
    
- Know when the OS becomes the bottleneck for AI/XR systems
    

This phase makes later work in **concurrency, GPU scheduling, and real-time systems honest**.

---

## Core Mental Model (Must Internalize)

> **The OS is a resource multiplexing engine that trades latency for fairness and safety.**

Everything you feel as “slowness” is a _policy decision_.

---

## Core Topics to Master

### 1) Processes, Threads, and Address Spaces

- Process isolation
    
- Virtual address spaces
    
- Threads vs processes
    
- Context switching
    
- Kernel vs user mode
    

**Key question:**  
Why does spawning a process feel “heavy” compared to a thread?

---

### 2) System Calls & Kernel Boundary

- Syscall mechanism
    
- Mode switches
    
- Kernel entry/exit
    
- Syscall cost
    
- Fast paths vs slow paths
    

**Key question:**  
Why are syscalls orders of magnitude slower than function calls?

---

### 3) Virtual Memory & Paging

- Virtual vs physical memory
    
- Page tables
    
- Page faults (minor vs major)
    
- TLBs
    
- Copy-on-write
    
- `mmap`
    

**Key question:**  
Why can a single page fault stall _every thread_?

---

### 4) Scheduling & Time

- Preemption
    
- Time slicing
    
- Scheduling policies
    
- CPU affinity
    
- Priority inversion (conceptual)
    

**Key question:**  
Why does “just run it on another core” fail?

---

### 5) IO Stack & Filesystems (Conceptual + Measured)

- Buffered vs direct IO
    
- Page cache
    
- Read/write vs mmap
    
- Sync vs async IO
    
- Filesystem abstraction cost
    

**Key question:**  
Why does IO often look like memory — until it doesn’t?

---

## Mathematical Lens (Applied)

You will reason with:

- Queueing intuition (run queues)
    
- Latency vs throughput
    
- Amortized costs (paging, IO)
    
- Back-of-the-envelope syscall budgets
    

---

## Energy & Hardware Reality (Integrated)

You will explicitly observe:

- Page faults spike power and latency
    
- Context switches increase cache misses
    
- Oversubscription hurts perf-per-watt
    
- Why real-time systems avoid kernel transitions
    

---

## Primary References (Use as Truth Sources)

- **Operating Systems: Three Easy Pieces**  
    (Primary conceptual anchor)
    
- Linux man pages (`man 2`, `man 7`)  
    (Primary factual reference)
    

---

# Execution Work (What You Build)

## Project 3.1 — Process vs Thread Reality Lab

**Goal:** Observe isolation and overhead

**Implement**

- Spawn many processes
    
- Spawn many threads
    
- Compare startup cost
    
- Compare memory behavior
    

**Measure**

- Time to create
    
- Memory usage
    
- Context switch counts
    

**Mastery check**

- You can explain when processes are worth the cost
    

---

## Project 3.2 — Syscall Cost Microscope

**Goal:** Quantify kernel boundary overhead

**Implement**

- Tight loops with:
    
    - pure computation
        
    - frequent syscalls
        
- Compare syscall-heavy vs syscall-free paths
    

**Tools**

- `strace`
    
- `perf`
    

**Mastery check**

- You can estimate syscall budgets for real-time loops
    

---

## Project 3.3 — Virtual Memory & Page Fault Lab

**Goal:** Make paging visible

**Implement**

- Allocate large memory regions
    
- Touch pages lazily
    
- Trigger page faults intentionally
    
- Compare `malloc` vs `mmap`
    

**Measure**

- Page fault counts
    
- Latency spikes
    
- Cache effects
    

**Mastery check**

- You understand why first access is slow
    

---

## Project 3.4 — mmap vs read() IO Experiment

**Goal:** Understand the IO illusion

**Implement**

- File reads via `read`
    
- File access via `mmap`
    
- Sequential vs random access
    

**Measure**

- Latency
    
- Throughput
    
- Page cache behavior
    

**Mastery check**

- You know when mmap helps — and when it hurts
    

---

## Project 3.5 — Scheduling & Affinity Lab

**Goal:** Observe scheduling tradeoffs

**Implement**

- CPU-bound tasks
    
- IO-bound tasks
    
- Mixed workloads
    
- Thread pinning vs free scheduling
    

**Measure**

- Throughput
    
- Latency variance
    
- Cache miss behavior
    

**Mastery check**

- You understand why pinning sometimes helps and sometimes destroys fairness
    

---

## Flagship Project — User-Space OS Illusion Explorer

**Goal:** Tie everything together

**What you build**  
A small user-space program suite that:

- Measures:
    
    - process creation
        
    - thread creation
        
    - syscall overhead
        
    - page fault latency
        
    - context switch cost
        
- Outputs:
    
    - timing summaries
        
    - commentary on tradeoffs
        

**Required explanation**  
Your README must clearly explain:

- Where the OS adds latency
    
- Which costs are amortized
    
- Why AI inference and XR loops try to minimize syscalls
    
- Why “kernel bypass” exists in high-performance systems
    

---

## Repo Plan (Phase 3)

**Repo name**

`systems-phase-3-operating-systems`

**Structure**

`systems-phase-3-operating-systems/ ├── README.md ├── notes/ │   ├── processes_vs_threads.md │   ├── syscalls_and_modes.md │   ├── virtual_memory.md │   ├── paging_and_tlbs.md │   ├── scheduling.md │   └── io_stack.md ├── src/ │   ├── processes/ │   ├── syscalls/ │   ├── vm/ │   ├── mmap_vs_read/ │   └── scheduling/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 3 README must answer:

- What OS costs surprised you the most?
    
- Which operations caused page faults?
    
- Where did cache effects dominate?
    
- How would these costs affect:
    
    - real-time XR frame loops?
        
    - AI inference runtimes?
        
    - high-throughput servers?
        
- What policies would you avoid in latency-critical systems?
    

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You can explain a page fault without diagrams
    
- You can estimate syscall and context switch costs
    
- You understand when to use processes vs threads
    
- You know why mmap can outperform read — and vice versa
    
- You instinctively minimize kernel crossings in hot paths
    

If anything feels fuzzy → repeat the measurements.

---

## Why Phase 3 Matters for What Comes Next

- **Concurrency (Phase 4):** scheduling + memory effects dominate
    
- **GPU systems:** kernel crossings kill latency
    
- **XR:** page faults cause dropped frames
    
- **AI systems:** memory mapping & NUMA placement matter
    
- **Security:** isolation boundaries become real