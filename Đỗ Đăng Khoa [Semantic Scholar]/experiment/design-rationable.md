# **Experiment Design Rationale – Evaluating LLM-generated BDD Test Cases**

Ngày: 2026-06-08  
 GAP source: `SLR/gap-analysis.md`

---

## **Bảng Quyết Định**

| Quyết định | Giá trị | Nguồn gốc |
| ----- | ----- | ----- |
| LLM/Tool | GPT-4o, Gemini 2.5 Pro, Claude 4 Sonnet | GAP-T: thiếu nghiên cứu đánh giá nhất quán giữa các LLM hiện đại |
| Dataset | User Stories và Requirements từ Swag Labs, CURA Healthcare Service và các case study BDD phổ biến | GAP-D: thiếu benchmark chuẩn |
| Metric chính | Coverage (%) | GAP-M: nhiều nghiên cứu chưa đánh giá đầy đủ độ bao phủ |
| Metric phụ | Correctness (%), Completeness (%), Reusability Score | Fernandes et al. (2025), Wang et al. (2024), Mughal (2024) |
| Baseline type | Manual-written Gherkin/Test Cases bởi Tester | GAP-S: thiếu đối chiếu với phương pháp thủ công |
| Threshold RQ1 | Coverage ≥ 80% | Case \[1/2/3\]: mức coverage được xem là chấp nhận được trong Acceptance Testing |
| Threshold RQ2 | Correctness ≥ 85% | Case \[1/2/3\]: đảm bảo scenario phản ánh đúng yêu cầu nghiệp vụ |
| Threshold RQ3 | Reusability Score ≥ 70% | Mughal (2024): tập trung khả năng tái sử dụng scenario |
| Evaluation Method | Expert Review \+ Rubric Scoring | Fernandes et al. (2025), Wang et al. (2024) |
| Pipeline base | Requirement → Prompt → LLM → Gherkin → Evaluation | Fernandes et al. (2025), Patel et al. (2025) |

## **Giải thích Threshold**

### **Threshold RQ1 – Coverage ≥ 80%**

Coverage từ 80% trở lên được xem là mức phù hợp để sử dụng trong Acceptance Testing thực tế. Giá trị này được chọn nhằm bảo đảm phần lớn yêu cầu nghiệp vụ đã được phản ánh trong tập Gherkin.

---

### **Threshold RQ2 – Correctness ≥ 85%**

Một Gherkin có độ phủ cao nhưng chứa nhiều lỗi diễn giải sẽ không hữu ích trong thực tế. Vì vậy nghiên cứu đặt ngưỡng Correctness tối thiểu là 85%.

---

### **Threshold RQ3 – Reusability ≥ 70%**

Theo Mughal (2024), khả năng tái sử dụng là một trong những lợi ích chính của BDD. Do đó nghiên cứu sử dụng ngưỡng 70% để xác định liệu output từ LLM có đủ chất lượng để đưa vào framework BDD thực tế hay không.

