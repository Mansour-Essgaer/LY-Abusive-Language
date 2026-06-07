

# 📜 Uncovering Linguistic Patterns in Libyan Dialect Abusive Language
### A Benchmark Dataset and Association Rule Mining Approach

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Dataset Available](https://img.shields.io/badge/Dataset-Available-green.svg)](#-dataset-statistics)
[![Citation](https://img.shields.io/badge/Cite-This_Work-orange.svg)](#-citation)

> **Official Repository** for the paper: *"Uncovering Linguistic Patterns in Libyan Dialect Abusive Language: An Association Rule Mining Approach Using FP-Growth"*

## 📌 Overview
The proliferation of abusive language on social media presents a significant challenge for content moderation, particularly for morphologically rich and dialectally diverse languages like Arabic. This repository provides a specialized, curated corpus of **Libyan Arabic dialect** abusive texts. 

Moving beyond traditional keyword-based filtering and supervised classification, this dataset is designed to analyze the **compositional structure of toxic discourse**. By applying the **FP-Growth algorithm**, we establish a baseline "grammar of toxicity," revealing that abusive language follows predictable, multi-word compositional patterns rather than random keyword assortments. This repository provides the dataset, preprocessing pipeline, and baseline pattern mining results to ensure reproducibility and foster advanced Arabic NLP research.

---

## 📊 Dataset Statistics
| Attribute | Value | Interpretation |
| :--- | :--- | :--- |
| **Total Documents** | 2,146 | Short, concise online comments |
| **Total Tokens** | 9,872 | Post-preprocessing vocabulary |
| **Unique Tokens (Vocabulary)** | 5,423 | High lexical richness |
| **Average Tokens per Document** | 4.60 | Characteristic of social media comments |
| **Average Word Length** | 5.10 chars | Standard for Arabic tokenization |
| **Language** | Libyan Arabic Dialect | Under-resourced Maghrebi variant |
| **Domain** | Abusive Language / Toxic Discourse | Sourced from Facebook comments |
| **Type-Token Ratio (TTR)** | 0.5493 | Indicates non-repetitive, diverse vocabulary |
| **Guiraud’s R** | 54.5804 | Standardized measure confirming lexical diversity |
| **Herdan’s C** | 0.9349 | Value close to 1.0 proves highly varied linguistic patterns |

---

## 📁 Data Format
The dataset is provided in CSV format with the following structure to support both text classification and unsupervised pattern mining tasks:

- `doc_id`: Unique identifier for the comment.
- `raw_text`: Original user comment in Libyan Arabic.
- `cleaned_text`: Text after normalization, stop-word removal, and noise filtering.
- `tokens`: JSON-formatted list of unigram tokens used for transaction mining.

### Example Data
| doc_id | raw_text | cleaned_text | tokens |
| :--- | :--- | :--- | :--- |
| `001` | "يا كلب يا حقير الدولة" | "كلب حقير دولة" | `["كلب", "حقير", "دولة"]` |
| `002` | "زمن خزي وعفن" | "زمن خزي عفن" | `["زمن", "خزي", "عفن"]` |

---

## 🧾 Data Collection & Preprocessing Pipeline
To ensure high linguistic validity and prepare the text for rigorous pattern mining, the following step-by-step procedure was applied:

1. **Filtration & Cleaning**: Regex-based removal of non-lexical elements, including URLs, numerical digits, and punctuation marks.
2. **Dialectal Stop Word Removal**: A two-layer approach. First, a standard NLTK Arabic stop word list was applied. Second, this was augmented with a **custom dictionary of 973 Libyan dialect words** (e.g., pronouns, prepositions, and common fillers like 'كحور', 'شقد', 'هابي') to achieve thorough semantic cleansing.
3. **Normalization**: Standardization of whitespace and removal of any documents that became empty after the cleaning process.
4. **Feature Engineering (Unigram Generation)**: Each document $D$ was tokenized into a set of terms, creating a transaction $T = \{t_1, t_2, ..., t_k\}$, transforming the corpus into a transactional database suitable for FP-Growth.

---
### Simple Associations (1 $\rightarrow$ 1)
*Foundational pairings acting as the "subject-predicate" grammar of insults.*

| Antecedents ($X$) | Consequents ($Y$) | Confidence | Lift |
| :--- | :--- | :--- | :--- |
| `{'الحقراء'}` | `{'دولة'}` | 0.80 | 190.76 |
| `{'وطط'}` | `{'سلطانة'}` | 0.40 | 143.07 |
| `{'المجاري'}` | `{'كان م'}` | 0.40 | 122.63 |
| `{'كديس'}` | `{'الناتو'}` | 0.40 | 107.30 |

### Complex Phrasing (2 $\rightarrow$ 1)
*Fixed idiomatic expressions that function as a single semantic unit, invisible to single-word keyword filters.*

| Antecedents ($X$) | Consequents ($Y$) | Confidence | Lift |
| :--- | :--- | :--- | :--- |
| `{'خزي', 'عفن'}` | `{'زمن'}` | **1.00** | **429.20** |
| `{'الشلال', 'الزيط'}` | `{'الخمرة'}` | **1.00** | 357.67 |
| `{'مقعت', 'رايتها'}` | `{'رايتها'}` | **1.00** | 306.57 |
| `{'بغل', 'تشاد'}` | `{'رمص'}` | 0.67 | 286.13 |

*(Note: A lift of 429.20 with 1.00 confidence indicates that every time "خزي" and "عفن" appear together, "زمن" is also present, representing a deeply embedded, fixed linguistic pattern used for condemnation.)*

---

## 🎯 Intended Use
This dataset and repository are designed for:
- **Unsupervised Pattern Mining**: Benchmarking frequent itemset and association rule algorithms in morphologically rich languages.
- **Context-Aware Moderation**: Developing systems that detect multi-word idiomatic insults rather than relying on simple keyword blacklists.
- **Arabic Dialect NLP**: Serving as a foundational resource for the highly under-resourced Libyan and broader Maghrebi dialects.
- **Hybrid Deep Learning**: Using the extracted high-lift rules as attention masks or feature injectors for transformer-based models (e.g., AraBERT, CAMeLBERT) to improve context-aware classification.

---

## ⚠️ Limitations
- **One-Class Corpus**: The dataset consists exclusively of abusive texts. Researchers aiming to train binary or multi-class classifiers will need to pair this with a separate corpus of benign/neutral Libyan dialect text.
- **Source-Specific**: Collected primarily from Facebook comments, which may not fully represent the linguistic nuances, slang, or toxicity patterns of other platforms (e.g., Twitter/X, TikTok).
- **Scale Constraints**: At 2,146 documents, the dataset is highly optimized for Association Rule Mining and linguistic analysis, but may be too small for pre-training large language models (LLMs) from scratch.
- **Dialectal Focus**: Strictly focused on the Libyan dialect. Orthographic inconsistencies inherent to informal Arabic social media text (e.g., character repetition, missing diacritics) are preserved in the `raw_text` column to maintain real-world authenticity.

---

## 📚 Citation
If you use this dataset, code, or methodology in your research, please cite our paper:

```bibtex
@inproceedings{safour2024uncovering,
  title={Uncovering Linguistic Patterns in Libyan Dialect Abusive Language: An Association Rule Mining Approach Using FP-Growth},
  author={Safour, Hana and Essgaer, Mansour and Asharef, Mona and Agaal, Asma},
  booktitle={Proceedings of the Conference on Sciences and Advanced Technology},
  year={2024},
  organization={IEEE},
  address={Sebha, Libya}
}
```

---

## 📄 License
This dataset is released under the **Creative Commons Attribution 4.0 (CC BY 4.0)** license. You are free to use, share, and adapt the data with proper attribution. 

> ⚠️ **Ethical Disclaimer**: This dataset contains offensive and abusive language. It is provided strictly for academic research, computational linguistics, and the development of content moderation systems. Please handle the data responsibly and in accordance with your institution's ethical guidelines.
