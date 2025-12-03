# DS340W-Project-by-Hyun-Woo-Jang
This repo uses the input datasets from the Kaggle notebook


📈 Evaluating the Impact of Macroeconomic Indicators on ML-Based Stock Trend Prediction
DS 340W — Final Research Project

Author: Hyunwoo Jang
Email: hfj5102@psu.edu

Institution: Penn State University, Data Science

📝 1. Project Overview

This project extends a machine-learning-based quantitative trading framework by investigating whether macroeconomic indicators improve the prediction of short-term stock trends.

The study compares:

① Technical Indicators Only (32 features)

vs

② Technical Indicators + 5 Macroeconomic Indicators (37 features)

All predictions target the direction (up/down) of
MA5, MA10, MA20 (next day).

The study period is:

Parent Paper: 2017–2021 (stable regime)

Our Study: 2020–2025 (volatile regime: COVID, inflation, rate hikes)

The goal is to determine:

Do macroeconomic indicators meaningfully improve short-term moving-average predictions?

📂 2. Repository Structure
📁 data/
    ├── features/
    │     ├── only_features/           # 32 technical indicator datasets
    │     └── features_with_ME/        # 32 technical + 5 macro indicators
    └── macro_raw/ (optional)

📄 DS340W_Final.ipynb                   # Full pipeline + macro/no-macro analysis
📄 DS340W_code_no_macro.ipynb          # Technical-only model pipeline
📄 DS340W_code_macro.ipynb             # Macro-enhanced pipeline
📄 PPT.pptx                             # Final presentation slides
📄 paper.docx                           # Final research paper (IEEE style)

README.md

📊 3. Data Description
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
Indicator	Meaning
FFR_Level	Federal Funds Rate
CPI_YoY	Inflation
UNRATE_Level	Unemployment Rate
YC_Slope_10Y3M	Yield Curve Slope
PMI_Level	Purchasing Managers' Index

Macroeconomic data (monthly) is forward-filled to align with daily stock data.

🤖 4. Machine Learning Models

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

🎯 5. Target Labels

Predict:

MA5_dir

MA10_dir

MA20_dir

Labeling rule:

Next day's MA > Today's MA → +1  
Next day's MA < Today's MA → -1

🧪 6. Experimental Design

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

📈 7. Key Results
7.1 Macro vs No-Macro (MAE Comparison)

MAE differences were extremely small (mostly within ±0.02).

No model consistently improved with macro features.

Macro variables are too slow-moving to predict daily MA flips.

Conclusion:
Macroeconomic indicators do not improve short-term MA prediction.

7.2 Macro vs No-Macro (Trading Returns)

Returns changed very little between technical-only and macro settings.

Max Drawdowns also nearly identical.

Because accuracy barely changed, returns barely changed.

7.3 2017–2021 vs 2020–2025

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

7.4 Drawdown Analysis

−10% drawdowns nearly doubled across all tickers.

−30% drawdowns went from rare → extremely common in 2020–2025.

MA signals break when trends shorten + volatility rises.

🧩 8. Final Conclusions
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

🛠 9. How to Run the Code
Install dependencies
pip install -r requirements.txt


(or the conda equivalent)

Run full analysis
jupyter notebook DS340W_Final.ipynb

📧 10. Contact

For questions or collaboration:

Hyunwoo Jang
hfj5102@psu.edu

Penn State University — Data Science
