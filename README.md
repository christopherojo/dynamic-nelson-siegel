# Dynamic Nelson–Siegel Yield Curve Modeling

A research-focused implementation of the Dynamic Nelson–Siegel (DNS) model using a state-space framework and Kalman filtering to estimate and forecast the yield curve.

---

## Overview

This repository explores term structure modeling through the lens of latent factor models. The yield curve is represented using three interpretable factors—level, slope, and curvature—that evolve dynamically over time.

Instead of estimating the yield curve independently at each point in time, this project models the underlying factors as hidden states and applies the Kalman filter to obtain smooth, robust, and forecastable estimates.

---

## Objectives

* Implement the Nelson–Siegel model for cross-sectional yield curve fitting
* Extend to the Dynamic Nelson–Siegel (DNS) framework
* Estimate latent factors using a Kalman filter
* Apply Rauch–Tung–Striebel smoothing
* Compare OLS, filtered, and smoothed factor estimates
* Build a foundation for forecasting and macro-augmented extensions

---

## Model

### Nelson–Siegel Representation

The yield curve is modeled as a function of maturity using three latent factors:

* **Level (β₀)** — long-term rates
* **Slope (β₁)** — short vs long-term spread
* **Curvature (β₂)** — medium-term hump

---

### State-Space Formulation

**Observation Equation:**

```
y_t = L β_t + ε_t
```

**State Equation:**

```
β_t = c + A β_{t-1} + η_t
```

Where:

* y_t: observed yields across maturities
* β_t: latent factors (level, slope, curvature)
* L: Nelson–Siegel loadings
* ε_t: observation noise
* η_t: state noise

---

## Methodology

1. Fit static Nelson–Siegel factors using OLS
2. Estimate factor dynamics via VAR(1)
3. Construct state-space model
4. Apply Kalman filter (forward pass)
5. Apply RTS smoother (backward pass)
6. Analyze and compare factor estimates

---

## Repository Structure

```
dynamic-nelson-siegel/
│
├── data/
│   ├── raw/                # Raw yield curve data (e.g., FRED)
│   ├── processed/          # Cleaned datasets
│
├── notebooks/
│   ├── 01_ns_fit.ipynb     # Static Nelson–Siegel fitting
│   ├── 02_ols_factors.ipynb
│   ├── 03_kalman_filter.ipynb
│   ├── 04_smoothing.ipynb
│
├── src/
│   ├── nelson_siegel.py    # NS function + loadings
│   ├── kalman.py           # Kalman filter implementation
│   ├── dns_model.py        # Full DNS pipeline
│   ├── utils.py
│
├── experiments/
│   ├── factor_analysis.py
│   ├── forecasting.py
│
├── results/
│   ├── figures/
│   ├── tables/
│
├── tests/
│   ├── test_kalman.py
│   ├── test_ns.py
│
├── requirements.txt
├── README.md
```

---

## Key Results (Planned)

* Smoothed latent factor trajectories
* Comparison of OLS vs Kalman estimates
* Yield curve reconstruction accuracy
* Stability under missing or noisy data

---

## Extensions

* Macro-augmented DNS (including economic covariates)
* Regime-switching factor dynamics
* Multi-country yield curve modeling
* Trading signals based on factor mispricing

---

## Setup

```
pip install -r requirements.txt
```

---

## Usage

Example workflow:

```
from src.dns_model import DNSModel

model = DNSModel(data)
model.fit()
factors = model.get_factors()
```

---

## References

* Diebold, F. X., & Li, C. (2006). Forecasting the term structure of government bond yields
* Nelson, C. R., & Siegel, A. F. (1987). Parsimonious modeling of yield curves

---

## Notes

This repository is intended as a research and learning environment for understanding:

* State-space models
* Kalman filtering
* Term structure modeling

It prioritizes clarity and modularity over production optimization.
