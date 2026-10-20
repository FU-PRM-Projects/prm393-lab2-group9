# Quyết định thiết kế

10 quyết định quan trọng nhất, mỗi quyết định có lý do gắn với persona, một heuristic của Nielsen, WCAG, hoặc một ràng buộc thật (phạm vi, thời gian, nền tảng). Mã màn và mã flow giống Figma (xem [`ux/user-flow.md`](../ux/user-flow.md)).

---

## 1. Bảng quyết định

| # | Quyết định | Lý do | Thấy ở Figma |
|---|---|---|---|
| 1 | **Một deadline được chia thành giai đoạn phủ kín số ngày tới hạn; mỗi giai đoạn có từ ngày, đến ngày và giờ nhắc mỗi ngày** | Minh có deadline dài cả tháng (paper 15/11, 31 ngày) và hay lỡ mốc giữa chừng. Nielsen #1 (hiển thị trạng thái): app luôn ghi "Đã chia 31/31 ngày" và "Ngày 3/7" để người dùng biết còn thiếu gì | `6b3`, `6b4`, `6b5`, `7c`, `7s`; flow C1 |
| 2 | **Thêm bước Mô tả; AI gợi ý giai đoạn từ mô tả, người dùng sửa, xoá, tạo lại hoặc tự nhập** | Minh muốn ghi "ai làm phần nào" trước khi chia. Nielsen #3 (người dùng kiểm soát): AI chỉ đề xuất, không tự lưu. Nielsen #9 (phục hồi lỗi): khi gọi AI lỗi, mô tả vẫn được giữ và có hai lối ra Thử lại, Tự nhập tay | `6b2a`, `6b3` (4 trạng thái); flow C1 |
| 3 | **Ghi chép và tài liệu gắn vào từng giai đoạn (tệp DOCX, PDF, XLSX, ZIP, ảnh, link)** | Pain point của Minh: "Không nhớ đã ghi chú, đã làm gì ở từng giai đoạn"; đang phải mở Notion để lưu. Nielsen #6 (nhận ra thay vì phải nhớ) | `7s`, `7s1`, `7s2`, `7t`; flow C1 phần 2, C2 |
| 4 | **Thông báo mở thẳng đúng màn của việc đó; thông báo đẩy có "Nhắc lại 15 phút"** | Minh dễ sót việc khi chuyển qua lại nhiều app. Quốc Huy bị nhắc giữa cuộc họp nên tắt hết thông báo. Nielsen #7 (linh hoạt, hiệu quả): một chạm từ thông báo tới việc cần làm, một chạm để lùi lời nhắc | `13p`, `13`; flow C3 |
| 5 | **Lịch nhiệt theo độ nặng (không theo số việc); mỗi ô có số độ nặng và khuôn mặt mascot** | Một Quiz và một Đồ án không nặng như nhau, nên đếm số việc không cho thấy ngày nặng thật. WCAG 1.4.1: màu không phải tín hiệu duy nhất. Màn `12` giải thích thang 1 → 8+ | `3`, `4`, `12`; flow C4 |
| 6 | **Chỉ gợi ý dời việc sang ngày nhẹ trước hạn nộp; khi không còn ngày nhẹ, gợi ý chia nhỏ việc thay vì dời** | Nielsen #5 (ngăn lỗi): không cho tạo kế hoạch dời quá hạn. Đăng Khoa bỏ kế hoạch khi phải tự sắp lại, nên app phải đưa ra lối đi tiếp thay vì báo "không được" | `4b`, `4c`, `4d`, `2c0`; flow C4, P4 |
| 7 | **Nút "Hoàn thành deadline" chỉ bật khi đã tick đủ giai đoạn, và cần xác nhận qua dialog** | Nielsen #5 (ngăn lỗi) và #3 (kiểm soát): tránh bấm nhầm bằng một tay. Dòng chữ "Tick đủ 3 giai đoạn để hoàn thành" cho biết vì sao nút đang tắt | `7`, `7d`, Overlay Hoàn thành, `8`; flow C2 |
| 8 | **Việc quá hạn có 3 cách xử lý: Đã nộp muộn, Dời hạn, Bỏ deadline (Bỏ cần xác nhận)** | Nielsen #9 (giúp nhận ra và sửa lỗi): chỉ hiện màu đỏ thì người dùng không biết làm gì tiếp. Màn `7o` còn giải thích "Vì sao bị tính quá hạn" | `7o`, `7o2`, Overlay Bỏ, `5o1`–`5o3`; flow P3 |
| 9 | **Còn 4 tab (Hôm nay, Kế hoạch, Deadline, Hồ sơ): bỏ tab Lộ trình và các thẻ thói quen (uống nước, vận động, ngủ); thay bằng chuỗi ngày đúng hạn** | Ràng buộc phạm vi: lab chấm theo flow chính, và Lab 3 phải dựng mọi màn. Nielsen #8 (tối giản): thẻ thói quen không phục vụ nỗi đau chính của Minh là lỡ deadline. Chuỗi đúng hạn vẫn giữ động lực "nộp đúng hạn" | `2`, `2f`, `BottomNav/iPhone · 4 tab` |
| 10 | **Thiết kế luôn Đăng nhập (Google và email), Hồ sơ, và 2 màn công cụ demo (Cấu hình ứng dụng, Kiểm tra lỗi)** | Ràng buộc từ Lab 3: bắt buộc Google Sign-In, hồ sơ, đăng xuất, Remote Config và Crashlytics có nút demo. Thiết kế trước để Lab 3 không phải thêm màn ngoài Figma | `1`–`1h`, `10`, `10e`, `14`, `15`; flow P2, P6, S3 |

---

## 2. Checklist accessibility và responsive

Kiểm tra trên file Figma ngày 20/10/2026 (đọc bằng script trên page 03 và 05). Tỉ lệ contrast tính theo công thức WCAG 2.x.

| Mục | Kết quả | Bằng chứng | Việc cần làm |
|---|---|---|---|
| Contrast chữ thường ≥ 4.5:1 | **Đạt một phần** | `on-surface` 15.6:1; `on-surface-variant` trên `surface-card` 6.31:1; `error` trên `tint/red` 5.30:1; `warning` trên `tint/orange` 4.79:1; chữ `on-surface` trên `heat/5` 4.79:1. **`success` #1F9D63 chỉ đạt 3.46:1 trên trắng, 3.24:1 trên `surface-card`, 3.02:1 trên `tint/green`** | Không dùng `success` cho chữ dưới 18 sp; hoặc đổi `success` sang màu đậm hơn (ví dụ bản cũ `#1B6B44`) |
| Contrast chữ lớn và điều khiển UI ≥ 3:1 | **Đạt** | `outline` trên trắng 3.93:1, trên `surface-card` 3.67:1; `primary` trên trắng 6.39:1; `primary` trên `primary-container` 5.11:1 | — |
| Vùng chạm ≥ 48 × 48 dp | **Đạt một phần** | 24 instance `Button` đều cao 48 dp; 17 instance `BottomNav` cao 64 dp | Đo thêm nút icon (Back, chuông, bút chì), chip và ô ngày ở `3` |
| Chữ nội dung ≥ 14 sp | **Chưa đạt** | 604 trên 1610 lớp chữ ở page 03 có cỡ 11–13 sp (2 lớp 11 sp, 396 lớp 12 sp, 206 lớp 13 sp). Một số là nội dung, không chỉ là nhãn, ví dụ "Nộp Lab 2 trước 23:59 để giữ chuỗi" (13 sp, `2`), "WDP301 · sớm 1 ngày" (12 sp, `2f`), "Sang T5 và T7 · Rất nặng → Nặng" (13 sp, `4`) | Nâng các dòng nội dung lên `Label/14`; chỉ giữ 12–13 sp cho nhãn tab, nhãn "BƯỚC n/5", số trên lịch |
| Không dùng màu làm tín hiệu duy nhất | **Đạt** | `Tag/Hạn nộp` luôn có chữ ("Trễ 1 ngày", "Còn 6 giờ"); ô lịch có số độ nặng và khuôn mặt; `Notification/Row` có icon riêng theo loại; màn `12` giải thích ý nghĩa | — |
| Dùng Auto Layout và constraint | **Đạt một phần** | 71/71 màn có Auto Layout (màn 360 × 800 xếp dọc: App bar, content, nút cố định cuối màn hoặc thanh điều hướng). Ở page 05, chỉ component `TypeIcon` không dùng Auto Layout | — |
| Component dùng token, không gán cứng | **Chưa đạt** | 435 trên 1043 màu nền (solid fill) trong component có gắn Variable. Còn gán cứng ở: `OptionGroup · Loại việc` (180), `ChipGroup · Môn học` (78), `SwatchGroup · Màu` (36), `TypeIcon` (30), `BottomNav` (28), `Card` (26), `Loading state` (9), `Error state` (8), `Empty state` (6), `Switch` (4), `PasswordField` (3). Bo góc 14, 16, 20 chưa có Variable | Gắn Variable cho các màu trên; thêm `radius/16`, `radius/20` |
| Đã kiểm tra ở 360 dp | **Đạt** | 71 màn ở page 03 có khung màn hình bên trong 360 × 800 dp (khung `Device · …` 388 × 828 chỉ là viền điện thoại bao ngoài). Nội dung dùng lề 16 dp (Kế hoạch dùng 12 dp) | Xuất PNG khung 360 × 800 bên trong (không lấy viền) vào `assets/figma/` |
| Đã kiểm tra ở 412 dp | **Chưa kiểm tra** | Chưa có frame 412 dp | Nhân bản `3` và `5`, đổi rộng 412 dp, chụp ảnh để làm bằng chứng |
| Chữ phóng to 130% (Quốc Huy) | **Chưa kiểm tra** | Không có frame kiểm tra trong Figma | Không bắt buộc theo đề; ghi là mục kiểm tra ở Lab 3 |

Sau khi sửa trong Figma, cập nhật cột Kết quả và thêm ảnh chụp vào `assets/figma/`.
