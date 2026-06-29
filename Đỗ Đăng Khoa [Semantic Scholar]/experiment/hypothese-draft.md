# **Hypotheses Draft – Đánh giá hiệu quả của LLM trong việc sinh Gherkin Test Cases**

Ngày: 2026-06-08

## **RQ1 – Khả năng bao phủ yêu cầu nghiệp vụ**

**RQ1:**

GPT-4o có thể tạo các Gherkin Test Cases từ Software Requirements đạt độ bao phủ (Coverage) từ 80% trở lên hay không?

**P (Population):**  
Tập User Stories và Software Requirements được sử dụng trong nghiên cứu.

**I (Intervention):**  
GPT-4o (temperature \= 0, zero-shot prompting).

**O (Outcome):**  
Coverage Score (%).

**C (Comparison):**  
Ngưỡng Coverage \= 80%.

**H0 (Giả thuyết không):**

GPT-4o không tạo được Gherkin Test Cases có Coverage trung vị đạt từ 80% trở lên.

**H1 (Giả thuyết đối):**

GPT-4o tạo được Gherkin Test Cases có Coverage trung vị đạt từ 80% trở lên.

**Kiểm định thống kê dự kiến:**

Wilcoxon Signed-Rank Test (α \= 0.05)

---

## **RQ2 – Độ chính xác của Gherkin Test Cases được sinh ra**

**RQ2:**

GPT-4o có thể tạo các Gherkin Test Cases đạt độ chính xác (Correctness) từ 85% trở lên hay không?

**P (Population):**  
Tập User Stories và Software Requirements được sử dụng trong nghiên cứu.

**I (Intervention):**  
GPT-4o (temperature \= 0, zero-shot prompting).

**O (Outcome):**  
Correctness Score (%).

**C (Comparison):**  
Ngưỡng Correctness \= 85%.

**H0 (Giả thuyết không):**

GPT-4o không tạo được Gherkin Test Cases có Correctness trung vị đạt từ 85% trở lên.

**H1 (Giả thuyết đối):**

GPT-4o tạo được Gherkin Test Cases có Correctness trung vị đạt từ 85% trở lên.

**Kiểm định thống kê dự kiến:**

Wilcoxon Signed-Rank Test (α \= 0.05)

---

## **RQ3 – Khả năng tái sử dụng của Gherkin Test Cases**

**RQ3:**

GPT-4o có thể tạo các Gherkin Test Cases đạt khả năng tái sử dụng (Reusability) từ 70% trở lên hay không?

**P (Population):**  
Tập User Stories và Software Requirements được sử dụng trong nghiên cứu.

**I (Intervention):**  
GPT-4o (temperature \= 0, zero-shot prompting).

**O (Outcome):**  
Reusability Score (%).

**C (Comparison):**  
Ngưỡng Reusability \= 70%.

**H0 (Giả thuyết không):**

GPT-4o không tạo được Gherkin Test Cases có Reusability trung vị đạt từ 70% trở lên.

**H1 (Giả thuyết đối):**

GPT-4o tạo được Gherkin Test Cases có Reusability trung vị đạt từ 70% trở lên.

**Kiểm định thống kê dự kiến:**

Wilcoxon Signed-Rank Test (α \= 0.05)

