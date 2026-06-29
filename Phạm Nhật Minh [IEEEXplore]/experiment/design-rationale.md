# Experiment Design Rationale – Zero-shot LLM Test Asset Generation
Ngày: 2026-06-14 | GAP source: SLR/gap-analysis.md

## Bảng Quyết Định

| Quyết định | Giá trị | Nguồn gốc |
|------------|---------|-----------|
| LLM/Tool | GPT-4o (gpt-4o-2024-05-13) & Claude 3.5 Sonnet (claude-sonnet-20240620) | GAP-T: cột Tool/LLM – hai frontier LLM phổ biến nhất hiện tại, phù hợp để đánh giá khả năng zero-shot trên cùng điều kiện |
| Dataset | 10–15 kịch bản nghiệp vụ thô (Raw Business Requirements) tự xây dựng: đăng nhập OTP, thanh toán VNPay, quản lý giỏ hàng, v.v. | GAP-D: không tồn tại benchmark chuẩn cho task chuyển đổi requirement → test asset; dataset tự xây dựng là lựa chọn bắt buộc và hợp lệ về mặt nghiên cứu |
| Metric chính | Requirement Coverage Rate (%) – tỷ lệ quy tắc nghiệp vụ trong requirement gốc được ánh xạ thành test case; đánh giá bằng manual inspection (2 người chấm độc lập theo checklist) | GAP-M: cột Metric – độ phủ là chỉ số trực tiếp và đo được nhất cho khả năng zero-shot generation trong phạm vi 4 tuần |
| Metric phụ | Semantic Correctness (Yes/No per scenario), Syntax Validity – manual inspection (Yes/No), Artifact Completeness (Yes/No), Traceability/Alignment (Yes/No) | Kế thừa từ framework đánh giá LLM output quality (Liu et al., 2023; Kang et al., 2023) |
| Baseline type | threshold – ngưỡng tối thiểu chấp nhận được cho từng metric, không so sánh với hệ thống khác | Claim type RQ: RQ đánh giá mức độ đủ dùng trong thực tế (sufficiency claim), không phải comparative claim |
| Threshold RQ1 | ≥ 80% Requirement Coverage Rate | Case 2: ngưỡng 80% được sử dụng rộng rãi trong industry QA practice như mức "acceptable coverage" trước khi release; thấp hơn 80% đồng nghĩa LLM bỏ sót quá nhiều nghiệp vụ, không thể dùng thực tế |
| Threshold RQ2 | ≥ 70% Syntax Validity (code không có lỗi cú pháp rõ ràng qua manual inspection) | Case 2: floor tham chiếu từ HumanEval pass@1 baseline của GPT-4 (~67%, Chen et al., 2021); đặt 70% để phản ánh yêu cầu cao hơn của task domain-specific so với benchmark tổng quát |
| Pipeline base | Single-turn Zero-shot Workflow: input là Raw Business Requirement, output là Test Asset Bundle (scenarios + execution logic + validation artifact) trong 1 lượt gọi duy nhất qua web interface | Trực tiếp từ GAP Secondary: thiếu nghiên cứu đánh giá end-to-end integrated single-shot workflow – pipeline này được chọn để lấp đúng GAP đã xác định |

## Lý giải threshold (1 đoạn cho mỗi threshold)

**Threshold RQ1 – Coverage Rate ≥ 80% – Case 2 – floor = 80% từ industry QA practice.**
Lý luận: Ngưỡng 80% requirement coverage được sử dụng rộng rãi trong thực tiễn kiểm thử phần mềm như mức tối thiểu để một bộ test case được chấp nhận trước giai đoạn release (Ammann & Offutt, 2016 – *Introduction to Software Testing*). Đây không phải ngưỡng lý tưởng mà là mức floor thực tế: (1) dưới 80%, LLM bỏ sót hơn 1/5 quy tắc nghiệp vụ – quá nhiều để chấp nhận dù có human review sau đó; (2) ngưỡng này cho phép so sánh kết quả của thực nghiệm với kỳ vọng trong môi trường doanh nghiệp thực tế, tăng tính ứng dụng của nghiên cứu.

**Threshold RQ2 – Syntax Validity ≥ 70% – Case 2 – floor tham chiếu từ HumanEval pass@1 baseline (Chen et al., 2021).**
Lý luận: Chen et al. (2021) công bố GPT-4 đạt ~67% pass@1 trên HumanEval – benchmark code generation tổng quát. Task trong thực nghiệm này có yêu cầu cao hơn vì code phải ánh xạ 1-1 với kịch bản nghiệp vụ cụ thể, không phải giải bài toán thuật toán chung. Do đó ngưỡng được đặt ở 70% – nhích cao hơn baseline tổng quát để phản ánh độ khó tăng thêm, đồng thời vẫn đủ thực tế: 70% code không có lỗi cú pháp là mức mà đội QA có thể chấp nhận với chi phí post-editing hợp lý. Lưu ý: do giới hạn thời gian 4 tuần, Syntax Validity được đánh giá bằng manual inspection (đọc code, kiểm tra cú pháp bằng mắt) thay vì chạy thực thi – điều này sẽ được ghi rõ là giới hạn của nghiên cứu (limitation).


