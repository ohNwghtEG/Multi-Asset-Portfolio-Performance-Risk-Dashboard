# Multi-Asset-Portfolio-Performance-Risk-Dashboard

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ohNwghtEG/Multi-Asset-Portfolio-Performance-Risk-Dashboard/blob/main/Multi-Asset%20Portfolio%20Performance%20%26%20Risk%20Dashboard.ipynb)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
This project is a Python-based portfolio analytics dashboard, built in Google Colab, that pulls live market data and computes standard institutional risk/return diagnostics for a multi-asset portfolio. It constructs a comprehensive, institutional-style performance and risk analytics dashboard for a multi-asset investment portfolio spanning US equities, investment-grade bonds, gold, Nasdaq-100 technology stocks, and Bitcoin. This dashboard covers the period from 2018 into 2024, a window that encompasses some of the most volatile and consequential market environments in modern financial history, such as the COVID-19 crash and recovery of 2020, the inflation surge and Federal Reserve tightening cycle of 2022, and the AI-driven equity bull market of 2023–2024.

This project is built entirely in Python using institutional-grade analytical methods and produces six interactive visualizations alongside a full risk-adjusted performance metrics table — the same categories of output that appear in hedge fund investor tear sheets, wealth management quarterly reports, and asset manager fact sheets.

(it is recommended you open the code in colab as github is restricting the graphs from being displayed after I ran the code)
# Core Quantitative Concepts

- Log vs. simple returns 
- Annualization conventions 
- Sharpe / Sortino / Calmar ratios 
- Maximum drawdown 
- Historical VaR & CVaR 
- Correlation vs. covariance 
- Rolling-window statistics

- Data pipeline:

Uses yfinance to download daily adjusted closing prices (2018–2024) for five tickers: SPY (US large-cap equities), AGG (US aggregate bonds), GLD (gold), QQQ (Nasdaq 100), and BTC-USD (Bitcoin) — a fixed 40/25/15/10/10 weight allocation.
Pulls the 3-month T-Bill yield (DGS3MO) from FRED via fredapi to use as the risk-free rate, converting it from annualized percentage to a daily decimal rate for Sharpe/Sortino calculations.
Computes both log returns (for statistical work) and simple returns (for compounding/cumulative growth), plus a weighted portfolio return series.
