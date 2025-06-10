# Utils Module

The Utils Module provides common utility functions and helpers that are used across the Pairs Trading Dashboard application.

## Purpose

This module serves as a collection of reusable functions that:
1. Simplify common operations
2. Ensure consistency across the application
3. Reduce code duplication
4. Handle cross-cutting concerns

## Components

### 1. Helper Functions (`helpers.py`)

General-purpose utility functions used throughout the application.

**Key Functions:**
- `format_number(number, precision=2)`: Formats numbers with consistent precision
- `calculate_date_range(start_date, end_date)`: Calculates number of trading days
- `generate_unique_id(prefix='')`: Generates unique identifiers for components
- `timer(func)`: Decorator for timing function execution
- `memoize(func)`: Decorator for caching function results
- `parallel_process(func, items)`: Executes function in parallel for multiple items

**Dependencies:**
- Standard Python libraries (datetime, uuid, functools)
- Optional: joblib for parallelization

### 2. Validators (`validators.py`)

Functions for validating user inputs and data.

**Key Functions:**
- `validate_ticker(ticker)`: Validates stock ticker symbols
- `validate_date_range(start_date, end_date)`: Validates date range inputs
- `validate_numeric_input(value, min_value, max_value)`: Validates numeric parameters
- `validate_window_size(window, data_length)`: Validates rolling window size
- `check_data_sufficiency(data, min_points)`: Checks if enough data points are available

**Dependencies:**
- Standard Python libraries (re, datetime)
- pandas for data validation

### 3. Configuration Helpers (`config_helpers.py`)

Functions for managing application configuration.

**Key Functions:**
- `load_config(config_file)`: Loads configuration from file
- `get_config_value(key, default=None)`: Retrieves configuration value
- `update_config(key, value)`: Updates configuration setting
- `save_config(config, config_file)`: Saves configuration to file
- `get_api_credentials(api_name)`: Retrieves API credentials securely

**Dependencies:**
- Standard Python libraries (json, configparser)
- Optional: keyring for secure credential storage

### 4. Error Handling (`error_handlers.py`)

Functions for consistent error handling across the application.

**Key Functions:**
- `handle_api_error(error)`: Handles API-related errors
- `handle_calculation_error(error)`: Handles errors in statistical calculations
- `log_error(error, context)`: Logs errors with context information
- `user_friendly_error(error)`: Converts technical errors to user-friendly messages
- `is_recoverable_error(error)`: Determines if an error is recoverable

**Dependencies:**
- Standard Python libraries (logging, traceback)

### 5. Data Utilities (`data_utils.py`)

Helper functions for common data operations.

**Key Functions:**
- `resample_data(data, frequency)`: Resamples time series data
- `align_time_series(series1, series2)`: Aligns two time series by date
- `detect_outliers(series, method='zscore')`: Identifies outliers in data
- `fill_missing_values(series, method='ffill')`: Fills missing values
- `calculate_returns(prices, method='simple')`: Calculates returns from prices

**Dependencies:**
- pandas for data manipulation
- numpy for numerical operations

## Usage Examples

### Helper Functions Example

```python
from utils.helpers import format_number, timer

@timer
def perform_calculation(data):
    # Complex calculation here
    result = data.sum()
    return format_number(result, precision=4)

# Usage
result = perform_calculation(data)
# Output: "Result: 123.4567 (Calculation took 0.25 seconds)"
```

### Validators Example

```python
from utils.validators import validate_ticker, validate_date_range

def process_user_input(ticker, start_date, end_date):
    # Validate inputs
    if not validate_ticker(ticker):
        return "Invalid ticker symbol"
    
    if not validate_date_range(start_date, end_date):
        return "Invalid date range"
    
    # Process valid inputs
    return "Processing data for {ticker} from {start_date} to {end_date}"
```

### Error Handling Example

```python
from utils.error_handlers import handle_api_error, user_friendly_error

def fetch_data(ticker):
    try:
        # API call that might fail
        return api.get_data(ticker)
    except ApiError as e:
        handle_api_error(e)
        return user_friendly_error(e)
```

## Integration with Other Modules

The utils module is used by all other modules in the application:

- **Data Module**: Uses validators for input validation and error handlers for API errors
- **Analysis Module**: Uses helpers for performance optimization and data utilities for preprocessing
- **Visualization Module**: Uses formatting helpers for consistent number display
- **Dashboard Module**: Uses validators for user input validation and error handlers for user feedback

## Best Practices

The utils module follows these best practices:

1. **Single Responsibility**: Each function does one thing well
2. **Reusability**: Functions are designed to be reused across the application
3. **Testability**: Functions are pure and easy to test
4. **Documentation**: All functions have clear docstrings
5. **Error Handling**: Functions handle edge cases gracefully

## Future Enhancements

- Expanded logging capabilities
- Performance profiling utilities
- Memory usage optimization helpers
- Internationalization support
- Enhanced security utilities