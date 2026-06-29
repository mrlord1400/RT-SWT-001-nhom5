# Quá trình Tinh chỉnh Câu hỏi Nghiên cứu (RQ) và PICO

## 1. RQ và PICO Ban đầu
**Câu hỏi Nghiên cứu (RQ) ban đầu:**
Đối với user stories viết theo format Connextra (P), LLM tự động sinh Gherkin scenarios và step definitions (I) so với BDD scenarios viết thủ công (C) có đạt semantic similarity ≥ 0.85 với expected behavior và executable không lỗi cú pháp không (O)?

**PICO ban đầu:**
* **P (Population/Problem):** User stories viết theo format Connextra.
* **I (Intervention):** LLM tự động sinh Gherkin scenarios và step definitions.
* **C (Comparison):** BDD scenarios viết thủ công.
* **O (Outcome):** Đạt semantic similarity ≥ 0.85 với expected behavior và executable không lỗi cú pháp.

---

## 2. Những điểm tinh chỉnh và Nguồn
| Chỗ còn mơ hồ trong RQ ban đầu | Sau khi phân tích Gap & Evidence / Hướng tinh chỉnh | Nguồn tham chiếu |
| :--- | :--- | :--- |
| **"LLM" nào?** | Xác định cụ thể là mô hình thế hệ mới tối ưu chi phí **GPT-4o mini**. | Final Gap Statement & Cột Tool/LLM trong Evidence table |
| **Temperature / Prompting?** | Cài đặt **zero-shot** với **temperature=0** để đảm bảo tính nhất quán và khả năng tái lập. | Final Gap Statement & Reproducibility best practice |
| **Đo lường Semantic Similarity bằng gì?** | Sử dụng **Cosine Similarity** dựa trên không gian nhúng câu (**Sentence-Transformers**). | Final Gap Statement |
| **Ngưỡng executable đánh giá như thế nào?** | Đặt mốc cụ thể là **≥ 80%**, kiểm tra tự động thông qua **Gherkin Parser** chuyên dụng. | Final Gap Statement & Evidence table |
| **Xác thực tính khoa học (Mới bổ sung)** | Bổ sung các kiểm định thống kê toán học nghiêm ngặt (**Wilcoxon signed-rank test** và **Binomial test**) để chứng minh ý nghĩa thống kê của kết quả. | Final Gap Statement |
| **Dữ liệu đầu vào (Dataset)** | Cụ thể hóa thành tập dữ liệu chuẩn gồm **55 User Stories** định dạng Connextra. | Final Gap Statement |

---

## 3. RQ và PICO Tinh chỉnh (Chính thức)
**Câu hỏi Nghiên cứu (RQ) chính thức:**
> "Does GPT-4o mini zero-shot (temperature=0) generate complete Gherkin acceptance test scenarios and step definitions that achieve cosine semantic similarity ≥ 0.85 (via Sentence-Transformers) with expert-written baselines AND an executable syntax rate ≥ 80% (via Gherkin parser), with results validated for statistical significance (using Wilcoxon and Binomial tests), when applied to a dataset of 55 Connextra-format user stories?"

**PICO tinh chỉnh:**
* **P (Population):** Tập dữ liệu gồm 55 User stories được chuẩn hóa theo định dạng Connextra.
* **I (Intervention):** Mô hình ngôn ngữ lớn tối ưu chi phí GPT-4o mini dưới cấu hình zero-shot (temperature=0) tự động sinh toàn bộ Gherkin scenarios và step definitions.
* **C (Comparison):** BDD scenarios (Gherkin + step definitions) chuẩn do chuyên gia viết thủ công (Expert baselines).
* **O (Outcome):** * Metric 1 (Semantic): Độ tương đồng ngữ nghĩa đo bằng Cosine Similarity (sử dụng Sentence-Transformers) đạt ngưỡng ≥ 0.85.
    * Metric 2 (Execution): Tỷ lệ cú pháp thực thi (Executable syntax rate) kiểm tra qua Gherkin Parser đạt ≥ 80%.
    * Metric 3 (Statistical Validation): Hiệu năng vượt trội và tính hiệu quả của mô hình được chứng minh có ý nghĩa thống kê bằng kiểm định Wilcoxon signed-rank test và Binomial test.
