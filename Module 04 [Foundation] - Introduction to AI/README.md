### 📌 **Module Overview & Instructor Profile**
* **Module Title:** Module 4 (Foundation) — Introduction to AI.
* **Instructor:** **Tejumade Afonja** (Doctoral Researcher at CISPA Helmholtz Center for Information Security, Co-founder of TRI AI & AI Saturdays Lagos, General Chair of Deep Learning Indaba 2025, former Google DeepMind Student Researcher, and 2022 DSSG Fellow).
* **Material Source:** The slide deck was adapted from the *AI Climate Institute Pilot Workshop* with added classwork exercises.
* **Session Recording / Platform Link:** Hosted via **Zoom** video conferencing, which served as the virtual summer school webinar platform. \
Recording Link : https://us06web.zoom.us/rec/play/ZqWsAoyJ-75fIqqUt1P2k9UhoAQZfY-jkYSbMy6V1onVETL-DvrHulJTcxwuO4X0SGUoFbbXvHZOciT8.sMUy4axXOH7rN_FN


---

### 📖 **Core Topics & Detailed Technical Breakdown**

#### **1. Artificial Intelligence vs. Machine Learning Fundamentals**
* **Artificial Intelligence (AI):** Broadly defined as any computer system or algorithm capable of emulating human cognitive functions, such as problem-solving, decision-making, and learning from data.
* **Rule-Based Systems vs. Machine Learning (ML):**
  * **Rule-Based Systems:** Rely on explicit, hand-coded rules specified by humans. The slides illustrate this through an in-class exercise attempting to write geometric rules to detect handwritten digits (e.g., the digit "9"), which quickly fails when encountering variations in handwriting.
  * **Machine Learning:** Enables systems to automatically extract patterns from data without being explicitly programmed (Arthur Samuel, 1959).
* **Hierarchy of Fields:** AI forms the outer umbrella; **Machine Learning** is a subset using statistical methods; **Deep Learning** is a subset of ML using multi-layer neural networks; and **Data Science** is the cross-disciplinary domain extracting value from data.
* **When to Use ML:** ML is best suited when rules cannot be easily written down, representative data exists, errors are acceptable (*"All models are wrong, some are useful"* — George Box), and the pipeline is cost-effective.

---

#### **2. Machine Learning Paradigms & Model Taxonomy**
The lecture categorizes machine learning techniques across multiple dimensions:

* **By Learning Approach:**
  1. **Supervised Learning (Task-Driven):** Learns a function \\(f(X) \approx y\\) using labeled data.
     * **Regression:** Predicts continuous, real-valued outputs \\(y\\) (e.g., predicting September Arctic sea ice extent over time).
     * **Classification:** Predicts discrete categorical targets \\(y\\) (e.g., identifying super-emitter methane well sites or filtering email spam). Common algorithms include Logistic Regression, SVMs, Decision Trees/Random Forests, Naive Bayes, and Neural Networks.
  2. **Unsupervised Learning (Data-Driven):** Finds internal patterns in unlabeled data. Used for **clustering** (e.g., monitoring hydrogen fueling station performance), **dimension reduction (PCA)**, **anomaly detection**, and **synthetic data generation**.
  3. **Semi-Supervised Learning:** Combines a small set of labeled data with a large set of unlabeled data.
  4. **Reinforcement Learning (Reward-Driven):** Trains an agent to interact with an environment and discover an optimal control policy that maximizes cumulative reward over time (e.g., building energy optimization or satellite image pan/zoom control).

* **By Probability Distribution (Generative vs. Discriminative):**
  * **Discriminative Models:** Model the conditional probability \\(P(Y|X)\\) to learn decision boundaries that separate classes (e.g., classical classifiers).
  * **Generative Models (GenAI):** Model the joint probability distribution \\(P(X,Y)\\) to learn underlying data distributions and generate new content (text, images, synthetic energy profiles). 
  * *Example (GPT):* Large Language Models predict the next token given prior context; while powerful at scale, they require massive compute, can hallucinate, and rely on pattern interpolation rather than direct fact retrieval.

* **Advanced Climate-Relevant Paradigms:**
  * **Task-Specific vs. General-Purpose (Foundation) Models:** Comparing single-purpose single-modality models with broad multimodal models (e.g., Geospatial foundation models for land-use segmentation and change detection).
  * **Surrogate & Physics-Informed Modeling:** Using ML to approximate expensive physics simulations (e.g., fluid dynamics, temperature field forecasting).
  * **Interpretable vs. Explainable vs. Causal ML:** Distinguishing between transparent models (interpretable), post-hoc explanation techniques (explainable, e.g., SHAP/LIME), and causal models that identify true cause-and-effect relationships \\(X \to Y\\) rather than correlations.

---

#### **3. Data Pipeline & ML Development Workflow**
* **Importance of Data:** Data quality directly dictates model quality.
* **4-Step Data Preparation Pipeline:**
  1. **Define the Task:** Outline temporal and spatial constraints (e.g., short-term grid balancing vs. long-term site planning for renewables).
  2. **Select & Label Data:** Verify if labels exist or can be acquired.
  3. **Explore & Clean:** Remove duplicates/outliers, handle missing values via exclusion or imputation, and quality-assure labels.
  4. **Dataset Splitting:** Partition data into **Training** (learn parameters), **Validation** (tune hyperparameters/select models), and **Testing** (assess generalization on unseen data).
* **Overfitting & Cross-Validation:** Demonstrates how model complexity affects training vs. testing accuracy, introducing **\\(k\\)-fold cross-validation** to prevent overfitting.

---

#### **4. Mathematical Deep-Dive: Linear Regression Algorithm**
The final section provides a step-by-step mathematical formulation of Linear Regression:

1. **Model Formulation:**
   Assumes a linear relationship between features \\(X\\) and continuous label \\(y\\):
   \\[\hat{y} = w_0 + w_1 x_1 + w_2 x_2 + \dots + w_n x_n\\]
   Where \\(\hat{y}\\) is the predicted output, \\(w_0\\) is the bias (y-intercept), and \\(w_1 \dots w_n\\) are feature weights.

2. **Loss Function (Mean Squared Error - MSE):**
   Measures prediction error across \\(m\\) training samples:
   \\[\mathcal{L}(w) = \frac{1}{m} \sum_{i=1}^{m} \left(y_i - \hat{y}_i\right)^2\\]

3. **Optimization Strategies (Minimizing Loss):**
   * **Closed-Form Solution (Normal Equation):**
     \\[w = \left(X^T X\right)^{-1} X^T y\\]
     Directly computes exact optimal weights, but requires \\(X^T X\\) to be invertible and is computationally restricted to small datasets.
   * **Gradient Descent Optimization:**
     Iteratively updates weights in the direction of the negative gradient for large datasets:
     \\[w_j := w_j - \alpha \frac{\partial \mathcal{L}}{\partial w_j} \quad \text{where} \quad \frac{\partial \mathcal{L}}{\partial w_j} = -\frac{2}{m} \sum_{i=1}^{m} x_{ij} \left(y_i - \hat{y}_i\right)\\]
     Where \\(\alpha\\) represents the **learning rate hyperparameter**. The slides illustrate the trade-offs of learning rates: setting \\(\alpha\\) too small leads to slow convergence, while setting it too large causes overshooting of the loss minimum.

---
---

### Key takeaways from the lecture:

- What is AI and Machine Learning: AI is any system that lets a machine perform tasks we'd associate with human intelligence. Within AI, machine learning is the part that learns patterns from data rather than following hand-written rules. The classic distinction: rule-based systems do exactly what you tell them; ML figures it out from examples.

- ML Is a Tool, Not a Magic Fix: Not every problem needs machine learning. It works best when the rules are too complex to write manually, when you have good quality data, and when some margin of error is acceptable. A simple rule-based approach is often the better call for straightforward problems.

- Three Main Types of ML: Supervised learning trains on labeled data to predict outcomes like forecasting Arctic sea ice or flagging methane super-emitter sites. Unsupervised learning finds hidden structure in unlabeled data, useful for clustering energy usage patterns. Reinforcement learning teaches a model through rewards and penalties common in energy optimization and game playing.

- Generative vs. Discriminative Models: Discriminative models learn to classify or predict spam vs. not spam. Generative models learn the underlying distribution of data and can create new content: text, images, synthetic datasets. Both have very different use cases and trade-offs.

- Data Is Everything: The quality of your model is only as good as the quality of your data. Collecting, cleaning, and preparing data is not a side task; it consistently takes the most time in any real ML project. Always split data into training, validation, and test sets, and never evaluate on data the model has already seen.

- Overfitting: A model that performs well on training data but fails on new data has overfit; it memorized instead of learned. The fix is more data, simpler models, or k-fold cross-validation to get a more honest picture of real-world performance.

- Linear Regression: The model learns a line that best fits the data by minimizing a loss function, the gap between predictions and real values. Weights are updated through gradient descent, where the learning rate controls the step size. Too large and the model overshoots; too small and training crawls. This logic applies to nearly every ML model, not just linear regression.

- The Ethical Questions Don't Have Clean Answers: Two big ones came up: Who owns the data used to train AI? And is synthetic data truly safe to share? These are live debates with no universal answers, and as people working at the intersection of AI and climate, being aware of them matters just as much as understanding the math.

---
