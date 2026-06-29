"Despite the rapid advancements in leveraging Large Language Models (LLMs) for automated test case generation (e.g., Fernandes et al., 2025; Wang et al., 2024), a significant research gap remains at the intersection of **semantic business-rule translation** and **executable BDD boilerplate alignment**.

Current literature predominantly focuses on unit test generation from structural source code (Chu et al., 2025; Walczak et al., 2025\) or the zero-shot generation of isolated Gherkin feature files from clean, plain-text user stories (Fernandes et al., 2025). However, existing approaches fail to address two critical practical bottlenecks:

1. **Contextual Hallucinations in Multi-turn Scenarios:** LLMs frequently hallucinate or generate mismatched Step Definitions when translating complex, multi-layered business rules into standard *Given-When-Then* syntaxes under real-world, messy production constraints (Liu et al., 2025).  
2. **Lack of Dynamic Reusability and Seamless CI/CD Integration:** While recent studies attempt to tackle framework scalability and scriptless architectures (Rehan et al., 2025; Murugan & Balamurugan, 2025), there is a distinct shortage of deterministic end-to-end methodologies that enable LLM-driven testing agents to dynamically refactor existing step libraries, maintain long-horizon test suites (Thai et al., 2025), and synchronize natively with enterprise CI/CD environments without high manual review overhead.

Therefore, this study aims to bridge this gap by proposing a novel, context-aware LLM framework specifically optimized for acceptance test automation that guarantees both syntactic correctness and semantic compliance in enterprise BDD workflows."

