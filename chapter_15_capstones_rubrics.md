# Chapter 15 — Capstones and Rubrics

***

## Why This Chapter Matters

This is the final chapter of the book. It is where you will put everything you have learned into practice. The goal of this chapter is to provide you with a set of challenging, real-world **capstone projects** that will test your knowledge and skills as a quantitative investor. These are not simple exercises with clean, pre-packaged data. These are open-ended research projects that will require you to get your hands dirty.

For each capstone project, we will provide a clear set of **deliverables** and a detailed **rubric** for how your work will be evaluated. The rubrics are designed to be unambiguous and to emphasize the key principles of this book: reproducibility, data hygiene, rigorous evidence, and clear communication.

Completing one or more of these capstone projects will be a significant accomplishment. It will demonstrate that you have mastered the material in this book and that you are ready to begin your journey as a serious, professional-grade quantitative investor.

## Capstone A — Regime-Aware Momentum ETF Tilt (Long-Only)

### Project Description

Build a tactical asset allocation strategy that tilts a long-only portfolio of broad-market ETFs towards the momentum factor, but only when the market is in a “risk-on” regime. The goal is to capture the momentum premium while avoiding the notorious momentum crashes that tend to occur during market turmoil.

### Deliverables

1.  **A Jupyter Notebook or R Markdown file** that contains all of your code, from data download to backtesting to performance analysis.
2.  **A final report** (in PDF or HTML format) that summarizes your methodology, your results, and your conclusions. The report should be well-written, well-structured, and easy to understand for a non-technical audience.
3.  **A performance summary** that includes the Sharpe ratio, maximum drawdown, turnover, and estimated transaction costs of your strategy.
4.  **An ablation analysis** that shows the performance of the strategy with and without the regime gate. This will demonstrate the value added by your regime detection model.

### Rubric

| Category | Weight | Description |
|---|---|---|
| **Reproducibility** | 25% | Can another researcher take your code and data and reproduce your results exactly? Is your code well-commented and easy to follow? |
| **Data Hygiene** | 25% | Have you used point-in-time data? Have you correctly handled dividends and corporate actions? Is your data pipeline robust and well-documented? |
| **Evidence** | 25% | Is your backtest statistically significant? Have you used out-of-sample validation techniques? Is your evidence for the strategy’s effectiveness compelling and robust? |
| **Clarity** | 25% | Is your final report clear, concise, and well-argued? Can a non-expert understand your investment thesis and the evidence you have presented? |

## Capstone B — PEAD + Revisions (Long-Only with Risk Control)

### Project Description

Build a long-only equity strategy that combines the Post-Earnings Announcement Drift (PEAD) anomaly with analyst earnings revisions. The goal is to identify stocks that have recently had a positive earnings surprise and are also seeing upward revisions from analysts. The strategy should also include a robust risk control overlay to manage volatility and drawdowns.

### Deliverables

1.  **A timestamp-correct data pipeline** for both earnings announcement dates and analyst revision dates. This is the most challenging part of the project.
2.  **An embargoed cross-validation** of your combined signal. This will provide a more honest estimate of the signal’s out-of-sample performance.
3.  **A performance attribution analysis** that decomposes the strategy’s returns into market, factor, and specific components.
4.  **A written report** that details your methodology, your results, and your analysis of the strategy’s risks and costs.

### Rubric

| Category | Weight | Description |
|---|---|---|
| **PIT Integrity** | 30% | Have you built a truly point-in-time data pipeline? Can you prove that there is no look-ahead bias in your signal construction? |
| **OOS Performance** | 30% | How well does your strategy perform in a rigorous out-of-sample validation? Is the alpha statistically and economically significant? |
| **Costs** | 20% | Have you included a realistic and conservative estimate of all transaction costs and borrow fees? Is the strategy still profitable after costs? |
| **Write-up** | 20% | Is your report well-written, well-structured, and persuasive? Have you clearly explained the economic intuition behind your strategy? |

## Capstone C — Options Carry Overlay on a Diversified Book

### Project Description

Build a systematic options carry strategy that sells covered calls and cash-secured puts on a diversified portfolio of liquid ETFs. The strategy should include filters to avoid selling options during periods of high risk, such as before earnings announcements or when the market is in a “risk-off” regime.

### Deliverables

1.  **A set of rules** for selecting which options to sell (e.g., strike, expiration, delta).
2.  **An IV-RV filter** that only sells options when the implied volatility is significantly higher than the recent realized volatility.
3.  **A regime/earnings filter** that suspends the strategy during periods of high risk.
4.  **A tail-loss analysis** that stress-tests the strategy against historical and simulated market crashes.

### Rubric

| Category | Weight | Description |
|---|---|---|
| **Risk Control** | 30% | How effective are your filters at avoiding large losses? Have you adequately managed the tail risk of the strategy? |
| **Regime Logic** | 25% | Is your regime detection model sensible and well-motivated? Does it add value to the strategy? |
| **Net PnL Realism** | 25% | Is your estimate of the strategy’s net P&L realistic, after accounting for all costs, fees, and margin requirements? |
| **Communication** | 20% | Can you clearly explain the risks and rewards of your strategy to a potential investor? |

## Key Takeaways

-   The capstone projects are designed to be challenging and to test your understanding of the entire quantitative investment process.
-   A successful project will demonstrate not only your technical skills, but also your ability to communicate your ideas clearly and persuasively.
-   The rubrics provide a clear roadmap for what is expected in each project.
-   Good luck!