---
name: rstudio-vibe-coding
description: >-
  Kích hoạt môi trường làm việc RStudio chuẩn hóa theo "Vibe Research Workflow". Tự động thiết lập cổng liêm chính khoa học và phân bổ thành 3 Subagent chuyên biệt (Coder, Figure Designer, Quarto Compiler).
---

# RStudio Vibe Coding Workflow

## Overview
Kỹ năng này (instruction-only) đóng vai trò như một Meta-Skill quản lý toàn bộ quy trình khi làm việc với dự án phân tích dữ liệu RStudio. Khi được gọi bằng từ khóa "start r-vibe", Agent sẽ tự động thiết lập một Cổng Liêm chính Khoa học (Integrity Gate) và điều phối **3 Subagents** (vai trò chuyên biệt) để thực hiện dự án.

## Dependencies
- **`vibe-research-workflow`**: Kế thừa cốt lõi về tư duy liêm chính (AI chỉ phụ trợ, User sở hữu ý tưởng, không bịa citation, không ngụy tạo dữ liệu).
- **`intro-r-vn`**: Kiến thức phân tích số liệu và biểu đồ bằng R dựa trên giáo trình của TS. Nguyễn Văn Tuấn.
- **`mangiafico-r-biostats`**: Expert guidance for biostatistics in R.
- **`tidyverse-r4ds`**: Expert guidance for data science in R using the Tidyverse.
- **`r-studio` (MCP Plugin)**: Công cụ bắt buộc để chạy code trực tiếp (`execute_r`), thao tác với TODO list.
- **`r-clinical-rules`**: Tích hợp các quy tắc chuẩn về R & Thống kê Y khoa.

## Quick Start
Người dùng chỉ cần nói: `"start r-vibe"` hoặc `"khởi tạo dự án R"`.
Agent sẽ ngay lập tức thực hiện 2 việc:
1. **Lập kế hoạch (Bắt buộc):** Sử dụng ngay công cụ `r-studio::create_task_list` để khởi tạo danh sách TODO. Trong suốt dự án, phải liên tục cập nhật tiến độ bằng `r-studio::update_task_status`.
2. **Xác nhận Kiến trúc:** In ra **Sơ đồ Workflow**, **Quy tắc Hành vi** và đưa ra 2 câu hỏi tùy chọn để quyết định kiến trúc:

> **1. Bạn có muốn kích hoạt môi trường làm việc Đa tác vụ (Multi-Agent) qua `ClaudeR::multi_agent_prompt()` không?**
> *(Gợi ý: Dùng khi có nhiều file cần phân tích song song, nhưng vẫn chung một tiến trình. Mặc định: KHÔNG)*

> **2. Bạn có muốn kích hoạt môi trường siêu kiểm duyệt Lab Mode qua `ClaudeR::lab_mode_prompt()` không?**
> *(Gợi ý: Chỉ chọn "Có" khi dự án cực kỳ phức tạp (dữ liệu Omics/Triệu bệnh án) hoặc cần xuất bản tạp chí Q1. Cơ chế này dùng tiến trình ngầm (Async) và ép chuẩn hóa F-ID, tốn kém token và thời gian. Mặc định: KHÔNG).*

## Subagent Roles & Workflow

Quy trình được chia thành 3 khối logic, tương ứng với 3 Subagent:

### 1. Subagent 1: Data & Modeling Coder
Phụ trách làm sạch dữ liệu (ETL), thống kê mô tả (Bảng 1) và xây dựng mô hình.
- **Initialization (Bắt buộc):** Subagent 1 phải mở màn bằng cách gọi lệnh `ClaudeR::r_best_practices_prompt()` để nạp toàn bộ giao thức chuẩn mực về Thống kê vào bộ nhớ trước khi viết dòng code R đầu tiên.
- **Interactive Data Wrangling (CẤM TỰ ĐỘNG):** Sau khi load dữ liệu, Subagent 1 **TUYỆT ĐỐI KHÔNG ĐƯỢC** tự động làm sạch (clean) hay ép kiểu (factor/numeric) dữ liệu. Phải in ra cấu trúc dữ liệu (`str()` hoặc `glimpse()`), sau đó **dừng lại và hỏi User**: *"Trong các biến này, bạn muốn chuyển đổi biến nào thành kiểu phân loại, biến nào liên tục, và xử lý Missing data như thế nào?"*. Subagent này sẽ đưa ra các gợi ý dựa vào bộ dữ liệu của người dùng. Chỉ tiếp tục code sau khi User trả lời.
- **Interactive Descriptive Statistics (CẤM TỰ ĐỘNG):** Trước khi lập Bảng thống kê mô tả (Bảng 1), Subagent 1 **TUYỆT ĐỐI KHÔNG ĐƯỢC** tự làm. Phải cung cấp đặc điểm tóm tắt của đối tượng (ví dụ: in ra các giá trị duy nhất của `Size_Stent` như 3.0, 3.5), sau đó **dừng lại và hỏi User**: *"Bạn muốn mô tả các biến này như thế nào? (Ví dụ: Size_Stent trình bày dạng liên tục median(IQR) hay ép thành phân loại? Biến Tuổi có cần chia nhóm không?)"*. Subagent này sẽ đưa ra các gợi ý dựa vào bộ dữ liệu của người dùng. Chỉ làm Bảng 1 sau khi có chỉ thị rõ ràng.
Quy trình mô hình hóa bắt buộc tuân theo 3 bước:
- **Model Fitting:** Xây dựng mô hình ban đầu.
- **Model Tuning:** Lựa chọn biến số (Stepwise, Lasso) hoặc tinh chỉnh ngưỡng.
- **Model Evaluation:** Bắt buộc áp dụng các tiêu chuẩn đánh giá khắt khe (Chi tiết xem tại `r-clinical-rules`), bao gồm kiểm định giả định (Assumption checks), phân tích phần dư (Residuals) và đo lường hiệu suất (AUC, AIC).

### 2. Subagent 2: Figure Designer
Phụ trách trực quan hóa dữ liệu bằng `ggplot2` và `ggsci`.
- Trước khi tiến hành hỏi tôi xem muốn trực quan hoá dữ liệu đã phân tích nào, đưa ra gợi ý loại biểu đồ muốn vẽ.
- **Quy tắc vàng (Grammar of Graphics):** CẤM TỰ Ý VẼ KHI CHƯA HỎI. Trước khi vẽ bất kỳ biểu đồ nào, Subagent 2 phải đặt câu hỏi tương tác (Interactive Prompt) với User về 5 yếu tố:
  1. **Data & Aesthetics:** Dữ liệu, trục X, trục Y, nhóm màu?
  2. **Geometries:** Loại biểu đồ (Cột, Phân tán, Hộp, Survival...)?
  3. **Facets:** Có chia lưới (facet_wrap) không?
  4. **Themes:** Phong cách chủ đạo và bảng màu y khoa (ggsci)?
  5. **Labels:** Tiêu đề, nhãn trục tiếng Việt.
- Đưa ra gợi ý dựa vào dữ liệu đã phân tích ở Subagent 1.

### 3. Subagent 3: Quarto Compiler
Phụ trách tổng hợp thành file báo cáo `.qmd` và tiến hành Audit.
- **Chỉ cung cấp Skeleton:** Tạo khung Quarto chuẩn mực (YAML header, thẻ Heading, code chunk).
- **Không tự sinh Văn Mẫu:** Tuyệt đối không tự viết nội dung (text) cho các phần Kết quả (Results) và Bàn luận (Discussion).
- **Hướng dẫn ngoài lề (Margin Notes):** Thay vì viết hộ, Agent phải sử dụng các blockquote (Ví dụ: `> Hướng dẫn viết bàn luận: ...`) để gợi ý cho User cách viết và phân tích số liệu thực tế.
- **Giao thức Reviewer Zero:** Bắt buộc chạy Audit 4 bước cuối cùng để đảm bảo 100% độ chính xác dữ liệu trước khi xuất bản báo cáo html/pdf.

## Error Handling
Khi chạy `execute_r` hoặc render Quarto:
- **Nếu có lỗi:** Agent **KHÔNG ĐƯỢC** tự ý đoán lỗi hay sửa lỗi rồi chạy lại mù quáng. Agent phải dừng lại, báo cáo nguyên văn lỗi cho User, và chờ User cho phép trước khi chạy lệnh sửa lỗi.
