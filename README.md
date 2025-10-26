
# 📊 RBI Liabilities and Assets Analysis & Forecasting

## 🧩 Overview
This project analyzes and forecasts the **Reserve Bank of India’s (RBI)** weekly balance sheet components — focusing on **Liabilities** and **Assets** over time.  
It explores key relationships between different financial entities (like Deposits and Loans), identifies historical trends, and uses **time-series forecasting models (ARIMA)** to predict future values.

The analysis provides an understanding of how various components of the RBI’s balance sheet evolve, interact, and influence monetary stability.

---

## 📁 Dataset Description

**Source:**  
Official RBI Database — *Weekly Statistical Supplement (WSS)* published by the [Reserve Bank of India](https://rbi.org.in/).

**File:** `RBI_Liabilities and Assets.csv`

Each row represents the **week-ended balance sheet** data (usually every Friday).

**Key Columns:**

| Category | Column | Description |
|-----------|---------|-------------|
| 🪙 **Notes** | `A1_Notes_in_Circulation`, `A2_Notes_Held_in_Banking_Department` | Currency in circulation and held by RBI |
| 💰 **Deposits (B)** | `B1_Deposits_Central_Government`, `B3_Deposits_State_Governments`, `B4_Deposits_Scheduled_Commercial_Banks`, `B5_Deposits_Scheduled_State_Cooperative_Banks`, etc. | Deposits maintained with RBI by various institutions |
| ⚖️ **Liabilities** | `C_Other_Liabilities`, `D_Total_Liabilities_OR_Assets` | Overall liabilities and assets on the RBI balance sheet |
| 💎 **Assets (D)** | `D1_Foreign_Currency_Assets`, `D2_Gold`, `D3_Rupee_Securities` | Composition of RBI’s asset holdings |
| 🏦 **Loans & Advances (E)** | `E1_Loans_Central_Government`, `E2_Loans_State_Governments`, `E4_Loans_Scheduled_Commercial_Banks`, `E5_Loans_Scheduled_State_Cooperative_Banks`, etc. | Loans extended by RBI to various entities |
| 📈 **Investments & Others** | `F_Investments`, `G_Other_Assets` | Investments and miscellaneous assets |
| 📅 **Date** | `Week_Ended` *(set as index)* | Date of the weekly report |

---

## 🧠 Project Objectives

1. **Data Cleaning & Preprocessing**
   - Handle missing values and format monetary figures
   - Set `Week_Ended` as the date index for time-series operations

2. **Exploratory Data Analysis (EDA)**
   - Identify relationships such as:
     - **B1 vs E1:** Central Government Deposits vs Loans  
     - **B3 vs E2:** State Government Deposits vs Loans  
     - **B4 vs E4:** Commercial Banks Deposits vs Loans  
     - **B5 vs E5:** Cooperative Banks Deposits vs Loans  
   - Visualize overall trends using line plots and moving averages
   - Compare **D1 vs D2 vs D3** (Foreign Currency, Gold, and Rupee Securities)
   - Compare **A1 vs A2** (Notes in Circulation vs Held in Banking Department)

3. **Forecasting Future Trends**
   - Built **ARIMA-based forecasting models** for major variables
   - Predicted the next **12 weeks** of values
   - Visualized historical and future trends with confidence intervals

---

## 🔮 Forecast Models

Each target column (e.g., `B1_Deposits_Central_Government`) is modeled as a **univariate time series**.  
The pipeline:

```python
# Example: Forecast for B1_Deposits_Central_Government
target = 'B1_Deposits_Central_Government'
series = df[target]
series.index = pd.to_datetime(series.index)

forecast_B1, model_B1 = forecast_arima(series, steps=12)
```

**Model Details:**
- Base Model: `statsmodels` ARIMA(p, d, q)
- Steps Ahead: 12 (next 12 weeks)
- Evaluation: AIC / Residual plots
- Output: Forecast plots showing future estimates vs actual trend

---

## 📊 Key Visual Analyses

1. **Deposits vs Loans Relationships**
   - Correlation and trend comparison between respective entities (B1–E1, B3–E2, etc.)
   - Insights into liquidity movements between governments and the banking system

2. **Foreign Reserves Composition**
   - Comparative analysis of `D1`, `D2`, `D3`  
     → Shows RBI’s balance between **foreign currency assets**, **gold**, and **rupee securities**

3. **Currency Circulation Trends**
   - `A1` vs `A2` illustrates how much currency is in active circulation vs retained by the RBI

4. **Forecast Visualization**
   - 12-week projections for key variables
   - Trend continuation and anomaly detection

---

## 🧮 Tools & Libraries

- **Python**
- **pandas**, **numpy** – Data preprocessing & analysis  
- **matplotlib**, **seaborn** – Visualization  
- **statsmodels**, **pmdarima** – Time series modeling  
- **scipy** – Statistical analysis  

---

## 🏁 Results & Insights

- Strong correlation observed between **Deposits and Loans** across sectors  
- **B1–E1** shows a cyclical relationship — government deposits decrease when loan advances rise  
- **Foreign Currency Assets (D1)** form the largest share among assets  
- **Gold (D2)** shows steady growth, aligning with RBI’s diversification policies  
- Forecasts indicate:
  - Moderate increase in total deposits and foreign assets  
  - Stable but slightly upward trend in notes in circulation

---

## 📚 Future Scope

- Extend model using **SARIMA** or **Prophet** for seasonal effects  
- Add **multivariate models** to include macroeconomic indicators (inflation, repo rate)  
- Build a dashboard using **Plotly Dash / Streamlit** for interactive visualization  

---

## 🏦 Reference

- **Data Source:** [Reserve Bank of India – Weekly Statistical Supplement](https://rbi.org.in/Scripts/BS_ViewWss.aspx)  
- **Project Author:** Aneerban Chowdhury  
- **Tools Used:** Python, pandas, matplotlib, statsmodels  
- **Dataset Frequency:** Weekly  
