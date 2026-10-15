# AI design log

Quy tắc của log này:

- Prompt ghi **nguyên văn từng chữ**, kể cả lỗi chính tả. Không tóm tắt.
- Câu trả lời của AI được giữ **toàn bộ**.
- Mỗi đề xuất quan trọng có quyết định **Chấp nhận / Chỉnh sửa / Từ chối** kèm lý do gắn với persona, heuristic hoặc ràng buộc.
- Mọi ảnh nằm trong `assets/stitch/`, đặt tên `<số thứ tự>-<màn>-<trước|sau>.png`.

## Khai báo công cụ AI

| Công cụ | Dùng để làm gì | Giai đoạn |
|---|---|---|
| Google Stitch | Tạo UI ban đầu và chạy các vòng lặp sửa UI | 4, 5 |
| Claude | Phản biện UI theo heuristic và persona, viết prompt sửa cho Stitch, vẽ bộ mascot Tụi Nốt và họa tiết (SVG), soạn bản nháp persona, IA, DESIGN.md và handoff | 1–5, 9 |
| Claude (Figma connector) | Dựng sơ đồ trên page 01 User Flow | 2 |

> TODO: thêm dòng nếu đã dùng công cụ khác (ví dụ Figma AI, ChatGPT).

---

## 0. UI ban đầu (Stitch)

Nguồn: lịch sử chat của project Stitch `PRM393_Lab2` (stitch.withgoogle.com/projects/17773013488802061578), lấy lại ngày 15/10/2026. Lúc này app còn tên **Khe** và persona là sinh viên vừa học vừa làm ca tối; sau đó đổi thành **Nốt** và persona Khả Hân.

- **Bản DESIGN.md đưa cho Stitch (nguyên văn):** file `ai/stitch-source/DESIGN-v0-Khe.md` (tải lên Stitch ngày 06/10/2026, 12:14). Đoạn mở đầu:

```
# DESIGN.md: Khe (study planner)
## Overview
Khe is an Android study planner for university students who also work evening
shifts that change every week. The interface is calm, flat and quick to scan:
each visit lasts under a minute and is usually one-handed. Material 3, light
theme only, phone layout at 360x800 dp. All UI text is in Vietnamese.
```

- **Prompt nguyên văn, lần 1** (06/10/2026, 12:14, kèm file DESIGN.md):

```
Tạo một hệ thống thiết kế bằng [DESIGN.md].
```

- **Prompt nguyên văn, lần 2** (06/10/2026, 12:55):

```
Thiết kế màn hình "Hôm nay" (Today screen)
```

- **Năm yếu tố của prompt nằm ở đâu** (prompt ngắn, các yếu tố nằm trong DESIGN.md đi kèm):

| Yếu tố | Câu nguyên văn trong DESIGN.md hoặc prompt |
|---|---|
| Persona | "university students who also work evening shifts that change every week" |
| Task | "each visit lasts under a minute and is usually one-handed"; prompt 2: màn "Hôm nay" |
| Mobile platform | "Android … Material 3, light theme only, phone layout at 360x800 dp" |
| Constraints | "Every touch target is at least 48x48dp", "Body text is never smaller than 14sp", "Never color alone" |
| Style | "calm, flat and quick to scan", "Don't use gradients, glassmorphism, heavy shadows" |

- **Màn hình Stitch tạo ra ở giai đoạn đầu** (trước các vòng lặp có ghi log): Hôm nay (06/10), Kế hoạch, Deadline, Lịch bận. Toàn bộ prompt sau đó (19 lượt) xem ở lịch sử chat Stitch.
- **Ảnh kết quả:** `assets/stitch/01-deadline-truoc.png` (màn Deadline). TODO: tải ảnh Kế hoạch và Lịch bận từ Stitch (Export → PNG) vào `assets/stitch/`. Ảnh chụp tự động của Stitch cho màn Hôm nay bị lỗi (chỉ hiện khung trống), nên cần chụp lại từ canvas.
- **Nhận xét ban đầu:** giao diện dạng chồng thẻ, trông "quá AI" và nhàm, chưa giống các app quản lý việc quen thuộc (ClickUp). Màn Deadline dày và khó nhìn.

---

## Vòng lặp 1 — Hôm nay: thấy cả "làm gì trước" lẫn "làm lúc nào"

- **Màn hình:** Hôm nay (S02). Ngày 06/10/2026, 18:38.
- **Vấn đề có tên:** danh sách cho biết việc nào trước nhưng giấu thời gian; timeline cho biết thời gian nhưng giấu mức ưu tiên.
- **Heuristic:** Nielsen #7, Flexibility and efficiency of use.
- **Ảnh trước:** màn Stitch "Hôm nay (Day Timeline)". **Ảnh sau:** "Hôm nay - Danh sách" và "Hôm nay - Lịch ngày".

**Prompt gửi Stitch (nguyên văn, đoạn đầu):**

```
Problem: a list view shows what to do first but hides when; a timeline shows when but hides
priority. The user needs both, on the same data.
Redesign the "Hôm nay" screen with two views of the same items, switched by a segmented control
directly under the header: "Danh sách" and "Lịch ngày". Generate both views as two versions of
the screen.
```

- **Quyết định:** Chấp nhận. Hai chế độ dùng chung một kiểu dòng; về sau thành nút chuyển "Danh sách / Theo giờ" ở 2.1 Chi tiết ngày.

---

## Vòng lặp 2 — Lịch ngày: thấy thời lượng và khoảng trống thật

- **Màn hình:** Hôm nay, chế độ Lịch ngày. Ngày 06/10/2026, 18:42.
- **Vấn đề có tên:** timeline dạng danh sách không cho thấy việc kéo dài bao lâu và khoảng trống lớn cỡ nào.
- **Heuristic:** Nielsen #2, Match between system and the real world (giống chế độ ngày của app lịch).
- **Ảnh trước:** "Hôm nay - Lịch ngày". **Ảnh sau:** "Hôm nay - Lịch ngày (Hour Grid)".

**Prompt gửi Stitch (nguyên văn, đoạn đầu):**

```
Problem: the timeline list does not show how long things take or how big the free gaps really are.
Redesign the "Lịch ngày" view as a day view with an hour grid, like a calendar app's day view.
```

- **Quyết định:** Chấp nhận. Chiều cao khối = thời lượng; khoảng trống từ 45 phút có nút "Thêm vào đây". Trở thành chế độ "Theo giờ".

---

## Vòng lặp 3 — Mật độ thông tin quá cao, tín hiệu khẩn cấp bị lặp

- **Màn hình:** Deadline (S04). Ngày 07/10/2026. Lần thử đầu lúc 14:32 (màn "Deadline (Tinh giản)"), bản chốt lúc 15:46.
- **Vấn đề có tên:** mỗi dòng việc có 7 thành phần; mức khẩn cấp hiện ba lần (tiêu đề nhóm, chip màu, vòng checkbox đỏ).
- **Heuristic:** Nielsen #8, Aesthetic and minimalist design.
- **Liên quan persona:** Hân có 7–8 deadline mỗi tuần và xem app dưới một phút, nên phải đọc lướt được.
- **Ảnh trước:** `assets/stitch/01-deadline-truoc.png`

**Prompt phản biện gửi Claude (nguyên văn):**

```
Cái này nhìn đang bị dày và khó chịu quá
```

**Câu trả lời của Claude (toàn bộ):**

```
TODO: dán toàn bộ câu trả lời của Claude.
```

**Bảng quyết định:**

| # | Phát hiện của Claude | Quyết định | Lý do |
|---|---|---|---|
| 1 | Mức khẩn cấp lặp 3 lần: tiêu đề nhóm, chip màu, vòng checkbox đỏ | Chấp nhận | Nielsen #8. Tiêu đề nhóm đã đủ nói mức gấp; giữ thời hạn dạng chữ bên phải để không phụ thuộc màu |
| 2 | Tiến độ lặp 2 lần: chữ "2/3 buổi" và thanh tiến độ | Chấp nhận | Giữ chữ "2/3 buổi" vì đọc được khi liếc và không cần màu; bỏ thanh tiến độ khỏi dòng (vẫn giữ ở Chi tiết deadline) |
| 3 | Số lượng lặp 2 lần: thẻ thống kê và số đếm ở tiêu đề nhóm | Chỉnh sửa | Không chỉ bỏ thẻ: thay thẻ ba con số bằng banner một câu ("1 việc quá hạn"), vì Hân cần biết ngay điều quan trọng nhất, không cần ba con số ngang hàng |
| 4 | Quá nhiều màu ngang hàng nhau | Chấp nhận | Nielsen #8. Màu nóng chỉ dành cho mức gấp và lịch nhiệt (DESIGN.md, nguyên tắc 5) |
| 5 | Dòng cao khoảng 44 dp, dưới mức vùng chạm 48 dp | Chấp nhận | Yêu cầu accessibility của đề và persona dùng một tay. Dòng tăng lên 60 dp |
| 6 | Cờ outline và cờ đặc khó phân biệt | TODO | TODO: ảnh sau vòng 1 vẫn còn cờ. Ghi quyết định thật của bạn |
| 7 | FAB che chữ của dòng cuối và cùng màu với tab đang chọn | Chấp nhận, xử lý ở vòng 2 | Che thời hạn của dòng cuối là mất thông tin. Lỗi này vẫn còn sau vòng 1 |

**Prompt gửi Stitch (nguyên văn):**

```
Use the attached image as the layout reference for the Deadline screen.
Keep my current colors, font and Vietnamese labels.

Changes:
- Replace the 3-number summary card with one summary banner:
  primary color background, title "1 việc quá hạn", subtitle
  "5 việc cần xong trong tuần này", and an empty 72x80dp image
  placeholder on the right labeled "mascot".
- Each group header (QUÁ HẠN, HÔM NAY, TUẦN NÀY, SAU ĐÓ) starts with an
  empty 24x24dp image placeholder labeled "mascot", then the group name
  as plain 12sp uppercase text, then the item count on the right.
- Do not draw any character or illustration. Leave the placeholders as
  plain rounded rectangles. I will add the artwork in Figma.
- Each task row has only: checkbox, title, one subtitle line, due text.
  No progress bar, no colored chips. Row height 60dp.
- Create a second screen for the empty state: a 260dp rounded area with
  a centered 140dp image placeholder labeled "mascot", the title
  "Chưa có deadline nào", one line of body text, and a primary button
  "Thêm deadline".
```

> TODO: so lại với prompt đã gửi thật. Nếu khác dù một chữ, sửa theo bản đã gửi.

- **Ảnh sau:** `assets/stitch/02-deadline-va-rong-sau-vong-1.png`
- **Kết quả:** dòng việc gọn, mức khẩn cấp chỉ còn ở tiêu đề nhóm và thời hạn dạng chữ; có thêm màn empty state.
- **Lỗi còn lại (chuyển sang vòng 2):** FAB che thời hạn của dòng cuối; tab thứ tư ghi "Ca làm" ở một màn và "Lịch bận" ở màn kia; màn rỗng có hai nút cùng việc (FAB và "Thêm deadline"); câu mô tả ở màn rỗng bị Stitch viết lại khác ý.

---

## Vòng sửa lỗi (07/10) — Nhãn điều hướng không nhất quán và hành động chính bị trùng

- **Màn hình:** Deadline (S04) và trạng thái rỗng của Deadline.
- **Vấn đề có tên:** cùng một tab có hai tên khác nhau; màn rỗng có hai nút làm cùng một việc; FAB che nội dung.
- **Heuristic:** Nielsen #4, Consistency and standards (tên tab), Nielsen #8 (hai hành động chính cạnh tranh), Nielsen #1 (thông tin bị che).
- **Khác vòng 1 ở chỗ:** vòng 1 giảm mật độ trong một dòng; vòng 2 sửa tính nhất quán giữa các màn và thứ bậc hành động.
- **Ảnh trước:** `assets/stitch/02-deadline-va-rong-sau-vong-1.png`

**Prompt gửi Stitch (nguyên văn):**

```
Fix these issues. Do not change anything else.
- Deadline screen: add 88dp bottom padding to the list so the FAB does
  not cover the due text of the last row.
- Bottom navigation: the fourth tab label is "Lịch bận" on every screen.
- Empty state screen: remove the FAB. Keep only the "Thêm deadline" button.
- Empty state body text: "Thêm deadline đầu tiên. Nốt sẽ thức dậy và
  nhắc bạn trước hạn."
```

- **Ảnh sau:** TODO: chạy prompt, lưu `assets/stitch/03-deadline-va-rong-sau-vong-2.png`.
- **Quyết định và lý do:** TODO sau khi xem kết quả. Gợi ý kiểm tra: tab thứ tư đúng "Lịch bận" trên mọi màn; màn rỗng chỉ còn một nút; dòng cuối không bị che.

---

## Vòng lặp tiếp theo — TODO: tên vấn đề (phải khác các vòng trên)

- **Màn hình:** TODO
- **Vấn đề có tên và heuristic:** TODO
- **Ảnh trước:** TODO
- **Prompt nguyên văn:** TODO
- **Ảnh sau:** TODO
- **Quyết định và lý do:** TODO

> Ứng viên tốt cho vòng 3 (chọn một, xóa ghi chú này sau khi làm): lịch nhiệt ở Kế hoạch chỉ dùng màu để báo mức nặng (WCAG 1.4.1); hoặc màn Hôm nay chưa có loading, empty, error state (Nielsen #1, #9).

---

## Phản biện bằng AI theo 10 heuristic của Nielsen

Yêu cầu của đề: dùng heuristic có tên, accessibility và persona; ít nhất 5 phát hiện, mỗi phát hiện gắn với một màn hình cụ thể.

- **Ảnh đưa cho AI:** TODO: liệt kê ảnh các màn đã gửi.
- **Prompt nguyên văn:**

```
TODO: dán prompt đã gửi.
```

- **Toàn bộ câu trả lời:**

```
TODO: dán toàn bộ câu trả lời.
```

- **Bảng quyết định:**

| # | Màn hình | Phát hiện | Heuristic hoặc tiêu chí | Quyết định | Lý do | Thấy trong Figma ở |
|---|---|---|---|---|---|---|
| 1 | TODO | TODO | TODO | TODO | TODO | TODO |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

> Lý do hợp lệ phải nhắc tới persona (Hân), một heuristic, hoặc một ràng buộc (phạm vi, thời gian, nền tảng). "Mình thích" và "AI nói vậy" không được tính.
