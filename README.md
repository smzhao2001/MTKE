# MTKE

This repository contains the datasets for the paper:

> **Multi-granularity Temporal Knowledge Editing over Large Language Models**  
> Simiao Zhao, Ning Pang, Zhen Tan, Yanli Hu, Weidong Xiao, Xiang Zhao

MTKE is a benchmark for **Temporal Knowledge Editing (TKE)** in Large Language Models, with a focus on **multi-granularity temporal reasoning**. It aims to evaluate whether models can integrate new temporal facts while preserving historical knowledge across different time granularities (year / month / day).

---

## 1. Datasets

### 1.1 Overview

MTKE is constructed from real-world temporal knowledge bases (e.g., GDELT, ICEWS, YAGO), and organized as **temporal fact chains** for a fixed subject–relation pair. Each chain records how the corresponding fact evolves over time.

- Total chains: **17,060**
- Temporal granularities: **year**, **month**, **day**
- Relation types: **44** relation types with a more balanced distribution
- Each instance is a **temporal knowledge editing case**, containing:
  - A *historical* fact (before editing)
  - A *target* updated fact (after editing)
  - Explicit temporal intervals for both
  - Question templates (current vs. historical, relative vs. explicit time)
  - Gold answers and alias sets

We provide two sub-datasets:

- **MTKE-SG (Single Granularity)**  
  Historical and updated facts share the **same** temporal granularity (e.g., year→year, month→month). This setting evaluates whether a model can perform consistent edits when temporal granularity is fixed.

- **MTKE-MG (Multiple Granularities)**  
  Historical and updated facts are annotated at **different** granularities (e.g., year→day). This setting evaluates whether a model can integrate and reason across different temporal granularities.

If your repository uses short names like `SG` and `DG` in file names, you can regard:

- `SG` ↔ **MTKE-SG** (single-granularity)
- `DG` ↔ **MTKE-MG** (dual / multi-granularity)

### 1.2 Files

We assume the datasets are placed under the `datasets/` directory. A typical structure is:

```text
MTKE/
├─ datasets/
│  ├─ MTKE-SG.json      # Single-granularity temporal editing benchmark
│  ├─ MTKE-MG.json      # Multi-granularity temporal editing benchmark (a.k.a. DG)
│  └─ README_datasets.md (optional)
└─ README.md
