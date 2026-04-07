# Scoring Data Quality Audit – AI-Powered Candidate Evaluation System

## 📌 Overview
This project is a focused data quality audit of an AI-powered candidate evaluation system.

The analysis evaluates the **technical reliability, consistency, and completeness** of the AI scoring pipeline before any downstream modeling or decision-making.

The goal is to identify data inconsistencies, pipeline failures, and structural limitations that could impact the reliability of AI-generated scores.

---

## 🎯 Objectives
- Assess completeness and consistency of AI-generated scores  
- Identify pipeline failures and missing outputs  
- Evaluate scoring behavior and confidence levels  
- Detect risks affecting downstream analytics and model monitoring  

---

## 🗂️ Data Sources
The analysis is based on the following tables:
- `candidate_scores`  
- `candidate_answers`  
- `candidate_answer_score_events`  

---

## 📁 Project Structure
.
├── notebook/
│   └── scoring.ipynb - Main analysis notebook containing data extraction, exploration, and audit findings  
├── README.md - Project documentation and summary of insights

---

## 🔍 Key Insights

### 1. Score Distribution
- Scores range from **0 to 4.5** (maximum score of 5 not observed)  
- Mean ≈ 2.05, Median ≈ 2.31 → mid-range clustering  
- Core scoring field is complete (no missing values)  

However:
- ~55% of composite scores are missing  (stale data)
- Stage-level breakdowns and AI-generated summaries are inconsistently populated  

➡️ This suggests **partial pipeline execution or conditional processing gaps**

---

### 2. Pipeline Failures
- ~3.7% of records contain transcripts but no AI score  
- Missing scores align with missing confidence values  

Identified causes:
- Silent recording misclassification  
- Score wipes during pipeline re-sync  

➡️ Although these issues were fixed, **stale affected records may still persist**

---

### 3. Dimension Inconsistency
- Naming inconsistencies observed (e.g., `"experience"` vs Title Case)  
- Highly concentrated at the project level  

➡️ Indicates **configuration inconsistencies and potential aggregation issues**

---

### 4. Re-scoring Limitations
- 99.4% of scores are initial evaluations  
- Only 0.57% are re-scored  

➡️ Limits the ability to perform **drift detection and model performance monitoring over time**

---

### 5. Confidence Scores
- Only 0.06% of scores fall below 0.5 confidence  

➡️ Indicates strong model certainty, but **confidence remains largely unvalidated**

---

### 6. Missing Human Benchmarks
- No human evaluation data available  

➡️ Prevents **ground-truth validation and benchmarking of AI-generated scores**

---

## ⚠️ Key Risks

### 1. Score Distribution & Missing Outputs
- Missing composite scores (~55%) and inconsistent downstream outputs reduce reliability of aggregated metrics  
- Incomplete outputs may lead to **misleading interpretations in downstream analysis**  
- Absence of maximum scores (5) may indicate **score calibration or compression issues**  

---

### 2. Pipeline Failures
- Records with transcripts but no scores introduce **data gaps that bias analysis**  
- Alignment between missing scores and confidence suggests **single-point pipeline failure risk**  
- Persistent stale records may reduce **trust in system completeness**  

---

### 3. Dimension Inconsistency
- Inconsistent naming prevents accurate aggregation across dimensions  
- Project-level inconsistencies may lead to **incorrect feature grouping and flawed insights**  
- Downstream usage may produce **fragmented or invalid results**  

---

### 4. Re-scoring Limitations
- Lack of re-scoring prevents **model monitoring and drift detection**  
- System cannot validate score stability across updates  
- Creates risk of **silent model degradation over time**  

---

### 5. Confidence Score Over-Reliance
- High confidence without validation may indicate **model overconfidence**  
- Confidence may be misinterpreted as accuracy  
- Leads to **over-reliance on automated decisions**  

---

### 6. Missing Human Benchmarks
- No ground-truth comparison for AI outputs  
- Limits ability to assess **accuracy, fairness, and bias**  
- Reduces credibility in **high-stakes evaluation scenarios**  

---

## 💡 Recommendations
- Standardize scoring dimension naming conventions  
- Reprocess and clean stale records affected by pipeline failures  
- Validate and recompute composite scores before analysis  
- Introduce re-scoring mechanisms for model monitoring  
- Integrate human evaluation data for benchmarking  

---

## 🛠️ Tech Stack
- Python (Pandas, SQLAlchemy)  
- PostgreSQL  
- Jupyter Notebook  

---

## 🚀 Key Takeaway
This project demonstrates the importance of validating data pipelines before relying on their outputs.

Beyond identifying data issues, the audit highlights how pipeline design and data quality directly impact the reliability of AI-driven decision systems.

---

## 📎 Note
All sensitive credentials and environment variables have been excluded from this repository.
