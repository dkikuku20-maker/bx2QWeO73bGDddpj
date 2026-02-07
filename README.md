# Candidate Ranking System (Human-in-the-Loop)

## Project Description
A Python-based system that ranks job candidates for a specific role and updates the ranking using recruiter feedback (starring a candidate).

---

## Problem Statement
Recruiters often search candidates using keywords and receive a ranked list.  
However, after manual review, the best candidate is not always ranked first.

The goal of this project is to:
- Rank candidates based on role relevance
- Update rankings when a recruiter identifies a strong candidate
- Keep the system simple, explainable, and human-guided

---

## Data Description
The dataset contains anonymized candidate information:
- `id`: unique candidate identifier  
- `job_title`: candidate job title (text)  
- `location`: geographic location  
- `connection`: number of professional connections  
- `fit`: desired output (not labeled in the dataset)

Because `fit` has no labels, a supervised prediction model cannot be trained.

---

## Approach and Methodology

### Initial Ranking
- Use role keywords (e.g., “Aspiring human resources”, “Seeking human resources”, “HR”)
- Convert job titles and keywords into numeric vectors using TF-IDF
- Compute cosine similarity to produce a relevance score
- Rank candidates by similarity score (0–1)

### Filtering
- Apply a light rule-based filter to remove clearly irrelevant technical roles
- Keep ambiguous titles to avoid excluding potential candidates

### Recruiter Feedback
- A recruiter can star a candidate they consider a strong fit
- The starred candidate is treated as an ideal reference profile

### Re-Ranking
Updated fit score:

0.8 × keyword similarity + 0.2 × similarity to starred candidate

This keeps role relevance dominant while learning from feedback.

---

## Evaluation
Because true labels are unavailable, evaluation focuses on ranking behavior:
- Average similarity of top-10 candidates to the starred profile increases after feedback
- Keyword relevance remains mostly stable after re-ranking
- More candidates similar to the starred profile appear in top results

These results indicate that ranking quality improves without overfitting.

---

## Cut-Off Strategy
- Use a Top-K approach (K = 50)
- Practical for recruiter review
- Consistent across different roles

---

## Technologies Used
- Python
- pandas
- scikit-learn
- TF-IDF
- Cosine similarity
- Jupyter Notebook

---

## How to Run
1. Clone the repository  
2. Install dependencies:

---

## Summary
This project demonstrates a human-in-the-loop candidate ranking system that:
- Uses text similarity for initial ranking
- Learns from recruiter feedback
- Improves ranking quality over time
- Remains transparent and explainable

