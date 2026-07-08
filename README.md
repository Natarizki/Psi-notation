# Ψ (Psi) Notation: Asymptotic Order Guarantees for Multi-Layer Systems

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)](https://github.com/Natarizki/psi-notation)

**Psi Notation** is a formal mathematical framework extending the classical Big-O, Big-Omega, and Big-Theta notations. While classical notations describe the growth rate of a *single* function, **Ψ (Big-Psi)** and **ψ (Little-Psi)** describe the *asymptotic ordering relationship* between **two or three** functions that share the same complexity class `Θ(g(n))`.

This framework is critical in modern system design—such as AI inference pipelines, microservices chains, and real-time data processing—where guaranteeing that upstream stages do not asymptotically outpace downstream stages is crucial for stability, latency, and resource utilization.

---

## 📐 Formal Definitions

### 1. Little-ψ (Two-Layer Ordering)

Let `F₁(n)` and `F₂(n)` be two positive functions representing the resource consumption (time, memory, or bandwidth) of two sequential processing stages. We say the ordered pair `(F₁, F₂)` belongs to the class `ψ(g(n))`, denoted `(F₁, F₂) ∈ ψ(g(n))`, if there exist **positive constants** `c₁, c₂, c₃` and a threshold `n₀ > 0` such that for all `n ≥ n₀`:

```

c₁ · g(n)  ≤  F₁(n)  ≤  c₂ · g(n)  ≤  F₂(n)  ≤  c₃ · g(n)

```

**Immediate Consequences:**
- Both `F₁` and `F₂` are tightly bounded by `g(n)`, i.e., `F₁ ∈ Θ(g(n))` and `F₂ ∈ Θ(g(n))`.
- There is a **guaranteed separation** between the two layers. The term `c₂·g(n)` acts as an *asymptotic bridge*: the worst-case of `F₁` is strictly bounded above by a value that is itself bounded below by the best-case of `F₂`. This mathematically prevents `F₁` from ever dominating `F₂`.

### 2. Big-Ψ (Three-Layer Ordering)

For systems with three sequential stages `(F₁, F₂, F₃)`, we extend the definition. We say `(F₁, F₂, F₃) ∈ Ψ(g(n))` if there exist **positive constants** `c₁, C₂, c₃, c₄` and `n₀ > 0` such that for all `n ≥ n₀`:

```

c₁ · g(n)  ≤  F₁(n)  ≤  C₂ · g(n)  ≤  F₂(n)  ≤  c₃ · g(n)  ≤  F₃(n)  ≤  c₄ · g(n)

```

Here, `C₂` bridges `F₁→F₂`, and `c₃` bridges `F₂→F₃`. This provides a *single unified guarantee* that the entire pipeline is strictly ordered (`F₁ ≤ F₂ ≤ F₃`) without needing to check pairs independently.

---

## 📊 Comprehensive Examples with Standard Complexity Classes

Since both `ψ` and `Ψ` require all functions to share the **same** `Θ(g(n))` class, we provide valid and invalid configurations across five fundamental complexity families: **constant (1)**, **logarithmic (log n)**, **linear (n)**, **linearithmic (n log n)**, and **quadratic (n²)**.

### Valid Configurations for Little-ψ (2 layers)

All pairs below satisfy `(F₁, F₂) ∈ ψ(g(n))` for sufficiently large `n`.

| `g(n)` | Example `F₁(n)` | Example `F₂(n)` | Valid Constants (`c₁, c₂, c₃`) | Condition for `n₀` |
|--------|----------------|----------------|-------------------------------|---------------------|
| `1`    | `5`            | `10`           | `(1, 7, 12)`                  | `n ≥ 1`             |
| `log n`| `2 log n + 1`  | `3 log n - 2`  | `(1, 2.5, 4)`                 | `n ≥ 10`            |
| `n`    | `2n + 10`      | `3n - 5`       | `(1, 2.5, 4)`                 | `n ≥ 20`            |
| `n log n` | `n log n`  | `2 n log n`    | `(0.5, 1.5, 3)`               | `n ≥ 2`             |
| `n²`   | `n² + n`       | `2n² - n`      | `(1, 1.5, 3)`                 | `n ≥ 2`             |

**Verification for `n` case:** We require `1·n ≤ 2n+10 ≤ 2.5n ≤ 3n-5 ≤ 4n`.  
- Left: `n ≤ 2n+10` true.  
- Middle 1: `2n+10 ≤ 2.5n` ⟹ `10 ≤ 0.5n` ⟹ `n ≥ 20`.  
- Middle 2: `2.5n ≤ 3n-5` ⟹ `5 ≤ 0.5n` ⟹ `n ≥ 10`.  
- Right: `3n-5 ≤ 4n` true. Thus `n₀ = 20` works.

### Invalid Configurations for Little-ψ

| `g(n)` | `F₁(n)` | `F₂(n)` | Reason for Invalidity |
|--------|---------|---------|------------------------|
| `n`    | `n`     | `n²`    | `F₂ ∈ Θ(n²)` not `Θ(n)`. No `c₂` can satisfy `c₂·n ≤ n²` and `n² ≤ c₃·n` simultaneously. |
| `n`    | `log n` | `n`     | `F₁ ∈ Θ(log n)` not `Θ(n)`. No `c₁` satisfies `c₁·n ≤ log n` for large `n`. |
| `n²`   | `n`     | `n²`    | `F₁ ∈ Θ(n)` not `Θ(n²)`. Fails lower bound `c₁·n² ≤ n`. |
| `n log n` | `n` | `n log n` | `F₁ ∈ Θ(n)` not `Θ(n log n)`. Fails lower bound. |

### Valid Configurations for Big-Ψ (3 layers)

All triples below satisfy `(F₁, F₂, F₃) ∈ Ψ(g(n))`.

| `g(n)` | `F₁(n)` | `F₂(n)` | `F₃(n)` | Valid Constants (`c₁, C₂, c₃, c₄`) |
|--------|---------|---------|---------|--------------------------------------|
| `1`    | `2`     | `5`     | `10`    | `(1, 3, 7, 12)`                      |
| `log n`| `log n` | `2 log n` | `3 log n` | `(0.5, 1.5, 2.5, 4)`              |
| `n`    | `n`     | `2n`    | `3n`    | `(0.5, 1.5, 2.5, 4)`                |
| `n log n` | `n log n` | `1.5 n log n` | `2 n log n` | `(0.8, 1.2, 1.8, 2.5)` |
| `n²`   | `n²`    | `1.5 n²` | `2 n²`  | `(0.8, 1.2, 1.8, 3)`                |

**Verification for `n` case:**  
`0.5n ≤ n ≤ 1.5n ≤ 2n ≤ 2.5n ≤ 3n ≤ 4n`. All hold trivially for `n ≥ 1`.

### Invalid Configurations for Big-Ψ

| `g(n)` | `F₁(n)` | `F₂(n)` | `F₃(n)` | Reason for Invalidity |
|--------|---------|---------|---------|------------------------|
| `n`    | `n`     | `n log n` | `n²` | Mixed `Θ` classes. A single `g(n)=n` cannot bound `n log n` or `n²`. |
| `log n` | `log n` | `n` | `n²` | Mixed classes. Fails upper bounds for `F₂` and `F₃`. |
| `n²`   | `n`     | `n²`    | `n³`   | `F₁` and `F₃` are not `Θ(n²)`. Fails both lower and upper bounds. |

---

## 🔗 Theorems and Properties

**Theorem 1 (Pair-wise Implication):**  
If `(F₁, F₂, F₃) ∈ Ψ(g(n))`, then both `(F₁, F₂) ∈ ψ(g(n))` and `(F₂, F₃) ∈ ψ(g(n))`.

**Theorem 2 (Strong Transitivity):**  
If `(F₁, F₂, F₃) ∈ Ψ(g(n))`, then for all sufficiently large `n`, `F₁(n) ≤ F₂(n) ≤ F₃(n)`.

**Theorem 3 (Quantitative Gap Bounds):**  
If `(F₁, F₂) ∈ ψ(g(n))`, the asymptotic gap between layers is bounded by:  
`(c₂ - c₁)·g(n) ≤ F₂(n) - F₁(n) ≤ (c₃ - c₂)·g(n)`.  
This provides explicit safety margins for buffer sizing and capacity planning.

---

## 💡 Motivation and Applications

- **AI Inference Pipelines:**  
  Preprocessing (CPU) → Inference (GPU) → Postprocessing (CPU). Enforcing `Ψ` guarantees the CPU preprocessing never starves the GPU.

- **Microservices Chains:**  
  Authentication → Order Processing → Payment. `ψ` ensures upstream services do not overwhelm downstream services, preventing queue overflow.

- **Compiler Auto-Scheduling (MLIR/LLVM):**  
  Compilers can use these constraints to automatically apply loop tiling or vectorization to restore constant gap violations, ensuring producer/consumer balance.

---

## 🧪 Python Implementation

This repository provides a full Python framework to validate these notations.

**Core Functions:**
- `validate_psi(F1, F2, g, n_range)` – Checks `(F₁, F₂) ∈ ψ(g(n))`.
- `validate_psi_big(F1, F2, F3, g, n_range)` – Checks `(F₁, F₂, F₃) ∈ Ψ(g(n))`.
- `auto_fix` – Suggests scaling factors to enforce the condition.
- `plot_bounds` – Visualizes the functions and bridging constants.

**Example:**
```python
from psi_notation import validate_psi
import math

def F1(n): return 2*n + 10
def F2(n): return 3*n - 5
def g(n): return n

print(validate_psi(F1, F2, g, n_range=(1, 1000)))  # True
```

Run Tests:

```bash
git clone https://github.com/Natarizki/psi-notation.git
cd psi-notation
python3 -m unittest discover tests/
```

---

📜 License

This project is licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0) License.
Full details: https://creativecommons.org/licenses/by-nc-nd/4.0/

---

Author: Natarizki
