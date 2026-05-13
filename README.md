# Malaysia Retirement Adequacy Analysis — MASA Hackathon 2025

An analytical study of Malaysia's retirement readiness, examining wage trends, demographic shifts, EPF savings, and macroeconomic indicators through exploratory data analysis, time series forecasting, and regression modeling.

> **Event:** Malaysian Actuarial Student Association (MASA) Hackathon 2025  
> **Team Members:** Wong Zhi Zhong · Nur Haziqah Binti Mohammad · Koh Yu Xuan · Daniel Lam Theen Seong · Cheng Yee Ern

---

## Overview

Malaysia faces a growing retirement adequacy challenge driven by an aging population, stagnating real wages, and insufficient EPF savings. This project uses publicly available datasets to:

1. **Explore** salary distributions, demographic trends, and EPF contribution patterns
2. **Forecast** key economic and demographic variables 20 years into the future
3. **Model** individual income determinants using regression analysis

## Key Findings

- The 60+ population is projected to grow significantly, straining the pension system
- Wage growth lags behind inflation in certain periods, eroding purchasing power
- Gender pay gaps persist across all age groups
- Fertility rates continue to decline, compounding the aging population problem
- EPF savings are insufficient for a large segment of retirees

## Methodology

| Stage | Techniques |
|-------|-----------|
| EDA | Trend analysis, distribution analysis, correlation analysis, data visualization |
| Synthetic Data | Log-normal income simulation calibrated to DOSM wage statistics |
| Time Series | ARIMA, Auto ARIMA, ETS, Auto ETS with Box-Cox transforms and cross-validation |
| Regression | Linear regression with feature engineering (age², gender dummies) |
| Model Selection | AIC/BIC, RMSE, MAE, time-series cross-validation (TSCV) |

### Variables Forecasted
- **Wages** — Auto ARIMA (champion)
- **GDP Growth** — ARIMA(2,1,1) (champion)
- **Aging Population (60+)** — Auto ARIMA with Box-Cox (champion)
- **Inflation** — ARIMA(2,1,5) with Box-Cox (champion)
- **Unemployment** — ARIMA(1,1,1) (champion)
- **Male/Female Mortality** — ARIMA with structural break adjustment (champion)
- **Fertility Rate** — ARIMA(1,1,2) with Box-Cox (champion)

## Project Structure

```
├── EDA.qmd                  # Main analysis (Quarto document)
├── data/
│   ├── raw/                 # Source datasets (MASA-provided + external)
│   │   ├── birth.csv
│   │   ├── employment.csv
│   │   ├── epf contribution rates.csv
│   │   ├── epf data.csv
│   │   ├── epf savings.csv
│   │   ├── fertility.csv
│   │   ├── female mortality.csv
│   │   ├── gdp growth.csv
│   │   ├── hh_income.csv
│   │   ├── inflation.csv
│   │   ├── male mortality.csv
│   │   ├── population.csv
│   │   └── wage.csv
│   └── processed/           # Generated / cleaned datasets
│       ├── births.csv
│       ├── final_wage.csv
│       ├── retiree_summary.csv
│       └── synthetic_income_data.csv
├── Hackathon.Rproj          # RStudio project file
├── .gitignore
└── README.md
```

## Data Sources

| Dataset | Source |
|---------|--------|
| Wages, Employment, Population, Births, EPF Savings | MASA (Hackathon-provided) |
| Household Income | [DOSM Open Data](https://open.dosm.gov.my/data-catalogue/hh_income) |
| EPF Financial Data | [data.gov.my](https://archive.data.gov.my/data/dataset/employees-provident-fund) |
| GDP Growth | [World Bank](https://data.worldbank.org/indicator/NY.GDP.MKTP.KD.ZG?locations=MY) |
| Inflation (CPI) | [World Bank](https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG?locations=MY) |
| Male Mortality | [World Bank](https://data.worldbank.org/indicator/SP.DYN.AMRT.MA?locations=MY) |
| Female Mortality | [World Bank](https://data.worldbank.org/indicator/SP.DYN.AMRT.FE?locations=MY) |
| Fertility Rate | [World Bank](https://data.worldbank.org/indicator/SP.DYN.TFRT.IN?locations=MY) |
| Household Size | [Khazanah Research Institute](https://www.krinstitute.org/assets/contentMS/img/template/editor/Part1_KRI_SOH_2018.pdf) |

## Tech Stack

- **Language:** R
- **Document:** Quarto (`.qmd`)
- **Key Packages:** `tidyverse`, `fpp2`, `tidymodels`, `caret`, `GGally`, `gt`, `modelsummary`, `truncdist`

## Getting Started

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/MASA-Hackathon-2025-EDA.git
   ```
2. Open `Hackathon.Rproj` in RStudio
3. Install dependencies
   ```r
   install.packages(c("tidyverse", "fpp2", "tidymodels", "GGally", 
                       "caret", "naniar", "gridExtra", "gt", 
                       "modelsummary", "truncdist"))
   ```
4. Render the analysis
   ```r
   quarto::quarto_render("EDA.qmd")
   ```

## License

This project was developed for the MASA Hackathon 2025. All external datasets are subject to their respective licenses.
