**GAP Analysis -- LLM-Based Software Testing and Test Automation**

Evidence table: N = 11 paper \| Ngày: 2026-06-04

**Bảng GAP**

| **Cột** | **Phát hiện** | **Loại GAP** | **Phản chứng** |
|----|----|----|----|
| **Tool/LLM** | Đánh giá khả năng mô hình mã nguồn mở trong việc tự động tạo toàn diện tài sản kiểm thử hành vi end-to-end từ yêu cầu nghiệp vụ chuẩn hóa trong một quy trình thống nhất. | GAP-T | ✅ Kiểm tra 11 paper |
| **Dataset** | So sánh định lượng các thành phần kiểm thử được tạo ra với kết quả chuẩn của chuyên gia bằng các chỉ số tương đồng ngữ nghĩa dựa trên embedding để đo lường độ chính xác hành vi ở một ngưỡng tin cậy xác định. | GAP-M | ✅ Kiểm tra 11 paper |
| **Metric** | Đánh giá đồng thời cả độ chính xác ngữ nghĩa và độ chính xác thực thi thông qua một khung đánh giá kép (dual-evaluation framework) kết hợp điểm số tương đồng với xác thực tính thực thi tự động (biên dịch, runtime). | GAP-M | ✅ Kiểm tra 11 paper |
| **Hạn chế** | Các nghiên cứu hiện tại thường chỉ đánh giá độc lập tính hữu dụng của tác vụ, độ bao phủ, tính hợp lệ của cú pháp, hoặc đánh giá thủ công từ con người thay vì kết hợp các phép đo ngữ nghĩa và thực thi trong một khung đánh giá thống nhất. | GAP-S | ✅ Kiểm tra 8/11 paper |

**GAP Chính: \[GAP-M\]**

Hiện tại, các nghiên cứu thiếu một khung đánh giá định lượng nghiêm ngặt cho các quy trình kiểm thử tự động end-to-end do LLM tạo ra, nơi mà độ chính xác về mặt ngữ nghĩa (alignment với chuyên gia) và tính thực thi hợp lệ (executable correctness) được đo lường đồng thời và thống nhất.

**GAP Secondary (nếu có): \[GAP-T\]**

Thiếu các nghiên cứu thực nghiệm đánh giá toàn diện khả năng zero-shot của các frontier LLM trong việc chuyển đổi trực tiếp từ yêu cầu nghiệp vụ thô sang tài sản kiểm thử hoàn chỉnh (bao gồm kịch bản, logic thực thi và tạo artifact xác thực) chỉ trong một workflow tích hợp duy nhất.

**Lý do chọn GAP-M làm Primary**

Mặc dù GAP-T chỉ ra sự thiếu hụt các nghiên cứu đánh giá khả năng zero-shot của frontier LLM trong việc tạo tài sản kiểm thử end-to-end từ yêu cầu nghiệp vụ, GAP-M được lựa chọn làm khoảng trống nghiên cứu chính vì nó giải quyết trực tiếp vấn đề đánh giá chất lượng của các tài sản kiểm thử do LLM sinh ra.

Hiện nay, các nghiên cứu thường đánh giá riêng lẻ tính đúng đắn ngữ nghĩa hoặc khả năng thực thi, dẫn đến kết quả khó so sánh và chưa phản ánh đầy đủ chất lượng thực tế. Một khung đánh giá kép kết hợp semantic similarity và executable correctness có thể cung cấp phương pháp đánh giá định lượng thống nhất, áp dụng cho nhiều mô hình LLM khác nhau.

Do đó, GAP-M được ưu tiên làm khoảng trống nghiên cứu chính, trong khi GAP-T đóng vai trò bổ trợ thông qua việc cung cấp các mô hình LLM để kiểm chứng hiệu quả của khung đánh giá được đề xuất.

**Chi tiết kiểm tra phản chứng**

| **Paper** | **Đã làm không?** | **Ghi chú** |
|----|----|----|
| **Cesa et al., 2025** | **Không** | **Đo lường tính hợp lệ cú pháp (Syntactic validity) một cách độc lập; không chấm điểm tương đồng ngữ nghĩa qua embedding kết hợp với bộ kiểm tra runtime.** |
| **Belo et al., 2026** | **Không** | **Đo lường tính tuân thủ mã nguồn, độ chính xác của assertion và độ ổn định thực thi UI; thiếu phép đối sánh ngữ nghĩa tự động với ground-truth.** |
| **Li et al., 2025** | **Không** | **Sử dụng tỷ lệ biên dịch cú pháp Gherkin và độ chính xác logic; phép đánh giá tách rời tính đúng đắn cú pháp và không tích hợp semantic embedding.** |
| **Wu et al., 2026** | **Không** | **Đánh giá tính chính xác của việc dịch yêu cầu và tuân thủ step-definition; không xây dựng khung kiểm tra kép đồng thời giữa ngữ nghĩa và thực thi.** |
| **Qian, 2026** | **Không** | **Thử nghiệm riêng rẽ trên quy mô nhỏ về sự mạch lạc ngữ nghĩa và độ chính xác thực thi; không gộp chung thành một bộ dual-metric thống nhất.** |
| **Zhu et al., 2026** | **Không** | **Đo lường tỷ lệ xác thực chức năng và khớp schema API trong môi trường mock; không kiểm tra toàn diện quy trình kiểm thử hành vi end-to-end.** |
| **Ning et al., 2024** | **Không** | **Tập trung tối ưu hóa độ bao phủ và giảm thiểu test dư thừa trên microservice; không đánh giá tương đồng ngữ nghĩa đối với test assets của chuyên gia.** |
| **Kumar et al., 2025** | **Không** | **Hoàn toàn dựa trên cấu trúc DOM của UI để đo độ ổn định selector và tỷ lệ thực thi; không xuất phát từ việc diễn giải yêu cầu nghiệp vụ chuẩn hóa.** |
| **Chen et al., 2020** | **Không** | **Kiểm tra độ chính xác tuân thủ quy tắc và độ bao phủ cấu trúc; thiếu việc đo lường độ tương đồng ngữ nghĩa tự động dựa trên không gian vector embedding.** |
| **Liu et al., 2024** | **Không** | **Đánh giá dựa trên mã nguồn đảo ngược (reverse-engineered) và hệ thống live; không phải quy trình zero-shot tạo test assets từ tài liệu yêu cầu chuẩn hóa.** |
| **Luo et al., 2017** | **Không** | **Chỉ dừng lại ở mức trích xuất chính xác cấu trúc/văn bản bằng RAG; không tích hợp bộ parser/compiler để xác thực tính thực thi tự động song song.** |

**Kết luận phản chứng:** Kết luận phân tích phản chứng: Kết quả đối soát hệ thống khẳng định $100\%$ ($11/11$) nghiên cứu được khảo sát đều tồn tại sự phân mảnh nghiêm trọng trong phương pháp luận đánh giá. Hoàn toàn không có bất kỳ công trình nào thiết lập một khung đánh giá kép (Dual-metric Framework) cho phép đo lường đồng thời, đồng bộ giữa cấu trúc vector ngữ nghĩa (Semantic Embedding) dựa trên ground-truth với bộ kích hoạt thực thi runtime tự động (Compilation/Execution Success Rate) trong một quy trình zero-shot tích hợp. Do đó, khoảng trống nghiên cứu [GAP-M] được xác lập một cách tường minh và không bị trùng lặp.

**Feasibility Check -- GAP Chính**

| **Tiêu chí** | **Mức** | **Ghi chú** |
|----|----|----|
| Dataset | ✅ | Sử dụng các bộ dữ liệu công khai gồm User Stories và Agile Requirements như Mendeley User Story Dataset và Parabol Agile Dataset. Chọn 30–50 yêu cầu phần mềm làm tập thực nghiệm để sinh Test Cases và Selenium Scripts. https://data.mendeley.com/datasets/7zbk8zsd8y/2 |
| Tool/API | ✅ | Sử dụng hoàn toàn các mô hình mã nguồn mở (DeepSeek-Coder, Qwen-Coder, Gemma hoặc Llama) thông qua Ollama cục bộ; không phát sinh chi phí API thương mại. |
| Compute | ⚠️ | Nguy cơ tiềm ẩn: Việc tính toán ma trận Cosine Similarity diện rộng và khởi chạy liên tục các sandbox thực thi code (Compilation & Runtime validation) có thể gây thắt nút cổ chai về CPU/RAM trên máy cục bộ. Giải pháp: Thiết kế hàng đợi thực thi tuần tự (Task Queue) thay vì chạy song song đồng thời. |
| Ground truth | ⚠️ | Thách thức lớn: Việc xây dựng thủ công toàn bộ các bộ Test Cases và Selenium Scripts chuẩn mực (Expert-level code) ứng với $30 - 50$ User Stories làm nhãn đối chứng cực kỳ tốn công sức và dễ sai sót.Giải pháp: Sử dụng các public repositories có sẵn mã nguồn Web Java và hệ thống test suite đi kèm của chuyên gia trên GitHub để làm Ground-truth nguyên bản. |
| Skills | ✅ | Yêu cầu kỹ năng Python, Selenium, Ollama và prompt engineering ở mức trung bình. |
| Thời gian | ⚠️ | Rủi ro tiến độ: Quá trình tinh chỉnh bộ Parser/Compiler tự động để bắt các ngoại lệ Runtime (Runtime Exceptions) của code sinh ra có thể phát sinh nhiều bug ngoài dự kiến. Giải pháp: Dành riêng $2$ tuần đầu trong lộ trình làm bộ đệm (buffer) chỉ để chuẩn hóa và đóng gói môi trường biên dịch tự động. |
| Contribution | ✅ | Đánh giá tính khả thi của kiến trúc Local Multi-Agent chi phí thấp cho sinh kiểm thử tự động mà vẫn đảm bảo yêu cầu bảo mật dữ liệu. |

**Kết quả tổng hợp Feasibility:** [0] ❌ / [3] ⚠️ **Hệ thống có thách thức kỹ thuật nhưng kiểm soát được, đủ điều kiện triển khai.**
