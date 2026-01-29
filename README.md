# Candidate Ranking System (Human-in-the-Loop)

## Overview
This project builds a simple and explainable system to **rank job candidates for a specific role** and **update the ranking based on recruiter feedback**.

The goal is not to replace recruiters, but to support decision-making by allowing human judgment to improve ranking quality over time.

---

## Problem Statement
Recruiters often search candidates using keywords and receive a ranked list.  
However, after manual review, the best candidate is not always ranked first.

This project explores:
- How to rank candidates using available text data
- How recruiter feedback (starring a candidate) can improve future rankings
- How to do this in a transparent and low-risk way

---

## Data Description
Each candidate record includes:
- `id` – unique candidate identifier  
- `job_title` – candidate job title (text)  
- `location` – geographic location  
- `connection` – number of professional connections  
- `fit` – desired output (not provided in the dataset)

⚠️ The `fit` column has no labels, so a supervised prediction model cannot be trained.  
Instead, a **fit score** is created using text similarity and recruiter feedback.

---

## Approach

### Initial Ranking
- Candidate job titles are compared to role keywords:
  - “Aspiring human resources”
  - “Seeking human resources”
  - “HR”
- TF-IDF and cosine similarity are used to compute a relevance score
- Candidates are ranked by similarity score (0–1)

---

### Light Filtering
- Obvious non-HR technical roles (e.g., software engineers) are removed
- Ambiguous titles are kept to avoid excluding strong candidates

---

### Recruiter Feedback (⭐)
- A recruiter can star a candidate they consider a strong fit
- The starred candidate is treated as an ideal reference profile

---

### Re-Ranking After Feedback
The updated fit score is computed as:
80% keyword relevance

20% similarity to the starred candidate

This keeps role relevance as the main signal while allowing feedback to guide the ranking.

---

## Evaluation Strategy
Because true labels are not available, evaluation focuses on ranking behavior:
- Average similarity of top-10 candidates to the starred profile increases
- Keyword relevance remains mostly stable after re-ranking
- More candidates similar to the starred profile appear in the top results

These results show that the ranking improves after feedback without overfitting.

---

## Cut-Off Strategy
- A Top-K approach is used (K = 50)
- This size is practical for recruiter review
- It works consistently across different roles without hiding strong candidates

---

## Bias Considerations
- Recruiter feedback is used as a soft signal (20% weight)
- Humans remain in control of decisions
- No sensitive personal attributes are used
- Feedback influence is capped to reduce bias amplification

---

## Technologies Used
- Python  
- pandas  
- scikit-learn  
- TF-IDF  
- Cosine similarity  
- Jupyter Notebook  

---



## Summary
This project demonstrates a **human-in-the-loop candidate ranking system** that:
- Ranks candidates using text similarity
- Learns from recruiter feedback
- Improves ranking quality over time
- Remains simple, transparent, and explainable

