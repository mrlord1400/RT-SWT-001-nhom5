# GAP Statement Final - [LLM for Acceptance Test Automation (BDD/Gherkin)]

Evidence table: N = 55 paper | Ngày: 2026-06-16

## Bảng GAP

| Cột | Phát hiện | Loại GAP | Phản chứng |
| --- | --- | --- | --- |
| **Tool/LLM** | Thiếu các nghiên cứu thực nghiệm đánh giá toàn diện khả năng zero-shot của các frontier LLM trong việc chuyển đổi trực tiếp từ yêu cầu nghiệp vụ thô sang tài sản kiểm thử hoàn chỉnh (bao gồm kịch bản, logic thực thi và tạo artifact xác thực) chỉ trong một workflow tích hợp duy nhất. | **GAP-T** (Primary) | ✅ Kiểm tra 55/55 nghiên cứu không trùng lặp |
| **Dataset** | Phần lớn các nghiên cứu phụ thuộc vào các định dạng đầu vào đã được chuẩn hóa (như cấu trúc Connextra) hoặc kịch bản có sẵn, thiếu vắng bộ dữ liệu tham chiếu đa miền chứa các "yêu cầu nghiệp vụ thô" (raw business requirements) chưa qua xử lý làm đầu vào trực tiếp. | **GAP-D** | ✅ Kiểm tra 55/55 nghiên cứu không trùng lặp |
| **Metric** | Thiếu một hệ thống đo lường hợp nhất (Unified Metric) để đánh giá tỷ lệ thành công của luồng end-to-end zero-shot: từ việc hiểu đúng ngữ nghĩa kinh doanh thô đến tính biên dịch thực thi của mã tự động sinh ra. | **GAP-M** | ✅ Kiểm tra 55/55 nghiên cứu cùng bộc lộ hạn chế |
| **Hạn chế** | Các nghiên cứu hiện tại thường sử dụng kỹ thuật few-shot, fine-tuning, RAG hoặc kiến trúc multi-agent phức tạp để đạt hiệu năng cao, dẫn đến thiếu hụt đánh giá nền tảng về giới hạn thực sự của năng lực "zero-shot" cốt lõi trên các mô hình tiên tiến nhất. | **GAP-S** | ✅ Kiểm tra 55/55 nghiên cứu cùng bộc lộ hạn chế |

## GAP Chính: [GAP-T]

**Thiếu các nghiên cứu thực nghiệm đánh giá toàn diện khả năng zero-shot của các frontier LLM trong việc chuyển đổi trực tiếp từ yêu cầu nghiệp vụ thô sang tài sản kiểm thử hoàn chỉnh (bao gồm kịch bản, logic thực thi và tạo artifact xác thực) chỉ trong một workflow tích hợp duy nhất.**

## Lý do lựa chọn GAP Primary (GAP-T) làm trọng tâm nghiên cứu

Nghiên cứu tập trung tối đa vào GAP-T nhằm xác định năng lực nội tại và giới hạn thực tế của các Frontier LLM (như GPT-4o, Claude 3.5, Gemini 1.5 Pro) khi hoạt động độc lập không cần dữ liệu huấn luyện (zero-shot). Việc thay thế các pipeline phân mảnh, tinh chỉnh (fine-tuning) phức tạp hay RAG bằng một luồng quy trình (workflow) tích hợp duy nhất đi thẳng từ yêu cầu thô sơ đến bộ mã kiểm thử thực thi giúp tối ưu hóa triệt để tài nguyên, giảm thiểu độ trễ và đánh giá chính xác mức độ sẵn sàng ứng dụng thực tiễn của AI thế hệ mới trong tự động hóa kiểm thử phần mềm.

## Chi tiết kiểm tra phản chứng

| Paper | Đã làm không? | Ghi chú (Dựa trên hướng tiếp cận Zero-shot & Single Workflow) |
| --- | --- | --- |
| **1. Cypress Copilot (2025)** | Không | Chỉ sinh mã thử nghiệm từ kịch bản BDD có sẵn và phụ thuộc vào kỹ thuật "few-shot chain prompt" để đạt độ chính xác cao, không phải zero-shot từ yêu cầu thô. |
| **2. Fonseca et al. (2025)** | Không | Xây dựng pipeline kiểm thử phức tạp qua framework ATOMIC sử dụng mô hình local (DeepSeek, Gemma), không tập trung đánh giá zero-shot của frontier LLMs trong một workflow. |
| **3. Rosenbach et al. (2025)** | Không | Tập trung khám phá giao diện (GUI) và phát hiện lỗi bất thường, không sinh tài sản kiểm thử (BDD/Step Defs) từ yêu cầu nghiệp vụ thô. |
| **4. Sisomboon et al. (2026)** | Không | Phụ thuộc vào kiến trúc Ensemble LLM và RAG để đạt độ phủ kiểm thử, đi ngược lại với tiêu chí đánh giá zero-shot workflow đơn lẻ. |
| **5. Jagielski et al. (2025)** | Không | Sử dụng mô hình Deepseek-coder-v2 cục bộ kết hợp với pipeline RAG chuyên biệt thay vì zero-shot trực tiếp từ frontier LLMs. |
| **6. Jang & Kim (2025)** | Không | Chuyển đổi ngôn ngữ tự nhiên tiếng Hàn sang mô hình đồ thị/cây quyết định bằng các API riêng biệt (Mecab-ko, KRA), không sinh mã thực thi kiểm thử hoàn chỉnh. |
| **7. Karpurapu et al. (2024)** | Không | Có đánh giá zero-shot trên GPT-4 nhưng chỉ giới hạn ở việc kiểm tra cú pháp Gherkin (gây ra 89% lỗi), hoàn toàn thiếu cấu phần sinh đồng thời mã thực thi và artifact xác thực. |
| **8. Ferreira et al. (2025)** | Không | Mô hình AutoUAT sinh mã kiểm thử từ kịch bản Gherkin và JIRA issue có sẵn, không phải chuyển đổi trực tiếp một chạm từ yêu cầu thô. |
| **9. Cesa et al. (2025)** | Không | Giải quyết bài toán di trú module giao diện cũ (legacy) bằng metadata, không sinh tài sản kiểm thử từ yêu cầu nghiệp vụ. |
| **10. ZhBelo et al. (2026)** | Không | Cải thiện độ phủ khẳng định (assertion) cho UI workflows, không đánh giá năng lực zero-shot toàn vẹn từ yêu cầu thô. |
| **11. KumarMohri & Zhong (2025)** | Không | Đánh giá tỷ lệ biên dịch cú pháp Gherkin từ user story doanh nghiệp nhưng không thực hiện sinh logic thực thi trong cùng một luồng. |
| **12. Wu et al. (2026)** | Không | Phụ thuộc vào các mô hình được tinh chỉnh (Fine-tuned StarCoder, CodeGen), vi phạm điều kiện zero-shot. |
| **13. Qian (2026)** | Không | Tập trung thiết lập framework và assertions cho ứng dụng web, nhưng quy mô nhỏ và không đánh giá định lượng khả năng zero-shot tổng thể. |
| **14. Zhu et al. (2026)** | Không | Sinh môi trường mock và payload cho API, không sinh tài sản kiểm thử BDD hoàn chỉnh (kịch bản + Step Definitions). |
| **15. Ning et al. (2024)** | Không | Tối ưu hóa độ phủ cho microservices, không liên quan đến quy trình sinh mã zero-shot từ yêu cầu thô. |
| **16. Kumar et al. (2025)** | Không | Giảm tính dễ gãy của script qua bộ chọn element web, không phải là workflow sinh mã từ yêu cầu kinh doanh. |
| **17. Chen et al. (2020)** | Không | Chuyển đổi luật an toàn thành khẳng định hành vi dùng mô hình cục bộ (Llama-3-8B), không ứng dụng frontier LLM zero-shot cho kiểm thử tổng quát. |
| **18. Liu et al. (2024)** | Không | Đảo ngược quy trình từ mã nguồn cũ thành mã kiểm thử mới, không đi từ yêu cầu nghiệp vụ thô. |
| **19. Luo et al. (2017)** | Không | Sử dụng RAG để giảm ảo tưởng khi trích xuất yêu cầu, không phải cấu trúc zero-shot nguyên bản. |
| **20. Rathnayake (2026)** | Không | Đánh giá zero-shot GPT-4 nhưng chỉ đo lường độ tương đồng ngữ nghĩa văn bản của kịch bản BDD, không sinh logic thực thi. |
| **21. Tiwari (2025)** | Không | Phụ thuộc vào dữ liệu nhập thủ công và các công cụ truyền thống (Selenium, Cucumber), không tích hợp một workflow tự động duy nhất. |
| **22. Almeyda (2025)** | Không | Sinh kịch bản và mã từ User Stories nhưng gặp tỷ lệ lỗi cú pháp do ảo tưởng, chưa thiết lập đánh giá năng lực zero-shot chuyên sâu. |
| **23. Farchi (2025)** | Không | Dùng SBERT đo lường độ rõ ràng của yêu cầu, không cung cấp cơ chế sinh tự động tài sản kiểm thử thực thi. |
| **24. Hassani (2026)** | Không | Chỉ dịch điều luật an toàn thực phẩm thành đặc tả Gherkin, thiếu cấu phần sinh mã Step Definitions thực thi. |
| **25. Drechsler (2025)** | Không | Giới hạn trong sinh mô hình mô phỏng Verilog cho phần cứng (ALU), không áp dụng cho kiểm thử phần mềm tổng quát từ yêu cầu thô. |
| **26. Rumiantsev (2025)** | Không | Khôi phục và sửa các kiểm thử kế thừa (legacy tests), không sinh mới toàn bộ từ yêu cầu. |
| **27. Jagielski (2025)** | Không | Sử dụng RAG và đánh giá cục bộ trên bài toán Hello World/MNIST thay vì workflow zero-shot từ yêu cầu thô. |
| **28. Zyberaj (2026)** | Không | Ánh xạ yêu cầu hệ thống điều hòa thành tín hiệu VSS, hiệu năng bị suy giảm khi mở rộng, không là định dạng sinh kiểm thử BDD chuẩn hóa. |
| **29. Zyberaj (2025)** | Không | Đòi hỏi điều chỉnh thủ công và ánh xạ tín hiệu tùy chỉnh, đi ngược lại tiêu chí luồng tích hợp tự động toàn vẹn. |
| **30. Karpurapu (2024)** | Không | Đánh giá cú pháp Gherkin dạng few-shot, hoàn toàn bỏ qua việc sinh logic mã thực thi đồng thời. |
| **31. Ferreira (2025)** | Không | Chuyển đổi từ user story sang Gherkin bị tách rời với mã nguồn, không sinh đồng thời cặp artifact thực thi. |
| **32. Bahaweres & Hasanah (2025)** | Không | Chỉ đánh giá các công cụ kiểm thử GUI truyền thống (Selenium, Katalon), không sử dụng LLM. |
| **33. Tang et al. (2026)** | Không | Xây dựng môi trường sandbox để đo lường AI Agent, không phải framework thực thi zero-shot E2E. |
| **34. Raju & Leong (2025)** | Không | Đánh giá lý thuyết về sự chuyển dịch sang AI, không đề xuất workflow ứng dụng zero-shot thực tiễn. |
| **35. Garg (2015)** | Không | Tài liệu hướng dẫn thiết lập thủ công cấu trúc BDD nền tảng, không có yếu tố tự động hóa AI. |
| **36. Fernandes et al. (2025)** | Không | Chỉ định lượng khả năng dịch ngôn ngữ tự nhiên sang Gherkin, thành phần sinh mã thực thi hoàn toàn bị bỏ qua. |
| **37. Liu et al. (2025)** | Không | Chẩn đoán hành vi lặp mã để giảm lỗi cú pháp, không xây dựng quy trình E2E từ yêu cầu nghiệp vụ thô. |
| **38. Liang et al. (2025)** | Không | Phát hiện bản sao mã ngữ nghĩa trong Step Definitions, không phục vụ mục đích sinh mới tài sản kiểm thử. |
| **39. Mughal (2024)** | Không | Tối ưu tự động hoàn thành Gherkin lúc runtime, không tự động hóa chuyển đổi zero-shot từ văn bản thô. |
| **40. Walczak et al. (2025)** | Không | Khảo sát chiến lược prompt cho Unit Test, không thuộc phạm vi sinh Acceptance Test E2E trong một quy trình duy nhất. |
| **41. Ouyang et al. (2026)** | Không | Dùng mô hình thị giác (VLM) để phân tích biểu đồ UML, không xử lý văn bản yêu cầu nghiệp vụ thô. |
| **42. Kasaram (2023)** | Không | Đưa ra kiến trúc framework API thủ công, không ứng dụng mô hình LLM. |
| **43. Mughal & Bilal (2026)** | Không | Mở rộng kiểm thử BDD xuống tầng mạng (API bảo mật), không đáp ứng yêu cầu workflow sinh tự động tổng quát. |
| **44. Wang et al. (2024)** | Không | Xây dựng bộ dataset benchmark (TESTEVAL), không phải là quy trình workflow tích hợp tạo sinh mã trực tiếp. |
| **45. Thai et al. (2025)** | Không | Đánh giá năng lực của AI Agent trong việc bảo trì và sửa lỗi mã nguồn dài hạn, không phải quy trình zero-shot tạo mới. |
| **46. Haldar & Capretz (2026)** | Không | Chuyển đổi tài liệu PRD thô thành Test Plan ở cấp độ cao, không sinh mã BDD chi tiết và logic thực thi đi kèm. |
| **47. Mughal (2025)** | Không | Sử dụng tác tử học tăng cường (RL) để tự động điều hướng UI, không giải quyết bài toán sinh mã kiểm thử từ đầu vào. |
| **48. Patel et al. (2025)** | Không | Đảo ngược quy trình: dùng LLM để sinh đặc tả BDD từ mã nguồn cũ có sẵn, đi ngược với mục tiêu chuyển đổi từ yêu cầu sang mã. |
| **49. Chu et al. (2025)** | Không | Tổng quan lý thuyết về sinh kiểm thử đơn vị (Unit Test), chưa mở rộng đánh giá thực nghiệm cho E2E BDD. |
| **50. Chatterjee (2025a)** | Không | Tối ưu hóa việc chạy BDD trong đường ống CI/CD, tập trung vào hạ tầng thay vì quy trình sinh nội dung tự động. |
| **51. Chatterjee (2025b)** | Không | Ánh xạ mã nguồn chức năng thành kịch bản kiểm thử, không xuất phát từ việc hiểu yêu cầu nghiệp vụ thô zero-shot. |
| **52. Rehan et al. (2025)** | Không | Tập trung mở rộng quy mô thông qua điều phối prompt đa luồng, không tập trung vào đánh giá giới hạn zero-shot nguyên bản. |
| **53. Bahaweres et al. (2020)** | Không | Nghiên cứu thủ công triển khai BDD nền tảng e-commerce làm mốc tham chiếu, không tích hợp LLM tiên tiến. |
| **54. Sung et al. (2025)** | Không | Chuyển đổi luật lập trình thi đấu thuật toán thành khẳng định, không hỗ trợ định dạng BDD và hệ thống doanh nghiệp tổng quát. |
| **55. Murugan & Balamurugan (2025)** | Không | Xây dựng engine kiểm thử dạng "scriptless" giấu mã thực thi đi, đi ngược với nhu cầu sinh tường minh Step Definitions trong BDD. |

## Feasibility Check - GAP Chính

| Tiêu chí | Mức | Ghi chú |
| --- | --- | --- |
| **Dataset** | 🟢 | Đầu vào là các đoạn văn bản chứa yêu cầu nghiệp vụ thô (Raw Business Requirements), dễ tiếp cận và thu thập từ các dự án mã nguồn mở hoặc biên soạn nội bộ mà không cần gán nhãn định dạng phức tạp. |
| **Tool/API** | 🟢 | Chỉ yêu cầu lời gọi API trực tiếp (Zero-shot) tới các Frontier LLMs (như GPT-4o, Gemini 1.5 Pro, Claude 3.5 Sonnet). Không cần chi phí và thời gian huấn luyện hay tinh chỉnh (Fine-tuning). |
| **Compute** | 🟢 | Toàn bộ năng lực suy luận ngôn ngữ phụ thuộc vào hạ tầng đám mây của nhà cung cấp LLM; máy trạm cấu hình cơ bản là hoàn toàn đủ để gửi prompt và lưu file đánh giá. |
| **Ground truth** | ⚠️ | Yêu cầu cần có một bộ tiêu chuẩn đánh giá mã nguồn sinh ra (thông qua compiler hoặc test runner) để đo lường tự động tỷ lệ thực thi (Executability) của output. |
| **Skills** | 🟢 | Chỉ yêu cầu hiểu biết nền tảng về thiết kế prompt (Prompt Engineering cơ bản), thao tác API và cách thức vận hành của framework BDD. |
| **Thời gian** | 🟢 | Bỏ qua bước xây dựng RAG hoặc Fine-tuning phức tạp giúp rút ngắn đáng kể thời gian phát triển và thực nghiệm hệ thống. |
| **Contribution** | 🟢 | Cung cấp bằng chứng thực nghiệm tiên phong về giới hạn và năng lực độc lập của các mô hình AI mạnh nhất khi đối mặt với quy trình kiểm thử sinh lời trực tiếp từ ý tưởng kinh doanh. |
| **Kết quả:** ✅ --> Rất khả thi & Tính đổi mới cao |  |  |