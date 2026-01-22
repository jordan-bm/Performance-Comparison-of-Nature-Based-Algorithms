# Nature-Inspired Optimization Benchmarking  
### Performance Comparison of BMO vs WOA vs MFO on Standard Test Functions

This project benchmarks and compares three well-known **nature-inspired metaheuristic optimization algorithms** across a set of widely used objective functions. Each algorithm is implemented from scratch and evaluated using identical benchmarking conditions to measure both:

- **Optimality** (how close the algorithm gets to the global optimum)
- **Efficiency / convergence behavior** (how quickly and reliably solutions improve)

Algorithms tested:

- **Bird Mating Optimizer (BMO)** - behavior-based optimization  
- **Whale Optimization Algorithm (WOA)** - swarm-based optimization  
- **Moth-Flame Optimization (MFO)** - swarm-based optimization  

All algorithms are evaluated using **six standard benchmark functions**, ranging from unimodal landscapes to highly multimodal (local-minima heavy) search spaces.

> Course Project (Artificial Intelligence, Fall 2025)  
> Authors: Sara Ali, Madison Jones, Jordan Burmylo-Magrann, Anthony Savage 

---

## Motivation

Nature-inspired optimization methods are often used when traditional optimization struggles, such as when:

- the search space is non-convex or discontinuous  
- gradients are unavailable
- many deceptive local minima exist
- exploration vs exploitation balance matters

Instead of focusing on one algorithm, this project emphasizes **direct comparison** across consistent tests to better understand how each method behaves under different landscapes. 

---

## Algorithms Implemented

### Bird Mating Optimizer (BMO) 
BMO simulates bird mating strategies by dividing individuals into behavioral groups (monogamous, polygynous, promiscuous, polyandrous, parthenogenetic). This diversity of mating behavior helps maintain exploration and avoid premature convergence.
- Implementation: Madison Jones
---

### Whale Optimization Algorithm (WOA)
WOA models humpback whales’ bubble-net hunting strategy with three primary movement behaviors:

- **encircling the best solution** (exploitation)
- **random exploration**
- **spiral updating** around the best position

A key feature is a time-varying parameter that shifts the algorithm from exploration to exploitation over iterations.
- Implementation: Jordan Burmylo-Magrann
---

### Moth-Flame Optimization (MFO)
MFO simulates moth navigation toward flames (elite solutions). Moths update positions using a spiral equation toward flames, and the number of flames decreases over time-encouraging exploitation later in the run.
- Implementation: Sara Ali
---

## Benchmark Functions

To test each algorithm, we use six standard objective functions, chosen to represent different optimization difficulty categories. The benchmarking functions are grouped as:

- **Unimodal:** single global minimum, tests convergence efficiency
- **Multimodal:** many local minima, tests exploration / local minimum avoidance
- **Multimodal with few local minima:** fewer deceptive regions, but still non-trivial

| ID | Function | Category | Dim | Bounds | f_min |
|---:|----------|----------|---:|--------|------:|
| f1 | Sphere | Unimodal | 30 | [-100, 100] | 0 |
| f2 | Absolute Sum + Absolute Product | Unimodal | 30 | [-10, 10] | 0 |
| f3 | Rastrigin | Multimodal | 30 | [-5.12, 5.12] | 0 |
| f4 | Griewank | Multimodal | 30 | [-600, 600] | 0 |
| f5 | Six-Hump Camel | Few-local-minima | 2 | [-5, 5] | -1.03162 |
| f6 | Branin | Few-local-minima | 2 | x∈[-5,10], y∈[0,15] | 0.397887 |

Benchmark definitions and parameters were selected based on standard function formulations used in optimization research.

---

## Experimental Setup

To ensure fair comparison:

- Each algorithm is run **30 independent times** per benchmark function
- Results are reported as:
  - mean best fitness
  - standard deviation
  - convergence behavior (fitness vs iteration)
- Iteration count used in evaluations: **500** generations/iterations 

---

## Results Summary (Key Findings)

Across nearly all benchmarks, the **Whale Optimization Algorithm (WOA)** performed best overall in terms of reliability, convergence speed, and final fitness.

### Unimodal functions (f1, f2)
- **WOA** converged fastest and most accurately (very low mean fitness, std ≈ 0)
- **BMO** also performed well, typically converging near the optimum
- **MFO** struggled on f1 (slow convergence, worse final fitness), but improved on f2 

### Multimodal functions with many local minima (f3, f4)
- **WOA** consistently reached the global optimum across runs
- **BMO** remained competitive and close behind
- **MFO** performed significantly worse and often became trapped in local minima 

### Multimodal functions with few local minima (f5, f6)
- All three algorithms performed similarly and reached expected optima
- Minor inconsistencies appeared in WOA behavior on f6 in some runs, likely due to overshooting narrow solution regions 

### Overall conclusion
- **WOA**: strongest and most reliable across all landscapes  
- **BMO**: solid performance, competitive with WOA, slightly less consistent  
- **MFO**: weakest overall, particularly on multimodal functions requiring strong exploration 