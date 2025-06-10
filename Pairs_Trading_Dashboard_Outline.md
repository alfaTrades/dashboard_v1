
# 📊 Pairs Trading Dashboard Outline

## 🎯 Purpose:
A comprehensive dashboard that enables traders to analyze **mean-reverting relationships** between any two assets (e.g., Gold and Silver), using statistical methods and visual tools to support **pairs trading strategies**.

---

## 🧩 Dashboard Sections

### 1. 🔧 User Input Panel
- Asset 1 Ticker (e.g., `GLD`)
- Asset 2 Ticker (e.g., `SLV`)
- Date Range Selector
- Rolling Window Length (default: 30 days)
- Z-score Thresholds (default: ±2)
- Data is fetched via financial APIs (e.g., `yfinance`).

---

### 2. 📈 Raw Price Series Plot
- Dual line chart of Asset 1 and Asset 2 prices over time
- Toggle for log-scale

---

### 3. 🔍 Price Ratio Analysis
- Compute: `Asset1 / Asset2`
- Plot:
  - Ratio over time
  - Rolling mean
  - ±1 and ±2 standard deviation bands
- Display current ratio and Z-score

---

### 4. 🧮 OLS Regression & Hedge Ratio
- Show regression: `Asset1 = α + β × Asset2 + ε`
- Display:
  - Beta (hedge ratio)
  - R² value
- Option for rolling regression

---

### 5. 📉 Spread Analysis
- Compute spread: `Asset1 - β × Asset2`
- Plot:
  - Spread over time
  - Mean and ±2σ bands
  - Entry/exit signal highlights

---

### 6. 📊 Z-score of Spread
- Plot:
  - Z-score of spread
  - ±1 and ±2 bands
  - Annotated trade signals

---

### 7. 🔄 Rolling Correlation
- Rolling correlation of daily returns
- Window: 30–90 days
- Helps identify structural breaks

---

### 8. 🧪 ADF Test & Cointegration
- ADF test on spread and price ratio
- Display:
  - ADF statistic
  - p-value
  - Stationarity decision
- Optional: Johansen test for multivariate analysis

---

### 9. 🕰️ Half-Life of Mean Reversion
- Estimate via AR(1): `ln(2) / (1 - ρ)`
- Display:
  - Half-life in days
  - Interpretation for trade timing

---

### 10. 🧠 Hurst Exponent
- Value between 0 and 1
- Interpretation:
  - < 0.5 = mean-reverting
  - > 0.5 = trending

---

### 11. 📌 Trade Signal Summary Table
- Historical trades based on Z-score thresholds
- Columns:
  - Date
  - Z-score
  - Trade Type
  - Entry & Exit Dates
  - PnL (if backtesting enabled)

---

### 12. 📤 Download / Export
- CSV export of metrics
- PNG/HTML export of charts
- Save/Reload session

---
