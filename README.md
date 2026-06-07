# 📜 Uncovering Linguistic Patterns in Libyan Dialect Abusive Language

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Dataset Available](https://img.shields.io/badge/Dataset-Available-green.svg)](#-dataset-description)
[![Citation](https://img.shields.io/badge/Cite-This_Work-orange.svg)](#-citation)

> **Official Repository** for the paper: *"Uncovering Linguistic Patterns in Libyan Dialect Abusive Language: An Association Rule Mining Approach Using FP-Growth"*

## 📌 Overview
The proliferation of abusive language on social media presents a significant challenge for content moderation, particularly for morphologically rich and dialectally diverse languages like Arabic. This repository accompanies our research that moves beyond traditional classification methods to analyze the **compositional structure of toxic discourse** within the **Libyan Arabic dialect**.

By applying the **FP-Growth algorithm** (Frequent Pattern Mining), we uncover a "grammar of toxicity," revealing that abusive language is not a random assortment of keywords but follows predictable, compositional patterns. We successfully identified complex, multi-word rules (e.g., two-word phrases predicting a third word) with perfect confidence scores and exceptionally high lift values (up to 429.2), representing fixed idiomatic insults.

---

## 📊 Dataset Description
To foster open science and reproducibility, we are releasing the curated corpus used in this study. The dataset is specifically tailored for Arabic NLP researchers focusing on dialectal variations, toxic language detection, and pattern mining.

### 📈 Corpus Statistics
| Metric | Value | Interpretation |
| :--- | :--- | :--- |
| **Number of Documents** | 2,146 | Short, concise online comments |
| **Total Tokens** | 9,872 | Post-preprocessing vocabulary |
| **Unique Tokens (Vocabulary)** | 5,423 | High lexical richness |
| **Avg. Tokens per Document** | 4.60 | Characteristic of social media comments |
| **Type-Token Ratio (TTR)** | 0.5493 | Indicates non-repetitive, diverse vocabulary |
| **Guiraud’s R** | 54.5804 | Standardized measure confirming lexical diversity |
| **Herdan’s C** | 0.9349 | Value close to 1.0 proves highly varied linguistic patterns |

### 📁 Data Format
The dataset is provided in a structured CSV/JSON format (see `data/` directory):
```json
{
  "id": "doc_001",
  "original_text": "Original raw Arabic text from social media",
  "cleaned_text": "Preprocessed text (no URLs, digits, or punctuation)",
  "tokens": ["token1", "token2", "token3"],
  "dialect": "Libyan"
}
