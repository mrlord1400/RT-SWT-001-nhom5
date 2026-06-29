# Hypotheses

Mỗi RQ tương ứng với một cặp giả thuyết H0/H1. H0 biểu thị điều kiện không đạt yêu cầu nghiên cứu, trong khi H1 thể hiện kết quả kỳ vọng.

## 1. RQ1 --- Semantic Similarity {#rq1-semantic-similarity}

**RQ1:** Các Gherkin scenarios do GPT-4o tạo ra có đạt semantic similarity từ 0.85 trở lên so với các BDD scenarios được viết thủ công hay không?

- **H0_1:** μ_similarity ≤ 0.85

- **H1_1:** μ_similarity \> 0.85

- **Metric:** Cosine Semantic Similarity

- **Kiểm định:** Wilcoxon Signed-Rank Test

- **Mức ý nghĩa:** α = 0.05

------------------------------------------------------------------------

## 2. RQ2 --- Executable Syntax Rate {#rq2-executable-syntax-rate}

**RQ2:** Các Gherkin scenarios và step definitions do GPT-4o tạo ra có đạt executable syntax rate từ 80% trở lên hay không?

- **H0_2:** executable_rate ≤ 0.80

- **H1_2:** executable_rate \> 0.80

- **Metric:** Executable Syntax Rate

- **Kiểm định:** One-tailed Binomial Test (p₀ = 0.80)

- **Mức ý nghĩa:** α = 0.05

------------------------------------------------------------------------

## Tiêu chí chấp nhận

Nghiên cứu được xem là đạt mục tiêu khi:

1.  Giá trị semantic similarity trung bình lớn hơn 0.85.
2.  Executable syntax rate lớn hơn 80%.
3.  Các kiểm định thống kê cho kết quả p-value \< 0.05.
