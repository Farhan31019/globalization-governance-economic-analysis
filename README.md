# Cross-National Empirical Analysis of Globalization, Governance, and Economic Distribution

![IBM SPSS Statistics](https://img.shields.io/badge/IBM%20SPSS-29.0-blue?style=flat&logo=ibm)
![ETL Pipeline](https://img.shields.io/badge/ETL-Power%20Query-green)
![Methodology](https://img.shields.io/badge/Reporting-APA%207th%20Edition-brightgreen)
![Status](https://img.shields.io/badge/Status-Completed-success)

An end-to-end comparative political economy study investigating the institutional, macroeconomic, and distributional consequences of globalization across 215 nations and territories. The project demonstrates an end-to-end data pipeline from multi-source data extraction and ETL to parametric/non-parametric assumption testing, bivariate correlation, and Ordinary Least Squares (OLS) regression modeling in IBM SPSS Statistics.

---

## 📌 Project Overview

This study addresses core theoretical debates in comparative politics—specifically contrasting **Modernization Theory** against **Dependency/Critical Perspectives**—by examining how cross-national integration influences institutional democratization, economic growth, and domestic income inequality. 

Key research questions investigated:
1. **Democratic Accountability:** Does deeper globalization foster civic liberties, political participation, and institutional transparency?
2. **Economic Expansion:** How strongly does global integration predict national wealth per capita?
3. **Distributional Equity:** Does globalization systematically compress or expand the relative income share of the poorest 20% of society?

---

## 📊 Summary of Key Empirical Findings

| Analysis Type | Model / Variable Pairing | Sample Size (N) | Key Test Statistic & p-Value | Substantive Empirical Conclusion |
| :--- | :--- | :--- | :--- | :--- |
| **OLS Linear Regression (Model 1)** | Voice & Accountability vs. KOFGI | N = 188 | R² = .332, F(1, 186) = 92.29, p < .001 | Globalization is a strong, positive predictor (Beta = .576, B = 0.039, p < .001); explains 33.2% of variance in democratic accountability. |
| **OLS Linear Regression (Model 2)** | GDP per Capita vs. KOFGI | N = 188 | R² = .160, F(1, 186) = 35.32, p < .001 | Globalization significantly predicts national wealth (Beta = .399, B = 663.73, p < .001); each 1-point increase yields ~$663.73 USD/capita. |
| **OLS Linear Regression (Model 3)** | Income Share Lowest 20% vs. KOFGI | N = 85 | R² = .114, F(1, 83) = 10.66, p = .002 | Moderate positive association (Beta = .337, B = 0.051, p = .002); refutes claims that global integration depresses bottom-tier income share. |
| **Parametric Correlation (Pearson r)** | KOFGI with Voice, GDP, and Lowest 20% | N = 85 to 188 | Voice (r = .576, p < .001), GDP (r = .399, p < .001), Lowest 20% (r = .337, p = .002) | All relationships are positive and statistically significant (p < .01) using pairwise missing-case exclusion. |
| **Non-Parametric Correlation (Spearman rho)** | KOFGI with Voice, GDP, and Lowest 20% | N = 85 to 188 | Voice (rho = .527, p < .001), GDP (rho = .654, p < .001), Lowest 20% (rho = .387, p < .001) | Rank-order correlation confirms robust monotonic relationships, especially correcting for skewed income distributions. |
| **Normality Diagnostics** | Shapiro-Wilk Tests on Model Variables | N = 85 | KOFGI (p = .013), Voice (p = .011), Lowest 20% (p = .037), GDP (p < .001) | GDP per capita exhibited severe positive skewness (Skewness = 1.882); justified the paired reporting of non-parametric statistics. |

---

## 🛠️ Data Sources & Variable Architecture

All data were harmonized for the cross-sectional benchmark year **2015** using standardized 3-letter ISO country codes:

* **Independent Variable:**
  * `KOFGI`: KOF Overall Globalization Index (KOF Swiss Economic Institute) — Continuous scale measuring economic, social, and political dimensions.
* **Dependent Variables:**
  * `Voice_Accountabilit`: Voice and Accountability Index (Worldwide Governance Indicators - WGI) — Captures perceptions of civic participation, freedom of expression, and free media.
  * `GDP_per_Capita`: Gross Domestic Product per capita in current US$ (World Bank WDI).
  * `Income_Lowest20`: Percentage share of income or consumption accrued to the lowest 20% of the income distribution (World Bank WDI).
* **Control / Contextual Variables:**
  * `FDI_Inflows`: Foreign direct investment net inflows (current US$, World Bank WDI).
  * `Trade_Pct_GDP`: Merchandise trade as a percentage of GDP (World Bank WDI).

---

## ⚙️ Analytical & Methodological Pipeline

1. **Data Engineering & ETL (Power Query):**
   * Harmonized multi-source flat files via Left-Outer joins on ISO-3 entity keys (`code` $\rightarrow$ `Country_Code`).
   * Cleaned database-level missing tokens (`..`) by casting to valid `null` system-missing states.
   * Reshaped horizontal indicator series into normalized, single-year columnar structures.
2. **Missing Data Management Strategy:**
   * **Pairwise Deletion** was utilized for bivariate correlation analyses to retain maximal degrees of freedom ($N = 188$ for macro indicators, $N = 85$ for survey-dependent inequality data).
   * **Model-Specific Listwise Deletion** was enforced during OLS estimation to prevent synthetic imputation bias across distinct causal models.
3. **Assumption Verification:**
   * **Normality & Linearity:** Assessed through Kolmogorov-Smirnov/Shapiro-Wilk statistics, skewness/kurtosis thresholds, and scatter plot inspection.
   * **Autocorrelation:** Evaluated using Durbin-Watson tests ($DW \in [1.748, 2.203]$), verifying the absence of first-order error correlation.
   * **Outlier Screening:** Residual statistics confirmed standardized residuals fell within acceptable parameters without distorting regression gradients.

---

## 📂 Repository Contents

```text
├── data/
│   ├── raw/                            # Original source files from KOF, World Bank WDI, and WGI
│   └── processed/                      # Harmonized analytical dataset (Globalization_SPSS_2015.xlsx / .sav)
├── syntax/
│   └── globalization_analysis.sps       # SPSS syntax script for reproducibility
├── outputs/
│   ├── tables/                         # Exported APA summary, correlation, and regression tables
│   └── figures/                        # Scatter plots with linear regression fit lines
├── docs/
│   └── globalization_research_report.pdf # Complete academic paper and theoretical analysis
└── README.md                           # Core project documentation and empirical summary
