# Stochastic-portfolio-optimization-updated-January-2026
This is the January 2026 update of my project where I used computational methods to build and update a portfolio.


# Project Overview

This project implements a multi-period portfolio optimization framework for equity investments using:
1) Exponential Weighted Mean & Covariance Estimation (EWMA) for adapting to recent market trends.
2) Stochastic simulation (Geometric Brownian Motion with correlations) to generate thousands of plausible future market paths.
3) Conditional Value-at-Risk (CVaR) optimization for risk management.
4) Realistic constraints such as turnover costs, execution costs, and long-only allocation with diversification caps.
5) The project simulates portfolio rebalancing over the period July 2024 – present, using 50 large-cap and emerging AI/green energy stocks

# Methodology
## 1. Data Preparation (Python)
Source: Yahoo Finance via yfinance.
Sample: 50 equities (e.g., AAPL, MSFT, NVDA, BRK-B, TSLA, FSLR, PLTR, etc.).
Start date: April 1, 2024 (quarter lookback before first allocation).
Data: Daily adjusted close prices → converted to daily returns

## 2. Optimization (Julia)- Julia was chosen for optimization because of its specialized libraries and ecosystem.

Libraries: JuMP, HiGHS, MathOptInterface, DataFrames.
Steps:
a) Compute exponentially weighted mean vector (μ) and covariance matrix (Σ).
b) Run stochastic daily-path simulations (~2000 scenarios per rebalance).
c) Optimize portfolio weights using CVaR at 95% confidence.
d) Apply diversification constraints: max 20% per stock, no shorting.
e) Deduct execution + turnover costs from portfolio value.
f) Rebalance on fixed dates (quarterly or monthly).

### Outputs:

Portfolio weights per rebalance (multi_period_weights.csv).
Portfolio values and stats (multi_period_rebalance_summary.csv).
Daily wealth path (portfolio_daily.csv).
Scenario quantiles for visualization (graph.csv)

## 3. Post-Optimization Analysis (Python)
Benchmarks: S&P 500, NASDAQ Composite, Dow Jones Industrial Average

### Plots:
Normalized Wealth vs Benchmarks.
Charts (1σ, 2σ, 3σ) showing stochastic forecast fans per rebalance.
Rebased indices: index returns rescaled to portfolio at each rebalance for clearer comparison.

### Performance metrics:
Sharpe ratio, Sortino ratio, Maximum Drawdown (MaxDD), Cumulative return

# Results

The portfolio reallocates across sectors (tech, banks, green energy) depending on risk-return tradeoffs.
CVaR optimization prevents extreme downside losses better than mean-variance.
Simulation charts show uncertainty widening over horizons, with realized returns typically staying within 1–2σ bands.
Compared to SPY/QQQ/DIA, the portfolio demonstrates comparable or stronger risk-adjusted returns, though subject to shocks (e.g., tariffs, macro volatility).

# How to Run:

Prepare Data (Python)- jupyter notebook data_preparation.ipynb
Generates returns.csv, prices.csv, tickers.csv.

Optimize (Julia)- jupyter notebook stochastic_optimization.ipynb
Produces rebalance weights, portfolio values, and simulation data.

Analyze (Python)- jupyter notebook post_optimization_analysis.ipynb
Creates plots, calculates performance metrics.

# Software used

Python: pandas, numpy, matplotlib, yfinance
Julia: JuMP, HiGHS, MathOptInterface, DataFrames, LinearAlgebra
Visualization: Fan charts, benchmark overlays


