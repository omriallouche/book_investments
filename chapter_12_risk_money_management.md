# Chapter 12 — Risk and Money Management (Drawdowns, Kelly, and Friends)

***

## Why This Chapter Matters

We have spent a lot of time talking about generating alpha and controlling risk. But at the end of the day, the goal of investing is to grow your capital over the long run. This chapter is about the science of **money management**. It’s about how to size your bets and manage your capital to maximize your long-term growth rate while minimizing your risk of ruin.

The key insight is that the optimal strategy for a single bet is not the same as the optimal strategy for a series of bets. To survive and thrive in the long run, you must be willing to leave some money on the table. You must be willing to sacrifice some potential return in order to protect your capital from large losses. As the legendary investor Warren Buffett has said, “Rule No. 1: Never lose money. Rule No. 2: Never forget Rule No. 1.”

This chapter will introduce you to the key concepts of risk and money management, from the classic performance metrics to the more sophisticated position sizing algorithms like the Kelly criterion. The goal is to ensure that you can **survive long enough to compound.**

## Core Ideas

- **Performance Metrics:** The classic measures of risk-adjusted return:
    - **Drawdown:** The peak-to-trough decline in your portfolio’s value. The **maximum drawdown** is the largest such decline over the life of the strategy.
    - **Sharpe Ratio:** The ratio of excess return to volatility. The most widely used measure of risk-adjusted return.
    - **Information Ratio (IR):** The ratio of active return (alpha) to active risk (tracking error). A measure of a manager’s skill.
    - **Sortino Ratio:** Similar to the Sharpe ratio, but it only penalizes for downside volatility.
    - **Calmar Ratio:** The ratio of annualized return to maximum drawdown. A measure of return per unit of drawdown risk.

- **Fractional Kelly:** The Kelly criterion is a mathematical formula for determining the optimal size of a bet to maximize the long-term growth rate of capital. The full Kelly bet can be very aggressive, so in practice, most traders use a **fractional Kelly** (e.g., half Kelly) to be more conservative.

- **Risk Budgets:** A top-down approach to risk management. You start by defining a total risk budget for your portfolio (e.g., a target volatility of 10%). You then allocate this risk budget to different “sleeves” or sub-strategies. This is a powerful way to ensure diversification and to control the overall risk of your portfolio.

## Math You’ll Use

### Single-Asset Kelly Criterion (ℓ*)

The formula for the optimal fraction of your capital to bet on a single asset is:

*ℓ* ≈ μ / σ<sup>2</sup>*

Where:
- *μ* is the expected excess return of the asset.
- *σ<sup>2</sup>* is the variance of the asset’s returns.

This simple formula shows that the optimal bet size is directly proportional to the expected return and inversely proportional to the variance. A higher return means you should bet more. A higher variance means you should bet less.

### Multi-Asset Kelly Criterion (w*)

For a portfolio of multiple assets, the Kelly criterion becomes a vector of optimal weights:

*w* ∝ Σ<sup>-1</sup>μ*

Where:
- *Σ<sup>-1</sup>* is the inverse of the covariance matrix of asset returns.
- *μ* is the vector of expected excess returns.

This is a more general and powerful version of the mean-variance optimization we saw in Chapter 5. It shows that the optimal portfolio is one that balances expected returns, variances, and covariances.

### Skew-Adjusted Sharpe Ratio

The standard Sharpe ratio does not account for the skewness of returns. A strategy with a negative skew (i.e., a tendency for large negative returns) is riskier than a strategy with a positive skew, even if they have the same volatility. The **skew-adjusted Sharpe ratio** is a modification of the Sharpe ratio that penalizes for negative skewness.

### Omega Ratio

The Omega ratio is another alternative to the Sharpe ratio that is more robust to non-normal return distributions. It is the ratio of the probability-weighted gains to the probability-weighted losses, relative to a certain target return.

## Narrative Example: Cutting Gross During a Drawdown

A quantitative hedge fund is running a successful market-neutral strategy. The strategy has a Sharpe ratio of 1.5 and has never had a down year. But in the summer of 2007, the quant crisis hits. A wave of forced deleveraging by a few large funds causes a fire sale in many of the stocks held by the fund. The fund’s strategy, which is based on historical relationships, suddenly stops working.

The fund’s risk management system has a pre-defined rule: if the portfolio’s drawdown exceeds 15%, the gross exposure of the portfolio must be cut in half. This is a painful decision. It means selling at the bottom and realizing losses. But it is a necessary one.

By cutting its gross exposure, the fund is able to survive the crisis. It lives to fight another day. Many other funds that did not have a similar drawdown control mechanism were wiped out.

The lesson is that you must have a plan for how you will react to a large drawdown *before* it happens. When you are in the middle of a crisis, you cannot trust your emotions. You must rely on a pre-defined, disciplined process.

## Hands-On: Implement Circuit-Breakers

1.  **Take your strategy:** Take your final, complete investment strategy.
2.  **Implement a circuit-breaker:** Implement a “circuit-breaker” rule: if the portfolio’s drawdown exceeds a certain threshold (e.g., 20%), the strategy’s gross exposure is immediately cut by a certain percentage (e.g., 50%).
3.  **Backtest with the rule:** Run a backtest of your strategy with and without the circuit-breaker rule.
4.  **Compare the results:** Compare the results in detail. Look at:
    -   The terminal wealth at the end of the backtest.
    -   The maximum drawdown.
    -   The Ulcer Index.
    -   The time it takes to recover from a drawdown.
5.  **Analyze the trade-offs:** Does the circuit-breaker improve the risk-adjusted performance of your strategy? Does it give you a higher terminal wealth? What is the trade-off between the reduction in drawdowns and the potential for missing a sharp recovery?

## Check Yourself

- What is the difference between the Sharpe ratio and the Sortino ratio?
- Why is it often a good idea to use a fractional Kelly bet instead of a full Kelly bet?
- What is a risk budget, and how would you use it to manage a multi-strategy portfolio?
- How does the Omega ratio differ from the Sharpe ratio?

## Common Pitfalls

- **Risk of Ruin:** The Kelly criterion assumes that you can accurately estimate the expected return and variance of your bets. If you overestimate your edge, you can end up betting too much and blowing up your account. It is always better to be too conservative than too aggressive.
- **Path Dependency:** The order in which your returns occur matters. A large loss at the beginning of your investment horizon is much more damaging than a large loss at the end. This is why it is so important to control drawdowns.
- **Behavioral Biases:** It is very difficult to stick to a disciplined money management strategy in the face of large gains or losses. The fear and greed emotions can be overwhelming. This is why it is so important to have a pre-defined, automated process.
- **Over-optimizing on a Single Metric:** Don’t get too focused on optimizing a single performance metric, like the Sharpe ratio. A good strategy should look good from multiple angles. You should always look at a full dashboard of risk and return metrics.

## Key Takeaways

-   Money management is the science of managing your capital to maximize long-term growth.
-   The Kelly criterion provides a mathematical framework for optimal bet sizing.
-   Drawdown control is essential for surviving in the long run.
-   A disciplined, pre-defined risk management process is your best defense against behavioral biases.