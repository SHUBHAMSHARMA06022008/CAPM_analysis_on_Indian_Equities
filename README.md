# CAPM Analysis: NIFTY 50 Alpha Generation Study

A quantitative analysis framework for evaluating individual stock performance against market returns using the Capital Asset Pricing Model (CAPM). This implementation focuses on the NIFTY 50 index constituents, identifying securities that generate excess risk-adjusted returns.

## Overview

This analysis employs regression-based methodology to decompose stock returns into systematic (market-driven) and idiosyncratic (stock-specific) components. By estimating Jensen's alpha for each security, we identify persistent outperformers and underperformers relative to their systematic risk exposure.

## Methodology

### Model Specification

The CAPM regression follows the standard specification:

```
Rᵢ - Rբ = αᵢ + βᵢ(Rₘ - Rբ) + εᵢ
```

Where:
- **Rᵢ**: Log returns of individual security *i*
- **Rₘ**: Log returns of market portfolio (NIFTY 50 index)
- **Rբ**: Risk-free rate (derived from annual rate of 5.624%)
- **αᵢ**: Jensen's alpha (excess return not explained by market exposure)
- **βᵢ**: Systematic risk coefficient
- **εᵢ**: Idiosyncratic error term

### Key Features

- **5-year historical analysis** with daily return calculations
- **Log returns** for time-additive properties and continuous compounding
- **Excess return framework** adjusting for risk-free rate
- **OLS regression** with statistical significance testing
- **Interactive visualization** of top and bottom performers

## Implementation

### Data Acquisition

```python
# Fetches 5 years of adjusted closing prices
# Handles missing data with configurable thresholds
# Processes NIFTY 50 constituents plus index (^NSEI)
```

### Return Calculation

```python
# Logarithmic returns: ln(Pₜ / Pₜ₋₁)
# Daily risk-free rate: (1 + r_annual)^(1/365) - 1
# Excess returns: R - Rբ
```

### Statistical Analysis

For each security:
- Ordinary Least Squares regression against market excess returns
- Alpha estimation with p-value significance testing
- Beta coefficient (systematic risk measure)
- R² (explanatory power of market returns)

## Output

### Visualization

An interactive horizontal bar chart displaying:
- **Top 20 alphas** (blue): Securities with highest excess returns
- **Bottom 20 alphas** (red): Securities with lowest excess returns
- Hover information includes beta and R² values

### Summary Statistics

```
- Top/Bottom 5 performers with key metrics
- Mean and median alpha across all securities
- Average beta and R² statistics
- Count of statistically significant alphas (p < 0.05)
```

## Dependencies

```python
yfinance          # Market data acquisition
pandas            # Data manipulation
numpy             # Numerical operations
statsmodels       # OLS regression
plotly            # Interactive visualization
```

## Interpretation

**Alpha (α)**: The annualized excess return after adjusting for systematic risk. Positive alpha suggests superior security selection or market inefficiency.

**Beta (β)**: Sensitivity to market movements. β > 1 indicates higher volatility than the market; β < 1 indicates lower volatility.

**R² (R-squared)**: Proportion of return variance explained by market returns. Higher values suggest returns are primarily driven by systematic factors.

**Statistical Significance**: P-values < 0.05 indicate alpha is unlikely due to random chance, though persistence of alpha remains an empirical question.

## Limitations

- Historical alpha does not guarantee future performance
- Transaction costs and taxes not incorporated
- Survivorship bias if index composition changed
- Assumes linear relationship between security and market returns
- Risk-free rate held constant over analysis period

## Usage

1. Ensure `ind_nifty50list.csv` contains current NIFTY 50 constituents
2. Execute notebook cells sequentially
3. Review statistical output and interactive visualization
4. Export results dataframe for further analysis

---

**Note**: This analysis is for educational and research purposes. Investment decisions should incorporate additional fundamental, technical, and risk management considerations.
