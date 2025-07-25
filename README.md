# Portfolio_Investment_Strategy

This project develops a **systematic long-short equity strategy** that predicts monthly stock excess returns and constructs dynamically rebalanced portfolios based on machine learning signals. The strategy is evaluated out-of-sample from **2010 to 2023** and consistently outperforms the S&P 500 benchmark.

## 🚀 Project Summary

We implement multiple models to forecast stock-level excess returns and earnings surprises, then design hybrid scoring signals to rank stocks each month. Top and bottom-ranked stocks are selected into **long** and **short** portfolios respectively. The strategy is tested under both **equal-weighted** and **market-value-weighted** constructions with dynamic rebalancing logic.

## 🧠 Models and Methodology

### Return Prediction Models:
- OLS / OLS Reduced
- Ridge / Lasso / Elastic Net
- XGBoost
- Autoencoder + Ridge
- Instrumented PCA (IPCA)

> **Expanding window setup** is used:  
> - 8 years training  
> - 2 years validation  
> - 1 year test  
> - Rolling 14 times (2010–2023)

### Earnings Surprise Model:
- Built separately using Lasso with automatic feature selection
- Forward-looking surprise signals are combined with return forecasts

## 💼 Portfolio Construction

- **Equal-Weighted Strategy**: Select top 50 long and bottom 50 short
- **Market-Weighted Strategy**: Same stocks, scaled by firm market equity

### Rebalancing Rule:
- Portfolio updated only when **signal spread ≥ 20th percentile** of historical spreads
- Otherwise, previous month's portfolio is reused (low turnover)

### Signal Design:
- **Equal-Weighted**: `0.7*(Return+Surprise) + 0.3*(Return×Surprise)`
- **Market-Weighted**: `1.5*Return + 0.3*(Return×Surprise)`

## 📊 Results Highlights

| Metric                  | Equal-Weighted | Market-Weighted | S&P 500 |
|------------------------|----------------|------------------|---------|
| **Annual Return**      | 17.80%         | 16.17%           | 11.52%  |
| **Sharpe Ratio**       | 0.91           | 0.96             | 0.72    |
| **Annual Alpha (CAPM)**| 20.8%          | 17.5%            | 0.0%    |
| **Max Drawdown**       | –38.9%         | –23.8%           | –24.8%  |
| **Turnover**           | 34.6%          | 37.6%            | N/A     |

- Equal-weighted strategy achieves higher return and alpha  
- Market-weighted strategy offers better downside control and smoother returns

## 🗂️ Folder Structure (Typical)

Portfolio_Investment_Strategy/
├── data/ # Raw and processed firm + macro data
├── models/ # Model training and prediction scripts
├── results/ # Stored predictions and portfolio weights
├── evaluation/ # Backtest and performance analysis
├── utils/ # Feature generation and data loading
├── notebooks/ # Exploratory and summary notebooks
└── README.md # Project description (this file)


## 🔍 Key Insights

- Combining earnings surprise with return models (additive + multiplicative) improves cross-sectional spread and portfolio alpha
- Rebalancing only when signals are strong reduces noise and turnover
- Strategy benefits from macro cycles: QE, COVID rebound, rising rate regime

## 📌 Future Improvements

- Incorporate quarterly return targets for better alignment with earnings
- Model ensembling (weighted average of Ridge, Lasso, OLS)
- Risk factor exposure control (e.g., size, value)
- Use nonlinear surprise models (e.g., gradient boosting, transformers)

---

📎 *See `Portfolio_Investment_Strategy.pdf` for full presentation and performance charts.*
