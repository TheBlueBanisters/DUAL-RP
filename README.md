# DUAL-RP: Dual Relational Path Modeling for Knowledge Graph Reasoning

📎 Supplementary materials for IJCNN 2026 camera-ready version

---

## 📖 Abstract

Knowledge graph completion (KGC) aims to infer missing relations between entities, which is essential for improving structured knowledge utilization in real-world systems.

However, existing approaches often struggle to **jointly model structural dependencies and semantic reasoning** within a unified framework.

We propose **DUAL-RP**, a relation prediction framework that bridges knowledge graph embedding (KGE) models and large language models (LLMs) through a **semantic re-ranking paradigm**.

Specifically:

- KGE models are used to generate a compact candidate set
- A **token translator** aligns structural embeddings with the LLM embedding space
- Multi-hop relational paths are incorporated as **natural-language context**

This enables effective **semantic–structural fusion** for relation prediction.

Extensive experiments on **FB15k-237, CoDEx-S, and DBpedia50** demonstrate that DUAL-RP consistently outperforms embedding-based, PLM-based, and LLM-based baselines in terms of **MRR and Hits@K**. :contentReference[oaicite:0]{index=0}

---

## 🧠 Framework Overview

<p align="center">
  <img src="figures/1.png" width="80%">
</p>

DUAL-RP follows a **coarse-to-fine pipeline**:

1. **Candidate Filtering (KGE)**  
   Reduce the relation space using structural scoring

2. **Structural Encoding**  
   Align embeddings with LLM token space via a token translator

3. **Multi-hop Semantic Expansion**  
   Inject relational paths as natural-language context

4. **Semantic–Structural Ranking (LLM)**  
   Re-rank candidates under unified contextual input

---

## 🔍 Case Study: Analysis of Key Factors

To better understand the behavior of DUAL-RP, we analyze three key factors:

- Candidate set size
- Backbone language model
- KGE method

All experiments are conducted under identical settings on:

- FB15k-237  
- CoDEx-S  
- DBpedia50  

---

### 🔹 Effect of Candidate Number

<p align="center">
  <img src="figures/C1.png" width="32%">
  <img src="figures/C2.png" width="32%">
  <img src="figures/C3.png" width="32%">
</p>

We observe that:

- Increasing candidate size from **20 → 40** consistently degrades performance  
- The drop is most significant on **CoDEx-S**  
- Larger candidate sets introduce more semantically similar relations  

Interestingly:

> The proportion of gold relations within top-k increases as candidate size grows

This indicates that:

- Performance degradation is **not caused by recall issues**
- Instead, it is due to **increased ranking difficulty**

👉 The model must distinguish between more fine-grained relations.

Overall, **25 candidates** provides the best trade-off between:

- Accuracy  
- Fairness  
- Computational cost  

---

### 🔹 Effect of Backbone Language Model

<p align="center">
  <img src="figures/B1.png" width="32%">
  <img src="figures/B2.png" width="32%">
  <img src="figures/B3.png" width="32%">
</p>

We evaluate different backbone models across scales.

Key findings:

- Performance improves from **1.5B → 7B**
- Gains saturate beyond **3B**
- **Qwen models outperform LLaMA** at similar scales  

This suggests:

- Instruction tuning improves reasoning quality  
- Larger models do not guarantee proportional gains  

👉 **Qwen2.5-3B** achieves the best balance between:

- Performance  
- Efficiency  
- Stability  

---

### 🔹 Effect of KGE Method

<p align="center">
  <img src="figures/K1.png" width="32%">
  <img src="figures/K2.png" width="32%">
  <img src="figures/K3.png" width="32%">
</p>

Different KGE methods introduce different structural biases.

We observe:

- **TransE**: simple but limited in complex patterns  
- **DistMult / ComplEx**: partially address symmetry but lack expressiveness  
- **RotatE**: consistently achieves the best performance  

This is because:

- RotatE models diverse relational patterns  
- Its geometric formulation aligns well with LLM representations  

👉 This makes it ideal for **semantic–structural fusion** in DUAL-RP  

---

## 📊 Summary

From these analyses:

- Candidate size affects **ranking difficulty**
- Backbone models influence **semantic representation quality**
- KGE methods determine **structural reasoning capability**

Together, they shape the overall effectiveness of DUAL-RP.

---

## 📌 Notes

- All experiments follow identical training and evaluation settings  
- This case study was removed from the main paper due to page limits  
- We release it here to improve transparency and completeness  

---

## 🔧 Code Availability

We are actively preparing the codebase for public release.

The full implementation, along with training and evaluation details, will be made available in this repository in the near future.
