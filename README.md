# Neural Network Training using PSO and PSO+GA

This project explores **neural network training using Particle Swarm Optimization (PSO)** and its **hybridization with Genetic Algorithms (GA)** for optimizing both structural (e.g., number of neurons) and non-structural (e.g., weights and biases) parameters. Multiple datasets have been used to evaluate model performance, and comparisons are made against traditional gradient-based methods like Adam.

## Overview

Traditional gradient-based optimization (like Adam or SGD) can be sensitive to local minima and computationally expensive for large search spaces. This project investigates the use of **PSO**, and a **hybrid PSO-GA** strategy, to efficiently search complex optimization landscapes in both structural and non-structural domains of neural networks.

## Repository Structure

```
Root
├── Results_Code_PSO
│   └── Neural network training using PSO on datasets: Iris, Digits, SpamBase, Wine, MNIST
│
├── Results__PSO_GA
│   └── Neural network training using a hybrid PSO + GA algorithm on datasets: Iris, Digits, SpamBase, Wine, MNIST
│
├── Plots_PSO
│   └── Visualizations of best vs. worst performing particles across iterations
│
├── LOGS_PSO
│   └── Training logs of PSO runs (accuracy and loss improvements across trials/iterations)
│
├── LOGS_PSO_GA
│   └── Training logs of PSO+GA runs (accuracy and loss improvements across trials/iterations)
│
├── Benchmark_Results_Adam_100
│   └── Neural network training using Adam optimizer for 100 epochs
│
├── Benchmark_Results_Adam_150
│   └── Neural network training using Adam optimizer for 150 epochs
│
└── Final_Report.pdf
    └── Detailed methodology, experiments, results, and analysis
```

## Datasets Used

* Iris
* Digits
* Wine
* SpamBase
* Breast Cancer
* MNIST
* CIFAR-10 (used in report only)

## Optimization Strategies

### Particle Swarm Optimization (PSO)

* Optimization of:

  * Structural parameters (e.g., number of hidden units)
  * Non-structural parameters (e.g., weight matrices)

#### PSO Setup - Results & Discussion

The PSO algorithm was tested on multiple datasets. Table II summarizes the results:

| Dataset       | Loss                  | Accuracy            |
| ------------- | --------------------- | ------------------- |
| Iris          | 0.33 → 0.32 (3% ↓)    | 93% → 93% (→ 0%)    |
| Wine          | 0.42 → 0.42 (→ 0%)    | 97% → 100% (3.1% ↑) |
| Digits        | 0.65 → 0.49 (24.6% ↓) | 84% → 86% (2.4% ↑)  |
| Breast Cancer | 0.05 → 0.05 (→ 0%)    | 98% → 99% (1.0% ↑)  |
| Spam Base     | 0.24 → 0.24 (→ 0%)    | 91% → 91% (→ 0%)    |
| MNIST         | 0.49 → 0.49 (→ 0%)    | 84% → 84% (→ 0%)    |
| CIFAR-10      | 0.20 → 0.07 (65% ↓)   | 95% → 98% (3.2% ↑)  |

**Key Observations:**

* Significant loss reduction was observed in the Digits (24.6%) and CIFAR-10 (65%) datasets, indicating effective convergence.
* Accuracy improvements were seen in Wine (3.1%), CIFAR-10 (3.2%), and Breast Cancer (1.0%); some datasets (e.g., Iris, Spam Base, MNIST) showed no change.
* Stagnation in optimization occurred in several cases (e.g., Wine, MNIST), likely due to PSO getting trapped in local optima.

**Particle Stagnation in PSO and Hybrid PSO–GA:**

* Poor-performing particles tended to linger and contribute minimally to convergence, reducing swarm diversity.
* High-dimensional landscapes challenge PSO’s standard exploration mechanisms.

### PSO + Genetic Algorithm (Hybrid)

* Combines:

  * **PSO for local exploitation**
  * **GA (crossover & mutation) for global exploration**

#### PSO-GA Setup - Results & Discussion

| Dataset       | Loss                    | Accuracy            |
| ------------- | ----------------------- | ------------------- |
| Iris          | 0.61 → 0.43 (29.5% ↓)   | 89% → 93% (4.5% ↑)  |
| Wine          | 0.19 → 0.05 (73.7% ↓)   | 97% → 100% (3.1% ↑) |
| Digits        | 3.00 → 0.67 (77.7% ↓)   | 43% → 84% (95.3% ↑) |
| Breast Cancer | 0.50 → 0.0006 (99.9% ↓) | 98% → 100% (2.0% ↑) |
| Spam Base     | 0.20 → 0.12 (40.0% ↓)   | 92% → 95% (3.3% ↑)  |
| MNIST         | 0.44 → 0.33 (25.0% ↓)   | 85% → 89% (4.7% ↑)  |
| CIFAR-10      | 0.20 → 0.11 (45.0% ↓)   | 96% → 97% (1.0% ↑)  |

**Key Observations:**

* Hybrid approach consistently improved results over standalone PSO.
* Demonstrated significant gains in datasets previously stagnant under PSO (e.g., Breast Cancer, Spam Base, MNIST).
* Slight decline in CIFAR-10 improvements likely due to complex interdependencies in convolutional architectures.

### Benchmarks with Adam

| Dataset       | Loss | Accuracy |
| ------------- | ---- | -------- |
| Iris          | 0.56 | 90%      |
| Wine          | 0.16 | 97%      |
| Digits        | 0.67 | 87%      |
| Breast Cancer | 0.11 | 97%      |
| Spam Base     | 0.20 | 92%      |
| MNIST         | 0.08 | 97%      |
| CIFAR-10      | 0.03 | 99%      |

**Convergence Dynamics:**
Gradient-based methods like Adam efficiently use derivatives, often outperforming PSO/GA in high-dimensional scenarios. Future work may explore hybridizing gradient and evolutionary approaches.

## Key Insights

* PSO achieved promising results in low- to mid-dimensional spaces.
* Hybrid PSO+GA improved convergence and generalization in many scenarios.
* Adam performed better in high-dimensional image datasets like CIFAR-10.
