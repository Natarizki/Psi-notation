# The Psi (ψ) Notation - Ordered Complexity Classes

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

## 📜 Description
This repository contains the formal definition of the **ψ (Psi) notation**, a novel notation in algorithmic complexity and system architecture analysis. 

Unlike classical notations (`O`, `Ω`, `Θ`) that analyze the growth of a *single* function, the **ψ** notation is specifically designed to analyze **ordered pairs of sequential functions** \((F_1, F_2)\), providing a mathematical guarantee that \(F_1\) will never asymptotically exceed \(F_2\).

## 📐 Formal Definition
A pair of functions \((F_1, F_2)\) is said to belong to the complexity class \(\psi(g(n))\) if there exist positive constants \(c_1, c_2, c_3\) such that for all sufficiently large \(n\):

\[
c_1 \cdot g(n) \le F_1(n) \le c_2 \cdot g(n) \le F_2(n) \le c_3 \cdot g(n)
\]

## 🧩 Supported Special Cases
| Notation | Complexity | Ideal Application |
| :--- | :--- | :--- |
| \(\psi(1)\) | Constant | Real-time systems with absolute latency guarantees |
| \(\psi(\log N)\) | Logarithmic | Binary Search & Divide-and-Conquer algorithms |
| \(\psi(N)\) | Linear | Simple data pipelines |
| \(\psi(N \log N)\) | Log-Linear | Sorting & Merge operations |
| \(\psi(N^2)\) | Quadratic | Nested-loop algorithms (e.g., certain AI models) |

## 🎯 Motivation
This notation was born out of the need to guarantee load balancing in **two-tier architectures**, such as *cache-to-database* systems or *retriever-to-generative* models (RAG). Formally, \(\psi\) ensures that the **upstream** layer (front-end) will never overload the **downstream** layer (back-end).

## 📂 Repository Contents
- **`ψ.pdf`** : Formal paper defining the Psi notation (2 pages).
- **`ψ.md`** : Concise definition notes in Markdown format.
- **`README.md`** : This landing page.

## 👤 Author
**Muhammad Nata Rizki Haynar**  
*(Add your LinkedIn, GitHub profile, or university affiliation here)*

## 📄 License
This work is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt it for research purposes, provided you give appropriate credit to the original author.

---
*"Bridging complexity analysis with real-world system architecture."*
