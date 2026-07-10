# Applied AI & ML Capstone Project

## Part 2 – Supervised Machine Learning: Build, Train and Evaluate Models

### Project Overview

In this part, the cleaned dataset from Part 1 was used to build supervised machine learning models. A regression model was created to predict laptop prices, and a classification model was built to classify laptops as above or below the median price. Different evaluation metrics and model comparison techniques were used to analyze the performance.

---

## Dataset

**Dataset:** Cleaned Laptop Price Prediction Dataset

This dataset is the cleaned version generated in Part 1.

### Target Variables

**Regression Target**

- `Price`

**Classification Target**

- `y_clf = (Price > Price.median()).astype(int)`

The classification target divides laptops into two classes:

- 1 → Price above the median
- 0 → Price below or equal to the median

---

## Project Structure

```text
Part-2/
│
├── data/
│   └── cleaned_data.csv
│
├── notebooks/
│   └── Capstone_Project_Masai_Part2.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Libraries Used

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

# Tasks Performed

## Task 1 – Data Preparation

- Loaded `cleaned_data.csv`.
- Created the feature matrix (`X`).
- Selected `Price` as the regression target.
- Created a binary classification target using the median price.

---

## Task 2 – Feature Encoding

The categorical columns did not have a natural order, so One-Hot Encoding was applied.

`drop_first=True` was used to avoid multicollinearity.

Label encoding was not used because it would incorrectly introduce an ordinal relationship between categories.

---

## Task 3 – Train-Test Split and Scaling

- Split the dataset into 80% training and 20% testing.
- Applied `StandardScaler`.
- The scaler was fitted only on the training data to avoid data leakage.

---

## Task 4 – Regression Models

### Linear Regression

The Linear Regression model was trained using the scaled training data.

Evaluation metrics:

- Mean Squared Error (MSE)
- R² Score

The three features with the largest coefficients were:

- Nvidia GeForce GTX 1070
- Intel Core i7-7700HQ 2.8GHz
- 512GB SSD

These features had the strongest influence on the predicted laptop price.

### Ridge Regression

Ridge Regression was trained using the same training and testing data.

The Ridge model achieved a slightly lower MSE and a slightly higher R² score than the Linear Regression model, indicating a small improvement due to regularization.

---

## Task 5 – Classification Model

A Logistic Regression model was trained to classify laptops as above or below the median price.

The class distribution was already balanced, so no resampling technique such as SMOTE was required.

Model evaluation included:

- Confusion Matrix
- Accuracy
- Precision
- Recall
- F1 Score
- ROC Curve
- AUC Score

The model achieved an AUC of approximately **0.97**, showing excellent class separation.

### Precision and Recall

Precision

```
TP / (TP + FP)
```

Recall

```
TP / (TP + FN)
```

For this dataset, both precision and recall are important because the two classes are balanced. The model achieved good performance on both metrics.

---

## Task 6 – Decision Threshold Analysis

The classification threshold was tested at:

- 0.30
- 0.40
- 0.50
- 0.60
- 0.70

The best F1-score was obtained at a threshold of **0.60**.

Increasing the threshold improved precision but slightly reduced recall.

---

## Task 7 – Regularization Experiment

A second Logistic Regression model was trained using:

```
C = 0.01
```

The model was compared with the default model (`C = 1.0`).

The regularized model achieved slightly better recall and AUC on this dataset, suggesting that stronger regularization improved generalization.

---

## Task 8 – Bootstrap Confidence Interval

A bootstrap experiment with **500 samples** was performed to compare the AUC difference between the two Logistic Regression models.

The resulting 95% confidence interval included zero.

This indicates that the observed performance difference between the two models is not statistically reliable across different samples.

---

## Overall Workflow

```text
Cleaned Dataset (cleaned_data.csv)
                │
                ▼
Load Dataset
                │
                ▼
Define Features (X)
and Targets (y)
                │
                ▼
One-Hot Encoding
                │
                ▼
Train-Test Split
                │
                ▼
Feature Scaling
(StandardScaler)
                │
                ▼
Regression Models
│
├── Linear Regression
└── Ridge Regression
                │
                ▼
Model Evaluation
(MSE & R²)
                │
                ▼
Classification Model
(Logistic Regression)
                │
                ▼
Confusion Matrix
Accuracy
Precision
Recall
F1 Score
ROC Curve
AUC
                │
                ▼
Decision Threshold Analysis
                │
                ▼
Regularization (C = 0.01)
                │
                ▼
Bootstrap Confidence Interval
```

---

## How to Run

1. Install the required libraries.

```bash
pip install -r requirements.txt
```

2. Open the notebook.

```text
notebooks/Capstone_Project_Masai_Part2.ipynb
```

3. Run all cells from top to bottom.

---

## Conclusion

The cleaned dataset from Part 1 was successfully used to build regression and classification models. Linear Regression, Ridge Regression, and Logistic Regression were trained and evaluated using different performance metrics. Threshold analysis, regularization, and bootstrap sampling were also performed to better understand the models. The results from this part provide a strong foundation for the advanced machine learning techniques in Part 3.