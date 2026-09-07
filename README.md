<div align="center">

# 🔬 Return Transmission & Herding Behavior in the Semiconductor Sector

### Financial Econometrics — Final Assessment · MSc International Business Management & Finance

<p>
  <img src="https://img.shields.io/badge/R-276DC3?style=for-the-badge&logo=r&logoColor=white" alt="R"/>
  <img src="https://img.shields.io/badge/Quarto-39729E?style=for-the-badge&logo=quarto&logoColor=white" alt="Quarto"/>
  <img src="https://img.shields.io/badge/Rennes%20School%20of%20Business-002B5C?style=for-the-badge" alt="RSB"/>
</p>

<p>
  <img src="https://img.shields.io/badge/tickers-44-blue?style=flat-square" alt="44 tickers"/>
  <img src="https://img.shields.io/badge/period-2018--2025-blue?style=flat-square" alt="2018-2025"/>
  <img src="https://img.shields.io/badge/status-completed-brightgreen?style=flat-square" alt="completed"/>
  <img src="https://img.shields.io/badge/herding-not%20detected-orange?style=flat-square" alt="no herding"/>
</p>

**Is NVIDIA's success just its own, or is the whole semiconductor chain moving together?**
PCA · Robust OLS · Logistic Regression · CSAD Herding Test · EGARCH Volatility Modeling

</div>

<div align="center">

### 📓 [**View the full interactive analysis (rendered notebook) →**](https://ludodelot.github.io/rsb-financial-econometrics-semiconductors/)

</div>

---

## 📌 TL;DR

| Question | Answer |
|---|---|
| Do semiconductor-chain returns move together? | ✅ Yes — 6 market factors (PCA) explain **82.2%** of the variance behind NVIDIA's daily moves |
| Do investors herd into these stocks? | ❌ **No** — NVDA / AMD / QCOM / TSM actually *diverge* more when the market swings hard |
| Is volatility "normal" in this sector? | ❌ No — fat tails everywhere (kurtosis 7.72 on NVDA), asymmetric shocks (bad news hits harder) |
| Can direction of returns be predicted? | 🎯 **80% accuracy** with a simple logit on 6 principal components |

---

## 📂 Table of Contents
1. [Research question](#-research-question)
2. [Data](#-data)
3. [Methods & key findings](#-methods--key-findings)
4. [Visuals](#-visuals)
5. [Conclusion](#-conclusion)
6. [Repo contents](#-repo-contents)
7. [Stack](#%EF%B8%8F-stack)

---

## ❓ Research question

> Is there a significant relationship between the stock returns of companies operating at different stages of the global semiconductor supply chain — **design** (NVIDIA, AMD), **manufacturing** (TSMC, Intel), and **equipment** (ASML)?

- **H₀** — no significant relationship.
- **H₁** — there is a significant relationship.

<details>
<summary>💬 Why this topic (personal motivation)</summary>

> "At this moment NVIDIA is the most valuable company in the world, driven by the boom in AI and data, and I personally hold NVIDIA in my investment portfolio... I currently work at LVMH, and even in the luxury sector I see increasing investment in AI, data systems, and digital infrastructure."
> — from the original research question

</details>

## 📊 Data

- **44 tickers** from Yahoo Finance, **2018-01-01 → 2025-10-24**
- Full value chain: *Design* (NVDA, AMD, AVGO, QCOM…) · *Manufacturing* (TSM, INTC, MU…) · *Equipment* (ASML, AMAT, LRCX…) · *Materials* · *OSAT* · *Distributors* · sector ETFs (SOXX, SMH, XSD)
- Macro controls: S&P 500, NASDAQ, VIX, 10Y yield, T-Bill, US Dollar Index, WTI, Copper, AAPL, TSLA
- **Panel data**: time series × cross-section

## 🧮 Methods & key findings

<table>
<tr><th>Section</th><th>Method</th><th>Result</th></tr>
<tr>
<td><b>Distribution</b></td>
<td>Shapiro-Wilk, Jarque-Bera, skew/kurtosis</td>
<td>NVDA log-returns <b>not normal</b> (p≈0) · skew -0.194 · kurtosis 7.72 → 🐘 fat tails</td>
</tr>
<tr>
<td><b>Regression</b></td>
<td>PCA (44 tickers → 6 PCs) + OLS, HC3 robust SE</td>
<td>6 PCs explain <b>82.19%</b> of variance · Adj. R² = <b>0.5062</b> · only PC1 significant (p=0.0007)</td>
</tr>
<tr>
<td><b>Classification</b></td>
<td>Logistic regression (return sign ~ 6 PCs)</td>
<td>🎯 Accuracy <b>0.80</b> · AIC = 32.21</td>
</tr>
<tr>
<td><b>Herding</b></td>
<td>CSAD (Chang–Cheng–Khorana) vs. Rm, Rm² — NVDA/QCOM/TSM/AMD, 2020–2025</td>
<td>β₂ = <b>+2.126</b> (significant, positive) → <b>no herding</b>: stocks diverge, not converge</td>
</tr>
<tr>
<td><b>Volatility</b></td>
<td>Ljung-Box + ARCH-LM (p&lt;0.001) → EGARCH(1,1) + ARMA(1,1), Student-t, on SOXX</td>
<td>Leverage effect γ₁=0.167 · persistence β₁=<b>0.96</b> · spikes around COVID-19, 2022 inflation, 2024-25 AI correction</td>
</tr>
<tr>
<td><b>Factor Analysis</b></td>
<td>PCA on all 44 tickers</td>
<td>6 PCs explain 74.5%. PC1 = broad semi-market factor · PC2 = macro/rates · PC5 = tech momentum</td>
</tr>
</table>

## 🖼️ Visuals

<table>
<tr>
<td width="50%"><img src="figures/corr_heatmap_cluster_A4.png" alt="Correlation heatmap"/><p align="center"><sub>Correlation clusters across the semiconductor value chain</sub></p></td>
<td width="50%"><img src="figures/lead_lag_impact_map_A4.png" alt="Lead-lag impact map"/><p align="center"><sub>Lead-lag impact map between segments</sub></p></td>
</tr>
<tr>
<td width="50%"><img src="figures/monthly_heatmap_A4.png" alt="Monthly returns heatmap"/><p align="center"><sub>Monthly return seasonality</sub></p></td>
<td width="50%"><img src="figures/EDA_NVDA_A4.png" alt="NVDA EDA"/><p align="center"><sub>NVIDIA exploratory data analysis</sub></p></td>
</tr>
</table>

## ✅ Conclusion

The results **support H₁**: semiconductor-chain returns are significantly linked through common market factors (PCA). But there is **no evidence of herding** among the sector's biggest names — investors react differently to information rather than following the crowd.

> 💡 **For portfolio management**: intra-sector diversification still has value, but risk models need to account for fat tails and asymmetric volatility (EGARCH) — not just normal-distribution assumptions.

<details>
<summary>⚠️ Limitations (self-critique from the original report)</summary>

- Potential omitted-variable bias — only a subset of the value chain was included.
- PCA reduces but doesn't eliminate the risk of hidden factors.
- Daily-return focus may miss longer-term structural trends.
- Normality doesn't hold for raw returns (expected in finance), though final OLS residuals happened to look normal in this small sample.

</details>

## 📁 Repo contents

| File | Description |
|---|---|
| [`analysis.qmd`](analysis.qmd) | Full R/Quarto source — data pull, EDA, PCA, OLS/Logit, CSAD herding test, EGARCH |
| [`docs/index.html`](docs/index.html) | Rendered notebook — served live via [GitHub Pages](https://ludodelot.github.io/rsb-financial-econometrics-semiconductors/) (GitHub doesn't render raw `.html` files in-browser, so this is the way to actually read it without downloading) |
| [`Report.pdf`](Report.pdf) | Full written report with interpretation of every result |
| [`LLM_Usage_Disclosure.pdf`](LLM_Usage_Disclosure.pdf) | Official AI-usage disclosure (required by the course) |
| `figures/` | Key charts (correlation heatmap, lead-lag map, monthly heatmap, NVDA EDA) |

## 🛠️ Stack

<p>
<img src="https://img.shields.io/badge/tidyquant-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/rugarch-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/FinTS-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/PerformanceAnalytics-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/ggplot2-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/sandwich%20%2F%20lmtest-blue?style=flat-square"/>
</p>

---

<div align="center">

**Author:** [Ludovic Delot](https://github.com/ludodelot) — MSc International Business Management & Finance, Rennes School of Business

</div>
