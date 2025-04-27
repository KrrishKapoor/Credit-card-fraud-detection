# Credit Card Fraud Detection — A Finance and Risk Management Perspective

---

## 🧩 Introduction — Why This Matters

Credit card fraud costs financial institutions billions each year, eroding both profits and customer trust.  
The earlier fraud is detected, the less financial loss is incurred.

In this project, I approached fraud detection **not simply as a machine learning task**, but as a **finance risk management challenge** — balancing fraud capture with operational cost.

---

## 🚀 The Challenge — Detecting a Needle in a Haystack

Fraudulent transactions account for **less than 0.2%** of all transactions — an extreme class imbalance.

Traditional machine learning models tend to **ignore the minority class** or become biased toward predicting everything as normal.

Thus, the core challenge was:
- **Accurately detect rare fraudulent transactions**
- **Minimize false alarms** that waste operational resources

---

## 🛠️ My Approach — Step by Step

### Step 1: Understanding the Data
- Used an anonymized credit card dataset with PCA-transformed features (V1–V28) + Amount.
- Verified there were **no missing values**.

### Step 2: Initial Preprocessing
- **Dropped irrelevant columns** (like 'id').
- **Standardized** features using **StandardScaler** to ensure fair model performance.

### Step 3: Modeling
- Trained a **Random Forest Classifier** with cross-validation:
  - 5-Fold CV
  - F1 score as the evaluation metric (to balance precision and recall).

**Early Result:**  
- High overall accuracy but initially suspiciously perfect F1 scores.

---

## ⚠️ A Surprise — The Leakage Problem

During early experimentation, I discovered that the model was **perfectly predicting** frauds.  
This triggered a red flag: *“Is there leakage?”*

Upon inspection, I realized that the `"Class"` column accidentally remained inside the feature set due to a syntax error during data dropping.

**Lesson Learned:**  
Always check input features carefully before training. Data leakage is silent but deadly!

---

## 🔥 Real Results — After Fixing and Improving

- **Mean Cross-Validated F1 Score:** ~84%
- **ROC AUC Score:** High — showing strong separation between fraud and normal transactions.
- **Top Features:** V17, V12, and V14 had the highest importance.

---

## 📊 Key Metrics Evaluated

| Metric | Why Used |
|:-------|:---------|
| **F1 Score** | Balanced precision and recall |
| **Precision / Recall** | Understand fraud detection vs false alarm tradeoff |
| **ROC Curve + AUC** | Overall model ability across thresholds |
| **Confusion Matrix** | Visualize true/false positives and negatives |

---

## 📈 Visual Analysis

### 1. Class Distribution
Extremely imbalanced dataset requiring special attention.

*([Class_distribution.png](https://github.com/KrrishKapoor/credit-card-fraud-detection/blob/main/Class_distribution.png))*

---

### 2. Confusion Matrix
Balanced detection after threshold tuning — real-world usable.

*(Insert Confusion Matrix heatmap)*

---

### 3. Feature Importance
Shows which patterns in transactions most strongly indicated fraud.

*(Insert Feature Importance plot)*

---

### 4. ROC Curve
Model achieved strong separation, supporting threshold adjustment strategy.

![ROC Curve](roc_curve.png)

---

## 📋 Business Recommendation

In real financial settings, **missing fraud** is costlier than **investigating false alarms**.

Thus, I recommend:
- **Lowering decision threshold** from 0.5 to ~0.4
- **Impact:** 
  - Catch more frauds
  - Accept a small manageable rise in false positives
- **Implementation:** 
  - Flag transactions exceeding threshold for manual review.

> Finance risk teams must align model settings with organizational risk appetite — this project shows how machine learning can support that process.

---

## 🛤️ Next Steps

- Use **SMOTE** to further balance training data.
- Experiment with **XGBoost** or **LightGBM** for even better precision-recall tradeoffs.
- Deploy model as **real-time transaction scoring API**.
- Incorporate **cost-sensitive evaluation** (fraud loss cost vs operational review cost).

---

# 📚 Lessons Learned

- Data preprocessing must be rigorous to avoid silent data leakage.
- Finance projects must think beyond accuracy — business risk must guide model decisions.
- Small model adjustments (like threshold tuning) can have **huge business impact**.

---
