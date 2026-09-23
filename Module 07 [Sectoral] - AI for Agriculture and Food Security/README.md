This module, titled **"AI for Agriculture and Food Security: From Earth Observation to Climate-Smart Decision Making"**, presented by **Dr. Aliny Reis** (Senior Remote Sensing Scientist at Corvian) for the Climate Change AI Virtual Summer School 2026, focuses on using AI and remote sensing to transform agricultural observations into actionable decision support across spatial scales.

---

### **1. Core Context & The Role of Data**
* **The Dual Role of Agriculture:** Agriculture both contributes significantly to climate change (via land-use change, livestock emissions, and soil management) and is deeply vulnerable to its impacts.
* **Four Pillars of Food Security:** Climate change threatens **availability, access, utilization, and stability**. AI systems aim to help increase productivity, improve resource efficiency, strengthen climate resilience, and protect ecosystems.
* **Stakeholder Spectrum:** Agricultural information serves diverse users across scales, including **farmers** (planting/harvesting decisions), **agronomists** (input optimization), **governments/insurers** (policy and risk response), and **humanitarian organizations** (food security monitoring).

---

### **2. From Observations to Decision Support**
* **Earth Observation (EO) Trade-Offs:** Remote sensing provides large-scale, consistent monitoring, but optical imagery faces cloud-cover limitations, trade-offs between spatial and temporal resolutions, and the need for ground validation.
* **The Value Pipeline:** AI transforms raw observations (satellite imagery, weather, soil, field data) into actionable indicators, maps, and alerts for decision-makers.
* **Types of Analytical Approaches:**
  * **Spatial Analysis:** Captures within-field variability at a single point in time (e.g., soil moisture or vegetation index maps).
  * **Temporal Analysis:** Tracks how crop variables evolve across the growing season (e.g., growth stages or drought trajectories).
  * **Spatio-Temporal Analysis:** Combines spatial patterns with temporal dynamics to model evolving crop conditions and trajectories.

---

### **3. Matching AI Methods to Agricultural Tasks**
The module outlines how specific AI tasks map to classical machine learning and deep learning architectures:
* **Regression:** Predicts continuous values like crop yield, biomass, or nitrogen needs using models like Random Forest, XGBoost, or LSTMs.
* **Classification:** Maps crop types or identifies diseases using Random Forest, Support Vector Machines (SVM), CNNs (ResNet, EfficientNet), or Vision Transformers (ViT).
* **Semantic Segmentation:** Delineates field boundaries or maps flood/burned areas using architectures like U-Net, DeepLabV3+, or Mask R-CNN.
* **Time Series & Forecasting:** Predicts yield trajectories or drought risks using ARIMA, LSTMs, GRUs, or Temporal Fusion Transformers (TFT).
* **Anomaly Detection:** Detects unexpected crop stress or irrigation failures using Isolation Forests or Autoencoders.

---

### **4. AI Across Decision Scales**
* **Field & Farm Level (Precision Agriculture):** Delivers targeted interventions—such as variable-rate nitrogen or seed application maps and pre-harvest yield prediction maps—to optimize inputs and reduce environmental runoff.
* **Regional & National Level:** Monitors complex transitions toward climate-smart agriculture (e.g., cover cropping, no-till, crop rotations). A featured case study demonstrates mapping **Integrated Crop-Livestock Systems (ICLS)** in Brazil using PlanetScope time-series imagery and deep neural networks (LSTM-FCN) to inform national land-use databases like MapBiomas.
* **Global Level:** Addresses global food security via initiatives like **ESA WorldCereal** (using the **Presto** geospatial foundation model) and the G20 **GEOGLAM Global Crop Monitor**, which synthesizes satellite data with expert consensus to issue early warnings.

---

### **5. Responsible AI & Future Directions**
* **Human-in-the-Loop:** While AI scales information, human expert judgment remains necessary to interpret outputs, evaluate uncertainty, and make high-stakes policy or humanitarian decisions.
* **Emerging Paradigms:** The field is shifting toward general-purpose **geospatial foundation models** (e.g., Presto, AlphaEarth embeddings) that learn representations across unlabeled data to streamline downstream fine-tuning.

---
---

### Key takeaways from today's lecture:

- Agriculture is both a cause and a casualty of climate change. It drives emissions through land-use change, livestock methane, and fertilizer N₂O, while being increasingly exposed to droughts, floods, and heat. Good AI systems have to account for both sides.

- Start from the decision, not the sensor or model. The scale of the decision (field, farm, regional, national, or global) determines the right data resolution, revisit frequency, and AI method. There's no one-size-fits-all setup.

- Earth observation scales monitoring; field data keeps it honest. Satellites give large-area, frequent, consistent coverage, but ground observations remain essential for calibration and validation. The two are complementary, not competing.

- Match the AI method to the question. Regression for yield and biomass, classification for crop type, segmentation for field delineation, object detection for counting, forecasting for yield and drought, anomaly detection for crop stress. The method should follow from the problem.

- The strongest models combine space and time. Many agricultural questions depend on how crops evolve, not just where they are. Complex systems like double/triple cropping and integrated crop-livestock systems genuinely need spatio-temporal models.

- Foundation models are reshaping the field. Geospatial foundation models (like Presto behind ESA WorldCereal, and AlphaEarth embeddings) learn general representations of the Earth from largely unlabeled data, cutting the need for scarce ground labels. That's especially valuable in data-scarce regions.

- Responsible AI means keeping humans in the loop. Models face geographic bias, limited transferability, climate non-stationarity, and rising uncertainty. AI should support expert judgment, not replace it, and the higher the stakes, the more that oversight matters.


Want to go further? The lecture pointed to some great open resources: Fields of the World (https://github.com/fieldsoftheworld/ftw-baselines), ESA WorldCereal (https://esa-worldcereal.org/en), and AlphaEarth embeddings (https://developers.google.com/earth-engine/datasets/catalog/GOOGLE_SATELLITE_EMBEDDING_V1_ANNUAL), plus tools like GEE (https://github.com/gee-community), Google Colab (https://colab.research.google.com/), and the CY-Bench crop-yield benchmark.

---
