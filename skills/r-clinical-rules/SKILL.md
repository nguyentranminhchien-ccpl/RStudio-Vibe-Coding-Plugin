---
name: r-clinical-rules
description: >-
  Quy tắc viết code R và phân tích thống kê lâm sàng (Clinical Analysis Guidelines). Hướng dẫn Agentic Workflow cho dữ liệu y khoa.
---

# Phân Tích Số Liệu Lâm Sàng - Quy Tắc Dự Án

File này hướng dẫn cách vận hành, xây dựng và kiểm thử code R trong dự án này.

## 🛠️ Lệnh Kiểm Thử & Chạy Mã Nguồn
- **Kiểm tra dữ liệu & code R:** Sử dụng công cụ MCP `r-studio::execute_r` để chạy lệnh trực tiếp trên R-Studio.
- **Biên dịch báo cáo (Render Quarto):** `rmarkdown::render("report.Rmd")` hoặc `quarto::quarto_render("report.qmd")` thông qua lệnh chạy R.
- **Kiểm tra thư viện:** Sử dụng `r-studio::verify_references` để kiểm định các package R được import.

## 📐 Quy Tắc Viết Code R & Thống Kê (Code Style & Statistics Guidelines)
- **Thư viện chính:** Ưu tiên sử dụng hệ sinh thái `tidyverse` (gồm `dplyr`, `ggplot2`, `readr`, `tidyr`).
- **Đặt tên biến:** Sử dụng chuẩn `snake_case` (ví dụ: `tuoi_benh_nhan`). Khuyến khích dùng gói `janitor::clean_names(df)`.
- **Thống kê mô tả:** 
  - Biến liên tục: Báo cáo `mean (sd)` nếu phân phối chuẩn, hoặc `median (IQR)` nếu phân phối lệch.
  - Biến phân loại: Báo cáo tỷ lệ phần trăm kèm số lượng `n (%)`.
  - Luôn luôn tính khoảng tin cậy 95% (95% CI) cho các tỷ lệ biến cố chính.

## 📊 Mô Hình Hóa & Đánh Giá (Modeling & Evaluation)
Quy trình mô hình hóa phải đi qua 3 bước: Fitting -> Tuning -> Evaluation. Các chỉ số đánh giá bắt buộc cho từng loại mô hình truyền thống:
- **Hồi quy Tuyến tính (Linear Regression):** Phải vẽ 6 biểu đồ chẩn đoán phần dư (Residuals plots) theo chuẩn giáo trình.
- **Hồi quy Logistic:** Phải đánh giá Đa cộng tuyến (VIF), Khoảng cách Cook (Cook's distance) để tìm điểm ngoại lai, và So sánh AIC để chọn mô hình tối ưu.
- **Hồi quy Cox (Survival Analysis):** Phải kiểm tra giả định tỷ lệ rủi ro (Proportional Hazards Assumption - Schoenfeld residuals), Đa cộng tuyến (VIF) và Giả định tuyến tính (Log-linearity).

## 🎨 Trực quan hóa (ggplot2 & Grammar of Graphics)
Cấm Agent tự ý vẽ biểu đồ khi chưa có sự đồng thuận. Phải hỏi User 5 yếu tố cốt lõi của Grammar of Graphics trước khi chạy code:
1. Dữ liệu & Biến số (Aesthetics)
2. Loại biểu đồ (Geometries)
3. Có phân ô không (Facets)
4. Phong cách (Themes) - bắt buộc ưu tiên theme_classic() và Medical palettes (ví dụ: `ggsci::scale_color_jama()`).
5. Tiêu đề và Nhãn (Labels) bằng tiếng Việt chuẩn y văn.

## 🤖 Quy Trình Vận Hành Agentic (Agentic Behavior Rules)
- **Tác vụ mới:** Luôn bắt đầu bằng việc tạo danh sách TODO trong R-Studio qua công cụ `r-studio::create_task_list` và cập nhật bằng `r-studio::update_task_status`.
- **Tự sửa lỗi (Self-debugging):** Khi chạy R bị lỗi, Agent phải tự động gọi `r-studio::clean_error_log` để xem chi tiết lỗi, **hỏi ý kiến User**, tự chỉnh sửa mã nguồn bằng `modify_code_section` và chạy lại. 
- **Xác minh đầu ra:** Trước khi bàn giao báo cáo Quarto, bắt buộc phải chạy thử lệnh render thành công.
- **Thư mục lưu trữ:** Lưu file .qmd và file .R vào chung một thư mục cùng tên.
