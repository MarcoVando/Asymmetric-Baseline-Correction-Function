# Background Profile Correction using Asymmetric Least Squares (ALS)

This repository contains a Python implementation of a background correction method using the Asymmetric Least Squares (ALS) smoothing technique described in:

**Baseline Correction with Asymmetric Least Squares Smoothing**  
*Paul H. C. Eilers and Hans F.M. Boelens, 2005*

Other implementations can be found around

## Overview

Baseline drift is a common problem in spectroscopic and chromatographic data. This algorithm estimates the smooth background of a signal and subtracts it to enhance the peak signal. The method uses a penalized least squares approach, where asymmetry in weighting allows the fit to ignore sharp positive peaks while fitting the smoother background.

## Method

The method minimizes the following cost function:

S = Σ wᵢ (yᵢ - zᵢ)² + λ Σ (Δ²zᵢ)²

Where:
- `yᵢ` is the input signal,
- `zᵢ` is the estimated baseline,
- `wᵢ` is a weight depending on whether the residual is positive or negative,
- `λ` is the smoothness parameter (higher means smoother),
- `Δ²zᵢ` represents the second derivative of the baseline (penalizing curvature).

The weights `wᵢ` are updated iteratively to impose asymmetry:
- Residuals below the baseline are weighted more heavily to prevent the fit from rising into peaks.

## Parameters

- `y`: Input 1D signal (numpy array).
- `lam`: Smoothness parameter (e.g., 1e5 to 1e7).
- `p`: Asymmetry parameter between 0 and 1 (e.g., 0.001).
- `niter`: Number of iterations (default: 10).

## Installation

```bash
pip install numpy scipy
```

## References

Paul H. C. Eilers and Hans F. M. Boelens (2005). "Baseline Correction with Asymmetric Least Squares Smoothing". Leiden University Medical Centre Report.
