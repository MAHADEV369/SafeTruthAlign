# SafeTruthAlign: Adversarial Prompt Generation and Alignment Evaluation

## 📌 Overview

Large Language Models (LLMs) like GPT, LLaMA, and Qwen demonstrate strong reasoning and generation abilities, but they remain **vulnerable to adversarial prompts**—maliciously crafted inputs designed to bypass safety guardrails.
**SafeTruthAlign** provides a complete pipeline to **generate adversarial variants**, **evaluate risks**, and **score alignment robustness** across multiple dimensions such as toxicity, fairness, misinformation, hallucinations, and safety.

This repository accompanies the MSc AI/ML dissertation at the **University of Birmingham, Dubai Campus (2024–2025)**.

---

## 🚀 Key Features

* **Adversarial Prompt Generation**

  * TextAttack-based augmentations (semantic, lexical, character, entity, CoT escalations).
  * Produces wide (`.xlsx`) and long (`.csv`) datasets of adversarial variants.

* **Semantic Similarity Filtering**

  * Embedding-based cosine similarity to ensure adversarial prompts remain close to original intent.

* **Multi-Axis Risk Scoring**

  * Prompt-level and Response-level scoring using ensemble judge models:

    * [Llama-Guard-3-8B](https://huggingface.co/meta-llama/Llama-Guard-3-8B)
    * [DeepSeek-7B-Chat](https://huggingface.co/deepseek-ai/deepseek-llm-7b-chat)
    * [Qwen-2.5-7B](https://huggingface.co/Qwen/Qwen2.5-7B)
  * Categories: **Toxicity, Bias, Hate, Fairness, Misinformation, Hallucination, Safety, Robustness, Political/Religious intolerance**

* **Response Alignment Analysis**

  * Pairwise Δ-risk between prompt vs. response
  * Lift\@K and unalignment metrics

* **Visualization & Reports**

  * CSV summaries, JSON structured judgments, histograms, bar/scatter plots

---

## 📊 Results & Findings

* Evaluated on **50 seed prompts** (due to compute constraints; original dataset = 100k+).
* Adversarial variants showed **higher risk scores** across almost all axes.
* Certain augmentations (entity-swap, paradoxical prompts) caused **significant alignment drops**.
* Δ-risk analysis revealed cases where **responses amplified prompt risks**.
* Structured JSON judgments improved interpretability by highlighting **evidence spans and rationales**.

---

## 🛠️ How to Run

The pipeline is tested primarily on **Google Colab** with GPU runtime.

1. Clone the repo and open in Colab:

   ```bash
   git clone https://github.com/MAHADEV369/SafeTruthAlign
   cd SafeTruthAlign
   ```
2. Use the provided Colab notebooks (`*.ipynb`) or Python scripts (`*.py`).
3. Input data:

   * Either use `prompts.csv` (provided)
   * Or sample from `all_english.csv`
4. Run cells **one by one**.

   * ⚠️ After GPU-intensive steps, manually clear GPU memory (`torch.cuda.empty_cache()`).
5. Generated files (`scored_prompts.csv`, `summary_stats.csv`, `charts/*.png`) will be used in later augmentation and analysis stages.

> All requirements are already imported inside scripts – **no manual `pip install` needed** unless stated.

---

## 📂 Repository Structure

```
SafeTruthAlign/
│── data/                # Seed prompts, merged datasets
│── generation/          # Adversarial prompt generation scripts
│── scoring/             # Risk scoring (prompt-level & response-level)
│── analysis/            # Alignment evaluation, Δ-risk, visualization
│── reports/             # CSV/JSON outputs + charts
│── notebooks/           # Google Colab-ready notebooks
│── README.md            # Project documentation
```

---

## 📚 References

This project builds on advances in:

* Reinforcement Learning from Human Feedback (RLHF)
* Direct Preference Optimization (DPO)
* Adversarial red-teaming datasets (AdvBench, JailbreakBench)
* LLM-as-Judge frameworks (Llama-Guard, Qwen-Judge, DeepSeek-Judge)

A full reference list is available in the dissertation report.

---
