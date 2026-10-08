# PRM323 Lab 2 — Nốt: Study Planner cho sinh viên năm cuối

## Chủ đề

Ứng dụng lập kế hoạch học và theo dõi deadline cho sinh viên năm cuối có tuần đã kín bởi 5 môn, đồ án và nghiên cứu, với deadline nằm rải rác trong nhiều nhóm Zalo. App gom deadline về một chỗ, cho thấy ngày nào đang quá tải bằng lịch nhiệt, và giúp xếp một việc bất ngờ vào khung giờ trống trong dưới 30 giây.

## Persona

Nguyễn Võ Khả Hân, 21 tuổi, sinh viên năm 4 ngành Kỹ thuật Phần mềm (Đại học FPT), học 5 môn cùng đồ án và nghiên cứu, nhận thêm freelance, có 7–8 deadline mỗi tuần trong 10 nhóm Zalo và thường vỡ kế hoạch khi một việc bất ngờ chen vào.

## Link Figma

[PRM393-LAB2-Study-Planner](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner)

Quyền chia sẻ: "Anyone with the link can view". File có 6 page theo thứ tự: 01 User Flow, 02 Wireframe, 03 Final UI, 04 Design System, 05 Components, 06 Prototype.

## Công cụ AI đã dùng

| Công cụ | Dùng để làm gì |
|---|---|
| Google Stitch | Tạo UI ban đầu và chạy các vòng lặp sửa UI |
| Claude | Phản biện UI theo heuristic và persona, viết prompt sửa cho Stitch, vẽ mascot Tụi Nốt và họa tiết (SVG), soạn bản nháp tài liệu, dựng sơ đồ page 01 User Flow trong Figma |

Chi tiết từng lần dùng: `ai/ai-design-log.md`.

## Sản phẩm nằm ở đâu

| Sản phẩm | Vị trí |
|---|---|
| Persona, phát biểu vấn đề, tiêu chí thành công | [`ux/persona.md`](ux/persona.md) |
| Information architecture, 5 user flow, bảng ánh xạ flow sang màn hình | [`ux/user-flow.md`](ux/user-flow.md) |
| Bản mô tả thiết kế (màu, chữ, khoảng cách, tone, quy tắc component) | [`design/DESIGN.md`](design/DESIGN.md) |
| Ý đồ từng màn hình và dữ liệu mẫu | [`design/screen-spec.md`](design/screen-spec.md) |
| 10 quyết định thiết kế và checklist accessibility | [`design/design-decisions.md`](design/design-decisions.md) |
| Prompt, kết quả, phản biện và quyết định với AI | [`ai/ai-design-log.md`](ai/ai-design-log.md) |
| Đặc tả cho lập trình viên Flutter | [`handoff/flutter-handoff.md`](handoff/flutter-handoff.md) |
| Ảnh chụp các phiên bản Stitch | [`assets/stitch/`](assets/stitch/) |
| PNG các màn hình cuối cùng (export từ Figma page 03) | [`assets/figma/`](assets/figma/) |
| Mascot Tụi Nốt, icon nhóm việc và họa tiết (SVG) | [`assets/mascot/`](assets/mascot/) |

## Tóm tắt thiết kế

| Hạng mục | Số lượng |
|---|---|
| Màn hình | 10: Đăng nhập, Hôm nay, Kế hoạch, Deadline, Lịch bận, Thêm / sửa deadline, Chi tiết deadline, Đã nộp, Chi tiết ngày, Hồ sơ |
| User flow | 5: Thêm deadline mới, Nộp một deadline, Giảm tải một ngày quá nặng, Xếp một việc phát sinh, Đổi nhắc hạn và đăng xuất |
| Vòng lặp AI | 3 (xem log) |
