# Pairs Trading Dashboard: Developer Guide

This guide provides information for developers who want to understand, modify, or extend the Pairs Trading Dashboard.

## Table of Contents

1. [Development Environment Setup](#development-environment-setup)
2. [Project Structure](#project-structure)
3. [Module Overview](#module-overview)
4. [Development Workflow](#development-workflow)
5. [Adding New Features](#adding-new-features)
6. [Testing](#testing)
7. [Performance Optimization](#performance-optimization)
8. [Contribution Guidelines](#contribution-guidelines)
9. [API Reference](#api-reference)

## Development Environment Setup

### Prerequisites

- Python 3.8 or higher
- Git
- pip (Python package installer)
- A code editor (VS Code, PyCharm, etc.)

### Setting Up the Development Environment

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/dashboard_v1.git
   cd dashboard_v1
   ```

2. **Create a virtual environment**:
   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment**:
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

4. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

5. **Install development dependencies**:
   ```bash
   pip install -r requirements-dev.txt
   ```

### Running the Application in Development Mode

```bash
python app.py
```

This will start the Dash development server, which includes:
- Hot reloading (changes are automatically reflected)
- Detailed error messages
- Debug information

Access the application at `http://localhost:8050` in your browser.

## Project Structure

The project follows a modular structure with clear separation of concerns:

```
dashboard_v1/
├── app.py                      # Main application entry point
├── config.py                   # Configuration settings
├── requirements.txt            # Project dependencies
├── requirements-dev.txt        # Development dependencies
├── data/                       # Data management
│   ├── __init__.py
│   ├── fetcher.py              # API data fetching
│   ├── processor.py            # Data preprocessing
│   ├── storage.py              # Data caching/storage
│   └── README.md               # Data module documentation
├── analysis/                   # Statistical analysis
│   ├── __init__.py
│   ├── pair_relationship/      # Pair relationship analysis
│   ├── stationarity/           # Stationarity and cointegration tests
│   ├── mean_reversion/         # Mean reversion metrics
│   ├── signals/                # Trading signal generation
│   ├── utils/                  # Analysis-specific utilities
│   └── README.md               # Analysis module documentation
├── visualization/              # Data visualization
│   ├── __init__.py
│   ├── charts.py               # Chart components
│   ├── layouts.py              # Dashboard layouts
│   ├── themes.py               # Visual styling
│   └── README.md               # Visualization module documentation
├── dashboard/                  # Dashboard components
│   ├── __init__.py
│   ├── components/             # Reusable UI components
│   ├── callbacks.py            # Dash callbacks
│   ├── layouts.py              # Page layouts
│   └── README.md               # Dashboard module documentation
├── utils/                      # Utility functions
│   ├── __init__.py
│   ├── helpers.py              # Helper functions
│   ├── validators.py           # Input validation
│   └── README.md               # Utilities documentation
├── tests/                      # Unit and integration tests
│   ├── __init__.py
│   ├── test_data.py
│   ├── test_analysis.py
│   └── test_visualization.py
└── docs/                       # Additional documentation
    ├── architecture.md         # Detailed architecture explanation
    ├── user_guide.md           # User documentation
    ├── developer_guide.md      # Developer documentation
    └── alternative_implementations.md  # Alternative tech stacks
```

## Module Overview

### Data Module

The Data Module handles all data-related operations:

- **fetcher.py**: Retrieves data from external APIs
- **processor.py**: Cleans and prepares data for analysis
- **storage.py**: Manages data caching and persistence

Key interfaces:
```python
# Fetch data for a single asset
data = fetcher.fetch_asset_data(ticker="GLD", start_date="2020-01-01", end_date="2021-01-01")

# Process raw data
processed_data = processor.clean_data(raw_data)

# Cache data for future use
storage.cache_data(key="GLD_2020", data=processed_data)
```

### Analysis Module

The Analysis Module implements statistical methods and algorithms:

- **pair_relationship/**: Analyzes relationships between assets
- **stationarity/**: Tests for mean-reverting properties
- **mean_reversion/**: Quantifies mean reversion characteristics
- **signals/**: Generates trading signals

Key interfaces:
```python
# Calculate hedge ratio
hedge_ratio = regression.calculate_hedge_ratio(asset1_data, asset2_data)

# Test for stationarity
adf_result = adf_test.test_stationarity(spread_data)

# Calculate half-life
half_life = half_life.calculate_half_life(spread_data)

# Generate trading signals
signals = entry_exit.generate_signals(zscore_data, threshold=2.0)
```

### Visualization Module

The Visualization Module creates interactive charts and plots:

- **charts.py**: Implements reusable chart components
- **layouts.py**: Manages chart arrangements
- **themes.py**: Provides consistent styling

Key interfaces:
```python
# Create a price chart
price_chart = charts.create_price_chart(asset1_data, asset2_data)

# Create a z-score chart with signals
zscore_chart = charts.create_zscore_chart(zscore_data, signals=signals)

# Apply a theme to a chart
styled_chart = themes.apply_theme(chart, theme="dark")
```

### Dashboard Module

The Dashboard Module builds the user interface:

- **components/**: Reusable UI elements
- **callbacks.py**: Handles user interactions
- **layouts.py**: Defines dashboard structure

Key interfaces:
```python
# Create input panel
input_panel = components.create_input_panel()

# Register callbacks
callbacks.register_input_callbacks(app)

# Create main layout
layout = layouts.create_main_layout()
```

### Utils Module

The Utils Module provides common utility functions:

- **helpers.py**: General utility functions
- **validators.py**: Input validation functions

Key interfaces:
```python
# Validate user input
is_valid = validators.validate_ticker("GLD")

# Format number for display
formatted = helpers.format_number(123.456789, precision=2)
```

## Development Workflow

### Feature Development Process

1. **Create a feature branch**:
   ```bash
   git checkout -b feature/new-feature-name
   ```

2. **Implement the feature**:
   - Add necessary files and code
   - Follow the project's coding standards
   - Add appropriate documentation

3. **Write tests**:
   - Add unit tests for new functionality
   - Ensure all tests pass

4. **Submit a pull request**:
   - Provide a clear description of the changes
   - Reference any related issues

### Code Style Guidelines

- Follow PEP 8 for Python code style
- Use meaningful variable and function names
- Add docstrings to all functions and classes
- Keep functions focused on a single responsibility
- Use type hints where appropriate

### Documentation Guidelines

- Update module README.md files when adding new functionality
- Add docstrings to all public functions and classes
- Include examples in docstrings
- Update user documentation if the feature affects the UI

## Adding New Features

### Adding a New Analysis Method

1. **Identify the appropriate submodule**:
   - Is it related to pair relationships, stationarity, mean reversion, or signals?

2. **Create a new file in the appropriate submodule**:
   - For example, to add a new stationarity test:
     ```python
     # analysis/stationarity/new_test.py
     def new_stationarity_test(data):
         """
         Implements a new stationarity test.
         
         Parameters:
         -----------
         data : pandas.Series
             The time series data to test
             
         Returns:
         --------
         dict
             Test results including test statistic and p-value
         """
         # Implementation here
         return results
     ```

3. **Add the function to the submodule's __init__.py**:
   ```python
   # analysis/stationarity/__init__.py
   from .adf_test import test_stationarity
   from .new_test import new_stationarity_test
   
   __all__ = ['test_stationarity', 'new_stationarity_test']
   ```

4. **Add tests**:
   ```python
   # tests/test_analysis.py
   def test_new_stationarity_test():
       # Test implementation
       pass
   ```

5. **Update documentation**:
   - Add the new function to the analysis module README.md
   - Update any relevant user documentation

### Adding a New Visualization

1. **Add the new chart function to charts.py**:
   ```python
   # visualization/charts.py
   def create_new_chart_type(data, options=None):
       """
       Creates a new type of chart.
       
       Parameters:
       -----------
       data : pandas.DataFrame
           The data to visualize
       options : dict, optional
           Chart configuration options
           
       Returns:
       --------
       plotly.graph_objects.Figure
           The chart figure
       """
       # Implementation here
       return fig
   ```

2. **Add tests**:
   ```python
   # tests/test_visualization.py
   def test_create_new_chart_type():
       # Test implementation
       pass
   ```

3. **Update documentation**:
   - Add the new chart type to the visualization module README.md
   - Update any relevant user documentation

### Adding a New Dashboard Component

1. **Create a new component file**:
   ```python
   # dashboard/components/new_component.py
   def create_new_component(options=None):
       """
       Creates a new dashboard component.
       
       Parameters:
       -----------
       options : dict, optional
           Component configuration options
           
       Returns:
       --------
       dash_html_components.Div
           The component
       """
       # Implementation here
       return component
   ```

2. **Add the component to the dashboard layout**:
   ```python
   # dashboard/layouts.py
   from dashboard.components.new_component import create_new_component
   
   def create_main_layout():
       # Existing code
       new_component = create_new_component()
       layout.children.append(new_component)
       return layout
   ```

3. **Add callbacks if needed**:
   ```python
   # dashboard/callbacks.py
   def register_new_component_callbacks(app):
       @app.callback(
           Output('new-component-output', 'children'),
           Input('new-component-input', 'value')
       )
       def update_new_component(value):
           # Callback implementation
           return processed_value
   ```

4. **Update documentation**:
   - Add the new component to the dashboard module README.md
   - Update any relevant user documentation

## Testing

### Running Tests

```bash
# Run all tests
pytest

# Run tests for a specific module
pytest tests/test_analysis.py

# Run a specific test
pytest tests/test_analysis.py::test_function_name

# Run tests with coverage
pytest --cov=.
```

### Writing Tests

1. **Unit Tests**:
   - Test individual functions and classes
   - Use pytest fixtures for test data
   - Mock external dependencies

   Example:
   ```python
   # tests/test_analysis.py
   import pytest
   import pandas as pd
   from analysis.pair_relationship.regression import calculate_hedge_ratio
   
   @pytest.fixture
   def sample_data():
       # Create sample data for testing
       asset1 = pd.Series([1, 2, 3, 4, 5])
       asset2 = pd.Series([2, 3, 4, 5, 6])
       return asset1, asset2
   
   def test_calculate_hedge_ratio(sample_data):
       asset1, asset2 = sample_data
       hedge_ratio = calculate_hedge_ratio(asset1, asset2)
       assert isinstance(hedge_ratio, float)
       assert 0.9 < hedge_ratio < 1.1  # Approximate expected value
   ```

2. **Integration Tests**:
   - Test interactions between modules
   - Verify data flow and transformations

   Example:
   ```python
   # tests/test_integration.py
   def test_data_to_analysis_flow():
       # Test that data flows correctly from data module to analysis module
       ticker = "GLD"
       start_date = "2020-01-01"
       end_date = "2021-01-01"
       
       # Fetch and process data
       raw_data = fetcher.fetch_asset_data(ticker, start_date, end_date)
       processed_data = processor.clean_data(raw_data)
       
       # Perform analysis
       result = some_analysis_function(processed_data)
       
       # Verify result
       assert result is not None
       # Additional assertions
   ```

3. **Dashboard Tests**:
   - Test Dash callbacks and component rendering
   - Use the Dash testing framework

   Example:
   ```python
   # tests/test_dashboard.py
   from dash.testing.application_runners import import_app
   
   def test_input_callback(dash_duo):
       app = import_app('app')
       dash_duo.start_server(app)
       
       # Interact with the dashboard
       dash_duo.find_element('#ticker-input').send_keys('GLD')
       dash_duo.find_element('#analyze-button').click()
       
       # Wait for callback to complete
       dash_duo.wait_for_element('#results-container')
       
       # Verify result
       assert dash_duo.find_element('#results-container').text != ''
   ```

## Performance Optimization

### Profiling

To identify performance bottlenecks:

```bash
# Install profiling tools
pip install snakeviz

# Profile a script
python -m cProfile -o profile_results.prof your_script.py

# Visualize results
snakeviz profile_results.prof
```

### Optimization Strategies

1. **Data Optimization**:
   - Use efficient data structures (NumPy arrays for numerical operations)
   - Implement caching for expensive operations
   - Use vectorized operations instead of loops

2. **Computation Optimization**:
   - Implement lazy evaluation for expensive calculations
   - Use parallel processing for independent operations
   - Optimize algorithms for time complexity

3. **Dashboard Optimization**:
   - Minimize callback overhead
   - Use efficient data transfer between callbacks
   - Implement pagination for large datasets

## Contribution Guidelines

### Pull Request Process

1. **Fork the repository**
2. **Create a feature branch**
3. **Make your changes**
4. **Run tests and ensure they pass**
5. **Submit a pull request**

### Code Review Criteria

Pull requests will be reviewed based on:
- Code quality and adherence to style guidelines
- Test coverage
- Documentation quality
- Performance impact
- Maintainability

### Versioning

The project follows Semantic Versioning (SemVer):
- MAJOR version for incompatible API changes
- MINOR version for backwards-compatible functionality
- PATCH version for backwards-compatible bug fixes

## API Reference

### Data Module API

```python
# fetcher.py
fetch_asset_data(ticker, start_date, end_date)
fetch_multiple_assets(tickers, start_date, end_date)

# processor.py
clean_data(df)
align_data(df1, df2)
calculate_returns(df)

# storage.py
cache_data(key, data)
get_cached_data(key)
save_data(data, filename)
load_data(filename)
```

### Analysis Module API

```python
# pair_relationship/regression.py
calculate_hedge_ratio(asset1, asset2)
rolling_hedge_ratio(asset1, asset2, window)

# stationarity/adf_test.py
test_stationarity(series)
interpret_adf_results(adf_result)

# mean_reversion/half_life.py
calculate_half_life(spread)
interpret_half_life(half_life)

# signals/entry_exit.py
generate_entry_signals(zscores, threshold)
generate_exit_signals(zscores, threshold)
```

### Visualization Module API

```python
# charts.py
create_price_chart(asset1_data, asset2_data)
create_ratio_chart(ratio_data, rolling_mean, std_bands)
create_regression_chart(asset1, asset2, regression_line)
create_spread_chart(spread, mean, bands, signals)
create_zscore_chart(zscore, thresholds, signals)

# themes.py
apply_theme(figure, theme='light')
create_color_palette(base_color, n_colors)
```

### Dashboard Module API

```python
# components/input_panel.py
create_ticker_input()
create_date_range_selector()
create_parameter_inputs()
create_input_panel()

# callbacks.py
register_input_callbacks(app)
register_chart_callbacks(app)
register_export_callbacks(app)

# layouts.py
create_main_layout()
create_header()
create_sidebar()
create_content_area()
```

### Utils Module API

```python
# helpers.py
format_number(number, precision=2)
calculate_date_range(start_date, end_date)
generate_unique_id(prefix='')

# validators.py
validate_ticker(ticker)
validate_date_range(start_date, end_date)
validate_numeric_input(value, min_value, max_value)
```

## Additional Resources

- [Dash Documentation](https://dash.plotly.com/)
- [Plotly Documentation](https://plotly.com/python/)
- [pandas Documentation](https://pandas.pydata.org/docs/)
- [statsmodels Documentation](https://www.statsmodels.org/stable/index.html)
- [pytest Documentation](https://docs.pytest.org/)