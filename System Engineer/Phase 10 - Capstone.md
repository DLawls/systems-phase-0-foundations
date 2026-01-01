**Purpose:** Prove end-to-end systems mastery under real constraints  
**Outcome:** A system you could credibly:

- turn into a start-up
    
- publish as a systems case study
    
- extend into research
    
- use as a career-defining portfolio artifact
    

You are no longer “learning topics”.  
You are **building a system that must survive reality**.

---

## Phase 10 Non-Negotiable Requirements

Your capstone **must**:

- Run on **real hardware** (desktop GPU)
    
- Enforce **hard constraints** (latency, memory, power, correctness)
    
- Contain **measurable performance goals**
    
- Fail gracefully under load
    
- Include a **clear architectural narrative**
    
- Integrate **multiple previous phases**
    
- Have **explicit tradeoffs**, not handwaving
    

If it doesn’t hurt a little to design — it’s not ambitious enough.

---

## Choose ONE Capstone Track

You should pick **exactly one**. Depth > breadth.

---

## OPTION A — Real-Time AI Runtime (XR-Class Constraints)

**Who this is for:**  
AI systems + XR + real-time obsession (your strongest overlap)

### What You Build

A **real-time AI inference runtime** that:

- Serves token-by-token inference
    
- Coexists with a simulated frame loop (e.g. 90Hz)
    
- Enforces **strict latency budgets**
    
- Uses:
    
    - KV cache management
        
    - dynamic batching
        
    - backpressure
        
    - memory arenas
        
- Never misses frame deadlines
    

### Hard Constraints

- Frame budget (e.g. 11.1ms)
    
- Tail latency (p99 < budget)
    
- Bounded memory growth
    
- Predictable degradation under load
    

### Why This Is Powerful

- Almost nobody can do this well
    
- Directly applicable to XR, robotics, on-device AI
    
- Investor-credible
    
- Research-adjacent
    

---

## OPTION B — GPU Workload Scheduler (AI + Graphics)

**Who this is for:**  
Systems + GPU + infra thinking

### What You Build

A **GPU workload scheduler** that:

- Manages competing GPU tasks:
    
    - graphics
        
    - inference
        
    - background compute
        
- Uses:
    
    - async compute
        
    - priority queues
        
    - budget enforcement
        
- Prevents starvation
    
- Adapts to power/thermal constraints
    

### Hard Constraints

- Fairness vs latency tradeoff
    
- Preemption limits
    
- Sustained performance under thermal pressure
    

### Why This Is Powerful

- Maps directly to engines, drivers, platforms
    
- Rare skillset
    
- Deep hardware/system understanding
    

---

## OPTION C — Edge AI Runtime (Cost + Power Optimized)

**Who this is for:**  
Startup + deployment realism

### What You Build

An **edge inference runtime** that:

- Runs quantized models (INT8 / INT4)
    
- Uses aggressive memory reuse
    
- Minimizes power draw
    
- Adapts quality under load
    
- Provides predictable latency
    

### Hard Constraints

- Power budgets
    
- Memory ceilings
    
- Accuracy vs speed tradeoffs
    
- Load spikes
    

### Why This Is Powerful

- Direct commercial relevance
    
- Clear differentiation
    
- Real customers exist
    

---

## OPTION D — Real-Time Simulation Engine (AI Agents)

**Who this is for:**  
Game dev + AI + systems synthesis

### What You Build

A **real-time simulation engine** that:

- Runs hundreds/thousands of AI agents
    
- Uses:
    
    - ECS or data-oriented design
        
    - task scheduling
        
    - cache-friendly layouts
        
- Enforces frame deadlines
    
- Remains deterministic
    

### Hard Constraints

- Frame pacing
    
- Memory locality
    
- Parallelism without chaos
    

### Why This Is Powerful

- Bridges games, AI, and infra
    
- Extremely strong signal of systems skill
    
- Great foundation for future products
    

---

## Capstone Architecture Requirements

Regardless of option, your system **must include**:

### 1. Clear Architecture Diagram (Textual OK)

- Components
    
- Data flow
    
- Control flow
    
- Hot paths
    
- Failure paths
    

### 2. Performance Budget

You must define:

- Latency budgets
    
- Memory budgets
    
- Throughput targets
    
- Power expectations (qualitative minimum)
    

### 3. Measurement Infrastructure

You must report:

- p50 / p95 / p99 latency
    
- Throughput
    
- Memory usage
    
- GPU utilization
    
- Failure behavior
    

No benchmarks → no credibility.

---

## Repo Plan (Phase 10)

**Repo name**

`systems-phase-10-capstone`

**Structure**

`systems-phase-10-capstone/ ├── README.md ├── architecture/ │   ├── design.md │   └── tradeoffs.md ├── notes/ │   ├── constraints.md │   ├── failure_modes.md │   └── future_work.md ├── src/ │   ├── core/ │   ├── scheduler/ │   ├── runtime/ │   ├── gpu/ │   └── metrics/ ├── benchmarks/ ├── tools.md └── build/`

---

## README Must Answer (Non-Optional)

Your README **must clearly answer**:

1. What problem does this system solve?
    
2. What constraints shaped the design?
    
3. What were the hardest tradeoffs?
    
4. Where did performance come from?
    
5. Where did it fail — and why?
    
6. How does it degrade under load?
    
7. What would you do next with more time?
    
8. Why is this system hard to build?
    

If someone technical reads it and says

> “Yeah, this is serious systems work”  
> —you succeeded.

---

## Graduation Criteria (This Is Important)

You are **done** when:

- You trust your measurements
    
- You can explain every major design decision
    
- You know exactly where the system breaks
    
- You understand what would make it 10× better
    
- You no longer feel like you’re “learning systems” — you’re **doing systems**
    

At that point, you are operating at:

- senior/principal systems engineer level
    
- or early-stage infra founder level