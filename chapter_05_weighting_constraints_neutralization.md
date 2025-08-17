# Chapter 5 — Weighting, Constraints, and Neutralization

***

## Why This Chapter Matters

In the previous chapters, we’ve done the hard work of generating promising signals and identifying the current market regime. We now have a list of stocks that we think are likely to outperform. But how do we translate that list into a real-world portfolio? This is the crucial, and often overlooked, step of **portfolio construction**.

It’s not as simple as just buying our top-ranked stocks. We need to decide *how much* of each stock to buy. This is the **weighting** decision. We also need to be mindful of real-world **constraints**, such as limits on our exposure to any single stock, sector, or country. And we need to ensure that our portfolio is not making any unintended bets – a process called **neutralization**.

This chapter is the bridge from abstract scores to a tradable, risk-managed portfolio. A poorly constructed portfolio can turn a great signal into a losing strategy. A well-constructed portfolio can enhance the performance of a good signal and, just as importantly, protect us from ourselves.

## Core Ideas

- **Weighting Schemes:** How do we decide the size of our position in each stock?
    - **Equal-Weight Deciles:** A simple and robust approach. We rank all stocks by our signal, divide them into ten deciles, and then give an equal weight to every stock in the top decile.
    - **Softmax Weighting:** A more sophisticated method that assigns weights based on the magnitude of the signal score. The formula is:

      *w<sub>i</sub> = e<sup>τs<sub>i</sub></sup> / Σ<sub>j</sub>e<sup>τs<sub>j</sub></sup>*

      Where *w<sub>i</sub>* is the weight of stock *i*, *s<sub>i</sub>* is its signal score, and *τ* (tau) is a parameter that controls the concentration of the portfolio. A higher *τ* leads to a more concentrated portfolio.

- **Constraints:** The real world imposes limits on our portfolios. These can include:
    - **Box Constraints:** Limits on the maximum weight of any single position (e.g., no more than 2% of the portfolio).
    - **Sector Constraints:** Limits on our exposure to any single industry (e.g., no more than 20% in technology stocks).
    - **Turnover Constraints:** Limits on how much we can trade in a given period, in order to control transaction costs.
    - **ADV Participation:** Limits on our daily trading volume in a stock as a percentage of its Average Daily Volume (ADV), to avoid moving the price against us.
    - **Cash Buffers:** Holding a certain amount of cash to meet unexpected redemptions or to take advantage of new opportunities.

- **Neutralization:** The process of removing unwanted factor exposures from our portfolio. If our signal is tilted towards small-cap stocks, we might want to neutralize this exposure to make a pure bet on the signal itself. We can do this through:
    - **Residualization:** As we saw in Chapter 3, we can regress our signal on a set of factor exposures and use the residual as a factor-neutral signal.
    - **Optimization:** We can use a portfolio optimizer to build a portfolio that has the highest possible exposure to our desired signal, subject to the constraint that its exposure to all other unwanted factors is zero.

## Math You’ll Use

### Mean-Variance Optimization

The classic portfolio optimization problem, formulated by Harry Markowitz, is to find the portfolio that maximizes return for a given level of risk. The formula is:

**max μ<sup>T</sup>w - λw<sup>T</sup>Σw**

Where:
- *w* is the vector of portfolio weights.
- *μ* is the vector of expected returns (our signal scores).
- *Σ* is the covariance matrix of asset returns.
- *λ* (lambda) is the risk aversion parameter. A higher *λ* means we care more about minimizing risk and less about maximizing return.

### KKT Conditions

The Karush-Kuhn-Tucker (KKT) conditions are the mathematical rules that a portfolio must satisfy to be the optimal solution to a constrained optimization problem. They are a generalization of the Lagrange multiplier method to handle inequality constraints (like our box and sector constraints).

### Ledoit-Wolf Shrinkage

The biggest challenge in mean-variance optimization is estimating the covariance matrix, *Σ*. The historical covariance matrix is often unstable and can lead to extreme and unintuitive portfolio weights. **Shrinkage** is a technique for improving the stability of the covariance matrix by “shrinking” it towards a more structured and stable target, such as the identity matrix. The Ledoit-Wolf method is a popular and effective way to do this.

## Narrative Example: From Top-Decile List to Tradable Portfolio

An analyst has developed a brilliant new signal for predicting earnings surprises. She backtests a simple strategy of buying the top decile of stocks ranked by her signal and holding them for a month. The backtest looks fantastic.

But when she tries to implement the strategy in the real world, she runs into problems. Her top-decile portfolio is heavily concentrated in a few small, illiquid biotech stocks. When she tries to buy them, the price moves against her, and her transaction costs are enormous. The portfolio is also heavily exposed to the momentum factor, which she doesn’t want.

This is where portfolio construction comes in. Instead of just buying the top decile, she could use a mean-variance optimizer with the following constraints:

-   A maximum weight of 2% in any single stock.
-   Sector weights that are within +/- 5% of the benchmark’s sector weights.
-   A beta of 1.0 to the market.
-   Zero exposure to the momentum factor.

The resulting portfolio will have a slightly lower expected return than the original, unconstrained portfolio. But it will be far more robust, tradable, and diversified. It’s a portfolio that can survive the open.

## Hands-On: Compare Weighting Schemes

1.  **Take your composite signal:** Take the composite signal you built in Chapter 3.
2.  **Construct three portfolios:** Construct three different portfolios based on this signal:
    a.  An equal-weight portfolio of the top decile of stocks.
    b.  A softmax-weighted portfolio. Experiment with different values of the concentration parameter, τ.
    c.  A mean-variance optimized portfolio with reasonable constraints (e.g., max weight of 2%, sector constraints).
3.  **Use shrinkage:** For the mean-variance portfolio, use a Ledoit-Wolf shrinkage estimator for the covariance matrix.
4.  **Compare and analyze:** Compare the performance and characteristics of the three portfolios. Look at:
    -   Risk-adjusted returns (Sharpe ratio).
    -   Turnover.
    -   Concentration (Herfindahl index).
    -   Exposure to common risk factors (beta, sectors, etc.).
    -   Plot the portfolio weights of each strategy over time. How do they differ?

## Check Yourself

- What is the purpose of the *τ* parameter in the softmax weighting scheme?
- What are the KKT conditions, and why are they important for portfolio optimization?
- Why is the historical covariance matrix often a poor input for a mean-variance optimizer?
- How would you build a portfolio that is neutral to the US dollar?

## Common Pitfalls

- **Optimizer Instability:** Mean-variance optimizers are notoriously sensitive to small changes in the inputs (expected returns and covariances). This can lead to large, unjustified swings in the portfolio weights. Using shrinkage and robust constraints is essential.
- **Covariance Mis-estimation:** The covariance matrix is the most important, and most difficult, input to get right. A poorly estimated covariance matrix can lead to a portfolio that looks optimal on paper but is actually very risky.
- **Hidden Factor Bets:** If you don’t explicitly neutralize your portfolio’s exposure to known factors, you may be making a large, unintended bet. Always run a factor analysis on your final portfolio to understand where your risk is coming from.
- **Ignoring Transaction Costs:** The optimal portfolio on paper may be very expensive to trade. We will address this in detail in Chapter 8.

## Key Takeaways

-   Portfolio construction is the crucial step that translates signals into a tradable portfolio.
-   There are many different ways to weight stocks, from simple equal-weighting to sophisticated mean-variance optimization.
-   Real-world constraints, such as limits on position sizes and turnover, must be incorporated into the portfolio construction process.
-   Neutralizing unwanted factor exposures is essential for building a pure bet on your signal.