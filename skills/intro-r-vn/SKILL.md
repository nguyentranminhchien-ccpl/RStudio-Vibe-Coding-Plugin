---
name: intro-r-vn
description: "Kiến thức phân tích số liệu và biểu đồ bằng R dựa trên giáo trình của TS. Nguyễn Văn Tuấn. Hỗ trợ các kỹ thuật nhập liệu, thống kê mô tả, kiểm định t, ANOVA, hồi quy tuyến tính/logistic và ước tính cỡ mẫu bằng tiếng Việt."
allowed-tools:
  - Read
  - Grep
argument-hint: [chủ đề, tên hàm, hoặc số chương]
---

# Phân tích số liệu và biểu đồ bằng R
**Tác giả**: Nguyễn Văn Tuấn | **Số chương**: 14 | **Ngôn ngữ**: Tiếng Việt | **Cập nhật**: 2026-06-10

## Cách sử dụng Skill này

- **Không đối số** — Tải các khung sườn phân tích cơ bản (Patterns).
- **Theo chủ đề** — Hỏi về `hồi quy`, `cỡ mẫu`, hoặc `biểu đồ`; tôi sẽ tìm và đọc chương tương ứng.
- **Theo chương** — Gõ `ch05` hoặc `ch12` để xem chi tiết kỹ thuật.
- **Dữ liệu Đột quỵ** — Hỏi về `case study` hoặc `dotquy` để xem ví dụ ứng dụng `tidyverse`.

---

## Khung sườn Phân tích (Core Frameworks)

1. **Quy trình Nhập & Làm sạch (Import & Clean)**:
   - Luôn ưu tiên `read.csv()` cho dữ liệu từ Excel.
   - Sử dụng `factor()` để định nghĩa các biến phân loại ngay từ đầu.
   - Kiểm tra cấu trúc bằng `dim()` và `names()` để tránh lỗi lệch hàng/cột.

2. **Tư duy Thống kê (Statistical Thinking)**:
   - Luôn vẽ biểu đồ (`boxplot`, `hist`) trước khi chạy kiểm định.
   - Sử dụng P-value < 0.05 làm ngưỡng ý nghĩa, nhưng phải kết hợp với Khoảng tin cậy (CI).
   - Kiểm tra giả định của mô hình (phân phối chuẩn, phần dư) bằng `plot(mô_hình)`.

3. **Nguyên tắc "Vừa đủ" (Sample Size)**:
   - Mọi nghiên cứu cần ước tính cỡ mẫu TRƯỚC khi thực hiện để đảm bảo sức mạnh thống kê (Power).
   - Dùng `power.t.test` hoặc `power.prop.test` dựa trên thông tin từ các nghiên cứu trước (SD, Effect Size).

---

## Danh mục Chương (Chapter Index)

| # | Tiêu đề | Nội dung chính |
|---|-------|----------------|
| [ch01](chapters/ch01-install-r.md) | Cài đặt R | Tải từ CRAN, setup Windows |
| [ch02](chapters/ch02-install-packages.md) | Cài đặt Package | `library`, `foreign`, `Hmisc` |
| [ch03](chapters/ch03-syntax-r.md) | Văn phạm R | Đối tượng, lệnh gán `<-`, case sensitivity |
| [ch04](chapters/ch04-import-data.md) | Nhập dữ liệu | `read.table`, `read.csv`, `read.spss` |
| [ch05](chapters/ch05-edit-data.md) | Biên tập số liệu | `subset`, `merge`, `factor`, `recode` |
| [ch06](chapters/ch06-simple-calc.md) | Tính toán cơ bản | Số học, ma trận, vector |
| [ch07](chapters/ch07-probability.md) | Xác suất | `norm`, `binom`, `pois`, `sample` |
| [ch08](chapters/ch08-graphics.md) | Biểu đồ | `plot`, `hist`, `boxplot`, `abline` |
| [ch09](chapters/ch09-descriptive-stats.md) | Thống kê mô tả | `summary`, `t.test`, CI 95% |
| [ch10](chapters/ch10-linear-regression.md) | Hồi quy tuyến tính | `lm`, $R^2$, phần dư (residuals) |
| [ch11](chapters/ch11-anova.md) | Phân tích phương sai | `anova`, `TukeyHSD`, so sánh nhiều nhóm |
| [ch12](chapters/ch12-logistic-regression.md) | Hồi quy Logistic | `glm`, Odds Ratio ($e^\beta$), AIC |
| [ch13](chapters/ch13-sample-size.md) | Ước tính cỡ mẫu | Power, Alpha, Effect Size |
| [ch14](chapters/ch14-dotquy-case-study.md) | Case Study: Đột quỵ | `tidyverse`, `mutate`, làm sạch dữ liệu |

---

## Chỉ mục Chủ đề (Topic Index)

- **ANOVA** → ch11, ch13
- **Biểu đồ (Graphics)** → ch08, ch10
- **Cỡ mẫu (Sample Size)** → ch13
- **Hồi quy (Regression)** → ch10, ch12
- **Kiểm định (Test)** → ch09, ch11
- **Nhập liệu (Import)** → ch04
- **Tidyverse** → ch14

---

## Các file hỗ trợ

- [glossary.md](glossary.md) — Từ điển thuật ngữ Anh-Việt
- [patterns.md](patterns.md) — Các mẫu code cho từng bài toán
- [cheatsheet.md](cheatsheet.md) — Bảng tra cứu lệnh nhanh

---

## Phạm vi & Giới hạn

Skill này tập trung vào các phương pháp thống kê căn bản và thực hành trên R. Đối với các kỹ thuật nâng cao hơn như mô hình hỗn hợp (mixed models), phân tích sống còn (survival analysis) chuyên sâu, hãy tham khảo các skill bổ trợ hoặc tài liệu nâng cao của TS. Nguyễn Văn Tuấn.
