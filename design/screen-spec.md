# Screen spec — Ý đồ từng phân hệ và màn hình

Hệ thống giao diện Nốt (Study Planner) trên Figma (page `03 Final UI` & `06 Prototype`) được tổ chức thành **7 phân hệ** với hơn 25 khung thiết bị, phục vụ 4 persona (Minh, Đăng Khoa, Bảo Ngọc, Quốc Huy). Chi tiết dựng giao diện và ánh xạ Flutter xem tại [`handoff/flutter-handoff.md`](file:///e:/prm393-lab2-group9/handoff/flutter-handoff.md).

---

## 1. Bảng phân hệ và màn hình

| Nhóm / Mã | Phân hệ · Màn hình | Device Frame (Figma) | Câu hỏi màn hình trả lời | Hiển thị nội dung gì | Hành động chính | Phục vụ Persona & Flow |
|---|---|---|---|---|---|---|
| **01 · Xác thực** | 1.1 Đăng nhập & Đăng ký | Device 1, 1b, 1c, 1d | "Vào app bằng cách nào?" | Mascot Nốt, form Đăng nhập/Đăng ký (Google / Email), thông báo lỗi và trạng thái xác thực | Đăng nhập / Chuyển sang Đăng ký | Tất cả (P2, S1) |
| | 1.2 Quên mật khẩu | Device 1e, 1f, 1g, 1h | "Làm sao lấy lại quyền truy cập?" | Nhập email nhận mã OTP, xác minh OTP 6 số, đặt mật khẩu mới, thông báo thành công | Đặt lại mật khẩu | Tất cả (P3, S1) |
| **02 · Làm quen** | 2.1 Onboarding 3 câu hỏi & Cá nhân hoá | Device 2a, 2b, 2c | "App này giúp được gì cho mình?" | 3 câu hỏi trắc nghiệm (Năm học & khối ngành, khung giờ học/làm việc, thói quen chia nhỏ việc), mascot chào đón | Hoàn thành cá nhân hóa | Bảo Ngọc, Đăng Khoa (P1) |
| **03 · Hôm nay** | 3.1 Hôm nay | Device 3 (gốc) | "Bây giờ làm gì tiếp?" | Banner tóm tắt công việc & mascot Nốt Tập Trung; thẻ "Làm tiếp" việc gấp nhất; dải lịch bận hôm nay; deadline gần nhất | Chạm thẻ "Làm tiếp" hoặc việc gấp | Tất cả (C1, C4) |
| | 3.2 Chia nhỏ việc & Xếp giờ | Device 2c0, 2c3 | "Chia việc lớn này ra các slot thế nào?" | Đề xuất chia nhỏ deadline thành các slot 45 phút, gợi ý khung giờ trống để kéo/xếp vào lịch | Xác nhận xếp lịch slot 45p | Bảo Ngọc, Minh (P7) |
| | 3.3 Bảng thành tích tuần | Device 3b | "Tuần này mình đã hoàn thành được bao nhiêu?" | Tổng kết việc đã nộp trong tuần, chuỗi ngày đúng hạn (streak), điểm tập trung, mascot Nốt Xong | Tiếp tục duy trì phong độ | Tất cả (C3) |
| **04 · Kế hoạch** | 4.1 Lịch nhiệt & Chi tiết ngày | Device 4, 4a, 4b, 4c, 3d | "Ngày nào đang quá tải? Dời bớt việc đi đâu?" | Lịch nhiệt tháng heat-0 đến heat-5 (số việc, mascot); danh sách việc và timeline giờ của ngày; bottom sheet dời việc | Chạm ngày quá tải để dời việc | Tất cả (C4, S2) |
| | 4.2 Tuần & Giờ bận & Hoãn việc | Device 4.2 | "Tuần này trống lúc nào? Thêm giờ bận thế nào?" | Dải 7 ngày theo tuần; danh sách ca làm/lịch học xen khung trống; nút thêm giờ bận và hoãn việc tự động | Thêm giờ bận / Hoãn việc | Đăng Khoa, Quốc Huy (P8, C4) |
| **05 · Thông báo** | 5.1 Danh sách thông báo | Device 13A (nền nhạt), 13B (hộp thư) | "Có nhắc nhở hoặc thay đổi gì mới?" | Danh sách thông báo theo nhóm: Đến hạn, Thay đổi lịch, Lời khen thành tích; trạng thái đã đọc/chưa đọc | Mở chi tiết deadline từ thông báo | Tất cả (C3, P6) |
| | 5.2 Thông báo đẩy màn khóa | Device 13c | "Nhắc nhở hiện ngoài màn hình thế nào?" | Thẻ thông báo lock screen hiển thị tên deadline, thời gian còn lại, hành động nhanh (Đã xong / Nhắc lại sau 15p) | Chạm vào xem hoặc đánh dấu xong | Minh, Đăng Khoa, Quốc Huy |
| **06 · Deadline** | 6.1 Danh sách deadline | Device 6.1 | "Việc nào gấp nhất? Phân nhóm ra sao?" | Segmented "Theo hạn / Theo môn-dự án"; các nhóm Quá hạn, Hôm nay, Tuần này, Sau đó, Đã nộp | FAB "+" thêm deadline | Tất cả (C1, P4) |
| | 6.2 Lọc theo môn & dự án | Device 6.2 | "Môn/dự án này có những đầu việc nào?" | Danh sách nhóm theo môn học (PRM393, MLN111, WDP301...) và dự án NCKH / freelance | Xem tiến độ từng môn/dự án | Minh, Bảo Ngọc (P4) |
| | 6.3 Thêm deadline nhanh / AI | Device 6.3 | "Ghi nhận deadline mới thế nào cho nhanh?" | Form nhập nhanh hoặc dán văn bản để AI gợi ý phân rã thành các giai đoạn (phase) | Lưu deadline & tạo giai đoạn | Minh, Bảo Ngọc (C1, P7) |
| | 6.4 Chi tiết giai đoạn, nộp & ghi chép | Device 7d, 7s, 7s1, 7s2, 7t | "Giai đoạn này ai phụ trách? File nộp ở đâu?" | Stepper 4 giai đoạn, phân công thành viên, chip tệp đính kèm (DOCX, PDF, XLSX, ZIP), ghi chép nhóm, nút Nộp | Đánh dấu hoàn thành giai đoạn / Nộp | Minh, Lan (C2, C3) |
| | 6.5 Sửa & Xóa deadline | Device Sửa, Overlay Xóa, Device 5e | "Cần đổi hạn hoặc hủy việc thì làm sao?" | Form chỉnh sửa thông tin deadline, dialog xác nhận xóa có cảnh báo mất giai đoạn | Xác nhận sửa / Xóa (có hoàn tác) | Tất cả (P5) |
| | 6.6 Xử lý quá hạn | Device 5o1, 7o2, 5o2, Overlay Bỏ, 5o3 | "Việc trễ hạn rồi thì giải quyết thế nào?" | 3 tùy chọn cứu vãn: Nộp muộn (ghi nhận thời gian), Dời hạn mới, hoặc Bỏ việc (xác nhận) | Chọn cách xử lý quá hạn | Tất cả (P6, S2) |
| **07 · Hồ sơ · Cài đặt** | 7.1 Hồ sơ cá nhân | Device 7.1 | "Thông tin tài khoản và kết nối thế nào?" | Avatar, tên sinh viên/người dùng, khối ngành, liên kết Google Calendar | Xem và chỉnh sửa hồ sơ | Tất cả |
| | 7.2 Cài đặt & Giờ họp (DND) | Device 7.2 | "Làm sao để app không làm phiền khi đang họp?" | Cài đặt nhắc hạn, chế độ Không làm phiền (DND) tự động im lặng trong khung giờ họp cố định | Lưu khung giờ DND | Quốc Huy, Đăng Khoa (P8) |
| | 7.3 Hướng dẫn sử dụng | Device 7.3 | "Tính năng này dùng thế nào?" | Các thẻ mẹo hướng dẫn: cách chia nhỏ việc 45p, cách dời việc tránh quá tải, mẹo quản lý tệp | Đọc hướng dẫn | Bảo Ngọc, người dùng mới |
| | 7.4 Demo kiểm tra lỗi & Text scale 130% | Device 7.4 | "Giao diện có bị vỡ khi chữ phóng to không?" | Bảng chuyển đổi giả lập lỗi mạng (offline), xung đột lịch và text scale 130% để kiểm tra tính co giãn UI | Bật/tắt kiểm thử responsive | Quốc Huy (Hỗ trợ trợ năng) |

---

## 2. Dữ liệu mẫu thống nhất toàn hệ thống (Mock Data)

Bộ dữ liệu mẫu thống nhất phản ánh đúng thực tế đồ án NCKH của Minh, ca làm xoay của Đăng Khoa, bài tập đồ họa của Bảo Ngọc và lịch họp của Quốc Huy:

### 2.1 Deadline lớn nhiều giai đoạn (NCKH Paper — Minh làm Lead)
- **Tên:** Báo cáo Khoa học NCKH (Paper 15/11)
- **Môn / Dự án:** Nghiên cứu Khoa học (NCKH)
- **Hạn chót:** 15/11 23:59 (Tổng thời lượng: 31 ngày)
- **Mức quan trọng:** Cao
- **Các giai đoạn (Phases):**
  1. *Giai đoạn 1 (Đề cương nghiên cứu):* Hạn 25/10 · Phụ trách: Lan · Trạng thái: Đã hoàn thành (100%)
  2. *Giai đoạn 2 (Thu thập & xử lý dữ liệu):* Hạn 02/11 · Phụ trách: Minh · Trạng thái: Đang thực hiện (60%)
  3. *Giai đoạn 3 (Bản thảo báo cáo):* Hạn 10/11 · Phụ trách: Minh & Lan · Trạng thái: Chưa bắt đầu
  4. *Giai đoạn 4 (Phản biện & nộp bài cuối):* Hạn 15/11 · Phụ trách: Cả nhóm · Trạng thái: Chưa bắt đầu
- **Tệp đính kèm (Attachments):**
  - `De-cuong-NCKH-v2.docx` (DOCX · 2.4 MB)
  - `So-lieu-khao-sat-oct.xlsx` (XLSX · 1.1 MB)
  - `Huong-dan-trinh-bay.pdf` (PDF · 4.8 MB)
  - `Source-code-notebooks.zip` (ZIP · 18.2 MB)

### 2.2 Các deadline khác trong tuần
| Deadline | Nhóm việc | Hạn nộp | Mức quan trọng | Tiến độ / Trạng thái | Persona liên quan |
|---|---|---|---|---|---|
| Lab 2: Thiết kế UI Figma | Môn học · PRM393 | Hôm nay 23:59 | Cao | 2/3 buổi (Đang làm) | Tất cả sinh viên |
| Quiz ITE302c tuần 1 | Môn học · ITE302c | Trễ 1 ngày (Quá hạn) | Cao | 0/1 buổi (Cần xử lý quá hạn) | Minh, Đăng Khoa |
| Moodboard & Typography poster | Môn học · Graphic Design | Còn 2 ngày | Vừa | 2/4 slot 45p | Bảo Ngọc |
| Báo cáo sprint 2 | Môn học · WDP301 | Còn 3 ngày | Vừa | 1/2 buổi | Minh, Đăng Khoa |
| Tiểu luận Triết học | Môn học · MLN111 | Còn 5 ngày | Vừa | 0/3 buổi | Bảo Ngọc |
| Code review & Release PR | Công việc / Dự án | Ngày mai 17:00 | Cao | Chưa nộp (DND 14:00-16:00) | Quốc Huy |

### 2.3 Lịch bận cố định & Ca làm việc
| Hoạt động | Loại lịch | Thời gian | Người dùng |
|---|---|---|---|
| Học trên trường (PRM393, WDP301) | Lịch học | Thứ Ba & Thứ Sáu, 09:30–17:15 | Minh, Đăng Khoa |
| Ca làm thêm quán cà phê | Ca làm việc | Thứ Hai, Tư, Sáu, Bảy, 18:00–22:00 | Đăng Khoa |
| Giờ họp Sprint / Daily meeting (DND) | Công việc | Thứ Hai đến Thứ Sáu, 14:00–15:30 | Quốc Huy |
| Ca trực đồ án xưởng in | Thực hành | Thứ Bảy, 08:30–11:30 | Bảo Ngọc |
