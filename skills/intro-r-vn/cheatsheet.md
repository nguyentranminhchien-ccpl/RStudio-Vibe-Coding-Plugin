# R Data Analysis Cheatsheet (Tiếng Việt)

## Lệnh hệ thống & Nhập liệu
| Tác vụ | Lệnh |
| :--- | :--- |
| Trợ giúp | `?hàm` hoặc `help(hàm)` |
| Thư mục làm việc | `getwd()`, `setwd("path")` |
| Đọc file CSV | `read.csv("file.csv", header=T)` |
| Đọc file Text | `read.table("file.txt", header=T)` |
| Lưu đối tượng | `save(obj, file="file.rda")` |
| Xem dữ liệu | `head(data)`, `names(data)`, `dim(data)` |

## Xử lý dữ liệu (Biên tập)
- **Gán giá trị**: `x <- 5`
- **Ghép vector**: `c(1, 2, 3)`
- **Lọc dữ liệu**: `subset(data, sex=="Nam" & age > 60)`
- **Chọn cột**: `data[, c(1, 3)]`
- **Khai báo nhóm**: `factor(biến, labels=c("Nhãn1", "Nhãn2"))`
- **Chia nhóm (Hmisc)**: `cut2(biến, g=số_nhóm)`

## Thống kê & Kiểm định
- **Tóm tắt**: `summary(data)`
- **Tính toán**: `mean()`, `sd()`, `var()`, `sum()`, `median()`, `range()`
- **Kiểm định t**: `t.test(y ~ x)`
- **ANOVA**: `anova(lm(y ~ x))`
- **Hồi quy**: `lm(y ~ x1 + x2)`
- **Logistic**: `glm(y ~ x, family="binomial")`
- **Tỉ số Odds Ratio**: `exp(coef(mô_hình))`

## Trực quan hóa (Biểu đồ)
- **Cột**: `barplot(table(biến))`
- **Tần số**: `hist(biến)`
- **Hộp**: `boxplot(y ~ x)`
- **Tán xạ**: `plot(x, y)`
- **Đường thẳng**: `abline(hàm_hồi_quy)`
- **Nhiều biểu đồ**: `par(mfrow=c(hàng, cột))`

## Ước tính cỡ mẫu
- **So sánh trung bình**: `power.t.test(delta, sd, power, sig.level)`
- **So sánh tỉ lệ**: `power.prop.test(p1, p2, power, sig.level)`
- **ANOVA**: `power.anova.test(groups, between.var, within.var, power)`

## Quy tắc vàng
1. R phân biệt **HOA/thường**.
2. Đường dẫn file dùng dấu `/`.
3. Kiểm tra giả định (biểu đồ phần dư) trước khi kết luận hồi quy.
4. P-value < 0.05 là ngưỡng thông dụng cho ý nghĩa thống kê.
