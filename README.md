# Risk Management: Methods of Valuation, Management and Control

Bachelor's thesis — University of Trieste, International Economics and Financial Markets, A.Y. 2023–2024.

**Author:** Tiziano Lostuzzi · **Supervisor:** Mario Marino

## Overview

The thesis reviews the main tools of financial risk management and applies them empirically in R. Contents:

1. **Financial risks** — market, credit, liquidity, operational, underwriting, model risk.
2. **Regulatory framework** — Basel III (three pillars) and Solvency I/II.
3. **Risk models** — loss distributions, VaR, Expected Shortfall, variance-covariance, historical simulation, Monte Carlo, backtesting.
4. **Empirical application** — VaR and ES on a multi-asset equity portfolio (JPM, GS, AAPL, BAC, BA, AMZN), comparing historical analysis with a multivariate normal Monte Carlo simulation.

## Repository contents

- `BScThesis_Tiziano_Lostuzzi.pdf` — full thesis.
- `risk_analysis.R` — R script for portfolio construction, historical VaR/ES, and Monte Carlo simulation.

## Requirements

```r
install.packages(c("quantmod", "PerformanceAnalytics", "ggplot2",
                   "MASS", "dplyr", "purrr", "scales"))
```

## Code description

The script is organized in modular sections:

1. **Parameters** — date range, tickers, portfolio weights, confidence level `alpha`, initial value, number of Monte Carlo simulations, and horizon in days. Weights are auto-normalized if they don't sum to 1.
2. **Data download** — adjusted close prices fetched from Yahoo Finance via `quantmod::getSymbols`, then converted into daily discrete returns and merged into a single dataframe.
3. **Portfolio construction** — asset returns combined through the weight vector to produce the daily portfolio return series.
4. **Historical risk metrics** — empirical VaR (quantile at `alpha`), Expected Shortfall (mean of returns below VaR), expected return, standard deviation, skewness, kurtosis, Sharpe and Sortino ratios, maximum drawdown, cumulative portfolio value, and a table of days breaching VaR/ES thresholds.
5. **Monte Carlo simulation** — estimates the mean vector and covariance matrix from historical returns, then generates `n_sim` scenarios via `MASS::mvrnorm` from a multivariate normal distribution. The same metrics are recomputed on the simulated distribution.
6. **Comparison and plots** — historical vs. simulated metrics side-by-side, plus `ggplot2` charts: return distribution with VaR/ES/E[R] markers, daily return time series, cumulative portfolio value, individual asset prices, and overlaid historical-vs-simulated densities.

## Usage

Edit the parameter block at the top of the script and run. All outputs (tables and plots) are generated automatically.

## Key finding

The Gaussian Monte Carlo underestimates tail risk: simulated VaR and ES are less severe than historical, with lower kurtosis and near-zero skewness vs. the heavy-tailed, negatively skewed empirical distribution — motivating the Basel III FRTB shift from VaR to ES.

## Data source

Daily adjusted close prices from [Yahoo Finance](https://finance.yahoo.com/).
