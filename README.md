# DS340W-Project-by-Hyun-Woo-Jang
This repo uses the input datasets from the Kaggle notebook


# 📈 Evaluating the Impact of Macroeconomic Indicators on ML-Based Stock Trend Prediction
DS 340W — Final Research Project

## Author: Hyunwoo Jang
## Email: hfj5102@psu.edu

Institution: Penn State University, Data Science

# 📝 1. Project Overview

This project extends a machine-learning-based quantitative trading framework by investigating whether macroeconomic indicators improve the prediction of short-term stock trends.

The study compares:

## ① Technical Indicators Only (32 features)

vs

## ② Technical Indicators + 5 Macroeconomic Indicators (37 features)

All predictions target the direction (up/down) of
MA5, MA10, MA20 (next day).

The study period is:

Parent Paper: 2017–2021 (stable regime)

Our Study: 2020–2025 (volatile regime: COVID, inflation, rate hikes)

The goal is to determine:

Do macroeconomic indicators meaningfully improve short-term moving-average predictions?

# 📊 2. Data Description
Stocks Included

Eight major U.S. technology stocks:
AAPL, MSFT, NVDA, AMD, ORCL, ADBE, CRM, NOW

Technical Indicators (32)

Examples:
Trend: MA5, MA10, MA20, EMA5, EMA10, EMA20
Momentum: RSI12, ROC5/10/20, MACD, MACDsignal, MACDhist
Volume: OBV, Volume_inc
Volatility: ATR14, BBU20, BBL20
Others: CCI10, STOCHk3, STOCHd3, etc.

Macroeconomic Indicators (5)

FFR_Level	Federal Funds Rate
CPI_YoY	Inflation
UNRATE_Level	Unemployment Rate
YC_Slope_10Y3M	Yield Curve Slope
PMI_Level	Purchasing Managers' Index

Macroeconomic data (monthly) is forward-filled to align with daily stock data.

# 🤖 3. Machine Learning Models

We evaluate 8 models:

Traditional Models

Decision Tree Regressor
Support Vector Regressor (Linear)
Bagging Regressor
Random Forest Regressor
AdaBoost Regressor
CatBoost Regressor

Modern Boosting Models

XGBoost Classifier
LightGBM Classifier

All regressors produce continuous outputs → converted to:

+1 (up) if prediction > 0
–1 (down) otherwise

# 🎯 4. Target Labels

Predict:

MA5_dir
MA10_dir
MA20_dir

Labeling rule:

Next day's MA > Today's MA → +1  
Next day's MA < Today's MA → -1

# 🧪 5. Experimental Design

✔ Time-aware split (80% train, 20% test)
✔ StandardScaler fit only on training data
✔ Two experimental settings:

Technical-only

Technical + Macro
✔ Evaluate accuracy + MAE/MSE/RMSE/R²
✔ Perform simple backtests:

Long when prediction = +1

Exit when prediction = –1
✔ Compare market regimes (2017–2021 vs 2020–2025)
✔ Analyze volatility & drawdowns

# 📈 6. Key Results
## 6.1 Macro vs No-Macro (MAE Comparison)

MAE differences were extremely small (mostly within ±0.02).
No model consistently improved with macro features.
Macro variables are too slow-moving to predict daily MA flips.

Conclusion:
Macroeconomic indicators do not improve short-term MA prediction.

## 6.2 Macro vs No-Macro (Trading Returns)

Returns changed very little between technical-only and macro settings.
Max Drawdowns also nearly identical.
Because accuracy barely changed, returns barely changed.

## 6.3 2017–2021 vs 2020–2025

When comparing the same technical-only model pipeline:
Parent paper showed strong accuracy & high returns (stable uptrend)
Our period (2020–2025) showed weaker accuracy & lower returns

Why?

Market Regime Shift:

COVID shock (2020)
Inflation spike (2021–2022)
Interest rate hikes (2022–2023)
Tech corrections (2022–2023)
Multiple deep drawdowns

MA-based models rely on smooth trends, but 2020–2025 had rapid reversals → accuracy drops.

## 6.4 Drawdown Analysis

−10% drawdowns nearly doubled across all tickers.

−30% drawdowns went from rare → extremely common in 2020–2025.

MA signals break when trends shorten + volatility rises.

# 🧩 7. Final Conclusions
1. Macroeconomic indicators did NOT improve predictions.
Their slow monthly frequency mismatches daily MA signals.

2. Returns were effectively unchanged.
Predictive accuracy drives trading returns — and accuracy didn’t improve.

3. The true reason for performance collapse: market regime.
2017–2021: stable uptrend → easy to predict
2020–2025: volatile + choppy → hard to predict

4. Trend-following indicators (MA5/10/20) fail in unstable markets.
5. Future Work

Regime classification models
Volatility state prediction
Sentiment & order-flow features
Longer-horizon macro forecasting

# 🛠 8. How to Run the Code

## Step 1 — Download required data

The repository requires the full dataset inside the data/ folder.
Inside data/features/, there are two versions of feature datasets:

### 1. features/only_features/

Contains datasets with 32 technical indicators only
Used for the no-macro baseline experiment

### 2. features/features_with_ME/

Contains datasets with 32 technical + 5 macro indicators
Used for the macro-enhanced experiment

# 📌 Important:
Make sure you download the entire data/ directory (including both feature folders) before running any notebook.

# Step 2 — Install dependencies

If using pip:
pip install -r requirements.txt

If using conda:
conda env create -f environment.yml
conda activate ds340w

# Step 3 — Run notebooks in the correct order

Because each notebook builds on the previous step,
the correct execution order is:

## ✅ 1) DS340W_code_no_macro.ipynb

Runs the technical-only model pipeline
(32 features, no macroeconomic indicators)

Outputs:

Baseline MAE
Baseline accuracy
Baseline trading returns

## ✅ 2) DS340W_code_macro.ipynb

Runs the macro-enhanced pipeline
(32 technical + 5 macro indicators)

Outputs:

Baseline MAE
Baseline accuracy
Baseline trading returns

## ✅ 3) DS340W_Final.ipynb (full analysis)

Combines all results and performs:

MAE summary
Trading performance summary
Market regime analysis
Drawdown heatmaps

Final conclusions

This notebook produces all the figures used in the presentation and final paper.
