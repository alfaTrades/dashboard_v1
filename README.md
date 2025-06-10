# Pairs Trading Dashboard

A comprehensive dashboard for analyzing mean-reverting relationships between asset pairs to support pairs trading strategies.

## Overview

This dashboard enables traders to analyze statistical relationships between any two assets (e.g., Gold and Silver), using various statistical methods and visual tools to identify potential pairs trading opportunities.

### Key Features (v1)

- Support for analyzing two assets simultaneously
- Comprehensive statistical analysis including:
  - Price ratio analysis
  - OLS regression and hedge ratio calculation
  - Spread analysis and Z-score calculation
  - Stationarity and cointegration tests
  - Mean reversion metrics (half-life, Hurst exponent)
  - Rolling correlation analysis
- Interactive visualizations for all analyses
- Trading signal generation based on Z-score thresholds
- Historical trade summary and basic performance metrics
- Data export functionality
- Local hosting

## Project Structure

```
dashboard_v1/
├── app.py                      # Main application entry point
├── config.py                   # Configuration settings
├── requirements.txt            # Project dependencies
├── data/                       # Data management
├── analysis/                   # Statistical analysis
├── visualization/              # Data visualization
├── dashboard/                  # Dashboard components
├── utils/                      # Utility functions
├── tests/                      # Unit and integration tests
└── docs/                       # Additional documentation
```

## Getting Started

### Prerequisites

- Python 3.8+
- pip (Python package installer)

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/dashboard_v1.git
   cd dashboard_v1
   ```

2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

3. Run the application:
   ```
   python app.py
   ```

4. Open your browser and navigate to:
   ```
   http://localhost:8050
   ```

## Documentation

For detailed documentation on each module, please refer to the README.md files in the respective directories:

- [Data Module](data/README.md)
- [Analysis Module](analysis/README.md)
- [Visualization Module](visualization/README.md)
- [Dashboard Module](dashboard/README.md)
- [Utils Module](utils/README.md)

Additional documentation can be found in the [docs](docs/) directory.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
