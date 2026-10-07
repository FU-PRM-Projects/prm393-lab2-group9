# DESIGN.md — bản mô tả thiết kế đưa cho Stitch

> TODO: đối chiếu các giá trị dưới đây với bản bạn đã đưa cho Stitch, rồi sửa cho khớp.

## Nền tảng
- Ứng dụng di động. Khung thiết kế cuối cùng: 360 × 800 dp. Kiểm tra thêm ở 412 dp.
- Ngôn ngữ giao diện: tiếng Việt.

## Màu
| Token | Giá trị | Dùng cho |
|---|---|---|
| primary | #3D4FD6 | Hành động chính, tab đang chọn |
| on-primary | #FFFFFF | Chữ trên nền primary |
| primary-container | #DDE1FF | Nền tonal của tab đang chọn |
| surface | #F6F7FB | Nền màn hình |
| surface-card | #FFFFFF | Thẻ, bottom navigation |
| on-surface | #1B1D2A | Chữ chính |
| on-surface-variant | #555B6E | Chữ phụ |
| outline | #7A8094 | Viền checkbox |
| error | #B3261E | Quá hạn |
| warning | #A84F00 | Đến hạn hôm nay |
| heat-1 … heat-5 | #A9DCF5, #7FD9B3, #FFD24A, #FF9A3D, #F0524B | Lịch nhiệt, từ nhẹ đến nặng |

## Typography
- Font: TODO (mascot sheet dùng Be Vietnam Pro; ghi đúng font trong file Figma của bạn).
- Thang cỡ chữ: 28 / 22 / 18 / 16 / 14 / 12 sp. Chữ nội dung tối thiểu 14 sp.

## Khoảng cách, bo góc, elevation
- Khoảng cách: 4, 8, 12, 16, 20, 24 dp. Lề màn hình 20 dp.
- Bo góc: 12 (nút nhỏ, ô), 16 (nút lớn), 20 (thẻ).
- Elevation: 0 cho thẻ, 1 cho FAB. TODO: xác nhận.

## Tone
Thân thiện, ngắn gọn, không trách người dùng. Ví dụ: "Chưa có deadline nào", không viết "Bạn chưa làm gì".

## Quy tắc component
- Mỗi màn hình có một hành động chính.
- Vùng chạm tối thiểu 48 × 48 dp.
- Một dòng task chỉ có: checkbox, tiêu đề, một dòng phụ, thời hạn.
- Không truyền đạt mức khẩn cấp chỉ bằng màu: luôn kèm chữ hoặc hình.

## Mascot và họa tiết
- Mascot (Tụi Nốt) chỉ xuất hiện ở: đầu nhóm, thẻ tóm tắt, trạng thái rỗng / đang tải / lỗi, màn Đã nộp.
- Không đặt mascot trong từng dòng task.
- File gốc: `assets/mascot/`.
