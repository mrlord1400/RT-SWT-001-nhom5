# Hypotheses Draft – Zero-shot LLM Test Asset Generation
Ngày: 2026-06-14

---

## RQ1 – Coverage (Độ phủ yêu cầu)

**Phát biểu RQ đầy đủ (công thức PICO):**
> GPT-4o và Claude 3.5 Sonnet zero-shot (I, temperature=0), khi nhận 10–15 Raw Business Requirements thuộc domain ứng dụng web thương mại điện tử Việt Nam (P), có đạt Requirement Coverage Rate ≥ 80% (O) so với ngưỡng tối thiểu chấp nhận được trong industry QA practice (C) không?

**H0:** GPT-4o và Claude 3.5 Sonnet zero-shot KHÔNG đạt Requirement Coverage Rate ≥ 80% trên bộ 10–15 Raw Business Requirements đã xây dựng.

**H1:** GPT-4o và Claude 3.5 Sonnet zero-shot ĐẠT Requirement Coverage Rate ≥ 80% trên bộ 10–15 Raw Business Requirements đã xây dựng.

**Statistical test dự kiến:** Binomial exact test (α = 0.05)

> **Lý do chọn Binomial:** Requirement Coverage Rate được tính bằng tỷ lệ đếm (số quy tắc nghiệp vụ được phủ / tổng số quy tắc) – đây là output nhị phân (Covered / Not Covered) per business rule. Binomial exact test phù hợp để kiểm định xem tỉ lệ quan sát được có ≥ ngưỡng 80% không (theo hướng dẫn: "Có '%' là tỉ lệ đếm → Binomial").

---

## RQ2 – Validity (Tính hợp lệ cú pháp của code)

**Phát biểu RQ đầy đủ (công thức PICO):**
> GPT-4o và Claude 3.5 Sonnet zero-shot (I, temperature=0), khi sinh execution logic từ 10–15 Raw Business Requirements thuộc domain ứng dụng web thương mại điện tử Việt Nam (P), có đạt Syntax Validity Rate ≥ 70% (O, đánh giá bằng manual inspection theo rubric 3 tiêu chí) so với ngưỡng floor tham chiếu từ HumanEval pass@1 baseline (C) không?

**H0:** GPT-4o và Claude 3.5 Sonnet zero-shot KHÔNG đạt Syntax Validity Rate ≥ 70% trên execution logic được sinh ra từ bộ Raw Business Requirements đã xây dựng.

**H1:** GPT-4o và Claude 3.5 Sonnet zero-shot ĐẠT Syntax Validity Rate ≥ 70% trên execution logic được sinh ra từ bộ Raw Business Requirements đã xây dựng.

**Statistical test dự kiến:** Binomial exact test (α = 0.05)

> **Lý do chọn Binomial:** Syntax Validity được đo bằng tỷ lệ đếm pass/fail (số file code đạt cả 3 tiêu chí / tổng số file code) – đây là output nhị phân (Valid / Not Valid) per code file. Binomial exact test phù hợp để kiểm định xem tỉ lệ file code hợp lệ có ≥ ngưỡng 70% không. Nếu phân phối thực tế khác dự kiến sau pilot, sẽ ghi amendment theo proposal §8.6.

---

## RQ3 – Comparative (So sánh 2 LLM)

**Phát biểu RQ đầy đủ (công thức PICO):**
> Trên cùng bộ 10–15 Raw Business Requirements thuộc domain ứng dụng web thương mại điện tử Việt Nam (P), GPT-4o zero-shot (I, temperature=0) có tốt hơn Claude 3.5 Sonnet zero-shot (C) về Requirement Coverage Rate (O) không?

**H0:** GPT-4o zero-shot KHÔNG tốt hơn Claude 3.5 Sonnet zero-shot về Requirement Coverage Rate trên cùng bộ Raw Business Requirements đã xây dựng.

**H1:** GPT-4o zero-shot tốt hơn Claude 3.5 Sonnet zero-shot về Requirement Coverage Rate trên cùng bộ Raw Business Requirements đã xây dựng.

**Statistical test dự kiến:** Mann-Whitney U test (α = 0.05)

> **Lý do chọn Mann-Whitney U:** RQ3 so sánh 2 hệ thống độc lập (GPT-4o vs Claude 3.5 Sonnet) trên cùng dataset. Coverage Rate per requirement là điểm số có thể phân bố không chuẩn (small sample, n=10–15), nên dùng Mann-Whitney U để so sánh 2 nhóm điểm số độc lập với nhau – không giả định phân phối chuẩn (theo hướng dẫn: "Có so với hệ thống khác → Mann-Whitney U").
