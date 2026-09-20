### Overview of Module 3: AI for Public Policy & Social Sciences

Module 3 of the Climate Change AI (CCAI) Virtual Summer School explores how artificial intelligence intersects with **public policy** and the **social sciences**. While physical climate science models the earth system, this module addresses the human, institutional, and socio-economic dimensions of climate action—examining how policies are designed, how society responds, and how AI can responsibly accelerate a just transition.

---

### Part A: AI for Public Policy (Dr. Carlos Rodriguez-Pardo)

Climate policy analysis aims to compare mitigation, adaptation, and loss-and-damage options, evaluate trade-offs, design policy instruments (e.g., carbon taxes, subsidies), and make decisions under deep uncertainty. AI enters across every stage of the policy cycle—from problem definition and formulation to implementation and evaluation.

#### 1. The 4-Part Framework for AI in Policy
* **Part 1: Foundations:** Defines the core goals of climate policy analysis, comparing policy levers across international, national, regional, and private scales.
* **Part 2: Measuring at Policy-Relevant Resolutions:**
  * **Policy Corpora & Literature:** Uses Natural Language Processing (NLP) to map hundreds of thousands of climate policy documents and scientific papers, creating harmonized cross-country policy datasets (e.g., IPCC-aligned panels) and evidence maps.
  * **High-Resolution Monitoring:** Combines computer vision, remote sensing, and subnational ML models to measure urban greenhouse gas emissions and air quality.
  * **Earth Foundation Models & Geospatial Embeddings:** Leverages foundation models (e.g., SatCLIP, GeoCLIP, Clay, AlphaEarth) to learn planetary representations once and reuse them across city-block, regional, and global adaptation tasks.
* **Part 3: Modeling Futures & Designing Policy Options:**
  * Uses **Integrated Assessment Model (IAM) emulators**, neural Partial Differential Equation (PDE) solvers, and Reinforcement Learning (RL) / multi-agent RL to simulate socio-economic trajectories and discover robust policies under deep uncertainty.
* **Part 4: Evaluation & Causal Machine Learning:**
  * Evaluates whether policies actually worked using **Causal ML** techniques (e.g., double machine learning extending synthetic controls, difference-in-differences, and instrumental variables) to isolate true policy impacts from confounding factors.

#### 2. The Deployment Gap & Open Problems
* **The Deployment Gap:** Thousands of academic papers produce ML models, but very few survive pilot stages or achieve institutional adoption.
* **Bridging the Gap:** Successfully deploying AI in public policy requires benchmarking tools for **policy usefulness rather than just predictive accuracy**, quantifying uncertainty in decision-relevant terms, and co-designing tools directly with affected communities and institutions.
* **Core Takeaway:** Integration across hazards, impacts, and socio-economic responses is the true frontier. Research should start from **policy-relevant questions**, not raw model capabilities.

---

### Part B: AI for Social Sciences (Dr. Mary Sanford)

Social science disciplines—including political science, economics, psychology, sociology, and communications—provide the critical foundation for establishing the **social and political feasibility** of the climate transition.

#### 1. Public Attitudes & Feasibility
* Large multinational surveys show widespread global public support for climate action. However, translating broad support into behavioral change and policy adoption requires diagnosing barriers, understanding organizational dynamics, and learning from past interventions.
* Social research is necessary to ensure technological advancements (such as AI or green tech) reach their full potential in real-world human systems.

#### 2. Responsible AI Principles ("Wisely, Not Widely")
* **Tool vs. Objective:** AI should be treated as a tool to serve social science objectives, keeping the focus on the "nail" (the research/policy goal) rather than the "hammer" (the AI method).
* **Validation & Auditing:** Large Language Models (LLMs) and automated tools must be audited for training biases, data coverage gaps (which are often thinnest where population vulnerability is highest), and validated before deployment.
* **Human-in-the-Loop:** Optimizing human-AI teamwork and keeping human judgment central is essential when addressing complex, value-laden social challenges.

---

### Summary Takeaway
While AI offers high-dimensional modeling, causal inference, and automated evidence mapping, **data and predictive accuracy alone cannot resolve political trade-offs or define social values**. Successful application requires interdisciplinary integration, human-in-the-loop validation, and co-design with decision-makers.

---

---

### Key takeaways from the last lecture:

- Begin with the Question, Not the Model: The most critical rule is to start with policy-relevant problems rather than using a specific dataset or model's capabilities.

- Integration is the New Frontier: The major restriction in climate policy is rarely solely "predictive accuracy". The primary obstacle is implementing AI findings at many sizes, institutions, and stages of the policy cycle.

- Measuring is Never Neutral: Very high-resolution data might give the impression of "false precision". Because modelling tends to be less accurate in the weakest areas where data is thinnest, we must remain mindful of data availability biases.

- Consider the "Sim-to-Real" Gap: A policy that performs well in an AI emulator (such as a Reinforcement Learning environment) may be rejected by a human policymaker if it violates social acceptability, equity, or legal limitations.

- AI Has a Footprint: We must consider the environmental impact of the AI tools themselves, particularly the energy and water used during compute-intensive training and inference.

- "Wisely, Not Widely" refers to the strategic application of AI. Because of its environmental impact, such as the estimated 1 billion litres of water used for GPT-5 training, we must defend its use for each project.

- Concentrate on the "Nail," not the "Hammer": Do not begin with a model and hunt for a problem. Begin with a critical social science objective (the nail) and apply AI (the hammer) only when it is the most effective tool for the work at hand.

- The Human-in-the-Loop is Non-Negotiable: Since LLMs are liable to misclassification bias and "Potemkin understanding," researchers must develop rigorous validation procedures rather than just applying models.

- Defend the Social Science Foundation: We must oppose the "deskilling" tendency, in which AI takes the place of the in-depth, subjective knowledge obtained through theory development and human-led qualitative interviews.

- Audit for errors or Biases: Make that the training data is appropriate for the context at all times. AI has the potential to replicate social identification biases (gender, etc.), which, if left unchecked, could compromise the credibility of climate research.

---
---


### Tutorial Walkthrough Video: 

#### NLP Models for Climate Policy Analysis — Evidence Synthesis

Research Synthesis using NLP in the Field of Climate Change: Part 1 - https://www.youtube.com/watch?v=KEScm0s7RCs

#### NLP Models for Climate Policy Analysis Part 2: Prompts for Sustainable Development Goals

Research Synthesis using NLP in the Field of Climate Change: Part 2 - https://www.youtube.com/watch?v=pPDsLQIvWMM

