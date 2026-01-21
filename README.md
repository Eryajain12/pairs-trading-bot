# Pairs Trading Algorithmic Bot (Statistical Arbitrage)

## Overview
This project implements a **Python-based algorithmic trading bot** that executes a **Pairs Trading strategy**, a classical statistical arbitrage approach that exploits **mean-reverting relationships between cointegrated equities**.

The bot identifies statistically valid trading pairs using **cointegration testing**, generates trading signals based on **Z-score deviations**, and evaluates performance through **historical backtesting and paper trading simulations**.

The project integrates **time-series econometrics, object-oriented programming, and risk-aware trading system design**, making it suitable for **quantitative finance, risk analytics, and trading roles**.

---

##  Strategy Methodology

### Cointegration Testing
- Uses the **Engle–Granger two-step method**
- Performs linear regression on asset price series
- Applies the **Augmented Dickey–Fuller (ADF) test** on regression residuals
- Trades only pairs with statistically significant cointegration (**p-value ≤ 0.05**)

This ensures the spread between assets is **stationary and mean-reverting**, a necessary condition for pairs trading.

---

### Z-Score–Based Signal Generation

The spread is normalized using the Z-score:

$$
Z_t = \frac{X_t - \mu}{\sigma}
$$

Where:
- $X_t$ = Current spread  
- $\mu$ = Historical mean of the spread  
- $\sigma$ = Historical standard deviation  

**Trading Rules**
- **Z > +2** → Short the spread  
- **Z < −2** → Long the spread  
- **Z ≈ 0** → Close positions  

Entry thresholds are motivated by the **95% empirical rule**, balancing trade frequency and signal quality.

---

##  Key Features
- Object-oriented design via a `PairsTradingBot` class
- Automated data retrieval using Yahoo Finance
- Robust error handling and API throttling
- Historical backtesting framework
- Paper trading simulation to approximate live portfolio behavior
- Performance evaluation using ROI, Sharpe Ratio, Max Drawdown
- Detailed logging of trades and portfolio evolution
- Visualizations for Z-score dynamics and portfolio performance

---

## Risk-Based Impact Score (RBIS)

To complement traditional performance metrics, the strategy introduces a **Risk-Based Impact Score (RBIS)** — a composite measure designed to evaluate **risk-adjusted effectiveness** rather than raw returns alone.

RBIS integrates **return, volatility, and downside risk** into a single interpretable metric, enabling consistent comparison across asset pairs and strategy configurations.

### RBIS Definition

$$
\text{RBIS} = \frac{\text{ROI} \times \text{Sharpe Ratio}}{\text{Max Drawdown}}
$$

Where:
- **ROI** = Total return over the backtest period  
- **Sharpe Ratio** = Risk-adjusted return  
- **Max Drawdown** = Maximum peak-to-trough portfolio loss  

---

### Interpretation
- **Higher RBIS** → Strong risk-adjusted performance with controlled drawdowns  
- **Lower RBIS** → Returns dominated by volatility or tail risk  
- Explicitly penalizes strategies with large drawdowns, even if raw returns appear attractive

RBIS is **unit-free** and facilitates comparison across:
- Different equity pairs  
- Lookback windows  
- Entry/exit thresholds  

---

##  Sample Backtest Results

**Example: DAL–KO Pair**
- **ROI:** ~24.6%  
- **Sharpe Ratio:** ~1.33  
- **Max Drawdown:** ~7.3%  

Resulting in:
RBIS ≈ 4.47


This indicates **strong risk-adjusted performance**, with profits achieved without excessive downside risk.

> Results vary by asset pair, market regime, and parameter selection.

---

##  Key Takeaways
- Cointegration ensures structural mean reversion rather than short-term correlation
- Z-score thresholds provide disciplined entry and exit rules
- RBIS enhances evaluation by penalizing drawdowns alongside volatility
- Paper trading validates strategy robustness beyond theoretical backtests

---

##  Disclaimer
This project is for **educational and research purposes only** and does not constitute financial or investment advice.
