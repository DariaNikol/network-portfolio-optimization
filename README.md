# Network Portfolio Optimization

## Overview
This project explores portfolio optimization using historical stock return data, with a focus on risk diversification and optimal asset allocation. The goal is to understand relationships between assets and evaluate portfolio performance rather than predict stock prices.

## Dataset
The dataset consists of historical stock price data from 2025, used to compute returns and correlations between assets.

**Note:** Data is retrieved programmatically using the Yahoo Finance library and is not stored in this repository.

## Methods Used
- Data collection via Yahoo Finance  
- Return and correlation analysis  
- Network-based representation of asset relationships  
- Monte Carlo simulation for portfolio optimization  
- Risk–return evaluation and comparison of portfolio allocations  

## Key Insights
- Correlation structure between assets plays a key role in diversification.
- Network analysis helps identify closely related stocks.
- Monte Carlo simulation highlights trade-offs between risk and expected return.
- Well-diversified portfolios can reduce risk without sacrificing performance.

## Practical Takeaways
This analysis demonstrates how combining network analysis with simulation-based optimization can support better portfolio construction. The approach is useful for understanding diversification benefits and making informed allocation decisions under uncertainty.

## Tools & Libraries
Python, pandas, NumPy, yfinance, matplotlib, networkx, scikit-learn
