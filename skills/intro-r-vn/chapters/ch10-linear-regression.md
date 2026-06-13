# Chapter 10: Phân tích hồi qui tuyến tính

## Core Idea
Xây dựng mô hình toán học để mô tả mối liên hệ giữa một biến phụ thuộc liên tục và một hoặc nhiều biến độc lập.

## Frameworks Introduced
- **Simple Linear Regression**: $y = \alpha + \beta x + \epsilon$.
- **Least Squares Method**: Phương pháp tìm $\alpha, \beta$ sao cho tổng bình phương các phần dư là nhỏ nhất.
- **Multiple Linear Regression**: Mô hình với nhiều biến độc lập $x_1, x_2, ...$.

## Key Concepts
- **`lm()` (Linear Model)**: Hàm chính để chạy hồi quy.
- **Intercept ($\alpha$)**: Điểm chặn (giá trị y khi x=0).
- **Slope ($\beta$)**: Độ dốc (mức thay đổi của y khi x tăng 1 đơn vị).
- **Residuals (Phần dư)**: Độ lệch giữa giá trị thực tế và giá trị tiên đoán ($y - \hat{y}$).
- **R-squared ($R^2$)**: Hệ số xác định, cho biết mô hình giải thích được bao nhiêu % biến thiên của dữ liệu.
- **`fitted()`**: Lấy các giá trị tiên đoán $\hat{y}$.
- **`resid()`**: Lấy các giá trị phần dư.

## Mental Models
- **Predictive Power**: $R^2$ càng gần 1, mô hình càng mạnh.
- **The "Adjusted" View**: Adjusted R-squared giúp đánh giá xem việc thêm biến mới có thực sự cải thiện mô hình hay không.

## Anti-patterns
- **Bỏ qua kiểm tra giả định**: Chạy mô hình mà không vẽ biểu đồ phần dư (residuals vs fitted) có thể dẫn đến kết luận sai lầm nếu mối quan hệ không phải tuyến tính.

## Code Examples
```r
# Hồi quy đơn biến
reg <- lm(chol ~ age)
summary(reg)

# Xem các giá trị tiên đoán và phần dư
fitted(reg)
resid(reg)

# Vẽ đường hồi quy lên đồ thị
plot(chol ~ age, pch=16)
abline(reg)

# Hồi quy đa biến
mreg <- lm(chol ~ age + bmi)
summary(mreg)

# Kiểm tra giả định (4 biểu đồ chuẩn)
par(mfrow=c(2,2))
plot(reg)
```

## Worked Example
**Dự báo nồng độ Cholesterol dựa trên tuổi:**
```r
reg <- lm(chol ~ age)
# Giả sử kết quả: Intercept = 1.08, age = 0.05
# Dự báo cho người 50 tuổi:
# cholesterol = 1.08 + 0.05 * 50 = 3.58
new_data <- data.frame(age = 50)
predict(reg, new_data)
```

## Key Takeaways
1. `lm(y ~ x)` là cú pháp cơ bản nhất.
2. `summary(reg)` cung cấp toàn bộ các kiểm định t cho hệ số hồi quy.
3. Luôn kiểm tra đồ thị "Normal Q-Q" của phần dư để đảm bảo tính chuẩn xác.

## Connects To
- **Ch 11**: ANOVA thực chất là một trường hợp đặc biệt của mô hình tuyến tính đa biến.
- **Ch 12**: Hồi quy Logistic là bước phát triển khi biến y không còn là liên tục mà là nhị phân.
