# Research Proposal:

**Nhóm:** 5
**Thành viên:** Võ Hải Long(SE204115), Phạm Nhật Minh(SE204177), Tiêu Anh Tuấn(SE203915), Đỗ Đăng Khoa(SE161631)
**Topic code:** RT-SWT-
**Ngày nộp:** 2026-06-19
**Version:** 1.0
**Trạng thái:** Đang chờ phê duyệt

## 2\. Research Problem Statement

### 2.1 Bối cảnh \& Tầm quan trọng

User stories theo format Connextra là nền tảng của phát triển phần mềm Agile, nhưng việc chuyển đổi chúng thành Gherkin scenarios và step definitions có thể executable vẫn là một bước thủ công tốn thời gian và dễ phát sinh lỗi cú pháp. Điều này đặc biệt quan trọng trong các dự án BDD quy mô lớn — theo Tiwari (2025), quy trình viết test thủ công chiếm thời gian đáng kể và dẫn đến số lượng defect cao hơn, trong khi việc tự động hóa bằng LLM đã giúp giảm 40% thời gian tạo test và 25% lượng defect được phát hiện sau khi ra production. Với sự phát triển của các mô hình ngôn ngữ lớn như GPT-4 và Claude, câu hỏi trung tâm là liệu LLM có thể sinh ra Gherkin scenarios vừa đảm bảo semantic similarity ≥ 0.85 so với hành vi mong đợi, vừa executable mà không có lỗi cú pháp hay không — từ đó xác định giá trị thực tiễn của chúng trong pipeline kiểm thử chấp nhận hiện đại.

### 2.2 State of the Art

Các nghiên cứu gần đây đã chứng minh LLM có khả năng sinh Gherkin đáng kể nhưng vẫn tồn tại khoảng cách về semantic và executability. Karpurapu et al. (2024) cho thấy GPT-3.5 và GPT-4 đạt gần như zero syntax error dưới few-shot prompting trên 50 user stories Agile thực tế, trong khi zero-shot gây ra tới 89% tổng số anomaly — nhấn mạnh tầm quan trọng của chiến lược prompting. Fonseca et al. (2025) triển khai framework ATOMIC với các LLM cục bộ (DeepSeek-R1, Gemma3) trên codebase Flutter 3M+ LOC, đạt 93.3% Gherkin syntactically valid và 100% executable UI tests. Về phía semantic, Ferreira et al. (2025) báo cáo AutoUAT đạt 95% helpfulness và 100% syntactic correctness nhưng chỉ 60% semantic correctness ở baseline, cho thấy syntactic và semantic là hai chiều độc lập cần đánh giá riêng. Rathnayake (2026) đánh giá trực tiếp 500 user stories/BDD scenarios, ghi nhận GPT-4 zero-shot đạt điểm semantic similarity cao nhất (4.63/5) trong khi Claude 3 dẫn đầu về human evaluation (4.06/5). Farchi (2025) bổ sung góc nhìn định lượng bằng SBERT cosine similarity, chứng minh rằng các requirement chất lượng cao cải thiện testability 55% và completeness 48% — gián tiếp khẳng định input format như Connextra có ảnh hưởng trực tiếp đến chất lượng output Gherkin.

### 2.3 GAP

Hiện nay, vẫn thiếu các nghiên cứu thực nghiệm đánh giá toàn diện khả năng zero-shot nguyên bản của các frontier LLM trong lĩnh vực tự động hóa kiểm thử phần mềm. Các tài liệu trước đây thường áp dụng phương pháp tiếp cận phân mảnh, phụ thuộc nhiều vào các kỹ thuật bổ trợ phức tạp (như few-shot, fine-tuning, RAG) hoặc đòi hỏi dữ liệu đầu vào đã được chuẩn hóa sẵn định dạng. Do đó, chưa có sự thấu đáo về khả năng của các mô hình này trong việc chuyển đổi trực tiếp và tự động từ một yêu cầu nghiệp vụ thô (raw business requirement) sang bộ tài sản kiểm thử hoàn chỉnh (bao gồm kịch bản BDD, logic mã thực thi và các artifact xác thực). Sự khuyết thiếu một quy trình (workflow) đánh giá tích hợp duy nhất từ đầu đến cuối này làm cản trở việc xác định giới hạn thực sự và tính sẵn sàng ứng dụng thực tiễn của AI thế hệ mới. Bổ sung: GAP-T và N=55 paper trong evidence-table

### 2.4 Motivation

Nếu gap này không được giải quyết, các team phát triển phần mềm sẽ tiếp tục đưa ra quyết định adoption AI dựa trên benchmark không đồng nhất — dẫn đến việc đầu tư vào các pipeline phức tạp (few-shot, RAG, fine-tuning) ngay cả khi năng lực zero-shot của frontier LLM đã đủ đáp ứng nhu cầu thực tế. Hệ quả trực tiếp là chi phí tích hợp AI vào quy trình BDD bị thổi phồng không cần thiết, trong khi các lỗi kiểm thử có thể phòng ngừa vẫn lọt qua production do thiếu một workflow tự động hóa end-to-end đã được kiểm chứng độc lập.

## 3\. Related Work

### 3.1 Overview

Bảng tóm tắt
| # | Paper | Tool / LLM | Dataset / Context | Metric | Key Findings / Results | Self-Stated Limitations |
| **1** | Fonseca (2025, IEEE/ACM ASE) | ATOMIC framework leveraging specialized local LLMs: DeepSeek-R1, DeepSeek-Coder-V2, and Gemma3:1b via Ollama. | MyBMW app (Production Flutter codebase with over 3M LOC, 36,000+ Dart files). Testing dataset of 13 JIRA issues linked to 67 GitHub commits, covering 170+ screens. | Generated artifact correctness (syntactic validity of Gherkin, executability of Page Objects/UI tests), processing time/token efficiency, and developer productivity survey. | Generated test pipelines in under 5 minutes per issue, delivering high-quality Gherkin (93.3% valid), error-free executable UI tests (100% success rate), saving up to a full day of manual work. | N/A |
| **2** | Jagielski (2025, GACLM) | Deepseek-coder-v2 paired with a RAG pipeline deployed locally via Ollama. | 100 iterative runs across two benchmarks: a simple Python "Hello World" script and a TensorFlow digit recognition model trained on the MNIST dataset. | Quality of generated tests via executable file ratios (%), test pass rates (%), and code statement lines coverage (%). | Gherkin Syntax prompts boosted file executability to 97.81% (vs. 71.0% for NL) in general code, and to 94.56% (vs. 49.43% for NL) in neural network testing. Both architectures shared 50.00%±0.00% coverage in ML tests. | N/A |
| **3** | Karpurapu (2024, IEEE Access) | GPT-3.5-turbo-0613, GPT-4 version, chat-bison-001 (PaLM-2), and Llama-2-13B-Chat. | Mendeley and Parabol Agile Dataset consisting of 50 real-world user stories compiled across distinct business domains (Agile Software Development / Automated Acceptance Testing). | Syntax validation accuracy ratios along with failure counts across four specific structural Gherkin error patterns under zero-shot and few-shot instruction rules. | Zero-shot prompting caused 89% of total anomalies (667 errors), while few-shot execution reduced flaws to 11% (80 errors), enabling GPT-3.5 and GPT-4 to lower failures to just 1 syntax error each. | N/A |
| **4** | Rathnayake (2026) | GPT-4, Claude 3, Gemini | 500 user stories/BDD scenarios across 4 products | Text/Semantic similarity, LLM \& Human eval (1–5) | GPT-4 zero-shot scored highest overall (4.63/5); Claude 3 had the highest human rating (4.06/5). | Single company data; limited human sample; evaluator bias. |
| **5** | Almeyda (2025) | AIDTG (Gemini 1.5 Pro \& GPT-4.0) | 50 real-world User Stories across 8 Epics | Time savings, human quality rating (1–5), functional correctness (%) | 80% time saved (25 mins to 5 mins/US); 4.75/5 human rating; 91.9% execution pass rate. | 8.1% failure rate due to minor syntax hallucinations; fault detection not evaluated. |
| **6** | Farchi (2025) | LLMs (unspecified) + SBERT (Sentence-BERT) | 12 projects, 150+ requirement-test case pairs | Rubric scores (1–5) for clarity, completeness, consistency, testability; SBERT cosine similarity | BDD-derived requirements improved testability by 55% and completeness by 48% over low-quality inputs; manual review effort reduced by 60–70%. | High dependency on input quality; potential domain context gaps; threshold calibration sensitivity; lacks enterprise platform integration (uses Excel). |
| **7** | Hassani (2026) | Claude 3.7 Sonnet, Llama 3.3 70B Instruct | 30 food-safety legal provisions resulting in 60 Gherkin specifications | 5-point scale (relevance, clarity, completeness, singularity, time savings) and binary plausibility check | Relevance 95%, clarity 100%, completeness 94.2%, singularity 93.4%, time savings 91.7%; no statistically reliable differences between Llama and Claude. | Occasional omissions, hallucinations, and mixed intents; quasi-experimental design without full control; evaluated by a limited pool of 10 university students lacking domain expertise. |
| **8** | Jagielski (2025) | deepseek-coder-v2 (Private GPT via Ollama) + RAG | Hello World program \& MNIST digit classifier (100 prompt runs each) | Executable (%), Pass Rate (%), Code Coverage (%) | Gherkin syntax prompts beat natural language (97.8% vs 71.0% executable for Hello World; 94.5% vs 49.4% for ML). | Stochastic nature of ML models makes fixed thresholds non-ideal; data leakage risks; dependency/import errors. |
| **9** | Ferreira (2025) | GPT-4 Turbo | 13 user stories, 50 Gherkin scenarios | Helpfulness, Syntactic/Semantic correctness | 95% helpfulness, 100% syntactic, 60% baseline semantic correctness. | Highly context-specific; small sample size; short 2-month evaluation period. |

### 3.2 Pattern Analysis

Nhìn chung, các nghiên cứu trên hội tụ quanh bốn pattern chính sau:

1. Syntactic validity của Gherkin được sinh bởi LLM đã đạt mức cao và tương đối ổn định khi có prompting strategy phù hợp — thể hiện qua Karpurapu et al. (2024), Fonseca et al. (2025), và Jagielski (2025). Karpurapu et al. (2024) ghi nhận GPT-3.5 và GPT-4 giảm syntax error xuống gần bằng 0 dưới few-shot prompting, trong khi Jagielski (2025) cho thấy Gherkin syntax prompt đẩy executability từ 71.0% lên 97.8% so với natural language input — gợi ý rằng structured input format như Connextra đóng vai trò "anchor" giúp mô hình định hình output chính xác hơn.
2. Executability end-to-end (sinh Gherkin kèm step definitions có thể chạy được) là một chiều đánh giá độc lập với syntactic correctness, và kết quả trên chiều này vẫn còn phân tán — thể hiện qua Fonseca et al. (2025), Ferreira (2025), và Almeyda (2025). Fonseca et al. (2025) đạt 100% executable UI tests trong điều kiện pipeline có kiểm soát chặt, trong khi Almeyda (2025) báo cáo 91.9% execution pass rate trên 50 user stories thực tế, và Ferreira (2025) chỉ đạt 60% semantic correctness ở baseline dù syntactic correctness đạt 100% — cho thấy một Gherkin scenario có thể chạy được về mặt cú pháp nhưng vẫn sai về mặt nghĩa so với expected behavior.
3. Semantic similarity giữa output của LLM và expected behavior là chiều yếu nhất và ít được đo lường trực tiếp nhất trong các nghiên cứu hiện tại — thể hiện qua Rathnayake (2026), Farchi (2025), và Ferreira (2025). Rathnayake (2026) đo semantic trên 500 scenarios và ghi nhận GPT-4 đạt mức cao nhất (4.63/5) nhưng dùng thang Likert thay vì cosine similarity, trong khi Farchi (2025) là nghiên cứu hiếm hoi áp dụng SBERT cosine similarity và xác nhận rằng input chất lượng cao cải thiện semantic output lên đến 55% — đặt ra câu hỏi trực tiếp liệu ngưỡng ≥ 0.85 trong PICO có đạt được một cách nhất quán ở điều kiện zero-shot hay không.
4. Phần lớn các nghiên cứu hiện tại không đánh giá năng lực zero-shot thuần túy của frontier LLM mà thường kết hợp với các kỹ thuật bổ trợ — thể hiện qua Karpurapu et al. (2024), Fonseca et al. (2025), và Hassani (2026). Karpurapu et al. (2024) cho thấy zero-shot gây ra 89% tổng số anomaly, Fonseca et al. (2025) dựa trên pipeline đa tầng với LLM chuyên biệt, và Hassani (2026) mặc dù đạt relevance 95% và clarity 100% ở điều kiện gần zero-shot nhưng vẫn ghi nhận hallucination và mixed intent — củng cố trực tiếp gap đã nêu ở phần 2.3 về sự thiếu vắng đánh giá zero-shot end-to-end toàn diện.

### 3.3 GAP Mapping

GAP-T/M/D/S | Evidence (số paper support) | Status
| **GAP-T:** Zero-shot frontier LLM chưa được đánh giá toàn diện trong workflow tích hợp end-to-end từ raw requirement → test asset hoàn chỉnh | 10 paper (Karpurapu 2024, Rathnayake 2026, Almeyda 2025, Ferreira 2025, Fonseca 2025, Jagielski 2025, Farchi 2025, Hassani 2026, Ferreira 2025 AST, Fernandes 2025) | **Confirmed** |
| **GAP-D:** Thiếu bộ dữ liệu tham chiếu đa miền với raw business requirements chưa qua chuẩn hóa | 7 paper (Karpurapu 2024, Almeyda 2025, Fonseca 2025, Hassani 2026, Rathnayake 2026, Ferreira 2025, Jagielski 2025) | **Confirmed-Deferred** |
| **GAP-M:** Thiếu Unified Metric đánh giá đồng thời semantic correctness + executability trong một pipeline duy nhất | 5 paper (Farchi 2025, Rathnayake 2026, Ferreira 2025, Karpurapu 2024, Almeyda 2025) | **Confirmed-Deferred** |
| **GAP-S:** Năng lực zero-shot cốt lõi bị che khuất bởi các kỹ thuật bổ trợ phức tạp | 8 paper (Karpurapu 2024, Fonseca 2025, Jagielski 2025, Hassani 2026, Ferreira 2025 AST, Liu 2024, Sisomboon 2026, Ferreira 2025) | **Confirmed-Deferred** |

## 4\. Research Questions

> \*\*RQ1:\*\* Kịch bản Gherkin và Step Definitions được LLM tự động sinh theo phương pháp zero-shot từ User Story chuẩn Connextra có đạt Semantic Similarity Score (Cosine) >= 0.85 so với kịch bản viết thủ công không?

**Loại claim:** Absolute threshold
**H0:** Kịch bản do LLM sinh theo phương pháp zero-shot KHÔNG đạt Semantic Similarity Score >= 0.85.
**H1:** Kịch bản do LLM sinh theo phương pháp zero-shot ĐẠT Semantic Similarity Score >= 0.85.
**Metric:** Cosine Similarity đo bằng SBERT (Sentence-BERT) giữa Gherkin scenarios do LLM sinh và kịch bản viết thủ công — thư viện sentence-transformers (model all-MiniLM-L6-v2)
**Ngưỡng:** 0.85 - Case 3: Ngưỡng này được hiệu chuẩn từ Farchi (2025), nghiên cứu duy nhất trong corpus áp dụng SBERT cosine similarity trực tiếp để đánh giá chất lượng semantic của cặp requirement–test case; đồng thời được củng cố bởi Rathnayake (2026) cho thấy GPT-4 zero-shot đạt điểm semantic cao nhất (4.63/5) — gợi ý ngưỡng ≥ 0.85 là khả thi nhưng chưa được kiểm chứng ở điều kiện zero-shot thuần túy.
**Statistical test:** One-sample Wilcoxon signed-rank test (α = 0.05)

> \*\*RQ2:\*\* GPT-4o và Claude 3.5 Sonnet zero-shot (I, temperature=0), khi sinh execution logic có đạt Syntax Validity Rate ≥ 70% (O, đánh giá bằng manual inspection theo rubric 3 tiêu chí)?

**Loại claim:** Absolute threshold
**H0:** GPT-4o và Claude 3.5 Sonnet zero-shot KHÔNG đạt Syntax Validity Rate ≥ 70% trên execution logic được sinh ra.
**H1:** GPT-4o và Claude 3.5 Sonnet zero-shot Đạt Syntax Validity Rate ≥ 70% trên execution logic được sinh ra.
**Metric:** Syntax Validity Rate (%) — tỷ lệ step definitions được sinh ra không có lỗi cú pháp, đánh giá bằng manual inspection theo rubric 3 tiêu chí: (1) cấu trúc Given/When/Then hợp lệ, (2) không có lỗi binding/regex trong step definitions, (3) file feature có thể parse được bởi Cucumber/Behave parser
**Ngưỡng:** 70% - Case 2: Ngưỡng này được thiết lập dựa trên floor reference từ Jagielski (2025), ghi nhận executability ở điều kiện natural language prompt (không có Gherkin syntax anchor) chỉ đạt 71.0% — tức là ngưỡng tối thiểu mà ngay cả prompting kém tối ưu cũng có thể vượt qua; đồng thời thấp hơn có chủ ý so với mức đạt được trong điều kiện pipeline có kiểm soát như Fonseca et al. (2025) (93.3%) và Almeyda (2025) (91.9%), nhằm kiểm tra xem zero-shot thuần túy có đủ vượt floor này không.
**Statistical test:** Binomial exact test (α = 0.05)

## 5\. Experiment Protocol

### 5.1 Pipeline tổng quan

1. Thu thập \& chuẩn bị input: Thu thập & chuẩn bị input: Sử dụng Mendeley and Parabol Agile Dataset — bộ 50 user stories thực tế theo format Connextra, được tổng hợp từ nhiều business domain (Agile Software Development / Automated Acceptance Testing) và đã được sử dụng trong Karpurapu et al. (2024). Mỗi user story được kiểm tra độ rõ nghĩa và tuân thủ format Connextra trước khi đưa vào thực nghiệm; các story không đủ chuẩn format sẽ bị loại và ghi nhận trong data log.
2. Sinh test asset (zero-shot): Gọi GPT-4o (gpt-4o-2024-05-13) và Claude 3.5 Sonnet (claude-sonnet-20240620) theo phương pháp single-turn zero-shot — mỗi requirement được đưa vào 1 lượt gọi duy nhất với prompt template cố định, không có ví dụ mẫu, không có chain-of-thought. Output yêu cầu gồm: Gherkin scenarios (.feature), step definitions (.py), và validation artifact.
3. Đánh giá semantic similarity (RQ1): Encode toàn bộ Gherkin scenarios do LLM sinh và kịch bản viết thủ công bằng sentence-transformers (all-MiniLM-L6-v2), tính cosine similarity từng cặp, so sánh với ngưỡng ≥ 0.85. Kiểm định bằng One-sample Wilcoxon signed-rank test (α = 0.05).
4. Đánh giá executability (RQ2): Chạy toàn bộ step definitions sinh ra qua behave 1.2.6 (hoặc pytest-bdd) với subprocess capture để ghi nhận syntax error/runtime error. Tính Syntax Validity Rate = số file không lỗi cú pháp / tổng số file. Kiểm định bằng Binomial exact test (α = 0.05).
5. Tổng hợp \& báo cáo: So sánh kết quả giữa GPT-4o và Claude 3.5 Sonnet trên cả hai metric, ghi nhận các lỗi phổ biến theo loại (syntax hallucination, semantic drift, incomplete step binding), và đánh giá effect size.

### 5.2 Dataset

Tên dataset: Mendeley and Parabol Agile Dataset | Nguồn: Karpurapu et al. (2024) — IEEE Access, DOI: 10.1109/ACCESS.2024.3391815 | Quy mô (N): 50 user stories thực tế trải rộng nhiều business domain; mỗi user story sinh ra 1 bộ test asset → 50 cặp để đánh giá (×2 mô hình = 100 observations tổng) | Domain: Đa miền — Agile Software Development và Automated Acceptance Testing, bao gồm các nghiệp vụ CRUD, workflow đa bước, và luồng có điều kiện | Preprocessing: Kiểm tra và lọc các story theo format Connextra chuẩn ("As a [role], I want [goal], so that [benefit]") trước khi đưa vào thực nghiệm; story thiếu cấu trúc sẽ bị loại và ghi nhận | Sampling strategy: Toàn bộ dataset (exhaustive) — không random sampling, đảm bảo reproducibility hoàn toàn |

Lý do chọn: Dataset này được lựa chọn vì ba lý do có liên kết chặt với thiết kế nghiên cứu. Thứ nhất, comparability trực tiếp với prior work: Karpurapu et al. (2024) đã dùng chính dataset này để đánh giá GPT-3.5 và GPT-4 dưới zero-shot và few-shot prompting, ghi nhận zero-shot gây ra 89% tổng số anomaly — điều này cho phép nghiên cứu hiện tại đặt kết quả trong cùng không gian thực nghiệm và tạo ra một so sánh có cơ sở: liệu GPT-4o và Claude 3.5 Sonnet (frontier model thế hệ mới hơn) có cải thiện được performance zero-shot trên cùng bộ input hay không. Thứ hai, tính đại diện đa miền: 50 user stories được thu thập từ nhiều business domain thực tế, đảm bảo kết quả không bị thiên lệch bởi đặc thù của một nghiệp vụ cụ thể — khắc phục trực tiếp GAP-D về thiếu dataset tham chiếu đa miền. Thứ ba, tính có sẵn và reproducibility: Dataset được công bố kèm theo paper peer-reviewed (IEEE Access), đảm bảo khả năng kiểm chứng độc lập và tái lập thực nghiệm mà không phụ thuộc vào nguồn dữ liệu nội bộ.

### 5.3 LLM/Tool Configuration

Model: gpt-4o-2024-05-13 | claude-sonnet-20240620
Hyperparameters: Temperature 0 | top\_p1.0 | max\_tokens 4096
Prompting strategy: Zero-shot (single-turn)
Prompt template:

You are a BDD test engineer. Given the following user story in Connextra format,
generate: (1) Gherkin scenarios in .feature format, (2) step definitions in Python,
(3) a validation checklist. Do not add examples, explanations, or additional context.

User Story: {input}

Lý do cấu hình: Temperature = 0 đảm bảo tính tái lập (reproducibility) và loại bỏ biến động ngẫu nhiên — nhất quán với GAP-S về việc đánh giá năng lực zero-shot cốt lõi, không phải năng lực sáng tạo của mô hình.

### 5.4 Measurement

Metric: | Tool + version: | Ground truth source: | IAA method +  threshold:
Semantic Similarity (RQ1) | sentence-transformers v2.2.2, model all-MiniLM-L6-v2 | Gherkin scenarios viết thủ công bởi 2 BDD practitioners | Cohen's κ ≥ 0.70 trên 20% sample ngẫu nhiên
Syntax Validity Rate (RQ2) | behave v1.2.6 + subprocess capture (Python 3.11) | Parser output (binary: valid / invalid) | Không cần IAA — kết quả parser là deterministic

### 5.5 Baseline

Không áp dụng — cả RQ1 và RQ2 đều là absolute threshold claim, không phải comparative claim. Ngưỡng tham chiếu được thiết lập từ literature (Farchi 2025, Jagielski 2025) thay vì so sánh với hệ thống khác.

### 5.6 Statistical Analysis Plan

Test: One-sample Wilcoxon signed-rank test, one-tailed
α: 0.05
Lý do chọn test: Distribution của cosine similarity scores không đảm bảo normal (N nhỏ, bounded [0,1]) → non-parametric
Effect size: Cohen's d (so sánh mean score với ngưỡng 0.85)
N và power: N = 50, power ≥ 0.80 theo power analysis bằng statsmodels; với N lớn hơn đáng kể so với minimum, power dự kiến cao hơn 0.80 — ghi nhận observed power cùng kết quả

Test: Binomial exact test, one-tailed
α: 0.05
Lý do chọn test: Metric là tỷ lệ nhị phân (valid/invalid) → exact test chính xác hơn chi-square; với N = 50, Binomial exact test vẫn được ưu tiên để đảm bảo tính chính xác thay vì dựa vào xấp xỉ normal
Effect size: Cohen's h (so sánh observed rate với ngưỡng 0.70)
N và power: N = 50, power ≥ 0.80; minimum detectable difference = 10% trên ngưỡng

## 6\. Evaluation Plan

### 6.1 Bảng Tiêu Chí Đánh Giá

|RQ|Metric|Ngưỡng|Test|H0 bị reject khi...|Kết quả âm tính có ý nghĩa?|
|-|-|-|-|-|-|
|**RQ1**|Cosine Similarity trung bình (SBERT `all-MiniLM-L6-v2`)|≥ 0.85|One-sample Wilcoxon signed-rank, one-tailed, α = 0.05|p < 0.05 **và** median cosine similarity ≥ 0.85|Có — chứng minh zero-shot LLM chưa đủ semantic fidelity để thay thế manual BDD, củng cố GAP-T|
|**RQ2**|Syntax Validity Rate (%) qua `behave` v1.2.6 parser|≥ 70%|Binomial exact test, one-tailed, α = 0.05|p < 0.05 **và** observed rate ≥ 70%|Có — cho thấy zero-shot sinh ra step definitions có tỷ lệ lỗi cú pháp không chấp nhận được trong thực tế|

### 6.2 Diễn Giải Tổng Hợp Kết Quả

**Tình huống 1 — Double Positive (RQ1 ✅ \& RQ2 ✅):** Cả semantic similarity ≥ 0.85 lẫn syntax validity ≥ 70% đều đạt ngưỡng và có ý nghĩa thống kê. Kết luận: Zero-shot frontier LLM (GPT-4o và/hoặc Claude 3.5 Sonnet) đủ năng lực sinh test asset có thể sử dụng trực tiếp từ Connextra user stories mà không cần kỹ thuật bổ trợ — GAP-T được lấp một phần, mở ra hướng adoption thực tế trong pipeline BDD.

**Tình huống 2 — Mixed (RQ1 ✅ \& RQ2 ❌ hoặc RQ1 ❌ \& RQ2 ✅):** Một chiều đạt ngưỡng, chiều còn lại không. Kết luận: LLM hiểu đúng nghĩa nghiệp vụ nhưng sinh mã không ổn định về cú pháp (hoặc ngược lại) — hai chiều đánh giá là độc lập và cần được đo riêng, nhất quán với phát hiện của Ferreira (2025) (100% syntactic, 60% semantic). Nghiên cứu sẽ báo cáo chiều nào là bottleneck và đề xuất can thiệp tối thiểu (ví dụ: post-processing parser) để khắc phục.

**Tình huống 3 — Double Negative (RQ1 ❌ \& RQ2 ❌):** Cả hai metric đều không đạt ngưỡng. Kết luận: Zero-shot thuần túy chưa đủ năng lực cho task end-to-end này ở điều kiện thực nghiệm — kết quả âm tính có giá trị khoa học độc lập, xác nhận sự cần thiết của các kỹ thuật bổ trợ (few-shot, RAG) và đặt ra baseline rõ ràng cho các nghiên cứu tiếp theo. Kết luận này **không** bị coi là thất bại của nghiên cứu.

### 6.3 Sub-group Analysis

**Điều kiện kích hoạt:** Sub-group analysis chỉ được thực hiện nếu N\_group ≥ 5 per subgroup — quyết định này được xác định TRƯỚC khi có data.

Hai sub-group được định nghĩa trước:

**Sub-group A — theo mô hình (GPT-4o vs. Claude 3.5 Sonnet):** So sánh cosine similarity score và syntax validity rate giữa hai mô hình bằng Mann-Whitney U test (α = 0.05). Mục tiêu: xác định liệu có sự khác biệt có ý nghĩa thống kê giữa hai frontier LLM ở cùng điều kiện zero-shot hay không — trả lời câu hỏi thực tiễn về lựa chọn mô hình.

**Sub-group B — theo độ phức tạp của requirement (simple vs. complex):** Phân loại 50 user stories thành 2 nhóm theo số lượng điều kiện nghiệp vụ (simple: ≤ 2 điều kiện; complex: ≥ 3 điều kiện), so sánh metric giữa hai nhóm. Mục tiêu: xác định liệu zero-shot LLM có bị suy giảm chất lượng đáng kể trên requirements phức tạp hay không — thông tin cần thiết để xác định giới hạn ứng dụng thực tế.

## 7\. Threats to Validity

### 7.1 Internal Validity

**Threat 1 — Model version drift:** OpenAI và Anthropic có thể silent-update model weights mà không thay đổi model string, khiến kết quả không tái lập nếu chạy lại thực nghiệm sau thời điểm thu thập data.
**Mitigation:** Pin version cứng trong toàn bộ API call: `gpt-4o-2024-05-13` và `claude-sonnet-20240620`. Log đầy đủ model string, timestamp, và response ID của từng lượt gọi vào file thực nghiệm. Nếu Anthropic hoặc OpenAI xác nhận có update trong khoảng thời gian thực nghiệm, ghi nhận là limitation.

**Threat 2 — Annotation bias trong ground truth:** Kịch bản Gherkin viết thủ công dùng làm ground truth cho RQ1 có thể bị ảnh hưởng bởi phong cách cá nhân của người viết (từ vựng, mức độ chi tiết của step), khiến cosine similarity bị lệch không phản ánh đúng semantic correctness thực sự.
**Mitigation:** Ground truth được viết độc lập bởi 2 BDD practitioners theo rubric cố định (Given = precondition, When = action, Then = expected outcome); tính inter-annotator agreement bằng Cohen's κ trước khi dùng làm reference. Chỉ sử dụng các scenario có κ ≥ 0.70; các scenario bất đồng được thảo luận và thống nhất trước khi đưa vào đánh giá.

**Threat 3 — Temperature = 0 không đảm bảo determinism hoàn toàn:** Một số nghiên cứu ghi nhận rằng ngay cả với temperature = 0, các cloud LLM vẫn có thể trả về output khác nhau giữa các lần gọi do batch processing và floating-point non-determinism ở phía server.
**Mitigation:** Mỗi requirement được gọi 3 lần độc lập; nếu output của 3 lần gọi khác nhau (đo bằng exact string match), ghi nhận variance và dùng lần gọi đầu tiên làm kết quả chính thức — quyết định này được xác định trước khi chạy thực nghiệm.

### 7.2 External Validity

**Threat 1 — Single source với domain scope có thể chưa đại diện:** Mặc dù Mendeley and Parabol Agile Dataset bao gồm nhiều business domain, toàn bộ 50 user stories được thu thập từ một nguồn duy nhất (Karpurapu et al. 2024), có thể phản ánh thiên lệch về cách diễn đạt requirements của nhóm nghiên cứu gốc hơn là phân phối tự nhiên của raw business requirements trong môi trường doanh nghiệp thực tế.
Mitigation: Ghi rõ single-source limitation trong phần kết luận. Tính đa dạng domain trong nội bộ dataset (CRUD đơn giản đến flow đa bước có điều kiện trên nhiều lĩnh vực nghiệp vụ) giúp tăng tính đại diện trong phạm vi cho phép. Đề xuất replication trên dataset tổng hợp từ nhiều nguồn là future work.

**Threat 2 — Dataset được thiết kế cho bối cảnh nghiên cứu năm 2024, có thể không phản ánh đặc thù của frontier LLM hiện tại:** 50 user stories trong Mendeley and Parabol Agile Dataset được thu thập và chuẩn hóa để đánh giá GPT-3.5/GPT-4 trong bối cảnh 2024; phân phối độ khó, độ dài, và cấu trúc ngôn ngữ của các stories này có thể không đại diện tối ưu cho dải năng lực của GPT-4o và Claude 3.5 Sonnet.
Mitigation: Giới hạn này được thừa nhận rõ ràng; tuy nhiên, việc dùng cùng dataset với prior work (Karpurapu 2024) tạo ra điểm so sánh có kiểm soát — mọi khác biệt về kết quả có thể gán cho sự tiến bộ của model, không phải thay đổi dataset. Đây là trade-off có chủ ý giữa comparability và novelty của input.

### 7.3 Construct Validity

**Threat 1 — Cosine similarity (SBERT) không đồng nhất với semantic correctness theo nghĩa nghiệp vụ:** Hai đoạn văn có thể có cosine similarity cao nhưng vẫn mô tả hành vi nghiệp vụ khác nhau nếu dùng từ vựng tương tự; ngược lại, một scenario đúng hoàn toàn nhưng dùng từ vựng khác với ground truth có thể bị đánh giá thấp.
**Mitigation:** SBERT được chọn thay vì BLEU vì đo semantic embedding thay vì n-gram overlap, nhất quán với Farchi (2025). Bổ sung manual spot-check trên 20% sample ngẫu nhiên bởi 1 reviewer độc lập để xác nhận rằng các scenario có cosine similarity ≥ 0.85 thực sự mô tả đúng hành vi nghiệp vụ — kết quả spot-check được báo cáo như một validation layer.

**Threat 2 — Syntax Validity Rate đo bằng parser không phản ánh đủ executability thực tế:** Một file `.feature` có thể pass parser của `behave` nhưng vẫn fail ở runtime do step definitions thiếu binding, selector sai, hoặc môi trường test chưa được cấu hình.
**Mitigation:** Ghi rõ trong phần Measurement rằng RQ2 đo *syntactic validity* (parser-level), không phải *runtime executability* — đây là scope được xác định trước, không phải sau khi có kết quả. Khuyến nghị runtime execution testing như một bước tiếp theo trong future work.

### 7.4 Conclusion Validity

**Threat 1 — Statistical power và độ tin cậy của kết quả:** Với N = 50, power của One-sample Wilcoxon và Binomial exact test dự kiến đạt hoặc vượt 0.80 ở α = 0.05 — tuy nhiên nếu effect size nhỏ hơn dự kiến, power thực tế có thể thấp hơn, làm tăng nguy cơ Type II error (không reject H0 dù LLM thực sự đạt ngưỡng).
Mitigation: Chạy power analysis bằng statsmodels trước khi thu thập data để xác định minimum detectable effect size ở N = 50, α = 0.05, power = 0.80. Báo cáo observed power cùng kết quả — không điều chỉnh ngưỡng hay thêm data sau khi thấy kết quả (tránh HARKing).

**Threat 2 — Multiple testing inflation:** Thực nghiệm kiểm định đồng thời 2 RQ và thêm 2 sub-group analyses, làm tăng family-wise error rate vượt quá α = 0.05 nếu không điều chỉnh.
**Mitigation:** Áp dụng Bonferroni correction cho sub-group analyses (α\_adjusted = 0.05 / 2 = 0.025). Hai RQ chính được giữ nguyên α = 0.05 vì là independent hypotheses, không phải multiple comparisons trên cùng một dataset.

## 8\. Timeline \& Resources

### 8.0 Phân Công Vai Trò

|Role|Thành viên|Trách nhiệm trong experiment|
|-|-|-|
|**PL** và **RW**|Võ Hải Long|Coordinate tiến độ, review nhất quán toàn proposal **và** Viết §1, §7, intro, conclusion; hỗ trợ DG viết §3; tạo figures|
|**DG**|Phạm Nhật Minh|Thu thập + clean dataset, tạo ground truth, tính IAA|
|**LR**|Tiêu Anh Tuấn|Cấu hình API, script chạy experiment, batch processing|
|**MS**|Đỗ Đăng Khoa|Implement metrics, chạy statistical tests, tính effect size|



### 8.1 Resource Inventory

|Tài nguyên|Trạng thái|Owner|Ghi chú|
|-|-|-|-|
|Dataset|✅|DG|Mendeley and Parabol Agile Dataset (Karpurapu et al. 2024) — 50 user stories thực tế, đa miền, format Connextra; cần verify link tải và license trước Tuần 5|
|API key — OpenAI|⚠️|LR|Free tier: 500 calls/day; cần upgrade nếu batch > 45 calls/run|
|API key — Anthropic|⚠️|LR|Free tier tương đương; pin version `claude-sonnet-20240620`|
|Compute|✅|LR|Google Colab T4 (metric computation + statistical tests); không cần GPU cho inference|
|Ground truth|⚠️|DG|Ước tính: 8 giờ × 2 người annotator (50 stories); IAA session cần lên lịch trước Tuần 7|
|`behave` v1.2.6 + `sentence-transformers` v2.2.2|✅|MS|Đã test local; `all-MiniLM-L6-v2` download một lần, cache offline|

### 8.2 Chi Phí Ước Tính

|Item|Số lượng|Đơn giá|Tổng|
|-|-|-|-|
|OpenAI API — GPT-4o (`gpt-4o-2024-05-13`)|50 requirements × 3 runs × \~1,500 tokens/call|\~$0.005/1K input token|\~$1.13|
|Anthropic API — Claude 3.5 Sonnet|50 requirements × 3 runs × \~1,500 tokens/call|\~$0.003/1K input token|\~$0.68|
|Google Colab Pro (nếu cần)|1 tháng|$9.99/tháng|$9.99 (optional)|
|Thời gian annotator ground truth|2 người × 8 giờ|—|16 người-giờ|
|**Tổng chi phí tiền mặt ước tính**|||**< $12 USD** hoặc **< 315000 VNĐ**|

### 8.3 Timeline Chi Tiết (Tuần 5–10)

|Tuần|Hoạt động|Owner|Checkpoint — output cụ thể|
|-|-|-|-|
|**5**|Viết proposal §2–§7 (RBL-2.1 → RBL-3.1 Bước 3)|DG + RW + PL|Draft §2–§7 trong `proposal.md`|
|**5**|Verify + download dataset, kiểm tra format, xác nhận license|DG|`data/raw/` folder + README mô tả schema|
|**5**|Setup API, test 1 sample call, xác nhận budget|LR|`test\_api.py` chạy được + cost log|
|**5**|Implement metric script sơ bộ, test data giả|MS|`compute\_metric.py` draft — chạy được trên dummy data|
|**6**|Hoàn thiện §8 + resource inventory + nộp GV|PL|`proposal.md` v1.0 — nộp GV|
|**6**|★ **GV phê duyệt** *(hard deadline: cuối Tuần 6)*|GV|`proposal.md` → Trạng thái: Approved|
|**7**|Annotate ground truth pilot (20% sample)|DG|`data/pilot\_ground\_truth.csv`|
|**7**|Chạy LLM trên pilot sample|LR|`results/pilot\_llm\_output.csv` + API log|
|**7**|Tính metric pilot, kiểm tra phân phối|MS|`results/pilot\_analysis.ipynb` — histogram + normality check|
|**7**|**All: Họp review pilot** → amendment nếu cần|PL|Meeting note. Amendment → nộp GV trong 24 giờ|
|**8**|Annotate full ground truth|DG|`data/full\_ground\_truth.csv` — N đầy đủ, IAA ≥ 0.70|
|**8**|Full experiment batch run|LR|`results/full\_llm\_output.csv` + cost log|
|**8**|Tính metric toàn bộ + statistical tests|MS|`results/full\_analysis.ipynb` — p-value, effect size|
|**8**|Tạo figures (≥ 2 plots)|RW|`figures/` — boxplot cosine scores + syntax validity bar|
|**9–10**|Viết paper + present|Tất cả|Xem **RBL-5**|

### 8.4 Contingency Plan

**Nếu proposal chưa duyệt cuối Tuần 6:** Chỉ làm RQ1, bỏ RQ2 — báo GV ngay.

**Nếu API rate limit:** Chia batch, chạy qua đêm, hoặc dùng model nhỏ hơn (cần amendment).

**Nếu dataset inaccessible (Mendeley link down hoặc license issue):** Liên hệ trực tiếp tác giả Karpurapu et al. qua email học thuật để xin dataset gốc; nếu không nhận được phản hồi trong 5 ngày làm việc, chuyển sang Almeyda (2025) dataset (50 user stories, 8 Epics) — tên + URL ghi sẵn trong README.

**Nếu pilot Tuần 7 phát hiện vấn đề kỹ thuật:** Xem §8.6 Amendment — nộp GV trong 24 giờ.

**Nếu thành viên không kịp deadline:** PL escalate sau 48 giờ trễ; redistribute task theo ma trận §8.5.

### 8.5 Checkpoint Per Member (Tuần 5–10)

|Role|Tuần 5|Tuần 6|Tuần 7|Tuần 8|Tuần 9–10|
|-|-|-|-|-|-|
|**PL**|Draft §2–§7 review|Submit proposal + theo dõi GV|Pilot meeting note|Verify full results|Coordinate paper + present|
|**DG**|data/raw/ + README (Mendeley dataset verified)|Confirm §8.1 resource|`data/pilot\_ground\_truth.csv`|`data/full\_ground\_truth.csv`|Hỗ trợ viết §3–§4|
|**LR**|`test\_api.py` pass|Confirm API budget|`results/pilot\_llm\_output.csv`|`results/full\_llm\_output.csv` + cost log|Review §5 reproducibility|
|**MS**|`compute\_metric.py` draft|Confirm stat test plan|`results/pilot\_analysis.ipynb`|`results/full\_analysis.ipynb`|Viết §6 results|
|**RW**|Draft §7 Threats|Format + proofread §1–§7|—|`figures/` folder|Draft §1 + conclusion + present slides|

### 8.6 Quy Trình Amendment (Khi Pilot Tuần 7 Phát Hiện Vấn Đề Kỹ Thuật)

**Khi nào cần amendment — khi nào không:**

|Phát hiện từ pilot|Cần amendment?|Lý do|
|-|-|-|
|Phân phối data khác loại dự kiến (bimodal, heavy-tail)|✅ Đổi statistical test|Lý do khoa học — test không phù hợp với data|
|Metric không tính được do lỗi implementation hoặc data format|✅ Đổi implementation|Lỗi kỹ thuật, không phải thay đổi hypothesis|
|N thực tế nhỏ hơn N trong proposal (dataset thiếu rows)|✅ Cập nhật §5.2 + power analysis|Thay đổi điều kiện thực nghiệm|
|Kết quả pilot thấp hơn threshold|❌ Không amendment|Đây là kết quả — không phải lý do để thay ngưỡng|
|Muốn thêm metric vì thấy kết quả thú vị|❌ Không amendment|HARKing — vi phạm khoa học|



