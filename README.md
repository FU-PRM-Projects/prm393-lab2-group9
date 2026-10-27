# PRM323 / PRM393 Lab 2 — Nốt: mỗi ngày một nốt tích cực

## Chủ đề

Nốt là app ghi chú hằng ngày mang năng lượng tích cực cho sinh viên năm cuối đang kiệt sức (và người trẻ đi làm). Mỗi tối người dùng ghi một "chiến thắng nhỏ" vào hũ chiến thắng thay vì nhìn danh sách việc chưa xong. App gom 5 thói quen tốt vào một vòng lặp: (1) chiến thắng nhỏ, (2) nhật ký, (3) tự chủ trước "dopamine rẻ" (lướt mạng vô thức, video ngắn, game quá giờ, nội dung không lành mạnh), (4) nói chuyện với người lạ, (5) vận động.

> **Đổi hướng ngày 24/10/2026:** theo góp ý giảng viên, Nốt chuyển từ app quản lý deadline (Study Planner) sang app ghi chú tích cực. Giữ màu, font và mascot Tụi Nốt. Bản Study Planner cũ xem ở commit `5f00bff`; trong Figma, các section cũ `01 · Xác thực` … `07 · Hồ sơ · Cài đặt` trên page 03 không còn dùng để chấm.

## Persona

Persona chính: **Minh**, 22 tuổi, sinh viên năm 4 Kỹ thuật phần mềm, trưởng nhóm nghiên cứu, làm thêm; mỗi tối chỉ nhớ việc chưa xong và lướt điện thoại đến 1–2h sáng để trốn áp lực.

Persona phụ: Quốc Huy (27, nhân viên văn phòng, tối tự học), Bảo Ngọc (18, sinh viên năm nhất, ngại nói chuyện). Chi tiết ở [`ux/persona.md`](ux/persona.md).

**Tiêu chí thành công:** ghi xong một chiến thắng nhỏ (tâm trạng + 1 chiến thắng) trong dưới 30 giây kể từ khi chạm thông báo buổi tối.

## Link Figma

[PRM393-LAB2-Study-Planner](https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=0-1)

Quyền chia sẻ: "Anyone with the link can view". Các page:

| Page | Nội dung |
|---|---|
| `01 User Flow` | Khung "User Flow · Nốt tích cực (24/10)": 3 flow chính (F1–F3), 8 flow phụ (P1–P8), 3 flow trạng thái (T1–T3) |
| `02 Wireframe` | Wireframe low-fidelity |
| `03 Final UI` | Section **Final UI · Nốt tích cực (24/10)**: 12 màn S01–S12 cùng biến thể trạng thái và overlay; section **AI · Nốt sắp xếp giúp (Gemini)** cho Final Assignment; section **A11y · kiểm tra 360 dp / 412 dp** |
| `04 Design System` | Variables: màu (Color), khoảng cách và bo góc (Size); text styles; effect styles |
| `05 Components` | Thư viện component có variant (xem bên dưới) |
| `06 Prototype` | 5 flow có starting point: F1 Ghi nốt buổi tối, F2 Tự chủ, F3 Thử thách, F4 Hành trình, P1 Đăng nhập lần đầu |
| `07 User flow - Canva` | Bản tham chiếu sơ đồ flow |
| `99 · Lưu trữ` | Các phương án cũ (bảng màu thử, Final UI v1), không dùng để chấm |

Component dùng trong Final UI (page 05): Button (Filled, Tonal, Outlined, Text, Destructive × Default, Pressed, Disabled, Loading), Text field (Default, Focused, Filled, Error, Disabled), Card/Nốt (4 loại × Default, Pressed), BottomNav · Nốt (4 tab), App bar (Default, With actions), Dialog (Confirmation, Destructive), Loading state, Empty state, Error state, MoodOption, Chip/Chiến thắng nhanh, Note/Tờ nốt, Cell/Ngày năng lượng, Cell/Pixel năm, Sticker/Mốc, SettingRow, Switch, Mascot.

## Công cụ AI đã dùng

| Công cụ | Dùng để làm gì |
|---|---|
| Google Stitch | Tạo UI ban đầu và chạy các vòng lặp sửa UI |
| Claude | Phản biện UI theo heuristic và persona, viết prompt sửa cho Stitch, vẽ mascot Tụi Nốt và họa tiết (SVG), phân tích app tương tự, soạn persona, user flow và tài liệu, dựng sơ đồ User Flow, Final UI và Prototype trong Figma (qua Figma connector), quét contrast và vùng chạm, đối chiếu tài liệu với Figma |

Chi tiết từng lần dùng: [`ai/ai-design-log.md`](ai/ai-design-log.md).

## Sản phẩm nằm ở đâu

| Sản phẩm | Vị trí |
|---|---|
| Persona, phát biểu vấn đề, tiêu chí thành công | [`ux/persona.md`](ux/persona.md) |
| Information architecture, user flow, bảng flow → màn hình | [`ux/user-flow.md`](ux/user-flow.md) |
| Bản mô tả thiết kế (màu, chữ, khoảng cách, tone, quy tắc component) | [`design/DESIGN.md`](design/DESIGN.md) |
| Ý đồ từng màn hình và dữ liệu mẫu | [`design/screen-spec.md`](design/screen-spec.md) |
| Quyết định thiết kế và checklist accessibility | [`design/design-decisions.md`](design/design-decisions.md) |
| Prompt, kết quả, phản biện và quyết định với AI | [`ai/ai-design-log.md`](ai/ai-design-log.md) |
| Đặc tả cho lập trình viên Flutter | [`handoff/flutter-handoff.md`](handoff/flutter-handoff.md) |
| Ảnh chụp các phiên bản Stitch | [`assets/stitch/`](assets/stitch/) |
| Ảnh trước và sau của 7 vòng sửa UI trên Figma với Claude (bản Study Planner, 16–17/10) | [`assets/ai-iterations/`](assets/ai-iterations/) |
| PNG các màn hình cuối cùng (export từ Figma page 03) | [`assets/figma/`](assets/figma/) |
| Mascot Tụi Nốt và họa tiết (SVG) | [`assets/mascot/`](assets/mascot/) |

## Tóm tắt thiết kế

| Hạng mục | Số lượng | Chi tiết |
|---|---|---|
| Tab | 4 | Hôm nay, Hũ, Thử thách, Hành trình |
| Màn hình | 12 | S01 Chào mừng & Đăng nhập, S02 Hôm nay, S03 Ghi nốt, S04 Nốt đã vào hũ, S05 Hũ & Nhật ký, S06 Chi tiết nốt, S07 Thử thách, S08 Chi tiết thử thách, S09 Tự chủ, S10 Thở 90 giây, S11 Hành trình, S12 Cài đặt |
| Frame ở page 03 (bản mới) | 30 + 8 AI + 8 a11y | Màn gốc, biến thể trạng thái, overlay |
| User flow | 14 | F1 Ghi nốt buổi tối, F2 Tự chủ: dừng lướt vô thức, F3 Nhận và hoàn thành thử thách; P1–P8; T1 Hũ rỗng, T2 Mất mạng, T3 Đang tải |
| Vòng lặp AI | 3 vòng Stitch + 7 vòng trên Figma | Xem `ai/ai-design-log.md` |
