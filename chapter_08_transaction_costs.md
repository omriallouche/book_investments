# Chapter 8 — Transaction Costs, Borrow, and Execution

***

## Why This Chapter Matters

Up to this point, we have been living in a frictionless, idealized world. We have assumed that we can trade any stock, in any quantity, at any time, for free. This is what we call **paper alpha**. But in the real world, trading is not free. Every time we execute a trade, we incur costs. These costs can be a significant drag on performance, and in some cases, they can turn a profitable strategy into a losing one.

This chapter is about the harsh realities of implementation. It’s about the difference between the return you see in your backtest and the return you actually get in your brokerage account. We will dissect the various components of transaction costs, from the obvious (commissions) to the more subtle (market impact). We will also discuss the practical challenges of shorting stocks, including borrow availability and fees.

As the saying goes, “amateurs talk about returns; professionals talk about costs.” An alpha that cannot survive the friction of the real world is not an alpha worth having.

## Core Ideas

- **Transaction Cost Analysis (TCA):** The process of measuring and analyzing the costs of trading. The main components of transaction costs are:
    - **Spread:** The difference between the price at which you can buy a stock (the ask) and the price at which you can sell it (the bid). This is the most direct and unavoidable cost of trading.
    - **Impact:** The effect that your own trading has on the price of the stock. If you submit a large buy order, you will likely push the price up. This is the most significant cost for large, institutional investors.
    - **Fees:** Commissions paid to your broker, exchange fees, and other regulatory fees.
    - **Taxes:** For taxable investors, capital gains taxes can be a major consideration.

- **Market Impact Models:** The market impact of a trade is not linear. The larger your trade is as a percentage of the stock’s average daily volume (ADV), the larger your impact will be. A common rule of thumb is the **square-root model**:

  *Impact ∝ (size / ADV)<sup>0.5</sup>*

- **Order Types:** The type of order you use to execute your trades can have a big impact on your costs.
    - **Limit Order:** An order to buy or sell at a specific price or better. A limit order protects you from paying more than you want, but it may not be executed if the price moves away from your limit.
    - **TWAP (Time-Weighted Average Price) Order:** An algorithmic order that breaks up a large order into smaller pieces and executes them at regular intervals throughout the day. This is a way to reduce market impact.
    - **IBKR Adaptive Algorithm:** A sophisticated order type offered by brokers like Interactive Brokers that attempts to minimize transaction costs by intelligently timing the execution of your trades.

- **Open/Close Risks:** The opening and closing auctions of the stock market are periods of high liquidity, but also high volatility. There is a risk that a large imbalance of orders at the open or close can cause the price to move sharply against you.

- **Borrow Availability and Fees:** Shorting a stock is not as simple as buying it. You must first borrow the stock from someone who owns it. For some stocks (especially those that are heavily shorted), it can be difficult or expensive to find shares to borrow. The **borrow fee** is the annualized interest rate you must pay to borrow the stock. This fee can range from near zero for liquid, easy-to-borrow stocks to over 100% for some hard-to-borrow names.

## Math You’ll Use

### Cost Decomposition

We can decompose the total transaction cost of a trade into its various components:

*Total Cost = (Execution Price - Arrival Price) + Commissions + Fees*

Where the **Arrival Price** is the mid-point of the bid-ask spread at the moment you decide to trade. The difference between the execution price and the arrival price is a measure of your market impact and the spread.

### Simple Almgren-Chriss Intuition

The Almgren-Chriss model is a mathematical framework for determining the optimal execution schedule for a large trade. The model balances the trade-off between market impact (which you can reduce by trading more slowly) and volatility risk (which you can reduce by trading more quickly). While the full model is complex, the key intuition is that for low-frequency strategies, you should generally trade more slowly to minimize impact.

### Optimal Participation Ceilings

Based on market impact models, we can determine an optimal ceiling for our participation rate in any given stock. For example, we might set a rule that our daily trading volume in a stock should not exceed 10% of its ADV. This is a simple but effective way to control our trading costs.

## Narrative Example: How a 30 bps Edge Vanished in Small Caps

An analyst develops a high-frequency reversal strategy that shows a 30 basis point (0.30%) profit per trade in a backtest. The strategy focuses on small-cap stocks, where these types of inefficiencies are more common.

He convinces his firm to let him trade the strategy with real money. But after a month, he has lost money. What went wrong?

The problem was transaction costs. The backtest had assumed zero costs. In the real world, the small-cap stocks he was trading had very wide bid-ask spreads. The average spread was 40 basis points. So, even before considering commissions or market impact, his strategy was a loser. He was paying 40 bps to get into and out of a trade that only made 30 bps on paper.

This is a classic example of how paper alpha can die at the exchange. A realistic estimate of transaction costs would have shown that the strategy was unprofitable from the start.

## Hands-On: Build a Pre-Trade TCA Model

1.  **Gather data:** For a universe of stocks, gather data on their bid-ask spreads and average daily trading volume (ADV).
2.  **Build a cost model:** Build a simple pre-trade transaction cost model that estimates the total cost of a round-trip trade in each stock. The model should include:
    -   The bid-ask spread.
    -   A market impact component, based on the square-root model. Assume a certain trade size (e.g., $10,000).
    -   A commission component (e.g., $0.005 per share).
3.  **Re-run your backtest:** Take your favorite trading strategy and re-run the backtest, this time subtracting your estimated transaction costs from each trade.
4.  **Analyze the results:** How does this affect the performance of the strategy? Is it still profitable? By how much did the Sharpe ratio decline?
5.  **Re-rank shorts:** Now, re-rank all potential short trades by their borrow cost. How does this change the composition of your short portfolio? Does it improve the performance of the short side of your strategy?

## Check Yourself

- What is the difference between the bid, the ask, and the mid-price?
- What is the main trade-off in the Almgren-Chriss model?
- Why is it generally more expensive to trade small-cap stocks than large-cap stocks?
- What is the difference between a stock being “hard to borrow” and being on the “threshold list”?

## Common Pitfalls

- **Illiquid Fridays:** Trading volume is often lower on Friday afternoons, especially during the summer. This can lead to higher transaction costs.
- **Partial Fills:** Your order may not be completely filled at your desired price. You need to have a plan for how to handle partial fills.
- **Ignoring Queue Position:** In a limit order book, your order is placed in a queue behind other orders at the same price. If there is a large queue of orders in front of you, your order may not be executed for a long time, or at all.
- **Assuming a Single Execution Price:** A large order is rarely executed at a single price. It will likely be broken up into many smaller trades at different prices. You must use the volume-weighted average price (VWAP) of all these trades to calculate your true execution cost.

## Key Takeaways

-   Transaction costs are a major hurdle to profitability.
-   A realistic transaction cost model is an essential part of any backtest.
-   The cost of shorting a stock can be a significant drag on performance.
-   The way you execute your trades can have a big impact on your costs.