# Chapter 2: Tải R package và cài đặt vào máy tính

## Core Idea
Cách mở rộng chức năng của R bằng các "package" (gói phần mềm nhỏ) được phát triển bởi cộng đồng thống kê.

## Frameworks Introduced
- **R Package System**: Hệ thống module cho phép R giải quyết các vấn đề chuyên biệt (dịch tễ, di truyền, đồ thị...).

## Key Concepts
- **Package**: Phần mềm nhỏ chạy trong R để thực hiện các phân tích cụ thể.
- **Library**: Nơi chứa các package đã cài đặt; dùng lệnh `library()` để gọi.
- **Install Packages**: Lệnh hoặc menu để tải package từ CRAN.
- **Local zip file**: Cách cài đặt package từ file có sẵn trên máy.

## Mental Models
- **R as a Smartphone, Packages as Apps**: R cung cấp nền tảng, còn package cung cấp tính năng chuyên sâu.

## Anti-patterns
- **Cài đặt quá nhiều package không cần thiết**: Chỉ nên cài những gì thực sự dùng để tránh xung đột và nặng máy.

## Code Examples
```r
# Cài đặt package trực tuyến
# (Thao tác qua menu: Packages -> Install package(s)...)

# Gọi package để sử dụng
library(Hmisc)
library(Design)
```

## Reference Tables
| Tên package | Chức năng chính |
| :--- | :--- |
| `trellis`, `lattice` | Vẽ đồ thị đẹp hơn |
| `Hmisc`, `Design` | Phương pháp mô hình dữ liệu của F. Harrell |
| `Epi`, `epitools` | Phân tích dịch tễ học |
| `Foreign` | Nhập dữ liệu từ SPSS, Stata, SAS |
| `survival` | Phân tích mô hình Cox |
| `meta`, `Rmeta` | Phân tích tổng hợp (meta-analysis) |

## Worked Example
**Cài đặt package `Hmisc` để phân tích dữ liệu:**
1. Mở R.
2. Chọn menu `Packages` -> `Install package(s)...`.
3. Chọn một CRAN mirror (ví dụ: Australia hoặc USA).
4. Tìm và chọn `Hmisc` trong danh sách, nhấn OK.
5. Sau khi cài xong, gõ `library(Hmisc)` để bắt đầu dùng các hàm như `cut2`.

## Key Takeaways
1. Package là sức mạnh thực sự của R.
2. Có thể cài trực tiếp từ CRAN hoặc từ file local.
3. Package `Foreign` là thiết yếu nếu bạn chuyển từ SPSS/SAS sang R.

## Connects To
- **Ch 4**: Dùng package `foreign` để nhập liệu từ SPSS.
- **Ch 5**: Dùng `Hmisc` để biên tập số liệu (hàm `cut2`).
