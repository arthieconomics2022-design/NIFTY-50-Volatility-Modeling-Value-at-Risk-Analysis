# NIFTY-50-Volatility-Modeling-Value-at-Risk-Analysis
Analyzed NIFTY 50 returns using statistical diagnostics, ARIMA, GARCH(1,1), and Historical, Parametric, Monte Carlo, and GARCH-based VaR models.
# NIFTY 50 Volatility Modeling & Value at Risk Analysis

## Project Overview

This project analyzes the return dynamics and volatility behavior of the **NIFTY 50 index** using financial time-series models and Value at Risk (VaR) techniques.

The analysis covers daily NIFTY 50 data from **January 2015 to August 2026** and applies statistical diagnostics, ARIMA modeling, GARCH volatility modeling, and multiple VaR approaches to quantify market risk.

The project was developed in Python using financial time-series and statistical modeling techniques.

---

## Objectives

* Analyze the statistical properties of NIFTY 50 returns.
* Test the stationarity of the return series.
* Examine autocorrelation and partial autocorrelation.
* Identify suitable ARIMA specifications.
* Test for the presence of ARCH effects.
* Model time-varying volatility using GARCH(1,1).
* Diagnose the standardized GARCH residuals.
* Estimate market risk using different VaR methodologies.
* Compare historical, parametric, Monte Carlo and GARCH-based VaR estimates.

---

## Dataset

**Asset:** NIFTY 50 Index
**Ticker:** `^NSEI`
**Frequency:** Daily
**Period:** January 2015 – August 2026
**Observations:** 2,871 price observations and 2,870 log-return observations

The historical market data was downloaded using the `yfinance` Python library.

---

## Methodology

### 1. Data Collection

NIFTY 50 historical price data was downloaded using `yfinance`.

The closing price was used to construct the return series.

### 2. Log Returns

Daily logarithmic returns were calculated as:

```text
r_t = ln(P_t / P_(t-1))
```

where:

* `P_t` = current closing price
* `P_(t-1)` = previous closing price

The resulting dataset contains 2,870 daily return observations.

### 3. Descriptive Statistics

The project examines:

* Mean return
* Standard deviation
* Minimum return
* Maximum return
* Quartiles
* Missing observations

The average daily log return was approximately **0.0367%**, while the standard deviation was approximately **1.026%**.

### 4. Time-Series Diagnostics

The return series was examined using:

* Augmented Dickey-Fuller (ADF) test
* ACF
* PACF
* Ljung-Box test
* Residual diagnostics

These tests were used to investigate stationarity and serial dependence in the return series.

### 5. ARIMA Modeling

ARIMA models were evaluated to examine the conditional mean dynamics of NIFTY 50 returns.

Model specifications were compared using information criteria including:

* AIC
* BIC

Residual ACF and PACF were also examined to assess remaining serial dependence.

### 6. ARCH Effect Testing

An ARCH test was performed on the AR model residuals.

The test produced a highly significant result, indicating the presence of conditional heteroskedasticity in the residuals.

This provided motivation for applying a volatility model such as GARCH.

### 7. GARCH(1,1) Model

A GARCH(1,1) model with a zero-mean specification and normally distributed innovations was estimated.

The estimated volatility parameters were:

| Parameter | Estimate |
| --------- | -------: |
| Omega     |   0.0236 |
| Alpha(1)  |   0.1010 |
| Beta(1)   |   0.8752 |

The relatively high persistence captured by the GARCH component indicates that volatility evolves over time rather than remaining constant.

### 8. GARCH Diagnostics

After estimating the GARCH model, standardized residuals were examined using:

* ARCH test
* Ljung-Box test on standardized residuals
* Ljung-Box test on squared standardized residuals

The ARCH test after GARCH produced a p-value of approximately **0.309**, indicating that the remaining ARCH effect was not statistically significant at conventional levels.

---

## Value at Risk Analysis

Four VaR approaches were implemented.

### 1. Historical VaR

Historical simulation was used to estimate the empirical lower-tail quantiles of the return distribution.

Results:

| Confidence Level | Historical VaR |
| ---------------- | -------------: |
| 95%              |       -1.4976% |
| 99%              |       -2.6902% |

### 2. Parametric VaR

Parametric VaR was estimated using the mean and standard deviation of NIFTY 50 returns under a normal-distribution assumption.

Results:

| Confidence Level | Parametric VaR |
| ---------------- | -------------: |
| 95%              |        1.6506% |
| 99%              |        2.3496% |

### 3. Monte Carlo VaR

10,000 simulated returns were generated using the estimated historical mean and standard deviation.

A fixed random seed (`42`) was used to make the simulation reproducible.

Results:

| Confidence Level | Monte Carlo VaR |
| ---------------- | --------------: |
| 95%              |         1.6608% |
| 99%              |         2.3437% |

### 4. GARCH-Based VaR

A one-step-ahead volatility forecast was generated from the GARCH model and incorporated into the VaR calculation.

Forecasted volatility:

**0.5927%**

GARCH-based VaR:

| Confidence Level | GARCH VaR |
| ---------------- | --------: |
| 95%              |   0.9382% |
| 99%              |   1.3421% |

---

## VaR Comparison

| Method      |  95% VaR |  99% VaR |
| ----------- | -------: | -------: |
| Historical  | 1.4976%* | 2.6902%* |
| Parametric  |  1.6506% |  2.3496% |
| Monte Carlo |  1.6608% |  2.3437% |
| GARCH       |  0.9382% |  1.3421% |

*Historical VaR is produced by the notebook as a negative return quantile, while the other VaR measures are reported as positive loss magnitudes.

---

## Key Findings

* NIFTY 50 daily returns exhibit substantial variability and non-constant volatility.
* The ARCH test indicates significant conditional heteroskedasticity in the pre-GARCH residuals.
* The GARCH(1,1) model captures time-varying volatility in the return series.
* Post-GARCH ARCH testing does not indicate significant remaining ARCH effects.
* Historical, parametric, Monte Carlo and GARCH-based approaches produce different estimates of downside market risk.
* The comparison demonstrates why volatility modeling can be important when measuring financial market risk.

---

## Technologies & Libraries

**Programming Language**

* Python

**Libraries**

* NumPy
* Pandas
* Matplotlib
* SciPy
* yfinance
* Statsmodels
* ARCH

**Methods**

* Log returns
* Descriptive statistics
* ADF test
* ACF/PACF
* ARIMA
* ARCH test
* GARCH(1,1)
* Historical VaR
* Parametric VaR
* Monte Carlo VaR

---

## Project Structure

```text
nifty50-volatility-var-analysis/
│
├── monte carlo.ipynb
└── README.md
```

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/nifty50-volatility-var-analysis.git
```

### 2. Install the required libraries

```bash
pip install yfinance pandas numpy matplotlib scipy statsmodels arch
```

### 3. Open the notebook

```bash
jupyter notebook
```

Open:

```text
monte carlo.ipynb
```

Run the cells sequentially.

---

## Disclaimer

This project is intended for **educational and analytical purposes**. The VaR estimates are model-dependent and should not be interpreted as investment advice or as forecasts of future market losses.

---

## Author

**Arthi S**

Applied Quantitative Finance
Financial Analytics | Python | Statistics | Machine Learning
