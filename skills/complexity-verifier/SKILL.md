---
name: complexity-verifier
description: Verify asymptotic Big-O time and space complexity against contest time and memory limits.
---

# Complexity Verifier Skill

## Overview
Mathematically proves the asymptotic runtime and memory footprint of algorithms, ensuring solutions pass within standard limits ($10^8$ operations, 256MB).

## Operations
1. Evaluates loop bounds, recursion depth, and data structure amortized costs.
2. Derives formal Big-O worst-case time and auxiliary space bounds.
3. Computes the execution feasibility score ($F$) against contest constraints.
4. Identifies integer overflow risks and prescribes 64-bit integer protections.
