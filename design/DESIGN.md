# DESIGN.md — Nốt (Study Planner)

Bản mô tả thiết kế dùng cho Google Stitch và làm gốc cho design system trong Figma (page 04, 05). Mọi giá trị dưới đây trùng với Figma Variables và text styles trong file `PRM393-LAB2-Study-Planner`.

> Lịch sử: bản đưa cho Stitch ở lần tạo đầu tiên được ghi nguyên văn trong `ai/ai-design-log.md`, mục 0. File này là bản hiện hành sau các vòng lặp.

---

## 1. Tóm tắt sản phẩm

| Mục | Chi tiết |
|---|---|
| Tên app | **Nốt**. Mascot là "Tụi Nốt", các tờ giấy ghi chú có khuôn mặt |
| Người dùng | Khả Hân, sinh viên năm 4, 5 môn cùng đồ án và nghiên cứu, 7–8 deadline mỗi tuần trong 10 nhóm Zalo |
| Vấn đề | Kế hoạch tuần bị vỡ khi việc bất ngờ chen vào, vì không thấy ngày nào còn trống và không biết lùi việc nào |
| Việc app phải làm tốt nhất | Xếp một việc phát sinh vào khung giờ trống trong dưới 30 giây |
| Nền tảng | Android, điện thoại, khung 360 × 800 dp, kiểm tra thêm ở 412 dp, Material 3, light theme |
| Ngôn ngữ giao diện | Tiếng Việt, giờ dạng 24 giờ |

## 2. Nguyên tắc thiết kế

1. **Liếc là hiểu.** Mỗi lần mở app dưới một phút, nên mỗi màn hình trả lời một câu hỏi. Hôm nay: "làm gì tiếp?". Kế hoạch: "ngày nào nặng?". Deadline: "cái gì gấp?". Lịch bận: "còn trống lúc nào?".
2. **Một tay, nửa dưới màn hình.** Hành động chính nằm trong vùng ngón cái: FAB hoặc nút cố định ở cuối màn hình, thanh điều hướng dưới.
3. **Sửa dễ hơn lập.** Dời việc là hành động hạng nhất, luôn hoàn tác được.
4. **Ít trường nhất có thể.** Form chỉ bắt buộc những gì app không tự suy ra được.
5. **Màu nóng chỉ để báo nặng hoặc gấp.** Màu nóng-lạnh của lịch nhiệt có độ tương phản cao để thấy ngay ngày nặng. Mọi tín hiệu màu luôn có chữ hoặc hình đi kèm.
6. **Vui nhưng gọn.** Mascot chỉ xuất hiện ở các vị trí cố định (mục 9), không chen vào từng dòng việc.

## 3. Màu

Light theme. Tên token theo vai trò của Material 3 để ánh xạ thẳng sang `ColorScheme` ở Lab 3.

### 3.1 Màu vai trò

| Token | Hex | Dùng cho |
|---|---|---|
| primary | #3D4FD6 | FAB, nút chính, tab đang chọn, banner tóm tắt |
| on-primary | #FFFFFF | Chữ và icon trên primary |
| primary-container | #DDE1FF | Nền tab đang chọn, chip đang chọn, buổi làm trong lưới giờ |
| on-primary-container | #2F3FB8 | Chữ trên primary-container |
| surface | #F6F7FB | Nền màn hình |
| surface-card | #FFFFFF | Thẻ, thanh điều hướng, text field, dialog |
| surface-variant | #E7E9F3 | Nền segmented control, skeleton, ô lịch nhiệt trống, khối lịch bận |
| on-surface | #1B1D2A | Chữ chính |
| on-surface-variant | #555B6E | Chữ phụ, icon chưa chọn |
| outline | #7A8094 | Viền checkbox, viền text field. Không dùng cho chữ |
| error | #B3261E | Lỗi nhập, nhãn Quá hạn, nút Xóa |
| on-error | #FFFFFF | Chữ trên error |
| error-container | #FDE1DF | Nền thông báo lỗi |
| warning | #A84F00 | Nhãn đến hạn hôm nay |
| warning-container | #FFE9D1 | Nền cảnh báo "ngày mới sau hạn nộp" |
| success | #1B6B44 | Nhãn Đã nộp, icon hoàn thành |
| success-container | #D8F3E6 | Nền nhóm Đã nộp |

### 3.2 Màu lịch nhiệt

Thang 5 mức từ lạnh đến nóng. Chữ trên ô lịch nhiệt luôn dùng on-surface.

| Token | Hex | Mức | Nhãn chữ | Mascot |
|---|---|---|---|---|
| heat-0 | #E7E9F3 | Trống | Trống | Không có |
| heat-1 | #A9DCF5 | Nhẹ | Nhẹ | Nốt Thong Thả |
| heat-2 | #7FD9B3 | Vừa | Vừa | Nốt Thong Thả |
| heat-3 | #FFD24A | Khá nặng | Khá nặng | Nốt Đợi |
| heat-4 | #FF9A3D | Nặng | Nặng | Nốt Vội |
| heat-5 | #F0524B | Quá tải | Quá tải | Nốt Cháy |

**Cách tính mức:** tỉ lệ thời gian đã kín trong ngày (lịch bận và buổi làm) trên 14 giờ thức. Dưới 25% là mức 1, 25–50% mức 2, 50–70% mức 3, 70–90% mức 4, trên 90% mức 5. Ngày có deadline đến hạn được cộng thêm một mức, tối đa mức 5.

### 3.3 Contrast đã tính (WCAG 2.1)

Yêu cầu: chữ thường ≥ 4.5:1, chữ lớn và điều khiển UI ≥ 3:1.

| Cặp màu | Tỉ lệ | Kết quả |
|---|---|---|
| on-surface trên surface | 15.62:1 | Đạt |
| on-surface trên surface-card | 16.72:1 | Đạt |
| on-surface-variant trên surface | 6.31:1 | Đạt |
| on-surface-variant trên surface-card | 6.76:1 | Đạt |
| on-surface-variant trên surface-variant | 5.58:1 | Đạt |
| on-primary trên primary | 6.39:1 | Đạt |
| primary trên surface | 5.97:1 | Đạt |
| on-primary-container trên primary-container | 6.45:1 | Đạt |
| error trên surface-card | 6.54:1 | Đạt |
| error trên error-container | 5.30:1 | Đạt |
| warning trên surface-card | 5.55:1 | Đạt |
| warning trên warning-container | 4.71:1 | Đạt |
| success trên surface-card | 6.50:1 | Đạt |
| success trên success-container | 5.53:1 | Đạt |
| outline trên surface-card | 3.93:1 | Đạt mức 3:1 cho viền điều khiển |
| on-surface trên heat-1 / 2 / 3 / 4 / 5 | 11.34 / 9.94 / 11.60 / 7.92 / 4.79 | Đạt |

Ô lịch nhiệt mức 1 trên nền trắng chỉ đạt 1.47:1. Vì vậy mức nặng không được truyền đạt bằng màu ô: mỗi ô luôn có số việc và khuôn mặt mascot, và màn Chi tiết ngày ghi nhãn chữ của mức.

## 4. Typography

Font: **Be Vietnam Pro** (Google Fonts, đủ dấu tiếng Việt, dùng được trong Figma và gói `google_fonts` của Flutter). Tên style theo `TextTheme` của Material 3. Line height: 1.25 cho headline và title, 1.4 cho body và label.

| Token | Cỡ (sp) | Weight | Dùng cho |
|---|---|---|---|
| headlineMedium | 28 | 700 | Tiêu đề màn top-level, tiêu đề màn Đã nộp |
| titleLarge | 22 | 700 | Tiêu đề App bar màn lồng, tiêu đề dialog |
| titleMedium | 18 | 600 | Tiêu đề banner tóm tắt, tiêu đề section |
| titleSmall | 16 | 600 | Tên việc trên một dòng, tên lịch bận |
| bodyLarge | 16 | 400 | Nội dung chính, chữ trong text field |
| bodyMedium | 14 | 400 | Dòng phụ: mã môn, số buổi, giờ |
| labelLarge | 14 | 600 | Chữ trên nút, chip, thời hạn |
| labelMedium | 12 | 600 | Nhãn thanh điều hướng, tiêu đề nhóm viết hoa, số trên ô lịch nhiệt |

- Chữ nội dung tối thiểu 14 sp. Cỡ 12 sp chỉ dùng cho nhãn ngắn, không dùng cho câu cần đọc.
- Giờ và ngày dùng số có độ rộng đều (tabular figures) để thẳng cột.
- Tên việc tối đa 2 dòng, quá thì cắt bằng dấu ba chấm.

## 5. Khoảng cách, bo góc, elevation

Lưới 4 dp.

| Nhóm | Token | Giá trị | Dùng cho |
|---|---|---|---|
| Spacing | space-1 | 4 dp | Giữa icon và chữ trong nhãn |
| Spacing | space-2 | 8 dp | Giữa các phần tử trong một dòng |
| Spacing | space-3 | 12 dp | Giữa các thẻ, padding dọc của dòng việc |
| Spacing | space-4 | 16 dp | Padding trong thẻ |
| Spacing | space-5 | 20 dp | Lề ngang màn hình |
| Spacing | space-6 | 24 dp | Giữa các nhóm nội dung |
| Spacing | space-8 | 32 dp | Khoảng trên dưới của empty state và error state |
| Bo góc | radius-sm | 8 dp | Chip, nhãn trạng thái, ô lịch nhiệt |
| Bo góc | radius-md | 12 dp | Text field, nút nhỏ, segmented control |
| Bo góc | radius-lg | 16 dp | Nút lớn, FAB |
| Bo góc | radius-xl | 20 dp | Thẻ, banner tóm tắt |
| Bo góc | radius-2xl | 28 dp | Dialog, bottom sheet (góc trên) |
| Elevation | level-0 | 0 dp | Thẻ (tách nền bằng màu, không bóng) |
| Elevation | level-2 | 3 dp | FAB, thanh điều hướng, snackbar |
| Elevation | level-3 | 6 dp | Dialog, bottom sheet |

- Vùng chạm tối thiểu 48 × 48 dp, kể cả khi icon chỉ 24 dp.
- Dòng việc cao tối thiểu 60 dp.
- Nút chính cao 48 dp. Nút cố định cuối màn lồng cao 56 dp, rộng hết chiều ngang trừ lề.
- Danh sách có FAB thì thêm 88 dp padding dưới để FAB không che dòng cuối.

## 6. Tone và ngôn ngữ

- **Giọng:** bạn cùng lớp có tổ chức. Ngắn, rõ, không trách, không dấu chấm than.
- **Xưng hô:** gọi người dùng là "bạn". App không tự xưng. Mascot có tên ("Nốt") nhưng không nói thay app trong thông báo lỗi.
- **Nút:** bắt đầu bằng động từ và nói rõ kết quả: "Lưu deadline", "Đánh dấu đã nộp", "Thử lại". Không dùng "OK", "Đồng ý".
- **Lỗi:** nói chuyện gì xảy ra, vì sao, làm gì tiếp.
- **Thời gian:** dưới 7 ngày dùng cách nói tương đối ("Hôm nay 23:59", "Còn 2 ngày", "Trễ 1 ngày"); xa hơn thì ghi ngày ("15 thg 10").

| Tình huống | Nên viết | Không viết |
|---|---|---|
| Chưa có deadline | Chưa có deadline nào. Thêm deadline đầu tiên, Nốt sẽ nhắc bạn trước hạn. | Bạn chưa làm gì |
| Mất mạng khi lưu | Chưa lưu được vì mất kết nối. Nội dung bạn nhập vẫn còn. Nút: Thử lại | Lỗi! Đã xảy ra sự cố. |
| Thiếu hạn nộp | Chọn hạn nộp cho deadline này | Dữ liệu không hợp lệ |
| Dời sau hạn nộp | Ngày này sau hạn nộp (thứ Sáu 23:59). Chọn ngày sớm hơn. | Không thể thực hiện |
| Sau khi nộp | Đã nộp · Hoàn tác | Thành công! |

## 7. Quy tắc component

Dùng component Material 3. Mọi component lấy giá trị từ token ở mục 3 đến 5, không gán cứng.

| Component | Quy tắc | Trạng thái bắt buộc |
|---|---|---|
| Button | Ba cấp: filled (hành động chính, mỗi màn một nút), tonal (hành động phụ), text (Hủy, Hoàn tác). Nút xóa dùng màu error | Default, pressed, disabled, loading (spinner thay chữ, giữ chiều rộng) |
| FAB | Icon "+", 56 × 56 dp, primary, góc phải dưới, trên thanh điều hướng. Chỉ ở Deadline và Lịch bận | Default, pressed |
| Text field | Kiểu outlined, nhãn luôn hiện phía trên, cao 56 dp. Lỗi nằm ngay dưới ô, kèm icon. Ngày và giờ dùng picker, không gõ tay | Default, focused, filled, error, disabled |
| Task row | Chỉ có: checkbox, tên việc, một dòng phụ ("PRM393 · 2/3 buổi"), thời hạn bên phải. Không thanh tiến độ, không chip màu | Default, pressed, đã xong |
| Card | Nền surface-card, radius-xl, không bóng. Banner tóm tắt dùng nền primary | Default, pressed (nếu bấm được) |
| Ô lịch nhiệt | Vuông 42 dp trong vùng chạm 48 × 48 dp, radius-sm, màu heat-0 đến heat-5, số việc ở giữa, khuôn mặt mascot nhỏ. Lưới 7 cột × 48 dp = 336 dp nên lưới dùng lề 12 dp thay vì 20 dp. Ngày đang chọn có viền 2 dp on-surface | 6 mức, đang chọn, hôm nay |
| Segmented control | Hai lựa chọn: "Theo hạn / Theo nhóm việc" ở Deadline, "Danh sách / Theo giờ" ở Chi tiết ngày | Mỗi lựa chọn ở trạng thái được chọn |
| Navigation | Thanh điều hướng dưới, 4 điểm đến: Hôm nay, Kế hoạch, Deadline, Lịch bận. Luôn có icon và nhãn chữ. Ẩn ở màn lồng | Mỗi điểm đến ở trạng thái được chọn |
| App bar | Màn top-level: tiêu đề lớn căn trái, không có Back. Màn lồng: Back, tiêu đề, tối đa một action | Default, có action |
| Dialog | Chỉ dùng khi sắp mất dữ liệu hoặc khó đảo ngược. Tiêu đề là câu hỏi, hai nút, nút an toàn bên trái | Xác nhận, destructive |
| Bottom sheet | Nhập nhanh không cần rời màn hình (Dời việc, Thêm lịch bận) | Default, lỗi nhập |
| Snackbar | Sau mọi hành động hoàn tác được. Hiện 5 giây, trên thanh điều hướng | Có action, không action |
| Loading state | Skeleton đúng hình dạng dòng việc hoặc lưới lịch nhiệt. Spinner chỉ dùng trong nút | Skeleton mức màn hình |
| Empty state | Mascot 140 dp, một tiêu đề, một câu giải thích, một nút | Chưa có deadline, ngày trống, chưa có lịch bận |
| Error state | Mascot Nốt Lạc, thông báo, nguyên nhân dễ hiểu, nút Thử lại. Không hiện mã lỗi | Mất mạng mức màn hình, lỗi khi lưu |

## 8. Icon

- Icon giao diện: Material Symbols Rounded, 24 dp.
- Thanh điều hướng: `today` (Hôm nay), `calendar_view_month` (Kế hoạch), `assignment_late` (Deadline), `event_busy` (Lịch bận).
- Icon nhóm việc (SVG trong `assets/mascot/`, 24 dp):

| Nhóm việc / loại lịch bận | Icon |
|---|---|
| Môn học | Sách (`loai-viec-sach.svg`) |
| Đồ án | Tên lửa (`loai-viec-ten-lua.svg`) |
| Nghiên cứu | Bình (`loai-viec-binh.svg`) |
| Khác (CV, việc riêng) | Tệp (`loai-viec-tep.svg`) |
| Lịch bận: Họp nhóm | Bóng nói (`loai-viec-bong-noi.svg`) |
| Lịch bận: Freelance | Chì (`loai-viec-chi.svg`) |

## 9. Mascot và họa tiết

Tụi Nốt là các tờ giấy ghi chú có khuôn mặt. File gốc ở `assets/mascot/`. Stitch không vẽ mascot; Stitch chỉ chừa ô trống, hình được đặt trong Figma.

| Mascot | Vị trí duy nhất được dùng |
|---|---|
| Nốt Tập Trung | Banner tóm tắt ở Hôm nay và Deadline |
| Nốt Cháy | Tiêu đề nhóm Quá hạn, ô lịch nhiệt mức 5 |
| Nốt Vội | Tiêu đề nhóm Hôm nay, ô lịch nhiệt mức 4 |
| Nốt Đợi | Tiêu đề nhóm Tuần này, ô lịch nhiệt mức 3 |
| Nốt Thong Thả | Tiêu đề nhóm Sau đó, ô lịch nhiệt mức 1 và 2 |
| Nốt Ngủ | Empty state |
| Nốt Lạc | Error state |
| Nốt Xong | Màn Đã nộp, tiêu đề nhóm Đã nộp |

- Không đặt mascot trong từng dòng việc.
- Họa tiết (giấy note, lưới nhiệt, sao và tick) chỉ dùng làm nền trang trí ở màn Đăng nhập, Đã nộp và empty state, độ mờ tối đa 40%, không nằm sau chữ nội dung.

## 10. Ràng buộc

- **Bố cục:** thiết kế ở 360 × 800 dp, kiểm tra ở 412 dp. Nội dung dài cuộn dọc; App bar, nút cố định cuối màn và thanh điều hướng đứng yên.
- **Bàn phím:** khi bàn phím mở, ô đang nhập và nút Lưu vẫn phải nhìn thấy.
- **Chuyển động:** chuyển cảnh mặc định của Material. Mascot ở màn Đã nộp được phép có một hiệu ứng vào 300 ms.

## 11. Không làm

- Không gradient, không glassmorphism, không bóng đổ đậm.
- Không truyền đạt trạng thái chỉ bằng màu.
- Không dark theme trong Lab 2 (đề không bắt buộc).
- Không dùng màu đỏ cho trang trí; đỏ chỉ dành cho lỗi, Quá hạn, Xóa và lịch nhiệt mức 5.
