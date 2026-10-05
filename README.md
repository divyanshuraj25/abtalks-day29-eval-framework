# ⚖️ Automated LLM-as-a-Judge Evaluation & Regression Suite

An automated AI evaluation and measurement framework built with Python and the Google Gemini API (`gemini-3.8-flash`). This framework implements an **LLM-as-a-Judge** pipeline to objectively benchmark knowledge assistant outputs across multi-dimensional rubrics and execute automated regression gates prior to production deployment.

---

## 📌 Overview

Automated evaluation systems that objectively score an AI system's outputs are critical production engineering components. This project establishes an automated pre-deployment testing pipeline that eliminates gut-feel assessments and relies on deterministic scoring.

### Evaluation Dimensions & Rubric
- **Groundedness (1–5)**: Ensures answers are strictly grounded in retrieved context without fabricated additions or hallucinations.
- **Correctness (1–5)**: Evaluates factual alignment with manually curated ground truth answers.
- **Completeness (1–5)**: Measures whether all essential aspects of the user query have been addressed without critical omissions.

---

## 🚀 Key Features

- **Pydantic Schema Validation**: Structured JSON outputs with strict typing and reasoning directly from Gemini API.
- **Exponential Backoff & Resilience**: Built-in retry handling for rate limits and server availability.
- **20-Question Curated Benchmark**: Custom labeled dataset covering core AI/ML, FAISS, and RAG concepts.
- **Automated Regression Gate**: Compares evaluation aggregates against historical baselines and triggers `PASS` / `FAIL` based on tolerance thresholds.

---

## 📊 Benchmark & Regression Results

Evaluated across a 20-question labeled evaluation suite:

| Dimension | Baseline Score | Achieved Score | Threshold Delta | Test Status |
| :--- | :---: | :---: | :---: | :---: |
| **Groundedness** | 4.50 / 5.0 | **4.95 / 5.0** | +0.45 | ✅ PASS |
| **Correctness** | 4.50 / 5.0 | **5.00 / 5.0** | +0.50 | ✅ PASS |
| **Completeness** | 4.00 / 5.0 | **4.35 / 5.0** | +0.35 | ✅ PASS |

> **Final CI/CD Regression Status**: **`PASS`** (All metrics met minimum acceptance criteria).

---

## 📂 Project Structure

├── notebook/
│   └── llm_as_a_judge_evaluation.ipynb   # Complete execution notebook
├── data/
│   └── dataset.json                      # 20-question labeled benchmark suite
├── src/
│   ├── judge.py                          # LLM judge logic & Pydantic schema
│   └── regression_runner.py              # Test suite & gate threshold evaluation
├── README.md
└── requirements.txt


---

## ⚙️ Installation & Usage

### 1. Install Dependencies
```bash
pip install google-genai pydantic
2. Configure Environment
Set your Gemini API key:

Bash
export GEMINI_API_KEY="your-api-key"
3. Run Evaluation
Python
from google import genai
from pydantic import BaseModel, Field

# Define schema and invoke llm_judge()
score = llm_judge(
    question="What is RAG?",
    context="Retrieval-Augmented Generation merges external retrieval with LLMs.",
    answer="RAG combines document retrieval with generative models.",
    ground_truth="Retrieval-Augmented Generation combines retrieval with LLMs to prevent hallucinations."
)
print(score)
⚠️ Limitations of LLM-as-a-Judge
While LLM-as-a-judge provides scalable evaluation, several structural limitations exist:

Verbosity Bias: Models naturally favor longer, highly structured answers over concise factual answers.

Alignment & Self-Preference: Evaluators can favor stylistic conventions characteristic of their underlying model family.

Multi-Hop Blindspots: Mathematical derivations and complex chronological facts can lead the judge LLM to hallucinate.

Need for Human Audits: High-stakes production systems still require human-in-the-loop sampling for legal, medical, and safety boundaries.

🛠️ Tech Stack
Model Engine: Google Gemini (gemini-3.8-flash)

Validation: Pydantic v2

Language: Python 3.10+


---

### 2. Professional LinkedIn Post / Description

> **"You cannot improve what you cannot measure."** 📊
>
> In production AI engineering, automated evaluation systems are what separate teams that iterate based on empirical data from teams that rely on gut feel.
>
> As part of the **#60DaysOfAI Challenge (Day 29)**, I built an automated **LLM-as-a-Judge Evaluation & Regression Testing Framework** using Python and the Google Gemini API (`gemini-3.8-flash`).
>
> ### 🔍 What I Built:
> 1. **Multi-Dimensional Evaluation Rubric**: Built a structured judge framework measuring **Groundedness**, **Factual Correctness**, and **Completeness** on a 1–5 scale.
> 2. **Pydantic Validation**: Enforced deterministic JSON schemas for reproducible metric outputs and transparent scoring rationales.
> 3. **Curated 20-Question Benchmark**: Designed a labeled evaluation dataset with strict ground truths spanning ML, vector databases (FAISS), and RAG architectures.
> 4. **Automated Regression Gate**: Implemented a `regression_test_runner()` function that compares current release scores against established baselines to gate deployments (`PASS`/`FAIL`).
> 5. **Built-in Resilience**: Handled traffic spikes and rate limits with exponential backoff and multi-model fallbacks.
>
> ### 📈 Key Results:
> - **Groundedness**: 4.95 / 5.0 (Base: 4.50) — ✅ PASS
> - **Correctness**: 5.00 / 5.0 (Base: 4.50) — ✅ PASS
> - **Completeness**: 4.35 / 5.0 (Base: 4.00) — ✅ PASS
> - **Final Suite Status**: **`PASS`**
>
> Building this highlighted both the scalability of automated evaluation and the importance of addressing biases like verbosity, position alignment, and the continued necessity of human spot-audits.
>
> 🔗 Code & Notebook: [Insert your GitHub Repo or Colab Link]
>
> #GenerativeAI #LLMOps #AIEvaluation #GeminiAPI #Python #MachineLearning #RAG #AIProductQua
