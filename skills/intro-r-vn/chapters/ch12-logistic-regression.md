# Chapter 12: Phân tích hồi qui logistic

## Core Idea
Mô hình hóa mối liên hệ giữa các biến độc lập và một biến phụ thuộc nhị phân (có/không, sống/chết) thông qua xác suất và Odds Ratio.

## Frameworks Introduced
- **Logit Function**: $\text{logit}(p) = \log(p/(1-p))$.
- **Odds Ratio (OR)**: Tỉ số khả dĩ, cho biết mức độ tăng nguy cơ khi biến độc lập tăng 1 đơn vị. $OR = e^\beta$.
- **Maximum Likelihood**: Phương pháp ước tính các thông số trong hồi quy logistic.

## Key Concepts
- **`glm()` (Generalized Linear Model)**: Hàm dùng cho hồi quy logistic với tham số `family="binomial"`.
- **Deviance**: Chỉ số đánh giá độ lệch của mô hình (tương tự phần dư trong hồi quy tuyến tính).
- **AIC (Akaike Information Criterion)**: Chỉ số dùng để so sánh các mô hình; AIC càng thấp mô hình càng tốt.

## Mental Models
- **S-Curve (Sigmoid)**: Xác suất trong hồi quy logistic luôn nằm trong khoảng [0, 1] và có hình dạng chữ S.
- **Odds vs Probability**: Xác suất 0.5 tương đương với Odds là 1 ($\text{logit} = 0$).

## Code Examples
```r
# Chạy mô hình hồi quy logistic
# Dự báo nguy cơ gãy xương (fx) dựa trên mật độ xương (bmd)
logistic <- glm(fx ~ bmd, family="binomial")
summary(logistic)

# Tính Odds Ratio
beta <- coef(logistic)["bmd"]
OR <- exp(beta)

# Dự báo xác suất cho dữ liệu mới
predict(logistic, type="response") # Trả về xác suất p
```

## Worked Example
**Phân tích nguy cơ gãy xương:**
```r
# BMD giảm 1 đơn vị, nguy cơ gãy xương thay đổi thế nào?
logistic <- glm(fx ~ bmd, family="binomial")
summary(logistic)
# Kết quả bmd = -2.27
# OR = exp(-2.27) = 0.103
# Có nghĩa là BMD càng cao thì nguy cơ gãy xương càng thấp (OR < 1).
```

## Key Takeaways
1. Luôn dùng `family="binomial"` trong hàm `glm`.
2. Hệ số $\beta$ trong kết quả `summary` cần được lấy lũy thừa cơ số $e$ (`exp`) để ra Odds Ratio dễ hiểu hơn.
3. Hồi quy logistic là công cụ chuẩn trong nghiên cứu y sinh và dịch tễ học.

## Connects To
- **Ch 10**: So sánh với hồi quy tuyến tính (biến y liên tục).
- **Ch 13**: Tính toán cỡ mẫu cho các nghiên cứu bệnh chứng (case-control).
