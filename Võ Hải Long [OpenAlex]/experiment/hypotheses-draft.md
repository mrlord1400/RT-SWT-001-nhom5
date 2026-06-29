# Hypotheses Draft — [LLM for Acceptance Test Automation (BDD/Gherkin)]

Ngày: 2026-06-13

## RQ1 — Semantic Similarity (Absolute Threshold)

**RQ:** Kịch bản Gherkin và Step Definitions được LLM tự động sinh theo phương pháp zero-shot từ User Story chuẩn Connextra có đạt Semantic Similarity Score (Cosine) >= 0.85 so với kịch bản viết thủ công không?

* **H0:** Kịch bản do LLM sinh theo phương pháp zero-shot KHÔNG đạt Semantic Similarity Score >= 0.85.
* **H1:** Kịch bản do LLM sinh theo phương pháp zero-shot ĐẠT Semantic Similarity Score >= 0.85.
* **Statistical test dự kiến:** One-sample Wilcoxon signed-rank test (alpha = 0.05).

## RQ2 — Executability Pass Rate (Absolute Threshold)

**RQ:** Kịch bản Gherkin và Step Definitions được LLM tự động sinh theo phương pháp zero-shot từ User Story chuẩn Connextra có đạt Executability Pass Rate (thực thi không lỗi cú pháp) >= 90% không?

* **H0:** Kịch bản do LLM sinh theo phương pháp zero-shot KHÔNG đạt Executability Pass Rate >= 90%.
* **H1:** Kịch bản do LLM sinh theo phương pháp zero-shot ĐẠT Executability Pass Rate >= 90%.
* **Statistical test dự kiến:** Binomial exact test (alpha = 0.05).

## RQ3 — Comparative Baseline (vs GPT-4o-mini)

**RQ:** Các mô hình LLM frontier (ví dụ: Gemini, DeepSeek) khi sinh pipeline BDD End-to-End từ User Story chuẩn Connextra có tốt hơn mô hình baseline (GPT-4o-mini) về các chỉ số Semantic Similarity và Executability không?

* **H0:** Các mô hình LLM frontier KHÔNG tốt hơn GPT-4o-mini về Semantic Similarity và Executability.
* **H1:** Các mô hình LLM frontier TỐT HƠN GPT-4o-mini về Semantic Similarity và Executability.
* **Statistical test dự kiến:** Mann-Whitney U test (alpha = 0.05).