# Bachelor Thesis ML Pipeline

## Project goal

This repository presents a **public demo version of my bachelor thesis machine-learning workflow**. The project focuses on **time-series forecasting** and was designed to predict the **total number of closures for the next month** using a structured modelling pipeline.

The main objective was not only to build forecasting models, but also to compare different feature-selection strategies, validation setups, and model families in a reproducible and interpretable way.

## Why this project matters

Forecasting tasks in business settings require more than fitting a single model once. A useful workflow should include careful feature selection, appropriate validation design, model comparison, and transparent evaluation.

This repository demonstrates an academic forecasting pipeline that goes beyond a simple notebook experiment. It shows how different modelling decisions affect performance and how a forecasting workflow can be organized in a structured, end-to-end manner.

## What this repository demonstrates

- structured academic machine-learning workflow
- time-series forecasting for a monthly target
- feature selection and feature comparison
- baseline modelling across multiple model families
- comparison of static split and expanding-window validation
- automated hyperparameter optimization with Optuna
- reproducible notebook-based experimentation
- clear separation of configuration, data, notebooks, and generated figures

## Data disclaimer

The dataset included in this repository is **not real**. It is a **synthetic / dummy dataset** provided only to demonstrate the pipeline in a public and runnable form.

Because the data is not real, the generated outputs, metrics, and forecasts are **illustrative only** and should not be interpreted as meaningful business results. Example plots generated from the dummy data are stored under `reports/figures`.

To obtain realistic results, the input data would need to be replaced with a real dataset in the same format, or the preprocessing pipeline would need to be adapted accordingly.

## Methodology

The forecasting workflow consists of four main stages.

### 1. Feature selection

Multiple feature-selection approaches were applied and compared to identify relevant predictors for the forecasting task:

- Mutual Information
- SelectKBest
- Recursive Feature Elimination (RFE)
- Lasso Regression
- Random Forest
- correlation heatmap for feature comparison

### 2. Model comparison and validation

The following forecasting models were evaluated throughout the study:

- Linear Regression
- Ridge Regression
- Lasso Regression
- SARIMAX
- XGBoost

These models were compared under two validation setups:

- **standard 80/20 split** for an initial baseline comparison
- **expanding-window validation** to better reflect the sequential nature of time-series forecasting

### 3. Hyperparameter optimization with Optuna

Optuna was used to improve model configurations and compare optimized versions of the same forecasting models under the expanding-window setup.
## Repository structure

```text
Bachelor-Thesis-ML-pipeline/
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── configs/
│   └── config.yaml
├── data/
│   └── data.csv
├── notebooks/
│   ├── 01_Feature Selection.ipynb
│   ├── 02_Baseline modelling with 80,20 split.ipynb
│   ├── 03_Baseline modelling with expanding window.ipynb
│   └── 04_Optuna modelling with expanding window.ipynb
└── reports/
    └── figures/
```
## Status
Completed public demo version of the bachelor thesis workflow. The repository contains the notebook-based pipeline, synthetic demonstration data, configuration files, and example output figures for a reproducible academic showcase.
