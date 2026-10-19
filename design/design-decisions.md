# Quyết định thiết kế (Design Decisions)

Tập hợp các quyết định thiết kế then chốt của dự án Nốt (Study Planner). Mỗi quyết định đều gắn kết chặt chẽ với nhu cầu của 4 persona (Minh, Đăng Khoa, Bảo Ngọc, Quốc Huy), hệ tiêu chuẩn heuristic của Nielsen, tiêu chuẩn tiếp cận WCAG 2.1 hoặc các ràng buộc kỹ thuật thực tế.

---

## 1. Bảng quyết định thiết kế chính

| # | Quyết định thiết kế | Lý do & Căn cứ phục vụ Persona / Heuristic / WCAG | Thể hiện trên Figma (Page 03 & 06) |
|---|---|---|---|
| 1 | **Hỗ trợ chia giai đoạn (multi-phase) và đính kèm tệp cho deadline lớn** | **Minh (Lead NCKH):** Nghiên cứu kéo dài 31 ngày, 4 thành viên, không thể quản lý bằng 1 việc đơn lẻ. Cần theo dõi tiến độ từng chặng (Đề cương → Số liệu → Bản thảo → Hoàn thiện) và lưu trữ tệp DOCX, PDF, XLSX, ZIP tại chỗ thay vì nhảy qua lại Drive/Zalo. *Nielsen #7 (Linh hoạt & Hiệu quả).* | Phân hệ 06: Device 7d, 7s, 7s1, 7s2, 7t |
| 2 | **Thêm giờ bận nhanh (≤3 chạm) và tự động dời việc trùng ca** | **Đăng Khoa:** Làm thêm ca tối (18:00–22:00) thường xuyên đổi lịch gấp trong 1–2 giờ trước ca. Đăng Khoa không thể ngồi kéo từng việc. Hệ thống cho phép thêm giờ bận trong 3 chạm và tự động dời các buổi học bị xung đột sang ngày nhẹ nhất kế tiếp. *Nielsen #5 (Phòng ngừa lỗi) & #8 (Tối giản).* | Phân hệ 04: Device 4.2 |
| 3 | **Quy trình Onboarding 3 câu hỏi trắc nghiệm & chia nhỏ việc 45 phút** | **Bảo Ngọc:** Sinh viên năm nhất lần đầu dùng app quản lý, dễ ngợp với danh sách trống hoặc form phức tạp. Onboarding 3 câu hỏi giúp thiết lập sẵn khối ngành, giờ sinh hoạt và tự động gợi ý chia nhỏ bài tập lớn thành các slot 45 phút vừa sức. *Nielsen #6 (Nhận biết thay vì nhớ) & #10 (Trợ giúp).* | Phân hệ 02 (Device 2a, 2b, 2c) & Phân hệ 03 (Device 2c0, 2c3) |
| 4 | **Bố cục co giãn tương thích Font Scale 130% & Chế độ họp im lặng (DND)** | **Quốc Huy:** Lập trình viên đi làm toàn thời gian, mắt cận dùng font scale 130% trên Android; cần app im lặng tuyệt đối trong giờ họp 14:00–15:30. Toàn bộ ô lịch nhiệt, chip và card dùng Auto Layout Wrap hoặc min-height linh hoạt, không gán cứng chiều cao tránh tràn viền (overflow). *WCAG 1.4.4 (Resize text up to 200%) & Nielsen #1 (Hiển thị trạng thái).* | Phân hệ 07: Device 7.2, 7.4 (Demo scale 130%) |
| 5 | **Lịch nhiệt 5 mức độ tải (heat-0 đến heat-5) với tín hiệu kép** | **Nỗi đau chung:** Người dùng không nhận biết được ngày nào đang quá tải để nhận thêm việc. Thang màu lạnh đến nóng trực quan hóa độ nặng. Tuy nhiên, ô lịch nhiệt luôn có số việc và khuôn mặt mascot đi kèm để người khiếm thị màu vẫn nhận diện được. *WCAG 1.4.1 (Không dùng màu làm tín hiệu duy nhất).* | Phân hệ 04: Device 4, 4a, 4b |
| 6 | **Form thêm deadline cấp tốc: Chỉ 3 trường bắt buộc, hỗ trợ AI phân rã** | Sinh viên ghi chép việc từ các nhóm Zalo/Teams khi đang đi trên đường. Form chỉ bắt buộc: Tên, Nhóm việc, Hạn chót. Khung giờ làm và giai đoạn được AI gợi ý tự động hoặc điền sẵn khi mở từ khung giờ trống. *Nielsen #7 (Linh hoạt) & Nielsen #8 (Tối giản).* | Phân hệ 06: Device 6.3 |
| 7 | **Chặn dời việc sang sau hạn chót (Hard Stop) kèm phản hồi giải thích** | Ngăn chặn việc sinh viên vô tình dời buổi học hoặc giai đoạn chuẩn bị sang sau thời điểm nộp bài. Nút Lưu bị khóa, ô ngày vi phạm chuyển cảnh báo warning-container giải thích rõ nguyên nhân. *Nielsen #5 (Phòng ngừa lỗi).* | Phân hệ 04: Bottom Sheet dời việc (Device 4c, 3d) |
| 8 | **Tam giác cứu vãn việc quá hạn (Nộp muộn / Dời hạn / Bỏ việc)** | Việc trễ hạn là thực tế khó tránh. Thay vì chỉ hiển thị màu đỏ cảnh cáo gây stress, app cung cấp 3 hành động khắc phục cụ thể: ghi nhận nộp muộn (giữ streak), dời sang hạn mới khả thi, hoặc xác nhận bỏ việc có lưu vết và hoàn tác. *Nielsen #3 (Người dùng tự do & kiểm soát) & #9 (Chẩn đoán & sửa lỗi).* | Phân hệ 06: Device 5o1, 7o2, 5o2, 5o3 |
| 9 | **Cơ chế lưu đệm ngoại tuyến (Offline-First Sync)** | **Đăng Khoa:** Thường xuyên sử dụng mạng 4G chập chờn khi di chuyển giữa trường và quán cà phê. Mọi thao tác đánh dấu hoàn thành, thêm giờ bận đều được ghi nhận ngay vào bộ nhớ local và tự động đồng bộ khi có kết nối lại. *Nielsen #1 (Phản hồi trạng thái hệ thống).* | Toàn hệ thống & Device 7.4 |
| 10 | **Hệ thống Mascot SVG đa cảm xúc với vị trí hiển thị chuẩn hóa** | Tụi Nốt (Mascot) không đặt tùy tiện gây rối mắt danh sách việc. Mỗi biểu cảm được định vị chính xác: Nốt Tập Trung (Hôm nay), Nốt Cháy (Quá tải/Gấp), Nốt Xong (Hoàn thành/Đã nộp), Nốt Lạc (Mất mạng/Lỗi). Giúp tạo sự đồng cảm thân thiện mà giữ giao diện chuyên nghiệp. *Nielsen #4 (Nhất quán & Tiêu chuẩn).* | Toàn bộ các phân hệ |

---

## 2. Checklist kiểm tra Trợ năng (Accessibility) và Đáp ứng (Responsive)

| Tiêu chuẩn / Mục kiểm tra | Trạng thái | Yêu cầu kỹ thuật | Bằng chứng thiết kế & Kiểm chứng trên Figma |
|---|---|---|---|
| **Độ tương phản chữ thường (Normal text contrast)** | **Đạt** | Tỉ lệ tương phản $\ge 4.5:1$ theo WCAG 2.1 AA | Mọi cặp màu chữ trên nền đều đạt từ $4.71:1$ đến $16.72:1$ (chi tiết xem tại [`design/DESIGN.md`](file:///e:/prm393-lab2-group9/design/DESIGN.md) mục 3.3). Cặp thấp nhất: warning trên warning-container ($4.71:1$). |
| **Độ tương phản thành phần UI & Icon** | **Đạt** | Tỉ lệ tương phản $\ge 3.0:1$ cho viền điều khiển, checkbox, tab | Outline viền trường nhập liệu trên nền trắng đạt $3.93:1$; Primary trên Surface đạt $5.97:1$. |
| **Vùng chạm tối thiểu (Touch target size)** | **Đạt** | Kích thước $\ge 48 \times 48\text{ dp}$ | Ô lịch nhiệt có vùng chạm $48 \times 48\text{ dp}$ (khối hiển thị $42\text{ dp}$); dòng công việc cao $\ge 60\text{ dp}$; FAB $56\text{ dp}$; nút thao tác chính $48\text{–}56\text{ dp}$. |
| **Kích thước chữ nội dung** | **Đạt** | Cỡ chữ nội dung $\ge 14\text{ sp}$ | Text style dùng `bodyMedium` ($14\text{ sp}$) cho thông tin phụ, `bodyLarge` ($16\text{ sp}$) cho nội dung chính. Cỡ $12\text{ sp}$ (`labelMedium`) chỉ dùng cho thẻ nhãn ngắn. |
| **Không dùng màu làm tín hiệu duy nhất** | **Đạt** | Luôn kèm chữ, icon hoặc mascot biểu thị trạng thái | Trạng thái quá hạn có icon cảnh báo và chữ "Trễ X ngày". Ô lịch nhiệt có số đếm công việc và mặt mascot tương ứng với mức tải. |
| **Hỗ trợ phóng to chữ Text Scale 130%** | **Đạt** | Giao diện không tràn màn hình, không mất chữ khi phóng to $1.3\times$ | Được kiểm chứng chuyên biệt trên màn Device 7.4 (Demo scale 130%). Dòng công việc và các container thẻ đều cấu hình Auto Layout dạng ôm nội dung dọc (`hug contents`). |
| **Thiết kế Auto Layout và Constraints** | **Đạt** | 100% component và frame trên Figma dùng Auto Layout | Các danh sách, form nhập, thanh điều hướng và dialog đều dùng Auto Layout đa tầng với ràng buộc Fill / Hug chuẩn xác. |
| **Kiểm tra hiển thị chuẩn 360 dp (Android nhỏ)** | **Đạt** | Không vỡ khung ở màn hình bề ngang nhỏ ($360 \times 800\text{ dp}$) | 25+ device frame trên Figma Page 03 đều được thiết kế ở khung chuẩn $360\text{ dp}$, lưới 7 cột lịch nhiệt vừa khít lề $12\text{ dp}$ ($7 \times 48 = 336\text{ dp}$). |
| **Kiểm tra hiển thị mở rộng 412 dp (Android chuẩn)** | **Đạt** | Giãn đều, không lệch trục trên màn hình lớn ($412 \times 915\text{ dp}$) | Bố cục linh hoạt giãn khoảng cách cột và vùng nội dung card mà không làm méo icon hay hình minh họa. |
