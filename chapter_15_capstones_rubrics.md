# Chapter 15: Capstones and Rubrics

***

## Prologue: The Final Exam

Welcome to the final chapter. There will be no new material here. There are no more theories to learn, no more formulas to memorize. The time for passive learning is over. The time for active creation has begun. This chapter is your final exam. It is your opportunity to synthesize everything you have learned in this book—from data hygiene to signal processing, from portfolio construction to risk management—and to apply it to a challenging, real-world research project.

The capstone projects in this chapter are not simple exercises with clean, pre-packaged data. They are open-ended, ambiguous, and difficult, just like the real world of quantitative research. They will test not only your technical skills, but also your creativity, your discipline, and your intellectual honesty. Completing one of these projects will be a significant accomplishment. It will be a demonstration that you have moved beyond the role of a student and have begun the journey of a true quantitative professional. This is your chance to build something real, something robust, something you can be proud of. Good luck.

## How to Approach a Quantitative Research Project: A Professional’s Guide

Before you dive into the capstone projects, let’s first discuss a professional framework for approaching a quantitative research project.

**The Scientific Method in Finance:**
Quantitative research is a science, and it should be guided by the principles of the scientific method:
1.  **Formulate a Hypothesis:** Start with a clear, testable hypothesis, grounded in a plausible economic or behavioral story. Why should this strategy work?
2.  **Gather the Data:** Assemble the necessary data to test your hypothesis. This is often the most time-consuming part of the process.
3.  **Design the Experiment (The Backtest):** Design a rigorous backtest to test your hypothesis. This includes defining your universe, your signals, your portfolio construction rules, and your transaction cost assumptions.
4.  **Analyze the Results:** Analyze the results of your backtest in detail. Look not just at the headline performance numbers, but also at the risks, the drawdowns, and the factor exposures.
5.  **Draw a Conclusion:** Based on the evidence, do you accept or reject your original hypothesis? Be honest and objective in your assessment.

**The Importance of a Research Diary:**
Throughout this process, you must keep a detailed **research diary**. This is a log of every single idea you have, every experiment you run, and every decision you make. A research diary serves two crucial purposes:
1.  **It enforces discipline.** By forcing you to write down your hypothesis *before* you run your backtest, it helps to protect you from the sin of data snooping.
2.  **It creates an audit trail.** It provides a complete record of your research process, which is invaluable for debugging, for sharing your work with others, and for protecting your intellectual property.

## Capstone A: The Regime-Aware Global Momentum Strategy

**Project Description:**
This project requires you to build a tactical asset allocation strategy that invests in a diversified universe of global ETFs. The core of the strategy is a simple momentum signal: you will go long the assets that have performed well in the recent past. However, you will add a crucial layer of risk management: a **regime detection model**. You will only take on the momentum exposure when your model indicates that the market is in a “risk-on” regime. During “risk-off” regimes, you will de-risk the portfolio by moving to a more defensive allocation (e.g., cash or government bonds). The investment thesis is that you can capture the powerful momentum premium while avoiding the catastrophic losses that momentum strategies tend to suffer during market crashes.

**Potential Data Sources:**
*   **ETF Prices:** Daily adjusted closing prices for a universe of global ETFs, available from sources like Yahoo Finance or Tiingo.
*   **Regime Indicators:** Macroeconomic and market data for your regime model, available from sources like the Federal Reserve Economic Data (FRED) database.

**Detailed Deliverables:**
1.  **A Research Report (PDF or HTML):** A professional-grade research report that includes:
    *   An executive summary.
    *   A detailed explanation of your investment thesis.
    *   A description of your data sources and your data cleaning process.
    *   A detailed explanation of your momentum signal and your regime detection model.
    *   A summary of your backtest results, including a performance attribution analysis.
    *   A conclusion that summarizes your findings and discusses the potential limitations of your strategy.
2.  **A Jupyter Notebook or R Markdown file:** A clean, well-commented, and reproducible script that contains all of your code.
3.  **An Ablation Analysis:** A specific analysis that shows the performance of the strategy with and without the regime filter. This is crucial for demonstrating the value added by your regime model.

**Granular Rubric:**
| Category | Weight | Description |
|---|---|---|
| **Reproducibility & Code Quality** | 25% | Is the code well-commented and easy to follow? Can a third party reproduce your results exactly using your code and data? |
| **Data Hygiene & PIT Integrity** | 25% | Have you correctly handled all corporate actions? Is your data pipeline robust and well-documented? Is there any possibility of look-ahead bias? |
| **Methodological Rigor** | 25% | Is your backtest methodology sound? Are your transaction cost assumptions realistic? Have you used out-of-sample validation techniques? |
| **Clarity of Communication** | 25% | Is your final report well-written, well-structured, and persuasive? Can a non-technical audience understand your investment thesis and your results? |

## Capstone B: The PEAD + Revisions Anomaly

**Project Description:**
This is a more challenging project that requires you to work with more complex data. The goal is to build a long-only U.S. equity strategy that combines two powerful anomalies: the **Post-Earnings Announcement Drift (PEAD)** and **analyst earnings revisions**. The PEAD anomaly is the tendency for stocks to drift in the direction of their most recent earnings surprise for several weeks or months after the announcement. The revisions anomaly is the tendency for stocks with upwardly revised earnings estimates to outperform. The investment thesis is that by combining these two signals, you can identify stocks with both a fundamental catalyst (the earnings surprise) and a powerful behavioral tailwind (the analyst revisions).

**Potential Data Sources:**
*   **Earnings Announcement Dates and EPS Data:** This is available from commercial vendors like Compustat or FactSet. It is crucial to have the exact date and time of the announcement.
*   **Analyst Estimates Data:** This is available from vendors like I/B/E/S. You will need a point-in-time database of analyst estimates to avoid look-ahead bias.

**Detailed Deliverables:**
1.  **A Point-in-Time Data Pipeline:** The most challenging part of this project will be building a truly point-in-time data pipeline for both the earnings data and the analyst revisions data.
2.  **A Rigorous Backtest:** A backtest of the combined signal, with a detailed analysis of its performance across different sectors, market cap quintiles, and market regimes.
3.  **A Performance Attribution Analysis:** A factor-based attribution analysis to determine how much of the strategy’s return is coming from known factors and how much is true alpha.

**Granular Rubric:**
| Category | Weight | Description |
|---|---|---|
| **Point-in-Time Integrity** | 40% | This is the most important part of the project. Can you prove, beyond a reasonable doubt, that there is no look-ahead bias in your signal construction? |
| **Statistical Significance** | 30% | Is the alpha of your strategy statistically and economically significant after accounting for all transaction costs? Have you used rigorous out-of-sample validation? |
| **Depth of Analysis** | 30% | Have you performed a thorough analysis of the strategy’s risks, costs, and factor exposures? Is your final report well-written and persuasive? |

## Capstone C: The Systematic VRP Harvesting Strategy

**Project Description:**
This project requires you to build a systematic options strategy to harvest the variance risk premium. You will build a portfolio of short-dated, out-of-the-money covered calls and cash-secured puts on a diversified universe of liquid, optionable ETFs. The core of the project will be the development of a set of **risk management filters** to protect the portfolio from the significant tail risk of short option strategies.

**Potential Data Sources:**
*   **Options Data:** Historical daily options data (prices, volumes, implied volatilities, Greeks) is available from vendors like the CBOE or specialized data providers.
*   **Underlying Asset Prices:** Daily adjusted closing prices for the underlying ETFs.

**Detailed Deliverables:**
1.  **A Rule-Based Options Trading Strategy:** A clear and explicit set of rules for selecting which options to sell (underlying, expiration, strike/delta).
2.  **A Set of Risk Management Filters:** This should include:
    *   An IV-RV filter that only sells options when implied volatility is high relative to recent realized volatility.
    *   A regime filter that suspends the strategy during periods of high market stress.
    *   An earnings filter that avoids selling options on individual stocks around their earnings announcements.
3.  **A Tail-Loss Analysis:** A detailed stress test of the strategy against historical and simulated market crashes.

**Granular Rubric:**
| Category | Weight | Description |
|---|---|---|
| **Risk Management** | 40% | How effective are your filters at avoiding large losses? Have you adequately and honestly assessed the tail risk of the strategy? |
| **Net P&L Realism** | 30% | Is your estimate of the strategy’s net P&L realistic, after accounting for all costs, fees, margin requirements, and the cost of hedging? |
| **Clarity of Communication** | 30% | Can you clearly and honestly explain the risks and rewards of your strategy to a potential investor who may not be an options expert? |

## Capstone D: The Cross-Asset Carry Strategy

**Project Description:**
This project requires you to build a diversified portfolio of **carry** strategies across different asset classes. A carry trade is a strategy that seeks to profit from the difference in the yield between two assets. The classic example is the **FX carry trade**, where you borrow a low-interest-rate currency and lend a high-interest-rate currency. But the carry principle can be applied to many other asset classes as well. The goal of this project is to build a diversified portfolio of carry strategies in equities, fixed income, commodities, and currencies.

**Potential Data Sources:**
*   **FX Spot and Forward Rates:** Available from sources like Bloomberg or Reuters.
*   **Government Bond Yields:** Available from central bank websites or FRED.
*   **Commodity Futures Curves:** Available from the CME or other futures exchanges.

**Detailed Deliverables:**
1.  **A Set of Individual Carry Signals:** A clear and explicit definition of the carry signal for each asset class.
2.  **A Diversified Portfolio:** A portfolio that combines the individual carry signals into a single, diversified strategy.
3.  **An Analysis of Diversification Benefits:** A detailed analysis of the correlations between the different carry strategies and the diversification benefits of combining them.

**Granular Rubric:**
| Category | Weight | Description |
|---|---|---|
| **Signal Construction** | 30% | Is your definition of the carry signal for each asset class sensible and well-motivated? |
| **Portfolio Construction** | 30% | Have you constructed a well-diversified portfolio that effectively combines the different carry signals? |
| **Risk Analysis** | 40% | Have you performed a thorough analysis of the risks of the strategy, particularly the risk of a “carry crash” where all carry trades unwind at the same time? |

## Conclusion: The Beginning of Your Journey

This book has given you the tools, the concepts, and the framework to be a successful quantitative investor. But the journey does not end here. The market is a dynamic, ever-evolving teacher. The process of learning, of adapting, of constantly questioning your own assumptions, is a lifelong one. The completion of a capstone project is not the end of your education; it is the beginning of your career. Now, go and build something great.
