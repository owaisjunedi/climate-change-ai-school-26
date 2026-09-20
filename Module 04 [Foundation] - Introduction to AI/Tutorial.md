### Executive Overview: The Machine Learning Pipeline

In this tutorial, you built and evaluated an **end-to-end Machine Learning pipeline** for predicting seismic tsunami hazards using global USGS earthquake data. 

As a Computer Science graduate, this workflow demonstrates key systems-level and theoretical ML concepts: **representation learning for topological domains**, **data leakage prevention**, **cost-sensitive learning for imbalanced distributions**, **the bias-variance tradeoff**, **ensemble mechanics**, and **operational risk analysis**.

---

### Phase 1: Feature Engineering & Representation Learning

```
Raw Longitude (-180° to +180°) ──► [sin(θ), cos(θ)] ──► Unit Circle S¹
  • Fiji-East (+179°) & Fiji-West (-179°)
  • Raw Difference: 358° (Discontinuous boundary)
  • Cyclic Euclidean Distance: ≈ 0.035 (Preserves spatial topology)
```

1. **Robust Missing Data Imputation:**
   * **Mechanism:** Missing numerical values (`gap`, `horizontalError`, `depthError`, `nst`) were imputed using the **median** rather than the mean.
   * **CS/ML Rationale:** Seismic measurement errors exhibit heavily skewed, long-tailed distributions. Median imputation prevents extreme station outages or bad telemetry from biasing central feature estimates.

2. **Cyclic Trigonometric Encoding for Spatial Continuity (\\(S^1\\) Mapping):**
   * **The Boundary Problem:** Longitude \\(\theta \in [-180^\circ, 180^\circ]\\) is a circular feature. On a 1D scalar line, \\(+179^\circ\\) (Fiji East) and \\(-179^\circ\\) (Fiji West) are mathematically \\(358^\circ\\) apart, causing models to treat neighboring subduction zones across the International Date Line as opposite ends of the Earth.
   * **The Mathematical Transformation:** Mapping longitude and latitude into 2D Cartesian coordinates on the unit circle:
     \\[\text{lon\_sin} = \sin(\text{radians}(\text{longitude})), \quad \text{lon\_cos} = \cos(\text{radians}(\text{longitude}))\\]
   * **Result:** The artificial discontinuity at \\(\pm 180^\circ\\) is eliminated. The Euclidean distance in \\(\mathbb{R}^2\\):
     \\[d = \sqrt{(\sin \theta_1 - \sin \theta_2)^2 + (\cos \theta_1 - \cos \theta_2)^2}\\]
     shrinks to \\(\approx 0.035\\) between \\(+179^\circ\\) and \\(-179^\circ\\), preserving true physical proximity on the sphere.

3. **Domain Knowledge Feature Injection:**
   * **Mechanism:** Created an explicit binary feature `shallow = (depth < 70).astype(int)`.
   * **CS/ML Rationale:** Linear classifiers cannot represent non-linear step thresholds without explicit interaction terms. Manually encoding the physical boundary at \\(70\text{ km}\\) gives simpler linear models a direct non-linear feature signal.

---

### Phase 2: Data Partitioning & Leakage Prevention

1. **Stratified Splitting (\\(60\% / 20\% / 20\%\\)):**
   * **Class Imbalance Context:** Tsunamis occur in only \\(\sim 3\%\\) of recorded earthquakes.
   * **Stratification (`stratify=y`):** Guarantees that the training (\\(60\%\\)), validation (\\(20\%\\)), and test (\\(20\%\\)) sets maintain the exact same positive class distribution (\\(\sim 3\%\\)), preventing zero-positive splits in rare-event subsets.

2. **Strict Pipeline Isolation (Preventing Data Leakage):**
   ```python
   X_train_scaled = scaler.fit_transform(X_train)  # Learn μ, σ from Train ONLY
   X_val_scaled   = scaler.transform(X_val)         # Apply Train μ, σ to Validation
   X_test_scaled  = scaler.transform(X_test)        # Apply Train μ, σ to Test
   ```
   * **CS/ML Rationale:** Calling `scaler.fit()` on the full dataset causes **data leakage**—information about the test set distribution (\\(\mu, \sigma\\)) leaks into training preprocessing, producing over-optimistic evaluation metrics that fail in production.

---

### Phase 3: Classification Under Class Imbalance

1. **The Accuracy Paradox:**
   * **Naive Baseline ("Always Predict 0"):** Achieves **\\(\sim 97\%\\) raw accuracy**, but **Recall = 0.000** and **\\(F_1 = 0.000\\)**.
   * **Takeaway:** Raw accuracy is a misleading metric for imbalanced classification.

2. **Cost-Sensitive Training (`class_weight='balanced'`):**
   * In standard Logistic Regression, loss minimization treats all misclassifications equally.
   * `class_weight='balanced'` scales the loss penalty inversely proportional to class frequencies:
     \\[w_1 = \frac{N_{\text{total}}}{2 \times N_{\text{positive}}}\\]
   * This heavily penalizes false negatives (\\(y=1\\) predicted as \\(0\\)), forcing the decision boundary to prioritize detecting rare tsunami events.

3. **Asymmetric Loss & Decision Threshold Tuning:**
   * **Asymmetric Risk:** In life-safety systems:
     * **False Negative (Missed Tsunami):** Catastrophic loss of human life.
     * **False Positive (False Alarm):** Temporary operational/evacuation cost.
   * **Threshold Shift:** By converting output probabilities \\(P(y=1|X)\\) to hard predictions using a lowered decision threshold (\\(\tau = 0.20 - 0.30\\) instead of \\(0.50\\)), **Recall rises toward \\(\sim 95\%+\\)**, accepting lower precision as an intentional trade-off.

---

### Phase 4: Model Complexity & The Bias-Variance Tradeoff

```
Tree Depth (Complexity) ──►
• Depth 1–3  : Underfitting (High Bias)  ──► Train F1: 0.25–0.35 | Val F1: 0.24–0.32 (Gap ≈ 0.02)
• Depth 5    : Sweet Spot (Optimal)      ──► Train F1: 0.445    | Val F1: 0.386    (Gap = 0.059)
• Depth None : Overfitting (High Variance)──► Train F1: 1.000    | Val F1: 0.483    (Gap = 0.517)
```

1. **Decision Tree Depth Analysis:**
   * **Underfitting (\\(\text{max\_depth} \le 3\\)):** High bias. The model lacks capacity to capture non-linear interaction terms between depth, magnitude, and coordinates.
   * **Overfitting (\\(\text{max\_depth} = \text{None}\\)):** High variance. The tree splits until every training leaf node is pure, achieving **100% Training \\(F_1\\)**, but creating a massive **\\(0.517\\) generalization gap** on validation data.
   * **Hyperparameter Tuning:** `max_depth = 5` optimizes the bias-variance tradeoff on validation data prior to test set evaluation.

2. **Ensemble Learning (Random Forest Classifier):**
   * Combines **Bootstrap Aggregating (Bagging)** and **Random Subspace Method** (random feature selection per split).
   * Reduces variance compared to a single deep decision tree, increasing test set Precision to **\\(66.7\%\\)** and achieving the overall highest \\(F_1\\) score (**\\(0.522\\)**).

---

### Phase 5: Comprehensive Model Evaluation Summary

| Model / Approach | Accuracy | Precision | **Recall** | **\\(F_1\\) Score** | Key Characteristics |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Always Predict 0** | **97.0%** | 0.0% | 0.0% | 0.000 | Accuracy paradox; zero utility. |
| **Physical Rule (\\(M \ge 7 \land \text{depth} < 70\\))** | 98.1% | **86.7%** | 31.0% | 0.456 | Conservative domain heuristic; low recall. |
| **Logistic Regression (\\(\tau = 0.5\\))** | 92.9% | 26.5% | **95.2%** | 0.415 | Highest Recall; catches almost all tsunamis. |
| **Decision Tree (\\(\text{depth} = 5\\))** | 97.6% | 53.8% | 50.0% | 0.519 | Balanced rule splits; moderate generalization. |
| **Random Forest (\\(\tau = 0.5\\))** | 97.9% | 66.7% | 42.9% | **0.522** | Highest \\(F_1\\)/Precision; needs \\(\tau \approx 0.25\\) for higher Recall. |

---

### Phase 6: Core Engineering Extensions

#### **1. Challenge A: Regional Filtering (Japan Subduction Zone)**
* **Domain Context:** Filtering to a single subduction zone (e.g., Japan: Lat \\(25^\circ-45^\circ\\), Lon \\(125^\circ-150^\circ\\)).
* **ML Dynamics:**
  * **Higher Base Rate:** Local tsunami incidence rises (\\(\sim 5-8\%\\)), raising model Precision.
  * **Sample Size Drop:** Reduces training sample size (\\(N\\)), making deep non-linear models prone to overfitting and favoring simpler regularized classifiers.
  * **Spatial Homogeneity:** Features focus on a single fault geometry (Japan Trench), sharpening the physical signal of magnitude and depth.

#### **2. Challenge B: Continuous Regression (\\(y = M_w\\) Earthquake Magnitude)**
* **Shift to Regression:** Target switched from binary `tsunami` to continuous magnitude `mag` using `RandomForestRegressor`.
* **Key Feature Discovered:** `nst` (**Number of Seismic Stations**) emerged as the dominant predictor of magnitude.
* **Physical Basis:** Earthquake energy scales exponentially (\\(\approx 10^{1.5 \times M}\\)). Larger ruptures send high-amplitude seismic waves globally, triggering detections across hundreds of recording stations.
* **Operational Caution:** `nst` requires wave arrival time, meaning it grows over minutes post-event. Utilizing `nst` recorded at \\(T=30\text{ mins}\\) to predict magnitude at \\(T=0\text{ secs}\\) would represent **temporal data leakage**.

---

### Phase 7: Systems & Operational Risk Engineering

1. **Feature Latency vs. Alert Speed:**
   * High-accuracy physical parameters like **focal mechanism (moment tensor solutions)** take \\(10-30\text{ minutes}\\) to invert from global waveforms. 
   * Early warning classifiers must rely on fast-arriving first-motion estimates (magnitude, hypocenter, depth) available within seconds, trading marginal accuracy for critical response time.

2. **Out-of-Distribution (OOD) Extrapolation Limits:**
   * Tree-based models (Decision Trees, Random Forests, XGBoost) **cannot extrapolate linear trends beyond training bounds**. An \\(M_w 9.2\\) megathrust event will be evaluated against the highest threshold learned in training (e.g., \\(M_w 7.8\\)).
   * Operational systems combine ML classifications with physics-based hydrodynamic ocean buoy simulations (e.g., NOAA SIFT) to maintain safety guarantees during black-swan events.

---

---

### Tutorial walkthrough: <br/>
https://www.youtube.com/watch?v=SdjQWHqs0YQ