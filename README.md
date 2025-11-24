# 📐 OpenMath-Difficulty-Annotated

![License](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)
![Task](https://img.shields.io/badge/Task-Mathematical_Reasoning-blue)
![Format](https://img.shields.io/badge/Format-JSONL-orange)
![Size](https://img.shields.io/badge/Size-10k_Samples-brightgreen)
![Verifier](https://img.shields.io/badge/Judge-GPT--OSS--120B-purple)

## 🚀 Overview

**OpenMath-Difficulty-Annotated** is a curated dataset of **10,176 high-quality mathematical reasoning problems**, derived from NVIDIA's *OpenMathInstruct-2*.

Unlike raw datasets, every sample in this repository has been **analyzed by a 120B Parameter "Judge" Model** to assign a precise **Difficulty Level (1–5)**.

This dataset is specifically designed to help developers train **Small Language Models (SLMs)** like Granite, Llama-3.2 (1B/3B), or Qwen2.5-Math by allowing them to filter out "Olympiad-level" noise and focus on attainable logic.

---

## 📂 File Information
The repository contains a single, ready-to-use file:
- **File:** `openmath_difficulty_clean.jsonl`
- **Format:** JSON Lines
- **Content:** Math problems, LaTeX solutions, Final answers, and Difficulty metadata.

---

## 📊 Difficulty Levels (The "Judge" Metrics)

The core value of this dataset is the `difficulty` field. It allows you to split the data based on your model's capacity.

| Level | Difficulty Description | Count | Recommended for |
| :--- | :--- | :--- | :--- |
| **1** | **Very Easy** (Arithmetic & Logic) | 1,597 | Mobile Models (0.5B+) |
| **2** | **Easy** (Algebra & Geometry Basics) | 4,814 | **Granite / Llama 1B** |
| **3** | **Medium** (High School Standard) | 2,912 | **Granite / Llama 3B** |
| **4** | **Hard** (Competition Math) | 816 | Mid-sized Models (7B+) |
| **5** | **Expert** (Olympiad Level) | 39 | Large Models (70B+) |

> **💡 Pro Tip:** If fine-tuning a 1B model, we strongly recommend filtering for `difficulty <= 3`.

---

## 🧠 Data Structure

Each line in the `.jsonl` file is a JSON object with the following fields:

| Field | Type | Description |
| :--- | :--- | :--- |
| `problem` | `str` | The math statement (contains LaTeX `$..$`). |
| `generated_solution` | `str` | Step-by-step reasoning (Source: NVIDIA OpenMath). |
| `expected_answer` | `str` | The normalized final answer. |
| `difficulty` | `int` | **[NEW]** The complexity score (1-5) assigned by the Judge. |
| `subject` | `str` | Domain (e.g., Algebra, Probability, Geometry). |
| `problem_source` | `str` | Original subset (e.g., `augmented_math`). |

### Sample Entry
```json
{
  "problem": "Solve for y: $\\frac{y^2 - 3y + 2}{y - 2} = y + 1$",
  "generated_solution": "Start by multiplying both sides by $y - 2$ to eliminate the denominator...\n\\[ y = \\boxed{2
