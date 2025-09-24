# Challenge with Options Data Trading Strategy  

This project presents a **machine learning–driven options trading strategy**, focusing on the **NIFTY BANK index** (July 2023 – December 2023). The strategy leverages option chain data, regression and classification models, and feature engineering to generate reliable buy/sell trading signals while managing risk effectively.  

---

## 📊 Data Acquisition & Preprocessing  

- **Source**: NIFTY BANK index data (6 months) + `yfinance` library.  
- **Missing Values**:
  - Filled `No. of contracts`, `Open Int`, and `Change in OI` with `0`.  
  - Filled `Open`, `High`, and `Low` with the corresponding day’s `Close`.  
- **Outlier Handling**:
  - Introduced **Normalized Close = Close Price / Strike Price**.  
  - Removed 1,416 outliers from 37,904 training data points using IQR.  

---

## 🛠 Feature Engineering  

Key features designed for predictive modeling:  

- **EMA Returns** – Profit/loss from Exponential Moving Average–based signals.  
- **EMA Put-to-Call Ratio** – Smoothed sentiment indicator using EMA.  
- **Implied Volatility (Calls & Puts)** – Expected volatility derived via Black-Scholes.  
- **Implied Volatility Spread** – Difference in implied volatility across options.  
- **Option-Index Volume Ratio (OS Volume)** – Relative measure of option vs index activity.  

👉 Features showed **low correlation**, ensuring each contributed unique predictive power.  

---

## 🤖 Models Used  

- **CatBoost Classifier**  
  - Outputs: `1` (price up next day), `0` (price down).  
- **Regressor Trees**  
  - Outputs magnitude of predicted returns.  

**Enhancements vs prior research**:  
- Added **OS Volume** feature.  
- Used **CatBoost** instead of AdaBoost (better performance).  
- Introduced **Regressor Trees** for return magnitude prediction.  
- Incorporated **buy threshold** for stricter risk control.  

---

## 📈 Strategy Logic  

- **Buy Condition**:  
  - CatBoost → predicts positive return (`1`).  
  - Regressor Trees → predicted magnitude > **Buy Threshold (0.001)**.  

- **Sell Condition**:  
  - CatBoost → predicts negative return (`0`).  
  - Or if **Stop Loss (2%)** is triggered.  

---

## 💡 Risk Management  

- **Stop Loss**: 2% per trade.  
- **Buy Threshold**: Prevents weak-signal trades.  

---

## 📉 Backtesting Results  

- **Profit**: **7.83%**  
- **Max Drawdown**: **8.75%**  
- **Sharpe Ratio**: **1.49**  
- **Total Trades**: **27**  

---

## 🚀 Future Improvements  

- Incorporate deep learning–based sequence models (LSTMs/Transformers).  
- Enhance volatility modeling with advanced GARCH-type features.  
- Expand to multi-index and cross-asset strategies.  

---

## 🙏 Acknowledgments  

- Inspired by a research paper from Stanford University on stock returns vs option chain data.
