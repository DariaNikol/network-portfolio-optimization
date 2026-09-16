# Network Portfolio Optimization

## Overview

This project constructs and evaluates an optimized 15-stock portfolio using rolling volatility
analysis, correlation-network analysis, and Monte Carlo simulation. The focus is on understanding
how assets relate to one another and when risk actually arrives, rather than on predicting prices.

The optimized allocation achieved an annualized Sharpe ratio of **1.58**, compared to **1.03** for
an equally weighted baseline, a 53% improvement in risk-adjusted return across the same 15 assets.

## Key Findings

**A single policy event drove volatility across four unrelated sectors.** Rolling 20-day volatility
for WMT, META, and GOOG peaked within a two-week window (April 22, May 1, and May 7, 2025), tracing
to the April 2, 2025 tariff announcement and the 12.4% market decline that followed. Four companies
in retail, social media, technology, and EV manufacturing moved together, confirming a market-wide
rather than sector-specific cause.

**NIO was the exception on both ends, for a verifiable reason.** Its volatility peaked on March 24,
nearly a month before the others, three days after its Q4 2024 earnings release, and it bottomed on
July 7, weeks ahead of the rest. Company-specific events, not the market-wide shock, drove its risk
profile, which makes it a genuine diversifier rather than another correlated holding.

**Network centrality identified the portfolio's structural hub.** Morgan Stanley (MS) ranked highest
on all three centrality measures (degree 0.29, betweenness 0.76, eigenvector 0.57) in the minimum
spanning tree, sitting on most shortest paths between sectors. NVDA was the most peripheral, five
steps from the hub and connected only through MSFT.

**Correlation structure supports diversification.** The median pairwise correlation was 0.29. The
strongest pairs were CVX and XOM at 0.86 and JPM and MS at 0.85, both within-sector. JNJ and NVDA
were the most negatively correlated at -0.26, while JNJ and MS were effectively independent at
-0.003, a pairing that reduces portfolio risk without either holding working against the other.

**The optimal allocation concentrates in risk-adjusted performers, not high-return ones.** Across
10,000 simulated portfolios, the maximum-Sharpe allocation weighted JNJ (16.1%), GOOG (14.2%),
JPM (12.0%), MS (11.8%), and NVDA (10.6%), roughly 65% of the portfolio. CVX received 0.19%, likely
because its 0.86 correlation with XOM makes it largely redundant.

## Dataset

Daily adjusted closing prices for 15 large-cap U.S. equities across technology, finance, energy,
healthcare, retail, and EV manufacturing, retrieved programmatically from Yahoo Finance.

The analysis period runs from January 2025 through December 2025 (233 trading days). For the
rolling volatility work the range extends back to October 15, 2024, so that the 20-day and 50-day
windows are fully populated from the first trading day of 2025 rather than returning nulls.

Data is retrieved at runtime and is not stored in this repository.

## Methods

1. Data collection from Yahoo Finance with split and dividend adjustments applied
2. Daily log returns, chosen for time-additivity and comparability across price levels
3. Rolling volatility over 20-day and 50-day windows, with peak and trough dates isolated
   programmatically and cross-referenced against published market events
4. Covariance and correlation matrices across all 15 assets
5. Correlation converted to a distance matrix and reduced to a minimum spanning tree; degree,
   betweenness, and eigenvector centrality computed on the resulting network
6. Equally weighted portfolio established as a baseline
7. Monte Carlo simulation of 10,000 random weight allocations, seeded for reproducibility
8. Efficient frontier plotted and the maximum-Sharpe portfolio identified

## Practical Takeaways

Static optimization and time-varying risk analysis answer different questions. Monte Carlo
simulation identifies the best average allocation, but it treats each stock's risk as one fixed
number for the year. The rolling volatility layer shows when that risk actually materialized, and
tying those dates to real market events explains why. A holding whose risk moves on its own
schedule, as NIO's did, contributes diversification that a correlation matrix alone understates.

The optimization assumes stable conditions and does not price in transaction costs or forward-looking
policy risk, which the April 2025 tariff episode demonstrates can reshape the entire portfolio's risk
profile within days.

## Tools & Libraries

Python, pandas, NumPy, yfinance, matplotlib, seaborn, networkx

## Repository Contents

| File | Description |
|---|---|
| `stocks.ipynb` | Full analysis notebook: data collection, rolling volatility, network analysis, Monte Carlo simulation, and conclusions |
| `README.md` | Project overview and findings |

## Reproducibility

The Monte Carlo simulation is seeded (`np.random.seed(42)`) and the notebook runs top to bottom
without manual intervention. Note that Yahoo Finance periodically revises historical adjusted
prices, so values may shift slightly on a future data pull.
