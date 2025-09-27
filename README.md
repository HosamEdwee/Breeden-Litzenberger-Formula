# Breeden-Litzenberger-Formula
apply Breeden-Litzenberger formula on AAPL stock



# Breeden-Litzenberger Formula: Extracting Market Probabilities from Option Prices

## Overview

The Breeden-Litzenberger formula provides a bridge between option prices and the market's view of future asset prices. It uses the prices of many different call options **on the same asset**. These options must all expire on the **same date** but have a wide range of strike prices. The formula focuses on how the option price changes as the strike price changes, measuring the rate of change of this change (the "second derivative"). A sharp change at a specific strike price indicates that the market views prices around that level as significant.

After adjusting for interest rates, the result is a probability distribution showing the market's implied probabilities for every possible price the asset could have on the expiration date. **A peak in the distribution at a certain price means the market assigns a high likelihood to the asset finishing near that price.**

## The Formula

$$f(K) = e^{r\tau} \frac{\partial^2 C(K)}{\partial K^2}$$

Where:
- $f(K)$ = Risk-neutral probability density at strike $K$
- $r$ = Risk-free interest rate
- $\tau$ = Time to maturity (in years)
- $C(K)$ = Call option price at strike $K$

## Understanding the Components

### The Relationship: Call Price vs Strike Price

Let's focus on the relationship between a call option's price $C(K)$ and its strike price $K$.

Consider two call options on the same stock, both expiring in one year:
- **Option A:** Strike price of $100
- **Option B:** Strike price of $101

Which is more valuable? Option A, because it gives you the right to buy at a lower price. Therefore, $C(\$100) > C(\$101)$.

**Fundamental rule: As the strike price ($K$) goes up, the call option price ($C(K)$) goes down.**

### First Derivative: The Speed of Change

$$\frac{\partial C(K)}{\partial K}$$

This measures *how fast* the option's price decreases as you increase the strike price by a tiny amount.

### Second Derivative: The Change in Speed

$$\frac{\partial^2 C(K)}{\partial K^2}$$

This is the **second derivative** - it measures the **change in that speed**.

#### Car Analogy
- Your *position* = option's price, $C(K)$
- Your *speed* = first derivative
- Your *acceleration* = second derivative

#### Example: Stock Trading at $100

1. **Low Strike Prices ($50 → $51):** Price difference ≈ $1 (fast drop)
2. **Near Stock Price ($100 → $101):** Price difference ≈ $0.50 (slowing down)
3. **High Strike Prices ($150 → $151):** Price difference ≈ $0 (very slow)

The second derivative measures how much this speed changes at any given strike price. A large value at a specific strike (e.g., $110) means the rate of change shifts abruptly around $110, indicating the market believes the stock will likely finish at exactly $110.

### The Adjustment Factor

$$e^{r\tau}$$

Where:
- $r$ = risk-free interest rate
- $\tau$ = time until expiration

This factor converts present values to future values, adjusting for the time value of money. It ensures that all probabilities $f(K)$ correctly sum to 1 (100%).

## Real-World Application: AAPL Analysis

### Initial Parameters
| Parameter | Value |
|-----------|-------|
| Ticker | AAPL |
| Current Stock Price | $255.46 |
| Selected Expiration | 2025-10-03 |
| Days to Expiry | 6 |
| Time to Maturity (τ) | 0.0164 years |

### Option Data Parameters
| Parameter | Value |
|-----------|-------|
| Filtered Strike Range | $217.14 - $293.78 |
| Number of Strikes Used | 31 |
| Risk-free Rate | 5.00% |

### Sample Option Data (ATM Strikes)
| Strike | Mid Price | Volume | Implied Volatility |
|--------|-----------|--------|-------------------|
| 250.0 | 6.600 | 4,454 | 0.238655 |
| 252.5 | 4.775 | 2,458 | 0.224617 |
| 255.0 | 3.250 | 18,970 | 0.217293 |
| 257.5 | 2.040 | 34,631 | 0.210945 |
| 260.0 | 1.210 | 64,733 | 0.208992 |

### Distribution Analysis Results
| Metric | Value |
|--------|-------|
| Expected Value | $241.89 |
| Mode (Peak) | $222.40 |
| Standard Deviation | $17.64 |
| Annualized Volatility | 53.85% |

### Probability Distribution
| Distribution | Probability |
|--------------|------------|
| Left of Current Price | 74.99% |
| Right of Current Price | 25.01% |
| Skew Indicator | Negative (crash fears) |

### Tail Probabilities (±5% move)
| Scenario | Probability |
|----------|------------|
| Downside (<$242.69) | 56.77% |
| Upside (>$268.23) | 6.45% |

![AAPL Breeden-Litzenberger Analysis](1.png)

## Code Implementation

The repository includes a Python implementation that:
- Fetches real-time option data using yfinance
- Applies cubic spline interpolation for smooth derivatives
- Calculates risk-neutral probability density
- Analyzes distribution statistics
- Generates visualization plots

### Key Features
- Automatic data retrieval for any ticker
- Robust filtering for liquid options
- Distribution analysis including skew and tail probabilities
- Professional visualization output

## Installation & Usage

```bash
# Install required packages
pip install yfinance numpy pandas scipy matplotlib

# Run the analysis
python breeden_litzenberger.py
```

## Author

**Hossam Edwee**  
[LinkedIn](https://www.linkedin.com/in/hossamedwee)

*Study Bites Series - February 2025*
