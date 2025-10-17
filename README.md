Estimating Cosmological Parameters with BayesFlow

Simulation-Based Inference Project
TU Dortmund University – Summer Term 2025
Authors: Maria Levina (230579), Rahul Vishwkarma (236862)

📌 Project Overview

This project applies Neural Posterior Estimation (NPE) using the BayesFlow framework to infer cosmological parameters 
from simulated noisy galaxy matter power spectra. The estimated parameters are:

H₀ (Hubble constant)

Ωₘ (matter density)

nₛ (spectral index)

Two posterior approximators were compared:

Affine Coupling Flow

Spline Coupling Flow

The spline-based approach showed superior calibration and parameter recovery.

🧠 Methodology
1. Data Generation

Prior distributions (independent, uniform):

H₀ ∼ U(30, 100)

Ωₘ ∼ U(0.1, 0.6)

nₛ ∼ U(0.8, 1.5)

Simulator:
CAMB (2025) generates Pθ(k) over K = 256 logarithmically spaced wavenumber values.

Noise model:
Add Gaussian noise in log10-space
ε ∼ 𝒩(0, 0.2·Iₖ)

Observation:

y = log10(Pθ(k)) + ε

2. NPE Framework (BayesFlow)

Summary Network:
1D CNN → latent 32-dim representation

Inference Networks:

Affine coupling flow

Spline coupling flow


Adapter: standardizes summaries and parameters

3. Training

10k training samples, 1k validation samples

Offline simulation

200 epochs, 200 batches/epoch, batch size 128

Optimization: Defaults from BayesFlow (Adam)

✅ Diagnostics & Results
🔹 Convergence

Smooth decrease of NLL

No overfitting

Spline flow achieves lower NLL than affine

🔹 Calibration (SBC)

ECDF-difference curves within 95% bands

Slight bias for Ωₘ in spline, but insignificant

🔹 Parameter Recovery

Correlation (true vs. posterior mean):

| Parameter | Affine | Spline |
| --------- | ------ | ------ |
| H₀        | 0.894  | 0.985  |
| Ωₘ        | 0.766  | 0.956  |
| nₛ        | 0.882  | 0.982  |


Spline flow clearly outperforms affine.
