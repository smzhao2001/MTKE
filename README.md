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
```

### 1.3 Data format

The datasets are saved as a **list of dicts / JSON objects**, where each object corresponds to one temporal editing case for a fixed `(subject, relation)` pair.

A schematic example of one instance is:

```jsonc
{
  "case_id": 1,
  "setting": "SG",        // "SG" for single granularity, "DG" for dual/multi granularity

  "meta": {
    "subject": "USA",
    "relation": "President_of",
    "relation_id": "<rel_id>",
    "granularity_true": "year",   // granularity of historical fact
    "granularity_new": "year"     // or "month"/"day" for the updated fact
  },

  "background": {
    "fact_chain": [
      {
        "object": "Donald Trump",
        "since": "2017-01-20",
        "until": "2021-01-20"
      },
      {
        "object": "Joseph Biden",
        "since": "2021-01-20",
        "until": "2025-01-20"
      },
      {
        "object": "Donald Trump",
        "since": "2025-01-20",
        "until": null
      }
    ]
  },

  "edit": {
    "target_true":  { "str": "Joseph Biden",  "id": "<old_obj_id>" },
    "target_new":   { "str": "Donald Trump",  "id": "<new_obj_id>" },

    "time_true": {
      "since": "2021",
      "until": "2025",
      "granularity": "year"
    },

    "time_new": {
      "since": "2025",
      "until": null,
      "granularity": "year"       // can be "day" in DG
    }
  },

  "evaluation": {
    "current": {
      "completion": "The president of the USA is",
      "questions": "Who is the president of the USA?",
      "time_completion": "From 2025 to now, the president of the USA is",
      "time_questions": "Who is the president of the USA in 2025?",
      "paraphrases": [
        "During 2025, the USA's president is",
        "The person serving as president of the United States in 2025 is"
      ]
    },

    "history": {
      "completion": "From 2021 to 2025, the president of the USA was",
      "questions": "Who was the president of the USA from 2021 to 2025?",
      "time_completion": "From 2021 to 2025, the individual holding the office of president of the USA was",
      "time_questions": "Who served as president of the United States between 2021 and 2025?",
      "paraphrases": [
        "During the period 2021–2025, the president of the USA was"
      ]
    }
  },

  "answers": {
    "answer_history":       [["Joseph Biden"], ["Biden"]],
    "answer_history_alias": [["Joseph R. Biden", "Joe Biden"]],

    "answer_current":       [["Donald Trump"]],
    "answer_current_alias": [["Donald J. Trump", "Trump"]]
  }
}
```

## 2. Issues or Questions?

If you encounter any issues while using MTKE (SG/DG) or have questions about the benchmark, please feel free to:

- Open a GitHub **issue** in this repository.

---

## 3. Citation

If you use MTKE in your research, please cite:

```bibtex

```




