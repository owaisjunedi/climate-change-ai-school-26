
# Deep Learning for Empirical Statistical Downscaling (DeepESD) of Climate Data

This project implements and evaluates deep learning architectures (**DeepESD** CNN and **U-Net**) for **Empirical Statistical Downscaling (ESD)** of precipitation over New Zealand. It maps coarse-resolution global atmospheric fields to high-resolution daily precipitation maps.

---

## 📌 Project Overview
* **Domain:** AI for Climate Science / Meteorology / Climate Change Adaptation.
* **Objective:** Predict fine-scale precipitation ($Y \in \mathbb{R}^{128 \times 128}$) from 15 coarse large-scale atmospheric predictor fields ($X \in \mathbb{R}^{15 \times 16 \times 16}$).
* **Study Area:** New Zealand (focusing on extreme orographic precipitation across the Southern Alps and West Coast).

---

## 🛠️ Tech Stack & Libraries
* **Framework:** PyTorch (`torch.nn`, `DataLoader`, `Dataset`)
* **Geospatial & Climate Data:** `xarray`, `numpy`, `pandas`
* **Visualization:** `matplotlib`, `cartopy`
* **Sustainability Tracking:** `codecarbon`

---

## 🏗️ Model Architectures

### 1. DeepESD (Baseline CNN)
* **Input:** 15 atmospheric predictor channels ($u, v, q, t, z$ at 850, 700, 500 hPa).
* **Convolutions:** 3 convolutional layers ($15 \rightarrow 50 \rightarrow 25 \rightarrow 1$) with 3x3 kernels and ReLU activations.
* **Output:** Fully connected linear layer mapping flattened feature maps directly to 16,384 spatial grid points.

### 2. U-Net Downscaler (Encoder-Decoder)
* **Encoder:** Multi-scale feature extraction with max-pooling.
* **Decoder:** Progressive upsampling with skip connections to preserve localized topographic features.

---

## 📊 Evaluation & Climate Diagnostics
Models are evaluated on test data (1981–2000) across both average climatology and key climate extremes:
* **RMSE:** Daily spatial root mean squared error.
* **SDII (Simple Daily Intensity Index):** Mean rainfall intensity on wet days ($\ge 1.0 \text{ mm/day}$).
* **P98:** 98th percentile daily precipitation (heavy rain events).
* **RX1day:** Annual maximum 1-day precipitation (flood risk metric).

---

## 🚀 Key Results & Insights
1. **Resolution Recovery:** DeepESD successfully recovers sharp localized precipitation gradients driven by mountain topography that coarse GCMs miss.
2. **Transferability:** The trained neural network generalizes effectively to unseen climate models (`GCM_TRANSFER`), demonstrating robust physical mapping ($f(X) \rightarrow Y$).
3. **Climate Projections (2080–2099):** Successfully projects localized climate change signals under end-of-century warming scenarios.

---

## 👤 Author
Developed as part of the **CCAI (Climate Change AI)** Virtual Summer School.

-----
-----

# 🧠 Core Concepts & Domain Context

### 🌍 The Climate Science Problem: Statistical Downscaling
* **The Challenge:** Global Climate Models (GCMs) simulate the Earth's atmosphere on coarse grid resolution (~100–200 km per cell). Because of this coarse scale, GCMs miss critical local topographic features—such as mountain ranges (e.g., New Zealand's Southern Alps) and coastal boundaries—failing to capture localized weather phenomena like **orographic precipitation** (heavy rainfall driven by moist air forced over mountains).
* **The Solution (ESD):** **Empirical Statistical Downscaling (ESD)** treats downscaling as a supervised machine learning problem (\\(f(X) \rightarrow Y\\)). It uses high-resolution observations or Regional Climate Models (RCMs) as "pseudo-reality" target ground truth (\\(Y\\)) and maps large-scale atmospheric state variables (\\(X\\)) to local precipitation maps.

---

# 💻 Computer Science & Machine Learning Architecture

### 1. Data Pipeline & Data Leakage Prevention
* **Predictors (\\(X\\)):** 15 large-scale atmospheric variables across 3 pressure levels (850, 700, and 500 hPa):
  * Zonal wind (\\(u\\)), Meridional wind (\\(v\\)), Specific humidity (\\(q\\)), Temperature (\\(t\\)), Geopotential height (\\(z\\)).
  * PyTorch Tensor Shape: `(batch_size, channels=15, height=16, width=16)`
* **Predictand (\\(Y\\)):** High-resolution daily surface precipitation (\\(pr\\), in mm/day) on a 128×128 spatial grid over New Zealand.
  * Target Tensor Shape: `(batch_size, n_gridpoints=16384)`
* **Strict Temporal Splitting:**
  * **Train Period:** 1961–1976 (16 years)
  * **Validation Period:** 1977–1980 (4 years)
  * **Test / Historical Period:** 1981–2000 (20 years)
* **Z-score Normalization:** Standardizes inputs using \\(Z = \frac{X - \mu}{\sigma}\\). **Crucial CS practice:** Mean (\\(\mu\\)) and standard deviation (\\(\sigma\\)) are computed **strictly from training years** to prevent data leakage into validation, testing, or future climate projection sets.

---

### 2. Model Architectures
#### A. **DeepESD (CNN Baseline)**
* **Type:** 3-layer Convolutional Neural Network followed by a dense linear readout.
* **Layers:**
  1. `Conv2d(15 -> 50, kernel=3, padding=1)` + ReLU
  2. `Conv2d(50 -> 25, kernel=3, padding=1)` + ReLU
  3. `Conv2d(25 -> 1, kernel=3, padding=1)` + ReLU
  4. `Flatten` + `Linear(flat_features -> 16384)`
* **Design Philosophy:** Captures local spatial combinations of wind, moisture, and temperature via convolutions, then projects the compressed atmospheric representation directly to all high-resolution target grid cells simultaneously.

#### B. **U-Net Downscaler (Advanced Architecture)**
* **Type:** Fully Convolutional Encoder-Decoder with Skip Connections.
* **Design Philosophy:** Uses downsampling (`MaxPool2d`) to extract multi-scale atmospheric features, and upsampling (`ConvTranspose2d` + bilinear upsampling) with skip connections (`torch.cat`) to preserve high-frequency spatial boundaries and terrain details.

---

### 3. Optimization, Loss & Physical Constraints
* **Loss Function:** Mean Squared Error (`nn.MSELoss()`).
* **Optimizer:** Adam (`lr=1e-3`, batch size=32, 50 epochs).
* **Physical Post-Processing (`da.clip(min=0.0)`):** MSE regression models can occasionally predict slight negative values for zero-inflated variables like rainfall. Output arrays are clipped at `0.0` to enforce physical reality (\\(pr \ge 0\\)).
* **Carbon Tracking (`CodeCarbon`):** Integrated `EmissionsTracker` to log electricity usage and \\(\text{CO}_2\text{eq}\\) footprint during GPU model training.

---

### 4. Climate Diagnostics & Extreme Evaluation Metrics
Standard MSE evaluates overall daily error, but climate impact studies require evaluating **extreme events**:
* **Daily Mean:** General precipitation climatology.
* **SDII (Simple Daily Intensity Index):** Average rainfall on wet days (\\(\ge 1.0\text{ mm/day}\\)), filtering out dry days.
* **P98 (98th Percentile):** Threshold for heavy rainfall days.
* **RX1day:** Annual maximum 1-day precipitation (key indicator for extreme flood risk).
* **Spatially Averaged Absolute Bias (\\(|\text{bias}|\\)):** Evaluates spatial bias without allowing positive biases (overestimation in mountains) and negative biases (underestimation at coasts) to cancel each other out.

---

### 5. Advanced ML Concepts Demonstrated
1. **Distribution Shift / GCM Predictor Bias:**
   * **"Perfect" Predictors:** Reanalysis/RCM-derived fields used for training.
   * **"Imperfect" Predictors:** Raw GCM atmospheric fields.
   * *Lesson:* Even in historical periods, GCM predictor distributions shift relative to reanalysis, showing why bias adjustment or robust feature extraction is necessary.
2. **End-of-Century Projection (2080–2099 vs 1981–2000):**
   * Evaluated climate change delta (\\(\Delta = \text{Future} - \text{Historical}\\)).
   * Proved that DeepESD successfully recovers local orographic climate change signals (e.g., sharp precipitation increases along the Southern Alps) that coarse GCMs completely blur.
3. **Out-of-Model Generalization (Transferability):**
   * Tested the model trained on `GCM_TRAIN` (ACCESS-CM2) by evaluating it on `GCM_TRANSFER` without retraining.
   * Confirmed that the neural network learned generalizable atmospheric physics rather than overfitting to one specific climate model's peculiarities.

---

-----

