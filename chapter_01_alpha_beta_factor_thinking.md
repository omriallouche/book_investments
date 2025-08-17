# Chapter 1 — Alpha, Beta, and Factor Thinking

***

## Why This Chapter Matters

In the last chapter, we laid the groundwork by defining returns. Now, we ask a more profound question: where do those returns come from? The answer, in the world of modern finance, is that returns can be decomposed into two fundamental components: beta and alpha.

**Beta (β)** represents the portion of an asset’s return that is explained by its exposure to broad market movements. If the stock market goes up, most stocks will go up with it. That’s beta at work. It’s the reward for taking on systematic risk, the risk you can’t diversify away.

**Alpha (α)** is the holy grail. It’s the portion of an asset’s return that is *not* explained by beta. It represents a manager’s skill, a unique edge, or a temporary market inefficiency. It’s the return you get without bearing market risk.

Understanding the difference is critical. A manager who delivers high returns might just be taking on a lot of market risk (high beta). A manager who delivers modest returns but with zero market exposure (all alpha) might be the true star. This chapter will give you the tools to tell the difference.

## Core Ideas

- **CAPM (Capital Asset Pricing Model):** The original and simplest factor model. It states that the expected excess return of an asset is proportional to its beta with respect to the market portfolio. The CAPM was a revolutionary idea, but it is now considered to be an incomplete model of the world.

- **Multi-factor Extensions:** The realization that the “market” isn’t the only source of systematic risk. Other factors, such as company size (SMB), value (HML), momentum (UMD), and quality (QMJ), have been shown to have explanatory power over asset returns. We will explore the economic intuition behind these factors in Chapter 3.

- **Cross-Sectional vs. Time-Series Views:** We can think about factor models in two ways. In a **time-series** view, we look at a single asset and see how its returns vary over time as a function of the factors. In a **cross-sectional** view, we look at a group of assets at a single point in time and see how their returns vary as a function of their factor exposures.

- **The Matrix Representation:** The relationship between returns, alpha, beta, and factors can be elegantly expressed in matrix form:

  *r = α1 + Bf + ε*

  Where:
  - *r* is a vector of asset returns.
  - *α* is a vector of alphas.
  - *1* is a vector of ones.
  - *B* is a matrix of factor loadings (betas).
  - *f* is a vector of factor returns.
  - *ε* is a vector of residual returns (the part of the return not explained by the factors).

## Math You’ll Derive

### OLS for β̂ and α̂

The workhorse for estimating betas and alphas is Ordinary Least Squares (OLS) regression. For a single-factor model, the formulas are:

*β̂ = Cov(r, r<sub>m</sub>) / Var(r<sub>m</sub>)*

*α̂ = E[r] - β̂E[r<sub>m</sub>]*

Where *r* is the asset’s excess return and *r<sub>m</sub>* is the market’s excess return. We will extend this to the multi-factor case using matrix algebra. The key assumption of OLS is that the errors are uncorrelated with the independent variables.

### Rolling Stability Tests

Are betas constant over time? Rarely. We can test for this by estimating betas over a rolling window (e.g., 36 months) and observing how they change. This gives us a time-varying estimate, *β<sub>t</sub>*. A plot of the rolling beta can be a powerful diagnostic tool.

### Wald and Chow Tests

These are statistical tests used to determine if there has been a “structural break” in a time series. For example, we could use a Chow test to determine if a company’s beta changed significantly after a merger or acquisition. A significant result would suggest that our single-beta model is misspecified.

### Factor Model Estimation and Residual Properties

After fitting a factor model, we must examine the residuals (*ε*). If the model is a good fit, the residuals should be small, uncorrelated with the factors, and have no discernible patterns. We will use various diagnostic plots and tests, such as the Ljung-Box test for autocorrelation, to assess the quality of our model.

## Narrative Example: The Mystery Winner

A new mutual fund, “Global Growth Leaders,” posts spectacular returns in its first three years, crushing the market. The marketing materials tout the manager’s brilliant stock-picking ability. But is it skill or just a hidden beta bet?

We can investigate by running a factor analysis on the fund’s returns. We might find that the fund has a very high beta to the “momentum” factor. During those three years, momentum stocks were on a tear. The fund’s high returns were not due to the manager’s unique insights (alpha), but rather to a large, implicit bet on a single factor (beta drift).

When the momentum factor inevitably turns, the fund’s performance will likely crash back to earth. This is a classic story of a manager who got lucky by taking on a risk they may not have fully understood.

## Hands-On: Decompose a Stock’s Returns

1.  **Select a stock and factors:** Pick a well-known global company (e.g., Apple, Toyota, Nestlé). Download its monthly returns for the past 10 years from a reputable source. Also, download the returns for a global market index (like MSCI World) and the Fama-French five factors (Market, Size, Value, Profitability, Investment).
2.  **Estimate time-varying betas:** Using a 36-month rolling window, estimate the stock’s time-varying betas to each of these factors. This will give you a time series of beta estimates.
3.  **Decompose returns:** In each month, decompose the stock’s return into the portion attributable to each factor and the residual (alpha). The formula for the factor contribution is simply the factor’s return multiplied by the stock’s beta to that factor.
4.  **Plot and analyze:** Plot the results. How much of the stock’s return is explained by the factors (i.e., what is the R-squared of your regression)? Has the stock’s alpha been consistent over time? Have its factor exposures changed significantly?

## Check Yourself

- What is the difference between a stock’s beta and its correlation to the market?
- How would you interpret a negative alpha?
- If a factor model has an R-squared of 0.8, what does that tell you about the residuals?
- What are the confidence bands on a beta estimate, and what do they represent?

## Common Pitfalls

- **Non-Synchronicity:** Using a U.S. market index to model the returns of a Japanese stock can be problematic because the trading hours don’t overlap. This can lead to artificially low beta estimates.
- **FX Translation Effects:** When modeling global stocks, it’s crucial to use returns that are all denominated in the same currency. A rising stock price can be offset by a falling local currency, and this will affect the estimated beta.
- **Omitted Variable Bias:** If we leave out an important factor from our model, its effect may be wrongly attributed to the factors we *do* include, or to alpha. This is why the search for new factors is a never-ending quest in quantitative finance.

## Key Takeaways

-   Returns can be decomposed into alpha and beta.
-   Beta is the return from exposure to systematic risk factors.
-   Alpha is the return that is not explained by beta.
-   Factor models are the primary tool for distinguishing between alpha and beta.
-   Always be aware of the limitations and potential pitfalls of factor modeling.