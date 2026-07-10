# Applied AI & ML Capstone Project

## Part 1 – Data Acquisition, Cleaning and Exploratory Data Analysis (EDA)

### Project Overview

The objective of this part is to understand the dataset before building any machine learning model. The dataset was loaded, cleaned, analyzed and visualized using different EDA techniques. A cleaned dataset was generated which will be used in Part 2 and Part 3 of the capstone project.

---

## Dataset

**Dataset:** Laptop Price Prediction Dataset

**Source:** Kaggle

**Link:** https://www.kaggle.com/datasets/ehtishamsadiq/uncleaned-laptop-price-dataset

The dataset contains laptop specifications such as company, RAM, processor, storage, operating system, weight and screen size along with the laptop price.

### Why this dataset?

I selected this dataset because it satisfies the project requirements:

- More than 500 rows
- More than 5 numeric features (after preprocessing)
- More than 2 categorical features
- Continuous target column (`Price`) suitable for regression and later classification

---

## Project Structure

```
Part-1/
│
├── data/
│   └── laptopData.csv
│
├── notebooks/
│   └── Capstone_Project_Masai_Part1.ipynb
│
├── cleaned_data.csv
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

---

# Work Completed

## Task 1 – Data Loading

- Loaded the dataset using pandas.
- Displayed the first five rows.
- Checked data types.
- Verified the dataset shape.

---

## Task 2 – Missing Value Analysis

- Calculated missing value count and percentage for every column.
- No column contained more than 20% missing values.
- Missing values in numeric columns were filled using the median because the dataset contains skewed distributions.

---

## Task 3 – Duplicate Detection

- Counted duplicate rows.
- Removed duplicate records.
- Compared null percentages before and after duplicate removal.

---

## Task 4 – Data Type Correction

The following changes were made:

- Removed unnecessary index column.
- Converted `Inches`, `Ram` and `Weight` to numeric.
- Converted `Company`, `TypeName` and `OpSys` to category datatype.
- Compared memory usage before and after conversion.

---

## Task 5 – Descriptive Statistics and Skewness

- Generated descriptive statistics using `describe()`.
- Calculated skewness for every numeric column.
- `Inches` showed the highest absolute skewness.
- Median was preferred over mean for imputation because skewed distributions are affected by extreme values.

---

## Task 6 – Outlier Detection

IQR analysis was performed on:

- Inches
- Weight

Outliers were identified but were not removed as instructed. They will be considered during feature engineering and model preparation in the next part.

---

## Task 7 – Data Visualization

The following visualizations were created:

- Line Plot
- Bar Chart
- Histogram
- Scatter Plot
- Box Plot

### Observations

- Laptop prices vary significantly across companies.
- Most laptops have screen sizes between 13 and 16 inches.
- RAM shows a positive relationship with price.
- Gaming and Workstation laptops generally have higher prices.
- Some unusual screen size and weight values were observed.

---

## Task 8 – Correlation Analysis

- Pearson correlation matrix was calculated.
- Correlation heatmap was generated.
- RAM and Price showed the highest positive correlation.

The correlation does not necessarily imply causation because other hardware specifications may also influence laptop prices.

---

## Task 9 – Additional Analysis

### 9a

Compared mean and median for the two most skewed columns before imputation.

Median was selected because it is more robust to skewed data.

### 9b

Calculated Spearman correlation matrix.

Compared Pearson and Spearman correlations.

Identified the three feature pairs with the largest differences.

Pearson correlation will be used as the primary guide for feature selection in Part 2.

### 9c

Performed grouped aggregation using Company and Price.

Calculated:

- Mean
- Standard Deviation
- Count

Razer had the highest average laptop price, while the large ratio between the highest and lowest mean suggests that Company carries useful predictive information.

---

## Output

The cleaned dataset was saved as:

```
cleaned_data.csv
```

This dataset will be used in the next parts of the capstone project.

---

## Overall Workflow

```text
Raw Dataset (laptopData.csv)
            │
            ▼
Load Dataset
            │
            ▼
Initial Inspection
(Head, Shape, Data Types)
            │
            ▼
Missing Value Analysis
            │
            ▼
Median Imputation
            │
            ▼
Duplicate Detection & Removal
            │
            ▼
Data Type Correction
            │
            ▼
Descriptive Statistics
            │
            ▼
Skewness Analysis
            │
            ▼
Outlier Detection (IQR)
            │
            ▼
Data Visualization
(Line, Bar, Histogram,
Scatter, Box Plot)
            │
            ▼
Correlation Analysis
(Pearson & Spearman)
            │
            ▼
Grouped Aggregation
            │
            ▼
Save cleaned_data.csv

---

```

## How to Run

1. Install the required libraries.

```
pip install -r requirements.txt
```

2. Open the notebook.

```
notebooks/Capstone_Project_Masai_Part1.ipynb
```

3. Run all cells from top to bottom.

---

## Conclusion

The raw dataset was successfully cleaned and analyzed. Missing values, duplicate rows and incorrect data types were handled. Outliers and correlations were studied, and several visualizations were created to understand the data. The cleaned dataset is now ready for feature engineering and machine learning in Part 2.
