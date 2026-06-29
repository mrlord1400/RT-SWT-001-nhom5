# Experiment Design Rationales – Dual-Evaluation Framework for Local LLM-Based Test Automation
Ngày: 2026-06-14 | GAP source: SLR/gap-analysis.md

## ## Bảng Quyết Định

| Quyết định | Giá trị | Nguồn gốc |
| :--- | :--- | :--- |
| LLM/Tool | Ollama v0.1.30 (DeepSeek-Coder-7B, Qwen-Coder-7B) | GAP-T: cột Tool/LLM |
| Dataset | Mendeley User Story Dataset (30–50 Agile Requirements) | GAP-D / benchmark |
| Metric chính | Semantic Cosine Similarity (Thư viện: `scikit-learn v1.4.0`) | GAP-M: cột Metric |
| Metric phụ | Executable Correctness Rate (ECR) (`Selenium v4.18.0` + `JUnit 5`) | Kế thừa tư duy Verifiable Reward của [Wu et al., 2026] |
| Baseline type | Llama-3-8B-Instruct (System baseline) | Relative Claim cho RQ2 |
| Threshold RQ1 | Semantic Cosine Similarity $\ge 0.85$ | Case 2: Floor value từ phân tích pilot văn bản nghiệp vụ |
| Threshold RQ2 | Executable Correctness Rate (ECR) $\ge 0.70$ | Case 2: Floor value kế thừa từ tỷ lệ lỗi runtime của mã Selenium |
| Pipeline base | Fault-Tolerant Analyzer-Rewriter Engine [Li et al., 2025] | [Lý do chọn]: Làm nền tảng cho vòng lặp sửa mã tự động |

---

## ## Lý giải threshold (ghi 1 đoạn cho mỗi threshold)

* **[Threshold 85% – Case 2 – floor = 85% từ phân tích pilot nghiệp vụ]:** Ngưỡng tương đồng ngữ nghĩa được đặt ở mức sàn tối thiểu là 0.85 dựa trên các kiểm định pilot đối sánh văn bản kịch bản Gherkin được sinh ra với User Story gốc. Do đặc thù đặc tả Agile mang tính cô đọng cao, bất kỳ sự sụt giảm vector nhúng nào dưới mức 0.85 đều phản ánh hiện tượng mất mát các thực thể nghiệp vụ cốt lõi hoặc làm sai lệch các bước tiền điều kiện (`Given-When-Then`), khiến test suite không còn khớp với mục tiêu ban đầu của chuyên gia.

* **[Threshold 70% – Case 2 – floor = 70% từ tư duy kiểm định thực thi của Wu et al., 2026]:** Ngưỡng thực thi mã kiểm thử (ECR) được thiết lập ở mức sàn 70% nhằm thích ứng với các phản hồi lỗi Runtime khi chạy Selenium WebDriver trên môi trường sandbox. Mức sàn này chấp nhận một tỷ lệ nhiễu nhỏ từ hạ tầng hoặc độ trễ tải trang cục bộ (UI Flakiness), nhưng cam kết lõi cấu trúc logic của kịch bản kiểm thử (`JUnit assertions`) phải biên dịch thành công và vượt qua tối thiểu 70% tổng số bước tương tác mà không gây crash hệ thống đột ngột.

---

## ## Liệt kê thay đổi của Pipeline so với Base Paper

Hệ thống thực nghiệm kế thừa kiến trúc vòng lặp Phân tích - Sửa lỗi (Analyzer-Rewriter Engine) từ nghiên cứu gốc của *Li et al., 2025*, tuy nhiên có những điều chỉnh cốt lõi để thích ứng với bài toán sinh mã kiểm thử UI trên môi trường cục bộ:

1. **Thay đổi miền tác vụ (Domain Adaptation):** Pipeline gốc của *Li et al., 2025* tập trung vào sửa mã cứng RTL (VHDL/Verilog) dựa trên lỗ hổng phần cứng do GNN phát hiện. Pipeline đề xuất được chuyển đổi hoàn toàn sang miền kiểm thử phần mềm: Nhận đầu vào là Agile User Stories, sinh mã kịch bản hành vi Gherkin, sau đó chuyển dịch thành mã thực thi `Selenium/JUnit 5`.
2. **Cơ chế hàng đợi Task Queue trên Ollama:** Khác với việc gọi các API đám mây phân tán hoặc chạy xử lý tĩnh, pipeline này bổ sung một hàng đợi tuần tự (`Task Queue`) độc lập nhằm điều phối dòng dữ liệu vào `Ollama v0.1.30`. Thay đổi này giúp cô lập tài nguyên phần cứng, ngăn ngừa hiện tượng nghẽn tài nguyên CPU/RAM cục bộ khi mô hình tính toán nhúng vector đặc trưng đồng thời với tiến trình kích hoạt trình duyệt sandbox chạy test UI tự động.