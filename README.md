# Pairs-Trading-using-Kalman-Filter

This project implements a complete pairs-trading research pipeline using a cointegration test to filter candidate pairs, Kalman-filter-based dynamic hedge-ratio estimation, mean-reverting spread modeling, z-score trading signals, tuning the entry-exit threshold parameters and a full long/short backtesting framework.

We begin by downloading historical price data for a broad multi-sector equity universe, testing all pair combinations for Engle–Granger cointegration, and selecting the most statistically reliable candidates, visualized through a clearly formatted cointegration heatmap.

For each chosen pair, the relationship between assets is modeled with a time-varying linear regression whose intercept and slope $α(t)$ and $β(t)$ are estimated using a Kalman filter, allowing the hedge ratio to evolve with market conditions rather than remain static. Using the resulting dynamic spread, the strategy computes a mean-reversion half-life that is used in an adaptive rolling window for z-score calculations, which in turn generate long and short entries when deviations become statistically significant and close positions as the spread reverts.

A consistent backtest engine evaluates daily PnL from spread changes, uses a coherent capital definition based on the underlying exposure $|y| + |β|·|x|$, supports transaction-cost penalties, and avoids look-ahead bias through a train/test split where entry and exit thresholds are tuned only on the training portion and then applied out-of-sample on the test data. The test data in the general setting is also obtained by an independent Kalman filter applied only on the test period and not using any past info.

The notebook concludes with an extensive metrics suite—including Sharpe, Sortino, CAGR, drawdowns, win/loss statistics, payoff ratio, Omega ratio, VaR/CVaR, exposure, and trade counts, providing a comprehensive assessment of strategy performance. The PnL charts are also drawn for the default and the tuned case for comparison. 
