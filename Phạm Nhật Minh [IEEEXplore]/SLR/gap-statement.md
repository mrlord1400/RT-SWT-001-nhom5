# Gap Statement - Automated Test Generation using LLMs (Evidence Table: N = 8 papers)

## Các khoảng trống phát hiện

### GAP-T (Technology): Lack of local multi-agent or ensemble model synchronization for multi-tier test artifact generation.
* **Mô tả:** The current literature primarily relies on either single-model proprietary APIs or isolated local deployments, failing to combine the benefits of local data privacy with multi-model cooperative frameworks (e.g., combining specialized code-generation models and RAG-driven orchestrators) to generate end-to-end multi-tier artifacts (e.g., generating requirements, structural models, and executable code simultaneously).
* **Bằng chứng (Cột Tool/LLM):** * **Proprietary API Reliance:** The most recent high-performing studies in 2025, such as **Paper 1** (Nettur et al., 2025) and **Paper 3** (Rosenbach et al., 2025), exclusively rely on centralized, proprietary models like GPT-4o or GPT-4-Turbo via OpenAI APIs. This limits their applicability in data-sensitive corporate environments.
    * **Isolated Local Deployments:** While **Paper 2** (Fonseca et al., 2025) and **Paper 5** (Jagielski et al., 2025) utilize local models via Ollama (DeepSeek-R1, DeepSeek-Coder-V2, Gemma3:1b), they deploy them in isolated frameworks (e.g., ATOMIC) without testing cross-model consensus architectures. 
    * **Ensemble limitations:** Conversely, **Paper 4** (Sisomboon et al., 2026) demonstrates that an ensemble framework achieves the highest test coverage (96.9%), yet their configuration is entirely reliant on commercial/cloud APIs (Claude, ChatGPT, Gemini, Qwen, Mistral). 
    * **Rule-based vs LLM isolation:** **Paper 6** (Jang & Kim, 2025) uses customized traditional NLP tools (Mecab-ko, Exobrain API, KRA) to generate complex structural artifacts (C3Tree, Cause-Effect graphs) but notes that general LLMs like ChatGPT and Claude perform poorly on logic conversion when used alone. No paper has yet bridged the gap by deploying a synchronized, local multi-agent ensemble that mirrors the logic processing of traditional architectures with the adaptability of modern code-LLMs.

---

### GAP-M (Metric): Absence of holistic, multi-dimensional validation metrics spanning requirement coverage, semantic alignment, and execution sustainability.
* **Mô tả:** Evaluation metrics in current research are heavily siloed. Studies focus heavily on syntactic/compilation validity or isolated execution counts, completely omitting the dual-validation of whether the generated tests accurately cover the original requirements (*Requirement Coverage*) without introducing technical debt or fragile test scripts (*Execution Sustainability*).
* **Bằng chứng (Cột Metric & Hạn chế tự nêu):**
    * **Paper 1** (Nettur et al., 2025) evaluates code completeness and runtime accuracy (achieving 95%-100% accuracy) but explicitly lists the ***exclusion of requirement coverage metrics*** as a primary limitation in its self-stated limitations column.
    * **Paper 3** (Rosenbach et al., 2025) focuses purely on exploration scale and unique GUI bug detection accuracy, but completely ***lacks an empirical baseline against manual testing*** or requirements mapping.
    * **Paper 4** (Sisomboon et al., 2026) evaluates requirement-driven testing coverage and model classification quality, but its metrics are limited to textual test case responses and ***do not measure the physical execution success, compilation rates, or code quality*** of the scripts.
    * **Paper 8** (Ferreira et al., 2025) measures Gherkin-to-script semantic relevance and user acceptance, but relies heavily on subjective developer surveys which are subject to ***potential feedback bias*** over tracking instances.

---

### GAP-D (Dataset): Critical domain restriction and dataset scale constraints in real-world application testing.
* **Mô tả:** The empirical validation of existing LLM test generation frameworks is heavily constrained by small sample sizes, narrow business domains, or single-platform environments, which restricts generalizability across cross-platform (Web, Mobile, Desktop) or highly specialized engineering environments.
* **Bằng chứng (Cột Dataset & Hạn chế tự nêu):**
    * **Small Sample Sizes / Narrow Domains:** **Paper 8** (Ferreira et al., 2025) validates its tool on a small sample size of only 13 JIRA issues and 50 Gherkin scenarios restricted entirely to a single-company e-commerce setup within the automotive sector. Similarly, **Paper 7** (Karpurapu et al., 2024) limits its dataset to only 50 real-world user stories from Mendeley and Parabol Agile datasets.
    * **Platform / Feature Isolation:** **Paper 3** (Rosenbach et al., 2025) tests an engineering simulation software but explicitly notes that it is ***restricted to a single feature (tool integration wizard) on Windows*** and has not been validated across diverse engineering software products. 
    * **Language & Structural Constraints:** **Paper 6** (Jang & Kim, 2025) utilizes an experimental batch of 79 Korean sentences but notes a severe dependency on a ***strict text layout containing clear cause and result clauses***, failing to automatically process other standard sentence formats without manual specification rewrites. 
    * **Simulated Benchmarks:** **Paper 5** (Jagielski et al., 2025) relies on highly simplistic, non-production datasets (a simple Python "Hello World" script and the standard MNIST dataset) which do not reflect real-world enterprise software complexities. The only massive production codebase evaluated is in **Paper 2** (MyBMW app with 3M+ lines of code), but its dataset remains constrained to only 13 real-world JIRA issues.

---

## Phát biểu GAP tổng hợp

Current automated test generation frameworks using Large Language Models suffer from a critical architectural trade-off, relying either on privacy-compromising public ensemble APIs or isolated local model deployments that lack the multi-agent synchronization required to generate complex, multi-tier test artifacts. Furthermore, existing research is empirically bottlenecked by narrow, single-domain datasets and disjointed evaluation metrics that measure script executability while completely omitting automated requirement-to-code coverage validation.