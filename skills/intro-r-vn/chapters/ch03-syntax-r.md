# Chapter 3: "Văn phạm" R

## Core Idea
Hiểu về cấu trúc câu lệnh (cú pháp) và cách R lưu trữ dữ liệu dưới dạng các "đối tượng" (objects).

## Frameworks Introduced
- **Object-Oriented Syntax**: Mọi thứ trong R đều là đối tượng. Kết quả của một hàm thường được lưu vào một đối tượng mới.
- **Interactive Language**: R phản hồi ngay lập tức sau mỗi câu lệnh đúng văn phạm.

## Key Concepts
- **Command/Function (Hàm)**: Câu lệnh thực hiện một tác vụ cụ thể.
- **Arguments (Thông số)**: Các yếu tố nằm trong ngoặc `()` của hàm.
- **Object (Đối tượng)**: Nơi chứa dữ liệu (biến, bảng dữ liệu, kết quả).
- **Assignment (`<-`)**: Kí hiệu gán giá trị vào đối tượng (khuyến khích hơn `=`).
- **Comments (`#`)**: Ghi chú, R sẽ bỏ qua những gì sau dấu này.
- **Case Sensitivity**: R phân biệt chữ hoa và chữ thường (ví dụ: `A` khác `a`).

## Mental Models
- **The Assignment Flow**: `đối tượng <- hàm(thông số)`. Hãy đọc là "Kết quả của hàm này được đổ vào đối tượng kia".
- **Object naming**: Đặt tên như `my.object` thay vì `my object` để tránh lỗi.

## Anti-patterns
- **Dùng dấu cách trong tên đối tượng**: R sẽ báo lỗi `syntax error`.
- **Quên phân biệt hoa/thường**: Dẫn đến lỗi "object not found".

## Code Examples
```r
# Cú pháp chung
đối tượng <- hàm(thông số 1, thông số 2, ...)

# Ví dụ cụ thể
reg <- lm(y ~ x)  # Chạy mô hình hồi quy và lưu vào 'reg'

# Kiểm tra thông số của hàm
args(lm)

# Gán giá trị
x <- rnorm(10)  # Tạo 10 số ngẫu nhiên chuẩn, lưu vào x

# Các kí hiệu so sánh
x == 5   # So sánh bằng
x != 5   # Không bằng
A & B    # Và (AND)
A | B    # Hoặc (OR)
```

## Worked Example
**Cách đặt tên và gán giá trị:**
```r
# Đúng
My.object.u <- 15
my.object.L <- 5
total <- My.object.u + my.object.L # Kết quả là 20

# Sai (Gây lỗi)
my object <- 10  # Lỗi vì có khoảng trống
```

## Key Takeaways
1. Luôn dùng `<-` để gán giá trị.
2. Dùng `help(tên_hàm)` hoặc `?tên_hàm` để xem hướng dẫn.
3. R rất khắt khe về chữ hoa/thường.

## Connects To
- **Ch 4**: Áp dụng cú pháp để nhập liệu.
- **Ch 6**: Thực hiện các phép tính toán dựa trên các kí hiệu đã học.
