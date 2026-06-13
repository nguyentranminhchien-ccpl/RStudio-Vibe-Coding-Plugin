# Chapter 4: Cách nhập dữ liệu vào R

## Core Idea
Các phương pháp chuyển dữ liệu từ bên ngoài (nhập tay, file text, Excel, SPSS) vào định dạng `data.frame` của R.

## Frameworks Introduced
- **Data Frame**: Cấu trúc dữ liệu chuẩn của R, giống như một bảng tính với hàng và cột.
- **Concatenation (`c()`)**: Hàm móc nối các phần tử đơn lẻ thành một vector.

## Key Concepts
- **`c()`**: Nhập dữ liệu thủ công theo cột.
- **`data.frame()`**: Nhập các cột đơn lẻ thành một bảng dữ liệu hoàn chỉnh.
- **`setwd()`**: Thiết lập thư mục làm việc (Working Directory).
- **`read.table()`**: Đọc file văn bản (.txt).
- **`read.csv()`**: Đọc file Excel đã lưu dạng CSV.
- **`read.spss()`**: Đọc file SPSS (.sav) - yêu cầu package `foreign`.
- **`save()`**: Lưu đối tượng R thành file `.rda` để dùng lại sau.

## Mental Models
- **Path Forward Slashes**: Trong Windows dùng `\`, nhưng trong R phải dùng `/` cho đường dẫn file (ví dụ: `c:/data/file.txt`).
- **Header check**: Khi đọc file, luôn xác định `header=TRUE` nếu dòng đầu là tên biến.

## Code Examples
```r
# 1. Nhập trực tiếp
age <- c(50, 62, 60)
insulin <- c(16.5, 10.8, 32.3)
tuan <- data.frame(age, insulin)

# 2. Đọc file Text
setwd("c:/works/insulin")
chol <- read.table("chol.txt", header=TRUE)

# 3. Đọc file CSV (từ Excel)
gh <- read.csv("excel.csv", header=TRUE)

# 4. Đọc file SPSS
library(foreign)
testo <- read.spss("testo.sav", to.data.frame=TRUE)

# Kiểm tra thông tin dữ liệu
dim(chol)    # Số dòng và cột
names(chol)  # Tên các biến số
table(chol$sex) # Tần số của biến phân loại
```

## Worked Example
**Quy trình nhập dữ liệu từ Excel:**
1. Trong Excel, chọn **File -> Save as**.
2. Chọn định dạng **CSV (Comma delimited)**, lưu thành `excel.csv`.
3. Trong R, gõ:
   ```r
   setwd("C:/du_lieu_cua_toi")
   my_data <- read.csv("excel.csv", header=TRUE)
   # Kiểm tra xem đã vào chưa
   head(my_data)
   ```

## Key Takeaways
1. `data.frame` là đích đến cuối cùng của mọi quá trình nhập liệu.
2. Lưu ý dấu `/` trong đường dẫn file trên Windows.
3. Dùng `names()` và `dim()` để kiểm tra ngay sau khi nhập.

## Connects To
- **Ch 5**: Sau khi nhập liệu, ta bắt đầu biên tập (subset, merge).
- **Ch 9**: Dữ liệu đã nhập được dùng cho thống kê mô tả.
