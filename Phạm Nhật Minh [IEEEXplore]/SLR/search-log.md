# Search Log — [LLM for Acceptance Test Automation (BDD/Gherkin)]											
**Thành viên:** Phạm Nhật Minh										
**Ngày thực hiện:** 2026-06-01									
											
---											
											
## Chuỗi tìm kiếm (Query Strings)											
											
### String A											
**Query nguyên văn:**											
```											
("user story" OR "Connextra format" OR "requirements") AND ("LLM" OR "GPT" OR "large language model") AND ("Gherkin generation" OR "step definitions" OR "BDD")									
```											
**Database:** IEEE Xplore										
**Bộ lọc:** Không có bộ lọc 										
**Ngày search:** 2026-06-01 09:34											
**Số kết quả:** 5 papers											
											
---											
											
### String B											
**Query nguyên văn:**											
```											
("LLM*" OR "large language model*" OR "GPT*" OR "generative AI") AND ("BDD" OR "behavior-driven development" OR "Gherkin" OR "acceptance test*") AND ("manual*" OR "human*" OR "traditional" OR "baseline")									
```											
**Database:** IEEE Xplore												
**Bộ lọc:** Không có bộ lọc 												
**Ngày search:** 2026-06-01 09:34										
**Số kết quả:** 25 papers											
											
---											
											
### String C											
**Query nguyên văn:**											
```											
("LLM*" OR "large language model*" OR "GPT*" OR "generative AI") AND ("BDD" OR "behavior-driven development" OR "Gherkin" OR "acceptance test*") AND ("similarity" OR "execut*" OR "quality" OR "evaluat*" OR "accuracy" OR "valid*")										
```											
**Database:** IEEE Xplore												
**Bộ lọc:** Không có bộ lọc 										
**Ngày search:** 2026-06-01 09:35										
**Số kết quả:** 33 papers											
											
---											
											
## Tổng hợp trước dedup											
											
| Database | String | Kết quả |											
|---------|--------|---------|											
| IEEE Xplore | String A | 5 |											
| IEEE Xplore | String B | 25 |											
| IEEE Xplore | String C | 33 |											
| **Tổng trước dedup** | | **63** |											
| **Sau dedup** | | **34** |											
| Số bị loại (trùng lặp) | | 29 |	

## Tổng hợp các bài báo (Paywalled), URL + DOI đã INCLUDE ở v1 nhưng bị loại ở v2 với lý do ("Full-text is unavailable via institutional access")

**01** Object Oriented BDD and Executable Human-Language Module Specification
**Link URL**: https://ieeexplore.ieee.org/document/10223873
**DOI**: 10.1109/SNPD-Winter57765.2023.10223873

**02** Exploring Large Language Models for Requirements on String Values
**Link URL**: https://ieeexplore.ieee.org/document/11028238
**DOI**: 10.1109/MO2RE66661.2025.00009

**03** Reverse-Engineering and Automating BDD for Modern Software Development with LLMs
**Link URL**: https://ieeexplore.ieee.org/document/11351772
**DOI**: 10.1109/ICoDSE68111.2025.11351772

**04** The Role of Machine Learning and Large Language Models in Software Testing and Validation
**Link URL**: https://ieeexplore.ieee.org/document/11364940
**DOI**: 10.1109/STA66620.2025.11364940

**05** User Acceptance Test Case Generation Using LLMs
**Link URL**: https://ieeexplore.ieee.org/document/11344173
**DOI**: 10.1109/CASCON66301.2025.00084

**06** AGORA: An Approach for Generating Acceptance Test Cases from Use Cases
**Link URL**: https://ieeexplore.ieee.org/document/10803349
**DOI**: 10.1109/SEAA64295.2024.00027

**07** Unit Test Generation Multi-Agent AI System for Enhancing Software Documentation and Code Coverage
**Link URL**: https://ieeexplore.ieee.org/document/10819096
**DOI**: 10.1109/TELFOR63250.2024.10819096

**08** SelfBehave, Generating a Synthetic Behaviour-Driven Development Dataset using SELF-INSTRUCT
**Link URL**: https://ieeexplore.ieee.org/document/10962479
**DOI**: 10.1109/ICSTW64639.2025.10962479

**09** API Test Case Generation by Extracting HTTP Requests During Front-End Testing
**Link URL**: https://ieeexplore.ieee.org/document/10784388
**DOI**: 10.1109/ICEBE62490.2024.00013

**10** Context-Aware Behavior-Driven Pipeline Generation
**Link URL**: https://ieeexplore.ieee.org/document/11011952
**DOI**: 10.1109/ISDFS65363.2025.11011952

**11** ATDLLMD: a test-driven framework for safe, reliable, and business-centric LLM development
**Link URL**: https://ieeexplore.ieee.org/document/11514379
**DOI**: 10.1049/icp.2025.4778

**12** Meet C4SE: Your New Collaborator for Software Engineering Tasks
**Link URL**: https://ieeexplore.ieee.org/document/10371523
**DOI**: 10.1109/SEAA60479.2023.00044

## Phần S - Cross Reference Search (Snowballing)
**Ngày thực hiện: 2026-06-02
** Paper included đã scan: 08 paper
** Paper mới phát hiện: 02 đã pass IC
- Từ paper: Cypress Copilot: Development of an AI Assistant for Boosting Productivity and Transforming Web Application Testing tìm được 2 bài báo:
+) "Make LLM a Testing Expert: Bringing Human-Like Interaction to Mobile GUI Testing via Functionality-Aware Decisions" của tác giả: Z. Liu, C. Chen, J. Wang, M. Chen, B. Wu, X. Che, D. Wang, and Q. Wang
+) "Enabling Cost-Effective UI Automation Testing with Retrieval-Based LLMs: A Case Study in WeChat" của tác giả: S. Feng, H. Lu, J. Jiang, T. Xiong, L. Huang, Y. Liang, X. Li, Y. Deng, and A. Aleti



---											
											
## Ghi chú											
											
- Thực hiện dedup bằng: Excel										
- Paper trùng nhau nhiều nhất: các paper từ String A và String C
- Snowballing: 02 là số paper mới tìm được, số pass v2: 02