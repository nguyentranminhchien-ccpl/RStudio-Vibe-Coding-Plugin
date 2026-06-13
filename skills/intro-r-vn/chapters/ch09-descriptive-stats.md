# Chapter 9: Phân tích thống kê mô tả

## Core Idea
Cách tóm tắt các đặc tính cơ bản của dữ liệu bằng các chỉ số thống kê (trung bình, độ lệch chuẩn) và các kiểm định so sánh cơ bản (t-test).

## Frameworks Introduced
- **Descriptive Statistics Table**: Tóm tắt dữ liệu qua các giá trị Min, Max, Mean, Median, và Quartiles.
- **Hypothesis Testing (Null Hypothesis)**: Giả thiết rằng không có sự khác biệt; kiểm định t dùng để bác bỏ giả thiết này.

## Key Concepts
- **`summary()`**: Hàm vạn năng để tóm tắt nhanh một biến hoặc toàn bộ dataframe.
- **`mean()`, `sd()`, `var()`**: Tính trung bình, độ lệch chuẩn, phương sai.
- **`tapply()`**: Tính toán chỉ số thống kê theo từng phân nhóm (ví dụ: trung bình igfi theo giới tính).
- **`t.test()`**: Kiểm định t cho một mẫu hoặc hai mẫu.
- **P-value**: Trị số xác suất để bác bỏ giả thiết Zero (thường < 0.05 là có ý nghĩa thống kê).
- **Confidence Interval (95% CI)**: Khoảng tin cậy cho giá trị trung bình.

## Mental Models
- **The P-value Threshold**: Nếu p < 0.05, sự khác biệt quan sát được khó có thể là do ngẫu nhiên.
- **Summary by group**: `by(data, group, summary)` là cách nhanh nhất để so sánh đặc tính giữa các nhóm.

## Code Examples
```r
# Tóm tắt nhanh
summary(age)

# Tính trung bình igfi theo giới tính
tapply(igfi, sex, mean)

# Kiểm định t một mẫu (so sánh với trung bình 30)
t.test(age, mu=30)

# Kiểm định t hai mẫu (so sánh nam và nữ)
t.test(igfi ~ sex)

# Tự viết hàm tóm tắt (Mean, SD, SE)
desc <- function(x) {
    av <- mean(x)
    sd <- sd(x)
    se <- sd/sqrt(length(x))
    c(MEAN=av, SD=sd, SE=se)
}
desc(als)
```

## Worked Example
**So sánh nồng độ hormone igfi giữa nam và nữ:**
```r
# Chạy kiểm định t
result <- t.test(igfi ~ sex)
# Xem kết quả
print(result)
# Nếu p-value < 0.05, kết luận có sự khác biệt giữa hai giới.
```

## Key Takeaways
1. Luôn bắt đầu bằng `summary()` để hiểu tổng quan dữ liệu.
2. `t.test` giả định dữ liệu tuân theo phân phối chuẩn.
3. Khoảng tin cậy 95% cung cấp nhiều thông tin hơn là chỉ một trị số p đơn lẻ.

## Connects To
- **Ch 11**: Mở rộng so sánh từ 2 nhóm lên nhiều nhóm (ANOVA).
- **Ch 12**: Chuyển từ so sánh trung bình sang so sánh xác suất/nguy cơ.
