# LLaMEA: Large Language Model Evolutionary Algorithm

**LLaMEA** combines evolutionary computation optimization with large language models (LLM) to automatically design metaheuristic optimization algorithms. Instead of requiring a human expert to manually craft algorithms, LLaMEA uses GPT-4 to generate, mutate, and select algorithms — then tests them on benchmarks to find the best performers.

> **Live at:** [xai-liacs.github.io/llamea/](https://xai-liacs.github.io/llamea/)

## Key Results

Generated algorithms **outperform** CMA-ES (Covariance Matrix Adaptation Evolution Strategy) and Differential Evolution on the BBOB benchmark in 5 dimensions — despite never seeing those instances during training.

## Explore the Wiki

| Page | Topic |
|------|-------|
| [00 — Start Here](pages/00-answer) | TL;DR — what LLaMEA actually does and why it matters |
| [01 — Optimization Foundations](pages/01-optimization-foundations) | Gradient, gradient-free, box-constrained |
| [02 — Evolutionary Computation](pages/02-evolutionary-computation) | Biological inspiration, algorithm portfolio |
| [03 — Metaheuristics Explained](pages/03-metaheuristics-explained) | Exploration vs. exploitation, 500+ methods |
| [04 — LLaMEA Core Loop](pages/04-llamea-core-loop) | How an LLM enters the evolutionary loop |
| [05 — Architecture](pages/05-architecture) | System architecture and module integration |
| [06 — BBOB Benchmark](pages/06-bbob-benchmark) | BBOB benchmark and IOHprofiler |
| [07 — Experimental Results](pages/07-experimental-results) | What LLaMEA actually achieves |
| [09 — Getting Started](pages/09-getting-started) | Installation and your first experiment |

## About

LLaMEA is developed by the [LIACS XAI Group](https://naco.liacs.nl/projects/2024-llamea/) at Leiden University.

**Citation:**
> van Stein & Bäck, *LLaMEA: A Large Language Model Evolutionary Algorithm for Automatically Generating Metaheuristics*, arXiv:2405.20132, 2024

## Navigation

Use the **sidebar** to browse all pages. Use the **search bar** to find specific topics.
