# 🎯 Agentic Workflow for Resume Tailoring: Apple Ads – Data Scientist Role

## 📌 Overview

This project applies a structured, agentic workflow to reshape a resume and interview prep strategy for the **Data Scientist, Research Analytics** position at **Apple Ads**.

The process mirrors a real-world data science pipeline: from data ingestion (JD + resume), through matching and transformation (resume tailoring), to evaluation (diff comparison), and delivery (HTML output and talking points).

---

## 🚀 Workflow Steps

### 1. Job Description Parsing
Key role requirements from Apple’s JD were extracted, including:

- **Skills & Tools**: Python, SQL, Pandas, Tableau, R, Spark
- **Methods**: A/B testing, causal inference, experiment design, predictive modeling
- **Qualifications**: Master's or PhD in a quantitative field, 3+ years of experience

### 2. Resume Ingestion & Evaluation
- Loaded the **original resume** (`.pdf`) using `PyMuPDF` and the **tailored version** (`.html`) via `BeautifulSoup`.
- Identified alignment and gaps between candidate’s background and job requirements.

### 3. Resume Reshaping
- Rewrote professional summary to better reflect ML experimentation, LLM pipelines, and business impact.
- Reorganized experience and added clearer, quantified outcomes.
- Grouped skills into ATS-friendly categories using a tag-based visual design.

### 4. Resume Rewriting & Export
- Final resume rendered as a visually clean, responsive `.html` document using CSS styling for readability and design consistency.

### 5. Diff-Based Comparison
- `difflib` was used to compare the original and tailored resume line-by-line, highlighting additions, deletions, and edits.
- Output saved as `resume_diff.txt` for review.

### 6. Summary of Resume Changes
- A full markdown summary of changes was included in the notebook, explaining what changed and why.

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
