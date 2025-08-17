# Chapter 14 — Minimal Math Blocks and Notation (Consolidated)

***

## Why This Chapter Matters

This book has covered a wide range of mathematical and statistical concepts. This chapter serves as a consolidated reference guide to the most important formulas, derivations, and notation used throughout the book. It is designed to be a quick and easy place to look up a definition or to refresh your memory on a key derivation.

There is no new material in this chapter. It is simply a reorganization and condensation of the mathematical content from the previous chapters. Use it as a study guide, a cheat sheet, or a starting point for your own library of quantitative code.

## Core Mathematical Blocks

### Returns

- **Simple Return:** *R<sub>t</sub> = (P<sub>t</sub> / P<sub>t-1</sub>) - 1*
- **Log Return:** *r<sub>t</sub> = ln(P<sub>t</sub> / P<sub>t-1</sub>)*
- **Relationship:** *r<sub>t</sub> = ln(1 + R<sub>t</sub>)*

### Risk and Performance

- **Annualized Log Return:** *252 \* r<sub>d</sub>*
- **Annualized Volatility:** *σ<sub>d</sub> \* √252*
- **Sharpe Ratio:** *(E[R] - R<sub>f</sub>) / σ[R]*

### Factor Models

- **CAPM:** *E[R<sub>i</sub>] - R<sub>f</sub> = β<sub>i</sub>(E[R<sub>m</sub>] - R<sub>f</sub>)*
- **OLS Beta:** *β̂ = Cov(r, r<sub>m</sub>) / Var(r<sub>m</sub>)*
- **OLS Alpha:** *α̂ = E[r] - β̂E[r<sub>m</sub>]*

### Portfolio Construction

- **Softmax Weighting:** *w<sub>i</sub> = e<sup>τs<sub>i</sub></sup> / Σ<sub>j</sub>e<sup>τs<sub>j</sub></sup>*
- **Mean-Variance Optimization:** *max μ<sup>T</sup>w - λw<sup>T</sup>Σw*

### Risk Management

- **EWMA Variance:** *σ̂<sup>2</sup><sub>t</sub> = λσ̂<sup>2</sup><sub>t-1</sub> + (1-λ)r<sup>2</sup><sub>t-1</sub>*
- **Volatility Target Scaling:** *k = σ<sub>tgt</sub> / σ̂*
- **Single-Asset Kelly Criterion:** *ℓ\* ≈ μ / σ<sup>2</sup>*
- **Multi-Asset Kelly Criterion:** *w\* ∝ Σ<sup>-1</sup>μ*

## Key Derivations

### KKT Conditions for Box-Constrained Mean-Variance Optimization

Consider the problem of maximizing the mean-variance objective function subject to a set of box constraints on the weights (e.g., 0 ≤ w<sub>i</sub> ≤ 0.02). The Lagrangian for this problem is:

*L(w, λ, μ) = μ<sup>T</sup>w - λw<sup>T</sup>Σw - Σ<sub>i</sub>λ<sub>i</sub>(w<sub>i</sub> - w<sub>max</sub>) - Σ<sub>i</sub>μ<sub>i</sub>(-w<sub>i</sub>)*

Where *λ<sub>i</sub>* and *μ<sub>i</sub>* are the Lagrange multipliers for the upper and lower bound constraints, respectively.

The KKT conditions are a set of necessary conditions for a solution to be optimal. They state that at the optimal solution, the gradient of the Lagrangian with respect to *w* must be zero, and the complementary slackness conditions must hold. This leads to a set of equations that can be solved to find the optimal portfolio weights.

### Projected Gradient Descent

Projected gradient descent is an iterative algorithm for solving constrained optimization problems. The idea is to take a step in the direction of the gradient of the objective function, and then “project” the resulting point back onto the feasible set defined by the constraints. For box constraints, the projection step is simple: you just cap the weights at their upper and lower bounds.

## Symbol Table

| Symbol | Definition |
|---|---|
| *P<sub>t</sub>* | Price at time *t* |
| *R<sub>t</sub>* | Simple return |
| *r<sub>t</sub>* | Log return |
| *σ* | Volatility (standard deviation) |
| *β* | Beta (factor loading) |
| *α* | Alpha (excess risk-adjusted return) |
| *μ* | Expected return |
| *Σ* | Covariance matrix |
| *w* | Vector of portfolio weights |
| *λ* | Risk aversion parameter or EWMA decay factor |
| *τ* | Softmax concentration parameter |
| *ℓ\** | Optimal Kelly fraction |

## Hands-On: Implement Key Algorithms

To solidify your understanding of these mathematical concepts, it is highly recommended that you implement them from scratch in your favorite programming language. Here are a few suggestions:

1.  **Ledoit-Wolf Shrinkage:** Write a function that takes a time series of asset returns and returns a shrunk covariance matrix using the Ledoit-Wolf formula.
2.  **HAC/Newey-West Standard Errors:** Implement the Newey-West procedure for estimating standard errors of regression coefficients that are robust to heteroskedasticity and autocorrelation.
3.  **Block Bootstrap:** Write a function to perform a block bootstrap on a time series of returns. Use this to construct a confidence interval for the Sharpe ratio.
4.  **Projected Gradient Descent:** Implement the projected gradient descent algorithm to solve a mean-variance optimization problem with box constraints. Compare your results to a off-the-shelf convex optimization library.

## Key Takeaways

-   A solid understanding of the core mathematical concepts is essential for any quantitative investor.
-   This chapter serves as a quick reference guide to the key formulas and notation used in this book.
-   Implementing these algorithms from scratch is a great way to solidify your understanding.