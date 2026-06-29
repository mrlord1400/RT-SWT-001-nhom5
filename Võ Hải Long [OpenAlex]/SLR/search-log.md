# Search Log — [LLM for Acceptance Test Automation (BDD/Gherkin)]											
**Thành viên:** Võ Hải Long											
**Ngày thực hiện:** 2026-05-28										
											
---											
											
## Chuỗi tìm kiếm (Query Strings)											
											
### String A											
**Query nguyên văn:**											
```											
("user story" OR "Connextra format" OR "requirements") AND ("LLM" OR "GPT" OR "large language model") AND ("Gherkin generation" OR "step definitions" OR "BDD")									
```											
**Database:** OpenAlex											
**Bộ lọc:** Không có bộ lọc (manual filter sau)												
**Ngày search:** 2026-05-28 07:49											
**Số kết quả:** 18 papers											
											
---											
											
### String B											
**Query nguyên văn:**											
```											
("LLM*" OR "large language model*" OR "GPT*" OR "generative AI") AND ("BDD" OR "behavior-driven development" OR "Gherkin" OR "acceptance test*") AND ("manual*" OR "human*" OR "traditional" OR "baseline")									
```											
**Database:** OpenAlex												
**Bộ lọc:** Không có bộ lọc (manual filter sau)													
**Ngày search:** 2026-05-28 07:50											
**Số kết quả:** 96 papers											
											
---											
											
### String C											
**Query nguyên văn:**											
```											
("LLM*" OR "large language model*" OR "GPT*" OR "generative AI") AND ("BDD" OR "behavior-driven development" OR "Gherkin" OR "acceptance test*") AND ("similarity" OR "execut*" OR "quality" OR "evaluat*" OR "accuracy" OR "valid*")										
```											
**Database:** OpenAlex											
**Bộ lọc:** Không có bộ lọc (manual filter sau)											
**Ngày search:** 2026-05-28 07:51										
**Số kết quả:** 80 papers											
											
---											
											
## Tổng hợp trước dedup											
											
| Database | String | Kết quả |											
|---------|--------|---------|											
| OpenAlex | String A | 18 |											
| OpenAlex | String B | 96 |											
| OpenAlex | String C | 80 |											
| **Tổng trước dedup** | | **194** |											
| **Sau dedup** | | **122** |											
| Số bị loại (trùng lặp) | | 72 |											
											
---											
											
## Ghi chú											
											
- Thực hiện dedup bằng: Excel										
- Paper trùng nhau nhiều nhất: các paper từ String 2 và String 3																			