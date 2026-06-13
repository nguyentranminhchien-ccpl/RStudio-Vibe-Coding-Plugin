## Pattern: Nhập liệu và Kiểm tra
**When to use**: Khi bắt đầu một dự án phân tích dữ liệu mới.
**How**:
1. `setwd("đường/dẫn")`
2. `data <- read.csv("file.csv", header=T)`
3. `names(data)`; `dim(data)`; `summary(data)`
**Trade-offs**: Nhập liệu qua Excel (CSV) dễ hơn nhập trực tiếp bằng `c()` nhưng cần cẩn thận với định dạng ngày tháng.

## Pattern: Kiểm định so sánh 2 nhóm
**When to use**: So sánh trung bình giữa nam/nữ, bệnh/không bệnh.
**How**:
1. Vẽ boxplot: `boxplot(y ~ x)`
2. Chạy t-test: `t.test(y ~ x)`
**Trade-offs**: Giả định dữ liệu phân phối chuẩn. Nếu không chuẩn, dùng `wilcox.test`.

## Pattern: Hồi quy Tuyến tính
**When to use**: Tìm mối liên hệ giữa các biến liên tục (ví dụ: tuổi và cholesterol).
**How**:
1. `reg <- lm(y ~ x1 + x2, data=mydata)`
2. `summary(reg)`
3. `plot(reg)` để kiểm tra phần dư.

## Pattern: Hồi quy Logistic (Y sinh)
**When to use**: Phân tích nguy cơ/xác suất biến cố (có/không).
**How**:
1. `fit <- glm(fx ~ age + bmd, family="binomial")`
2. `exp(coef(fit))` để lấy Odds Ratio.

## Pattern: Biến đổi hàng loạt (Bulk Transform)
**When to use**: Khi cần chuyển nhiều biến sang cùng một định dạng (factor, numeric, v.v.).
**How**:
```r
data <- data %>%
  mutate(across(c(Col1, Col2, Col3), as.factor))

# Dùng công thức (lambda) để truyền thêm tham số
data <- data %>%
  mutate(across(c(Var1, Var2), ~factor(.x, levels=c(0, 1), labels=c("N", "Y"))))
```
**Trade-offs**: Code ngắn gọn hơn nhưng cần cẩn thận để không chọn nhầm cột không mong muốn.

## Pattern: Ước tính cỡ mẫu
**When to use**: Giai đoạn thiết kế nghiên cứu (trước khi thu thập số liệu).
**How**:
1. Xác định $\Delta$ (hiệu ứng mong muốn) và $\sigma$ (độ biến thiên).
2. `power.t.test(delta=..., sd=..., power=0.8)`
