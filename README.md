# Applied AI & ML Capstone Project

## Overview

This repository contains my complete **Applied AI & Machine Learning Capstone Project**, completed as part of the Applied AI & ML program.

The project is divided into four progressive parts, covering the complete machine learning lifecycle—from data preprocessing to explainable AI using Large Language Models (LLMs).

---

## Repository Structure

```
Applied-AI-ML-Capstone
│
├── Part-1
├── Part-2
├── Part-3
└── Part-4
```

---

# Project Parts

## Part 1 – Data Cleaning & Exploratory Data Analysis

- Data acquisition
- Data cleaning
- Missing value handling
- Duplicate removal
- Exploratory Data Analysis
- Feature understanding
- Data visualization

---

## Part 2 – Supervised Machine Learning

- Regression
- Classification
- Model evaluation
- Confusion Matrix
- ROC-AUC
- Logistic Regression
- Linear Regression

---

## Part 3 – Advanced Machine Learning

- Decision Trees
- Random Forest
- Gradient Boosting
- Cross Validation
- Hyperparameter Tuning
- GridSearchCV
- Feature Importance
- Feature Ablation
- Learning Curves
- Model Serialization

---

## Part 4 – Explainable AI with LLM

- Load trained Random Forest model
- Feature Encoding
- PII Guardrail
- JSON Schema Validation
- Google Gemini API Integration
- Structured Prediction Explanation
- End-to-End AI Pipeline

---

# Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Joblib
- Google Gemini API
- JSON Schema
- Google Colab

---

# Highlights

- Complete end-to-end machine learning workflow.
- Modular project structure.
- Best model serialized using Joblib.
- Explainable AI using a Large Language Model.
- Structured JSON output validation.
- Production-style pipeline with graceful handling of external API failures.

---

# Note

The LLM integration was initially implemented using the OpenRouter API. During testing, repeated free-tier provider rate limits and upstream timeout issues affected reliability. To ensure a stable submission, the project was migrated to the **Google Gemini API**. This change only affected the LLM communication layer; the machine learning pipeline, prediction logic, validation, and overall architecture remained unchanged.

---

## Author

**Ishwar Devnarayan Vishwakarma**

Applied AI & ML Capstone Project
