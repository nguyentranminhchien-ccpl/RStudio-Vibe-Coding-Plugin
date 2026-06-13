# Chapter 8: Biểu đồ

## Core Idea
Sử dụng các hàm đồ họa cơ bản của R để trực quan hóa dữ liệu từ đơn giản (barplot, pie) đến phức tạp (scatter plot, boxplot).

## Key Concepts
- **`barplot()`**: Biểu đồ cột cho biến rời rạc.
- **`pie()`**: Biểu đồ hình tròn.
- **`hist()`**: Biểu đồ tần số (histogram) cho biến liên tục.
- **`boxplot()`**: Biểu đồ hộp, hiển thị trung vị và các tứ phân vị.
- **`plot()`**: Biểu đồ tán xạ (scatter plot) cho mối liên hệ giữa hai biến.
- **`pairs()`**: Biểu đồ ma trận so sánh nhiều biến cùng lúc.
- **`abline()`**: Vẽ đường thẳng (ví dụ: đường hồi quy) lên biểu đồ.
- **`lowess()`**: Vẽ đường làm trơn dữ liệu (non-parametric smooth).

## Mental Models
- **Layering Graphics**: Bạn có thể vẽ biểu đồ nền bằng `plot()`, sau đó thêm các thành phần khác bằng `lines()`, `abline()`, `arrows()`.
- **Conditioning Plots**: Dùng `ifelse()` trong tham số `pch` hoặc `col` để phân biệt các nhóm dữ liệu trên biểu đồ tán xạ.

## Code Examples
```r
# 1. Biểu đồ cột
sex.freq <- table(sex)
barplot(sex.freq, main="Giới tính")

# 2. Histogram
hist(age, main="Phân phối độ tuổi", xlab="Tuổi")

# 3. Boxplot so sánh 2 nhóm
boxplot(tc ~ sex, main="Cholesterol theo giới tính")

# 4. Biểu đồ tán xạ với đường hồi quy
plot(hdl ~ tc, pch=16)
reg <- lm(hdl ~ tc)
abline(reg, col="red")

# 5. Làm trơn dữ liệu
lines(lowess(hdl, tc), col="blue")

# 6. Ma trận biểu đồ
pairs(data.frame(age, bmi, tc), pch=16)
```

## Worked Example
**Vẽ biểu đồ tán xạ phân biệt giới tính bằng ký hiệu khác nhau:**
```r
# pch=16 là hình tròn đặc, pch=22 là hình vuông
plot(hdl, tc, pch=ifelse(sex=="Nam", 16, 22), 
     main="Mối liên hệ HDL và TC theo giới tính")
# Thêm chú thích hoặc đường hồi quy nếu cần
```

## Key Takeaways
1. Biểu đồ trong R rất linh hoạt, có thể tùy chỉnh mọi thông số (màu sắc, tiêu đề, ký hiệu).
2. Dùng `par(mfrow=c(rows, cols))` để vẽ nhiều biểu đồ trên cùng một cửa sổ.
3. `boxplot` là cách tốt nhất để phát hiện giá trị ngoại biên (outliers).

## Connects To
- **Ch 10**: Trực quan hóa đường hồi quy sau khi chạy mô hình `lm()`.
- **Ch 11**: Dùng `boxplot` để kiểm tra sự khác biệt giữa các nhóm trong ANOVA.
