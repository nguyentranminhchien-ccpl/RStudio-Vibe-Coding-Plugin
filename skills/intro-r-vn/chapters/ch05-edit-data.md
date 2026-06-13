# Chapter 5: Biên tập số liệu

## Core Idea
Các kỹ thuật xử lý dữ liệu sau khi nhập: trích xuất mẫu (subset), gộp bảng (merge), và biến đổi biến số (recode).

## Frameworks Introduced
- **Logical Indexing**: Sử dụng các điều kiện logic (như `==`, `>`, `&`) để chọn lọc dữ liệu.
- **Factor Transformation**: Chuyển biến số từ dạng định lượng sang định danh (yếu tố) để phân tích thống kê đúng bản chất.

## Key Concepts
- **`subset()`**: Tách dữ liệu dựa trên điều kiện (ví dụ: chỉ lấy Nam giới).
- **`merge()`**: Nhập hai bảng dữ liệu thành một dựa trên một biến chung (như ID).
- **Indexing `[]`**: Trích xuất dòng/cột cụ thể (ví dụ: `data[dòng, cột]`).
- **`NA` (Not Available)**: Giá trị trống trong R.
- **`replace()`**: Thay thế giá trị trong biến số.
- **`factor()`**: Khai báo biến phân loại.
- **`cut2()`**: Phân nhóm biến liên tục thành các khoảng (yêu cầu package `Hmisc`).

## Mental Models
- **Row/Column Matrix**: `data[1:10, c(1,3)]` nghĩa là lấy 10 dòng đầu của cột 1 và 3.
- **NA Propagation**: Một biến số là factor thì không thể tính `mean()` (kết quả sẽ là `NA`).

## Anti-patterns
- **Dùng `=` thay cho `==` trong điều kiện**: Lệnh `subset(chol, sex="Nam")` sẽ báo lỗi hoặc chạy sai; phải dùng `==`.

## Code Examples
```r
# Tách dữ liệu
nam <- subset(chol, sex=="Nam")
old <- subset(chol, age >= 60)

# Trích xuất cột 1, 3, 7
data2 <- chol[, c(1,3,7)]

# Gộp bảng
d <- merge(d1, d2, by="id", all=TRUE)

# Biến đổi biến số (Recoding)
diagnosis <- bmd
diagnosis[bmd <= -2.5] <- 1  # Loãng xương
diagnosis[bmd > -2.5 & bmd <= -1.0] <- 2 # Xốp xương

# Chuyển thành factor
diag <- factor(diagnosis)
```

## Worked Example
**Phân nhóm mật độ xương (BMD) bằng `cut2`:**
```r
library(Hmisc)
bmd <- c(-0.92, 0.21, 0.17, -3.21, -1.80, -2.60, -2.00, 1.71, 2.12, -2.11)
# Chia bmd thành 3 nhóm có số lượng quan sát tương đương
group <- cut2(bmd, g=3)
table(group)
# Kết quả sẽ cho thấy 3 khoảng giá trị và số lượng mẫu trong mỗi khoảng.
```

## Key Takeaways
1. `subset` là cách nhanh nhất để lọc dữ liệu theo nhóm.
2. Luôn nhớ dùng `factor()` cho các biến định danh trước khi làm thống kê.
3. `NA` xuất hiện khi gộp bảng mà thiếu dữ liệu tương ứng.

## Connects To
- **Ch 9**: Biến factor là bắt buộc cho các kiểm định như t-test hay ANOVA theo nhóm.
- **Ch 8**: Dùng dữ liệu đã subset để vẽ biểu đồ riêng cho từng nhóm.
