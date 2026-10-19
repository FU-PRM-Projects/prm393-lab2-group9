# DESIGN.md — Nốt (Study Planner)

Bản mô tả hệ thống thiết kế (Design System Specification) dùng làm tiêu chuẩn cho Figma (page `04 Design System`, `05 Components`) và triển khai code Flutter (Material 3). Mọi giá trị dưới đây đồng bộ tuyệt đối với Figma Variables và Text Styles trong file `PRM393-LAB2-Study-Planner`.

---

## 1. Tóm tắt sản phẩm

| Mục | Chi tiết đặc tả |
|---|---|
| **Tên ứng dụng** | **Nốt (Study Planner)**. Mascot đại diện: "Tụi Nốt" (những tờ giấy ghi chú có linh hồn và biểu cảm) |
| **Đối tượng người dùng** | Phục vụ 4 nhóm sinh viên & người đi làm trẻ:<br>• **Minh (Chính):** Trưởng nhóm Nghiên cứu Khoa học (NCKH), quản lý đồ án dài hơi nhiều giai đoạn.<br>• **Đăng Khoa (Phụ):** Sinh viên IT làm thêm ca tối quán cà phê (18:00–22:00), cần đổi ca và dời lịch nhanh.<br>• **Bảo Ngọc (Phụ):** Sinh viên năm nhất Thiết kế Đồ họa, cần chia nhỏ bài tập lớn thành các slot 45 phút.<br>• **Quốc Huy (Hỗ trợ):** Lập trình viên đi làm toàn thời gian, dùng font scale 130%, cần im lặng trong giờ họp (DND). |
| **Vấn đề cốt lõi giải quyết** | Xung đột lịch học – lịch làm, quá tải bài tập và phân mảnh công cụ quản lý (phải nhảy qua lại giữa Zalo, Notion, Google Calendar, ClickUp). |
| **Năng lực vượt trội** | • Tự động xếp lịch và chia nhỏ việc thành các slot 45 phút.<br>• Phân rã deadline lớn thành nhiều giai đoạn (phases) và lưu trữ tệp đính kèm trực tiếp (DOCX, PDF, XLSX, ZIP).<br>• Dời việc tự động chỉ trong 3 chạm khi phát sinh ca làm đột xuất.<br>• Trực quan hóa tải công việc bằng lịch nhiệt 5 mức độ (heat map). |
| **Nền tảng & Thiết bị** | Android Phone, chuẩn $360 \times 800\text{ dp}$, tương thích mở rộng $412 \times 915\text{ dp}$, hỗ trợ Text Scaling $1.3\times$, Material Design 3, Light Theme. |
| **Ngôn ngữ & Định dạng** | Tiếng Việt, hiển thị thời gian chuẩn 24 giờ. |

---

## 2. Nguyên tắc thiết kế

1. **Liếc là hiểu (Glanceable UI):** Mỗi màn hình giải quyết dứt điểm một câu hỏi cốt lõi. Hôm nay: "Bây giờ làm gì?"; Kế hoạch: "Ngày nào quá tải?"; Deadline: "Việc nào gấp nhất?"; Chi tiết: "Giai đoạn này ai làm, file ở đâu?".
2. **Thao tác một tay, tối ưu ngón cái (Thumb-zone Driven):** Các nút bấm chính (Primary Action, FAB, Bottom Sheet trigger) tập trung ở nửa dưới màn hình.
3. **Phân rã việc lớn để bớt ngợp (Chunking by Default):** Mọi đồ án hoặc bài tập dài kỳ đều được gợi ý chia thành các phase hoặc slot 45 phút.
4. **Nhập liệu cấp tốc (Frictionless Input):** Chỉ bắt buộc 3 trường tối thiểu (Tên, Nhóm, Hạn nộp). Các thông tin khác có thể suy diễn tự động hoặc điền sau.
5. **Độ tương phản cao & Tín hiệu kép:** Màu nhiệt (lạnh đến nóng) trực quan nhưng không phải tín hiệu duy nhất; luôn đi kèm con số, nhãn chữ và biểu cảm mascot để đảm bảo chuẩn tiếp cận WCAG 2.1 AA.
6. **Co giãn an toàn (Responsive & Text Scalable):** Toàn bộ component phải co giãn linh hoạt khi hệ thống bật cỡ chữ lớn (Text Scale 130%) mà không bị vỡ bố cục hay che khuất nội dung.

---

## 3. Màu sắc (Color Tokens)

Hệ thống token màu chuẩn Material 3 ánh xạ trực tiếp sang `ColorScheme` trong Flutter:

### 3.1 Bảng màu chức năng (Functional Colors)

| Token | Mã Hex | Ý nghĩa và Vị trí sử dụng |
|---|---|---|
| `primary` | `#3D4FD6` | Màu thương hiệu chính: FAB, nút filled, tab đang chọn, banner tóm tắt |
| `on-primary` | `#FFFFFF` | Chữ và icon nổi trên nền primary |
| `primary-container` | `#DDE1FF` | Nền chip đang chọn, khối buổi làm trong lưới giờ, stepper đang chạy |
| `on-primary-container` | `#2F3FB8` | Chữ và icon đậm trên nền primary-container |
| `surface` | `#F6F7FB` | Nền màn hình tổng thể (Scaffold background) |
| `surface-card` | `#FFFFFF` | Nền thẻ (Card), thanh điều hướng dưới, ô nhập liệu, hộp thoại dialog |
| `surface-variant` | `#E7E9F3` | Nền thanh phân đoạn (segmented), khối lịch bận, ô ngày trống trên lịch |
| `on-surface` | `#1B1D2A` | Chữ tiêu đề và nội dung chính |
| `on-surface-variant` | `#555B6E` | Chữ mô tả phụ, icon trạng thái chưa chọn, nhãn thời gian |
| `outline` | `#7A8094` | Viền checkbox, đường phân cách, viền trường nhập liệu |
| `error` | `#B3261E` | Trạng thái quá hạn, cảnh báo lỗi, nút xóa dữ liệu |
| `on-error` | `#FFFFFF` | Chữ trên nền nút error |
| `error-container` | `#FDE1DF` | Nền thẻ cảnh báo lỗi, banner thông báo quá hạn nghiêm trọng |
| `warning` | `#A84F00` | Cảnh báo hạn gấp trong ngày, cảnh báo dời việc sau hạn chót |
| `warning-container` | `#FFE9D1` | Nền thông báo vi phạm hạn nộp |
| `success` | `#1B6B44` | Đánh dấu hoàn thành giai đoạn, nộp bài thành công, trạng thái đúng hạn |
| `success-container` | `#D8F3E6` | Nền huy hiệu thành tích, thẻ việc đã hoàn thành |

### 3.2 Bảng màu lịch nhiệt (Heat Map Scale)

Thang đo 5 cấp độ tải công việc dựa trên tỷ lệ thời gian bị chiếm dụng trong 14 giờ thức của sinh viên:

| Token | Mã Hex | Mức độ | Nhãn hiển thị | Mascot tương ứng | Ngưỡng tính toán thời gian |
|---|---|---|---|---|---|
| `heat-0` | `#E7E9F3` | Mức 0 | Trống | Không có | 0 giờ bận trong ngày |
| `heat-1` | `#A9DCF5` | Mức 1 | Nhẹ | Nốt Thong Thả | Chiếm dưới 25% thời gian thức (< 3.5 giờ) |
| `heat-2` | `#7FD9B3` | Mức 2 | Vừa | Nốt Thong Thả | Chiếm 25% – 50% thời gian thức (3.5 – 7.0 giờ) |
| `heat-3` | `#FFD24A` | Mức 3 | Khá nặng | Nốt Đợi | Chiếm 50% – 70% thời gian thức (7.0 – 9.8 giờ) |
| `heat-4` | `#FF9A3D` | Mức 4 | Nặng | Nốt Vội | Chiếm 70% – 90% thời gian thức (9.8 – 12.6 giờ) |
| `heat-5` | `#F0524B` | Mức 5 | Quá tải | Nốt Cháy | Chiếm > 90% thời gian thức hoặc có > 2 deadline gấp |

### 3.3 Tỉ lệ tương phản kiểm định (WCAG 2.1 AA)

| Cặp màu kiểm tra | Tỉ lệ tương phản | Tiêu chuẩn WCAG | Đánh giá |
|---|---|---|---|
| `on-surface` trên `surface` | **15.62:1** | $\ge 4.5:1$ (Chữ thường) | Đạt xuất sắc |
| `on-surface` trên `surface-card` | **16.72:1** | $\ge 4.5:1$ (Chữ thường) | Đạt xuất sắc |
| `on-surface-variant` trên `surface-card` | **6.76:1** | $\ge 4.5:1$ (Chữ thường) | Đạt |
| `on-primary` trên `primary` | **6.39:1** | $\ge 4.5:1$ (Chữ nút bấm) | Đạt |
| `outline` trên `surface-card` | **3.93:1** | $\ge 3.0:1$ (Viền UI control) | Đạt |
| `error` trên `surface-card` | **6.54:1** | $\ge 4.5:1$ (Chữ lỗi) | Đạt |
| `warning` trên `warning-container` | **4.71:1** | $\ge 4.5:1$ (Chữ cảnh báo) | Đạt |
| `on-surface` trên `heat-1` đến `heat-5` | **4.79:1 – 11.60:1** | $\ge 4.5:1$ (Số việc trên ô) | Đạt |

---

## 4. Typography

Họ phông chữ: **Be Vietnam Pro** (Google Fonts).

| Token | Kích thước (sp) | Chiều cao dòng (Line Height) | Độ đậm (Weight) | Vị trí sử dụng |
|---|---|---|---|---|
| `headlineMedium` | 28 sp | 1.25 (35 sp) | Bold (700) | Tiêu đề màn hình cấp cao nhất, màn Thành tích |
| `titleLarge` | 22 sp | 1.25 (28 sp) | Bold (700) | Tiêu đề App bar màn con, tiêu đề hộp thoại Dialog |
| `titleMedium` | 18 sp | 1.25 (24 sp) | Semi-bold (600) | Tiêu đề Banner tóm tắt, tên Section nhóm |
| `titleSmall` | 16 sp | 1.40 (22 sp) | Semi-bold (600) | Tên deadline, tên giai đoạn, tên ca làm việc |
| `bodyLarge` | 16 sp | 1.40 (22 sp) | Regular (400) | Nội dung văn bản chính, chữ trong ô nhập liệu |
| `bodyMedium` | 14 sp | 1.40 (20 sp) | Regular (400) | Dòng thông tin phụ: mã môn, hạn nộp, người phụ trách |
| `labelLarge` | 14 sp | 1.40 (20 sp) | Semi-bold (600) | Chữ trên nút bấm filled/tonal, chip giai đoạn |
| `labelMedium` | 12 sp | 1.40 (17 sp) | Semi-bold (600) | Nhãn thanh điều hướng, số việc trên ô lịch nhiệt |

*Quy tắc tiếp cận Text Scale:* Toàn bộ giao diện khi hiển thị ở hệ số `TextScaler.linear(1.3)` (130%) phải tự động tăng chiều cao container (dùng Auto Layout dạng Hug / Wrap). Tuyệt đối không cố định chiều cao thẻ danh sách để tránh mất chữ.

---

## 5. Khoảng cách (Spacing) & Hình học (Radii, Elevation)

### 5.1 Khoảng cách (Spacing System - Hệ 4 dp)
- `space-1` (4 dp): Khoảng cách giữa icon và chữ trong chip nhãn.
- `space-2` (8 dp): Khoảng cách giữa các phần tử liền kề (avatar, tag).
- `space-3` (12 dp): Khoảng cách giữa các thẻ danh sách, lề lưới lịch nhiệt.
- `space-4` (16 dp): Lề trong (padding) tiêu chuẩn của thẻ Card.
- `space-5` (20 dp): Lề biên ngang màn hình (Screen horizontal padding).
- `space-6` (24 dp): Khoảng cách giữa các nhóm section lớn.
- `space-8` (32 dp): Khoảng cách phân cách trạng thái rỗng (empty state) hoặc lỗi.

### 5.2 Bo góc (Corner Radii)
- `radius-sm` (8 dp): Thẻ chip đính kèm tệp, ô lịch nhiệt, badge trạng thái.
- `radius-md` (12 dp): Ô nhập text field, nút bấm phụ, thanh segmented control.
- `radius-lg` (16 dp): Nút bấm chính, nút nổi FAB.
- `radius-xl` (20 dp): Thẻ công việc (Card), Banner tóm tắt.
- `radius-2xl` (28 dp): Hộp thoại Dialog, góc trên của Bottom Sheet dời việc.

### 5.3 Độ nổi (Elevation)
- `level-0` (0 dp): Các thẻ Card phân tách bằng màu nền, không đổ bóng đậm.
- `level-2` (3 dp): Thanh điều hướng dưới, nút FAB, thông báo snackbar.
- `level-3` (6 dp): Hộp thoại Dialog xác nhận, Bottom Sheet dời việc.

---

## 6. Quy chuẩn thành phần (Component Specifications)

### 6.1 Stepper giai đoạn (Phase Stepper)
- Dùng trong Chi tiết deadline (Phân hệ 06 - Device 7d, 7s).
- Gồm 4 trạng thái giai đoạn: Đã hoàn thành (icon tick xanh success), Đang thực hiện (vòng tròn viền primary kèm tiến độ %), Chưa bắt đầu (vòng tròn xám outline), Trễ hạn (icon than đỏ error).
- Mỗi giai đoạn hiển thị: Tên phase, Hạn chót, Avatar thành viên phụ trách (Lan, Minh...) và danh sách tệp đính kèm tương ứng.

### 6.2 Thẻ tệp đính kèm (Attachment Chip)
- Hỗ trợ các định dạng: DOCX (màu xanh dương), PDF (màu đỏ mận), XLSX (màu xanh lá), ZIP (màu vàng cam).
- Kích thước: cao 36 dp, gồm icon định dạng tệp 18 dp, tên tệp (cắt ngắn ở 20 ký tự), dung lượng (ví dụ: `2.4 MB`) và icon tải xuống/xem trước.

### 6.3 Dòng công việc (Task Row)
- Chiều cao tối thiểu 60 dp (tự mở rộng khi text scale 130%).
- Cấu trúc: Checkbox hoàn thành (bên trái, vùng chạm 48 dp) → Cột thông tin (Tên deadline, Mã môn, Tiến độ phase) → Cột thời hạn bên phải (Màu error nếu trễ, warning nếu hôm nay, on-surface-variant nếu xa).

### 6.4 Ô lịch nhiệt (Heat Map Cell)
- Kích thước hiển thị $42 \times 42\text{ dp}$ đặt trong vùng chạm thực tế $48 \times 48\text{ dp}$.
- Hiển thị ngày trong tháng (phía trên), số lượng đầu việc (ở giữa, phông đậm), khuôn mặt mascot thu nhỏ (phía dưới). Ngày đang chọn có viền kép 2 dp `primary`.

### 6.5 Thẻ thông báo màn khóa (Lock Screen Card)
- Dùng trong Device 13c (Phân hệ 05).
- Kích thước chuẩn hóa, nền bo góc 16 dp mờ nhẹ, biểu tượng Nốt, tên deadline, hạn chót và 2 nút hành động nhanh: "Đã hoàn thành" và "Nhắc lại sau 15 phút".

---

## 7. Mascot & Biểu cảm (Tụi Nốt)

Tụi Nốt được thiết kế dạng vector SVG độc quyền, xuất hiện tại các vị trí cố định để tăng tính sinh động mà không làm loãng thông tin:

| Tên Mascot | Biểu cảm & Đặc điểm | Vị trí hiển thị quy định |
|---|---|---|
| **Nốt Tập Trung** | Đeo băng đô quyết tâm | Banner tóm tắt trang Hôm nay và Deadline |
| **Nốt Cháy** | Bốc hỏa đỏ rực, toát mồ hôi | Tiêu đề nhóm Quá hạn, ô lịch nhiệt mức 5 (Quá tải) |
| **Nốt Vội** | Chạy gấp, đồng hồ reo | Tiêu đề nhóm Đến hạn hôm nay, ô lịch nhiệt mức 4 |
| **Nốt Đợi** | Chờ đợi, gõ nhịp ngón tay | Tiêu đề nhóm Tuần này, ô lịch nhiệt mức 3 |
| **Nốt Thong Thả** | Cười nhẹ, thư thái | Tiêu đề nhóm Tuần sau, ô lịch nhiệt mức 1 và 2 |
| **Nốt Xong** | Nhảy múa vui mừng, rực rỡ | Màn hình Báo công / Đã nộp thành công, Bảng thành tích |
| **Nốt Ngủ** | Nhắm mắt ngủ say bên gối | Trạng thái không có việc (Empty state hôm nay) |
| **Nốt Lạc** | Cầm bản đồ gãi đầu ngơ ngác | Màn hình mất mạng (Offline / Error state) |
