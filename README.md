# Pairs Trading Algorithmic Bot (Statistical Arbitrage)

## Overview
This project implements a **Python-based algorithmic trading bot** that executes a **Pairs Trading strategy**, a classical statistical arbitrage approach that exploits **mean-reverting relationships between cointegrated equities**.

The bot identifies statistically valid trading pairs using **cointegration testing**, generates trading signals based on **Z-score deviations**, and evaluates performance through **historical backtesting and paper trading simulations**.

This project combines **time-series econometrics, object-oriented programming, and trading system design**, making it suitable for quantitative finance, risk analytics, and trading roles.

---

## Strategy Methodology

### Cointegration Testing
- Uses the **Engle–Granger two-step method**
- Performs linear regression on asset price series
- Applies the **Augmented Dickey-Fuller (ADF) test** on residuals
- Trades only pairs with statistically significant cointegration (p-value ≤ 0.05)

This ensures the spread between assets is **stationary and mean-reverting**, a core requirement for pairs trading.

---

### Z-Score Based Signal Generation

The spread is normalized using the Z-score:

$$
Z_t = \frac{X_t - \mu}{\sigma}
$$

Where:
- $X_t$ = current spread  
- $\mu$ = historical mean of spread  
- $\sigma$ = historical standard deviation  

**Trading Rules:**
- **Z > +2** → Short the spread  
- **Z < -2** → Long the spread  
- **Z ≈ 0** → Close positions  

Thresholds are based on the **95% empirical rule**.

---

## Key Features
- Object-Oriented design via a `PairsTradingBot` class
- Automated data retrieval using Yahoo Finance
- API throttling and error handling
- Historical backtesting with ROI, Sharpe Ratio, and Max Drawdown
- Paper trading simulation to mimic live portfolio behavior
- Detailed logging of trades and portfolio evolution
- Visualizations for Z-score dynamics and portfolio performance

---

## Sample Backtest Results

Example (DAL–KO pair):
- **ROI:** ~24.6%
- **Sharpe Ratio:** ~1.33
- **Max Drawdown:** ~7.3%

> Results vary based on asset pair, lookback window, and market conditions.

---

## Project Structure

```text
pairs-trading-bot/
│
├── README.md
├── requirements.txt
│
├── src/
│   ├── pairs_trading_bot.py   # Core strategy logic
│   ├── backtest.py            # Backtesting engine
│   ├── paper_trading.py       # Paper trading simulation
│   └── utils.py               # Statistical helper functions
│
├── notebooks/
│   └── exploratory_analysis.ipynb
│
├── logs/
│   └── trading.log
│
└── reports/
    └── final_report.pdf
Technologies Used

Python

NumPy, pandas

statsmodels

matplotlib

Yahoo Finance API

Object-Oriented Programming

Time-series econometrics

How to Run

Clone the repository:
git clone https://github.com/eryajain12/pairs-trading-bot.git
cd pairs-trading-bot

Install dependencies:
pip install -r requirements.txt

Run the bot:
python src/pairs_trading_bot.py

Future Improvements

Multivariate cointegration (Johansen test)

Dynamic hedge ratio estimation

Transaction cost modeling

Risk-adjusted position sizing

Intraday data support

Live broker API integration
