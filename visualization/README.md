# Visualization Module

The Visualization Module is responsible for creating interactive charts and plots that display the results of the statistical analyses in an intuitive and informative way.

## Purpose

This module transforms complex statistical data into visual representations that help traders:
1. Identify trading opportunities
2. Understand the statistical relationship between assets
3. Evaluate the strength and reliability of pairs trading signals
4. Monitor the performance of trading strategies

## Components

### 1. Chart Components (`charts.py`)

Implements reusable chart components for different types of analyses.

**Key Functions:**
- `create_price_chart(asset1_data, asset2_data)`: Creates dual-axis price chart for two assets
- `create_ratio_chart(ratio_data, rolling_mean, std_bands)`: Creates price ratio chart with bands
- `create_regression_chart(asset1, asset2, regression_line)`: Creates scatter plot with regression line
- `create_spread_chart(spread, mean, bands, signals)`: Creates spread chart with signals
- `create_zscore_chart(zscore, thresholds, signals)`: Creates z-score chart with threshold lines
- `create_correlation_chart(correlation_data)`: Creates rolling correlation chart
- `create_half_life_chart(half_life_data)`: Creates half-life evolution chart
- `create_backtest_chart(equity_curve)`: Creates equity curve for backtest results

**Dependencies:**
- Plotly for interactive charts
- pandas for data handling

### 2. Layout Management (`layouts.py`)

Manages the arrangement and organization of charts in the dashboard.

**Key Functions:**
- `create_grid_layout(charts, rows, cols)`: Arranges charts in a grid layout
- `create_tab_layout(charts, tab_names)`: Organizes charts in tabbed interface
- `create_expandable_layout(charts, titles)`: Creates expandable/collapsible sections
- `create_responsive_layout(charts)`: Ensures charts are responsive to screen size

**Dependencies:**
- Dash for layout components
- Plotly for figure management

### 3. Visual Styling (`themes.py`)

Provides consistent styling and theming across all visualizations.

**Key Functions:**
- `apply_theme(figure, theme='light')`: Applies theme to a figure
- `create_color_palette(base_color, n_colors)`: Generates harmonious color palette
- `style_axis(figure, axis_title, range=None)`: Applies consistent axis styling
- `add_annotations(figure, annotations)`: Adds annotations to charts

**Dependencies:**
- Plotly for figure styling
- ColorLover or similar for color palette generation

## Chart Types

### 1. Time Series Charts
- **Raw Price Series**: Dual-axis line chart showing prices of both assets
- **Price Ratio**: Line chart with rolling mean and standard deviation bands
- **Spread Chart**: Line chart showing the spread with mean and bands
- **Z-score Chart**: Line chart with threshold lines and signal markers

### 2. Statistical Charts
- **Regression Scatter Plot**: Scatter plot with regression line
- **Rolling Correlation**: Line chart showing correlation evolution
- **Rolling Hedge Ratio**: Line chart showing hedge ratio evolution
- **Half-Life Chart**: Bar or line chart showing mean reversion speed

### 3. Performance Charts
- **Equity Curve**: Line chart showing cumulative returns
- **Drawdown Chart**: Line chart showing drawdowns
- **Trade Distribution**: Histogram of trade returns
- **Performance Metrics**: Radar chart of key performance indicators

## Interactive Features

All charts include interactive features:
- **Zoom and Pan**: Allows users to focus on specific time periods
- **Hover Information**: Shows detailed data on hover
- **Crosshair**: Synchronizes cursor position across charts
- **Legend Toggle**: Enables showing/hiding series
- **Download**: Allows saving charts as PNG/SVG
- **Tooltips**: Provides explanations of metrics and indicators

## Integration with Other Modules

### Analysis Module Integration
- Receives analysis results and transforms them into visual representations
- Adapts chart types based on analysis outputs

### Dashboard Module Integration
- Provides chart components to be embedded in dashboard layouts
- Updates charts in response to user input changes
- Implements callbacks for interactive features

## Usage Example

```python
from visualization.charts import create_zscore_chart
from visualization.themes import apply_theme

# Create z-score chart with signals
zscore_chart = create_zscore_chart(
    zscore_data=zscore_series,
    thresholds=[-2, -1, 1, 2],
    signals=signal_data
)

# Apply styling
styled_chart = apply_theme(zscore_chart, theme='dark')

# The chart is now ready to be added to the dashboard
```

## Visualization Best Practices

The module implements visualization best practices:
1. **Consistent Color Coding**: Using consistent colors for related metrics
2. **Clear Labeling**: Providing informative titles, axis labels, and legends
3. **Appropriate Chart Types**: Selecting the most suitable chart type for each analysis
4. **Visual Hierarchy**: Emphasizing important information through size, color, and position
5. **Responsive Design**: Ensuring charts work well on different screen sizes

## Future Enhancements

- Advanced interactive features (brushing, linking)
- Custom visualization types for pairs trading
- 3D visualizations for multivariate relationships
- Animation capabilities for time-evolving metrics
- Dashboard templates for different analysis focuses