# Scoring System & Funnel Performance Audit – VettedAI

## 📌 Overview
This project is a comprehensive data quality and system performance audit of an AI-powered candidate evaluation platform.

The analysis evaluates both:
- The **technical reliability** of the AI scoring pipeline  
- The **operational efficiency** of the candidate funnel  

The goal is to identify data inconsistencies, pipeline failures, and business-level bottlenecks that impact decision-making.

---

## 🎯 Objectives
- Assess completeness and consistency of AI-generated scores  
- Identify pipeline failures and missing outputs  
- Evaluate scoring behavior and confidence levels  
- Analyze candidate funnel performance  
- Detect risks affecting downstream analytics and model monitoring  

---

## 🗂️ Data Sources
The analysis is based on the following tables:
- `candidate_scores`  
- `candidate_answers`  
- `candidate_answer_score_events`  

---

## 🔍 Key Insights

### 1. Score Distribution
- Scores range from **0 to 4.5** (max of 5 not reached)  
- Mean ≈ 2.05, Median ≈ 2.31 → mid-range clustering  
- Core scoring field is complete (no missing values)  

However:
- ~55% of composite scores are missing  
- Downstream outputs (summaries, stage breakdowns) are inconsistent  

---

### 2. Pipeline Failures
- ~3.7% of records contain transcripts but no AI score  
- Missing scores align with missing confidence values  

Identified causes:
- Silent recording misclassification  
- Score wipes during pipeline re-sync  

---

### 3. Dimension Inconsistency
- Naming inconsistencies (e.g., `"experience"` vs Title Case)  
- Concentrated at project level  

---

### 4. Re-scoring Limitations
- 99.4% of scores are initial evaluations  
- Only 0.57% are re-scored  

➡️ Limits model monitoring and drift detection  

---

### 5. Confidence Scores
- Only 0.06% below 0.5 confidence  

➡️ High model certainty, but not sufficiently validated  

---

### 6. Missing Human Benchmarks
- No human evaluation data available  

➡️ Cannot validate AI accuracy  

---

## ⚠️ Key Risks

### 1. Score Distribution & Missing Outputs
- Missing composite scores (~55%) and inconsistent downstream outputs reduce the reliability of aggregated metrics  
- Incomplete pipeline outputs may lead to **misleading interpretations in downstream analysis and reporting**  
- The absence of maximum scores (5) may indicate **score compression or calibration issues**, affecting candidate differentiation  

---

### 2. Pipeline Failures
- Records with transcripts but no scores introduce **data gaps that bias analysis results**  
- Alignment between missing scores and confidence suggests **single-point pipeline failure risk**  
- If not remediated, these failures can reduce **trust in system reliability and completeness**  

---

### 3. Dimension Inconsistency
- Inconsistent naming prevents accurate aggregation and comparison across dimensions  
- Project-level inconsistencies may lead to **incorrect feature grouping and flawed insights**  
- Downstream models or dashboards relying on these fields may produce **invalid or fragmented results**  

---

### 4. Re-scoring Limitations
- Lack of re-scoring data prevents **drift detection and model performance tracking over time**  
- The system cannot validate whether scores remain stable across model updates  
- This creates long-term risk of **silent model degradation**  

---

### 5. Confidence Score Over-Reliance
- Extremely high confidence levels without validation may indicate **overconfidence in model outputs**  
- Without challenge mechanisms (re-scoring or human review), confidence scores may be **misinterpreted as accuracy**  
- This can lead to **over-trusting automated decisions**  

---

### 6. Missing Human Benchmarks
- Absence of human evaluation prevents **ground-truth validation of AI scoring**  
- Limits ability to assess fairness, bias, and real-world accuracy  
- Reduces credibility of the system in **high-stakes decision-making contexts**   

---

## 💡 Recommendations
- Standardize scoring dimension naming  
- Reprocess stale and affected records  
- Validate and recompute composite scores  
- Introduce re-scoring mechanisms  
- Integrate human evaluation benchmarks  
---

## 🛠️ Tech Stack
- Python (Pandas, SQLAlchemy)  
- PostgreSQL  
- Jupyter Notebook  

---

## 🚀 Key Takeaway
This project highlights the importance of combining **data quality analysis with product and system thinking**.

Beyond identifying data issues, the audit uncovers how pipeline design, user behavior, and infrastructure gaps directly impact the effectiveness of an AI-driven platform.

---

## 📎 Note
All sensitive credentials and environment variables have been excluded from this repository.