# Research Hypotheses & Statistical Analysis Plan

## 1. RQ1: Khả năng tạo mã kiểm thử khả thi (Syntax Correctness)
* $H_0$: Mô hình đề xuất  **KHÔNG** **ĐẠT** tỷ lệ kịch bản BDD chạy được ngay  > 85%  (**ĐẠT** trung bình $\le 85\%$).
* $H_1$: Mô hình đề xuất  **ĐẠT** tỷ lệ kịch bản BDD chạy được ngay  > 85% .
* **Statistical test dự kiến:** **Binomial exact test** (Alpha = 0.05). Kiểm định này được áp dụng trên phân phối nhị phân (Thành công/Thất bại khi thực thi kịch bản) nhằm xác định xem tỷ lệ kịch bản chạy được ngay mà không cần sửa lỗi (`% executable`) có thực sự vượt qua ngưỡng tối thiểu 85% hay không.

## 2. RQ2: Nâng cao độ bao phủ mã nguồn (Requirement & Code Coverage)
* $H_0$: Phương pháp LLM kết hợp RAG  **KHÔNG** **ĐẠT** mức cải thiện độ bao phủ mã nguồn hoặc điểm số cấu trúc  > 80% (hoặc F1-score > 0.85)  (**ĐẠT** trung bình `Statement Coverage` $\le 80\%$ hoặc `F1-score` $\le 0.85$).
* $H_1$: Phương pháp LLM kết hợp RAG  **ĐẠT** mức cải thiện độ bao phủ mã nguồn hoặc điểm số cấu trúc  > 80% (hoặc F1-score > 0.85) .
* **Statistical test dự kiến:** **Wilcoxon signed-rank test** (Alpha = 0.05). Đây là kiểm định phi tham số cho dữ liệu cặp (Paired data), dùng để so sánh sự chênh lệch có ý nghĩa thống kê về độ phủ code trên cùng một tập mẫu trước và sau khi được tối ưu hóa bằng RAG orchestrator.

## 3. RQ3: Hiệu suất và độ bền vững của kịch bản (Execution Sustainability)
* $H_0$: Kiến trúc Local Multi-Agent Ensemble  **KHÔNG** **ĐẠT** điểm số tương đồng ngữ nghĩa và tính bền vững  cao hơn so với kiến trúc Single-Model thông thường > 0.80  (Hiệu năng của nhóm Ensemble kém hơn, bằng, hoặc **ĐẠT** mức baseline cố định $\le 0.80$).
* $H_1$: Kiến trúc Local Multi-Agent Ensemble  **ĐẠT** điểm số tương đồng ngữ nghĩa và tính bền vững  cao hơn so với kiến trúc Single-Model thông thường > 0.80  (Hiệu năng trung bình của nhóm Ensemble lớn hơn rõ rệt so với nhóm Single-Model và vượt ngưỡng 0.80).
* **Statistical test dự kiến:** **Mann-Whitney U test** (Alpha = 0.05). Kiểm định phi tham số dành cho hai mẫu độc lập (Independent samples) nhằm so sánh và xác định xem phân phối hiệu năng đầu ra (`Cosine similarity` và độ bền vững kịch bản) của kiến trúc đề xuất có thực sự vượt trội hơn kiến trúc nền tảng hay không.