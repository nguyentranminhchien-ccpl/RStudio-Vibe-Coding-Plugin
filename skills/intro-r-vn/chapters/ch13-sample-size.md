# Chapter 13: Ước tính cỡ mẫu (Sample Size)

## Core Idea
Xác định số lượng đối tượng tối thiểu cần thiết để nghiên cứu có đủ độ tin cậy và sức mạnh thống kê (power), tránh lãng phí tài nguyên hoặc kết luận sai lầm.

## Frameworks Introduced
- **Statistical Power (1 - $\beta$)**: Xác suất phát hiện được sự khác biệt khi sự khác biệt đó thực sự tồn tại (thường chọn 0.8 hoặc 0.9).
- **Type I Error ($\alpha$)**: Sai sót khi kết luận có sự khác biệt nhưng thực tế không có (thường chọn 0.05).
- **Effect Size ($\Delta$)**: Mức độ khác biệt tối thiểu mà nhà nghiên cứu muốn phát hiện.

## Key Concepts
- **`power.t.test()`**: Ước tính cỡ mẫu cho kiểm định t (so sánh trung bình).
- **`power.anova.test()`**: Ước tính cỡ mẫu cho phân tích phương sai.
- **`power.prop.test()`**: Ước tính cỡ mẫu cho so sánh tỉ lệ.
- **Variability ($\sigma$)**: Độ lệch chuẩn của đo lường; càng cao thì cỡ mẫu cần thiết càng lớn.

## Mental Models
- **The Sample Size Triangle**: Cỡ mẫu phụ thuộc vào $\alpha$, $\beta$, và $\Delta$. Muốn $\Delta$ nhỏ (chính xác cao), cỡ mẫu phải lớn.
- **Before-After Study**: Nghiên cứu đo lường trên cùng một nhóm trước và sau can thiệp (dùng `type="one.sample"`).

## Code Examples
```r
# 1. So sánh chiều cao (1 nhóm)
# Sai số 1cm, SD 4.6, Alpha 0.05, Power 0.8
power.t.test(delta=1, sd=4.6, sig.level=0.05, power=0.8, type="one.sample")

# 2. So sánh 2 nhóm thuốc (BMD)
# Khác biệt 0.04, SD 0.12, Alpha 0.05, Power 0.9
power.t.test(delta=0.04, sd=0.12, sig.level=0.05, power=0.9, type="two.sample")

# 3. So sánh tỉ lệ gãy xương (2 nhóm)
# P1=0.10, P2=0.06, Alpha 0.01, Power 0.9
power.prop.test(p1=0.10, p2=0.06, sig.level=0.01, power=0.9)

# 4. ANOVA (4 nhóm)
groupmeans <- c(4.5, 3.0, 5.6, 1.3)
power.anova.test(groups=4, between.var=var(groupmeans), within.var=8.7, power=0.9)
```

## Worked Example
**Tính số bệnh nhân cần thiết cho thử nghiệm thuốc:**
Giả sử thuốc mới giúp tăng nồng độ chất X thêm 5 đơn vị. SD của chất X là 15.
```r
power.t.test(delta=5, sd=15, sig.level=0.05, power=0.8, type="one.sample")
# Kết quả n = 72. Một nghiên cứu "trước-sau" cần 72 bệnh nhân.
```

## Key Takeaways
1. Ước tính cỡ mẫu phải được thực hiện TRƯỚC khi bắt đầu thu thập số liệu.
2. Cỡ mẫu quá nhỏ dẫn đến kết quả "âm tính giả" (không phát hiện được hiệu quả dù thuốc có tác dụng).
3. Luôn cần thông tin về độ lệch chuẩn (SD) từ các nghiên cứu trước hoặc nghiên cứu sơ khởi (pilot study).

## Connects To
- **Ch 7**: Nền tảng về phân phối xác suất và lấy mẫu.
- **Ch 9, 11, 12**: Sau khi có đủ cỡ mẫu, ta tiến hành các kiểm định t, ANOVA hoặc hồi quy tương ứng.
