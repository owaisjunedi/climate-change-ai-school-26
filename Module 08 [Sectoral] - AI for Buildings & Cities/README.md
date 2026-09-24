
---

### Key takeaways from today's lecture, from Dr. Batra’s talk:

- Buildings are a massive, measurable climate lever. They account for ~30% of global final energy and roughly a third of energy-related CO₂ once embodied/construction carbon is included — and unlike many sectors, they're already metered, making them a natural target for ML.

- The whole talk runs on one loop: Sense → Model → Decide → Verify. This template repeats across all four applications (energy disaggregation, demand forecasting/shifting, comfort-aware control, and low-carbon design search) — the question each time is whether the result survives a new building, the real grid, and real people.

- There's a fundamental trade-off between reach and resolution in data. Utility bills are cheap but too coarse; sub-metering gives ground truth but is expensive to install/maintain; smart meters are the useful middle ground — which is exactly why NILM (non-intrusive load monitoring) exists: to infer the rich appliance-level signal from one cheap aggregate meter.

- Accuracy isn't the same as impact. Low prediction error can still miss the events that matter (e.g., models with low MAE still missed most microwave events); real value comes from turning a model into a specific, actionable decision — e.g., splitting a fridge's load into baseline/defrost/usage pointed to fixes worth 23–26% of its energy.

- Match the model/method to the job, and prefer simple, robust baselines first. Persistence forecasts are hard to beat; gradient boosting won a major forecasting competition over deep learning; white/grey/black-box models suit design, control, and forecasting respectively; and rules should be tried before reinforcement learning, which only earns its complexity with a credible simulator, hard safety bounds, and monitoring.

----
----
----


### Key takeaways from today's lecture, from Dr Binyu Lei’s talk:

- AI augments, not replaces, planners. AI is framed as pattern recognition support for human judgement — a "cross-validation" aid — with planning values and human decision-making always coming first.

- The city-to-policy pipeline is: City → Data → Model → Insights → Policy → (feedback to City). Urban AI's value comes from moving systematically through this loop, not from any single step alone.

- AI plays four core roles in planning: prediction, simulation, interpretation, and intervention — estimating missing/future urban states, testing "what-if" scenarios, explaining why places behave differently, and supporting real-world decisions and feedback loops.

- Spatial data is the foundation, represented as points, lines, and polygons (vector) or continuous grids (raster). Concepts like distance, adjacency, connectivity, and neighborhood effects are central — geometry plus attributes are both needed for meaningful analysis, and scale must match the planning question.

- Data quality and bias matter as much as the models. Data reflects who/what gets measured and who has access to it (open vs. commercial data, ethical/legal constraints); combined with methods like computer vision, graph learning, and explainable AI, the goal is to help planners "ask better questions, see hidden relationships, and act with greater care."

---
