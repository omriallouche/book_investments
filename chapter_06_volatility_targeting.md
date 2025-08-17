# Chapter 6 — Volatility Targeting, Beta Control, and Turnover Discipline

***

## Why This Chapter Matters

In the last chapter, we built a static, one-period portfolio. But in the real world, portfolios are dynamic. They need to be managed over time. This chapter is about the ongoing process of risk management. Our motto is: **Control risk first; alpha follows.**

We will introduce three powerful techniques for managing the risk of your portfolio on a day-to-day basis:

1.  **Volatility Targeting:** Keeping the portfolio’s risk level constant, regardless of the market environment.
2.  **Beta Control:** Managing the portfolio’s exposure to systematic market risk.
3.  **Turnover Discipline:** Minimizing transaction costs by only trading when it’s absolutely necessary.

These techniques are not about increasing your returns. They are about controlling your losses and improving your risk-adjusted performance. A strategy that can deliver the same expected return with a lower drawdown and a smoother equity curve is a superior strategy. It’s a strategy that will keep you in the game for the long run.

## Core Ideas

- **Volatility Targeting:** The volatility of the market is not constant. It can be low for long periods and then spike suddenly. If you have a fixed set of portfolio weights, the volatility of your portfolio will fluctuate with the market. Volatility targeting is a technique for maintaining a constant level of portfolio volatility. The mechanism is simple: when market volatility rises, you reduce your leverage or gross exposure. When market volatility falls, you increase it.

- **EWMA/GARCH Volatility:** To implement a volatility targeting strategy, we need a way to forecast near-term volatility. The two most common models are:
    - **EWMA (Exponentially Weighted Moving Average):** A simple model that calculates a weighted average of past squared returns, with more weight given to recent returns.
    - **GARCH (Generalized Autoregressive Conditional Heteroskedasticity):** A more sophisticated model that captures the tendency of volatility to cluster (i.e., high-volatility days are often followed by more high-volatility days).

- **Target Scaling:** The formula for adjusting your portfolio exposure is:

  *k = σ<sub>tgt</sub> / σ̂*

  Where *k* is the scaling factor, *σ<sub>tgt</sub>* is your target volatility, and *σ̂* is your forecast of volatility.

- **Beta Control:** The beta of your portfolio measures its sensitivity to the market. If you want to run a market-neutral strategy, you need to keep your beta close to zero. You can do this by:
    - **Rolling Beta:** Continuously monitoring your portfolio’s beta, estimated over a rolling window.
    - **Index/Futures Hedges:** If your beta drifts away from its target, you can use index futures or ETFs to hedge it back to your desired level. For example, if your portfolio’s beta has drifted up to 0.2, you can short an appropriate amount of S&P 500 futures to bring it back to zero.

- **Turnover Discipline:** Trading is costly. Every time you buy or sell a stock, you pay a commission and a bid-ask spread. A strategy that trades too frequently can see all of its profits eaten up by transaction costs. We can control this by:
    - **Trade Bands:** Only rebalancing the portfolio when a position’s weight deviates from its target weight by more than a certain threshold (e.g., +/- 0.5%).
    - **Cost-Aware Rebalancing:** Explicitly including a penalty for turnover in our portfolio optimization process.

## Math You’ll Use

### EWMA σ̂<sup>2</sup><sub>t</sub>

The formula for an EWMA volatility forecast is:

*σ̂<sup>2</sup><sub>t</sub> = λσ̂<sup>2</sup><sub>t-1</sub> + (1-λ)r<sup>2</sup><sub>t-1</sub>*

Where:
- *σ̂<sup>2</sup><sub>t</sub>* is the variance forecast for day *t*.
- *λ* (lambda) is the decay factor (typically between 0.9 and 1.0). A higher *λ* means that past observations have a longer-lasting impact.
- *r<sup>2</sup><sub>t-1</sub>* is the squared return on day *t-1*.

### Hedge Ratio

To hedge your portfolio’s beta, you need to calculate the correct hedge ratio. The formula is:

*Hedge Ratio = -β<sub>p</sub> \* (V<sub>p</sub> / V<sub>f</sub>)*

Where:
- *β<sub>p</sub>* is the portfolio’s beta.
- *V<sub>p</sub>* is the market value of the portfolio.
- *V<sub>f</sub>* is the market value of one futures contract.

The result is the number of futures contracts you need to short to make your portfolio market-neutral.

### Turnover Penalty

We can add a penalty for turnover to our mean-variance optimization objective function:

**max μ<sup>T</sup>w - λw<sup>T</sup>Σw - cΣ|w<sub>t</sub> - w<sub>t-1</sub>|**

Where:
- *c* is a parameter that controls the size of the penalty.
- *w<sub>t</sub>* is the vector of new portfolio weights.
- *w<sub>t-1</sub>* is the vector of existing portfolio weights.

## Narrative Example: The Strategy That “Won” by Avoiding Whiplash

Two portfolio managers, Alice and Bob, are given the same long-only momentum strategy. The strategy has a positive alpha, but it is also very volatile and prone to sharp drawdowns.

Bob implements the strategy as is. His portfolio’s volatility lurches up and down with the market. During periods of high volatility, he suffers large losses and is forced to sell at the bottom to meet redemptions. His position sizes are constantly being whipsawed around.

Alice, on the other hand, implements a volatility targeting overlay. When market volatility spikes, she reduces her portfolio’s exposure. When volatility falls, she increases it. Her portfolio’s volatility remains stable at a target of 10% per year. She also implements trade bands, so she only rebalances when her positions have drifted significantly from their targets.

At the end of five years, Alice and Bob have the same average annual return. But Alice’s portfolio has had a much smoother ride. Her maximum drawdown was half of Bob’s, and her Sharpe ratio was significantly higher. She “won” not by having a better signal, but by having a better risk management process.

## Hands-On: Add Risk Overlays to Your Portfolio

1.  **Take your portfolio:** Take the best-performing portfolio you constructed in Chapter 5.
2.  **Implement volatility targeting:** Implement a volatility targeting overlay. Use an EWMA model to forecast daily volatility and scale your portfolio’s exposure to maintain a constant target volatility (e.g., 12%).
3.  **Add trade bands:** Now, add trade bands to your rebalancing process. Only rebalance a position if its weight has drifted more than 10% from its target weight.
4.  **Quantify the impact:** Quantify the impact of these changes. Calculate:
    -   The annualized return and volatility.
    -   The Sharpe ratio and Sortino ratio.
    -   The maximum drawdown.
    -   The Ulcer Index (a measure of the depth and duration of drawdowns).
    -   The portfolio’s turnover.
5.  **Analyze the results:** How much did you save in transaction costs (assuming a certain cost per trade)? Did the volatility targeting improve the risk-adjusted return? Did the trade bands hurt performance by allowing the portfolio to drift from its optimal weights?

## Check Yourself

- What is the economic intuition behind volatility clustering?
- How does a volatility targeting strategy affect the skewness and kurtosis of your returns?
- What are the pros and cons of using a wider trade band?
- If your portfolio has a beta of 1.2, do you need to buy or sell index futures to hedge it?

## Common Pitfalls

- **Overreactive λ:** Choosing a low value for *λ* in your EWMA model will make your volatility forecast very sensitive to recent returns. This can cause you to overreact to short-term noise, leading to excessive trading.
- **Hedge Slippage:** The theoretical hedge ratio is not always the same as the real-world hedge ratio. The price of futures contracts can deviate from their fair value, and you will incur transaction costs when you trade them. This is known as **slippage**.
- **Chasing Stale Vol:** Your volatility forecast is, by definition, based on past data. If there is a sudden, unexpected event, your forecast will be slow to react. This is a fundamental limitation of any backward-looking risk model.
- **Ignoring the Cost of Leverage:** A volatility targeting strategy may require you to use leverage (i.e., borrow money to invest). The cost of this leverage must be factored into your performance calculations.

## Key Takeaways

-   Risk management is a dynamic, ongoing process.
-   Volatility targeting can help you maintain a constant risk profile and improve your risk-adjusted returns.
-   Beta control is essential for running a market-neutral strategy.
-   Turnover discipline is crucial for minimizing transaction costs.