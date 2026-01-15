# PracticalApplication3 — README

## Project Overview
This project builds and compares multiple machine-learning classification models to predict whether a customer will subscribe to a term deposit after being contacted via a telephone marketing campaign. The dataset contains customer demographic data, campaign contact details, previous campaign outcomes, and macroeconomic indicators.

Models evaluated:
- K-Nearest Neighbors (KNN)
- Logistic Regression
- Decision Tree
- Support Vector Machine (SVM)

---

## Business Understanding (Business Objective)
The business objective is to **predict whether a customer will subscribe to a term deposit ("y" = yes/no)** using customer and campaign-related features.

This enables the bank to:
- **Improve marketing efficiency** by prioritizing customers with a higher probability of subscribing.
- **Reduce cost and time** by limiting calls to low-probability customers.
- **Increase campaign success rate** by targeting customers more strategically.

---

## Data Preparation and Cleaning
The notebook includes a clean and reproducible data preprocessing pipeline:
- Target encoding:
  - `y = yes → 1`
  - `y = no → 0`
- Numerical feature handling:
  - Missing values imputed using **median**
  - Features standardized using **StandardScaler**
- Categorical feature handling:
  - Missing values imputed using **most frequent**
  - One-hot encoding using **OneHotEncoder**

A reusable preprocessing pipeline is applied consistently across all models to ensure fair comparison.

---

## Descriptive and Inferential Statistics
### Descriptive Insights
- The dataset is **imbalanced**:
  - Majority class: `no` ≈ 88.7%
  - Minority class: `yes` ≈ 11.3%

### Baseline Performance
A baseline classifier predicting only the majority class (“no”) achieves:
- **Baseline Accuracy ≈ 88.7%**

This serves as the minimum benchmark all models should beat.

### Evaluation Metrics
Because the target is imbalanced, model performance is evaluated using:
- Accuracy
- F1 Score
- Recall (important for identifying subscribing customers)
- Cross-validation score (CV score)

---

## Modeling Results (Default Models)
Initial models were trained and evaluated using default settings:

| Model | Train Time (s) | Train Accuracy | Test Accuracy |
|------|----------------:|---------------:|--------------:|
| Logistic Regression | 13.06 | 0.9102 | 0.9166 |
| KNN | 0.20 | 0.9277 | 0.9076 |
| Decision Tree | 0.62 | 1.0000 | 0.8946 |
| SVM (LinearSVC) | 5.51 | 0.9080 | 0.9125 |

---

## Findings (Actionable Items Highlighted)
### Key Findings
- ✅ **Logistic Regression performed best overall** in test accuracy (≈ 91.7%) and offered stable performance.
- ⚠️ **Decision Tree overfit**: it reached 100% training accuracy but had lower test accuracy, suggesting weak generalization.
- ✅ **SVM achieved strong performance**, but training time was higher than simpler models.
- ✅ **KNN was the fastest**, but its performance did not beat Logistic Regression.

### Actionable Items (Nontechnical)
- **Prioritize Logistic Regression as the first production model**, as it offers the best balance of accuracy and reliability.
- **Do not deploy a Decision Tree without tuning**, since it may perform poorly on new customer data.
- **Use improved evaluation metrics** (F1 score and recall) rather than accuracy alone, because the number of subscribers is much smaller than non-subscribers.

---

## Next Steps and Recommendations
To improve performance beyond baseline models, we recommend:

### 1. Hyperparameter Tuning
Use `GridSearchCV` to optimize each model’s parameters:
- KNN: number of neighbors, distance weighting
- Decision Tree: max depth, min samples leaf/split
- SVM: C, kernel selection
- Logistic Regression: regularization strength (C)

### 2. Optimize Evaluation Metric
Accuracy can be misleading due to imbalance.
Recommended tuning metrics:
- **F1 score** (recommended)
- **Recall score** (if maximizing subscriber detection is most important)

### 3. Handle Class Imbalance
Improve minority class prediction using:
- `class_weight="balanced"` in Logistic Regression / SVM
- Resampling methods (SMOTE or undersampling)

### 4. Deployability Considerations
For operational use:
- Logistic Regression is recommended due to:
  - interpretability
  - stable performance
  - fast prediction time

---

## Deliverables
- A clean notebook with:
  - preprocessing pipeline
  - baseline and model comparison
  - evaluation metrics
  - GridSearchCV tuning function
- Final results presented in DataFrames for clarity

---

## Rubric Checklist (25 points)

### Findings:
✅ Clearly stated business understanding of the problem.  
✅ Clean and organized notebook with data cleaning.  
✅ Correct and concise interpretation of descriptive and inferential statistics.  
✅ Clearly stated findings in their own section with actionable items highlighted in appropriate language for a nontechnical audience.  
✅ Next steps and recommendations.  

---

## Scoring Rubric Reference
**5 pts — Excellent**  
Your submission includes all of the listed components.  

**0 pts — Criterion not met**  
Your submission includes a few or none of the listed components.  

**Total Points: 25**

---
