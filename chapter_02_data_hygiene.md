# Chapter 2 — Data Hygiene and Research Integrity (Point-in-Time or Bust)

***

## Why This Chapter Matters

This might be the most important chapter in the entire book. You can have the most brilliant investment idea, the most sophisticated model, and the most powerful computers. But if your data is flawed, your results will be worthless. Garbage in, garbage out.

This chapter is about building a fortress around your research process. It’s about preventing the two most insidious and common errors in quantitative finance: **survivorship bias** and **look-ahead bias**. These errors are like ghosts in the machine; they are subtle, hard to detect, and they will haunt your backtests, making them look far better than they would have been in reality.

Before you write a single line of code for a trading signal, you must first become a data detective. Your mantra must be: **Point-in-Time or Bust.**

## Core Ideas

- **Point-in-Time (PIT) Data:** This is the golden rule. A PIT database is a perfect snapshot of the world as it was known *at that exact moment in time*. It includes all the data that was available, and it excludes all the data that was not. For example, if a company restates its earnings, a PIT database will show the original, incorrect earnings figure until the date of the restatement, at which point it will be updated.

- **Revisions and Restatements:** Companies frequently revise their financial statements. A non-PIT database will often just show the latest, revised number, making it seem like you had access to information that was not actually public at the time. This is a classic form of look-ahead bias.

- **Corporate Actions:** These are events that have a material impact on a company’s stock price and share structure. They include:
    - **Splits:** A 2-for-1 stock split doubles the number of shares and halves the price. Your price data must be adjusted to account for this.
    - **Dividends:** When a company pays a dividend, its stock price typically drops by a corresponding amount. Your returns must be calculated on a **total return** basis, which includes dividends.
    - **Spinoffs:** A company may spin off a division into a new, independent company. Shareholders of the parent company will receive shares in the new company.
    - **Delistings:** Companies that go bankrupt or are acquired are removed from the stock exchange. This is the primary source of **survivorship bias**. If you only include the “survivors” in your backtest, your results will be artificially inflated.

- **Event Timestamps:** Knowing the exact date and, if possible, the time of an event is critical. Did a company release its earnings report before the market opened or after it closed? The answer can have a huge impact on how you model the market’s reaction.

- **Exchange Calendars and Time Zones:** Trading days and hours vary across the globe. A holiday in Japan might be a trading day in London. You must have a precise calendar for each exchange you trade on.

## Math/Procedures

### Total-Return Reconstruction

To accurately calculate historical returns, you must reconstruct a total return series from raw price and corporate action data. The formula for a daily total return is:

*TR<sub>t</sub> = (P<sub>t</sub> + D<sub>t</sub> - S<sub>t</sub>) / P<sub>t-1</sub> - 1*

Where:
- *P<sub>t</sub>* is the split-adjusted price at time *t*.
- *D<sub>t</sub>* is the dividend per share paid on day *t*.
- *S<sub>t</sub>* is the value of any spinoffs or other distributions on day *t*.

It is crucial that the corporate action data is applied on the correct ex-dividend date.

### Event-Time Alignment

When studying the impact of an event (like an earnings announcement), we often want to align multiple stocks in “event time.” Day 0 is the day of the announcement. Day -1 is the day before, and Day +1 is the day after. This allows us to aggregate the results of many different events that happened on different calendar dates.

### Block Bootstrap vs. IID Bootstrap

When we test the statistical significance of our results, we often use a technique called bootstrapping, which involves resampling our data with replacement. However, if the data is autocorrelated (as financial time series often are), the standard “independent and identically distributed” (IID) bootstrap is not appropriate. The **block bootstrap** is a more robust technique that involves resampling blocks of consecutive data points, thus preserving the autocorrelation structure. The choice of block size is a critical parameter in this procedure.

## Narrative Example: The Backtest That “Beat the Market”

A young, ambitious analyst builds a backtest of a simple value strategy. He downloads a list of all the stocks in the S&P 500 *today*, and then pulls their historical financial data for the past 20 years. He buys the 10% of stocks with the lowest Price-to-Book ratio and rebalances annually.

The results are astonishing. The strategy delivers a 25% annualized return, crushing the market. The analyst is hailed as a genius.

But there’s a fatal flaw. By using the list of S&P 500 companies from *today*, he has committed survivorship bias. He has unknowingly excluded all the companies that were in the S&P 500 at some point in the past 20 years but have since gone bankrupt or been acquired. These are, by definition, the losers. His backtest only included the winners, the companies that were successful enough to survive for 20 years.

A more careful researcher would have used a point-in-time list of index constituents for each year of the backtest. The results of this more realistic backtest would have been far less impressive.

## Hands-On: Recreate an Index

This is a challenging but incredibly valuable exercise.

1.  **Obtain historical constituents:** Obtain a list of the historical constituents of a major stock index (like the S&P 500) for a specific period (e.g., the last 5 years). This data can be found in historical archives or purchased from specialized data vendors.
2.  **Gather raw data:** Find a source for raw, unadjusted daily price data and corporate action data for all of these stocks. Ensure your corporate action data includes ex-dates and payment dates.
3.  **Build the index:** Write the code to create a daily time series of the index’s total return, as if you were calculating it in real-time. You will need to handle all corporate actions and constituent changes correctly.
4.  **Compare and reconcile:** Compare your reconstructed index to the actual published index return. Can you match it perfectly? If not, can you explain the discrepancies? This process of reconciliation is a powerful way to uncover subtle data issues.
5.  **Create an audit log:** Build an “audit log” that tracks every adjustment you make to the data. This will be an invaluable tool for debugging and for demonstrating the integrity of your process.

## Check Yourself

- What is the difference between a price return and a total return?
- How would you handle a 3-for-2 stock split in your price data?
- What is the danger of using a database that does not provide point-in-time financial data?
- Can you produce a “provenance report” for your data, tracing it back to its original source?

## Common Pitfalls

- **Vendor Defaults:** Never trust a data vendor’s default settings. Always ask detailed questions about how they handle corporate actions, restatements, and other data issues.
- **Daylight Saving Mismatches:** A subtle but real problem. Time zone conversions must correctly account for daylight saving rules, which can vary from year to year and country to country.
- **Earnings Time Ambiguity:** A company might report earnings on “May 10th.” But was that before the market opened, after it closed, or during trading hours? The exact timestamp is crucial, and often hard to find.
- **Ignoring the Cost of Data:** High-quality, point-in-time data is expensive. But the cost of making bad decisions based on flawed data is far higher.

## Key Takeaways

-   Data hygiene is the foundation of all quantitative research.
-   Survivorship bias and look-ahead bias are the two most dangerous errors in backtesting.
-   Always use point-in-time data.
-   A detailed audit trail is your best defense against data errors.