# Analysis Module

The Analysis Module is the core of the Pairs Trading Dashboard, implementing all statistical methods and algorithms needed to identify and evaluate pairs trading opportunities.

## Purpose

This module provides comprehensive statistical analysis of asset pairs to:
1. Identify mean-reverting relationships
2. Calculate optimal hedge ratios
3. Generate trading signals
4. Evaluate statistical significance of relationships
5. Measure mean reversion characteristics

## Structure

The analysis module is organized into specialized submodules:

```
analysis/
├── __init__.py
├── pair_relationship/          # Pair relationship analysis
├── stationarity/               # Stationarity and cointegration tests
├── mean_reversion/             # Mean reversion metrics
├── signals/                    # Trading signal generation
└── utils/                      # Analysis-specific utilities
```

## Components

### 1. Pair Relationship Analysis (`pair_relationship/`)

Analyzes the statistical relationship between two assets.

#### Price Ratio Analysis (`price_ratio.py`)
- `calculate_ratio(asset1, asset2)`: Computes price ratio between assets
- `rolling_ratio_stats(ratio, window)`: Calculates rolling mean and standard deviation
- `ratio_zscore(ratio, window)`: Computes z-score of the ratio

#### Regression Analysis (`regression.py`)
- `calculate_hedge_ratio(asset1, asset2)`: Performs OLS regression to find optimal hedge ratio
- `rolling_hedge_ratio(asset1, asset2, window)`: Calculates hedge ratio over rolling window
- `regression_metrics(asset1, asset2)`: Computes R², p-values, and other regression statistics

#### Correlation Analysis (`correlation.py`)
- `rolling_correlation(asset1, asset2, window)`: Calculates rolling correlation of returns
- `correlation_stability(correlations)`: Measures stability of correlation over time
- `detect_structural_breaks(correlations)`: Identifies significant changes in correlation

#### Spread Analysis (`spread.py`)
- `calculate_spread(asset1, asset2, hedge_ratio)`: Computes spread between hedged assets
- `spread_statistics(spread)`: Calculates mean, standard deviation, skewness, kurtosis
- `normalize_spread(spread)`: Normalizes spread for comparison

### 2. Stationarity and Cointegration Tests (`stationarity/`)

Implements statistical tests to validate pairs trading assumptions.

#### ADF Test (`adf_test.py`)
- `adf_test(series)`: Performs Augmented Dickey-Fuller test
- `interpret_adf_results(adf_result)`: Provides interpretation of test results
- `rolling_adf_test(series, window)`: Computes ADF test over rolling window

#### Cointegration Analysis (`cointegration.py`)
- `johansen_test(asset1, asset2)`: Performs Johansen cointegration test
- `engle_granger_test(asset1, asset2)`: Implements Engle-Granger two-step method
- `cointegration_summary(asset1, asset2)`: Provides comprehensive cointegration analysis

#### Hurst Exponent (`hurst.py`)
- `calculate_hurst(series)`: Computes Hurst exponent
- `interpret_hurst(hurst_value)`: Interprets Hurst exponent value
- `rolling_hurst(series, window)`: Calculates Hurst exponent over rolling window

### 3. Mean Reversion Metrics (`mean_reversion/`)

Quantifies mean-reversion characteristics of the pair.

#### Half-Life Calculation (`half_life.py`)
- `calculate_half_life(spread)`: Estimates half-life via AR(1) model
- `interpret_half_life(half_life)`: Provides trade timing guidance based on half-life
- `rolling_half_life(spread, window)`: Computes half-life over rolling window

#### Z-Score Analysis (`z_score.py`)
- `calculate_zscore(series, window)`: Computes z-score using rolling mean and std
- `zscore_crossovers(zscores, threshold)`: Identifies threshold crossovers
- `zscore_statistics(zscores)`: Analyzes z-score distribution and behavior

#### Volatility Analysis (`volatility.py`)
- `calculate_volatility(spread, window)`: Computes rolling volatility
- `volatility_adjusted_zscore(spread, window)`: Calculates volatility-adjusted z-scores
- `detect_volatility_regimes(spread)`: Identifies changes in volatility regime

### 4. Signal Generation (`signals/`)

Generates trading signals and evaluates performance.

#### Entry/Exit Signals (`entry_exit.py`)
- `generate_entry_signals(zscores, threshold)`: Identifies entry points based on z-score
- `generate_exit_signals(zscores, threshold)`: Identifies exit points based on z-score
- `filter_signals(signals, min_holding_period)`: Filters signals based on criteria

#### Backtesting (`backtest.py`)
- `backtest_strategy(asset1, asset2, signals, hedge_ratio)`: Simulates trading strategy
- `calculate_position_sizes(signals, capital)`: Determines position sizes for trades
- `simulate_execution(signals, slippage)`: Simulates trade execution with slippage

#### Performance Metrics (`performance.py`)
- `calculate_returns(trades)`: Computes returns for each trade
- `calculate_sharpe_ratio(returns)`: Calculates Sharpe ratio
- `calculate_drawdown(returns)`: Computes maximum drawdown
- `generate_performance_summary(trades)`: Creates comprehensive performance report

### 5. Analysis Utilities (`utils/`)

Provides helper functions for statistical analysis.

#### Statistical Utilities (`statistics.py`)
- `calculate_autocorrelation(series, lags)`: Computes autocorrelation function
- `calculate_partial_autocorrelation(series, lags)`: Computes partial autocorrelation
- `jarque_bera_test(series)`: Tests for normality

#### Data Transformations (`transformations.py`)
- `log_transform(series)`: Applies logarithmic transformation
- `difference_series(series)`: Computes first differences
- `standardize_series(series)`: Standardizes series to zero mean and unit variance

## Integration with Other Modules

### Data Module Integration
- Receives clean, processed data from the data module
- Returns analysis results that can be cached for future use

### Visualization Module Integration
- Provides data structures suitable for visualization
- Includes metadata for proper chart labeling and interpretation

### Dashboard Module Integration
- Exposes key functions to be called from dashboard callbacks
- Provides real-time analysis as user inputs change

## Usage Example

```python
from analysis.pair_relationship.regression import calculate_hedge_ratio
from analysis.stationarity.adf_test import adf_test
from analysis.mean_reversion.half_life import calculate_half_life
from analysis.signals.entry_exit import generate_entry_signals

# Calculate hedge ratio
hedge_ratio = calculate_hedge_ratio(asset1_data, asset2_data)

# Calculate spread
spread = asset1_data - hedge_ratio * asset2_data

# Test for stationarity
adf_result = adf_test(spread)

# Calculate mean reversion half-life
half_life = calculate_half_life(spread)

# Generate trading signals
signals = generate_entry_signals(spread, threshold=2.0)
```

## Statistical Methodology

The analysis module implements rigorous statistical methods based on established academic research in pairs trading, including:

1. **Cointegration-based approach**: Using cointegration tests to identify pairs with long-term equilibrium relationships
2. **Distance-based approach**: Using distance metrics to identify pairs with similar price movements
3. **Mean-reversion metrics**: Quantifying the speed and reliability of mean reversion
4. **Statistical arbitrage**: Identifying mispricing based on statistical deviations

## Future Enhancements

- Implementation of machine learning models for pair selection
- Addition of more advanced statistical tests
- Support for multivariate analysis (more than two assets)
- Integration of risk management metrics
- Optimization of trading parameters