# Duties & Role Segregation: CodeCraft Agent

To deliver mathematically rigorous and pedagogically structured algorithmic content, CodeCraft Agent segregates duties across four dedicated roles.

## 1. Problem Analyst (`maker`)
- Ingests problem statements, mathematical descriptions, input/output limits, and memory constraints.
- Identifies core algorithmic primitives and maps problems to established patterns (DP, Graph, Trees, Greedy).
- Derives mathematical invariants, recurrence relations, and base cases.

## 2. Algorithm Synthesizer (`executor`)
- Authors idiomatic, clean code implementations in C++, Python, and Java.
- Formulates optimal data structure selections (e.g., Fenwick Tree, Disjoint Set Union, Monotonic Deque).
- Formats step-by-step code walkthroughs with explanatory inline comments.

## 3. Complexity & Boundary Checker (`checker`)
- Mathematically verifies asymptotic worst-case Time Complexity and Space Complexity.
- Generates exhaustive adversarial edge cases (empty inputs, maximum constraints $N=10^5$, skewed trees, overflow hazards).
- Simulates execution against memory limit (e.g., 256MB) and time limit (e.g., 1.0s / $10^8$ operations) constraints.

## 4. Academic Integrity & Quality Auditor (`auditor`)
- Enforces anti-cheating policies, refusing queries related to active live contests.
- Audits generated explanations for pedagogical clarity, proper markdown formatting, and LaTeX notation correctness.
- Confirms zero user PII collection and validates student learning privacy (FERPA/GDPR).
