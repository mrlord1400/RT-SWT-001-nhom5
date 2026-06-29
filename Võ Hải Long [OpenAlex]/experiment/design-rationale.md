# Experiment Design Rationale – [LLM for Acceptance Test Automation (BDD/Gherkin)]

Ngày: 2026-06-12 | GAP source: SLR/gap-analysis.md

## Bảng Quyết Định

| Quyết định | Giá trị | Nguồn gốc |
| --- | --- | --- |
| **LLM/Tool** | Gemini, DeepSeek (Thử nghiệm) vs OpenAI GPT-4o-mini (Baseline) | **Feasibility Check:** Cột Tool/API đề xuất sử dụng API của các mô hình LLM phổ biến hiện nay. |
| **Dataset** | E2EDev: Benchmarking Large Language Models in End-to-End Software Development Task | Benchmark |
| **Metric chính** | Cosine similarity (sentence-transformers với model all-MiniLM-L6-v2) | Farchi_2025, Rathnayaker_2026, Ferreira et al._2025 |
| **Metric phụ** | Executable rate (framework behave 1.2.6 (hoặc pytest-bdd) + subprocess capture) | Jagielski et al._2025, Karpurapu et al._2024, Nettur et al._2025, Fonseca et al._2025, Almeyda_2025 |
| **Baseline type** | Absolute threshold (Semantic Score ≥ 0.85). | Claim type RQ |
| **Threshold RQ1 (Semantic)** | ≥ 0.85 | **Case 3:** |
| **Threshold RQ2 (Executability)** | 85% | **Case 2:** floor = 85% từ Paper 18 (Liu et al., 2024) , threshold = 85% |
| **Pipeline base** | Streamlining Acceptance Test Generation for Mobile Applications Through Large Language Models: An Industrial Case Study (2025, IEEE/ACM ASE) | đây là paper duy nhất trong bảng có evaluation paradigm phân rã đúng 3 thành phần của gap: Gherkin (scenario), Page Objects/UI test code (execution logic), executability của UI test đó (validation) — đo bằng syntactic validity (93.3%) và execution success rate (100%). |

---

## Lý giải threshold

**Threshold ≥ 0.85 Semantic Similarity – Case 3**
**Lý luận:** 
Dữ liệu đối chiếu từ Evidence Table: Rà soát các nghiên cứu liên quan đến độ đo tương đồng ngữ nghĩa trong bảng tổng hợp:  
Paper 23 (Farchi, 2025) có sử dụng thước đo SBERT cosine similarity để đối chiếu, nhưng kết quả chỉ báo cáo tỷ lệ phần trăm cải thiện tương đối (tăng 55% tính khả kiểm - testability) chứ không cung cấp điểm số tuyệt đối làm mức nền.  
Paper 20 (Rathnayake, 2026) có đánh giá Text/Semantic similarity nhưng lại báo cáo kết quả dựa trên thang điểm đánh giá của con người (đạt 4.63/5) thay vì một ngưỡng hệ số Cosine từ 0.0 đến 1.0.  
Xác định Threshold: Do các nghiên cứu hiện tại trong Literature Review không báo cáo kết quả số cụ thể (absolute score) cho độ đo Cosine Similarity để có thể trích xuất mức sàn (floor value), trường hợp này rơi vào Case 3. Việc tự ý thiết lập ngưỡng 0.85 mà không có nguồn tham chiếu trực tiếp là vi phạm quy tắc xây dựng giả thuyết.
Cách làm thực tế: Thay vì ấn định trước một con số, ngưỡng Threshold chính thức cho RQ1 sẽ được xác định thông qua một đợt chạy thử nghiệm sơ bộ (mini-pilot PRE-PROPOSAL). Nghiên cứu sẽ trích xuất và chạy thử 5–10 sample thủ công bằng phương pháp zero-shot, tính toán điểm Cosine Similarity trung bình thấp nhất đạt mức chấp nhận được, và sử dụng giá trị thực nghiệm này làm ngưỡng (Threshold) cho giai đoạn đánh giá chính thức.

**Threshold 90% Pass Rate (Executability) – Case 2 – floor = 89% từ Paper 28 (Zyberaj, 2026), threshold = 90% (làm tròn)**
**Lý luận:**
Lọc hệ tham chiếu: Bảng Evidence Table ghi nhận các tỷ lệ pass rate dao động rất lớn, từ 11% (zero-shot cú pháp - Paper 7), 60% (kịch bản web đơn giản - Paper 8), đến 91.9% (User story - Paper 22). Vì RQ2 tập trung vào các kịch bản thực thi thực tế (end-to-end execution logic) từ các yêu cầu nghiệp vụ phức tạp, ta chỉ xét các kết quả đại diện cho việc sinh mã end-to-end/business-driven.
Xác định mức sàn: Trong nhóm này, Paper 18 (Liu et al., 2024) đại diện cho mức sàn (floor value) của khả năng sinh executable end-to-end tests thực tế, đạt 85%. Các nghiên cứu cao hơn như Paper 28 đạt 89% và Paper 22 đạt 91.9%.
Kết luận Threshold: Áp dụng quy tắc Case 2, ta lấy kết quả thấp nhất trong nhóm tham chiếu tương đương: floor = 85%, threshold = 85%.