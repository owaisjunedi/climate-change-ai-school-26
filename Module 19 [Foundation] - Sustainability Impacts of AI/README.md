### Key takeaways from today's lecture:





- Inventory Analysis of Carbon Emissions and Water Usage: emissions are measured by GHG Protocol, a global standardized framework that categorizes emissions as Scope 1, 2, or 3. This framework has also been extended to measure water impact.



- Operational vs. embodied emissions: Operational emissions from energy consumed during ML computation is generally significantly higher than embodied emissions from the production and end-of-life of ML hardware. Within operational emissions, whether emissions from training or inference is greater depends on the use case, but large AI providers (e.g., Meta and Google) have reported higher inference emissions than training emissions.



- Jevon’s Paradox: The increased efficiency of modern AI services is largely outweighed by usage growth, resulting to net higher emissions despite efficiency gains.



- Heterogeneity of AI emissions by task: Different AI inference tasks have widely different energy needs, ranging up to 4 orders of magnitude between text summarization or question answering (less energy consumption) and image generation (more energy consumption).



- Frugal AI: There are many strategies to reduce emissions from solving a given task, such as using task-specific smaller models, task-specific data that requires less training, and local/edge models that can run on lower-power hardware.



- Energy sources: Electricity generation for data centers currently comes from primarily natural gas and renewables, with coal and nuclear constituting a smaller fraction of power. This trend is expected to continue. We cannot count on renewables alone (“greening the grid”) to reduce emissions from data centers.



- Impacts beyond emissions: AI usage is also driving significant usage of raw materials (for fabricating chips and building data centers) and water (for cooling power plants and for cooling data centers). The indirect water usage from data centers (mostly for cooling power plants that supply electricity to the data centers) generally outweighs direct water usage (for cooling the data centers themselves).



- Application-focused analysis: AI impacts on emissions must account for applications. Estimates of emissions savings potential of AI are generally unreliable and likely overstating the positive impacts. On the other hand, AI is actively being used to accelerate emissions-intensive industries such as oil and gas applications.



- System-level impacts of AI applications include rebound and lock-in effects, increased societal consumption, misinformation and polarization, and induced societal power shifts.



- “GenAI Fallacy:” Tech companies often promote “AI for climate” applications to justify the environmental impacts of their large models, but this is misleading. Most AI use across society is in non-climate applications. Furthermore, we can have AI-for-climate progress without large computing-related energy costs.



- Regulatory requirements: Regulations for addressing the sustainability impacts of AI are geographically fragmented. For example, the EU has enacted the EU AI Act which requires disclosure of energy used during model development. However, it does not require disclosure for model inference. The US has proposed (but not enacted) related legislation.

---
