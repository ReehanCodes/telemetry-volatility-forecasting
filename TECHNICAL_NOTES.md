# Technical Notes: Time Series Forecasting with Heteroskedastic Models

## 1. Time Series Fundamentals

### 1.1 Definition

A **time series** is a sequence of observations indexed by time: {y₁, y₂, ..., yₜ}, where temporal ordering carries information.

**Key property:** Observations exhibit **temporal dependence**—yₜ is correlated with yₜ₋₁, yₜ₋₂, etc.

### 1.2 Stationarity

A time series is **weakly stationary** if:
1. Constant mean: E[yₜ] = μ for all t
2. Constant variance: Var(yₜ) = σ² for all t  
3. Covariance depends only on lag: Cov(yₜ, yₜ₋ₖ) = γₖ

**Why it matters:** Stationary processes are predictable—their statistical properties persist into the future.

## 2. AR(1) Model

### 2.1 Model Specification

The AR(1) (first-order autoregressive) model:
```
yₜ = μ + φ(yₜ₋₁ - μ) + εₜ
```

where:
- μ = unconditional mean
- φ = autoregressive coefficient (|φ| < 1 for stationarity)
- εₜ ~ N(0, σ²) = white noise errors

**Alternative form:**
```
yₜ = c + φ yₜ₋₁ + εₜ    where c = μ(1-φ)
```

### 2.2 Properties

**Unconditional mean:**

Taking expectations:
```
E[yₜ] = μ + φ(E[yₜ₋₁] - μ) + E[εₜ]
```

In stationarity, E[yₜ] = E[yₜ₋₁] = E[y]:
```
E[y] = μ + φ(E[y] - μ)
E[y] = μ
```

**Unconditional variance:**

Taking variance:
```
Var(yₜ) = φ² Var(yₜ₋₁) + Var(εₜ)
```

In stationarity:
```
σ²ᵧ = φ² σ²ᵧ + σ²
σ²ᵧ(1 - φ²) = σ²
σ²ᵧ = σ²/(1 - φ²)
```

**Autocorrelation function:**

For lag k:
```
ρₖ = Correlation(yₜ, yₜ₋ₖ) = φᵏ
```

Correlation decays exponentially with lag.

**Stationarity condition:** |φ| < 1

If φ = 1: random walk (non-stationary, variance grows without bound)  
If |φ| > 1: explosive process

### 2.3 Interpretation