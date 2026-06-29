# GAP Analysis - [LLM for Acceptance Test Automation (BDD/Gherkin)]
Evidence table: N = 55 paper | Ngày: 2026-06-10

## Bảng GAP

| Cột | Phát hiện | Loại GAP | Phản chứng |
|-----|-----------|----------|------------|
| **Tool/LLM** | Các nghiên cứu hiện tại bị tách rời cấu phần (chỉ sinh đơn lẻ Gherkin hoặc mã kiểm thử từ kịch bản có sẵn). Thiếu quy trình tự động toàn vẹn (End-to-End) từ việc kiểm soát định dạng đầu vào (chuẩn Connextra) đến việc sinh đồng thời cả kịch bản Gherkin lẫn mã Step Definitions thực thi không lỗi cú pháp. | **GAP-T** | ✅ Kiểm tra 55/55 nghiên cứu không trùng lặp |
| **Dataset** | Thiếu vắng bộ dữ liệu tham chiếu chuẩn hóa đa miền (Multi-domain Golden Dataset) cô lập riêng định dạng Connextra được thiết kế và xác thực thủ công bởi chuyên gia nhằm làm hệ quy chiếu (baseline) đối chứng trực tiếp. | **GAP-D** | ✅ Kiểm tra 55/55 nghiên cứu không trùng lặp |
| **Metric** | Chưa có khung đánh giá kép thiết lập ngưỡng định lượng tự động nhằm đo lường đồng thời cả độ tương đồng ngữ nghĩa (như ngưỡng Semantic Similarity >= 0.85 bằng SBERT) song hành cùng tính biên dịch/thực thi (Executability) của mã BDD sinh ra. | **GAP-M** | ✅ Kiểm tra 55/55 nghiên cứu cùng bộc lộ hạn chế |
| **Hạn chế** | Các nghiên cứu bộc lộ rủi ro cao về lỗi ảo giác cú pháp nhỏ (syntax hallucinations) hoặc suy thoái hiệu năng khi đối mặt với quy trình nghiệp vụ lồng nhau phức tạp, đồng thời thiếu một nền tảng đối chứng thực nghiệm với kịch bản BDD do con người viết thủ công (Manual Baseline). | **GAP-S** | ✅ Kiểm tra 55/55 nghiên cứu cùng bộc lộ hạn chế |

## GAP Chính: [GAP-T]

Các nghiên cứu hiện tại bị tách rời cấu phần (chỉ sinh đơn lẻ Gherkin hoặc mã kiểm thử từ kịch bản có sẵn). Thiếu quy trình tự động toàn vẹn (End-to-End) từ việc kiểm soát định dạng đầu vào (chuẩn Connextra) đến việc sinh đồng thời cả kịch bản Gherkin lẫn mã Step Definitions thực thi không lỗi cú pháp.

## Lý do lựa chọn GAP Primary (GAP-T) làm trọng tâm nghiên cứu

Nghiên cứu tập trung tối đa vào GAP-T nhằm phá vỡ sự phân mảnh của các nghiên cứu trước bằng cách xây dựng một pipeline tự động hóa toàn vẹn (End-to-End) từ User Story chuẩn Connextra đến việc sinh đồng thời cả kịch bản Gherkin và mã Step Definitions. Hướng đi này tối ưu hóa tài nguyên triển khai của nhóm thông qua việc tận dụng các API và hạ tầng tính toán trong vùng khả thi, giúp loại bỏ hoàn toàn các nguy cơ thắt nút (Blocker) về mặt thời gian và chuyên gia so với việc xây dựng dữ liệu lớn.

## Chi tiết kiểm tra phản chứng
| Paper | Đã làm không? | Ghi chú |
| :--- | :--- | :--- |
| **1. Cypress Copilot (2025)** | Không | Chỉ sinh mã thử nghiệm (Step/POM methods) từ kịch bản BDD có sẵn; cấu phần bị tách rời và không kiểm soát định dạng câu lệnh Connextra từ đầu vào. |
| **2. Fonseca et al. (2025)** | Không | Framework ATOMIC sinh pipeline kiểm thử từ JIRA issues và GitHub commits cho ứng dụng Flutter; không thiết lập cơ chế kiểm soát và chuẩn hóa định dạng Connextra đầu vào. |
| **3. Rosenbach et al. (2025)** | Không | Tập trung phát hiện lỗi GUI bất thường qua framework GERALLT; không hỗ trợ quy trình tự động toàn vẹn sinh kịch bản Gherkin và Step Definitions đồng thời. |
| **4. Sisomboon et al. (2026)** | Không | Tập trung vào việc đo lường độ phủ yêu cầu thông qua mô hình cấu hình Ensemble; không xây dựng quy trình sinh đồng thời hai cấu phần Gherkin và Step Defs. |
| **5. Jagielski et al. (2025)** | Không | Đánh giá prompt cú pháp Gherkin so với ngôn ngữ tự nhiên cho mã Python/TensorFlow; thiếu cơ chế kiểm soát định dạng đầu vào tổng thể. |
| **6. Jang & Kim (2025)** | Không | Phân tích cấu trúc câu tiếng Hàn phi cấu trúc để tạo mô hình đồ thị/cây quyết định; không hỗ trợ sinh mã Step Definitions thực thi đồng thời. |
| **7. Karpurapu et al. (2024)** | Không | Chỉ tập trung chuyển đổi từ user story sang văn bản cú pháp Gherkin và đo lường lỗi; hoàn toàn thiếu cấu phần sinh đồng thời mã Step Definitions thực thi. |
| **8. Ferreira et al. (2025)** | Không | Mô hình AutoUAT sinh mã kiểm thử TypeScript từ kịch bản Gherkin và JIRA issue có sẵn; quy trình mang tính tách rời cấu phần và không kiểm soát định dạng Connextra. |
| **9. Cesa et al. (2025)** | Không | Tập trung vào tốc độ di trú module giao diện cũ và tỷ lệ phát hiện hồi quy; không thuộc phạm vi quy trình sinh kịch bản BDD tự động từ yêu cầu đầu vào. |
| **10. ZhBelo et al. (2026)** | Không | Tập trung cải thiện độ phủ khẳng định (assertion) và xử lý tương tác UI bất đồng bộ; không nghiên cứu quy trình sinh BDD đồng thời không lỗi cú pháp. |
| **11. KumarMohri & Zhong (2025)** | Không | Chỉ đánh giá tỷ lệ biên dịch cú pháp Gherkin từ các user story doanh nghiệp; không thực hiện sinh mã thực thi song song. |
| **12. Wu et al. (2026)** | Không | Chuyển đổi tài liệu yêu cầu kinh doanh phi cấu trúc thành framework kiểm thử; chưa có bộ kiểm soát định dạng câu lệnh Connextra nghiêm ngặt ở đầu vào. |
| **13. Qian (2026)** | Không | Tập trung giảm thời gian và công sức thiết lập framework cho luồng hành vi ứng dụng web; quy trình quy mô nhỏ và không kiểm soát định dạng Connextra. |
| **14. Zhu et al. (2026)** | Không | Sinh cấu trúc môi trường mock và payload cho API; không hỗ trợ quy trình sinh đồng thời kịch bản Gherkin và Step Definitions cho luồng hành vi UI. |
| **15. Ning et al. (2024)** | Không | Tối ưu hóa độ phủ và loại bỏ kiểm thử dư thừa cho microservice không trạng thái; không liên quan đến sinh mã BDD đồng thời từ định dạng đầu vào. |
| **16. Kumar et al. (2025)** | Không | Tập trung giảm tính dễ gãy của script qua việc sinh bộ chọn element ổn định trên layout web; không phải là quy trình E2E sinh BDD từ yêu cầu. |
| **17. Chen et al. (2020)** | Không | Chuyển đổi quy định an toàn thành khẳng định hành vi; tập trung vào văn bản quy phạm pháp luật, thiếu quy trình kiểm soát định dạng Connextra đầu vào. |
| **18. Liu et al. (2024)** | Không | Đảo ngược quy trình để hiểu và tạo mã kiểm thử cho module cũ không có tài liệu; không đi từ yêu cầu định dạng Connextra đầu vào để sinh mã mới. |
| **19. Luo et al. (2017)** | Không | Sử dụng RAG để giảm tỷ lệ ảo tưởng khi trích xuất yêu cầu doanh nghiệp; thiếu cơ chế sinh đồng thời kịch bản và mã thực thi không lỗi. |
| **20. Rathnayake (2026)** | Không | Chỉ đánh giá văn bản kịch bản BDD dựa trên độ tương đồng ngữ nghĩa bằng LLM và con người; không tích hợp sinh mã thực thi đồng thời. |
| **21. Tiwari (2025)** | Không | Triển khai kiểm thử từ luật kinh doanh và user story có sẵn; phụ thuộc vào dữ liệu nhập thủ công, không tự động kiểm soát định dạng đầu vào toàn vẹn. |
| **22. Almeyda (2025)** | Không | Sinh kịch bản và mã từ User Stories nhưng vẫn gặp tỷ lệ lỗi cú pháp (8.1%) do ảo tưởng LLM; chưa tối ưu hóa quy trình đồng thời để đảm bảo không lỗi. |
| **23. Farchi (2025)** | Không | Tập trung đo lường độ rõ ràng và tính kiểm thử của yêu cầu bằng SBERT và biểu mẫu đánh giá; thiếu hệ thống sinh mã thực thi tự động đồng thời. |
| **24. Hassani (2026)** | Không | Chuyển đổi điều luật an toàn thực phẩm thành đặc tả Gherkin; tập trung dịch thuật văn bản quy định, thiếu sinh mã Step Definitions thực thi. |
| **25. Drechsler (2025)** | Không | Tự động sinh mô hình Verilog và kịch bản Gherkin cho ALU 16-bit từ đặc tả; giới hạn trong mô phỏng phần cứng đơn lẻ, không áp dụng cho phần mềm tổng quát. |
| **26. Rumiantsev (2025)** | Không | Khôi phục và sửa chữa các kiểm thử kế thừa bị lỗi bằng framework MSpec; tập trung sửa lỗi cũ, không sinh mới E2E từ định dạng Connextra. |
| **27. Jagielski (2025)** | Không | Thử nghiệm cục bộ với prompt Gherkin trên bài toán Hello World và MNIST; thiếu hệ thống kiểm soát và chuẩn hóa đầu vào theo chuẩn Connextra. |
| **28. Zyberaj (2026)** | Không | Ánh xạ yêu cầu CPDS sang danh mục VSS cho hệ thống HVAC; hiệu năng giảm khi danh mục lớn, không hỗ trợ định dạng Connextra tổng quát. |
| **29. Zyberaj (2025)** | Không | Sinh Gherkin và Python từ lưu đồ yêu cầu HVAC; đòi hỏi điều chỉnh thủ công và ánh xạ tín hiệu VSS tùy chỉnh, cấu phần bị tách rời. |
| **30. Karpurapu (2024)** | Không | Đánh giá lỗi cú pháp Gherkin của các mô hình dưới dạng few-shot; hoàn toàn thiếu cấu phần sinh mã Step Definitions thực thi đồng thời. |
| **31. Ferreira (2025)** | Không | Đánh giá độ hữu dụng và tính chính xác cú pháp từ user story sang Gherkin; quy trình tách rời, không sinh đồng thời cặp artifact thực thi không lỗi. |
| **32. Bahaweres & Hasanah (2025)** | Không | Đánh giá thực nghiệm các công cụ kiểm thử GUI truyền thống như Selenium IDE, UiPath; chỉ đóng vai trò làm nền tảng so sánh, không tích hợp LLM. |
| **33. Tang et al. (2026)** | Không | Cung cấp môi trường sandbox DevOps-Gym để đánh giá năng lực của AI Agent; là nền tảng đo lường hiệu năng, không phải framework sinh mã E2E. |
| **34. Raju & Leong (2025)** | Không | Nghiên cứu lý thuyết về sự chuyển dịch kiến trúc kiểm thử từ deterministic sang AI; không đề xuất hay cài đặt quy trình tự động cụ thể. |
| **35. Garg (2015)** | Không | Sách hướng dẫn thiết lập các mẫu cấu trúc BDD nền tảng với Cucumber; không chứa quy trình tự động hóa hay điều khiển bằng LLM. |
| **36. Fernandes et al. (2025)** | Không | Định lượng khả năng dịch thuật ngữ nghĩa từ yêu cầu tự nhiên sang cấu trúc Gherkin; thành phần mã nguồn bị tách rời, không sinh mã Step Defs. |
| **37. Liu et al. (2025)** | Không | Chẩn đoán hành vi lặp lại của LLM để giảm ảo tưởng cú pháp; không xây dựng quy trình tự động hóa kiểm soát định dạng Connextra đầu vào. |
| **38. Liang et al. (2025)** | Không | Phát hiện bản sao mã ngữ nghĩa trong Step Definitions để tối ưu bảo trì; không tập trung vào quy trình sinh mới E2E từ yêu cầu. |
| **39. Mughal (2024)** | Không | Triển khai cơ chế tự động hoàn thành câu lệnh Gherkin và tối ưu tái sử dụng kịch bản lúc runtime; không sinh mã thực thi đồng thời từ yêu cầu. |
| **40. Walczak et al. (2025)** | Không | Khảo sát chiến lược prompt để tối ưu hóa tính chính xác cấu trúc của kiểm thử đơn vị (Unit Test); không thuộc phạm vi kiểm thử chấp nhận BDD. |
| **41. Ouyang et al. (2026)** | Không | Dùng mô hình thị giác (VLM) để phân tích biểu đồ UML sang luồng BDD; thiếu cấu phần sinh đồng thời mã Step Definitions thực thi không lỗi. |
| **42. Kasaram (2023)** | Không | Đưa ra bản thiết kế kiến trúc thủ công cho framework kiểm thử API kết hợp Cucumber và REST Assured; không tự động hóa sinh mã bằng LLM. |
| **43. Mughal & Bilal (2026)** | Không | Mở rộng kiểm thử BDD xuống tầng mạng để giám sát bảo mật và đánh giá chất lượng API; tập trung vào an ninh mạng, không sinh E2E từ user story tổng quát. |
| **44. Wang et al. (2024)** | Không | Bộ benchmark TESTEVAL đo lường mức độ sẵn sàng biên dịch của code kiểm thử do LLM sinh; là tập dữ liệu đánh giá, không phải quy trình sinh tự động. |
| **45. Thai et al. (2025)** | Không | Đánh giá các coding agent trong việc bảo trì và sửa lỗi kiểm thử chấp nhận qua chu kỳ dài; không cung cấp quy trình kiểm soát định dạng Connextra đầu vào. |
| **46. Haldar & Capretz (2026)** | Không | Chuyển đổi tài liệu PRD thô thành Test Plan cấp cao bằng LLM; không sinh ra kịch bản Gherkin chi tiết đi kèm mã Step Definitions thực thi được. |
| **47. Mughal (2025)** | Không | Xây dựng agent học tăng cường (RL) để tự động điều hướng UI theo kịch bản BDD; không giải quyết bài toán sinh mã Acceptance Test từ đầu vào. |
| **48. Patel et al. (2025)** | Không | Sử dụng LLM để đảo ngược kỹ thuật từ mã nguồn cũ sang đặc tả BDD; đi ngược luồng quy trình (từ code sang yêu cầu thay vì từ yêu cầu Connextra sang code). |
| **49. Chu et al. (2025)** | Không | Hệ thống hóa thành tựu và thách thức của LLM trong sinh kiểm thử đơn vị; chỉ mang tính chất tổng quan lý thuyết cho unit test, chưa mở rộng cho E2E acceptance test. |
| **50. Chatterjee (2025a)** | Không | Thiết kế kiến trúc tối ưu hóa để chạy BDD trong đường ống CI/CD; tập trung vào hạ tầng thực thi và pipeline, không tích hợp quy trình sinh tự động E2E. |
| **51. Chatterjee (2025b)** | Không | Thuật toán phân tích mã nguồn chức năng để ánh xạ thành kịch bản kiểm thử E2E hoàn chỉnh; đi từ mã nguồn có sẵn, không kiểm soát yêu cầu Connextra đầu vào. |
| **52. Rehan et al. (2025)** | Không | Tối ưu hóa việc mở rộng quy mô kiểm thử bằng điều phối prompt đa luồng; không tập trung vào tính toàn vẹn cú pháp và đồng thời của cặp Gherkin + Step Defs. |
| **53. Bahaweres et al. (2020)** | Không | Nghiên cứu thực nghiệm triển khai Cucumber và Katalon trên nền tảng thương mại điện tử; thực hiện thủ công để làm mốc so sánh, không ứng dụng LLM tự động. |
| **54. Sung et al. (2025)** | Không | Chuyển đổi luật kinh doanh phức tạp thành khẳng định kiểm thử trong lập trình thi đấu; không hỗ trợ framework BDD và định dạng Connextra tiêu chuẩn. |
| **55. Murugan & Balamurugan (2025)** | Không | Xây dựng engine kiểm thử BDD dạng "scriptless" (không viết mã) dựa trên AI ngữ cảnh; đi ngược mục tiêu sinh mã Step Definitions thực thi không lỗi cú pháp. |

## Feasibility CHeck - GAP Chính
| Tiêu chí | Mức | Ghi chú |
| :--- | :---: | :--- |
| **Dataset** | 🟢 | Đầu vào là các câu User Story chuẩn Connextra, có thể tự biên soạn hoặc tổng hợp từ tài liệu học tập sẵn có, không mất thời gian thu thập phức tạp. |
| **Tool/API** | ⚠️ | Sử dụng API của các mô hình LLM (Gemini, OpenAI, DeepSeek). Tận dụng Free tier hoặc chi phí ước tính rẻ (< $5). |
| **Compute** | 🟢 | Xử lý nặng diễn ra trên server của nhà cung cấp LLM; máy cá nhân thông thường hoặc Google Colab Free là đủ để điều phối pipeline. |
| **Ground truth** | 🟢 | Ở bước xây dựng công cụ này, pipeline chỉ thực hiện tác vụ sinh tự động (Generation), không yêu cầu tạo nhãn đối chứng phức tạp. |
| **Skills** | ⚠️ | Cần tối thiểu 1 tuần nghiên cứu thư viện kết nối API, kỹ thuật Prompt Engineering (Few-shot, CoT) và parse dữ liệu đầu ra. |
| **Thời gian** | 🟢 | Lộ trình triển khai tường minh, khả thi và có thể hoàn thành với $\ge$ 1 tuần dự phòng buffer. |
| **Contribution** | 🟢 | Đóng góp giải pháp kiến trúc End-to-End tự động hóa toàn vẹn đầu tiên nối liền định dạng Connextra ra thẳng mã kiểm thử thực thi được. |
**Kết quả:** ✅ --> An toàn