# Pilot Study — Setup Notes (ĐÃ HIỆU ĐÍNH)
**Dataset**: Requirements data sets (user stories)
**Source**: Dalpiaz, F. (2018). *Requirements data sets (user stories)*. Mendeley Data, V1, DOI: 10.17632/7zbk8zsd8y.1
**Date**: 2026-06-28 (hiệu đính)
**Prepared by**: DG (Data & Ground-truth team)

---

## 1. Random Seed

```
RANDOM_SEED = 42
```

Seed được chọn theo convention phổ biến trong nghiên cứu tái lập (reproducibility).
Đã verify: chạy `random.seed(42); random.sample(range(50), 10)` cho đúng kết quả bên dưới 

---

## 2. Thông tin Sampling

| Thông số | Giá trị |
|---|---|
| Tổng số user stories (N) | 50 |
| Tỉ lệ pilot | 20% |
| Số story pilot | 10 |
| Phương pháp | `random.sample()` — Python built-in, không thay thế (without replacement) |
| Random seed | 42 |
| Indices đã chọn (0-based) | [1, 5, 6, 7, 8, 14, 15, 17, 34, 40] |

> **Lý do chọn 20% (không phải 10%):** Dataset nhỏ (N=50); 20% = 10 stories đủ để kiểm tra đa dạng domain trước khi scale toàn bộ.

---

## 3. Stories được chọn vào Pilot (ĐÃ SỬA — đối chiếu trực tiếp với `pilot_sample.csv`)

| Story ID | Domain (thật) | Complexity (thật) |
|---|---|---|
| US002 | Recycling & Facilities | Complex |
| US006 | Data Packaging | Medium |
| US007 | Data Packaging | Complex |
| US008 | Recycling & Facilities | Complex |
| US009 | University Research Archive | Complex |
| US015 | Government Services | Complex |
| US016 | Conference Management | Complex |
| US018 | Federal Spending | Simple |
| US035 | Agile / Scrum | Complex |
| US041 | Open Data Publishing | Complex |

**Distribution thật: Simple = 1, Medium = 1, Complex = 8.**

---

## 4. Connextra Format Check

Tất cả 10 story đều đạt chuẩn Connextra: **"As a [role], I want [goal], so that [benefit]"** 


## 5. Inter-Annotator Agreement (IAA)

**IAA** (Inter-Annotator Agreement) = mức độ đồng thuận giữa 2 người gán nhãn, đo bằng **Cohen's Kappa**.

### Ngưỡng đánh giá:

| Kappa | Đánh giá | Hành động |
|---|---|---|
| κ ≥ 0.8 | Tốt | Tiến hành full annotation |
| 0.7 ≤ κ < 0.8 | Chấp nhận được | Tiến hành nhưng theo dõi sát |
| κ < 0.7 | DỪNG | Làm rõ hướng dẫn gán nhãn, gán lại |

### Kết quả IAA trên Pilot (n=10) — ĐÃ TÍNH LẠI trực tiếp từ `pilot_ground_truth.csv`:

| Chỉ số | Giá trị |
|---|---|
| N (stories được gán nhãn) | 10 |
| Trung bình Annotator 1 | 3.60 |
| Trung bình Annotator 2 | 3.20 |
| P_observed (đồng thuận tuyệt đối) | 0.60 |
| P_expected | 0.28 |
| **Cohen's κ (unweighted)** | **0.4444** |
| **Cohen's κ (linear weighted)** | **0.6154** |
| **Kết luận** | **κ < 0.7 → DỪNG** |

### Kết luận: DỪNG — κ_w = 0.6154 < 0.7

Kết quả IAA **chưa đạt ngưỡng chấp nhận được**. Cần thực hiện các bước sau trước khi tiếp tục:

**Nguyên nhân bất đồng chính:**
- **US006** (Data Packaging – Medium): A1=3 vs A2=2 → role "Researcher" mơ hồ (không phải actor hệ thống cụ thể); goal quá implementation-specific cho một user story
- **US008** (Recycling & Facilities – Complex): A1=4 vs A2=3 → goal là goal ghép ("browse AND see"), Annotator 2 cho rằng nên tách thành 2 story
- **US015** (Government Services – Complex): A1=3 vs A2=2 → goal "Complete Building Development Project" quá rộng/trừu tượng, Annotator 2 đánh giá cần decomposition
- **US041** (Open Data Publishing – Complex): A1=4 vs A2=3 → "textual descriptions" mơ hồ, có thể hiểu là tooltip, caption, hay alt-text

**Hành động bắt buộc (theo thứ tự):**
1. **Calibration session** — 2 annotators review 4 story bất đồng (US006, US008, US015, US041), thống nhất rubric
2. **Cập nhật Annotation Guideline** — làm rõ tiêu chí: (a) role phải là actor hệ thống cụ thể, không dùng role mơ hồ như "Researcher"; (b) goal ghép ("X and Y") nên được gắn cờ để xem xét tách story; (c) ranh giới "đủ cụ thể" với goal cấp cao/trừu tượng
3. **Gán nhãn lại toàn bộ 10 story pilot** với guideline đã cập nhật
4. **Tính lại IAA** — nếu κ_w ≥ 0.70 → tiến hành full annotation 50 stories

### Thang điểm annotator (1–5):
- 1 = Poor — story không thể viết acceptance test
- 2 = Fair — story mơ hồ, cần suy đoán nhiều
- 3 = Adequate — testable nhưng edge cases không tường minh
- 4 = Good — rõ positive/negative path, benefit đo được
- 5 = Excellent — đầy đủ, boundary conditions hiển nhiên trong text

