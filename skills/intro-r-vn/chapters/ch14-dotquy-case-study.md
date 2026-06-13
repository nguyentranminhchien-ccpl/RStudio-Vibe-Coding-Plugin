# Case Study: Phân tích dữ liệu Đột quỵ (Dotquy.R)

## Core Idea
Ứng dụng thực tế các kỹ thuật xử lý dữ liệu hiện đại bằng `tidyverse` để làm sạch và phân nhóm dữ liệu bệnh nhân đột quỵ.

## Frameworks Introduced
- **The Pipe Operator (`%>%`)**: Chuyển tiếp kết quả của hàm này sang hàm kế tiếp, giúp code dễ đọc hơn.
- **Data Mutation**: Thay đổi cấu trúc hoặc giá trị của biến số một cách hệ thống.

## Code Examples
```r
# Tải thư viện
library(tidyverse)

# Nhập dữ liệu
dotquy <- read.csv("DuLieu.csv", header = TRUE)

# Kỹ thuật: Chuyển đổi hàng loạt với across()
# Tiết kiệm thời gian khi có nhiều biến cần chuyển sang factor
dotquy <- dotquy %>%
  mutate(across(c(GioiTinh, TienSu, KetQua), 
                ~factor(.x, levels = c(0, 1), labels = c("Không", "Có"))))

# Hoặc chuyển nhanh mọi cột ký tự sang factor
dotquy <- dotquy %>%
  mutate(across(where(is.character), as.factor))
```

## Key Concepts
- **`library(tidyverse)`**: Bộ công cụ mạnh mẽ bao gồm `dplyr`, `ggplot2`, `mutate`.
- **`mutate()`**: Tạo hoặc sửa đổi biến số.
- **`across()`**: Áp dụng cùng một hàm lên nhiều cột cùng lúc (giảm lặp code).
- **`factor()` with Labels**: Chuyển mã số (0, 1) thành nhãn có ý nghĩa ("Nữ", "Nam").

## Worked Example
**Giải thích đoạn mã xử lý giới tính:**
Đoạn mã `mutate(GioiTinh = factor(GioiTinh, levels = c(0, 1), labels = c("Nữ", "Nam")))` thực hiện 2 việc:
1. Xác định 0 và 1 là các cấp độ (levels).
2. Gán nhãn "Nữ" cho 0 và "Nam" cho 1.
Sau bước này, khi vẽ biểu đồ hoặc chạy thống kê, R sẽ hiển thị chữ thay vì con số khô khan.

## Key Takeaways
1. Sử dụng `tidyverse` giúp code R trở nên trực quan và mạnh mẽ hơn.
2. Luôn kiểm tra `dim()` của dữ liệu sau mỗi bước lọc (`subset`) để đảm bảo không mất mát dữ liệu ngoài ý muốn.

## Connects To
- **Ch 4 & 5**: Đây là sự mở rộng và hiện đại hóa của các phương pháp nhập/biên tập dữ liệu cơ bản.
- **Ch 9**: Chuẩn bị dữ liệu sạch là bước bắt buộc trước khi chạy `t.test` hay `summary`.
