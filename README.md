## Long and Short position, and weighted break most men, if not all
=========================

### Executive Summary
This project aims to combine alpha signal generation through momentum factors with dynamic portfolio optimization techniques to enhance equity trading strategies. Using assets from the S&P 500 universe, the approach constructs a long-short portfolio by ranking securities based on z-scored momentum signals. The selected assets are rebalanced monthly using two distinct weighting methods: one that maximizes the Sharpe ratio and another that minimizes portfolio volatility. Monte Carlo simulations are employed to identify optimal allocations along the efficient frontier. A 5-year backtest evaluates performance against the SPY ETF benchmark, focusing on cumulative returns and relative risk-adjusted metrics. This project demonstrates the real-world applicability of modern portfolio theory in a systematic trading environment.


... Problem

In the realm of quantitative finance, investors constantly seek strategies that can generate alpha while managing risk effectively. Traditional long-only portfolios often underperform in volatile or sideways markets and lack adaptability to changing conditions. Additionally, many retail and institutional investors rely on static portfolio allocations that fail to respond to shifts in market dynamics. This project addresses the dual challenge of identifying momentum-based opportunities and dynamically adjusting portfolio weights to optimize performance. By building a systematic framework for monthly rebalancing of long-short portfolios using advanced optimization techniques, this project tackles the inefficiencies present in passive investment strategies and offers a robust alternative for improving capital allocation decisions.



... What is the data science opportunity

This project presents a compelling data science opportunity by applying statistical analysis, simulation techniques, and machine learning principles to financial markets. The core opportunity lies in transforming historical price and volume data into actionable insights through factor construction, asset ranking, and portfolio simulation. Using Monte Carlo methods, the project models thousands of portfolio combinations to identify optimal weightings along the efficient frontier—a process that would be infeasible manually. Additionally, the dynamic and repeatable nature of this framework allows for automated rebalancing and model refinement over time. The use of z-score normalization, backtesting, and risk-adjusted return metrics aligns this work with real-world applications in quantitative asset management, making it a strong example of data-driven decision-making in finance.
     
      •	Data Collection: Aggregating historical asset prices (open and close), and
          indicators from 
           •  Data Acquisition
               o Preprocessing & Feature Engineering:
                 Data Acquisition
               o Clean ticker list to resolve missing or invalid tickers.
               o Align time indices and resample data (e.g., monthly frequency) for uniformity.
          
          • Missing Value Handling
               o Drop or forward-fill (ffill) missing price or volume entries.
               o Exclude tickers with excessive missing data (e.g., more than 7% NaNs).
          
          • Feature Construction (Momentum Factors) 
               o Trend (Linear Regression Slope):
               o Compute rolling 1-year price trends using np.polyfit.
          
          • Percent Above 52-week Low:
               o (Price − 52-week low)/ 52-week low

          • Price Oscillator:
               o Difference between 20-day moving average and 260-day average normalized `                      standard deviation.

          • 39-Week Return:
               o Cumulative return over ~9 months.

          • Price × Volume Trend:
               o Slope of dollar-volume time series as a liquidity-adjusted momentum proxy.
               
          • Normalization
               o Z-score each factor across all tickers monthly to allow comparability.

          • Composite Momentum Score
               o Aggregate normalized factors into a single momentum score                                      (e.g., by summing z-scores).

               o Rank stocks by momentum score to form long and short baskets.

          • Backtesting Dataset Preparation
               o Create lagged returns for post-ranking evaluation.
               o Align factor ranks and future returns to simulate 
                 real-world rebalancing logic.

          • Portfolio Simulation Inputs
               o Build monthly return matrix for selected long and short tickers.
               o Prepare inputs for Monte Carlo simulation
                 (returns, covariance matrix, etc.).


      
      Statistical Analysis
      
          • Descriptive Statistics:
          • Computed mean, standard deviation, and variance of individual stock returns.

          - Evaluated correlation matrix to understand asset co-movement and diversification               potential.
          • Factor Behavior:
          • Analyzed the distribution and time-series stability of each momentum factor (e.g.,             trend, oscillator, return).
          - Assessed multicollinearity among factors to validate aggregation into a composite              momentum score.

          • Risk Metrics:
          • Measured portfolio volatility, Sharpe ratio, and drawdowns across backtest periods.
          - Benchmarked performance against SPY ETF to evaluate relative efficiency.
          • Basket Performance:
          • Compared average returns of long vs. short baskets monthly.
          - Tracked how basket composition shifts over time based on momentum changes.

          Model Building
          • Monte Carlo Simulation:
          • Generated thousands of random weight combinations for selected assets.
          - Calculated expected return, volatility, and Sharpe ratio for each simulated                    portfolio.
          • Optimization Objectives:
          • Sharpe Ratio Maximization: Identified the portfolio with the highest return-to-                risk ratio.
          - Volatility Minimization: Found the weight configuration with the lowest standard               deviation.
          • Constraint Handling:
          •	- Ensured portfolio weights sum to 1.
          - Applied bounds to prevent shorting in constrained scenarios (0 ≤ weight ≤ 1).
          • Rebalancing Logic:
          •	- Reapplied model monthly based on updated rankings and new return data.
          - Allowed dynamic adaptation to changing market conditions.
          • Backtest Framework:
          •	- Recorded monthly portfolio returns under both optimization schemes.
          - Compared results across a 5-year testing window using cumulative returns and                   monthly bars.


... Key takeaways

          • Momentum signals can effectively identify outperforming and underperforming stocks             when derived from trend, return, and price-volume metrics.
          • Long-short baskets provide a market-neutral framework that reduces directional e               exposure and isolates alpha.
          • Monte Carlo simulations offer a powerful tool for exploring the efficient frontier             and optimizing portfolio weights under uncertainty.
          • Sharpe ratio maximization and volatility minimization yield distinct yet valuable              allocation strategies, allowing flexibility based on investor risk preferences.
          • Monthly rebalancing based on updated factor rankings ensures that the portfolio                adapts to changing market conditions.
          • This project demonstrates how data science and modern portfolio theory can be                  integrated to create transparent, repeatable, and quantitatively sound investment              strategies.


### Demo

![Cumilative Returns vs SPY](https://github.com/user-attachments/assets/12ecb937-5d3b-45fb-b09e-96dad550fadb)





### Methodology

... High-level diagrams of entire process:
          This project develops a systematic trading strategy that combines momentum-based                asset selection with quantitative portfolio optimization. Stocks from the S&P 500 are           ranked monthly based on engineered momentum signals and grouped into long and short             baskets. Portfolio weights are then optimized using Monte Carlo simulation to either            maximize the Sharpe ratio or minimize volatility. The strategy is backtested over a             5-year period, demonstrating how data-driven rebalancing and risk-aware allocation              can outperform a passive benchmark like SPY.

#### Dataset

... Yfinance

### Credits & References

... Izuchukwu Egonu, Berry Cox, 
