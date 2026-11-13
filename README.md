# Cross-Sectional Equity Alpha: Market-Neutral vs. Sector-Neutral Portfolio Backtest

A quantitative backtesting and risk-attribution study evaluating the impact of **Market Neutralization** and **Sector Neutralization** on cross-sectional equity factor portfolios[cite: 18]. The framework compares annualized risk-adjusted performance, maximum drawdown, and historical stress-period resilience across five distinct market regime shocks[cite: 18].

---

## Methodology & Portfolio Construction

Cross-sectional equity strategies often carry unintended directional beta and industry concentration risks. This project constructs and evaluates three portfolio weighting schemes from raw alpha signals[cite: 18]:

1. **Non-Market Neutral Portfolio:** Raw cross-sectional signal weights without zero-sum dollar or sector constraints, leaving the book exposed to broad market directionality[cite: 18].
2. **Market Neutral Portfolio:** Demeans portfolio weights cross-sectionally across the entire tradable universe at each rebalance period ($\sum_i w_{i,t} = 0$), eliminating net dollar/market exposure while allowing cross-sector tilts[cite: 18].
3. **Sector Neutral Portfolio:** Demeans portfolio weights within each GICS sector independently ($\sum_{i \in S_k} w_{i,t} = 0 \quad \forall k$), neutralizing both aggregate market beta and unintended industry/sector factor bets[cite: 18].

---

## Empirical Performance Summary

Neutralizing both market and sector exposures yields substantial improvements in risk-adjusted returns, boosting the daily annualized Sharpe ratio from **0.40** (Non-Market Neutral) to **1.78** (Sector Neutral) while compressing maximum drawdown from **-54.54%** to **-15.52%**[cite: 18].

| Metric | Sector Neutral | Market Neutral | Non-Market Neutral |
| :--- | :---: | :---: | :---: |
| **Daily Annualized Sharpe Ratio** | **1.78** | 1.53 | 0.40 |
| **Average Annual Return** | **15.23%** | 14.50% | 7.44% |
| **Total Cumulative Return** | **152.08%** | 144.79% | 74.27% |
| **Maximum Drawdown** | **-15.52%** | -20.92% | -54.54% |

---

## Historical Stress-Period Attribution

To evaluate tail-risk behavior and factor crowding vulnerability, the three portfolios are stress-tested across five historical market dislocations[cite: 18]:

| Historical Stress Regime | Sector Neutral | Market Neutral | Non-Market Neutral |
| :--- | :---: | :---: | :---: |
| **COVID-19 Crash (Early 2020)** | **-11.46%** | -13.61% | -45.58% |
| **Q4 2018 Selloff (Dec 2018)** | **+3.31%** | +3.58% | +2.03% |
| **China / Yuan Devaluation Shock (Fall 2015)** | **+1.80%** | +2.15% | +4.52% |
| ** Ebola / Oil Vol Shock (Oct 2014)** | **+1.04%** | +0.48% | -2.08% |
| **Taper Tantrum / Quant Quake (Aug 2013)** | **-0.11%** | -0.11% | +0.19% |

### Key Takeaways
* **Crash Protection:** During the COVID-19 liquidity shock, the Non-Market Neutral book suffered a **-45.58%** drawdown, whereas Market Neutral (**-13.61%**) and Sector Neutral (**-11.46%**) isolated pure alpha and preserved capital[cite: 18].
* **Sector Risk Removal:** Enforcing sector neutrality reduced maximum drawdown by **540 bps** compared to simple dollar-neutrality (-15.52% vs. -20.92%) and increased the annualized Sharpe ratio by **+0.25** (1.78 vs. 1.53) by stripping out uncompensated industry beta[cite: 18].

---

## Repository Contents

* `stat_arb_neutralization_backtest.ipynb` — Full backtesting engine, neutralization transformations, stress-period analytics, and cumulative return / drawdown visualizations.
* `requirements.txt` — Python package dependencies.
