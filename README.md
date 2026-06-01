# Time-Series Forecasting Pipeline

End-to-end pipeline for predicting monthly mortgage closure volumes in a Swiss
online banking channel, using interest rate indicators and market factors as
predictors for proactive capacity planning.

> **Best result: R² 0.764, MAE 3.29, error rate 18.88%** with Optuna-optimized Ridge Regression.
> Structural analysis revealed two distinct customer channels, leading to
> separate specialized models that better reflect each channel's dynamics.

---

## Results

Optuna-optimized models under expanding-window validation:

| Model | R² | MAE | Error rate |
|---|---|---|---|
| Ridge Regression | **0.764** | **3.29** | **18.88%** |
| Lasso Regression | 0.705 | 3.57 | 21.05% |
| XGBoost | 0.617 | 4.10 | 23.52% |
| Linear Regression | 0.504 | 4.63 | 26.72% |
| SARIMAX | 0.466 | 4.97 | 29.24% |

---

## Approach

| Stage | What was done |
|---|---|
| **Feature selection** | Five methods compared: Mutual Information, SelectKBest, RFE, Lasso, Random Forest |
| **Baseline modelling** | Five model families under 80/20 split and expanding-window validation |
| **Hyperparameter optimization** | Optuna for feature refinement and parameter search across all models |
| **Model interpretation** | SHAP analysis and what-if scenarios for actionable business insights |

---

## Key Findings

**Ridge Regression outperforms all other model families.** Under Optuna-optimized
expanding-window validation, Ridge achieves R² 0.764 and MAE 3.29, outperforming
XGBoost (R² 0.617) and SARIMAX (R² 0.466). The L2 regularization in Ridge handles
multicollinearity in the interest rate features more effectively than the other approaches.

**Channel structure matters more than model complexity.** Exploratory analysis
revealed that two customer channels behave structurally differently. Splitting into
channel-specific Ridge models improved interpretability and produced more stable
forecasts than a single combined model.

**SARON surcharge and rent price index are the strongest predictors.** SHAP analysis
identified the SARON reward surcharge (Lag1) and rent price index (Lag3) as the
features with the largest influence on predicted volume, providing concrete and
actionable levers for demand management.

**Expanding-window validation is essential for honest time-series evaluation.**
The 80/20 static split significantly overestimates real-world performance. Expanding window validation, which mirrors the actual deployment scenario, produces a more
reliable estimate of production accuracy.

---

## Visualisations

Ridge Regression forecast vs. actual monthly closure volumes. R² 0.764, MAE 3.29,
error rate 18.88% under Optuna-optimized expanding-window validation.

<img src="assets/forecast_ridge.png" alt="Ridge Regression forecast vs actual" width="900">

SHAP feature importance for the Ridge model on the Brokermarket/Swissfex channel.
The SARON reward surcharge (Lag1) has the strongest individual influence on predicted
closure volume, followed by the rent price index (Lag3) and working days.

<img src="assets/shap_ridge.png" alt="SHAP feature importance Ridge model" width="900">

---

## Data

The dataset included in this repository is synthetic and provided only to demonstrate
the pipeline in a runnable form. Because the data is not real, the metrics and forecasts
are illustrative only. To obtain meaningful results, replace the input data with a real
dataset in the same format as `data/data.csv`.

The plots in `reports/figures/` were generated from this synthetic dataset and are
illustrative pipeline outputs only. The visualisations in `assets/` show results from
the real dataset and reflect the actual model performance reported above.

---

## Notes

Expanding-window validation was used as the primary evaluation setup to reflect the
sequential nature of monthly forecasting. The 80/20 static split is included for
comparison only and is not recommended for production evaluation of time-series models.
