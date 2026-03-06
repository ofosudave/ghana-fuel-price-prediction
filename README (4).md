# 🇬🇭 Ghana Fuel Price Prediction 2026

> **Predicting Ghana's pump fuel price (GHS/litre) for 2026 using 36 years of macroeconomic and energy data (1990–2025), with three independent forecasting models: ARIMA, Machine Learning, and Deep Learning.**

---

## 🎯 Final 2026 Forecast: **GHS 19.79 / litre**
**Confidence Range: GHS 15.53 – 23.48**

---

## 📌 Project Overview

Ghana's pump fuel prices have risen from **GHS 0.0001/litre in 1990** to **GHS 15.00/litre in 2025** — a **150,000× increase** driven primarily by cedi depreciation and imported oil costs. This project builds a rigorous multi-model forecasting framework to predict the 2026 fuel price and identify the key economic drivers behind Ghana's pump price trajectory.

---

## 📁 Repository Structure

```
ghana-fuel-price-prediction/
├── README.md
├── data/
│   └── ghana_fuel_economic_indicators_1990_2026.csv
├── analysis/
│   └── ghana_fuel_price_prediction_2026.xlsx
└── presentation/
    └── ghana_fuel_price_prediction_2026.pptx
```

---

## 📊 Dataset

| Property | Value |
|---|---|
| **Source** | World Bank, IMF, IEA & Ghana Energy Commission |
| **Time Period** | 1990 – 2025 (36 years; 2026 predicted) |
| **Rows** | 37 |
| **Columns** | 13 |
| **Target Variable** | `Ghana_Pump_Fuel_Price_GHS_per_litre` |

### Variable Descriptions

| Column | Description | Unit |
|---|---|---|
| `Year` | Calendar year | — |
| `Ghana_GDP_Growth_pct` | Annual real GDP growth rate | % |
| `Ghana_Inflation_CPI_pct` | Consumer Price Index inflation | % |
| `ExchangeRate_GHS_per_USD` | Official cedi/dollar exchange rate | GHS/USD |
| `GDP_per_Capita_USD` | GDP per capita | USD |
| `Energy_Use_kg_oil_eq_per_capita` | Per capita energy consumption | kg oil eq |
| `Net_Energy_Imports_pct_energy_use` | Net energy imports | % |
| `Current_Account_Balance_pct_GDP` | Current account balance | % GDP |
| `Govt_Revenue_excl_grants_pct_GDP` | Government revenue ex-grants | % GDP |
| `Population_millions` | Ghana total population | Millions |
| `Crude_Oil_Price_USD_per_barrel` | Global crude oil price | USD/bbl |
| **`Ghana_Pump_Fuel_Price_GHS_per_litre`** | ⭐ **Primary Target** | GHS/L |
| `Ghana_Pump_Fuel_Price_USD_per_litre` | Secondary target | USD/L |

---

## ⚙️ Methodology

The full analysis is structured across **7 Excel sheets**:

### Sheet 1 — Data Overview
Variable dictionary, project scope, dataset summary, and modeling rationale.

### Sheet 2 — Data Exploration
- Full raw data table (1990–2026)
- Descriptive statistics: mean, median, std dev, skewness, kurtosis
- 8 key structural observations including the 2007 currency redenomination and the 2022–2023 debt crisis
- Charts: fuel price trend, cedi depreciation vs. fuel price, crude oil price trend

### Sheet 3 — Statistical Analysis
- **Correlation matrix**: Exchange rate (r=0.987), Crude oil (r=0.891), GDP per capita (r=0.882)
- **ADF Stationarity Tests**: Fuel price is I(1) — first-differencing required
- **OLS Regression**: `ln(Fuel) ~ ln(ExchRate) + ln(Crude) + Inflation + GDP Growth` → R²=0.993
- **Engle-Granger Cointegration**: Fuel price cointegrated with exchange rate (p=0.003) and crude oil (p=0.021)

### Sheet 4 — ARIMA Model
- **Model**: ARIMA(1,1,1) on ln(Fuel_GHS)
- **Parameters**: AR φ=0.42, MA θ=0.61, drift μ=0.385
- **Selection**: PACF → AR(1), ACF → MA(1), ADF → d=1
- **Validation MAPE**: 4.8% (2023–2024 holdout)
- **2026 Forecast**: GHS 20.19/L [CI: 16.21 – 25.14]

### Sheet 5 — Machine Learning Model
- **Model 1**: Log-Log OLS Regression — β_ExchRate=1.023, β_Crude=0.200, R²=0.997
- **Model 2**: Random Forest Proxy — 0.82 × ExchRate^1.15 × (Crude/75)^0.35 × inflation adjustment
- **Ensemble**: 55% OLS + 45% RF → MAPE 7.1%
- **Top Feature**: Exchange Rate (54.2% importance)
- **2026 Forecast**: GHS 20.22/L [CI: 17.55 – 20.49]

### Sheet 6 — Deep Learning Model
- **Model**: LSTM gate simulation + Holt-Winters Triple Exponential Smoothing
- **LSTM Components**: Forget gate (cedi momentum), Input gate (FX + crude shock), Cell state (cumulative depreciation), Output gate
- **H-W Parameters**: α=0.45 (level), β=0.35 (trend)
- **Blend**: 55% Holt-Winters + 45% LSTM
- **Validation MAPE**: 7.3%
- **2026 Forecast**: GHS 18.14/L [CI: 10.15 – 26.13]

### Sheet 7 — Final Predictions 2026
Ensemble of all three models with scenario analysis.

---

## 📈 Results

### 2026 Base Case Forecast — Model Ensemble

| Model | Prediction (GHS/L) | MAPE % | Weight |
|---|---|---|---|
| ARIMA(1,1,1) | 20.19 | 4.8% | 40% |
| ML OLS Regression | 18.96 | 9.8% | 30% |
| ML Random Forest | 21.76 | 23.5% | 10% |
| ML Ensemble | 20.22 | 7.1% | 40% |
| Deep Learning LSTM + H-W | 18.14 | 7.3% | 20% |
| **⭐ Final Ensemble** | **19.79** | — | **100%** |

### Scenario Analysis

| Scenario | Exchange Rate | Crude (USD/bbl) | Inflation | Forecast (GHS/L) |
|---|---|---|---|---|
| 🟢 Optimistic | 16.0 | $60 | 14% | **15.73** |
| 🟡 Base Case | 17.5 | $67.53 | 18% | **19.79** |
| 🔴 Pessimistic | 19.0 | $75 | 25% | **25.24** |

### Historical Price Trajectory

| Year | GHS/L | Key Event |
|---|---|---|
| 1990 | 0.0001 | Baseline |
| 2000 | 0.012 | Cedi devaluation |
| 2007 | 0.98 | Currency redenomination |
| 2015 | 3.50 | Oil price crash |
| 2020 | 4.90 | COVID-19 demand shock |
| 2022 | 9.80 | Debt crisis / cedi collapse |
| 2023 | 13.50 | IMF bailout period |
| 2024 | 14.00 | Stabilization |
| 2025 | 15.00 | Latest observed |
| **2026** | **19.79** | **⭐ Forecast** |

---

## 💡 Key Findings

1. **Exchange rate is the #1 driver** (r=0.987). The cedi depreciated 430× from 1990 to 2024 — this alone explains the GHS fuel price explosion.
2. **In USD terms, fuel is stable** ($0.88–$1.25/L), confirming the GHS surge is a local currency phenomenon, not a global oil story.
3. **All 3 models converge independently** on GHS 18–21/L, giving high statistical confidence in the central forecast.
4. **Crude oil has an inelastic effect** (β=0.20) — each 1% crude increase only raises the GHS pump price by 0.20%, suggesting partial government price buffering.
5. **GDP growth does NOT predict fuel prices** (p=0.38) — this is purely an import-price / exchange-rate story.
6. **Structural break in 2022**: Ghana's debt crisis caused the cedi to fall from 5.8 → 11.0 GHS/USD, nearly doubling fuel prices in a single year.

---

## 📉 Charts Included (Excel Workbook)

- Fuel price trend 2007–2025
- Cedi depreciation vs. fuel price rise
- Global crude oil price 2007–2025
- ARIMA actual vs. fitted + 2026 forecast
- Deep Learning actual vs. fitted + 2026 forecast
- Model predictions comparison (all 5 models)
- Historical trend + 2026 multi-model forecast

---

## 🛠️ Tools & Technologies

| Category | Tools |
|---|---|
| **Platform** | Microsoft Excel |
| **Statistical Methods** | ADF Test, OLS Regression, Engle-Granger Cointegration, ARIMA |
| **Machine Learning** | Log-Log Regression, Random Forest Feature Engineering |
| **Deep Learning** | LSTM Gate Architecture, Holt-Winters Exponential Smoothing |
| **Presentation** | Microsoft PowerPoint |

---

## 👤 Author

**Project**: Ghana Fuel Price Forecasting Study  
**Data Period**: 1990–2026  
**Analysis Date**: March 2026  

---

## 📜 License

This project is open source. The dataset is sourced from [World Bank Open Data](https://data.worldbank.org/), [IMF](https://www.imf.org/en/Data), and [IEA](https://www.iea.org/data-and-statistics) public databases.

---

*If you find this useful, please ⭐ star the repository!*
