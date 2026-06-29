# Evidence Table Synthesis - BDD/Gherkin Generation (Connextra Format)

**All 12 papers reviewed all** utilize Large Language Models (such as GPT-4, Claude, and Gemini) to automate BDD/Gherkin test generation, focusing predominantly on general requirement inputs, basic syntax validity, time savings, or subjective human evaluations.

**But, NO papers:**
* **(1) [I - Intervention/Approach]:** Evaluate the end-to-end capability of frontier LLMs to automatically generate *both* Gherkin scenarios and their underlying step definitions specifically from user stories written in the strict **Connextra format** (P).
* **(2) [O - Outcome Metric 1]:** Quantitatively measure the **semantic similarity** between the LLM-generated outputs and manually expert-written BDD scenarios (C) to ensure it meets a high-reliability threshold (e.g., $\ge 0.85$) using embedding-based metrics.
* **(3) [O - Outcome Metric 2]:** Strictly verify the **executable rate** of these generated scenarios and step definitions using an automated Gherkin parser to ensure they run with zero syntax errors.

**--> GAP:** There is a lack of quantitative evaluation on how effectively LLMs can automatically generate both Gherkin scenarios and step definitions from Connextra-format user stories, specifically missing a dual-metric assessment that combines embedding-based semantic similarity ($\ge 0.85$) against manual baselines and strict executable syntax parsing.

**--> Contribution:** This research evaluates the zero-shot performance of LLMs in generating complete Gherkin scenarios and step definitions from Connextra-format user stories, using semantic similarity (compared to manually written expected behaviors) and syntax-error-free execution rates (via a Gherkin parser) as the primary evaluation metrics.
