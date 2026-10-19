# PRM323 / PRM393 Lab 2 — Nốt: Study Planner cho sinh viên & người trẻ bận rộn

## Chủ đề

Ứng dụng lập kế hoạch học và theo dõi deadline cho sinh viên và người trẻ bận rộn (học nhiều môn, làm đồ án tốt nghiệp, nghiên cứu khoa học, làm thêm ca tối, freelance). App giải quyết vấn đề phân mảnh khi phải chuyển qua lại giữa nhiều công cụ (Calendar, Notion, ClickUp, Zalo), gom deadline về một nơi, cho phép chia deadline dài hạn thành các giai đoạn khớp đúng số ngày kèm tệp đính kèm, cảnh báo ngày quá tải qua lịch nhiệt 5 mức, và hỗ trợ dời việc hoặc lùi lịch khi đổi ca đột xuất trong dưới 10 giây.

## Hệ thống Persona

Gồm 4 persona (1 chính, 2 phụ, 1 hỗ trợ):
1. **Minh (Primary Persona - 21–22 tuổi):** Sinh viên năm cuối, Trưởng nhóm nghiên cứu khoa học 4 người, làm thêm; cần quản lý deadline dài hạn (paper hội nghị), chia giai đoạn khớp 31 ngày, ghi chú phân công ai làm phần nào và đính kèm tệp (DOCX, PDF, XLSX, ZIP) thay vì dùng cùng lúc Calendar, Notion, ClickUp.
2. **Đăng Khoa (Secondary Persona - 20 tuổi):** Sinh viên năm 2 CNTT, làm thêm ca tối quán cà phê (18:00–22:00, 4 tối/tuần), 4G chập chờn; cần thêm giờ bận và lùi việc bị trùng trong vài giây, hoạt động offline.
3. **Bảo Ngọc (Secondary Persona - 18 tuổi):** Sinh viên năm 1 Thiết kế đồ họa ở ký túc xá, lần đầu dùng app; cần onboarding làm quen 3 câu hỏi và hỗ trợ chia nhỏ đồ án dài hạn thành các phiên làm 45 phút.
4. **Quốc Huy (Supporting Persona - 24 tuổi):** Lập trình viên đi làm toàn thời gian (8:00–17:00), dùng Android phóng to chữ 130%; cần nhắc nhở kín đáo tránh reo khi đang họp và giao diện không bị vỡ layout khi phóng to chữ.

## Link Figma

[PRM393-LAB2-Study-Planner](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=767-1906)

Quyền chia sẻ: "Anyone with the link can view". File có 9 page theo thứ tự:
- `00 Persona`: Tổng quan 4 persona, ma trận Persona × Flow, chi tiết chân dung và template 5 khối
- `01 User Flow`: Sơ đồ luồng người dùng hoàn chỉnh cho toàn bộ hệ thống
- `02 Wireframe`: Dàn khung cấu trúc màn hình cho cả 7 phân hệ
- `03 Final UI`: Thiết kế giao diện chi tiết hoàn chỉnh (High-fidelity) cho tất cả các thiết bị và trạng thái
- `04 Design System`: Hệ thống biến (Variables), bảng màu vai trò M3, màu lịch nhiệt, typography, khoảng cách, bo góc
- `05 Components`: Thư viện component tái sử dụng (Buttons, Cards, Task Rows, Heat Cells, Form Controls, Dialogs, Overlays)
- `06 Prototype`: Bản mẫu tương tác hoàn chỉnh, phân chia theo nhóm Flow chính (C1–C4), Flow phụ (P1–P8), và Trạng thái lỗi (S1–S2)
- `07 User flow - Canva`: Tham chiếu sơ đồ trực quan luồng trải nghiệm
- `99 · Lưu trữ`: Bản lưu nháp các phiên bản trước

## Công cụ AI đã dùng

| Công cụ | Dùng để làm gì |
|---|---|
| Google Stitch | Tạo UI ban đầu và chạy các vòng lặp sửa UI |
| Claude | Phản biện UI theo heuristic và persona, viết prompt sửa cho Stitch, vẽ mascot Tụi Nốt và họa tiết (SVG), soạn bản nháp tài liệu, dựng sơ đồ User Flow và Prototype trong Figma |

Chi tiết từng lần dùng: `ai/ai-design-log.md`.

## Sản phẩm nằm ở đâu

| Sản phẩm | Vị trí |
|---|---|
| Persona (4 chân dung, ma trận flow, tiêu chí thành công) | [`ux/persona.md`](ux/persona.md) |
| Information architecture, danh mục flow (C1–C4, P1–P8, S1–S2), bảng ánh xạ | [`ux/user-flow.md`](ux/user-flow.md) |
| Bản mô tả thiết kế (màu, chữ, khoảng cách, tone, quy tắc component) | [`design/DESIGN.md`](design/DESIGN.md) |
| Ý đồ từng màn hình trong 7 phân hệ và dữ liệu mẫu | [`design/screen-spec.md`](design/screen-spec.md) |
| Quyết định thiết kế và checklist accessibility (kèm test text 130%) | [`design/design-decisions.md`](design/design-decisions.md) |
| Prompt, kết quả, phản biện và quyết định với AI | [`ai/ai-design-log.md`](ai/ai-design-log.md) |
| Đặc tả cho lập trình viên Flutter | [`handoff/flutter-handoff.md`](handoff/flutter-handoff.md) |
| Ảnh chụp các phiên bản Stitch | [`assets/stitch/`](assets/stitch/) |
| PNG các màn hình cuối cùng (export từ Figma page 03) | [`assets/figma/`](assets/figma/) |
| Mascot Tụi Nốt, icon nhóm việc và họa tiết (SVG) | [`assets/mascot/`](assets/mascot/) |

## Tóm tắt thiết kế

| Hạng mục | Số lượng | Chi tiết |
|---|---|---|
| Phân hệ màn hình | 7 nhóm lớn | 01 Xác thực, 02 Làm quen, 03 Hôm nay & Chia nhỏ việc, 04 Kế hoạch & Dời việc, 05 Thông báo, 06 Deadline & Giai đoạn/Tệp đính kèm, 07 Hồ sơ & Cài đặt |
| Màn hình & Device Frames | 25+ frames | Đăng nhập/Đăng ký/Quên mật khẩu, Onboarding 3 câu hỏi, Dashboard Hôm nay, Bảng thành tích, Lịch nhiệt tháng, Lịch tuần & Giờ bận, Chi tiết ngày, Thông báo (13A/13B), Thêm deadline AI, Chi tiết giai đoạn dự án & Đính kèm tệp, Xử lý quá hạn, Hồ sơ, Cài đặt, Demo kiểm tra lỗi 130% |
| User flow | 14 flow & trạng thái | 4 Flow chính (C1–C4), 8 Flow phụ (P1–P8), 2 Trạng thái lỗi và phục hồi (S1–S2) |
| Vòng lặp AI | 3 vòng lặp chính | Xem chi tiết trong log thiết kế |

