# Breast Cancer Classification

A machine learning project for binary classification of breast tumors (Malignant vs. Benign) using the the Wisconsin Breast Cancer Dataset.

## 📋 Project Overview

This project develops and evaluates multiple machine learning models to classify breast cancer tumors based on cell nucleus measurements from fine needle aspirate (FNA) images. The analysis emphasizes **high recall** for malignant cases, as false negatives carry severe medical and financial consequences in insurance contexts.

### Key Features:
- ✅ Comprehensive exploratory data analysis (EDA)
- ✅ Multiple model comparison (Logistic Regression, SVM, Decision Tree, Random Forest)
- ✅ Advanced threshold tuning to maximize recall
- ✅ Feature importance analysis
- ✅ Business-focused evaluation (precision-recall curves, cost-benefit analysis)

---

## 🎯 Key Results

| Model | Accuracy | Recall (Malignant)
|-------|----------|-------------------
| **Logistic Regression** | **97.1%** | **93.8%** 
| Random Forest | 96.5% | 91% 
| SVM (RBF) | 95.9% | 89.1% 
| Decision Tree | 91.8% | 78.6% 

**Best Model:** Logistic Regression with optimized threshold (0.24)
- **At threshold 0.24:** 98% accuracy, 98% recall, only 1 false negative
- **At threshold 0.05:** 100% recall (zero false negatives) with acceptable precision trade-off

---

## 🔬 Dataset

**Source:** Wisconsin Breast Cancer Dataset  
**Samples:** 569 (357 Benign, 212 Malignant)  
**Features:** 30 numeric features computed from cell nucleus images  
**Missing Values:** 0

### Feature Categories:
- **Mean values** (10 features): Average measurements across cells
- **Standard error** (10 features): Variability in measurements
- **Worst values** (10 features): Largest/most severe cell measurements

**Key Finding:** "Worst" features (e.g., `concave points_worst`, `area_worst`, `radius_worst`) are most predictive of malignancy.

---

## 📊 Installation & Usage

### Prerequisites
```bash
Python 3.8+
pip
```

### Setup
```bash
# Clone the repository
git clone https://github.com/mzamanir/breast-cancer-classification.git
cd breast-cancer-classification

# Install dependencies
pip install -r requirements.txt
```

### Running the Analysis

```bash
jupyter notebook notebooks/analysis.ipynb
```

---

## 🧪 Methodology

### 1. Exploratory Data Analysis (EDA)
- Class distribution analysis (62.7% Benign, 37.3% Malignant)
- Feature correlation analysis
- Distribution comparisons (Benign vs. Malignant)


### 2. Data Preprocessing
- Train/test split (70/30) with stratification
- StandardScaler normalization
- No missing values to handle

### 3. Model Development
Trained and compared 4 algorithms:
- **Logistic Regression** (with L2 regularization)
- **Support Vector Machine** (RBF kernel)
- **Decision Tree** (with pruning via GridSearchCV)
- **Random Forest** (100 estimators)

### 4. Hyperparameter Tuning
All models were tuned using **GridSearchCV with 5-fold cross-validation**.  
The primary optimization target was overall accuracy, while **recall (malignant sensitivity)** was continuously monitored to ensure clinical safety.

### 5. Threshold Optimization
Classification thresholds were systematically evaluated using a **False Negatives vs. Threshold** curve.

Two clinically relevant operating points emerged:

- **Threshold = 0.24** → Best balance of accuracy and recall  
- **Threshold = 0.10** → Eliminates all false negatives (perfect recall)

Threshold tuning is essential in medical applications, where missing a malignant case is unacceptable.

---

## 📈 Model Evaluation Metrics

### Primary Metrics Used
- **Recall (Sensitivity):** Proportion of malignant cases correctly identified  
- **Precision:** Proportion of predicted malignant cases that are actually malignant  
- **F1-Score:** Balanced metric for precision and recall  

### Why Recall Matters Most
In medical and insurance contexts, **false negatives carry significantly higher cost**:

- A missed cancer diagnosis can delay treatment, worsen outcomes, and increase long-term claim cost  
- A false positive generally leads to additional testing—much lower impact  

➡️ **Conclusion:** The model must prioritize high recall to minimize false negatives.

---

## 📝 Key Findings

1. **Logistic Regression delivered the strongest performance**, achieving ~97% accuracy and high malignant recall.
2. **Threshold tuning is essential:**  
   - At threshold 0.50 → recall = 94%  
   - At threshold 0.24 → recall = 98%  
   - At threshold 0.05 → **recall = 100%**, eliminating all false negatives.
3. **“Worst” tumor measurements dominate predictive power**, consistent with medical knowledge:  
   - concave points_worst  
   - perimeter_worst  
   - area_worst  
4. **Feature importance is stable across models:** The same 5–6 features consistently rank highest across correlation analysis, Random Forest, and model coefficients.
5. **Real-world readiness:**  
   - The model can operate in either *balanced mode* (threshold=0.24)  
   - or *maximum safety mode* (threshold=0.10) for clinical scenarios requiring zero false negatives.

---
## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

