# Table of Contents - Quantitative Investment Strategies

## Part I — Foundations

### [Chapter 0 — Orientation: Markets, Returns, and Your Math Toolkit](chapter_00_orientation.md)
- **Why:** Establish common language; prevent notation drift and compounding mistakes
- **Core ideas:** Asset classes; simple vs. log returns; excess returns; compounding; volatility drag; covariance; stationarity caveats
- **Math you'll derive:** Log vs. simple return relationships; annualization rules; HAC/Newey–West SEs for autocorrelated returns
- **Narrative example:** Two portfolios with same mean/σ but different skew—why wealth paths diverge
- **Hands-on:** Build a "returns micro-library" (vectorized); confirm identities with toy data
- **Check yourself:** Convert between daily/log/annual metrics correctly
- **Pitfalls:** Mixing currencies and returns; annualizing Sharpe on overlapping windows

### [Chapter 1 — Alpha, Beta, and Factor Thinking](chapter_01_alpha_beta_factor_thinking.md)
- **Why:** Separate market exposure from skill
- **Core ideas:** CAPM; multi-factor extensions; cross-sectional vs. time-series views; matrix r=α1+Bf+ε
- **Math:** OLS for β̂,α̂; rolling stability tests; Wald/Chow; factor model estimation and residual properties
- **Narrative:** A "mystery winner" explained by beta drift vs. true alpha
- **Hands-on:** Estimate time-varying betas for global names; decompose returns into factor/specific
- **Check:** Interpret confidence bands on βt; explain residual diagnostics
- **Pitfalls:** Non-synchronicity; FX translation effects on beta

### [Chapter 2 — Data Hygiene and Research Integrity (Point-in-Time or Bust)](chapter_02_data_hygiene.md)
- **Why:** Prevent leakage and survivorship bias before you write a single signal
- **Core ideas:** PIT data; revisions/restatements; corporate actions; event timestamps; exchange calendars/time zones
- **Math/Procedures:** Total-return reconstruction; event-time alignment; block bootstrap vs. iid bootstrap
- **Narrative:** The backtest that "beat the market" by forgetting delisted losers
- **Hands-on:** Build audit logs; recreate an index from raw quotes + corp actions
- **Check:** Re-run any experiment from a snapshot; produce a provenance report
- **Pitfalls:** Vendor defaults; daylight saving mismatches; earnings time ambiguity

## Part II — Signals and Regimes

### [Chapter 3 — Signal Families: Value, Momentum, Quality, Accruals, Revisions, Crowding](chapter_03_signal_families.md)
- **Why:** Turn economic hypotheses into computable, PIT signals
- **Core ideas:** Exact definitions (12–1 momentum with skip month; EBIT/EV, FCF/EV; ROIC; accruals; SUE; revisions breadth; days-to-cover, borrow fee)
- **Math:** Robust winsorization; z-scores; composite scoring; sector/beta neutralization via regression residuals
- **Narrative:** "Cheap or trap?"—a cyclical with ugly optics but strong quality
- **Hands-on:** Build a value+quality composite; replicate 12–1 momentum; measure crash exposure
- **Check:** Show sector-neutral vs. raw performance delta
- **Pitfalls:** IFRS vs. GAAP mapping; stale analyst data; short-borrow fees erased gains

### [Chapter 4 — Regime Detection: When Edges Change Sign](chapter_04_regime_detection.md)
- **Why:** Tail risk and Sharpe are regime-dependent
- **Core ideas:** Term spreads; credit OAS; VIX term structure ratios; breadth; cross-asset trends
- **Math:** Two-state HMM likelihood; logistic/XGBoost with probability calibration; Brier score; threshold selection for actionability
- **Narrative:** Credit spreads whisper before equities scream
- **Hands-on:** Train an HMM monthly; compute regime probabilities; gate gross exposure
- **Check:** Out-of-sample calibration plot; drawdown-conditioned performance
- **Pitfalls:** Publication lags; overfitting to a single crisis; unstable features

## Part III — From Scores to Portfolios

### [Chapter 5 — Weighting, Constraints, and Neutralization](chapter_05_weighting_constraints_neutralization.md)
- **Why:** Bridge from signal ranks to tradable positions
- **Core ideas:** Equal-weight deciles; softmax wi=eτsi/∑jeτsj; box/sector/turnover constraints; ADV participation; cash buffers
- **Math:** Mean-variance maxμ⊤w−λw⊤Σw; KKT conditions; Ledoit–Wolf shrinkage; residualization for beta/sector neutrality
- **Narrative:** Turning a top-decile list into a portfolio that survives the open
- **Hands-on:** Compare equal-weight vs. softmax vs. MV on the same scores and risk target
- **Check:** Exposure dashboard: beta, sector, country, currency, crowding
- **Pitfalls:** Optimizer instability; covariance mis-estimation; hidden factor bets

### [Chapter 6 — Volatility Targeting, Beta Control, and Turnover Discipline](chapter_06_volatility_targeting.md)
- **Why:** Control risk first; alpha follows
- **Core ideas:** EWMA/GARCH vol; target scaling k=σtgt/σ̂; rolling beta; index/futures hedges; trade bands; cost-aware rebalancing
- **Math:** EWMA σ̂t2; hedge-ratio; turnover penalty c∑|wt−wt−1|
- **Narrative:** The strategy that "won" by avoiding position size whiplash
- **Hands-on:** Add vol targeting + trade bands; quantify turnover and costs saved
- **Check:** Same expected return, lower DD and ulcer index
- **Pitfalls:** Overreactive λ; hedge slippage; chasing stale vol

## Part IV — Evidence and Costs

### [Chapter 7 — Validation and Overfitting Control](chapter_07_validation_overfitting.md)
- **Why:** Credibility > backtest beauty
- **Core ideas:** Walk-forward; purged K-Fold with embargo; lockbox; multiple-testing control (Deflated Sharpe Ratio)
- **Math:** DSR; variance of Sharpe; embargo sizing vs. label horizon
- **Narrative:** The champion model that flopped OOS—and why the lockbox saved face
- **Hands-on:** Re-evaluate your best signal with purged CV; report DSR
- **Check:** Distinct train/validation/test timelines with embargo rationale
- **Pitfalls:** Hyperparameter seepage; selecting on OOS; peeking at the lockbox

### [Chapter 8 — Transaction Costs, Borrow, and Execution](chapter_08_transaction_costs.md)
- **Why:** Paper alpha dies at the exchange
- **Core ideas:** Spread, impact (square-root ∝(size/ADV)0.5), fees, taxes; order types; open/close risks; borrow availability/fees
- **Math:** Cost decomposition; simple Almgren–Chriss intuition; optimal participation ceilings
- **Narrative:** How a 30 bps edge vanished in small caps with wide spreads
- **Hands-on:** Pre-trade TCA model; re-rank shorts by borrow cost
- **Check:** Net vs. gross PnL attribution; slippage within budget
- **Pitfalls:** Illiquid Fridays; partial fills; ignoring queue position

## Part V — Overlays and Advanced Topics

### [Chapter 9 — Options Carry and the Variance Risk Premium (CC & CSP)](chapter_09_options_carry.md)
- **Why:** Systematically harvest IV>RV while managing left tails
- **Core ideas:** IV vs. RV; Δ/Θ/Vega/Γ; skew; ex-div assignment; regime filters
- **Math:** Carry P&L decomposition; realized vol estimation; parity links; margin mechanics
- **Narrative:** "Getting paid to wait": when selling puts mimics limit buying
- **Hands-on:** Monthly CC overlay on a diversified ETF with a regime gate
- **Check:** Theta harvested vs. tail losses; vega exposure controlled
- **Pitfalls:** Earnings weeks; vol spikes; thin ex-US options markets

## Part VI — Practice, Governance, and Capstones

### [Chapter 10 — Practical Implementation (Low-Frequency, IBKR-Friendly)](chapter_10_practical_implementation.md)
- **Why:** Ship a robust monthly/quarterly process
- **Core ideas:** Cadence; snapshotting; config/versioning; deterministic seeds; earnings-aware execution windows; attribution
- **Math/Process:** Rebalance calendar design; failure-mode playbooks
- **Narrative:** The runbook that prevented an earnings-week blow-up
- **Hands-on:** Build a "one-pager" operations runbook + research diary template
- **Check:** Reproducible run from cold start; clean PnL lineage
- **Pitfalls:** Silent vendor revisions; parameter drift; environment mismatch

### [Chapter 11 — Typical Pitfalls (Red-Team Your Strategy)](chapter_11_typical_pitfalls.md)
- **Why:** Consolidate failure patterns and fixes
- **Catalogue:** Leakage; too many knobs; under-modeling costs; capacity illusions; unmanaged exposures
- **Hands-on:** Red-team exercise: find one plausible leakage path and eliminate it
- **Check:** Independent reviewer signs off on PIT, costs, and capacity checks

### [Chapter 12 — Risk and Money Management (Drawdowns, Kelly, and Friends)](chapter_12_risk_money_management.md)
- **Why:** Survive long enough to compounding
- **Core ideas:** Drawdown, Sharpe, IR, Sortino, Calmar; fractional Kelly; risk budgets across sleeves
- **Math:** Single-asset ℓ*≈μ/σ2; multi-asset w*∝Σ−1μ; skew-adjusted Sharpe; Omega ratio
- **Narrative:** Cutting gross during a 12–15% DD without killing recovery
- **Hands-on:** Implement circuit-breakers; compare terminal wealth and ulcer index
- **Check:** Risk budget adherence; DD profile improved vs. baseline

### [Chapter 13 — Ethics, Regulation, and the Edge You Want to Keep](chapter_13_ethics_regulation.md)
- **Why:** Stay on the right side of the line; design for fairness and robustness
- **Core ideas:** MNPI/insider trading basics; Reg FD/MiFID-style principles; data licensing and web-scrape pitfalls; backtest marketing ethics; client suitability; audit trails
- **Narrative:** The well-meaning analyst and the "leaky" alternative dataset
- **Hands-on:** Build a compliance checklist for your research/data sources
- **Check:** Every dataset has provenance, license, and MNPI risk assessment

### [Chapter 14 — Minimal Math Blocks and Notation](chapter_14_math_notation.md)
- **Why:** One place to look up the recurring derivations and symbols
- **Blocks:** EWMA/GARCH; softmax mapping; risk contributions; Ledoit–Wolf shrinkage; HAC/Newey–West; block bootstrap; hedge-ratio formulas; symbol table
- **Hands-on:** Derive KKT for box-constrained MV; implement projected gradient

### [Chapter 15 — Capstones and Rubrics](chapter_15_capstones_rubrics.md)
- **Capstone A — Regime-Aware Momentum ETF Tilt (long-only):**
  - Deliverables: Notebook + report; SR, DD, turnover, cost budget; ablation on regime gate
  - Rubric: Reproducibility (25), hygiene (25), evidence (25), clarity (25)
- **Capstone B — PEAD + Revisions (long-only with risk control):**
  - Deliverables: Timestamp-correct pipeline; embargoed CV; attribution vs. market/factors
  - Rubric: PIT integrity (30), OOS performance (30), costs (20), write-up (20)
- **Capstone C — Options Carry Overlay on a Diversified Book:**
  - Deliverables: CC/CSP rules; IV–RV filter; regime/earnings filter; tail-loss analysis
  - Rubric: Risk control (30), regime logic (25), net PnL realism (25), communication (20)

---

## Teaching Design Features
- **Dual-lane exposition:** Intuition boxes alongside derivation corners
- **Cognitive load management:** "You-are-here" maps; margin summaries; consistent notation
- **Assessment:** Exit-ticket questions + 5-point rubric; small datasets for completion in one sitting
- **Global lens:** Currency choice, FX impact decomposition, IFRS/GAAP mapping notes, holiday/auction effects

## Learning Outcomes
By the end of this course, students will be able to:
1. Design and implement quantitative investment strategies from first principles
2. Navigate the pitfalls of backtesting and overfitting
3. Build robust, production-ready investment systems
4. Understand the ethical and regulatory landscape of quantitative finance
5. Complete end-to-end projects with measurable outcomes and clear rubrics 