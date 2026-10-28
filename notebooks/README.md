
# Bitcoin Volatility Modelling - Python Notebook

## Overview

This directory contains the Jupyter Notebook developed for
the High-Frequency Bitcoin Volatility Estimation and
Forecasting project.

## Analytical Workflow

### 1. Data Engineering
- Load over 5 million Bitcoin trade observations
- Clean timestamps and validate transaction data
- Identify anomalies and extreme returns
- Analyse cross-exchange prices and trading volumes

### 2. Volatility Estimation
- Construct five-minute Volume-Weighted Average Prices
- Calculate logarithmic returns
- Estimate hourly realised variance
- Calculate daily realised volatility
- Construct Garman-Klass variance estimates

### 3. Statistical Forecasting
- Lagged realised variance regression
- Garman-Klass variance regression
- Multivariate regression incorporating trading volume
- Chronological train-test splitting
- Out-of-sample model evaluation

### 4. Results and Visualisation
- Bitcoin price evolution
- Exchange-level trading volume
- Hourly realised variance
- Daily realised volatility
- Realised variance versus Garman-Klass variance

## Execution

The notebook expects the original dataset
`BTC_2018-12.txt`.

The dataset contains more than 5 million trade observations
and is handled separately because of GitHub's standard
file-size restrictions.

Run the notebook sequentially after configuring the dataset
path and installing the required Python libraries.
