## Optional Lecture-Related Readings

### Highlighted resources:

- But what is a Neural Network? (3Blue1Brown) <br/> https://www.3blue1brown.com/lessons/neural-networks/

- Machine Learning Crash Course (Google) <br/> https://developers.google.com/machine-learning/crash-course

- Machine Learning Glossary (Google) <br/> https://developers.google.com/machine-learning/glossary

- The Values Encoded in Machine Learning Research (Birhane et al., 2021) <br/> https://arxiv.org/abs/2106.15590


### Relevant Courses :

- Practical Data Science course: https://www.datasciencecourse.org/

- TRI AI Saturdays Cohort 8 Lectures: https://www.youtube.com/playlist?list=PLD0HH4Qq3rceefnTGs9vD2y32SeQpjmPI

- Google DeepMind AI Research Foundations Course 1: https://www.skills.google/course_templates/1341


### Additional resources:

 - Introduction to Python & ML - CCAI Virtual Summer School 2026  <br/>
 https://docs.google.com/document/u/1/d/1-0RN9NRXJHrHlFg6UBgfGL2fppHHeORVuiBjrllKsm0/edit?tab=t.n3zkn6db89kc


---
---
---

Here is an in-depth breakdown of these above mentioned resources, explaining what each contains, how the technical mechanics work, and how they fit together, followed by a unified synopsis of the entire set.

---

### 1. **"But what is a Neural Network?" | 3Blue1Brown**
* **Type:** Educational Video / Lesson (Grant Sanderson)
* **Core Topic:** Mathematical structure and visual intuition of artificial neural networks.
* **In-Depth Explanation:**
  * **Network Architecture:** Uses handwritten digit recognition (MNIST, \\(28 \times 28\\) pixel grayscale images) as a concrete example. The input layer consists of **784 input neurons** (one per pixel, holding activation values from 0.0 for black to 1.0 for white), leading through **hidden layers** (e.g., two layers of 16 neurons each) to an **output layer of 10 neurons** representing digits 0–9.
  * **Parameters & Computation:** Information passes between layers via weighted connections (\\(W\\)) and biases (\\(b\\)). Each neuron calculates a weighted sum of activations from the previous layer, adds a bias, and passes the result through an activation function:
    \\[a^{(l)} = \sigma(W a^{(l-1)} + b)\\]
    The network in this example contains **13,002 total tweakable weights and biases**.
  * **Activation Functions (Sigmoid vs. ReLU):** Explains that traditional **Sigmoid** functions squish weighted sums between 0 and 1, but flatten out at extreme values, causing gradients to vanish and making training slow. Modern deep networks rely on **ReLU (Rectified Linear Unit)**—defined as \\(\max(0, x)\\)—which avoids flattening for positive inputs, maintaining constant gradients that enable efficient backpropagation across many layers.
  * **Hierarchy of Abstraction:** Shows how hidden layers theoretically break complex visual tasks into bite-sized subcomponents—from raw pixels to edge detectors, to loops and line segments, and finally to digit classifications.

---

### 2. **Google DeepMind: 01 Build Your Own Small Language Model | Google Skills**
* **Type:** Practical Hands-on Course (Google Skills / DeepMind)
* **Core Topic:** Designing, training, evaluating, and applying Small Language Models (SLMs).
* **In-Depth Explanation:**
  * **Language Modeling Principles:** Teaches language modeling as a probabilistic next-word prediction problem.
  * **Architectural Comparisons:** Contrasts classical statistical **N-Gram models** with modern **Transformer-based language models**.
  * **Training Pipeline:** Guides learners through the ML development cycle—dataset preparation, tokenization, model training, and performance evaluation.
  * **Ethical Frameworks & Application:** Incorporates ethical perspectives (such as local cultural lenses, the Ubuntu framework, and moral dilemmas like the trolley problem in AI decision-making) alongside developing concrete problem statements for real-world deployment.

---

### 3. **Introduction to Python & ML - CCAI Virtual Summer School 2026**
* **Type:** Climate Change AI (CCAI) Curriculum & Resource Roadmap
* **Core Topic:** Applying machine learning paradigms to climate mitigation, adaptation, and environmental science.
* **In-Depth Explanation:**
  * **Core Stack & Tools:** Details essential Python libraries for data processing and modeling, including **Pandas** (tabular data), **GeoPandas** (shapefiles/GeoTIFFs), **NumPy** (array math), **Scikit-learn** (classical ML), **PyTorch/TensorFlow** (deep learning), and **Matplotlib** (visualization).
  * **Specialized ML Paradigms for Climate Applications:**
    * **Geospatial AI & Vision:** Applying Convolutional Neural Networks (CNNs) and Vision Transformers to satellite imagery and spatial rasters.
    * **Natural Language Processing (NLP):** Using tokenization, embeddings, LSTMs, and Transformers to analyze climate policy documents, corporate disclosures, and environmental reports.
    * **Physics-Informed Machine Learning (PINNs):** Embedding physical laws (such as differential equations and energy conservation principles) directly into neural network loss functions. This significantly reduces required training data, prevents physically impossible predictions, and ensures model predictions conform to real-world physical constraints in weather and climate modeling.
    * **Interpretability & Explainability (XAI):** Utilizing tools like **SHAP**, **LIME**, activation maps, and saliency maps to explain high-stakes model decisions (e.g., power grid operations or disaster management) to human operators.

---

### 4. **Machine Learning Glossary | Google for Developers**
* **Type:** Technical Reference & Dictionary
* **Core Topic:** Authoritative definitions for key concepts across classical machine learning, deep learning, generative AI, responsible AI, and agentic systems.
* **In-Depth Explanation:**
  * **Evaluation Metrics & Losses:** Defines key metrics including Accuracy, Precision, Recall, F1 Score, AUC-ROC, Log Loss, Mean Squared Error (MSE), Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE).
  * **Model Architectures:** Details Perceptrons, Dense Layers, Convolutional Neural Networks (convolutions, pooling), Recurrent Neural Networks (RNNs, LSTMs), Transformers (self-attention, multi-head attention), Autoencoders, GANs, Decision Trees, and Random Forests (bagging, boosting).
  * **Generative AI & LLMs:** Covers Zero-Shot/Few-Shot Prompting, Chain-of-Thought, Fine-Tuning, Low-Rank Adaptability (LoRA), Model Distillation, Hallucinations, Groundedness, Retrieval-Augmented Generation (RAG), ROUGE, BLEU, Perplexity, and Temperature.
  * **Responsible AI & Fairness:** Breaks down Demographic Parity, Equalized Odds, Counterfactual Fairness, Disparate Impact, Proxy Attributes, and Historical/Selection Biases.
  * **Agentic AI & Reinforcement Learning:** Explains autonomous agents, the agentic loop (**Reason \\(\rightarrow\\) Act \\(\rightarrow\\) Feedback**), Action Spaces, Q-Learning, the Bellman Equation, and Markov Decision Processes.

---

### 5. **Machine Learning | Google for Developers (ML Crash Course)**
* **Type:** Practical Interactive Course Structure
* **Core Topic:** Google’s foundational machine learning curriculum.
* **In-Depth Explanation:**
  * **Supervised Learning Fundamentals:** Covers Linear Regression, Logistic Regression, Binary/Multi-Class Classification, Decision Boundaries, and Confusion Matrices.
  * **Data Operations:** Explores feature engineering for numerical data (normalization, clipping, z-score scaling) and categorical data (one-hot encoding, feature crosses, hashing), alongside dataset partitioning (train/val/test) to diagnose overfitting.
  * **Advanced Architecture & Deployment:** Introduces neural network hidden layers, dense embeddings, Transformer architecture for LLMs, production pipeline best practices, AutoML, and ML fairness auditing.

---

### 6. **Practical Data Science**
* **Type:** Technical Capability Taxonomy
* **Core Topic:** Structural breakdown of full-stack data science requirements.
* **In-Depth Explanation:**
  * **Data Ingestion & Management:** Ingesting structured/unstructured sources using relational models, time series analysis, graph processing, NLP, and Geographic Information Systems (GIS).
  * **Statistical Modeling:** Hypothesis testing, experimental design, and statistical data analysis.
  * **Advanced Modeling:** Applying kernel methods, ensemble boosting, deep learning, anomaly detection, matrix factorization (for recommendation systems), and probabilistic modeling.

---

### 7. **"The Values Encoded in Machine Learning Research" (Birhane et al., 2021)**
* **Type:** Empirical Research Paper (arXiv:2106.15590)
* **Core Topic:** Critical analysis of institutional and societal values encoded in top-tier machine learning research.
* **In-Depth Explanation:**
  * Analyzes a dataset of papers from top ML conferences (such as NeurIPS and ICML).
  * Demonstrates how mainstream ML research systematically prioritizes **quantitative benchmark performance**, **computational scale**, and **technical efficiency** over human safety, ethical considerations, and real-world societal impact.
  * Highlights how technical choices in AI research reflect commercial interests, institutional power dynamics, and implicit normative assumptions about progress.

---

### 🌐 **Unified Synopsis**

This collection of resources forms an **end-to-end curriculum bridging fundamental AI engineering with climate domain applications and societal responsibility**:

1. **Foundations & Mathematical Intuition:** The **3Blue1Brown** lesson and **Google MLCC** build deep visual and mathematical intuition for how neural networks transform raw features into representations through matrix multiplication, biases, and non-linear activation functions.
2. **Full-Stack Engineering & Practical Workflows:** The **Google ML Glossary** and **Practical Data Science** guides establish the technical lexicon and engineering pipeline—spanning feature preprocessing (scaling, feature crosses), model selection, evaluation metrics, and advanced architectures (Transformers, Autoencoders, Agents).
3. **Generative AI & LLMs:** **Google DeepMind's SLM course** and the glossary’s Generative AI modules show how to build, fine-tune (via LoRA/Distillation), ground (via RAG), and evaluate small, device-friendly language models.
4. **Climate Domain Integration:** The **Climate Change AI (CCAI)** roadmap operationalizes these techniques for real-world environmental challenges—combining Geospatial AI, NLP for policy, Physics-Informed Neural Networks (PINNs), and Explainable AI (XAI) for critical infrastructure decision-making.
5. **Responsible AI & Critical Reflection:** Finally, the **Birhane et al. paper** and Google's ML Fairness guides provide the essential critical lens, challenging developers to look beyond pure benchmark optimization and evaluate the institutional values, ethical trade-offs, and social impacts encoded in AI models.

---

