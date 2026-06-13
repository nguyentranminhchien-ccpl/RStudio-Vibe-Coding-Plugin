# Chapter 7: Sử dụng R cho tính toán xác suất

## Core Idea
Sử dụng các hàm tích hợp trong R để tính toán hoán vị, tổ hợp và các loại phân phối xác suất phổ biến (nhị phân, Poisson, chuẩn).

## Frameworks Introduced
- **Probability Distribution Functions**: Mỗi loại phân phối trong R có 4 biến thể hàm bắt đầu bằng:
  - `d` (density): Hàm mật độ xác suất.
  - `p` (probability): Hàm phân phối tích lũy.
  - `q` (quantile): Hàm định bậc.
  - `r` (random): Hàm mô phỏng ngẫu nhiên.

## Key Concepts
- **Hoán vị (Permutation)**: Dùng `prod(n:1)` để tính n!.
- **Tổ hợp (Combination)**: Dùng `choose(n, k)`.
- **Phân phối nhị phân (Binomial)**: `dbinom`, `pbinom`.
- **Phân phối Poisson**: `dpois`, `ppois`.
- **Phân phối chuẩn (Normal)**: `dnorm`, `pnorm`, `qnorm`, `rnorm`.
- **Z-score**: Chỉ số chuẩn hóa (trung bình 0, độ lệch chuẩn 1).
- **Lấy mẫu ngẫu nhiên**: Dùng `sample()`.

## Mental Models
- **Standardized Normal Distribution**: Một biến số chuẩn hóa $Z = (X - \mu)/\sigma$ cho phép so sánh các biến có đơn vị đo lường khác nhau.
- **Random Sampling with Replacement**: Dùng `replace=TRUE` trong `sample()` nếu muốn một đối tượng có thể được chọn nhiều lần.

## Code Examples
```r
# Tính 10!
prod(10:1)

# Tính tổ hợp chọn 2 từ 5
choose(5, 2)

# Xác suất 2 thành công trong 3 lần thử với p=0.6
dbinom(2, 3, 0.6)

# Xác suất chiều cao thấp hơn 150cm (với mean=156, sd=4.6)
pnorm(150, 156, 4.6)

# Tìm giá trị z sao cho P(Z < z) = 0.95
qnorm(0.95)

# Chọn ngẫu nhiên 5 số từ 1 đến 40
sample(1:40, 5)
```

## Reference Tables
| Loại phân phối | Tên trong R | Thông số chính |
| :--- | :--- | :--- |
| Chuẩn (Normal) | `norm` | `mean`, `sd` |
| Nhị phân (Binomial) | `binom` | `n`, `p` |
| Poisson | `pois` | `lambda` |
| T-distribution | `t` | `df` (bậc tự do) |

## Worked Example
**Mô phỏng 1000 lần chọn mẫu 20 người trong quần thể có 20% mắc cao huyết áp:**
```r
# Mô phỏng
b <- rbinom(1000, 20, 0.20)
# Xem tần số
table(b)
# Vẽ biểu đồ phân phối
hist(b, main="Số bệnh nhân cao huyết áp")
```

## Key Takeaways
1. R hỗ trợ hầu hết các loại phân phối xác suất trong thống kê.
2. Quy tắc đặt tên `d/p/q/r` giúp dễ dàng ghi nhớ hàng loạt hàm.
3. `sample()` là công cụ cực kỳ hữu ích cho việc thiết kế thí nghiệm ngẫu nhiên.

## Connects To
- **Ch 9**: Các kiểm định thống kê (t-test) dựa trên phân phối chuẩn.
- **Ch 13**: Ước tính cỡ mẫu dựa trên các nguyên tắc xác suất.
