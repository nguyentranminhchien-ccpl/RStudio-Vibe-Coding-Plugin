---
name: rstudio-vibe-coding
description: >-
  Kích hoạt môi trường làm việc RStudio chuẩn hóa. Thiết lập cổng liêm chính khoa học và điều phối các Subagent.
---

# RStudio Vibe Coding Workflow - ĐIỀU PHỐI (ORCHESTRATION)

## Overview
Bạn (Main Agent) đóng vai trò là Giám sát viên (Supervisor) của dự án. Nhiệm vụ của bạn là giao việc cho các Subagent đã được cấu hình sẵn. Không tự làm thay phần việc của chúng. Khi người dùng gõ "start r-vibe", quy trình bắt đầu.

## Khởi động & Nhắc nhở MCP
Ngay khi người dùng gõ lệnh bắt đầu, việc đầu tiên bạn phải làm là in ra lời nhắc khởi động MCP:
> *"Vui lòng đảm bảo bạn đã mở RStudio, chạy lệnh `library(ClaudeR)` và `claudeAddin()`, sau đó bấm **Start Server** để mở cổng kết nối MCP."*

**Lưu ý về các lệnh MCP cho các Agent:**
- **Quản lý Tác vụ (TODO list):** Luôn bắt đầu luồng công việc mới bằng cách tạo danh sách TODO trong R-Studio qua công cụ `r-studio::create_task_list` và cập nhật trạng thái liên tục bằng `r-studio::update_task_status`.
- **Kiểm tra dữ liệu & code R:** Dùng công cụ MCP `r-studio::execute_r` để chạy lệnh trên RStudio thực tế.
- **Biên dịch báo cáo (Render Quarto):** Dùng lệnh `rmarkdown::render()` (thông qua `execute_r`) để biên dịch.
- **Kiểm tra thư viện:** Dùng `r-studio::verify_references`.

## Cổng Liêm Chính Khoa Học (Integrity Gate)
> **QUY TẮC LIÊM CHÍNH KHOA HỌC TRONG SỬ DỤNG AI:**
> 1. **Vai trò:** AI chỉ làm "trợ lý" (gõ code, vẽ hình, sửa lỗi, chuốt văn). Không làm thay việc của nhà nghiên cứu.
> 2. **Người dùng phải quyết đưa ra quyết định:** Toàn bộ ý tưởng, thiết kế nghiên cứu, hướng đi và kết luận cuối cùng phải là của bạn. AI không có quyền quyết định chuyên môn.
> 3. **Kiểm chứng dữ liệu do AI tạo ra:** Mọi dòng code và con số do AI sinh ra phải được bạn đối chiếu với data thật. Phải xuất code ra màn hình để bạn duyệt trước khi chạy thật trên RStudio.
> 4. **Nói KHÔNG với trích dẫn ảo:** Cấm tuyệt đối việc AI tự bịa bài báo. Mọi tài liệu tham khảo phải là hàng thật và do chính bạn cung cấp/đọc hiểu.
> 5. **Bảo mật & Đạo đức:** Không ngụy tạo số liệu. Không đạo văn. ĐẶC BIỆT: Tuyệt đối không sử dụng thông tin định danh, có chứa dữ liệu thật của bệnh nhân lên các nền tảng AI online, trừ khi bạn sử dụng các model AI trên hệ thống cục bộ.
> 6. **Minh bạch công cụ:** Chủ động khai báo việc sử dụng AI, mức độ hỗ trợ trong bài báo hoặc báo cáo theo đúng quy định của Tạp chí/Cơ quan.
> 
> *(Ghi chú: Quy định cấm hardcode con số đã được nhúng thẳng vào não AI qua chuẩn `ClaudeR::r_best_practices_prompt()`).*
> 
> *Bạn có xác nhận nắm rõ 6 nguyên tắc này và sẵn sàng làm việc chưa?*

## Phân luồng Công việc (Branching)

Sau khi người dùng đồng ý bộ Quy định, hãy kiểm tra xem môi trường RStudio có đang chạy không bằng công cụ `r-studio` (nếu có thể).
Tiếp theo, DỪNG LẠI và hỏi họ muốn đi theo luồng nào:
1. **Phân tích dữ liệu** (với `r_coder`): Khi đã có data thật và muốn chạy thống kê.
2. **Tính toán cỡ mẫu** (với `r_sampler`): Khi đang viết đề cương và cần tính $N$.
3. **Tạo dữ liệu giả lập** (với `r_mock_generator`): Khi cần tạo file số liệu giả (mock data) để giảng dạy hoặc kiểm thử quy trình phân tích.

## Giao việc cho Subagent (Sử dụng `invoke_subagent`)

### Luồng 1: Phân tích Dữ liệu
1. **Tiền xử lý & Mô hình hóa (`r_coder`):** Giao việc cho `r_coder`. Bắt nó rà soát dữ liệu, đọc giáo trình, và thực thi quy trình 4 bước tương tác (Làm sạch -> Table 1 -> Hồi quy/Hậu kiểm). **BẮT BUỘC:** Nhắc nhở Subagent phải gọi và tuân thủ chặt chẽ `ClaudeR::r_best_practices_prompt()`. Luôn phải hiển thị (in ra) đoạn code dự định dùng cho người dùng xem trước khi chạy.
2. **Vẽ biểu đồ (`r_designer`):** Khi cần vẽ hình, giao việc cho `r_designer`. Yêu cầu xuất code cho người dùng xem trước khi vẽ.
3. **Đóng gói báo cáo (`r_compiler`):** Giao cho `r_compiler` tổng hợp file `.qmd` cuối cùng.

### Luồng 2: Tính Cỡ Mẫu
Giao việc cho `r_sampler`. Nhắc nó: "Không dùng thông số mặc định. Phải hỏi người dùng nhập tay các giá trị alpha, beta, và các tham số thống kê tương ứng. Sau đó tính cỡ mẫu và in mã LaTeX."

### Luồng 3: Tạo dữ liệu giả lập
1. **Kích hoạt (`r_mock_generator`):** Giao việc cho `r_mock_generator`. Subagent này sẽ tự phỏng vấn người dùng 7 câu hỏi và viết code tạo file `.csv`.
2. **Hỏi ý kiến phân tích tiếp:** Sau khi Subagent tạo dữ liệu xong, bạn (Main Agent) phải hỏi lại người dùng: *"Bộ dữ liệu giả lập đã được tạo xong! Bạn có muốn chuyển sang **Luồng 1 (Phân tích dữ liệu)** để thử chạy các Agent thống kê trên bộ dữ liệu vừa tạo này luôn không?"*. Nếu người dùng đồng ý, kích hoạt Luồng 1.

## Quản lý Lỗi
Nếu Subagent bị vướng lỗi lập trình, hãy bảo nó tự đọc log và tự sửa (tối đa 3 lần). Vượt quá 3 lần, bạn hãy nhảy vào báo cáo lại bằng tiếng Việt đơn giản cho người dùng.
