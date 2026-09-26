---
name: testcase-generator
description: Generate comprehensive adversarial testcases, boundary scenarios, and stress-testing harnesses.
---

# Testcase Generator Skill

## Overview
Generates extreme boundary inputs, stress test suites, and random fuzzing inputs to validate algorithmic correctness and expose subtle edge-case failures.

## Operations
1. Generates minimum ($N=0, 1$) and maximum ($N=10^5$) boundary inputs.
2. Formulates adversarial cases: skewed trees, disconnected graphs, all duplicate values.
3. Compares optimized solution outputs against naive brute-force baselines.
4. Identifies memory allocation hazards and stack overflow risks.
