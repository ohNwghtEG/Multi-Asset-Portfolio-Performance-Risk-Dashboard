# Multi-Asset-Portfolio-Performance-Risk-Dashboard

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ohNwghtEG/Multi-Asset-Portfolio-Performance-Risk-Dashboard/blob/main/Multi-Asset%20Portfolio%20Performance%20%26%20Risk%20Dashboard.ipynb)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License: CC0-1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)

This project is a Python-based portfolio analytics dashboard, built in Google Colab, that pulls live market data and computes standard institutional risk/return diagnostics for a multi-asset portfolio. It constructs a comprehensive, institutional-style performance and risk analytics dashboard for a multi-asset investment portfolio spanning US equities, investment-grade bonds, gold, Nasdaq-100 technology stocks, and Bitcoin. This dashboard covers the period from 2018 into 2024, a window that encompasses some of the most volatile and consequential market environments in modern financial history, such as the COVID-19 crash and recovery of 2020, the inflation surge and Federal Reserve tightening cycle of 2022, and the AI-driven equity bull market of 2023–2024.

This project is built entirely in Python using institutional-grade analytical methods and produces six interactive visualizations alongside a full risk-adjusted performance metrics table — the same categories of output that appear in hedge fund investor tear sheets, wealth management quarterly reports, and asset manager fact sheets. It downloads historical market data for a multi-asset portfolio and generates an institutional-style risk and performance tearsheet, made up of cumulative returns, drawdowns, rolling Sharpe, correlation structure, tail risk (VaR/CVaR), and market regime detection.

(it is recommended you open the code in colab as github is restricting the graphs from being displayed after I ran the code)
# Core Quantitative Concepts

- Log vs. simple returns 
- Annualization conventions 
- Sharpe / Sortino / Calmar ratios 
- Maximum drawdown 
- Historical VaR & CVaR 
- Correlation vs. covariance 
- Rolling-window statistics

## Overview

This project answers a simple question: **how would a given asset allocation have actually performed, and how risky was the ride?**

It's built around a sample 5-asset portfolio (equities, bonds, gold, tech, and Bitcoin), but the tickers and weights are fully configurable — point it at any set of Yahoo Finance tickers and it will compute the same analytics.

| Asset | Ticker | Weight |
|---|---|---|
| US Large Cap Equities | `SPY` | 40% |
| US Aggregate Bonds | `AGG` | 25% |
| Gold | `GLD` | 15% |
| Nasdaq 100 (Tech) | `QQQ` | 10% |
| Bitcoin | `BTC-USD` | 10% |

## Features

- **Data pipeline** — pulls daily adjusted prices via `yfinance` and the 3-month T-Bill risk-free rate via `fredapi` (FRED series `DGS3MO`).
- **Performance metrics** — annualized return, volatility, Sharpe ratio, Sortino ratio, max drawdown, Calmar ratio, 95% VaR, and 95% CVaR for every asset and the blended portfolio.
- **Visualizations** (interactive, Plotly):
  - Cumulative growth-of-$1 chart
  - Drawdown ("underwater") chart
  - Rolling 60-day annualized Sharpe ratio
  - Asset correlation heatmap
  - Daily return distribution histograms
  - Bull/bear regime overlay using the 200-day moving average
  - Combined 3-panel portfolio dashboard vs. benchmark

## Tech Stack

- Python 3
- `yfinance` — market data
- `fredapi` — risk-free rate data
- `pandas` / `numpy` — data wrangling and statistics
- `plotly` — interactive charts
- `quantstats` (optional, for extended tearsheet stats)

## Getting Started

### Prerequisites

- Python 3.10+
- A free [FRED API key](https://fred.stlouisfed.org/docs/api/api_key.html)

### Installation

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
pip install -r requirements.txt
```

**`requirements.txt`**
```
yfinance
fredapi
plotly
pandas
numpy
quantstats
```

### Configuration

Set your FRED API key as an environment variable (or, if running in Google Colab, store it in Colab's Secrets manager as `FRED_KEY`):

```bash
export FRED_KEY="your_fred_api_key_here"
```

### Usage

Open `Portfolio_Dashboard.ipynb` in Jupyter, JupyterLab, VS Code, or Google Colab and run all cells. To analyze a different portfolio, edit the configuration block near the top:

```python
TICKERS = ['SPY', 'AGG', 'GLD', 'QQQ', 'BTC-USD']
WEIGHTS = {
    'SPY': 0.40, 'AGG': 0.25, 'GLD': 0.15,
    'QQQ': 0.10, 'BTC-USD': 0.10,
}
START_DATE = '2018-01-01'
END_DATE   = '2024-12-31'
BENCHMARK  = 'SPY'
```

## Metrics Reference

| Metric | What it measures |
|---|---|
| Annualized Return | Average yearly growth rate |
| Annualized Volatility | Standard deviation of returns, scaled to a year |
| Sharpe Ratio | Return per unit of total risk |
| Sortino Ratio | Return per unit of *downside* risk only |
| Max Drawdown | Worst peak-to-trough loss |
| Calmar Ratio | Return per unit of worst-case drawdown |
| VaR (95%) | Loss threshold exceeded only 5% of the time |
| CVaR (95%) | Average loss on the worst 5% of days |

## Sample Output

*(Add a screenshot or GIF of the dashboard here once you've run it, e.g. `docs/dashboard_preview.png`)*

```
![Dashboard preview](docs/dashboard_preview.png)
```

## Project Structure

```
.
├── Portfolio_Dashboard.ipynb   # main notebook
├── requirements.txt
├── README.md
└── docs/
    └── dashboard_preview.png   # optional screenshot
```

## Roadmap / Ideas

- [ ] Add rebalancing logic (e.g., quarterly rebalance back to target weights)
- [ ] Support custom, non-equal-weight optimization (e.g., mean-variance / max Sharpe)
- [ ] Export tearsheet to PDF/HTML report
- [ ] Add walk-forward backtesting

## Disclaimer

This project is for educational and informational purposes only. It does not constitute financial advice. Past performance is not indicative of future results.

## License

This project is released under [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) — dedicated to the public domain. You can copy, modify, and use it for any purpose, including commercially, without asking permission or providing attribution. See [LICENSE](LICENSE) for the full legal text.
