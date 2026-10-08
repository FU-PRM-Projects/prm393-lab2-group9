# Screen spec — ý đồ từng màn hình

Mỗi màn hình trả lời một câu hỏi của Hân và có đúng một hành động chính. Chi tiết dựng giao diện nằm ở `handoff/flutter-handoff.md`.

| Mã | Màn hình | Câu hỏi màn hình trả lời | Hiển thị nội dung gì | Hành động chính | Thuộc flow |
|---|---|---|---|---|---|
| S01 | Đăng nhập | "Vào app bằng cách nào?" | Mascot Tụi Nốt trên nền họa tiết, tên app "Nốt", một câu giới thiệu, lỗi đăng nhập (nếu có) | Đăng nhập bằng Google | 1, 5 |
| S02 | Hôm nay | "Bây giờ làm gì tiếp?" | Lời chào và avatar; banner tóm tắt (số việc hôm nay, số việc quá hạn, Nốt Tập Trung); thẻ "Làm tiếp" cho việc gấp nhất; lịch bận hôm nay; danh sách "Deadline gần nhất" | Chạm thẻ "Làm tiếp" để mở Chi tiết deadline | 1, 2, 4, 5 |
| S03 | Kế hoạch | "Ngày nào đang quá tải?" | Lịch nhiệt tháng (ô màu heat-0 đến heat-5, số việc, khuôn mặt mascot), chú giải 5 mức bằng chữ, thẻ tóm tắt ngày đang chọn | Chạm một ngày để mở Chi tiết ngày | 3, 4 |
| S04 | Deadline | "Việc nào gấp nhất?" | Banner tóm tắt; segmented "Theo hạn / Theo nhóm việc"; các nhóm Quá hạn, Hôm nay, Tuần này, Sau đó, Đã nộp (thu gọn); mỗi nhóm có mascot ở tiêu đề và số lượng | FAB "+" mở Thêm deadline | 1, 2 |
| S05 | Lịch bận | "Hôm nay còn trống lúc nào?" | Dải 7 ngày của tuần; danh sách khối lịch bận của ngày chọn (lịch học, họp nhóm, freelance) xen với các khung trống "15:00–17:00 · Trống 2 giờ" | Chạm một khung trống để thêm việc vào đó | 4 |
| S06 | Thêm / sửa deadline | "Ghi việc này thế nào cho nhanh?" | 3 trường bắt buộc: Tên, Nhóm việc, Hạn nộp. 2 trường tùy chọn: Mức quan trọng (mặc định Vừa), Khung giờ làm (điền sẵn khi mở từ Lịch bận hoặc Kế hoạch) | Lưu deadline | 1, 4 |
| S07 | Chi tiết deadline | "Việc này đang tới đâu?" | Tên, nhóm việc, mức quan trọng, hạn nộp kèm nhãn trạng thái, tiến độ "2/3 buổi", danh sách buổi làm có checkbox | Đánh dấu đã nộp | 2 |
| S08 | Đã nộp | "Xong chưa? Tuần này còn bao nhiêu?" | Mascot Nốt Xong, tên việc vừa nộp, thời điểm nộp so với hạn, tiến độ tuần "Đã nộp 3/7 việc tuần này" | Về Deadline | 2 |
| S09 | Chi tiết ngày | "Ngày này có gì, dời bớt được không?" | Tiêu đề ngày và nhãn mức nặng ("Thứ Ba 14/10 · Quá tải"); segmented "Danh sách / Theo giờ"; lịch bận và buổi làm của ngày, mỗi buổi làm có nút "Dời" | Dời một việc sang ngày khác | 3 |
| S10 | Hồ sơ | "Nốt nhắc mình lúc nào?" | Ảnh, tên, email từ Google; công tắc "Nhắc trước hạn" và lựa chọn 1 giờ / 1 ngày / 2 ngày; nút Đăng xuất | Lưu thay đổi nhắc hạn (lưu ngay khi đổi) | 5 |

## Dữ liệu mẫu dùng thống nhất trên mọi màn

| Deadline | Nhóm việc | Hạn | Mức quan trọng | Tiến độ |
|---|---|---|---|---|
| Quiz ITE302c tuần 1 | Môn học · ITE302c | Trễ 1 ngày | Cao | 0/1 buổi |
| Lab 2: Thiết kế UI | Môn học · PRM393 | Hôm nay 23:59 | Cao | 2/3 buổi |
| Báo cáo sprint 2 | Môn học · WDP301 | Còn 2 ngày | Vừa | 0/2 buổi |
| Tiểu luận chương 3 | Môn học · MLN111 | Còn 2 ngày | Vừa | 1/3 buổi |
| Pitch deck | Môn học · EXE201 | Còn 6 ngày | Vừa | 0/2 buổi |
| Đề cương đồ án | Đồ án | Còn 12 ngày | Cao | 1/4 buổi |

| Lịch bận | Loại | Thời gian |
|---|---|---|
| MLN111, PRM393, WDP301 | Lịch học | Thứ Ba và thứ Sáu, 9:30–17:15 |
| EXE201 | Lịch học | Thứ Năm, 15:00–17:15 |
| Họp nhóm WDP301 | Họp nhóm | Thứ Tư, 20:00–21:00 |
| Landing page cho khách | Freelance | Thứ Bảy, 9:00–12:00 |
