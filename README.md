# PRM323 / PRM393 Lab 2 — Nốt: Study Planner cho sinh viên và người trẻ bận rộn

## Chủ đề

Nốt là app lập kế hoạch học và theo dõi deadline cho sinh viên năm cuối và người trẻ bận rộn (nhiều môn, đồ án, nghiên cứu khoa học, làm thêm, đi làm). App gom deadline về một chỗ thay cho Calendar, Notion, ClickUp và Linear; chia một deadline dài thành các giai đoạn phủ kín số ngày tới hạn (AI gợi ý từ mô tả, hoặc tự nhập); nhắc đúng giai đoạn mỗi ngày; cho thấy ngày nào quá nặng và gợi ý dời việc sang ngày nhẹ hơn trước hạn.

## Persona

Persona chính: **Minh**, 22 tuổi (giả định), sinh viên năm cuối, trưởng nhóm nghiên cứu khoa học 4 người, đi làm thêm, đang phải chuyển qua lại giữa Calendar, Notion, ClickUp và Linear.

Cả bộ có 4 persona (1 chính, 2 phụ, 1 hỗ trợ): Minh, Đăng Khoa (năm 2, làm ca tối), Bảo Ngọc (năm 1, lần đầu dùng app), Quốc Huy (lập trình viên đi làm, học khoá online buổi tối). Chi tiết ở [`ux/persona.md`](ux/persona.md).

## Link Figma

[PRM393-LAB2-Study-Planner](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=0-1)

Quyền chia sẻ: "Anyone with the link can view". Các page:

| Page | Nội dung |
|---|---|
| `00 Persona` | Tổng quan 4 persona, ma trận persona × flow, chân dung từng persona |
| `01 User Flow` | Sơ đồ 15 flow: 4 chính (C1–C4), 8 phụ (P1–P8), 3 trạng thái (S1–S3) |
| `02 Wireframe` | Wireframe low-fidelity của tất cả màn |
| `03 Final UI` | 74 frame trong 7 nhóm, biến thể trạng thái đặt cạnh màn gốc |
| `04 Design System` | Variables: màu (Color), khoảng cách và bo góc (Size); text styles; effect styles |
| `05 Components` | Thư viện component có variant (xem bên dưới) |
| `06 Prototype` | 15 flow có starting point, cùng tên với page 01 |
| `07 User flow - Canva` | Bản tham chiếu sơ đồ flow |
| `99 · Lưu trữ` | Các phương án cũ, không dùng để chấm |

Component chính ở page 05: Button (Filled, Tonal, Outlined, Text, Destructive × Default, Pressed, Disabled, Loading), Text field (Default, Focused, Filled, Error, Disabled), Card (Task, Summary × Default, Pressed), BottomNav 4 tab, App bar (Default, With actions), Dialog (Confirmation, Destructive), Loading state (Skeleton list, Spinner), Empty state, Error state (Offline, Load failed), Tag/Hạn nộp, Notification/Row, File/Đính kèm, Stepper/Thêm deadline, Switch, Mascot.

## Công cụ AI đã dùng

| Công cụ | Dùng để làm gì |
|---|---|
| Google Stitch | Tạo UI ban đầu và chạy các vòng lặp sửa UI |
| Claude | Phản biện UI theo heuristic và persona, viết prompt sửa cho Stitch, vẽ mascot Tụi Nốt và họa tiết (SVG), soạn bản nháp tài liệu, dựng sơ đồ User Flow, Final UI và Prototype trong Figma (qua Figma connector), đối chiếu tài liệu với Figma |

Chi tiết từng lần dùng: [`ai/ai-design-log.md`](ai/ai-design-log.md).

## Sản phẩm nằm ở đâu

| Sản phẩm | Vị trí |
|---|---|
| Persona, phát biểu vấn đề, tiêu chí thành công | [`ux/persona.md`](ux/persona.md) |
| Information architecture, 15 user flow, bảng flow → màn hình | [`ux/user-flow.md`](ux/user-flow.md) |
| Bản mô tả thiết kế (màu, chữ, khoảng cách, tone, quy tắc component) | [`design/DESIGN.md`](design/DESIGN.md) |
| Ý đồ từng màn hình và dữ liệu mẫu | [`design/screen-spec.md`](design/screen-spec.md) |
| Quyết định thiết kế và checklist accessibility | [`design/design-decisions.md`](design/design-decisions.md) |
| Prompt, kết quả, phản biện và quyết định với AI | [`ai/ai-design-log.md`](ai/ai-design-log.md) |
| Đặc tả cho lập trình viên Flutter | [`handoff/flutter-handoff.md`](handoff/flutter-handoff.md) |
| Ảnh chụp các phiên bản Stitch | [`assets/stitch/`](assets/stitch/) |
| PNG các màn hình cuối cùng (export từ Figma page 03) | [`assets/figma/`](assets/figma/) |
| Mascot Tụi Nốt, icon loại việc và họa tiết (SVG) | [`assets/mascot/`](assets/mascot/) |

## Tóm tắt thiết kế

| Hạng mục | Số lượng | Chi tiết |
|---|---|---|
| Tab | 4 | Hôm nay, Kế hoạch (Tháng / Tuần), Deadline (Sắp đến hạn / Môn học), Hồ sơ |
| Nhóm màn | 7 | 01 Xác thực, 02 Làm quen, 03 Hôm nay, 04 Kế hoạch, 05 Thông báo, 06 Deadline, 07 Hồ sơ · Cài đặt |
| Frame ở page 03 | 74 | Gồm màn gốc, biến thể trạng thái và 3 overlay |
| User flow | 15 | C1 Thêm deadline, C2 Hôm nay → nộp bài, C3 Thông báo → mở giai đoạn, C4 Dời việc khi ngày quá nặng; P1–P8; S1 Rỗng, S2 Mất mạng, S3 Kiểm tra lỗi |
| Vòng lặp AI | 3 | Xem `ai/ai-design-log.md` |
