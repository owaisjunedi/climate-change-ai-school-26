**Module 16: Shaping Your AI-for-Climate Project in Practice** (presented by **Dina Machuve, PhD**) provides a practical, end-to-end framework for designing, deploying, and evaluating AI projects focused on climate mitigation and adaptation.

The module moves beyond theoretical model building to examine real-world technology readiness, operational pipelines, impact metrics, and equity dynamics.

---

### **1. Assessing AI Fit and Technology Readiness**
* **ML is Only One Layer:** Machine learning models are just a single component within a larger system comprising data infrastructure/governance, operational pipelines, and human workflow integration.
* **Asking "Is AI the Right Tool?":** Before selecting AI, teams must evaluate data quality, operational compatibility, stakeholder acceptance, and whether simpler rule-based approaches can achieve similar outcomes.
  * **When AI adds value:** Complex high-dimensional pattern recognition, scalability needs, and real-time inference requirements.
  * **When simpler methods suffice:** Rule-based logic, limited data availability, or high-stakes environments where explainability is non-negotiable.
* **Technology Readiness Levels (TRL):**
  * **Deployable Now:** Satellite-based deforestation tracking, energy load forecasting, carbon stock estimation, regional crop yield modeling, and emissions inventory automation.
  * **Requires Further Innovation:** Hyper-local microclimate forecasting, grid-scale renewable balancing agents, autonomous wildfire suppression, and cross-sectoral optimization cascades.
* **Methodological Trade-offs:** Algorithmic choices trade off specific priorities (e.g., Random Forest/XGBoost trade speed for interpretability; CNNs trade accuracy for complexity; GANs/Autoencoders trade spatial resolution for compute).

---

### **2. Data Pipelines and Deployment Pathways**
The project lifecycle follows a 6-stage pipeline built with continuous, non-linear feedback loops to discover misalignments early:
1. **Climate Challenge Identification:** Scoping problem definitions and assessing stakeholder needs.
2. **ML Task Definition:** Translating real-world problems into formal prediction, classification, or optimal control tasks.
3. **Method Development:** Model training, validation, feature engineering, and handling non-stationary climate conditions.
4. **Piloting & Testing:** Limited rollouts measuring usability and early performance signals.
5. **Scaling & Deployment:** Production rollout with full infrastructure and operational support.
6. **Monitoring & Maintenance:** Performance tracking, handling data drift, and iterative updates.

---

### **3. Impact Assessment and Metrics**
* **Defining Outcomes First:** Metrics must follow a validated causal chain from desired outcomes to measurable proxies ("Easy indicators \\(\neq\\) Meaningful indicators").
* **Direct vs. Inferred Measurements:** Easily measured direct metrics (e.g., grid electricity use or satellite vegetation indices) contrast with latent variables requiring modeling (e.g., household appliance efficiency or below-canopy biodiversity). Unmeasured variables accumulate bias over time if ignored.
* **Short-Term vs. Long-Term Indicators:** Short-term operational indicators (adoption rates, model accuracy) are tracked continuously, whereas long-term systemic impacts (emissions reductions, climate resilience) involve higher attribution difficulty and require longer multi-year evaluations.

---

### **4. Stakeholders, Power Dynamics, and Sustainability**
* **Stakeholder Categorization:** Projects must categorize stakeholders into **Shapers** (regulators/funders), **Users** (operators/frontline workers), **Affected Parties** (indirectly impacted communities), and **Opponents** (those bearing concentrated losses).
* **Moving Beyond Tokenism:** Using frameworks like *Arnstein’s Ladder of Citizen Participation*, projects should transition from one-way informing or consulting toward true power transfer (partnerships, delegated authority, and citizen control).
* **Governance & Control Questions:** Projects must explicitly define data sovereignty (who owns raw geo-location data?), model weight access, compute control, and feature roadmap priorities.
* **Long-Term Sustainability:** Demands economic viability beyond initial pilot funding, institutional ownership, local expertise development, and clear exit strategies.

---

### **5. Case Study: Coffee Farming in Tanzania & EUDR Compliance**
* **Context:** Tanzania is Africa's 4th largest coffee producer, with 90% of exports produced by 450,000 smallholder families.
* **Regulatory Driver (EUDR):** The EU Deforestation Regulation requires traceable, deforestation-free supply chains for coffee entering the EU market (which accounts for 40% of Tanzanian coffee exports).
* **The Gap:** National central registries handle farm geo-mapping for compliance, but registration alone does not help smallholders adapt to escalating climate risks.
* **AI Solutions & Value-Add:**
  * **Deforestation Monitoring:** ChangeNet / U-Net satellite vision models for real-time compliance.
  * **Advisory & Risk Tools:** LSTM/Prophet yield forecasting, Random Forest disease/frost risk alerts delivered via SMS/USSD, RL harvest timing advisors, and carbon sequestration estimators.
* **Critical Ethical Considerations:** Preventing data extraction that serves export compliance while leaving farmers without actionable benefits, avoiding connectivity exclusion via offline-first design, and ensuring farmers act as co-developers rather than passive data sources.

---
---
---

### Key takeaways from today's lecture:

1. AI is only one piece of the system — not the whole solution. <br/>
The model is just one layer. Data infrastructure/governance and deployment/human workflow integration matter just as much. Real impact comes from all three layers working together, not model accuracy alone.

2. Not every climate problem needs AI — assess fit before building. <br/>
Before reaching for AI, ask the fit questions first: Is there enough quality data? Do operational constraints allow it? Will stakeholders actually trust the outputs? Could a simpler method do the job? And know the difference between what's deployable now (deforestation monitoring, yield prediction) and what still needs real innovation (autonomous wildfire suppression).

3. Deployment is a loop, not a line. <br/>
The pipeline (challenge → task definition → modeling → piloting → scaling → monitoring) only works when each stage feeds back into the ones before it. Pilot in one district, gather real feedback, then iterate before scaling. Deploying everywhere at once is what turns a promising model into a brittle rollout.

4. Easy-to-measure metrics aren't the same as meaningful ones. <br/>
Start from the outcome you actually want (eg. reduced emissions, real resilience) and work backward to find genuine proxies for it, instead of defaulting to whatever's easiest to count (alerts sent, model accuracy, user numbers). Short-term metrics matter, but the real climate impact shows up in the long-term, verified outcomes.

5. Power and data ownership determine who actually benefits. <br/>
Who owns the data, who controls the infrastructure, who bears the costs, and who actually gets a say (not just a consultation) determines whether a project helps the people it's meant for, or just extracts their data for someone else's compliance requirement. Treating farmers (or any affected community) as co-developers, not data sources, is what moves a project from tokenism toward genuine shared power.

---

