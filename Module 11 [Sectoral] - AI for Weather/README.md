This module—**Module 11: AI for Weather**—explores how artificial intelligence and machine learning are transforming short-range weather forecasting, long-range seasonal climate predictions, and impact-driven weather risk management.

Below is an in-depth summary of the core themes, model architectures, and evaluation frameworks covered in this module:

---

### **1. Short-Range Weather Forecasting (Weather as an Initial Value Problem)**
* **The "Quiet Revolution" of NWP:** Traditional Numerical Weather Prediction (NWP) relies on high-performance supercomputing to solve physical fluid dynamics equations.
* **Emergence of Machine-Learned Weather Prediction (MLWP):** Breakthrough AI models—such as **GraphCast**, **GenCast**, **FourCastNet**, **Pangu Weather**, **AIFS**, **FuXi**, and **Prithvi WxC**—now match or exceed traditional physics-based models in medium-range forecasting accuracy while running at a tiny fraction of the computational cost.
* **Architecture Evolution:** Weather AI has progressed rapidly from basic feed-forward and convolutional networks (CNNs) to **Graph Neural Networks (GNNs)**, **Vision Transformers (ViTs)**, **Diffusion models**, and **Masked Auto-Encoders**.
* **Hybrid Physics-AI Futures:** Rather than completely replacing physics, the near-term operational future combines dynamic physics-based cores with learned AI parameterizations and AI-accelerated data assimilation.

---

### **2. Long-Range & Seasonal Forecasting (S2S)**
* **Seasonal Dynamics:** While short-range weather relies on initial atmospheric conditions, seasonal forecasting (e.g., predicting climate conditions over 90-day periods) depends on slower Earth system drivers like **El Niño-Southern Oscillation (ENSO)** and ocean sea surface temperatures (SSTs).
* **AI in Seasonal Time Scales:** Machine learning models (such as adaptively forced probabilistic models like **GenCast**) are showing promising ability to capture El Niño and La Niña climate anomalies.

---

### **3. Bias Correction & Deep Learning Frameworks**
* **The Bias Challenge:** Raw output from both physical global climate models and AI models contains spatial and temporal biases that limit their direct operational use.
* **Traditional vs. AI Bias Correction:** Traditional methods—like **Linear Scaling (LS)** and **Quantile Mapping (QM)**—assume stationary or constant bias distributions.
* **Season-Net Framework:** The module highlights **Season-Net**, a hybrid deep learning model combining **U-Net** and **ConvLSTM** architectures with a sliding-window quantile loss function. It learns dynamic, spatiotemporal biases to significantly improve extreme event predictions (e.g., heavy precipitation days and warm days exceeding 35°C) across regions in Africa and North America.

---

### **4. Impact-Based Evaluation & Decision Utility**
* **Going Beyond Raw Accuracy:** Traditional metrics like Mean Absolute Error (MAE) or correlation coefficients can mask poor model skill on critical real-world impacts.
* **Probabilistic Skill Metrics:** The module emphasizes proper probabilistic scoring rules—evaluating **calibration**, **discrimination**, **uncertainty**, **CRPS**, and the **Brier Skill Score (BSS)**.
* **Bridge to Real-World Action:** Forecast skill only creates tangible value when co-produced with national meteorological services and local stakeholders (such as smallholder farmers) to deliver trusted, decision-relevant climate information.
---
---
---

### Key takeaways from today’s lecture:

- AI is No Longer Just a Prototype: Models like GraphCast and GenCast now rival physics-based NWP in accuracy for many variables.

- Probabilistic Skill is Paramount: Raw accuracy is insufficient; the utility of a forecast depends on its calibration, discrimination, and uncertainty quantification.

- Bias Correction is Mandatory: Raw seasonal models are inherently biased; techniques like Quantile Mapping and Season-Net are essential before forecasts can be used for decision-making.

- Focus on Impacts, Not Just Variables: High correlation coefficients can hide a model's failure to predict the extreme "impact-based" events that cause the most harm.

- Co-Production Closes the Loop: Forecast skill only creates value when it reaches people; co-production with end-users (like farmers) turns model output into trusted services.

- Accuracy vs Lead Time Dynamics: While AI models are highly competitive, their accuracy relative to traditional systems such as the Integrated Forecasting System (IFS) can degrade more significantly as lead time increases.

- Variable-Resolution Flexibility: Architectures like Graph Transformers are significantly easier to adapt to variable-resolution models, enabling high-resolution refinement (down to 2.5 km) in specific regions within a global framework.

- The Reanalysis Correction Requirement: Because many AI models are trained on ERA5 reanalysis data, which can be unrealistic for variables like rainfall, it is critical to correct these models toward real-world satellite estimates for operational reliability.

---
---

#### Tutorial walkthrough

https://www.youtube.com/watch?v=BBXR0qPomro

---
