# Applied AI & ML Capstone Project

# Part 4 – LLM Integration and Explainable AI

## Project Overview

This part extends the machine learning pipeline developed in Part 3 by integrating a Large Language Model (LLM). The trained Random Forest model predicts whether a laptop belongs to the **High Price** or **Low Price** category, while the LLM generates a human-readable explanation for the prediction.

The objective is to combine traditional machine learning with Generative AI by producing structured explanations in JSON format while validating the responses before presenting them to the user.

---

# Objectives

- Load the trained machine learning model.
- Predict laptop price category.
- Generate natural language explanations using an LLM.
- Validate the generated JSON response.
- Detect Personally Identifiable Information (PII).
- Demonstrate a complete end-to-end AI pipeline.

---

# Dataset

The project uses the cleaned laptop dataset generated in **Part 1**.

The prediction model used in this notebook is the **best Random Forest pipeline** obtained in **Part 3**.

---

# Project Structure

```
Part-4/
│
├── data/
│   └── cleaned_data.csv
│
├── models/
│   └── best_model.pkl
│
├── notebooks/
│   └── Capstone_Project_Masai_Part4.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

# Libraries Used

- pandas
- numpy
- scikit-learn
- joblib
- json
- jsonschema
- google-genai

---

# Work Completed

## Task 1 – Environment Setup

- Imported all required libraries.
- Loaded the Gemini API key securely using Google Colab Secrets.
- Configured the Gemini client.

---

## Task 2 – Load Trained Model

- Loaded the serialized Random Forest model (`best_model.pkl`) using Joblib.
- Reused the trained pipeline from Part 3 without retraining.

---

## Task 3 – LLM Integration

A reusable `call_llm()` function was implemented to communicate with the Gemini API.

The function:

- sends prompts to the model
- receives responses
- returns generated text for further validation

---

## Task 4 – API Connection Test

A simple prompt was used to verify that the Gemini API was connected successfully before integrating it into the prediction workflow.

---

## Task 5 – System Prompt and JSON Schema

A system prompt was created to instruct the LLM to generate structured explanations.

A JSON Schema validates that every response contains exactly these fields:

- prediction_label
- confidence_level
- top_reason
- second_reason
- next_step

This prevents unexpected response formats from entering the pipeline.

---

## Task 6 – Feature Encoding

The `encode_record()` function converts user-provided laptop specifications into the same feature format used during model training.

This ensures compatibility with the trained Random Forest model.

---

## Task 7 – PII Guardrail

A simple guardrail checks user input for potential Personally Identifiable Information (PII), including:

- Email addresses
- Phone numbers

If PII is detected, explanation generation is skipped.

---

## Task 8 – Handcrafted Test Records

Three manually created laptop configurations were prepared to test the complete prediction pipeline.

These records represent different hardware specifications and expected pricing categories.

---

## Task 9 – Prediction and Explanation

For each laptop:

1. Features are encoded.
2. The trained Random Forest predicts the price category.
3. Prediction confidence is calculated.
4. The prediction is passed to the Gemini API.
5. Gemini generates a structured JSON explanation.
6. The JSON response is validated before being displayed.

---

## Task 10 – Temperature Comparison

The explanation was generated using different temperature values to compare deterministic and more creative responses.

Lower temperature values produced more consistent outputs, making them more suitable for structured JSON generation.

---

## Task 11 – End-to-End Demonstration

The complete workflow demonstrates how traditional machine learning and Large Language Models can work together in a single application.

---

# Overall Workflow

```text
Laptop Specifications
           │
           ▼
Feature Encoding
           │
           ▼
Random Forest Model
           │
           ▼
Prediction
           │
           ▼
Confidence Calculation
           │
           ▼
PII Guardrail
           │
           ▼
Gemini API
           │
           ▼
JSON Validation
           │
           ▼
Structured Explanation
```

---

# Why Google Gemini Instead of OpenRouter?

The project was initially developed using the OpenRouter API because it provides access to multiple open-source LLMs through a single interface.

During implementation, repeated testing encountered temporary issues such as provider rate limits and upstream timeout errors on the free-tier endpoints. These issues were related to external API availability rather than the application logic.

To ensure a more stable and consistent integration, the project was migrated to the Google Gemini API.

The migration required only changes to the LLM communication layer. The overall project architecture, prediction pipeline, JSON validation, guardrails, and machine learning model remained unchanged.

This demonstrates that the application has been designed in a modular way, allowing different LLM providers to be integrated without changing the core prediction workflow.

---

# Error Handling

The notebook includes basic error handling for external API responses.

If the LLM returns malformed or incomplete JSON, the application:

- preserves the machine learning prediction,
- validates the response,
- and provides a fallback explanation instead of terminating execution.

This keeps the overall pipeline functional even when external API services experience temporary issues.

---

# How to Run

## 1. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 2. Configure Gemini API

Create a Google Gemini API key.

In Google Colab:

- Open **Secrets**
- Add

```
GEMINI_API_KEY
```

- Paste your API key
- Enable notebook access

---

## 3. Run the notebook

Open:

```
notebooks/Capstone_Project_Masai_Part4.ipynb
```

Run every cell from top to bottom.

---

# Conclusion

This project combines a supervised machine learning model with a Large Language Model to produce both predictions and human-readable explanations.

The trained Random Forest model performs the prediction task, while the Gemini API generates structured explanations that are validated using a predefined JSON schema.

The final application demonstrates a complete explainable AI pipeline, including feature encoding, prediction, guardrails, structured LLM output, validation, and end-to-end execution.