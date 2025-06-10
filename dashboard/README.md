# Dashboard Module

The Dashboard Module is responsible for creating the user interface of the Pairs Trading Dashboard, handling user interactions, and orchestrating the flow of data between the UI and the backend components.

## Purpose

This module serves as the presentation layer of the application, providing:
1. User input controls for selecting assets and parameters
2. Layout structure for organizing visualizations
3. Interactive elements for exploring data
4. Callbacks for handling user interactions
5. Session management for saving/loading analysis

## Components

### 1. UI Components (`components/`)

Reusable UI elements for building the dashboard interface.

#### Input Panel (`input_panel.py`)
- `create_ticker_input()`: Creates input fields for asset tickers
- `create_date_range_selector()`: Creates date range picker
- `create_parameter_inputs()`: Creates inputs for analysis parameters
- `create_input_panel()`: Combines all inputs into a cohesive panel

#### Chart Panel (`chart_panel.py`)
- `create_chart_container(title, chart)`: Creates container for charts with title and description
- `create_chart_grid(charts)`: Arranges multiple charts in a grid
- `create_chart_tabs(charts)`: Organizes charts in tabs
- `create_expandable_chart(chart, title)`: Creates expandable/collapsible chart section

#### Summary Panel (`summary_panel.py`)
- `create_metrics_table(metrics)`: Creates table of key metrics
- `create_signal_table(signals)`: Creates table of trading signals
- `create_performance_summary(performance)`: Creates performance summary
- `create_statistical_summary(stats)`: Creates summary of statistical tests

### 2. Callbacks (`callbacks.py`)

Handles user interactions and updates the dashboard in response.

**Key Functions:**
- `register_input_callbacks(app)`: Registers callbacks for input changes
- `register_chart_callbacks(app)`: Registers callbacks for chart interactions
- `register_export_callbacks(app)`: Registers callbacks for data export
- `update_analysis(input_values)`: Updates analysis based on user inputs
- `update_charts(analysis_results)`: Updates charts based on analysis results

**Dependencies:**
- Dash for callback registration
- Analysis module for performing calculations
- Visualization module for updating charts

### 3. Layouts (`layouts.py`)

Defines the overall structure and organization of the dashboard.

**Key Functions:**
- `create_main_layout()`: Creates the main dashboard layout
- `create_header()`: Creates dashboard header with title and controls
- `create_sidebar()`: Creates sidebar with inputs and controls
- `create_content_area()`: Creates main content area for charts
- `create_footer()`: Creates footer with additional information

**Dependencies:**
- Dash for layout components
- Dash Bootstrap Components for responsive layout

## Dashboard Sections

Based on the project outline, the dashboard is organized into the following sections:

### 1. User Input Panel
- Asset ticker inputs
- Date range selector
- Parameter inputs (rolling window, z-score thresholds)
- Analysis control buttons

### 2. Raw Price Series Section
- Dual-axis price chart
- Log-scale toggle
- Price statistics summary

### 3. Price Ratio Analysis Section
- Ratio chart with bands
- Current ratio and z-score display
- Ratio statistics summary

### 4. OLS Regression Section
- Scatter plot with regression line
- Hedge ratio and R² display
- Rolling regression option

### 5. Spread Analysis Section
- Spread chart with bands and signals
- Spread statistics display
- Signal highlight controls

### 6. Z-score Section
- Z-score chart with threshold lines
- Signal annotations
- Z-score statistics summary

### 7. Correlation Analysis Section
- Rolling correlation chart
- Correlation statistics
- Structural break indicators

### 8. Statistical Tests Section
- ADF test results
- Cointegration test results
- Stationarity decision display

### 9. Mean Reversion Metrics Section
- Half-life display and interpretation
- Hurst exponent display and interpretation
- Mean reversion strength indicators

### 10. Trade Signal Summary Section
- Table of historical signals
- Entry/exit points
- Performance metrics (if backtesting enabled)

### 11. Export Section
- Data export controls
- Chart export controls
- Session save/load controls

## User Interaction Flow

1. User enters asset tickers and parameters
2. Dashboard fetches data and performs initial analysis
3. Charts and statistics are displayed
4. User can adjust parameters to refine analysis
5. User can explore charts through interactive features
6. User can export data or save session for later use

## Integration with Other Modules

### Data Module Integration
- Requests data based on user inputs
- Handles data refresh when inputs change

### Analysis Module Integration
- Triggers analysis calculations based on user inputs
- Displays analysis results in appropriate sections

### Visualization Module Integration
- Embeds visualization components in dashboard layout
- Updates visualizations when analysis results change

## Usage Example

```python
from dashboard.components.input_panel import create_input_panel
from dashboard.components.chart_panel import create_chart_container
from dashboard.layouts import create_main_layout
from dashboard.callbacks import register_callbacks

# Create dashboard components
input_panel = create_input_panel()
chart_container = create_chart_container("Z-Score Analysis", zscore_chart)

# Create main layout
layout = create_main_layout(input_panel, chart_container)

# Initialize app with layout
app = dash.Dash(__name__)
app.layout = layout

# Register callbacks
register_callbacks(app)

# Run the app
if __name__ == '__main__':
    app.run_server(debug=True)
```

## User Experience Considerations

The dashboard module implements UX best practices:
1. **Intuitive Layout**: Organizing information in a logical flow
2. **Progressive Disclosure**: Showing basic information first, with details available on demand
3. **Responsive Design**: Adapting to different screen sizes
4. **Consistent Styling**: Maintaining visual consistency throughout
5. **Helpful Guidance**: Providing tooltips and explanations for complex concepts

## Future Enhancements

- User authentication and personalized settings
- Dashboard templates for different analysis focuses
- Advanced filtering and sorting of results
- Comparison of multiple pairs simultaneously
- Notification system for new trading signals