**GAP Analysis – LLM-based BDD Test Generatio** 

Evidence table: N \= 24 papers | Ngày: 2026-06-08

---

## **Bảng GAP**

| Cột | Phát hiện | Loại GAP | Phân chứng |
| ----- | ----- | ----- | ----- |
| Tool/LLM | Nhiều nghiên cứu sử dụng LLM để sinh Gherkin hoặc BDD artifacts (Fernandes 2025, Patel 2025, Murugan 2025\) nhưng chưa có sự đánh giá nhất quán giữa các mô hình LLM hiện đại trên cùng bộ yêu cầu phần mềm và cùng tiêu chí đánh giá. | GAP-T | ✓ Fernandes et al. (2025), Patel et al. (2025), Murugan & Balamurugan (2025) |
| Dataset | Hầu hết nghiên cứu sử dụng dataset riêng hoặc case study đơn lẻ; thiếu benchmark chuẩn cho yêu cầu phần mềm dùng trong sinh Gherkin/Test Case BDD. | GAP-D | ✓ Fernandes et al. (2025), Wang et al. (2024), Bahaweres et al. (2020) |
| Metric | Nhiều nghiên cứu đánh giá bằng tính đúng cú pháp hoặc tính khả thi thực thi, nhưng ít nghiên cứu đánh giá đồng thời Coverage, Correctness, Completeness và Reusability của test case sinh bởi LLM. | GAP-M | ✓ Wang et al. (2024), Fernandes et al. (2025), Mughal (2024) |
| Hạn chế | Chưa có nghiên cứu thực nghiệm đầy đủ so sánh chất lượng BDD/Test Case được tạo bởi các LLM khác nhau với phương pháp thủ công trong bối cảnh Acceptance Testing thực tế. | GAP-S | ✓ Fernandes et al. (2025), Wang et al. (2024), Rehan et al. (2025) |

---

# **GAP Chính \[GAP-T/M/D\]**

Mặc dù các nghiên cứu gần đây đã chứng minh khả năng của Large Language Models trong việc tự động sinh Gherkin scenarios và BDD artifacts từ yêu cầu phần mềm, nhưng vẫn thiếu một framework thực nghiệm chuẩn để đánh giá và so sánh chất lượng đầu ra của các LLM khác nhau trên cùng một tập requirements với các tiêu chí toàn diện như Coverage, Correctness, Completeness và Reusability.

---

# **GAP Secondary \[GAP-S\]**

Các nghiên cứu hiện tại chủ yếu tập trung vào khả năng sinh Gherkin hoặc tối ưu hóa framework BDD, trong khi còn thiếu bằng chứng thực nghiệm về mức độ thay thế hoạt động viết test thủ công của tester trong quy trình Acceptance Testing thực tế.

---

# **Chi tiết kiểm tra bằng chứng**

### **Fernandes et al. (2025)**

* So sánh nhiều LLM sinh Gherkin.  
* Tập trung vào khả năng generate.  
* Chưa xây dựng benchmark chuẩn cho Acceptance Testing.  
* Chưa đối chiếu với test case thủ công.

### **Mughal (2024)**

* Tập trung auto-complete và tái sử dụng scenario.  
* Không đánh giá nhiều mô hình LLM.  
* Không đo coverage thực tế.

### **Patel et al. (2025)**

* Reverse engineering source code thành BDD.  
* Tập trung đặc tả hành vi.  
* Không so sánh với manual testing.

### **Murugan & Balamurugan (2025)**

* Scriptless BDD.  
* Tập trung coverage enhancement.  
* Không benchmark đa LLM.

### **Wang et al. (2024)**

* Benchmark test generation.  
* Chủ yếu đánh giá test generation tổng quát.  
* Chưa tập trung riêng cho BDD/Gherkin Acceptance Testing.

---

# **Feasibility Check – GAP Chính**

| Tiêu chí | Mức | Ghi chú |
| ----- | ----- | ----- |
| Dataset | ✅ | Có thể sử dụng User Stories/Requirements từ các hệ thống mẫu (Swag Labs, CURA, Open Source Projects) |
| Tool/API | ✅ | GPT-4o, Gemini, Claude, DeepSeek, Llama đều có thể truy cập |
| Compute | ✅ | Không yêu cầu tài nguyên lớn |
| Ground truth | ⚠️ | Cần tester hoặc chuyên gia xây bộ Gherkin chuẩn để đối chiếu |
| Skills | ✅ | Phù hợp với năng lực sinh viên ngành SE/QA |
| Thời gian | ✅ | Hoàn thành trong phạm vi đồ án hoặc luận văn |
| Contribution | ✅ | Đóng góp rõ ràng cho lĩnh vực AI-assisted Acceptance Testing |

**Kết quả:** ✅ Khả thi cao và có đóng góp nghiên cứu rõ ràng.

