# LLaMEA: Large Language Model Evolutionary Algorithm

**LLaMEA** combines evolutionary computation optimization with large language models (LLM) to automatically design metaheuristic optimization algorithms. Instead of requiring a human expert to manually craft algorithms, LLaMEA uses GPT-4 to generate, mutate, and select algorithms — then tests them on benchmarks to find the best performers.

> **Live at:** [xai-liacs.github.io/llamea/](https://xai-liacs.github.io/llamea/)

## Key Results

Generated algorithms **outperform** CMA-ES (Covariance Matrix Adaptation Evolution Strategy) and Differential Evolution on the BBOB benchmark in 5 dimensions — despite never seeing those instances during training.

## Explore the Wiki

| Page | Topic |
|------|-------|
| [[00-answer\|Start Here]] | TL;DR — what LLaMEA actually does and why it matters |
| [[01-optimization-foundations\|01]] | Optimization foundations (gradient, gradient-free, box-constrained) |
| [[02-evolutionary-computation\|02]] | Evolutionary computation (biological inspiration, algorithm portfolio) |
| [[03-metaheuristics-explained\|03]] | Metaheuristics (exploration vs. exploitation, 500+ methods) |
| [[04-llamea-core-loop\|04]] | **LLaMEA core loop** — how an LLM enters the evolutionary loop |
| [[05-architecture\|05]] | System architecture and module integration |
| [[06-bbob-benchmark\|06]] | BBOB benchmark and IOHprofiler |
| [[07-experimental-results\|07]] | Experimental results and what they mean |
| [[09-getting-started\|09]] | Installation and your first experiment |

## About

LLaMEA is developed by the [LIACS XAI Group](https://naco.liacs.nl/projects/2024-llamea/) at Leiden University.

**Citation:**
> van Stein & Bäck, *LLaMEA: A Large Language Model Evolutionary Algorithm for Automatically Generating Metaheuristics*, arXiv:2405.20132, 2024

## Navigation

Use the **sidebar** to browse all pages. Use the **search bar** to find specific topics.
