# Portfolio Analytics & Risk-Return System

A Python-based project that analyzes a 15-stock portfolio across 5 sectors,
calculates risk and return metrics, applies Modern Portfolio Theory to find an
optimal asset allocation, backtests the result on unseen data, and visualizes
findings in an interactive Power BI dashboard.

## What This Project Does
- Pulls 5 years of historical price data (2021–2026) for 15 stocks across 5 sectors
  (Banking, IT, FMCG, Auto, Pharma) plus the Nifty 50 benchmark
- Stores and queries the data using SQLite
- Calculates annualized return, volatility, Sharpe ratio, and beta for each stock
- Builds a correlation matrix to understand how stocks move together
- Runs a Monte Carlo simulation (50,000 portfolios) to find the optimal
  risk-return allocation using Modern Portfolio Theory
- Backtests the optimized portfolio on a genuinely unseen test period: weights
  are trained only on 2021–2023 data and evaluated on 2024–2025 returns, avoiding
  the data leakage that would come from optimizing and testing on overlapping data
- Visualizes sector allocation, risk-return trade-offs, and backtest performance
  in an interactive Power BI dashboard

## Dashboard
<img width="866" height="486" alt="image" src="https://github.com/user-attachments/assets/5290a4d5-5bbb-455f-9248-3dca778aabdf" />
<img width="871" height="459" alt="image" src="https://github.com/user-attachments/assets/e09b961b-b34a-4ad7-b65d-6da08f971381" />


## Tools Used
- Python (pandas, numpy, yfinance, matplotlib, seaborn)
- SQLite (data storage and querying)
- Power BI


## Key Findings

**Individual stock performance**
- M&M had the strongest individual risk-adjusted return (Sharpe ratio: 1.09),
  followed by SBI (0.88), Sun Pharma (0.85), and Eicher Motors (0.73) — all
  comfortably ahead of the Nifty 50 benchmark (0.55)
- TCS (-0.10) and Hindustan Unilever (-0.23) were the weakest risk-adjusted
  performers over the period, underperforming even a risk-free return

**Market sensitivity (beta)**
- SBI was the most market-sensitive stock (beta: 1.23) — it tends to move
  roughly 23% more than the Nifty 50 in either direction
- M&M, ICICI Bank, HDFC Bank, and Wipro also showed betas above 1
- ITC was among the most defensive stocks, moving less than the market

**Diversification and correlation**
- The three IT stocks (TCS, Infosys, Wipro) showed the highest correlation in
  the portfolio (~0.70), indicating limited diversification benefit from
  holding all three together
- An equal-weighted baseline portfolio (1/15 each) returned 15.39% annually;
  diversification alone meaningfully reduced risk versus holding the stocks
  independently

**Portfolio optimization**
- A Monte Carlo simulation of 50,000 portfolios identified an optimal (max
  Sharpe) allocation concentrated in M&M, Sun Pharma, and Eicher Motors, with
  a projected return of 26.13% at 16.35% risk (Sharpe ratio: 1.23)

**Backtest result (the key validation step)**
- To avoid data leakage, portfolio weights were re-optimized using only
  2021–2023 data, then tested on a genuinely unseen 2024–2025 period
- Result: the optimized portfolio returned **24.63%** cumulatively over the
  test period, versus the Nifty 50 benchmark's **20.24%** — a modest but
  genuine **+4.39 percentage point** outperformance on out-of-sample data
- This is a more credible and defensible result than a naive backtest, which
  would have shown a much larger (and misleading) outperformance had the
  optimization been allowed to "see" the test period in advance

## Limitations
- The full-period optimization (used for the general portfolio theory analysis,
  separate from the backtest) still includes a small allocation to the
  benchmark itself as an investable asset — a minor methodological
  simplification that does not affect the backtest, which correctly excludes it
- Backtest does not account for transaction costs, taxes, or portfolio
  rebalancing over time
- The test period covers 2 years, which is a reasonable but still limited
  window for judging long-term robustness
- Optimization assumes historical returns and correlations are a reasonable
  guide to near-term future performance, which does not always hold in practice

## Author
Sanjeev Subramaniam — MSc Business Analytics, MAHE Manipal
[LinkedIn](https://www.linkedin.com/in/sanjeevsubramaniam)
