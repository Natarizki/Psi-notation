# The Psi (ψ) Notation for Ordered Complexity Classes

[![Status](https://img.shields.io/badge/status-active-brightgreen)](https://github.com/Natarizki/psi-notation)
[![Version](https://img.shields.io/badge/version-1.0-blue)](https://github.com/Natarizki/psi-notation)
[![Made with LaTeX](https://img.shields.io/badge/Made%20with-LaTeX-008080?logo=latex)](https://www.latex-project.org/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-black?logo=github)](https://github.com/Natarizki)

> **A novel asymptotic notation for guaranteeing ordering constraints in two-tier computational architectures.**

## 📜 Introduction
Classical notations (`O`, `Ω`, `Θ`) describe the *growth rate* of a single function. However, in modern system architectures (e.g., AI pipelines, caching layers), we require a **structural guarantee** that an upstream layer ($F_1$) will never exceed a downstream layer ($F_2$).

The **ψ (Psi) notation** fills this gap by providing a formal mathematical framework for *ordered asymptotic bounds*.

## 📐 Formal Definition
Let $F_1, F_2: \mathbb{N} \to \mathbb{R}^+$ be a pair of non-negative functions. The ordered pair $(F_1, F_2)$ belongs to the complexity class $\psi(g(n))$ if there exist positive constants $c_1, c_2, c_3$ such that for all sufficiently large $n$:

$$
c_1 \cdot g(n) \;\le\; F_1(n) \;\le\; c_2 \cdot g(n) \;\le\; F_2(n) \;\le\; c_3 \cdot g(n)
$$

The core idea is the **"Bridge Inequality"** at $c_2 \cdot g(n)$, ensuring that $F_1$ is strictly bounded above by $F_2$.

## 🧩 Complexity Classes
| Notation | Growth Rate | Ideal Application |
| :--- | :--- | :--- |
| $\psi(1)$ | Constant | Real-time systems with absolute latency guarantees |
| $\psi(\log N)$ | Logarithmic | Binary Search & Divide-and-Conquer algorithms |
| $\psi(N)$ | Linear | Simple data streaming and ETL pipelines |
| $\psi(N \log N)$ | Log-Linear | Sorting algorithms (Merge Sort, Quick Sort) |
| $\psi(N^2)$ | Quadratic | Nested-loop algorithms and certain DP approaches |

## 🎯 Motivation
This notation was designed to solve a practical problem in **two-tier systems** like *Retrieval-Augmented Generation (RAG)* or *Microservices*:

> *"How do we mathematically guarantee that the retriever (F₁) doesn't flood the generator (F₂) with more requests than it can handle?"*

$\psi$ provides a rigorous proof that $F_1 \le F_2$ asymptotically, preventing system overload without relying on heuristic thresholds.

## 📂 Repository Structure
```

.
├── ψ.pdf              # Formal paper defining the Psi notation (2 pages)
├── ψ.md               # Quick reference guide
└── README.md          # This landing page

```

## 📝 Citation
If you use this notation in your research or projects, please cite it as:

```bibtex
@misc{haynar2026psi,
  author       = {Muhammad Nata Rizki Haynar},
  title        = {The Psi (ψ) Notation for Ordered Complexity Classes},
  year         = {2026},
  howpublished = {\url{https://github.com/Natarizki/psi-notation}}
}
```

👤 Author

Muhammad Nata Rizki Haynar
[![github profile](https://img.shields.io/badge/GitHub-Profile-black?logo=githu)](https://github.com/Natarizki)

"Bridging complexity analysis with real-world system architecture."
