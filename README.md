# 📊 Revenue Growth Trend Analysis & 12-Month Forecasting

## 📌 Project Overview

This project analyzes 84 months of synthetic SaaS Monthly Recurring Revenue (MRR) data to understand revenue growth patterns, identify structural changes, compare statistical models, and forecast revenue for the next 12 months.

Using Python and statistical techniques, the project explores revenue trends across three business phases and develops a Logistic growth model combined with AR(1) residual modelling for forecasting.

> **Note:** This project uses synthetic data for educational and analytical purposes. It does not represent actual financial data from a real company.

## 🎯 Problem Statement

Understanding historical revenue growth and predicting future revenue are important for business planning. However, revenue growth patterns may change over time, and forecasting models may contain autocorrelated residuals.

This project aims to analyze historical MRR, identify structural breaks, compare different growth models, validate statistical assumptions, and generate a 12-month revenue forecast with prediction intervals.

## 🎯 Project Objectives

- Clean and prepare the revenue dataset.
- Analyze historical revenue trends and monthly growth rates.
- Compare revenue growth across different business phases.
- Calculate Compound Annual Growth Rate (CAGR).
- Examine time-series characteristics and stationarity.
- Fit and compare different statistical models.
- Identify structural breaks in revenue trends.
- Test differences in growth rates across phases.
- Diagnose and model residual autocorrelation.
- Forecast the next 12 months of revenue with prediction intervals.

## 🛠️ Tools & Technologies

- **Python** — Data processing, statistical analysis, modelling, and forecasting.
- **Pandas** — Data manipulation and preparation.
- **NumPy** — Numerical calculations.
- **Matplotlib** — Data visualization.
- **Seaborn** — Statistical visualization.
- **SciPy** — Statistical tests and nonlinear model fitting.
- **Statsmodels** — Statistical modelling, time-series diagnostics, and hypothesis testing.
- **Jupyter Notebook** — Interactive analysis and documentation.

## 📂 Dataset Overview

The project uses a synthetic SaaS revenue dataset containing customer-level records across 84 monthly periods.

### Key Variables

| Column | Description |
|---|---|
| `Month_Number` | Sequential month identifier |
| `Month_Date` | Revenue reporting month |
| `Phase` | Business growth phase |
| `Customer_ID` | Customer identifier |
| `Industry` | Customer industry |
| `Region` | Customer region |
| `Plan_Type` | Subscription plan |
| `Seats` | Number of customer seats |
| `Customer_Status` | Customer status |
| `MRR_Amount` | Customer-level monthly recurring revenue |
| `Total_Company_MRR` | Total company MRR for the month |
| `Active_Customer_Count` | Number of active customers |

**Primary analysis variable:** `Total_Company_MRR`

For company-level time-series analysis, customer-level records are aggregated into a monthly dataset containing one observation per month.

## 🔄 Project Methodology

### 1. Data Cleaning & Preparation

- Inspected dataset structure and data types.
- Identified and handled missing values.
- Removed duplicate records.
- Handled invalid values.
- Standardized date formats.
- Checked data quality and consistency.
- Prepared the monthly company-level dataset.

### 2. Exploratory Data Analysis (EDA)

- Calculated descriptive statistics.
- Examined revenue distribution.
- Visualized historical revenue trends.
- Calculated month-over-month growth rates.
- Compared revenue across business phases.
- Calculated phase-wise CAGR.
- Examined correlations between numerical variables.

### 3. Time-Series Diagnostics

**Autocorrelation Function (ACF)**
- Examined correlations between a time series and its past values.

**Partial Autocorrelation Function (PACF)**
- Examined direct relationships between observations at different lags.

**Augmented Dickey-Fuller (ADF) Test**
- Tested the null hypothesis that the series has a unit root.

**Kwiatkowski–Phillips–Schmidt–Shin (KPSS) Test**
- Tested the null hypothesis that the series is stationary under the selected specification.

**Time-Series Decomposition**
- Examined trend, seasonal, and residual components.

### 4. Statistical Model Fitting

Four models were compared to identify the model that best represented the historical revenue trend.

- Linear Regression
- Exponential Model
- Logarithmic Model
- Logistic Growth Model (S-Curve)

### 5. Model Evaluation

The models were compared using:

| Metric | Purpose |
|---|---|
| R² | Measures the proportion of variation explained by the model |
| MAE | Measures average absolute prediction error |
| RMSE | Measures prediction error while penalizing larger errors |
| RSE | Measures residual variation around the fitted model |
| AIC | Compares model fit while penalizing complexity |
| BIC | Compares model fit with a complexity penalty |

Prediction error metrics were compared on the original MRR scale.

### 6. Residual Diagnostics

- Examined residual plots for systematic patterns.
- Used the Durbin–Watson statistic to assess first-order residual autocorrelation.
- Examined residual ACF patterns.
- Investigated remaining residual dependence before forecasting.

### 7. Statistical Validation

**Chow Test**
- Tested for structural breaks at specified months.

**One-Way ANOVA**
- Tested whether mean monthly growth rates differed across the three phases.

**Tukey HSD**
- Identified which pairs of phases differed in their mean monthly growth rates.

### 8. Residual Modelling & Forecasting

- Fitted an AR(1) model to the Logistic model residuals.
- Used the Ljung–Box test to assess remaining residual autocorrelation.
- Combined the Logistic trend and AR(1) residual forecasts.
- Generated a 12-month revenue forecast.
- Calculated 80% and 95% model-based prediction intervals.

## 📈 Key Results

### Phase-Wise CAGR

| Business Phase | CAGR |
|---|---:|
| Phase 1 — Startup | 170.56% |
| Phase 2 — Rapid Expansion | 57.97% |
| Phase 3 — Maturation | 16.26% |

The calculated CAGR decreases across the three phases, indicating a slowdown in annualized revenue growth over the observed periods.

### Model Comparison

| Model | R² | MAE | RMSE |
|---|---:|---:|---:|
| Linear | 0.9814 | 7,137.11 | 8,192.62 |
| Exponential | 0.7122 | 19,807.59 | 32,200.95 |
| Logarithmic | 0.7485 | 26,434.45 | 30,100.93 |
| Logistic | 0.9990 | 1,550.04 | 1,865.98 |

**Selected trend model:** Logistic Growth Model (S-Curve)

The Logistic model achieved the highest R² and lowest MAE and RMSE among the four evaluated models on the original MRR scale. However, residual diagnostics identified autocorrelation, so the Logistic model was supplemented with AR(1) residual modelling.

### Structural Break Analysis

The Chow Test was conducted at two specified breakpoints.

| Breakpoint | F-Statistic | p-value |
|---|---:|---:|
| Month 24 | 152.98 | < 0.001 |
| Month 60 | 33.97 | < 0.001 |

Both tests indicate statistically significant structural changes at the specified breakpoints.

### Growth-Rate Significance

**One-Way ANOVA**
- F-statistic: 142.47
- p-value: < 0.001

The analysis identified statistically significant differences in mean monthly growth rates across the three phases.

**Tukey HSD:** All three pairwise phase comparisons were statistically significant at the 0.05 level.

### Residual Model Validation

- **AR(1) coefficient:** 0.8763
- **AR(1) coefficient p-value:** < 0.001
- **Ljung–Box statistic at lag 10:** 9.690
- **Ljung–Box p-value:** 0.468

The AR(1) coefficient indicates significant lag-1 residual dependence. The Ljung–Box test did not find statistically significant evidence of remaining autocorrelation at the tested lag structure.

### 12-Month Revenue Forecast

| Forecast Period | Forecasted MRR |
|---|---:|
| Month 85 | 188,853.42 |
| Month 90 | 194,021.34 |
| Month 96 | 198,790.53 |

The model projects an upward revenue trend over the 12-month forecast horizon.

The project also calculates **80% and 95% prediction intervals** to communicate forecast uncertainty.

> Forecasts are model-based estimates from synthetic data and should not be interpreted as actual company revenue or guaranteed future performance.

## 💡 Key Insights

- Revenue growth differs across the three defined business phases.
- Phase-wise CAGR decreases from Startup to Maturation.
- The Logistic model best fits the observed revenue trend among the four models evaluated.
- Chow Test results indicate structural breaks at the specified months.
- ANOVA and Tukey HSD indicate differences in mean monthly growth rates across phases.
- AR(1) modelling was used to account for residual dependence in the forecasting process.
- Prediction intervals provide an indication of uncertainty around future revenue estimates.

## ⚠️ Limitations

- The dataset is synthetic and does not represent actual company financial records.
- Model performance is evaluated on the observed historical data; high in-sample fit does not guarantee equivalent out-of-sample accuracy.
- Forecasts depend on the assumptions and limitations of the selected models.
- The model-based prediction intervals may not capture all uncertainty, including uncertainty in estimated Logistic model parameters.
- Business decisions should not rely on this forecast alone.

## 🚀 Future Improvements

- Evaluate forecast accuracy using a time-based holdout sample.
- Compare the results with alternative time-series forecasting models.
- Investigate potential seasonal effects.
- Incorporate customer churn, acquisition, and retention metrics.
- Evaluate forecast performance as new observations become available.

## 📌 Conclusion

This project demonstrates how Python and statistical techniques can be used to analyze historical revenue patterns, compare growth models, test structural changes, diagnose residual dependence, and forecast future MRR.

By combining Logistic trend modelling with AR(1) residual modelling, the project provides a structured approach to revenue forecasting and communicates uncertainty through prediction intervals.

## 👩‍💻 Skills Demonstrated

- Data Cleaning & Preprocessing
- Exploratory Data Analysis
- Statistical Hypothesis Testing
- Time-Series Analysis
- Regression & Nonlinear Modelling
- Residual Diagnostics
- Model Evaluation
- Revenue Forecasting
- Data Visualization
- Statistical Interpretation

---

**Project Type:** Python & Statistics  
**Domain:** SaaS Revenue Analytics  
**Dataset:** Synthetic  
**Forecast Horizon:** 12 Months

⭐ If you find this project useful, feel free to explore the repository and share your feedback.
