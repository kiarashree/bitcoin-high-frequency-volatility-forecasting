
# Results & Insights

## 1. Executive Summary

This project investigated Bitcoin volatility using more than 5 million high-frequency trade observations across four cryptocurrency exchanges.

The analysis constructed five-minute Volume-Weighted Average Prices (VWAP), hourly realised variance and daily realised volatility, and evaluated regression-based forecasting methods.

**Central finding:** High-frequency data provided detailed measurements of Bitcoin volatility, but the tested regression models showed limited out-of-sample forecasting accuracy.

---

## 2. Data Engineering & Processing

| Metric | Result |
|---|---|
| Raw transaction observations | Over 5.2 million |
| Exchanges analysed | 4 |
| Observation period | 1-31 December 2018 |
| Five-minute price observations, selected exchange | 8,928 |
| Hourly realised variance observations | 744 |
| Daily realised volatility observations | 31 |
| Selected exchange | Exchange 3 |

### Data Quality Findings

| Exchange | Missing Five-Minute Intervals |
|---|---:|
| Exchange 1 | 21 |
| Exchange 2 | 1 |
| Exchange 3 | 0 |
| Exchange 4 | 4 |

**Finding:** Exchange 3 provided the most complete five-minute series and was selected for detailed volatility modelling.

---

## 3. Volatility Estimation

We squared five-minute logarithmic returns and aggregated them to estimate hourly realised variance.

Daily realised volatility was calculated from aggregated daily realised variance.

### Key Result

**Peak daily realised volatility: 6.99% on 7 December 2018.**

Hourly realised variance displayed volatility clustering and significant changes in intraday market conditions.

### Financial Interpretation

Volatility was not constant over time. This highlights the value of high-frequency market monitoring when assessing changing risk exposures.

---

## 4. Forecasting Model Comparison

3 hourly forecasting specifications were evaluated using chronological train-test splitting.

| Model | Out-of-Sample R² | Main Finding |
|---|---:|---|
| Lagged Realised Variance | -0.010 | Weak predictive accuracy |
| Lagged Garman-Klass Variance | -0.008 | Marginal improvement |
| Realised Variance + Trading Volume | -0.0015 | Best reported hourly specification, but still weak |

### Model A - Lagged Realised Variance

The model produced a positive regression coefficient of approximately 0.121, consistent with some volatility persistence.

However, the negative out-of-sample R² indicated poor predictive performance.

### Model B - Garman-Klass Variance

The range-based estimator achieved marginally better out-of-sample performance than the realised variance benchmark.

Nevertheless, its predictive accuracy remained limited.

### Model C - Realised Variance and Volume

Lagged trading volume was statistically significant in the reported multivariate regression:

- Volume p-value: 0.024
- In-sample R²: approximately 2%
- Out-of-sample R²: approximately -0.0015

**Interpretation:** Trading activity contained statistically significant information, but the model did not achieve strong out-of-sample predictive accuracy.

---

## 5. Daily Price-Level Regression

A separate regression investigated whether lagged daily realised volatility predicted Bitcoin closing prices.

| Metric | Result |
|---|---:|
| In-sample R² | Approximately 0.07 |
| Lagged volatility p-value | 0.161 |
| Out-of-sample R² | -1.75 |

The results did not provide convincing evidence that lagged realised volatility predicted future Bitcoin price levels.

---

## 6. Business & Risk Management Implications

### Risk Monitoring

High-frequency realised variance can reveal changes in market volatility that are less visible in lower-frequency summaries.

### Exchange Data Quality

Missing observations and inconsistent transaction records can affect volatility estimation. Exchange selection and data validation are therefore important.

### Forecast Model Validation

A statistically significant predictor does not necessarily produce a useful forecasting model.

Chronological out-of-sample evaluation is essential for assessing predictive performance.

### Model Development

The results motivate further investigation of richer volatility forecasting specifications, including HAR-RV, GARCH-family and machine-learning approaches.

These methods are proposed extensions rather than models implemented in the original project.

---

## 7. Limitations

- The sample covers only December 2018.
- Results may not generalise to other cryptocurrency market conditions.
- The forecasting specifications were relatively simple.
- Some model results were statistically informative but had weak out-of-sample performance.
- Realised volatility and Garman-Klass variance are different volatility estimators and are sensitive to their construction methods.

---

## 8. Conclusion

The project demonstrated a complete analytical workflow from high-frequency transaction data to volatility estimation and statistical forecasting.

The central outcome was a distinction between **accurately measuring observed market variability** and **successfully predicting future volatility**.

The findings support the importance of data quality, multiple volatility measures and rigorous out-of-sample model evaluation.

---

*Results are drawn from the original academic project report and have not yet been independently reproduced in a fresh execution environment.*
