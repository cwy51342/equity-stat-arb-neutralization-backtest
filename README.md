# Cross-Sectional Equity Alpha: Dollar-Neutral vs. Sector-Neutral Portfolio Backtest

A quantitative backtesting and risk-attribution study evaluating the impact of **Market (Dollar) Neutralization** and **Sector Neutralization** on cross-sectional equity factor portfolios. The framework compares annualized risk-adjusted performance, maximum drawdown, and historical stress-period resilience across five distinct market regime shocks.

---

## Methodology & Portfolio Construction

Cross-sectional equity strategies often carry unintended directional exposure and industry concentration risks. This project constructs and evaluates three portfolio weighting schemes from raw cross-sectional alpha signals:

1. **Non-Neutral Portfolio:** Raw cross-sectional signal weights without zero-sum dollar or sector constraints, leaving the book exposed to broad market directionality.
2. **Market (Dollar) Neutral Portfolio:** Demeans portfolio weights cross-sectionally across the entire tradable universe at each rebalance period ($\sum_i w_{i,t} = 0$), eliminating net dollar exposure while still permitting cross-sector tilts.
3. **Sector Neutral Portfolio:** Demeans portfolio weights independently within each GICS sector ($\sum_{i \in S_k} w_{i,t} = 0 \quad \forall k$), achieving zero net dollar exposure both across the book and within every industry group to strip out unintended sector tilts.

### Backtest Scope & Assumptions
> *Note: Fill in these 4 specifics directly from `stat_arb_neutralization_backtest.ipynb` before committing.*
* **Alpha Signal:** `[TODO: e.g., 5-day short-term reversal / momentum / composite factor]`
* **Universe & Sample Period:** `[TODO: e.g., S&P 500 / Russell 1000 equities, 2013–2023]`
* **Rebalance Frequency:** `[TODO: e.g., Daily close-to-close / Weekly]`
* **Cost Basis:** Gross returns (pre-transaction costs, slippage, and short-borrow fees) `[TODO: update if net of bps]`

---

## Empirical Performance Summary

Neutralizing both aggregate dollar and sector exposures yields substantial improvements in risk-adjusted performance, lifting the daily annualized Sharpe ratio from **0.40** (Non-Neutral) to **1.78** (Sector Neutral) while compressing maximum drawdown from **-54.54%** to **-15.52%**.

| Metric | Sector Neutral | Market (Dollar) Neutral | Non-Neutral |
| :--- | :---: | :---: | :---: |
| **Daily Annualized Sharpe Ratio** | **1.78** | 1.53 | 0.40 |
| **Average Annual Return** | **15.23%** | 14.50% | 7.44% |
| **Total Cumulative Return** | **152.08%** | 144.79% | 74.27% |
| **Maximum Drawdown** | **-15.52%** | -20.92% | -54.54% |

---

## Historical Stress-Period Attribution

To evaluate tail-risk behavior and factor crowding vulnerability, the three portfolios are stress-tested across five historical market dislocations:

| Historical Stress Regime | Sector Neutral | Market (Dollar) Neutral | Non-Neutral |
| :--- | :---: | :---: | :---: |
| **COVID-19 Crash (Early 2020)** | **-11.46%** | -13.61% | -45.58% |
| **Q4 2018 Selloff (Dec 2018)** | **+3.31%** | +3.58% | +2.03% |
| **China / Yuan Devaluation Shock (Fall 2015)** | **+1.80%** | +2.15% | +4.52% |
| **Ebola / Oil Vol Shock (Oct 2014)** | **+1.04%** | +0.48% | -2.08% |
| **Taper Tantrum / Quant Quake (Aug 2013)** | **-0.11%** | -0.11% | +0.19% |

### Key Takeaways
* **Crash Protection:** During the COVID-19 liquidity shock, the Non-Neutral book suffered a **-45.58%** drawdown, whereas Market Neutral (**-13.61%**) and Sector Neutral (**-11.46%**) significantly curtailed systemic downside.
* **Sector Risk Removal:** Enforcing within-sector dollar neutrality reduced maximum drawdown by **540 bps** relative to simple market dollar-neutrality (-15.52% vs. -20.92%) and improved annualized Sharpe by **+0.25** (1.78 vs. 1.53) by eliminating uncompensated industry concentration.

---

## Known Limitations & Next Steps

* **Dollar-Neutrality vs. True Beta-Neutrality:** Zero-sum dollar weights ($\sum w_i = 0$) can still carry residual market beta if long and short legs differ in realized beta. Next iterations will constrain explicit rolling beta ($\sum w_i \beta_i = 0$) and orthogonalize against statistical/fundamental risk factors (PCA or Barra-style style factors).
* **Turnover & Execution Costs:** Evaluating net-of-cost Sharpe requires incorporating daily turnover tracking, bid-ask spread slippage, market impact, and hard-to-borrow short financing fees.

---

## Repository Contents

* `stat_arb_neutralization_backtest.ipynb` — Full backtesting engine, neutralization transformations, stress-period analytics, and cumulative return / drawdown visualizations.
* `requirements.txt` — Python package dependencies.
