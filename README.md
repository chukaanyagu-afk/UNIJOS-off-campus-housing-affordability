# UNIJOS-off-campus-housing-affordability
Logistic Regression classifier to predict UNIJOS off-campus housing as Affordable (≤170k) vs Expensive (>170k). 
# UNIJOS Off-Campus Housing Affordability Classifier

> Can we predict if a student lodge around UNIJOS will be Affordable or Expensive before you even visit?

A Logistic Regression model to classify student housing around Farin Gada, Bauchi Road, and Ring Road, Jos.

**Final Model: 75% Accuracy | F1-Score: 0.76 | ROC-AUC: 0.60**

## 🚨 My Key Learning: Why I Celebrated a Drop from 95% to 75%

### First Run (Wrong): 95% Accuracy

- Defined Expensive as > ₦100,000
- Result: 90% of data was "Expensive", test set was 19 Expensive / 1 Affordable
- Model just guessed "Expensive" every time. Fake accuracy.

### Fixes Applied

1. **Fixed Data Leakage:** Dropped `Lodge/Accommodation Name` (e.g., "Grace Villa") - it's a unique ID, not a feature.
2. **Fixed Class Imbalance:** Changed threshold to > ₦170,000 to get balanced classes (50% Affordable / 50% Expensive).
3. **Fixed Evaluation:** Used `stratify=y` and focused on F1-score, not just Accuracy.

### Final Run (Correct): 75% Accuracy

- Balanced confusion matrix, model actually learns `Location + House Type + Furnished`.

## 📊 Dataset

- **Source:** 100 lodges manually collected around UNIJOS
- **Location:** Farin Gada, Bauchi Road, Ring Road, Angwan Rukuba
- **Features:**
    - `Location` (Categorical)
    - `House Type` (Single Room, Self-Contain, 1-Bedroom Flat)
    - `Has Light`, `Has Water`, `Furnished` (Binary)
    - `Price (₦)` → Converted to target `expensive` (0/1)

## 🔬 Methodology

1. EDA & Cleaning
2. OneHotEncoding for categorical + StandardScaler for numeric in a `sklearn Pipeline`
3. Train/Test Split (80/20, stratified)
4. Logistic Regression
5. Evaluation: Confusion Matrix, Classification Report, ROC-AUC

## 📈 Results

| Metric | Affordable (0) | Expensive (1) |
| :--- | :--- | :--- |
| Precision | 0.40 | 0.87 |
| Recall | 0.50 | 0.81 |
| F1-Score | 0.44| 0.84 |

**Key Insight:** Self-Contain and 1-Bedroom Flats in Farin Gada are 3x more likely to be Expensive (>170k) than Single Rooms in Bauchi Road.


cd unijos-off-campus-housing-affordability
pip install -r requirements.txt
jupyter notebook notebooks/01_housing_model.ipynb
