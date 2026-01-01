
**Purpose:** Remove abstraction myths and establish low-level muscle memory  
**Outcome:** You stop being surprised by crashes, slowdowns, and “weird” behavior

---

## Phase 0 Objectives (Non-Negotiable)

By the end of this phase, you will:

- Think in **memory layouts**, not variables
    
- Understand **stack vs heap** mechanically
    
- Recognize **undefined behavior** on sight
    
- Read **compiler-generated assembly**
    
- Debug without guesswork
    
- Trust tools, not intuition
    

This phase is the **foundation for everything that follows**.

---

## Core Topics to Master

### 1. The C Memory Model (Practical)

- Stack frames
    
- Heap allocation
    
- Object lifetimes
    
- Aliasing
    
- Alignment
    
- Padding
    
- Endianness
    

You are not memorizing rules — you are learning _what the machine does_.

---

### 2. Undefined Behavior (UB) as a Concept

- Why UB exists
    
- Why compilers exploit it
    
- How UB creates “working” bugs
    
- Why sanitizers matter
    

Key insight:

> If behavior is undefined, **the compiler is allowed to betray you**.

---

### 3. Toolchain Literacy (Critical Skill)

You must become fluent with:

- `clang` / `gcc` flags
    
- `gdb` stack inspection
    
- `objdump` disassembly
    
- `perf` for basic measurement
    
- `valgrind` / sanitizers
    

This is not optional — this is your **microscope**.

---

### 4. Assembly Awareness (Not Mastery)

- Function prologues/epilogues
    
- Calling conventions
    
- Registers vs memory
    
- How loops compile
    
- How optimizations change code
    

You are learning to **recognize patterns**, not write assembly by hand.

---

## Reference Material (Used Lightly)

- **Computer Systems: A Programmer’s Perspective**  
    Use selectively:
    
    - Data representation
        
    - Machine-level code
        
    - Memory hierarchy (preview only)
        

This is a _reference_, not a cover-to-cover read.

---

## Execution Work (What You Actually Build)

### Project 0.1 — Memory Reality Lab

**Goal:** Understand how memory actually behaves

**What to implement**

- Stack vs heap allocation experiments
    
- Struct padding & alignment tests
    
- Pointer aliasing examples
    
- Endianness inspection
    
- Lifetime violations
    

**Required experiments**

- Print raw memory
    
- Inspect addresses
    
- Trigger and explain crashes
    
- Compare behavior under `-O0` vs `-O2`
    

---

### Project 0.2 — Undefined Behavior Zoo

**Goal:** Learn to _recognize and respect_ UB

**What to implement**

- Use-after-free
    
- Double free
    
- Uninitialized reads
    
- Out-of-bounds access
    
- Signed overflow
    

**Required analysis**

- Run with:
    
    - No sanitizers
        
    - AddressSanitizer
        
    - UndefinedBehaviorSanitizer
        
- Observe _different outcomes_
    
- Document what changed and why
    

---

### Project 0.3 — Compiler Illusions

**Goal:** See how code becomes instructions

**What to implement**

- Small C programs
    
- Compile with different optimization levels
    
- Disassemble output
    
- Compare control flow
    
- Observe dead code elimination
    
- Observe reordering
    

**Key insight**

> “Readable C” ≠ “predictable machine behavior”

---

### Project 0.4 — Debugger Fluency

**Goal:** Remove fear of debugging

**What to practice**

- Stack inspection
    
- Register inspection
    
- Memory examination
    
- Breakpoints & watchpoints
    
- Stepping assembly
    

You should be able to answer:

> “Why did this segfault?”  
> without guessing.

---

## GitHub Repository Structure (Phase 0)

Create **one repo per phase**, starting now.

### Repository name

`systems-phase-0-foundations`

### Recommended structure

`systems-phase-0-foundations/ ├── README.md ├── notes/ │   ├── memory_model.md │   ├── undefined_behavior.md │   ├── compiler_optimizations.md │   └── debugging_notes.md ├── src/ │   ├── memory/ │   │   ├── stack_vs_heap.c │   │   ├── struct_padding.c │   │   └── endianness.c │   ├── ub/ │   │   ├── use_after_free.c │   │   ├── double_free.c │   │   └── overflow.c │   ├── compiler/ │   │   ├── optimization_test.c │   │   └── dead_code.c │   └── debug/ │       └── crash_me.c ├── build/ ├── CMakeLists.txt └── tools.md`

---

## Required Documentation (This Matters)

Your `README.md` **must answer**:

- What surprised you?
    
- What assumptions were wrong?
    
- What changed under optimization?
    
- What tools revealed hidden behavior?
    
- What now feels _obvious_ that didn’t before?
    

This reflection is **part of mastery**.

---

## Mastery Checklist (Must All Be True)

You do **not** move on until:

- You can explain stack vs heap **without metaphors**
    
- You know why UB exists and why it’s dangerous
    
- You can read simple disassembly
    
- You can debug a crash confidently
    
- You trust tools over intuition
    
- Segfaults no longer feel mysterious
    

If any item feels shaky → repeat experiments.

---

## Why Phase 0 Is So Important

This phase:

- Prevents superstition
    
- Makes later performance work honest
    
- Makes security vulnerabilities intuitive
    
- Makes concurrency reasoning possible
    
- Makes AI systems _understandable_
    

Most developers never complete this phase properly.  
That’s why they hit a ceiling.