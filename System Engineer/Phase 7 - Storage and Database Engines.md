**Purpose:** Build durable, high-performance data systems  
**Outcome:** You understand how data survives crashes _and_ stays fast

---

## Phase 7 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand **durability vs performance tradeoffs**
    
- Know why **append-only logs dominate storage**
    
- Build **LSM trees and B-trees**
    
- Understand **write amplification, read amplification**
    
- Understand **MVCC and snapshot isolation**
    
- Know how **databases recover from crashes**
    
- Reason about **storage cost, latency, and energy**
    

This phase is critical for:

- AI feature stores
    
- XR world state
    
- Distributed systems correctness
    
- Startup data reliability
    

---

## Core Mental Model (Must Internalize)

> **Storage engines trade write cost for read cost (or vice versa).  
> There is no free lunch — only different amplification patterns.**

---

## Core Topics to Master

### 1) Storage Media Reality

- DRAM vs SSD vs HDD
    
- Latency vs throughput
    
- Sequential vs random IO
    
- fsync and durability semantics
    

**Key question:**  
Why is sequential IO still king?

---

### 2) Write-Ahead Logging (WAL)

- Append-only logs
    
- Crash recovery
    
- Replay
    
- Group commit
    

**Key question:**  
Why do databases write data _twice_?

---

### 3) Indexing Structures

- B-trees
    
- LSM trees
    
- Bloom filters
    
- Compaction
    

**Key question:**  
Why do modern databases prefer LSM trees?

---

### 4) Concurrency Control & MVCC

- Snapshot isolation
    
- Version chains
    
- Read vs write conflicts
    
- Garbage collection of versions
    

**Key question:**  
How do readers avoid blocking writers?

---

### 5) Query Execution (Light but Real)

- Point lookups
    
- Range scans
    
- Query planning intuition
    
- Cost-based decisions
    

**Key question:**  
Why is “just scan it” sometimes optimal?

---

## Mathematical Lens (Applied)

You will reason with:

- Amortized analysis
    
- Write amplification
    
- Read amplification
    
- Space amplification
    
- Latency distributions
    

---

## Energy & Hardware Reality (Integrated)

You will observe:

- Writes are expensive (energy + wear)
    
- fsync is slow for a reason
    
- Compaction burns IO and power
    
- Memory-heavy systems reduce IO cost
    

---

## Primary References (Anchors)

- **Database Internals** — primary reference
    
- Selected database papers (LSM, WAL, MVCC)
    

Use as **engineering references**, not textbooks.

---

# Execution Work (What You Build)

## Project 7.1 — WAL & Crash Recovery

**Goal:** Make durability concrete

**Implement**

- Append-only log
    
- Periodic checkpoints
    
- Crash + replay recovery
    

**Simulate**

- Process crash mid-write
    
- Recovery correctness
    

**Mastery check**

- You understand why WAL precedes writes
    

---

## Project 7.2 — B-Tree Engine

**Goal:** Understand classic indexing

**Implement**

- Disk-backed B-tree
    
- Insert / lookup / range scan
    
- Page splitting & merging
    

**Mastery check**

- You understand why B-trees are read-optimized
    

---

## Project 7.3 — LSM Tree Engine

**Goal:** Understand modern write-heavy databases

**Implement**

- Memtable
    
- SSTables
    
- Compaction
    
- Bloom filters
    

**Measure**

- Write amplification
    
- Read amplification
    

**Mastery check**

- You can explain why compaction exists — and why it hurts
    

---

## Project 7.4 — MVCC & Snapshots

**Goal:** Enable concurrent access

**Implement**

- Versioned records
    
- Snapshot reads
    
- Simple garbage collection
    

**Mastery check**

- You understand how readers avoid blocking writers
    

---

## Project 7.5 — Mini Query Engine

**Goal:** Tie indexing and execution together

**Implement**

- Simple planner for:
    
    - point queries
        
    - range scans
        
- Measure cost tradeoffs
    

**Mastery check**

- You know why some queries avoid indexes
    

---

## 🔥 Flagship Project — Crash-Safe Key-Value Store

**Goal:** Integrate everything

### What you build

A persistent KV store with:

- WAL
    
- Either B-tree or LSM index
    
- MVCC reads
    
- Crash recovery
    

### Required explanation

Your README must explain:

- Durability guarantees
    
- Amplification tradeoffs
    
- Failure modes
    
- Applicability to:
    
    - AI feature storage
        
    - XR world state
        
    - Distributed replication (Phase 6)
        

---

## Repo Plan (Phase 7)

**Repo name**

`systems-phase-7-storage-engines`

**Structure**

`systems-phase-7-storage-engines/ ├── README.md ├── notes/ │   ├── wal_and_recovery.md │   ├── btrees.md │   ├── lsm_trees.md │   ├── mvcc.md │   └── query_execution.md ├── src/ │   ├── wal/ │   ├── btree/ │   ├── lsm/ │   ├── mvcc/ │   └── kv_store/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 7 README must answer:

- Why does WAL exist?
    
- What amplifications did you observe?
    
- Which workloads favor B-trees vs LSM?
    
- How does MVCC affect memory usage?
    
- How would this design change for:
    
    - AI feature stores?
        
    - XR world state?
        
    - Distributed replication?
        

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You understand crash recovery deeply
    
- You can explain LSM vs B-tree tradeoffs
    
- You understand amplification costs
    
- You trust your durability guarantees
    
- You see why storage dominates system design
    

---

## Why Phase 7 Matters for What Comes Next

- **AI systems:** feature storage, checkpoints
    
- **XR:** persistent world state
    
- **Distributed systems:** replication + logs
    
- **Security:** integrity & durability
    
- **Startups:** data loss = death