# Quyết định thiết kế

10 quyết định quan trọng nhất của bản Nốt tích cực (sau khi đổi hướng ngày 24/10/2026), mỗi quyết định có lý do gắn với persona, một heuristic của Nielsen, WCAG, hoặc một ràng buộc thật (phạm vi, thời gian, nền tảng). Mã màn và mã flow giống Figma (xem [`ux/user-flow.md`](../ux/user-flow.md)).

---

## 1. Bảng quyết định

| # | Quyết định | Lý do | Thấy ở Figma |
|---|---|---|---|
| 1 | **Đổi đề tài từ app quản lý deadline sang app ghi chú tích cực; giữ màu, font và mascot** | Ràng buộc thật: giảng viên yêu cầu đổi hướng (24/10). Minh đã có Calendar, Notion, ClickUp, Linear để quản lý việc; nỗi đau còn lại là tinh thần, không phải danh sách việc. Giữ design system để không làm lại page 04–05 | Section `Final UI · Nốt tích cực (24/10)` trên page 03 |
| 2 | **Ghi nốt chỉ 3 bước (tâm trạng → chiến thắng → nhật ký), bước 3 bỏ qua được; có chip chiến thắng chọn nhanh** | Tiêu chí thành công: ghi xong dưới 30 giây. Minh mở app lúc 22h–1h, nằm, một tay. Nielsen #7 (linh hoạt, hiệu quả): người mệt chỉ cần chạm 1 chip | `S03a`, `S03b`; flow F1 |
| 3 | **Mỗi màn một hình lớn + một hành động chính; Hũ dùng lưới tờ nốt thay cho danh sách thẻ** | Góp ý giảng viên: bản trước nhiều chữ và rối. Nielsen #8 (tối giản). Rubric "một hành động chính rõ ràng mỗi màn" | `S02`, `S05`, `S07`; bản v1 ở page 99 |
| 4 | **Không phạt: đếm số nốt và số lần tự chủ; thử thách "để mai" không bị trừ; lỡ lướt vẫn được ghi "Nhận ra cũng là bắt đầu tự chủ"** | Điều Minh không muốn: "mất chuỗi là về 0". Bài học ngược từ Opal (streak gây áp lực). Nielsen #9 (giúp phục hồi) | `S09`, `S11b`; flow F2, F3 |
| 5 | **Nút "Mình vừa dừng lại" 1 chạm trên `S02`, không cần mở khoá; danh sách thói quen ở `S09` thì khoá** | Tiêu chí phụ: 1 lần chạm. Học từ one sec (một nhịp dừng nhỏ). Riêng tư là tính năng chính (Fortify, Brainbuddy): Quốc Huy không muốn người khác thấy | `S02`, `S09`, `S12`; flow F2 |
| 6 | **Màn thở 90 giây cho lúc khó dừng, sau đó gợi ý việc thay thế** | Nielsen #3 (người dùng kiểm soát): có lối ra "Thở thêm 1 vòng". Tiêu chí phụ: mở dưới 2 giây nên không có bước tải dữ liệu | `S10`, `S10 · sau khi thở`; flow F2 |
| 7 | **Tâm trạng luôn có màu + mặt mascot + chữ; thang `heat/*` đổi nghĩa thành tâm trạng (lạnh = vui, ấm = rối)** | WCAG 1.4.1 (không chỉ dùng màu); nhu cầu accessibility của Minh. Học từ How We Feel (lưới tâm trạng). Dùng lại biến cũ để không phá component | `MoodOption`, `Cell/Ngày năng lượng`, `S11c` |
| 8 | **Mất mạng thì lưu trên máy và báo bằng banner; thoát giữa chừng thì hỏi "Giữ nốt đang ghi?"** | Bảo Ngọc ở ký túc xá mạng chập chờn. Bài học từ Finch (người dùng mất dữ liệu). Nielsen #5 (ngăn lỗi), #1 (hiển thị trạng thái) | `S04 · lưu khi mất mạng`, `Overlay · Giữ nốt đang ghi?`; flow F1, T2 |
| 9 | **Xoá nốt cần dialog destructive và có Hoàn tác 5 giây** | Nielsen #3 (kiểm soát, có lối thoát) và #5 (ngăn lỗi): bấm nhầm bằng một tay khi nằm | `S06 · dialog xoá nốt`, `S05 · vừa xoá nốt`; flow P5 |
| 10 | **Thiết kế sẵn Đăng nhập Google, Cài đặt, trạng thái đang tải, và tính năng AI "Nốt sắp xếp giúp" có nhãn "Gợi ý từ AI", cho sửa, có màn "AI đang nghỉ"** | Ràng buộc Lab 3 (Google Sign-In, Remote Config, FCM) và Final Assignment (Gemini Level 2: người dùng xác nhận, có fallback, không gửi dữ liệu cá nhân). Thiết kế trước để không phải thêm màn ngoài Figma | `S01`, `S12`, `S11c · đang tải`, section `AI · Nốt sắp xếp giúp (Gemini)` |

---

## 2. Checklist accessibility và responsive

Kiểm tra trên page `03 Final UI` ngày 24/10/2026: 28 màn, 444 lớp chữ, 145 phần tử bấm được. Contrast tính bằng công thức WCAG 2.x (quét tự động bằng script trong Figma).

| Mục | Kết quả | Bằng chứng / cách sửa |
|---|---|---|
| Contrast chữ ≥ 4.5:1 (chữ thường), ≥ 3:1 (chữ lớn, điều khiển UI) | **Đạt** — thấp nhất 4.56:1 | Trước khi sửa có 7 lỗi: token `success` `#1F9D63` trên nền xanh nhạt chỉ 3.0:1 → đổi token thành `#187A4D` (4.63:1 trên nền nhạt, 5.31:1 trên trắng); ô lịch "Rối" chữ trắng trên đỏ 3.5:1 → chữ màu `on-surface`; chữ gợi ý ở Thẻ tuần opacity 0.75 → 0.92 |
| Vùng chạm ≥ 48 × 48 dp | **Đạt** | Chip "chiến thắng nhanh" 40–42 → minHeight 48 (sửa ở component); Button minWidth 64 (nút "Bỏ" trong dialog từng chỉ 46); tab Con đường / Thống kê / Lịch và Tháng / Năm 40 → 48. Gỡ 1 link cũ trên chữ chú giải 18 × 17 |
| Chữ nội dung ≥ 14 sp | **Đạt** | Nội dung dùng Body 15–16. Chữ 12–13 chỉ cho nhãn phụ (ngày, meta, chú thích). Chữ dưới 12 (9–10.5 px ở trục Year in pixels, số ngày trên Thẻ tuần, nhãn tháng của sticker) → nâng lên 12 hoặc ẩn khi chỉ để trang trí |
| Không truyền thông tin chỉ bằng màu | **Đạt** | Tâm trạng: màu + mặt mascot + chữ trong chú giải; biểu đồ: chú giải có chữ, tooltip có số, dòng cuối viết ý chính; nút trên Con đường: tick / ngôi sao / ổ khoá; tờ nốt có nhãn loại bằng chữ |
| Bố cục dùng Auto Layout, kiểm tra ở 360 dp và 412 dp | **Đạt** (có ghi chú) | Section `A11y · kiểm tra 360 dp / 412 dp (24/10)` trên page 03: `S02`, `S03b`, `S09`, `S11b` ở 360 × 800 và 412 × 915. Auto Layout FILL giãn đúng; thanh tab căn giữa, nút nổi bám phải. Ghi chú: biểu đồ vẽ cố định 294 px trong Figma; trong Flutter dùng `fl_chart` co giãn theo chiều rộng thẻ |
| Component dùng token | **Đạt một phần** | Màu của các component mới (`Card/Nốt`, `Note/Tờ nốt`, `MoodOption`, `Chip/Chiến thắng nhanh`, `Cell/Ngày năng lượng`) gắn Variable. Bo góc 14, 16, 32, 999 chưa có Variable → cần thêm `radius/14`, `radius/16`, `radius/32`, `radius/full` (xem `DESIGN.md` mục 5.2) |

Ảnh bằng chứng: export các frame trong section A11y vào `assets/figma/`.
