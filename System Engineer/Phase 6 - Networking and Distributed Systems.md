**Purpose:** Reason about time, failure, and truth across machines  
**Outcome:** You can design distributed systems that stay correct under latency, loss, and partial failure

---

## Phase 6 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Understand **latency vs throughput** at the network level
    
- Know how **packets actually move**
    
- Understand **why clocks lie**
    
- Build **replicated, fault-tolerant systems**
    
- Reason in **invariants**, not hope
    
- Understand why “just add retries” breaks systems
    
- Design backpressure-aware distributed pipelines
    

This phase changes how you think about **APIs, services, and reliability** forever.

---

## Core Mental Model (Must Internalize)

> **Distributed systems fail by default. Correctness must be designed, not assumed.**

If something _can_ arrive late, duplicated, or out of order — it eventually will.

---

## Core Topics to Master

### 1) Networking Reality (Packets, Not APIs)

- Ethernet, IP, TCP (conceptual)
    
- UDP vs TCP
    
- Latency vs bandwidth
    
- Congestion & queues
    
- Head-of-line blocking
    
- QUIC (conceptual)
    

**Key question:**  
Why does high throughput often increase latency?

---

### 2) Time & Clocks

- Wall clocks vs monotonic clocks
    
- Clock drift
    
- NTP (conceptual)
    
- Why clocks cannot be trusted for ordering
    

**Key question:**  
Why is “timestamp ordering” a trap?

---

### 3) Failure Models

- Crash failures
    
- Omission failures
    
- Network partitions
    
- Slow nodes (the worst kind)
    
- Partial failure
    

**Key question:**  
Why is a slow node more dangerous than a dead one?

---

### 4) Replication & Logs

- Write-ahead logs
    
- Append-only design
    
- State machines
    
- Replication lag
    
- Determinism
    

**Key question:**  
Why do logs dominate distributed system design?

---

### 5) Consensus (Practical, Not Academic)

- Leader-based consensus
    
- Quorums
    
- Raft mental model
    
- Safety vs liveness
    
- Configuration changes (conceptual)
    

**Key question:**  
What does consensus _actually_ guarantee?

---

### 6) Consistency & Tradeoffs

- Strong vs eventual consistency
    
- Read-your-writes
    
- Linearizability (intuition)
    
- CAP (correct interpretation)
    

**Key question:**  
What invariants must never be violated?

---

## Mathematical Lens (Applied)

You will reason with:

- Latency distributions (not averages)
    
- Tail latency
    
- Quorum math (majorities)
    
- Backpressure propagation
    

No proofs — only system behavior under stress.

---

## Energy & Hardware Reality (Integrated)

You will observe:

- Network IO is expensive (power + latency)
    
- Serialization costs dominate
    
- Retries amplify load
    
- Data movement is often the biggest cost
    

---

## Primary References (Anchors)

- **Designing Data-Intensive Applications** — primary truth source
    
- MIT 6.824 lecture notes (reference)
    
- TCP/IP RFCs (skim selectively)
    

---

# Execution Work (What You Build)

## Project 6.1 — Reliable UDP Protocol

**Goal:** Understand what TCP gives you

**Implement**

- UDP-based protocol with:
    
    - sequencing
        
    - acknowledgements
        
    - retransmissions
        
    - basic congestion control
        

**Simulate**

- Packet loss
    
- Reordering
    
- Duplication
    

**Mastery check**

- You understand why TCP exists
    

---

## Project 6.2 — Latency vs Throughput Lab

**Goal:** Observe queueing effects

**Implement**

- Simple client/server
    
- Vary:
    
    - request rate
        
    - payload size
        
    - concurrency
        

**Measure**

- Mean latency
    
- Tail latency (p95/p99)
    

**Mastery check**

- You can explain latency explosions
    

---

## Project 6.3 — Replicated Log

**Goal:** Build the backbone of distributed systems

**Implement**

- Append-only log
    
- Leader/follower replication
    
- Replay on restart
    

**Mastery check**

- You understand state machine replication
    

---

## Project 6.4 — Consensus (Raft-Style)

**Goal:** Build fault tolerance deliberately

**Implement**

- Leader election
    
- Log replication
    
- Basic failure handling
    

**Simulate**

- Node crashes
    
- Network partitions
    

**Mastery check**

- You can explain safety vs liveness
    

---

## Project 6.5 — Distributed Key-Value Store

**Goal:** Integrate everything

**Implement**

- KV store on top of replicated log
    
- Consistent reads/writes
    
- Failure recovery
    

**Mastery check**

- You know what guarantees your system provides — and which it doesn’t
    

---

## 🔥 Flagship Project — Failure Injection Harness

**Goal:** Make failure a first-class citizen

### What you build

A harness that:

- Injects:
    
    - latency
        
    - packet loss
        
    - node crashes
        
- Measures:
    
    - correctness
        
    - recovery time
        
    - tail latency
        

### Required explanation

Your README must explain:

- Which failures broke the system
    
- Which invariants held
    
- Why retries can amplify failure
    
- Implications for:
    
    - AI inference services
        
    - XR shared worlds
        
    - Real-time data feeds
        

---

## Repo Plan (Phase 6)

**Repo name**

`systems-phase-6-distributed-systems`

**Structure**

`systems-phase-6-distributed-systems/ ├── README.md ├── notes/ │   ├── networking_realities.md │   ├── clocks_and_time.md │   ├── failure_models.md │   ├── replication_and_logs.md │   ├── consensus.md │   └── consistency.md ├── src/ │   ├── udp_protocol/ │   ├── latency_tests/ │   ├── replicated_log/ │   ├── consensus/ │   └── kv_store/ ├── tools.md ├── build/ └── CMakeLists.txt`

---

## Required Documentation (Mandatory)

Your Phase 6 README must answer:

- Which failures caused incorrect behavior?
    
- What invariants did you enforce?
    
- Why did latency explode under load?
    
- How does backpressure stabilize systems?
    
- How would these lessons apply to:
    
    - AI inference serving?
        
    - XR multiplayer worlds?
        
    - Exchanges and real-time feeds?
        

---

## Mastery Checklist (All Must Be True)

You may proceed only when:

- You reason in invariants, not timestamps
    
- You understand quorum-based decisions
    
- You expect partial failure
    
- You understand tail latency
    
- You design retries carefully
    
- You stop trusting “eventual” by default
    

---

## Why Phase 6 Matters for What Comes Next

- **Databases:** replication & durability
    
- **AI systems:** model serving & scaling
    
- **XR:** shared state & synchronization
    
- **Security:** trust boundaries
    
- **Startups:** reliability is reputation