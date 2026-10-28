
# High-Frequency Bitcoin Volatility Estimation & Forecasting

### Realised Variance | Garman-Klass Estimator | High-Frequency Data | Statistical Forecasting


**Project Type:** Individual Data Science Project  
**Domain:** Quantitative Finance | Cryptocurrency Markets | Financial Risk Analytics  
**Technologies:** Python, Pandas, NumPy, Scikit-learn, Statsmodels, Matplotlib, Seaborn

---

## 1. Business Problem

Cryptocurrency markets exhibit rapid price fluctuations, fragmented liquidity and significant volatility.

For traders, financial institutions and risk management teams, understanding intraday volatility is essential for monitoring market risk and evaluating short-term trading conditions.

However, accurately forecasting volatility is challenging because cryptocurrency markets operate continuously and are influenced by rapidly changing trading activity.

### Research Questions

- How does Bitcoin price behaviour differ across cryptocurrency exchanges?
- Can high-frequency trading data be used to estimate intraday volatility?
- Which volatility estimators capture short-horizon market fluctuations?
- Does historical volatility predict future volatility?
- Does trading volume provide additional predictive information?

**Objective:** Develop a high-frequency Bitcoin volatility estimation and forecasting framework using trade-level market data and evaluate its predictive reliability.

---

## 2. Dataset & Data Engineering

### Dataset Overview

| Attribute | Description |
|---|---|
| Asset | Bitcoin (BTC) |
| Observation Period | 1–31 December 2018 |
| Data Frequency | Trade-level, high frequency |
| Dataset Size | Over 5 million transactions |
| Exchange Coverage | Four cryptocurrency exchanges |
| Variables | Timestamp, Price, Volume, Exchange ID |

### Data Preparation

The raw dataset was processed using Python to enable time-series analysis.

Key steps included:

1. Loading and structuring trade-level observations.
2. Correcting timestamp formatting inconsistencies.
3. Converting timestamps into datetime objects.
4. Sorting transactions chronologically.
5. Checking missing and invalid price or volume observations.
6. Investigating duplicate timestamps and extreme returns.
7. Resampling high-frequency trades into standardised time intervals.

A robust Median Absolute Deviation (MAD) approach was used to identify extreme one-minute return observations.

### Exchange Selection

Missing five-minute intervals were assessed across four exchanges.

| Exchange | Missing Five-Minute Intervals |
|---|---:|
| Exchange 1 | 21 |
| Exchange 2 | 1 |
| Exchange 3 | 0 |
| Exchange 4 | 4 |

**Decision:** Exchange 3 was selected for detailed volatility modelling because it exhibited no missing five-minute intervals.

This reduced the need for imputation and the associated risk of introducing interpolation bias.

---

## 3. Analytical Process

### Phase 1 - Market Microstructure Analysis

Bitcoin price movements and trading volumes were compared across exchanges.

The analysis investigated:

- Cross-exchange price consistency
- Short-lived price deviations
- Trading activity and liquidity
- Extreme one-minute returns
- Potential market microstructure anomalies

**Finding:** Prices across exchanges generally moved together, although temporary differences were observed.

Exchange 4 recorded the highest total trading volume during the sample period.

### Phase 2 - Five-Minute VWAP Construction

High-frequency transactions were aggregated into five-minute intervals.

Volume-Weighted Average Price (VWAP) was calculated as:

VWAP = Sum(Price x Volume) / Sum(Volume)

The resulting five-minute price series was used to calculate logarithmic returns.

This produced 8,928 five-minute price observations for the selected exchange before return differencing.

### Phase 3 - Realised Variance Estimation

Hourly realised variance was estimated by aggregating squared five-minute logarithmic returns.

RV_hourly = Sum(Five-Minute Log Returns Squared)

The analysis generated:

- 744 hourly realised variance observations
- 31 daily realised volatility observations

Daily realised volatility was obtained by taking the square root of aggregated daily realised variance.

**Finding:** The highest reported daily realised volatility was approximately 6.99% on 7 December 2018.

### Phase 4 - Garman-Klass Volatility Estimation

An alternative volatility estimator was constructed using hourly Open, High, Low and Close (OHLC) prices.

The Garman-Klass estimator incorporates the intraperiod high-low range alongside open-close price movements.

The objective was to evaluate whether range-based volatility information provided useful signals for short-horizon forecasting.

---

## 4. Volatility Forecasting Models

3 regression specifications were assessed for next-hour realised variance.

### Model A - Lagged Realised Variance

The first model used current hourly realised variance to forecast the following hour.

**Results:**
- Regression coefficient: approximately 0.121
- Out-of-sample R²: approximately -0.010

The positive coefficient suggested some volatility persistence.

However, the negative out-of-sample R² indicated that the model did not outperform a basic test-set mean benchmark.

### Model B - Garman-Klass Volatility

The second model used the Garman-Klass variance estimator as the forecasting predictor.

**Results:**
- Regression coefficient: approximately 0.306
- Out-of-sample R²: approximately -0.008

The Garman-Klass model produced marginally better predictive performance than lagged realised variance.

Nevertheless, both models exhibited weak out-of-sample forecasting ability.

### Model C - Realised Variance and Trading Volume

A multivariate regression was developed using realised variance and trading volume.

**Results:**
- Trading volume p-value: approximately 0.024
- In-sample R²: approximately 2%
- Out-of-sample R²: approximately -0.0015

Trading volume was statistically significant at the 5% level in the reported regression.

However, its inclusion did not generate strong out-of-sample predictive performance.

### Forecasting Comparison

| Model | Out-of-Sample R² | Interpretation |
|---|---:|---|
| Lagged Realised Variance | -0.010 | Weak predictive power |
| Garman-Klass Variance | -0.008 | Marginal improvement |
| RV + Trading Volume | -0.0015 | Best reported hourly model, but still weak |

**Key Insight:** Adding market information improved forecasting performance slightly, but none of the models achieved positive out-of-sample R².

---

## 5. Results & Business Insights

### Finding 1 - Bitcoin Volatility Exhibited Clustering

Hourly realised variance displayed pronounced volatility spikes during early and late December 2018.

**Implication:** Cryptocurrency risk can change rapidly, making continuous risk monitoring important.

### Finding 2 - Data Completeness Influenced Model Selection

Exchange 3 exhibited no missing five-minute intervals.

**Implication:** High-quality market data is important for avoiding unnecessary interpolation and maintaining consistent volatility estimates.

### Finding 3 - Trading Activity Contained Incremental Information

Lagged trading volume was statistically significant in the multivariate regression.

However, overall forecasting performance remained weak.

**Implication:** Statistical significance does not necessarily translate into useful predictive accuracy.

### Finding 4 - Volatility Did Not Reliably Predict Bitcoin Price Levels

A separate regression examined whether lagged daily realised volatility predicted daily closing prices.

Reported results:

- In-sample R²: approximately 0.069
- Coefficient p-value: approximately 0.161
- Out-of-sample R²: approximately -1.75

The findings did not provide convincing evidence that lagged realised volatility predicted future Bitcoin price levels.

**Implication:** Volatility measures capture price variability rather than necessarily predicting market direction.

---

## 6. Solution & Recommendations

The project developed a framework for examining Bitcoin market behaviour using high-frequency data.

The methodology combined:

- Trade-level data cleaning and validation
- Exchange-level liquidity analysis
- Five-minute VWAP construction
- Realised variance estimation
- Garman-Klass volatility measurement
- Statistical forecasting
- Out-of-sample model evaluation

### Key Recommendations

1. Prioritise clean and complete high-frequency datasets before modelling.
2. Compare multiple volatility estimators rather than relying on a single measure.
3. Evaluate forecasting methods using chronological out-of-sample testing.
4. Distinguish statistical significance from practical predictive performance.
5. Consider more advanced volatility models, longer training samples and richer predictors in future research.

### Conclusion

The project demonstrated that high-frequency Bitcoin trading data can be used to construct detailed measures of realised market volatility.

However, simple regression models provided limited out-of-sample forecasting accuracy.

This highlights the distinction between **measuring financial risk** and **successfully forecasting future risk**.

---

## 7. Technical Skills Demonstrated

**Programming & Data Engineering**
- Python
- Pandas
- NumPy
- Time-Series Data Processing
- Data Cleaning and Validation
- Resampling and Aggregation
- Feature Engineering

**Financial Data Science**
- High-Frequency Financial Data
- Cryptocurrency Market Analysis
- Volume-Weighted Average Price
- Realised Variance
- Realised Volatility
- Garman-Klass Estimation
- Market Microstructure Analysis

**Statistical Modelling**
- Linear Regression
- Multivariate Regression
- Ordinary Least Squares
- Time-Based Train-Test Splitting
- Out-of-Sample Forecast Evaluation
- Mean Squared Error
- R-Squared
- Statistical Significance Testing

**Data Visualisation**
- Matplotlib
- Seaborn
- Financial Time-Series Visualisation
- Cross-Exchange Comparisons

---

## 8. Project Information

**Author:** Kiara Shree

**University:** University College Dublin

**School:** Michael Smurfit Graduate Business School

**Programme:** MSc Financial Data Science

**Module:** FIN42110 - Data Science for Trading & Risk Management

**Project Type:** Individual Academic Assignment

---

## 9. Repository Structure

```text
bitcoin-high-frequency-volatility-forecasting/
|
|-- README.md
|-- requirements.txt
|
|-- notebooks/
|   |-- DATA_SCIENEC_HOMEWORK1.ipynb
|
|-- data/
|   |-- README.md
|
|-- reports/
|   |-- DATA SCIENCE HOMEWORK.pdf
```

The original high-frequency dataset is not directly stored in the repository because it exceeds GitHub's standard file-size limit. Dataset access and reproducibility instructions will be documented separately.

---

## 10. Limitations & Future Improvements

The analysis was based on one month of Bitcoin transactions during December 2018.

The short sample period and simple linear forecasting specifications limit the generalisability of the forecasting conclusions.

Possible future extensions include:

- HAR-RV volatility models
- GARCH-family models
- Regularised regression
- Machine-learning forecasting methods
- Additional market microstructure features
- Longer historical evaluation periods
- Walk-forward validation

These are proposed improvements and were not implemented in the original analysis.

---

## 11. Disclaimer

This repository documents academic research completed as part of the MSc Financial Data Science programme at University College Dublin.

It is intended for educational and professional portfolio purposes and does not constitute investment advice.
