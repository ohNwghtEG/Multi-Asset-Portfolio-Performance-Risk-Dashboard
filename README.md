# Multi-Asset-Portfolio-Performance-Risk-Dashboard

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ohNwghtEG/Multi-Asset-Portfolio-Performance-Risk-Dashboard/blob/main/Multi-Asset%20Portfolio%20Performance%20%26%20Risk%20Dashboard.ipynb)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License: CC0-1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)

This project is a Python-based portfolio analytics dashboard, built in Google Colab, that pulls live market data and computes standard institutional risk/return diagnostics for a multi-asset portfolio. It constructs a comprehensive, institutional-style performance and risk analytics dashboard for a multi-asset investment portfolio spanning US equities, investment-grade bonds, gold, Nasdaq-100 technology stocks, and Bitcoin. This dashboard covers the period from 2018 into 2024, a window that encompasses some of the most volatile and consequential market environments in modern financial history, such as the COVID-19 crash and recovery of 2020, the inflation surge and Federal Reserve tightening cycle of 2022, and the AI-driven equity bull market of 2023–2024.

This project is built entirely in Python using institutional-grade analytical methods and produces six interactive visualizations alongside a full risk-adjusted performance metrics table — the same categories of output that appear in hedge fund investor tear sheets, wealth management quarterly reports, and asset manager fact sheets. It downloads historical market data for a multi-asset portfolio and generates an institutional-style risk and performance tear sheet, made up of cumulative returns, drawdowns, rolling Sharpe, correlation structure, tail risk (VaR/CVaR), and market regime detection.

(It is recommended you open the code in Colab, as GitHub is restricting the graphs from being displayed after I ran the code)
# Core Quantitative Concepts

- Log vs. simple returns 
- Annualization conventions 
- Sharpe / Sortino / Calmar ratios 
- Maximum drawdown 
- Historical VaR & CVaR 
- Correlation vs. covariance 
- Rolling-window statistics


# Overview

This project answers a simple question: **How would a given asset allocation have actually performed, and how risky was the ride?**

It's built around a sample 5-asset portfolio (equities, bonds, gold, tech, and Bitcoin), but the tickers and weights are fully configurable — point it at any set of Yahoo Finance tickers and it will compute the same analytics.

| Asset | Ticker | Weight |
|---|---|---|
| US Large Cap Equities | `SPY` | 40% |
| US Aggregate Bonds | `AGG` | 25% |
| Gold | `GLD` | 15% |
| Nasdaq 100 (Tech) | `QQQ` | 10% |
| Bitcoin | `BTC-USD` | 10% |


# What does it do?

**Imagine you invested money like this: 40% in a big US stock fund, 25% in bonds, 15% in gold, 10% in tech stocks, and 10% in Bitcoin. This code answers the question: "How would that mix of investments have performed from 2018 to 2024, and how risky was it?"**

- Firstly, our code grabs the historical prices for those five investments from Yahoo Finance, going back to 2018.
- Also grabs a "safe" interest rate (like what you'd earn on a Treasury bill) so it can judge whether the portfolio's returns were actually worth the risk taken.
- Calculates how much $1 invested would have grown to over time for each asset and for the whole blended portfolio — this is the classic "growth chart" you see in investment brochures.
- Tracks the worst losses — how far each investment fell from its peak at any point (a "drawdown" chart), which tells you how painful it would've been to hold through the bad times.
- Measures risk-adjusted performance — not just "did it go up," but "did it go up enough to justify how bumpy the ride was" (that's what the Sharpe/Sortino ratios do).
- Checks how the assets move together — a heatmap showing whether, say, gold tends to zig when stocks zag (useful for understanding diversification).
- Shows worst-case-day risk — how bad a really bad day could get, statistically.
- Marks bull vs. bear markets for stocks using a simple 200-day trend line.
- Finally, it stitches several of these into one summary "dashboard" comparing the whole portfolio against just holding the S&P 500 alone.



# Features

- **Data pipeline** — pulls daily adjusted prices via `yfinance` and the 3-month T-Bill risk-free rate via `fredapi` (FRED series `DGS3MO`).
- **Performance metrics** — annualized return, volatility, Sharpe ratio, Sortino ratio, max drawdown, Calmar ratio, 95% VaR, and 95% CVaR for every asset and the blended portfolio.
- **Visualizations** (interactive, Plotly):
  - Cumulative growth-of-$1 chart
  - Drawdown ("underwater") chart
  - Rolling 60-day annualized Sharpe ratio
  - Asset correlation heatmap (diversification diagnostic)
  - Overlaid daily return histograms with VaR context
  - Bull/bear regime overlay using the 200-day moving average
  - A combined 3-panel dashboard: portfolio vs. benchmark cumulative return, portfolio drawdown, and rolling Sharpe — essentially a tearsheet.

## Core quantitative concepts (EXPANDED)

1. **Returns**

- Log returns (ln(P_t / P_t-1)) — used for statistical work because they're time-additive and closer to normally distributed.

- Simple returns (P_t/P_t-1 - 1) — used for compounding/cumulative growth, since they reflect actual dollar growth correctly.

2. **Risk-free rate**

- The 3-month T-Bill yield, used as the "do-nothing" baseline. Any return above this is called excess return — the reward for taking on risk at all.

3. **Volatility (standard deviation)**

- The spread of daily returns, annualized by multiplying by √252 (252 trading days/year). This is the standard proxy for "risk" in modern portfolio theory.

4. **Sharpe ratio**

- (mean excess return) / (total volatility) — return earned per unit of total risk taken. Higher is better; it's the most common risk-adjusted performance metric.

5. **Sortino ratio**

- Like Sharpe, but only penalizes downside volatility (negative returns), not upside swings. Reflects the intuition that investors don't mind volatility when it's making them money.

6. **Drawdown & Max Drawdown**

- How far a cumulative return curve has fallen from its highest previous peak. Max drawdown is the worst peak-to-trough loss over the whole period — a visceral "how much pain would I have felt" measure.

7. **Calmar ratio**

- annualized return / |max drawdown| — return earned per unit of worst-case pain, rather than per unit of average volatility.

8. **Value at Risk (VaR) & Conditional VaR (CVaR/Expected Shortfall)**

- VaR (95%) is the loss threshold you'd expect to exceed only 5% of the time on a given day. CVaR is the average loss on those worst days — it answers "when it's bad, how bad?"

9. **Correlation matrix**

- Measures how assets move together (-1 to +1). Low or negative correlations are what actually create diversification benefit — this is the mathematical core of why a mixed portfolio is less risky than any single asset.

10. **Rolling metrics (60-day Sharpe)**

- Recomputing a metric over a moving window rather than the whole history, to see how risk-adjusted performance changes over time rather than as one static number.

11. **Regime detection (200-day moving average)**

- A simple trend-following heuristic: price above its 200-day average = "bull," below = "bear." Common technical/quant shorthand for market regime.

## Tech Stack

- Python
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
git clone https://github.com/<ohNwghtEG>/<Multi-Asset-Portfolio-Performance-Risk-Dashboard>.git
cd <Multi-Asset-Portfolio-Performance-Risk-Dashboard>
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
