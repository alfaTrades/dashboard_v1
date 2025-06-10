# Pairs Trading Dashboard: User Guide

This guide provides instructions on how to use the Pairs Trading Dashboard effectively for analyzing pairs trading opportunities.

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Dashboard Sections](#dashboard-sections)
4. [Analyzing Pairs](#analyzing-pairs)
5. [Interpreting Results](#interpreting-results)
6. [Trading Signals](#trading-signals)
7. [Exporting Data](#exporting-data)
8. [Troubleshooting](#troubleshooting)
9. [Glossary](#glossary)

## Introduction

The Pairs Trading Dashboard is a tool for analyzing mean-reverting relationships between two assets. It provides statistical analysis, visualization, and trading signal generation to support pairs trading strategies.

### What is Pairs Trading?

Pairs trading is a market-neutral trading strategy that matches a long position in one asset with a short position in another related asset. The strategy is based on the assumption that two historically correlated assets will revert to their mean relationship after periods of divergence.

### Key Concepts

- **Mean Reversion**: The tendency for a price series to return to its long-term average
- **Cointegration**: A statistical property where two time series share a long-term equilibrium relationship
- **Hedge Ratio**: The ratio used to determine the relative position sizes in the two assets
- **Z-score**: A measure of how many standard deviations a value is from the mean

## Getting Started

### System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Internet connection for data retrieval
- Minimum screen resolution of 1280x720 for optimal viewing

### Launching the Dashboard

1. Open a terminal or command prompt
2. Navigate to the dashboard directory
3. Run the command: `python app.py`
4. Open your browser and go to: `http://localhost:8050`

### Initial Setup

When you first launch the dashboard, you'll need to:

1. Enter two asset tickers (e.g., GLD for Gold ETF, SLV for Silver ETF)
2. Select a date range for analysis
3. Click "Analyze" to begin the analysis

## Dashboard Sections

The dashboard is organized into several sections, each providing different insights into the pair relationship.

### 1. User Input Panel

Located at the top of the dashboard, this panel allows you to:

- Enter asset tickers
- Select date range
- Adjust analysis parameters
- Trigger analysis

### 2. Raw Price Series

This section displays:

- Price charts for both assets
- Option to toggle log scale
- Basic price statistics

### 3. Price Ratio Analysis

This section shows:

- Ratio of Asset 1 to Asset 2 over time
- Rolling mean of the ratio
- Standard deviation bands
- Current ratio and z-score

### 4. OLS Regression & Hedge Ratio

This section provides:

- Scatter plot of Asset 1 vs Asset 2
- Regression line
- Hedge ratio (beta coefficient)
- R² value
- Option for rolling regression

### 5. Spread Analysis

This section displays:

- Spread between assets (Asset 1 - β × Asset 2)
- Mean and standard deviation bands
- Entry/exit signal highlights

### 6. Z-score of Spread

This section shows:

- Z-score of the spread over time
- Threshold lines (typically ±1, ±2)
- Trade signal annotations

### 7. Rolling Correlation

This section displays:

- Correlation between asset returns over time
- Helps identify structural breaks in the relationship

### 8. Statistical Tests

This section provides:

- ADF test results for stationarity
- Cointegration test results
- Interpretation of statistical significance

### 9. Mean Reversion Metrics

This section shows:

- Half-life of mean reversion
- Hurst exponent
- Interpretation for trading

### 10. Trade Signal Summary

This section displays:

- Table of historical trading signals
- Entry and exit points
- Performance metrics (if backtesting is enabled)

### 11. Export Options

This section allows you to:

- Export data to CSV
- Export charts as PNG/HTML
- Save/load analysis sessions

## Analyzing Pairs

### Selecting Asset Pairs

Good candidate pairs typically have:

1. Economic relationship (e.g., Gold and Silver)
2. Same industry or sector (e.g., Coca-Cola and Pepsi)
3. Historical correlation
4. Similar market capitalization

### Setting Parameters

Key parameters to adjust:

1. **Rolling Window Length**:
   - Default: 30 days
   - Shorter windows: More responsive but noisier
   - Longer windows: Smoother but less responsive

2. **Z-score Thresholds**:
   - Default: ±2
   - Lower thresholds: More frequent signals but potentially lower quality
   - Higher thresholds: Fewer signals but potentially higher quality

3. **Date Range**:
   - Training period: Historical data to establish relationship
   - Testing period: Recent data to validate signals

### Analysis Workflow

1. Start with a pair that has a known relationship
2. Analyze the price ratio and check for mean-reverting behavior
3. Check statistical tests for cointegration and stationarity
4. Examine the half-life to understand mean reversion speed
5. Review historical signals and their performance
6. Adjust parameters to optimize the strategy

## Interpreting Results

### Price Ratio Analysis

- **Mean-reverting pattern**: Indicates potential for pairs trading
- **Trending pattern**: May not be suitable for pairs trading
- **Structural breaks**: Periods where the relationship changes significantly

### Regression Analysis

- **High R²**: Strong linear relationship between assets
- **Stable hedge ratio**: Consistent relationship over time
- **Changing hedge ratio**: May require adaptive position sizing

### Spread Analysis

- **Mean-reverting spread**: Good candidate for pairs trading
- **Trending spread**: Poor candidate for pairs trading
- **Changing volatility**: May require volatility-adjusted signals

### Statistical Tests

#### ADF Test
- **p-value < 0.05**: Spread is likely stationary (good for pairs trading)
- **p-value > 0.05**: Spread may not be stationary (caution advised)

#### Cointegration Test
- **p-value < 0.05**: Assets are likely cointegrated (good for pairs trading)
- **p-value > 0.05**: Assets may not be cointegrated (caution advised)

### Mean Reversion Metrics

#### Half-Life
- **Short half-life (1-5 days)**: Fast mean reversion, shorter holding periods
- **Medium half-life (5-20 days)**: Moderate mean reversion, medium holding periods
- **Long half-life (>20 days)**: Slow mean reversion, longer holding periods

#### Hurst Exponent
- **H < 0.5**: Mean-reverting series (good for pairs trading)
- **H = 0.5**: Random walk
- **H > 0.5**: Trending series (poor for pairs trading)

## Trading Signals

### Signal Generation

The dashboard generates trading signals based on z-score thresholds:

1. **Entry Signals**:
   - **Long the spread**: When z-score < lower threshold (e.g., -2)
   - **Short the spread**: When z-score > upper threshold (e.g., +2)

2. **Exit Signals**:
   - **Exit long spread**: When z-score crosses zero or reaches upper threshold
   - **Exit short spread**: When z-score crosses zero or reaches lower threshold

### Implementing Trades

To implement a pairs trade based on signals:

1. **Long the spread** (z-score < -2):
   - Buy Asset 1
   - Sell Asset 2 × hedge ratio

2. **Short the spread** (z-score > +2):
   - Sell Asset 1
   - Buy Asset 2 × hedge ratio

3. **Position Sizing**:
   - Use the hedge ratio to determine relative position sizes
   - Consider total capital and risk management rules

### Signal Quality Assessment

Factors affecting signal quality:

- **Statistical significance**: Stronger statistical evidence suggests better signals
- **Historical performance**: Consistent historical performance suggests reliability
- **Current market conditions**: Changes in market regime may affect performance
- **Half-life**: Should match your intended holding period

## Exporting Data

### CSV Export

Export data for further analysis:

1. Navigate to the Export section
2. Select data to export (price data, analysis results, signals)
3. Click "Export to CSV"
4. Choose save location

### Chart Export

Export charts for presentations or records:

1. Navigate to the Export section
2. Select charts to export
3. Choose format (PNG, HTML)
4. Click "Export Charts"
5. Choose save location

### Saving Sessions

Save your analysis for future reference:

1. Navigate to the Export section
2. Click "Save Session"
3. Enter session name
4. Click "Save"

To reload a saved session:

1. Navigate to the Export section
2. Click "Load Session"
3. Select saved session
4. Click "Load"

## Troubleshooting

### Common Issues

#### Data Retrieval Issues
- **Problem**: Unable to fetch data for tickers
- **Solution**: Verify ticker symbols, check internet connection, or try alternative data source

#### Analysis Errors
- **Problem**: Statistical tests fail to run
- **Solution**: Ensure sufficient data points, check for missing values, or adjust date range

#### Visualization Issues
- **Problem**: Charts not displaying correctly
- **Solution**: Try refreshing the page, clearing browser cache, or using a different browser

### Error Messages

- **"Invalid ticker symbol"**: Verify the ticker exists and is correctly spelled
- **"Insufficient data points"**: Select a longer date range
- **"API rate limit exceeded"**: Wait and try again later
- **"No cointegration detected"**: The assets may not be suitable for pairs trading

## Glossary

- **ADF Test**: Augmented Dickey-Fuller test, used to test for stationarity
- **Cointegration**: A statistical property where two time series share a long-term equilibrium relationship
- **Half-Life**: The time taken for a deviation to decay by half, measured in days
- **Hedge Ratio**: The ratio of positions between two assets, typically derived from regression
- **Hurst Exponent**: A measure of the long-term memory of a time series
- **Mean Reversion**: The tendency for a price series to return to its long-term average
- **OLS Regression**: Ordinary Least Squares regression, used to find the relationship between assets
- **Pairs Trading**: A market-neutral strategy that matches a long position in one asset with a short position in another
- **Spread**: The difference between two assets, typically calculated as Asset1 - (β × Asset2)
- **Stationarity**: A property where statistical properties do not change over time
- **Z-score**: A measure of how many standard deviations a value is from the mean