# Chapter 9: Options Carry and the Variance Risk Premium

***

## Prologue: The Insurance Company of the Stock Market

Imagine you are in the business of selling insurance. Every day, people come to you and ask you to protect them against some future, uncertain event. You sell them a policy, and in return, they pay you a premium. Most of the time, the event they are worried about does not happen, and you simply keep the premium as profit. But occasionally, the event does happen, and you are forced to pay out a large claim. The key to being a successful insurance company is to ensure that, on average, the premiums you collect are greater than the claims you pay out.

Now, imagine that the event your clients are worried about is a sharp, sudden move in the stock market. They are willing to pay you a premium to protect them from this risk. You, as the insurer, can sell them a policy that will pay out if the market moves by more than a certain amount. This policy is called an **option**. The premium they pay you is the price of the option. By selling this option, you have just entered the business of selling insurance on the stock market. You have become a seller of **volatility**.

This chapter is your introduction to this fascinating business. It is about a powerful and persistent source of alpha known as the **variance risk premium (VRP)**. The VRP is the empirical fact that the “insurance premium” embedded in the price of options is, on average, systematically higher than the actual, subsequent cost of the claims. By systematically selling options, we can act like a disciplined insurance company, collecting a steady stream of premium income. But this is not a free lunch. It is a strategy that comes with its own unique and significant risks, particularly the risk of a rare, catastrophic event. This chapter will teach you how to harvest this premium while managing the inherent **tail risk**.

## The World of Options: A Brief Primer

An option is a contract that gives the buyer the **right**, but not the obligation, to buy or sell an underlying asset at a specified price (the **strike price**) on or before a specified date (the **expiration date**). There are two basic types of options:
*   **Call Option:** Gives the buyer the right to *buy* the underlying asset.
*   **Put Option:** Gives the buyer the right to *sell* the underlying asset.

For every buyer of an option, there must be a seller. The seller of an option has the **obligation** to fulfill the terms of the contract if the buyer chooses to exercise their right.

This leads to four basic option positions:
1.  **Long Call:** You buy a call option, betting that the price of the underlying asset will go up.
2.  **Short Call:** You sell a call option, betting that the price will not go up significantly.
3.  **Long Put:** You buy a put option, betting that the price of the underlying asset will go down.
4.  **Short Put:** You sell a put option, betting that the price will not go down significantly.

## The Variance Risk Premium (VRP): The “Secret” Alpha of the Options Market

The central concept in this chapter is the variance risk premium. To understand it, we must first understand the difference between two types of volatility.

**Implied vs. Realized Volatility: A Deep Dive**
*   **Realized Volatility (RV):** This is the actual, historical volatility of the underlying asset. We can measure it by calculating the standard deviation of the asset’s daily log returns over a given period and then annualizing it. Realized volatility is a backward-looking measure.
*   **Implied Volatility (IV):** This is the market’s forecast of the future volatility of the underlying asset over the life of the option. It is not directly observable. Instead, it is the value of volatility that, when plugged into an option pricing model like the **Black-Scholes model**, yields the current market price of the option. You can think of implied volatility as the “price” of volatility. It is a forward-looking measure.

The **variance risk premium (VRP)** is the simple but powerful empirical observation that, over long periods of time, implied volatility is systematically higher than subsequent realized volatility. In other words, the market consistently overpays for options. The VRP is the difference between the two: *VRP = IV - RV*.

**Why Does the VRP Exist?**
There are two main explanations for the existence of this persistent premium:
1.  **The Risk Aversion Story:** Most investors are risk-averse. They are more concerned about losing money than they are about making money. They are willing to pay a premium for insurance against large, adverse market moves. This is especially true for protection against market crashes (puts). This persistent demand from buyers of insurance pushes up the price of options, creating a premium for the sellers of that insurance.
2.  **The Limits to Arbitrage Story:** If options are systematically overpriced, why don’t arbitrageurs come in and drive the price down? The answer is that shorting volatility is a risky and capital-intensive business. A seller of options faces the risk of large, potentially unlimited losses if the market makes a sharp move. This risk, and the capital required to manage it, prevents arbitrageurs from completely eliminating the VRP.

## The Greeks: The DNA of an Option’s Risk

To be a successful option seller, you must have a deep and intuitive understanding of the various risks you are taking on. These risks are quantified by a set of sensitivity measures known as the **Greeks**.

*   **Delta (Δ):** This is the most important Greek. It measures the change in an option’s price for a $1 change in the price of the underlying asset. A call option has a positive delta (it becomes more valuable as the stock price goes up), while a put option has a negative delta. An at-the-money option has a delta of approximately 0.5 (for a call) or -0.5 (for a put).
*   **Gamma (Γ):** This measures the change in an option’s delta for a $1 change in the price of the underlying asset. It is the second derivative of the option price with respect to the underlying price. Gamma is highest for at-the-money options and near expiration. A long option position has positive gamma, while a short option position has negative gamma. Negative gamma is the primary source of risk for an option seller. It means that as the market moves against you, your losses will accelerate.
*   **Theta (Θ):** This measures the change in an option’s price for a one-day change in the time to expiration. It is the source of our carry. An option is a decaying asset. All else being equal, its value will decline as it gets closer to expiration. This time decay is theta. A short option position has positive theta; you make money every day just from the passage of time.
*   **Vega (ν):** This measures the change in an option’s price for a 1% change in implied volatility. A long option position has positive vega, while a short option position has negative vega. This is another major source of risk for an option seller. If you are short options and implied volatility spikes, you will suffer large losses.

## The Strategies: Harvesting the VRP

Now, let’s look at two of the simplest and most popular strategies for systematically harvesting the VRP.

### The Covered Call (CC)

**The Mechanics:**
A covered call strategy involves two positions:
1.  A long position in an underlying asset (e.g., 100 shares of a stock).
2.  A short call option on that same asset.

The position is “covered” because if the call option is exercised, you already own the shares that you are obligated to deliver.

**The Risk-Return Profile:**
By selling the call option, you receive a premium, which provides you with an immediate source of income. This income enhances your return if the stock price stays flat or goes up modestly. It also provides a small cushion if the stock price goes down. The “cost” of the covered call is that you give up the potential for unlimited upside gains. If the stock price rallies sharply above the strike price of your call, your gains will be capped.

### The Cash-Secured Put (CSP)

**The Mechanics:**
A cash-secured put strategy involves two positions:
1.  A short put option on an underlying asset.
2.  A cash position large enough to buy the shares if the put option is exercised.

The position is “cash-secured” because you have the cash on hand to meet your obligation to buy the stock if the price falls below the strike price.

**The Risk-Return Profile:**
By selling the put option, you receive a premium. If the stock price stays above the strike price, the option expires worthless, and you keep the premium. If the stock price falls below the strike price, you are forced to buy the stock at the strike price. However, your effective purchase price is the strike price minus the premium you received. This is a conservative strategy that can be used to generate income and to enter a long stock position at a discount.

**The Equivalence of the CC and the CSP:**
It is a fundamental principle of option pricing theory that a covered call is synthetically equivalent to a cash-secured put. This can be proven using the **put-call parity** relationship. This means that the two strategies have the exact same risk-return profile. The choice between them is often a matter of convenience or broker margin rules.

## The Real World: Practical Considerations for Option Sellers

**Strike Selection:**
The choice of strike price is a crucial decision. A common approach is to use **delta** as a guide. For example, a systematic covered call strategy might sell a call option with a delta of 30 each month. This means that the option has roughly a 30% chance of expiring in-the-money. A lower delta means a more conservative strategy with a lower premium but a higher probability of success. A higher delta means a more aggressive strategy with a higher premium but a lower probability of success.

**Expiration Selection:**
The choice of expiration date involves a trade-off. Theta decay is not linear; it accelerates as you get closer to expiration. This means that short-dated options offer the highest potential theta per day. However, they also have the highest gamma risk. A common choice for systematic option sellers is to sell options with around 30 to 45 days to expiration. This provides a good balance between theta decay and gamma risk.

**Managing Assignment Risk:**
If you are short a call option on a dividend-paying stock, you face the risk of **early assignment**. An investor who is long the call may choose to exercise it just before the ex-dividend date in order to capture the dividend. You must be aware of this risk and have a plan for how to manage it.

**The Volatility Skew:**
The **volatility skew** (or “smile”) is the empirical fact that out-of-the-money puts tend to have a higher implied volatility than out-of-the-money calls. This is a direct result of the risk aversion of investors; they are willing to pay a large premium for protection against market crashes. This means that the VRP is generally larger for puts than for calls. Many systematic VRP harvesting strategies focus primarily on selling puts.

## Conclusion: The Disciplined Insurer

The variance risk premium is one of the most persistent and well-documented sources of alpha in all of finance. It is a reward for taking on a risk that most investors are unwilling to bear: the risk of a sudden, sharp move in the market. The strategies of selling covered calls and cash-secured puts are simple, powerful, and robust ways to harvest this premium.

But selling options is not a path to easy riches. It is a business that requires discipline, patience, and a deep respect for risk. The successful option seller is not a speculator; they are a disciplined insurance company. They know that they will have to pay out claims from time to time. But they also know that if they are prudent in their underwriting (their strike and expiration selection) and they manage their risks carefully, they can collect a steady stream of premium income that will, over the long run, more than compensate them for the occasional loss. They are the house, and the house, in the long run, always has an edge.
