Mỗi RQ → 1 cặp H0/H1. H0 = phủ định điều muốn chứng minh. H1 = điều kỳ vọng đúng.

**1. RQ1 — Semantic Similarity**

* H0_1: μ_similarity <= 0.85 (GPT-4o CHƯA đạt ngưỡng)
* H1_1: μ_similarity > 0.85 (GPT-4o ĐẠT ngưỡng)
* Kiểm định: Wilcoxon signed-rank test · α = 0.05

**2. RQ2 — Executable Syntax**

* H0_2: executable_rate <= 0.80 (GPT-4o CHƯA đạt ngưỡng tỷ lệ thực thi)
* H1_2: executable_rate > 0.80 (GPT-4o ĐẠT ngưỡng tỷ lệ thực thi)
* Kiểm định: Binomial test (one-tailed, p_0 = 0.80) · α = 0.05