
# Reference Guide: Machine Learning, Prompt Engineering & RAG for Climate Policy & ESG Analysis

---

## Part 1: Multi-Label SDG Classification & In-Context Learning (ICL)

Part 1 focuses on building, evaluating, and debugging Large Language Model (LLM) pipelines for text classification over the 17 United Nations Sustainable Development Goals (SDGs) using national climate policy disclosures.

### 1. Document-Level Group-Based Data Splitting (`make_new_splits`)
* **Problem & Data Leakage Risk:** Sentences within the same national policy report share distinct vocabulary, geographic entities, and writing styles. Splitting data randomly at the sentence level causes severe data leakage—the model memorizes country-specific phrasing and document provenance rather than learning generalized SDG semantic concepts.
* **Algorithmic Solution:** Group the dataset by unique document identifiers (`filename`) prior to performing split operations using `sklearn.model_selection.train_test_split`:
  \\[\text{Target condition: } D_{\text{train}} \cap D_{\text{val}} = \emptyset \quad \text{and} \quad D_{\text{train}} \cap D_{\text{test}} = \emptyset\\]
* **Split Ratios:** 60% Train, 20% Validation, 20% Test.

### 2. Few-Shot In-Context Learning Prompting (`in_context_prompt`)
* **Core Concept:** Rather than relying solely on zero-shot taxonomy descriptions, \\(N\\) demonstration examples (\\(x_i, y_i\\)) are sampled from \\(D_{\text{train}}\\) and dynamically injected into the prompt context window.
* **Prompt Structural Components:**
  1. **Taxonomy & System Instruction:** Top-level definitions for all 17 SDGs.
  2. **Demonstrations Block (`[BEGIN OF EXAMPLES]` ... `[END OF EXAMPLES]`):** \\(N\\) labeled demonstration pairs.
  3. **Target Test Example:** Formatted with `test_input_only=True` (omitting the goal label).
  4. **Completion Cue (`goal:`):** Directs the LLM to output only the target goal index.

### 3. Multi-Label Evaluation & Aggregation Metrics (`calculate_accuracy` & `most_common`)
* **Multi-Label Evaluation:** In policy analysis, a single text snippet often aligns with multiple SDGs simultaneously (e.g., clean energy projects impact both **SDG 7** and **SDG 13**).
  \\[\text{Accuracy} = \frac{1}{N} \sum_{i=1}^{N} \mathbb{I}(\hat{y}_i \in T_i)\\]
  Where \\(T_i\\) is the set of ground-truth target goal labels and \\(\hat{y}_i\\) is the model's top predicted goal.
* **Majority Voting Aggregation (`most_common`):** Computes the mode element \\(\max(S, \text{key}=\text{count})\\) for self-consistency sampling across multiple LLM runs or annotator consensus.

### 4. End-to-End Evaluation Pipeline (`run_eval`)
* **Text Grouping:** Uses `df_test.groupby(obs_column)` to aggregate duplicate text snippets and build multi-label target arrays.
* **Per-Sample Dynamic ICL:** Samples a fresh set of \\(N\\) demonstration examples from \\(D_{\text{train}}\\) for every test instance inside the evaluation loop, eliminating demonstration-selection bias.

### 5. Diagnostics, Output Parsing, and Baselines
* **Regex Output Filtering:** Employs regex matching (`re.search(r'\b(1|)\b', response)`) to strip conversational preamble and extract valid integer predictions in \\(\{1, \dots, 17\}\\).
* **Random Uniform Baseline Simulation (`plot_random_histogram`):**
  - Uses Monte Carlo simulation (1,000 trials) uniform sampling over 17 classes.
  - Theoretical single-label baseline: \\(\frac{1}{17} \approx 5.88\%\\).
  - Empirical multi-label baseline: \\(\approx 10\% - 15\%\\) due to multi-target hit probability.
  - Model performance: \\(\approx 30\%\\) accuracy (\\(\sim 2.5\times\\) over random chance).

---

## Part 2: Advanced Prompt Engineering & LlamaIndex RAG Pipeline

Part 2 transitions into advanced prompt engineering (role prompting, structured schema constraints, critical reflection) and implements a Retrieval-Augmented Generation (RAG) system using LlamaIndex over corporate sustainability reports.

### 1. Iterative Prompt Engineering Strategies
* **Role Prompting / Persona Assignment:** Setting the system persona to a *"Senior ESG Analyst"* to enforce an analytical, objective tone.
* **Delimiters:** Using delimiters (`<...>` and `-----`) to insulate instructions from untrusted source texts.
* **Output Format Control:** Instructing models to produce structured output formats:
  - Bulleted lists of positive vs. negative practices.
  - Strict JSON schemas (`{"positive_aspects": [...], "negative_aspects": [...]}`).
* **Critical Reflection & Adversarial Red-Teaming:** Prompting the model to contrast corporate self-claims (e.g., 2008 UN PRI signatory) against independent third-party evidence (\$25M SEC regulatory settlement, whistleblower reports) to evaluate greenwashing risk.

### 2. LlamaIndex RAG System Architecture
* **Document Ingestion & Page-Level Auditability (`SimpleDirectoryReader`, `PyMuPDFReader`):** Loads PDF pages while preserving metadata (`page_label`, `page_number`, `file_name`) on every node for exact line-item citation and auditability.
* **Vector Indexing & Retrieval (`VectorStoreIndex`, `VectorIndexRetriever`):** Generates dense vector embeddings and retrieves the top-\\(K\\) (\\(K=5\\)) nearest-neighbor document nodes.

### 3. Semantic Chunking Strategies for Tabular Data (`SentenceSplitter`)
* **Tabular Chunking Trade-offs:** Corporate climate disclosures place Scope 1, Scope 2, and Scope 3 emissions inventories inside multi-column tables.
* **Chunk Size Tuning:**
  - `CHUNK_SIZE = 200`: Works well for standard prose, but risks splitting tabular data across chunk boundaries (separating row headers from numerical values).
  - `CHUNK_SIZE = 400`: Essential for financial and emissions tables to keep headers, row labels, numerical figures, and units intact within a single node.
  - `CHUNK_OVERLAP = 50`: Retains boundary context across adjacent nodes.

### 4. Embedding Models (Commercial vs. Free Open-Source)
* **Commercial:** `OpenAIEmbedding(model="text-embedding-3-small")`.
* **Free / Local Open-Source:** `HuggingFaceEmbedding(model_name="BAAI/bge-small-en-v1.5")` via `llama-index-embeddings-huggingface` running locally on CPU/GPU without API key dependencies or usage limits.

### 5. Citation-Enforced RAG Prompting & Robust JSON Parsing
* **Prompt Template Design (`prompt_template`):** Injects retrieved text blocks tagged with `PAGE X:` and directs the LLM to output a JSON object containing:
  - `ANSWER`: Narrative response starting with binary verdicts (`[[YES]]`/`[[NO]]`) or specific numbers with units.
  - `SOURCE_PAGES`: List of exact page numbers cited.
* **Robust JSON Handling (`visualize_answer`):** To avoid `JSONDecodeError: Extra data` when LLMs append commentary after the closing brace `}`, regex extraction (`re.search(r'\{.*\}', answer, re.DOTALL)`) isolates and parses strictly the `{ ... }` JSON block.

---

### Summary of Utility Functions

| Function Name | Primary Role | Key Technology |
| :--- | :--- | :--- |
| `make_new_splits` | Group-based split by document `filename` | `scikit-learn` |
| `in_context_prompt` | Dynamic \\(N\\)-shot ICL prompt generation | `pandas` |
| `calculate_accuracy` | Multi-label hit evaluation metric | Python stdlib |
| `run_eval` | End-to-end evaluation pipeline over test set | `pandas`, Transformers / OpenAI |
| `createRetriever` | LlamaIndex document ingestion & vector index creation | `llama-index`, `PyMuPDF` |
| `createSources` | Top-\\(K\\) vector similarity retrieval & context injection | `llama-index` |
| `visualize_answer` | Robust JSON parsing & HTML citation rendering | `re`, `json`, `IPython` |

---
