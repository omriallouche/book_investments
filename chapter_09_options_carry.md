# Chapter 9 — Options Carry and the Variance Risk Premium (CC & CSP)

***

## Why This Chapter Matters

In the previous chapters, we have focused exclusively on trading the underlying assets (stocks). But there is a whole other world of financial instruments that we can use to express our views and generate returns: **options**.

This chapter introduces two of the most popular and robust options strategies: **covered calls (CC)** and **cash-secured puts (CSP)**. These are not speculative, directional bets. They are systematic strategies for harvesting a persistent risk premium known as the **variance risk premium (VRP)**.

The VRP is the empirical fact that the implied volatility of options is, on average, higher than the subsequent realized volatility of the underlying asset. In other words, options are systematically overpriced. By selling options, we can collect this premium, which is a form of **carry**. This is a powerful source of alpha that is largely uncorrelated with traditional stock and bond returns.

But selling options is not a free lunch. It comes with its own unique set of risks, particularly **tail risk**. This chapter will teach you how to harvest the VRP while managing the significant risks involved.

## Core Ideas

- **Implied vs. Realized Volatility:**
    - **Implied Volatility (IV):** The market’s forecast of future volatility, as implied by the price of an option. You can think of it as the “price” of an option.
    - **Realized Volatility (RV):** The actual, historical volatility of the underlying asset over a given period.
    - The **variance risk premium** is the difference between IV and RV.

- **The “Greeks”:** The measures of an option’s sensitivity to various factors:
    - **Delta (Δ):** The change in an option’s price for a $1 change in the price of the underlying asset.
    - **Theta (Θ):** The change in an option’s price for a one-day change in the time to expiration. This is the source of our carry.
    - **Vega (ν):** The change in an option’s price for a 1% change in implied volatility.
    - **Gamma (Γ):** The change in an option’s delta for a $1 change in the price of the underlying asset.

- **Skew:** The fact that out-of-the-money puts are generally more expensive (have a higher IV) than out-of-the-money calls. This is because investors are willing to pay a premium for protection against market crashes.

- **Ex-Dividend Assignment:** If you are short a call option on a stock that is about to pay a dividend, you may be assigned early (i.e., forced to sell your shares) by an investor who wants to capture the dividend. You must be aware of this risk.

- **Regime Filters:** The VRP is not constant. It tends to be highest during periods of market stress. We can use the regime detection models we built in Chapter 4 to time our entry and exit from these strategies. For example, we might only sell options when credit spreads are tight and the VIX term structure is in contango.

## Math You’ll Use

### Carry P&L Decomposition

The profit and loss (P&L) of a short option position can be decomposed into its various components:

*P&L ≈ (Θ \* dt) + (Δ \* dS) + (Γ/2 \* dS<sup>2</sup>) + (ν \* dIV)*

Where:
- *dt* is the change in time.
- *dS* is the change in the underlying price.
- *dIV* is the change in implied volatility.

Our goal is to harvest the **theta** while minimizing our losses from the other components.

### Realized Volatility Estimation

We can estimate the realized volatility of an asset by taking the standard deviation of its daily log returns and annualizing it:

*RV = σ<sub>daily</sub> \* √252*

### Parity Links

Put-call parity is a fundamental relationship that links the prices of European puts and calls on the same underlying asset:

*C - P = S - K*e<sup>-rT</sup>*

Where:
- *C* is the price of the call.
- *P* is the price of the put.
- *S* is the price of the underlying asset.
- *K* is the strike price.
- *r* is the risk-free rate.
- *T* is the time to expiration.

This relationship is the foundation of option pricing theory.

### Margin Mechanics

When you sell an option, you are required to post margin with your broker. The margin is a form of collateral that protects the broker in case you are unable to meet your obligations. The margin requirements for short option positions can be complex and can change with market conditions.

## Narrative Example: “Getting Paid to Wait”

An investor wants to buy a large-cap, dividend-paying ETF. The current price is $100, but she thinks she can get a better price if she is patient. Instead of placing a limit order to buy at $95, she sells a cash-secured put with a strike price of $95.

Let’s say she collects a premium of $2 for selling this put. Two things can happen:

1.  The ETF price stays above $95. The put expires worthless, and she keeps the $2 premium. She has effectively been “paid to wait” for her desired entry price.
2.  The ETF price falls below $95. She is assigned on the put and is forced to buy the ETF at $95. However, her effective purchase price is only $93 ($95 strike - $2 premium). She has bought the ETF at a discount to her original target price.

This is the power of selling cash-secured puts. It’s a conservative strategy that can be used to generate income and to enter long positions at a lower price.

## Hands-On: Build a Covered Call Overlay

1.  **Select an underlying:** Take a diversified portfolio of stocks or a broad market ETF (like SPY).
2.  **Implement the overlay:** Implement a monthly covered call overlay on this portfolio. Each month, sell a 30-day, out-of-the-money call option against your long position. A common choice is to sell a call with a delta of 30.
3.  **Add a regime filter:** Now, add a regime filter to this strategy. Only sell the covered call if your regime model from Chapter 4 indicates that we are in a “risk-on” environment.
4.  **Analyze the results:** Analyze the results in detail. How does the covered call overlay affect the portfolio’s:
    -   Total return?
    -   Volatility and Sharpe ratio?
    -   Skewness and maximum drawdown?
    -   Theta harvested vs. tail losses?
    -   Vega exposure?
5.  **Stress test:** Stress test the strategy by simulating a large, sudden spike in volatility. How does the strategy perform in this scenario?

## Check Yourself

- What is the difference between implied volatility and historical volatility?
- Why do we sell out-of-the-money options in a carry strategy?
- What is the main risk of a covered call strategy?
- What is the main risk of a cash-secured put strategy?

## Common Pitfalls

- **Earnings Weeks:** Implied volatility tends to be very high in the week leading up to a company’s earnings announcement. This can make it tempting to sell options. However, the risk of a large price move on the earnings day is also very high. Many systematic option sellers avoid selling options during earnings weeks.
- **Volatility Spikes:** A sudden, sharp spike in volatility can cause large losses for an option seller. This is the main tail risk of these strategies. It is crucial to have a plan for managing these events, such as buying back your short options or hedging with VIX futures.
- **Thin Ex-US Options Markets:** The options markets in the United States are the most liquid and competitive in the world. In many other countries, the options markets are much thinner, with wider bid-ask spreads and fewer available strikes and expirations. This can make it more difficult and expensive to implement these strategies on a global basis.
- **Assignment Risk:** As mentioned earlier, you must be aware of the risk of early assignment, especially for call options on dividend-paying stocks.

## Key Takeaways

-   The variance risk premium is a persistent source of alpha in the options market.
-   Covered calls and cash-secured puts are two simple and effective strategies for harvesting the VRP.
-   Selling options is not a free lunch. You must be aware of the tail risks involved.
-   Regime filters can be used to improve the risk-adjusted returns of option-selling strategies.