# Portfolio Risk Simulation — Monte Carlo VaR & Expected Shortfall

A Monte Carlo simulation in R to estimate the risk profile of a 40/60 stock-bond portfolio.

## Description

The script downloads historical daily price data for the S&P 500 and a U.S. Treasury Bond ETF (IEI) from Yahoo Finance, estimates the return distribution of each asset, and runs 100,000 Monte Carlo simulations of a one-year horizon using Geometric Brownian Motion.

From the simulated portfolio return distribution it computes Value at Risk (VaR) at the 95% confidence level and Expected Shortfall (ES), then plots the full distribution as a histogram with a density curve and annotated vertical lines for VaR, ES and expected return.

## Dependencies

```r
quantmod
PerformanceAnalytics
ggplot2
```
