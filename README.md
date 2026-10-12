# QUANTISCAN

[![DOI](https://zenodo.org/badge/1414339580.svg)](https://doi.org/10.5281/zenodo.23318482)

A computational mathematics and simulation framework evaluating the absolute physical reconstruction boundaries of **Filtered Backprojection (FBP)** algorithm under low-dose quantum noise constraints.

---

## Project Overview
**QuantiScan** bridges pure computational mathematics with applied clinical medical physics. Modern low-dose computed tomography (CT) protocols prioritize minimizing ionizing radiation exposure, which inherently increases quantum noise (mottle) and creates streak artifacts. This framework models that trade-off using an end-to-end discrete simulation pipeline to map where and how traditional FBP image reconstruction experiences structural breakdown.

By utilizing multi-factor parametric sweeps across photon count levels $I_0$ and projection angles $N_\theta$, this project isolates the geometric boundaries of feature detectability, image quality, and structural fidelity based on three different quantative image metrics.

---

## Pipeline Architecture
The simulation framework executes via five highly transparent, reproducible pipeline phases directly mapped in the codebase:
1. **Analytical Phantom Generation (`build_phantom`):** Synthesizes custom geometric targets with controllable feature radii $r=8$ and localized attenuation contrasts $(\Delta\mu=+0.15\)$.
2. **Forward Projection Simulation (`forward_transform`):** Executes a discrete Radon transform across varying angular sampling densities $10$ to $180$ angles) to generate raw sinograms.
3. **Stochastic Noise Injection (`add_poisson_noise`):** Employs independent Monte Carlo trials sampling directly from a Poisson distribution to accurately model quantum mottle at specific x-ray flux thresholds $10^2$ to $10^5$.
4. **Inverse Radon Reconstruction (`fbp_reconstruction`):** Implements deterministic Filtered Backprojection utilizing standard ramp/Ram-Lak filtering matrices to reconstruct the spatial domain.
5. **Image Quantification via Image Metrics (`compute_cnr`, `compute_psnr`, `compute_ssim`):** Calculates global domain matrices alongside highly localized Contrast-to-Noise Ratios (CNR) to evaluate structural integrity against noise boundaries.

---

## Software Environment & Dependencies
This framework is built using Python 3.10+ and relies completely on the following open-source scientific computing libraries:
* **`scikit-image`:** Core processing engine for the forward Radon and inverse Filtered Backprojection (`iradon`) operations, as well as structural similarity (SSIM) measurements.
* **`numpy`:** Matrix vectorization and stochastic numerical generation using high-integrity pseudo-random number generator (PRNG) seeds.
* **`pandas`:** Data structuring engine to catalog raw execution metrics across all $240$ multi-factor trial coordinates.

---

## How to Execute and Reproduce
You can immediately interact with, audit, and run the complete simulation pipeline live in your browser:
1. Click the **"Open In Colab"** badge at the very top of this page.
2. Select **Runtime -> Run all** from the Google Colab navigation menu to execute the end-to-end multi-factor sweep.
3. **Adaptive Storage Pipeline:** The codebase features an automated environment checker. If you choose not to mount a personal Google Drive account, the script seamlessly switches to **Local Mode** and stores all output matrices/CSVs in a temporary `./outputs` directory within the Colab sidebar container.

---

##  License
This repository is licensed under the terms of the **MIT License**. Feel free to use, modify, or branch this code for open scientific research.
