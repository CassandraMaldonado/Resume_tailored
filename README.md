# 📄 Agentic Workflow for Data Science Resume Tailoring

## Overview

This project applies an agentic workflow to reshape a resume and interview prep strategy for Data Scientist positions.

## Workflow Steps

### 1. Job Description Parsing
Key role requirements from the job description are extracted, including:

- _Skills & Tools:_ Python, SQL, Pandas, Tableau, R, Spark, etc.
- _Methods:_ A/B testing, causal inference, experiment design and predictive modeling.
- _Qualifications:_ Master's or PhD in a quantitative field and years of experience.

### 2. Resume Evaluation
- Load the original resume in (`.pdf`).
- Identifies alignment and gaps between the candidate’s background and the job requirements.

### 3. Resume Reshaping
- Rewrites the professional summary to better reflect ML experimentation, LLM pipelines and business impact.
- Reorganizes experience and adds clearer, quantified outcomes.
- Groups skills into ATS friendly categories using a tag-based visual design.

### 4. Resume Rewriting & Export
- Final resume rendered as a visually clean, responsive `.html` document for readability and design consistency.

### 5. Diff-Based Comparison
- `difflib` is use to compare the original and tailored resume line-by-line, highlighting additions, deletions and edits.
- The output is saved as `resume_diff.txt` for review.

### 6. Summary of Resume Changes
- A full markdown summary of changes is included in the notebook, explaining what changed and why.

### 7. Interview Talking Points
- [✅ Placeholder] A set of 5–7 talking points were (or will be) generated to prepare for a recruiter screen or first-round interview — focusing on LLM, experimentation, business alignment, and analytics communication.

---

## ✅ Deliverables

| File | Description |
|------|-------------|
| `Tailored_Resume_CM.ipynb` | The main Colab/Notebook with the agentic workflow |
| `Cassandra_Sullivan_DataScience.pdf` | Original resume (baseline for comparison) |
| `datascience_resume_20250805_225420.html` | Tailored resume optimized for Apple Ads role |
| `resume_diff.txt` | Unified diff comparison of original vs tailored resume |
| `README.md` | This file: explanation of process and files |
| `talking_points.md` | [Pending] Interview preparation points tied to JD |
| ✅ Embedded in notebook | Summary of Resume Changes (markdown cell)

---

## 🧠 Purpose

This project demonstrates how data science principles — such as semantic matching, pipeline design, feature engineering (resume content), and output validation — can be applied to the job search process. It encourages intentional, optimized self-representation based on data and strategy rather than guesswork.

The approach mirrors what a data scientist might do for customer targeting or modeling: align the product (you) with market demand (the job), optimize, and evaluate the result.
