# Applied AI & ML Capstone Project

## Part 3 – Advanced Modeling – Ensembles, Hyperparameter Tuning and ML Pipeline

### Project Overview

The objective of this part is to compare multiple machine learning models, improve performance using ensemble methods, perform hyperparameter tuning, evaluate models using cross-validation, and build a reusable machine learning pipeline. The final trained model was saved and reloaded successfully for future predictions.

---

## Dataset

**Dataset:** Cleaned Laptop Price Prediction Dataset

This dataset is the cleaned version generated in Part 1.

### Target Variable

Binary Classification Target

```python
y_clf = (Price > Price.median()).astype(int)
```

- 1 → Laptop price above the median
- 0 → Laptop price below or equal to the median

---

## Project Structure

```text
Part-3/
│
├── data/
│   └── cleaned_data.csv
│
├── notebooks/
│   └── Capstone_Project_Masai_Part3.ipynb
│
├── best_model.pkl
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
- joblib

---

# Work Completed

## Task 1 – Decision Tree Baseline

- Trained a DecisionTreeClassifier using default parameters.
- Reported training and testing accuracy.

### Results

- Training Accuracy: **99.80%**
- Testing Accuracy: **88.63%**

### Observation

The model showed clear signs of overfitting because the training accuracy was much higher than the testing accuracy.

Decision Trees are considered **high-variance models** because they greedily choose the best split at every node and can easily memorize the training data without generalizing well to unseen data.

---

## Task 2 – Controlled Decision Tree

A second Decision Tree was trained using:

- `max_depth = 5`
- `min_samples_split = 20`

### Results

- Training Accuracy: **88.13%**
- Testing Accuracy: **89.80%**

### Observation

The controlled tree reduced overfitting and achieved slightly better testing performance.

### Parameter Explanation

**max_depth**

Limits how deep the tree can grow, reducing model variance while slightly increasing bias.

**min_samples_split**

Prevents splitting nodes containing fewer than the specified number of samples, reducing splits based on noise.

Compared to the unconstrained tree, the controlled tree produced a much smaller train-test accuracy gap.

---

## Task 3 – Gini vs Entropy Comparison

Two Decision Trees were trained using different splitting criteria.

- Gini
- Entropy

### Results

- Gini Accuracy: **89.41%**
- Entropy Accuracy: **89.80%**

### Formula

**Gini Impurity**

```
Gini = 1 − Σ(pi²)
```

**Entropy**

```
Entropy = −Σ(pi log₂(pi))
```

A **Gini value of 0** means the node is completely pure, meaning every sample belongs to the same class.

### Observation

Both criteria produced very similar performance. Entropy achieved slightly higher accuracy on this dataset.

---

## Task 4 – Random Forest

A Random Forest classifier was trained using:

- n_estimators = 100
- max_depth = 10
- random_state = 42

### Results

- Training Accuracy: **91.76%**
- Testing Accuracy: **90.98%**
- ROC-AUC: **0.9717**

### Top 5 Important Features

| Feature | Importance |
|---------|-----------:|
| Ram | 0.159243 |
| TypeName_Notebook | 0.129593 |
| Weight | 0.074105 |
| Memory_1TB HDD | 0.062813 |
| TypeName_Gaming | 0.047444 |

### Feature Importance

Random Forest computes feature importance by measuring the average reduction in Gini impurity contributed by each feature across all trees.

Unlike Linear Regression coefficients, feature importance does not indicate positive or negative influence. Instead, it measures how useful each feature is for making accurate splits.

### Bagging

Random Forest uses **bootstrap sampling**, where every tree is trained on a different random sample (with replacement) of the training data.

At every split, only a random subset of features is considered.

Combining predictions from many trees reduces variance and usually produces better generalization than a single Decision Tree.

---

## Task 4a – Gradient Boosting

A Gradient Boosting classifier was trained using:

- n_estimators = 100
- learning_rate = 0.1
- max_depth = 3

### Results

- Training Accuracy: **93.82%**
- Testing Accuracy: **92.55%**
- ROC-AUC: **0.9791**

### Observation

Gradient Boosting achieved the highest testing ROC-AUC among all evaluated models.

Unlike Random Forest, each new tree attempts to correct the mistakes made by previous trees.

---

## Task 4b – Feature Ablation Study

The five least important features identified by the Random Forest were removed.

A second Random Forest model was trained using the reduced feature set.

### Results

| Model | ROC-AUC |
|------|---------:|
| Original Random Forest | **0.9717** |
| Reduced Random Forest | **0.9693** |

### Observation

The ROC-AUC decreased only slightly after removing the least important features.

This indicates that these features contributed very little to the model.

Using fewer features can reduce inference time and maintenance cost while maintaining almost the same predictive performance.

---

## Task 5 – Cross-Validated Comparison

Five-fold Stratified Cross Validation was performed using ROC-AUC.

### Results

| Model | Mean AUC | Std AUC |
|------|---------:|---------:|
| Logistic Regression | 0.9478 | 0.0093 |
| Decision Tree | 0.8914 | 0.0266 |
| Random Forest | **0.9578** | **0.0044** |
| Gradient Boosting | 0.9559 | 0.0101 |

### Observation

Cross-validation provides a more reliable estimate of model performance because every sample participates in both training and validation across different folds.

Random Forest achieved the highest average ROC-AUC with the lowest standard deviation, indicating consistent performance.

---

## Task 6 – Hyperparameter Tuning with GridSearchCV

A Pipeline was created using:

- SimpleImputer
- StandardScaler
- RandomForestClassifier

The following parameter grid was used:

- n_estimators → 50, 100, 200
- max_depth → 5, 10, None
- min_samples_leaf → 1, 5

### Results

**Best Parameters**

- max_depth = None
- min_samples_leaf = 1
- n_estimators = 100

**Best ROC-AUC**

```
0.9632
```

### Total Configurations Evaluated

Parameter combinations:

```
3 × 3 × 2 = 18
```

Five-fold Cross Validation:

```
18 × 5 = 90 model fits
```

### Grid Search vs Randomized Search

Grid Search evaluates every parameter combination and generally finds the best configuration but requires more computation.

Randomized Search evaluates only a subset of combinations, making it faster for larger parameter spaces.

---

## Task 7 – Manual Learning Curve

The best pipeline was trained using:

- 20%
- 40%
- 60%
- 80%
- 100%

of the training data.

### Results

| Training Fraction | Training AUC | Test AUC |
|-----------------:|-------------:|---------:|
| 20% | 1.0000 | 0.9545 |
| 40% | 1.0000 | 0.9676 |
| 60% | 1.0000 | 0.9776 |
| 80% | 1.0000 | 0.9789 |
| 100% | 1.0000 | 0.9804 |

### Interpretation

**Did the training AUC decrease?**

No. The training AUC remained at 1.0 for every training subset.

**Did the test AUC increase?**

Yes. The test AUC improved steadily as more training data became available.

**Is the model data-limited or capacity-limited?**

The model appears to benefit from additional training data because the testing AUC continued increasing with larger training sets.

---

## Task 8 – Model Serialization

The best pipeline was saved using:

```python
joblib.dump(best_pipeline, "best_model.pkl")
```

The model was successfully reloaded using:

```python
joblib.load("best_model.pkl")
```

Predictions were generated successfully on sample input data.

This confirms that the saved model can be reused without retraining.

---

## Summary Comparison

| Model | 5-Fold Mean AUC | 5-Fold Std AUC | Test ROC-AUC |
|------|----------------:|---------------:|-------------:|
| Logistic Regression | 0.9478 | 0.0093 | 0.9724 |
| Decision Tree | 0.8914 | 0.0266 | — |
| Random Forest | **0.9578** | **0.0044** | 0.9717 |
| Gradient Boosting | 0.9559 | 0.0101 | **0.9791** |

### Final Recommendation

Gradient Boosting achieved the highest ROC-AUC on the test set. However, Random Forest achieved the highest average cross-validation ROC-AUC and the lowest variation across folds, indicating more consistent performance. Considering both predictive performance and stability, Random Forest is recommended as the final model for deployment.

---

## Overall Workflow

```text
Cleaned Dataset
        │
        ▼
Train-Test Split
        │
        ▼
Decision Tree
        │
        ▼
Controlled Decision Tree
        │
        ▼
Gini vs Entropy Comparison
        │
        ▼
Random Forest
        │
        ▼
Gradient Boosting
        │
        ▼
Feature Ablation
        │
        ▼
Cross Validation
        │
        ▼
GridSearchCV
        │
        ▼
Best Pipeline
        │
        ▼
Manual Learning Curve
        │
        ▼
Model Serialization
(best_model.pkl)
```

---

## How to Run

1. Install the required libraries.

```bash
pip install -r requirements.txt
```

2. Open the notebook.

```text
notebooks/Capstone_Project_Masai_Part3.ipynb
```

3. Run all notebook cells from top to bottom.

---

## Conclusion

Different ensemble learning techniques were trained and compared using multiple evaluation methods. Hyperparameter tuning, cross-validation, feature importance analysis, feature ablation, learning curve analysis and model serialization were successfully completed. The final trained model is reproducible, reusable and ready for deployment in the final phase of the capstone project.