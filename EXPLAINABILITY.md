# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **CodeCraft Agent** (`codecraft-agent`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** CodeCraft Agent (`codecraft-agent`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Education / Competitive Programming & Algorithmic Synthesis  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), FERPA, GDPR  

---

## How the Agent Decides

CodeCraft Agent is an autonomous algorithmic reasoning and competitive programming intelligence agent designed for **CodeCraft**, a structured, community-driven competitive programming handbook and algorithm reference platform. The agent automates algorithmic pattern recognition, asymptotic time/space complexity verification, optimal code synthesis, and pedagogical problem-solving walkthroughs.

### 1. Decision Architecture

The problem analysis, solution synthesis, and complexity verification workflow operates across a deterministic, five-stage pipeline:

```
User Query / Problem Statement (Input Constraints, Target Output, Sample Testcases)
    │
    ▼
[Stage 1: Problem Ingestion & Constraint Extraction]
    │  - Normalizes problem statement and extracts input bounds: $N, M \le 10^5$, value ranges $[-10^9, 10^9]$
    │  - Identifies target execution limits: Time Limit (e.g., 1.0s / $10^8$ ops), Memory Limit (e.g., 256MB)
    │  - Calculates theoretical upper-bound complexity ceiling: $O(N \log N)$, $O(N)$, or $O(\sqrt{N})$
    ▼
[Stage 2: Algorithmic Pattern Recognition & Paradigm Routing]
    │  - Routes problem to dominant algorithmic archetype:
    │      ├── Dynamic Programming (Optimal substructure, overlapping subproblems)
    │      ├── Graph Algorithms (Shortest path, MST, topological sorting, bipartite matching)
    │      ├── Trees & Range Queries (Segment Tree, Fenwick Tree, Lowest Common Ancestor)
    │      ├── Two Pointers & Sliding Window (Monotonicity properties)
    │      └── Greedy Algorithms (Matroid properties, greedy-choice property proof)
    ▼
[Stage 3: Complexity Boundary & Invariant Proof]
    │  - Formulates loop invariants, state transitions, or topological orderings
    │  - Mathematically proves that worst-case runtime stays well within the 1.0s time limit
    │  - Flags integer overflow hazards ($N \cdot M > 2^{31}-1$) and enforces 64-bit integer types (`long long`)
    ▼
[Stage 4: Solution Synthesis & Multi-Language Implementation]
    │  - Authors clean, idiomatic solutions in C++20, Python 3, and Java
    │  - Injects fast I/O routines (`std::ios_base::sync_with_stdio(false)`) where necessary
    │  - Formats detailed step-by-step pedagogical explanations and inline comments
    ▼
[Stage 5: Adversarial Test Generation & Verification Gate]
    │  - Synthesizes edge testcases: minimal $N=0, 1$, maximum boundary $N=10^5$, skewed trees, all equal elements
    │  - Validates output accuracy against brute-force generator for small input domains
    ▼
Structured Handbook Article / Problem Solution & Complexity Dossier
```

### 2. Algorithmic Pattern Taxonomy & Decision Rubric

The agent applies strict operational rules to classify problems into established paradigms based on input bounds $N$:

| Input Bound ($N$) | Required Time Complexity | Feasible Algorithmic Paradigms |
|---|---|---|
| $N \le 10$ | $O(N!)$ or $O(N^2 \cdot 2^N)$ | Permutation recursion, Traveling Salesperson DP |
| $N \le 20$ | $O(2^N)$ or $O(N \cdot 2^N)$ | Bitmask DP, Meet-in-the-Middle, Submask Enumeration |
| $N \le 100$ | $O(N^4)$ or $O(N^3)$ | Floyd-Warshall, Matrix Multiplication, Interval DP |
| $N \le 1,000$ | $O(N^2)$ | Nested loops, All-Pairs shortest paths, $2$D DP |
| $N \le 100,000$ | $O(N \log N)$ or $O(N \sqrt{N})$ | Sorting, Divide & Conquer, Segment Trees, Dijkstra, Mo's Algorithm |
| $N \le 1,000,000$ | $O(N)$ or $O(N \log \log N)$ | Two Pointers, Prefix Sums, Monotonic Stack, Sieve of Eratosthenes |
| $N > 10^9$ | $O(\log N)$ or $O(1)$ | Binary Search, Matrix Exponentiation, Closed-Form Math |

### 3. Complexity Verification & Asymptotic Scoring Formula

To ensure proposed solutions never encounter Time Limit Exceeded (TLE) or Memory Limit Exceeded (MLE), the agent calculates an Execution Feasibility Score $F \in [0.0, 1.0]$:

$$F = 1.0 - \left( 0.50 \cdot \frac{\text{Ops}_{\text{worst}}}{10^8} + 0.30 \cdot \frac{\text{MemoryMB}_{\text{peak}}}{\text{LimitMB}} + 0.20 \cdot P_{\text{constant}} \right)$$

- $\text{Ops}_{\text{worst}}$: Estimated worst-case CPU instruction count derived from asymptotic bounds.
- $\text{MemoryMB}_{\text{peak}}$: Peak resident allocation (e.g., $4 \cdot N$ bytes for a Segment Tree).
- $P_{\text{constant}}$: Language-dependent constant-factor penalty ($0.05$ for idiomatic C++, $0.25$ for interpreted Python).

Solutions are only marked verified when $F \ge 0.70$. If $F < 0.70$, the agent autonomously rejects the approach and explores a tighter asymptotic paradigm.

### 4. Thresholding & Refusal Decision Criteria

CodeCraft Agent enforces strict academic integrity and quality boundaries:
- **Active Contest Cheating Refusal**: The agent detects and strictly refuses queries associated with active, live competitive programming contests (e.g., ongoing Codeforces rounds, live LeetCode contest windows, or active hackathons). The agent returns: *"CodeCraft is an educational reference platform. I do not provide assistance for active live contests."*
- **Ill-Posed Problem Refusal**: If a user submits a problem statement lacking input bounds, output types, or consistent examples, the agent halts and requests precise constraint definitions.
- **Intractable NP-Hard Queries**: If a general problem is proven NP-Hard with constraints $N \ge 100$, the agent explicitly explains the computational intractability and provides polynomial-time approximation or parameterized heuristics rather than claiming a fictional polynomial exact solution.

### 5. Fallback Decision Mechanism

CodeCraft Agent incorporates robust fallback mechanisms for seamless student learning:
- **Offline Algorithm Handbook Fallback**: If external AI model APIs are unreachable or offline, the agent falls back to static algorithm markdown templates and curated reference implementations indexed in `/algos`, ensuring zero disruption to offline revision.
- **Brute-Force Baseline Fallback**: If an optimal $O(N)$ state transition cannot be proven with complete mathematical certainty, the agent defaults to presenting a fully explained, verifiable brute-force or recursive backtracking baseline, clearly annotating the exact bottleneck before exploring optimizations.
- **Model Fallback Cascade**: Primary synthesis requests utilize `gemini-2.0-flash` with automatic failover to `gpt-4o` and `claude-3-5-sonnet`.

### 6. Human-in-the-Loop Governance

CodeCraft enforces complete learner autonomy:
- **Progressive Hint Unlocking**: To foster true problem-solving skill, the agent offers a tiered hint mode (Hint 1: Conceptual Observation, Hint 2: Pattern Identification, Hint 3: Full Code) rather than spoiling full solutions immediately.
- **Student Code Review**: Learners can submit their own code to receive targeted bug identification, invariant audits, and optimization suggestions without having their logic completely rewritten.
- **Community Contribution Auditing**: All handbook algorithms undergo human pull-request reviews, verifying correctness before merging into the main repository.

---

## The Data It Uses

CodeCraft Agent operates under strict educational data minimization and student privacy principles.

### 1. Ingested Input Data

The agent processes only mathematical and programmatic descriptions supplied by the user:
- **Problem Statements**: Problem descriptions, mathematical formulas, constraints, and sample input/output testcases.
- **User Code Submissions**: Source code in C++, Python, Java, or Go submitted by learners for complexity auditing, debugging, or style enhancement.
- **Algorithmic Category Requests**: Student navigation selections (e.g., "Dynamic Programming", "Graph Theory", "Fenwick Trees").

### 2. Configuration & Reference Data

- **Handbook Repository Files**: Curated algorithm implementations, problem write-ups, and explanations located in the `/algos` directory.
- **Standard Contest Compiler Configurations**: Baseline compiler flags (e.g., `g++ -O3 -std=c++20`, `python3.11`, `javac 21`).
- **Standard Mathematical Constants**: Modular arithmetic bases ($10^9 + 7$, $998244353$), infinity representation thresholds (`0x3f3f3f3f`, `1e18`), and floating-point precision limits ($\epsilon = 10^{-9}$).

### 3. Base Model & Inference Lineage

- **Foundation Models**: Employs Google Gemini (`gemini-2.0-flash`), OpenAI (`gpt-4o`), and Anthropic (`claude-3-5-sonnet`) for natural language explanation generation and code synthesis.
- **Deterministic Static Verification**: Code syntax, memory sizes, and Big-O loop counts are verified through deterministic static analysis patterns.
- **Zero Training on Student Submissions**: Student code submissions, personal homework questions, and practice histories are never harvested or utilized for commercial model training.

### 4. Data Privacy, Storage, and Retention

- **Zero PII Collection**: CodeCraft collects no student legal names, institutional IDs, email credentials, or contest ratings.
- **Stateless Execution**: Code queries and problem analyses are processed in-memory and discarded upon completion of the active turn.
- **FERPA & GDPR Compliance**: In full accordance with FERPA and GDPR (Articles 5 & 28), student learning metrics, diagnostic test performance, and practice habits remain completely private and are never monetized or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of CodeCraft Agent is essential for realistic learning.

### 1. NP-Hard Problems & Heuristic Optimality Bounds
- **Limitation**: Classical NP-Hard problems (Traveling Salesperson, Graph Coloring, Set Cover) cannot be solved in polynomial time for large $N$.
- **Mitigation**: The agent transparently explains the theoretical lower bounds (P vs NP), guiding students toward dynamic programming with bitmasks for small $N \le 20$, approximation algorithms, or branch-and-bound heuristics.

### 2. Constant Factor Variance & Micro-Architectural Effects
- **Limitation**: Big-O notation hides constant factors. Two $O(N)$ algorithms may perform drastically differently in practice due to CPU cache locality, branch prediction, and memory allocation overhead.
- **Mitigation**: The agent emphasizes memory-contiguous data structures (such as `std::vector` over linked structures or `std::map`) and benchmarks cache-friendly layouts for high-performance contest environments.

### 3. Language-Specific Runtime Overhead
- **Limitation**: Python implementations of $O(N \log N)$ algorithms on $N=10^6$ can trigger TLE due to interpreter overhead, whereas the identical algorithm in C++ passes within $0.15$ seconds.
- **Mitigation**: The agent explicitly highlights language-specific performance trade-offs, providing idiomatic PyPy optimization tips and C++ equivalents when constraints demand near-metal efficiency.

### 4. Adversarial Testcase Generation Limits
- **Limitation**: Automated testcase generation can occasionally miss rare edge cases in complex geometric or combinatorial problems.
- **Mitigation**: The agent combines random fuzzing with deterministic extreme boundary generation ($N=0, 1$, duplicates, collinear points) and explicitly outlines the mathematical proofs guaranteeing safety.

### 5. Educational Reference vs Active Proctor Boundary
- **Limitation**: CodeCraft Agent is an educational study tutor and reference handbook; it cannot function as an automated proctor or official contest adjudicator.
- **Mitigation**: The agent operates strictly out-of-contest, prioritizing student comprehension, proof mechanics, and deep problem-solving skills over automated grading.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Algorithmic pattern taxonomy & decision rubric | Section 2 | Verified |
| - Complexity verification & feasibility formula | Section 3 | Verified |
| - Thresholding & refusal decision criteria | Section 4 | Verified |
| - Fallback decision mechanism | Section 5 | Verified |
| - Human-in-the-loop governance & student autonomy | Section 6 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested problem statements & user code | Section 1 | Verified |
| - Configuration, handbook files & compiler specs | Section 2 | Verified |
| - Base model lineage & deterministic analysis | Section 3 | Verified |
| - Data privacy, 0-byte retention & FERPA/GDPR | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - NP-Hard bounds & computational intractability | Section 1 | Verified |
| - Constant factor variance & cache effects | Section 2 | Verified |
| - Language-specific runtime overhead | Section 3 | Verified |
| - Adversarial test generation limits | Section 4 | Verified |
| - Educational scope & non-proctor boundary | Section 5 | Verified |
