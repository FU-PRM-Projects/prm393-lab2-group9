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
| Claude (Figma connector) | Dựng sơ đồ trên page 01 User Flow; đọc page 00–06 để đối chiếu tài liệu với Figma (20/10) | 2, 9 |
| Claude (tài liệu) | Viết lại `ux/user-flow.md`, `ux/persona.md`, `README.md`, `design/DESIGN.md`, `design/screen-spec.md`, `design/design-decisions.md`, `handoff/flutter-handoff.md` cho khớp Figma (20/10); viết lại lần nữa theo bản đổi hướng "Nốt tích cực" (27/10) | 1–3, 9 |
| Claude (phân tích, Figma) | Phân tích app tương tự (Finch, Daylio, How We Feel, one sec, Opal, Fortify, Unmute), viết persona và user flow mới, dựng Final UI và Prototype bản Nốt tích cực, quét contrast và vùng chạm (24/10) | 1–2, 6–8 |

| Claude (Figma connector, Cowork) | 7 vòng sửa UI trên Figma (16–17/10, mục "Vòng lặp trên Figma") và phản biện theo heuristic (20/10) | 5, 6 |

> Nếu nhóm còn dùng công cụ AI khác (ví dụ Figma AI, ChatGPT, Gemini), thêm một dòng vào bảng này.

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
| 6 | Cờ outline và cờ đặc khó phân biệt | Chấp nhận (làm ở Figma) | Nielsen #4 và WCAG 1.4.1: hai kiểu cờ chỉ khác nhau ở độ đặc, khó phân biệt khi liếc. Stitch vẫn giữ cờ sau vòng 1, nên nhóm bỏ cờ khi dựng lại trong Figma; mức hạn giờ dùng `Tag/Hạn nộp` có chữ ("Trễ 1 ngày", "Còn 6 giờ") |
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

## Vòng lặp trên Figma với Claude (16–17/10/2026)

Sau khi dựng lại UI trong Figma (Stitch xuất ra các layer rời, đề bài yêu cầu dựng lại bằng Auto Layout và component), nhóm dùng Claude qua Figma connector để sửa từng vấn đề. Mỗi vòng nhắm một vấn đề có tên khác nhau. Ảnh trước và sau nằm ở `assets/ai-iterations/` (số đỏ trên ảnh "trước" là số của vấn đề). Bản trình bày các vòng này là slide "Nốt · AI Iterations".

> **Prompt nguyên văn của các vòng F1–F7:** nằm trong các phiên Claude ngày 16–17/10. TODO: mở lại lịch sử chat và dán nguyên văn từng prompt vào dòng "Prompt" của mỗi vòng.

| Vòng | Màn hình | Vấn đề có tên | Tiêu chí | Ảnh trước → sau | AI đã làm | Quyết định và lý do |
|---|---|---|---|---|---|---|
| F1 | Deadline (`5`) | Danh sách là một khối liền, không có ranh giới giữa các nhóm, khó đọc lướt | Nielsen #8 | `vong-f1-deadline-truoc.png` → `vong-f1-deadline-sau.png` | Mỗi nhóm một thẻ, mọi dòng cao 56 dp, lề 16 dp | **Chỉnh sửa.** AI không thấy nhóm cuối dùng nhầm mascot vàng của nhóm Tuần này; nhóm tự sửa và đổi tên nhóm "Sau này" thành "Sắp tới" |
| F2 | Xem trước dời việc (`4b`) | App tự chọn ngày đích, người dùng không đổi được | Nielsen #3 | `vong-f2-doi-viec-truoc.png` → `vong-f2-doi-viec-sau.png` | Bản đầu vẫn không cho chọn. Sau khi yêu cầu lại: mỗi việc có checkbox và ô "Dời sang" có ngày đề xuất, ngày sau hạn bị khoá | **Chỉnh sửa.** Đăng Khoa cần tự quyết khi đổi ca; ngày sau hạn bị khoá để ngăn lỗi (Nielsen #5) |
| F3 | Giai đoạn đã xong (`7s1`) | Tệp đính kèm hiển thị bằng emoji, mỗi máy vẽ khác nhau | Nielsen #4 | `vong-f3-ghi-chep-giai-doan-truoc.png` → `vong-f3-ghi-chep-giai-doan-sau.png` | Icon theo loại tệp, thẻ "Đã xong" màu xanh với thanh 3 giai đoạn, ghi chép dạng dòng thời gian | **Chấp nhận.** Bản của AI đạt mục tiêu |
| F4 | Thêm deadline, bước giai đoạn | Giai đoạn chỉ có ngày, không có giờ làm và lời nhắc; bấm Lưu mà không biết khi nào được nhắc | Nielsen #2 | `vong-f4-them-deadline-giai-doan-truoc.png` → `vong-f4-them-deadline-giai-doan-sau.png` | Luồng 4 bước (Môn, Deadline, Giai đoạn, Xem lại); mỗi giai đoạn có ngày, giờ và nhãn nhắc; bước Xem lại liệt kê mọi lời nhắc | **Chỉnh sửa.** Chữ của AI quá dài nên gộp ngày và giờ thành một dòng. Vòng F7 đổi tiếp sang khoảng ngày |
| F5 | Thông báo (`13`) | Mascot thay cho icon, màu là tín hiệu duy nhất để biết loại thông báo | WCAG 1.4.1 | `vong-f5-thong-bao-truoc.png` → `vong-f5-thong-bao-sau.png` | Bản đầu dùng thẻ lớn, quá dày. Sau 3 prompt nữa: mỗi thông báo một dòng, một icon màu theo loại, giờ tương đối ("15 phút", "2 giờ") | **Chỉnh sửa.** Minh xem thông báo trong vài giây, nên cần một dòng mỗi thông báo |
| F6 | Chi tiết giai đoạn (`7s`) | Chỉ có một link, không thấy tệp DOCX, PDF đã làm | Nielsen #1 | `vong-f6-chi-tiet-giai-doan-truoc.png` → `vong-f6-chi-tiet-giai-doan-sau.png` | Danh sách tệp có icon theo loại, dòng "Nhắc 18:00", thẻ tiến độ, nút Tải lên | **Chấp nhận.** Đúng nỗi đau "không nhớ đã làm gì ở từng giai đoạn" của Minh |
| F7 | Thêm deadline, bước giai đoạn (`6b3`, `6b4`) | Mỗi giai đoạn chỉ là một buổi tối, nhưng giai đoạn thật như "chạy thực nghiệm" kéo dài cả tuần | Persona Minh | `vong-f7-giai-doan-nhieu-ngay-truoc.png` → `vong-f7-giai-doan-nhieu-ngay-sau.png`, `vong-f7-giai-doan-nhieu-ngay-sau-sheet.png` | Nút chuyển Môn học / Dự án ở bước 1; giai đoạn có từ ngày đến ngày; thanh "31/31 ngày"; giờ nhắc mỗi ngày trong sheet; thêm ô "Giao cho" với avatar thành viên | **Chỉnh sửa.** Bỏ ô "Giao cho": Nốt là app cá nhân, ai làm phần nào ghi trong ghi chép của giai đoạn |

---

## Phản biện bằng AI theo 10 heuristic của Nielsen (20/10/2026)

Yêu cầu của đề: dùng heuristic có tên, accessibility và persona; ít nhất 5 phát hiện, mỗi phát hiện gắn với một màn hình cụ thể.

- **Công cụ:** Claude, đọc trực tiếp 75 màn của page `03 Final UI` qua Figma connector (cùng bộ ảnh trong `assets/figma/`).
- **Ảnh đưa cho AI:** toàn bộ `assets/figma/*.png` (75 màn, 360 × 800).
- **Yêu cầu của Kim (nguyên văn):** `Làm mục 1 2 3 trước` (mục 3 là phần phản biện AI còn trống trong log).
- **Prompt phản biện Claude dùng (nguyên văn):**

```
Review the final UI of the "Nốt" study planner (75 screens, 360x800, page 03 Final UI).
Primary persona: Minh, final-year student, team lead of 4, part-time job, opens the app
for a few seconds between classes on an iPhone 12, and currently juggles Google Calendar,
Notion, ClickUp and Linear. Secondary: Đăng Khoa (evening shifts, weak 4G), Bảo Ngọc
(first-year, first time using a planner). Supporting: Quốc Huy (developer, 130% text).
Check against Nielsen's 10 usability heuristics, WCAG 2.1 AA (contrast 4.5:1 for body
text and 3:1 for large text and UI controls, 48x48 dp touch targets, body text at least
14 sp, no information by colour alone), and the persona's needs.
Give at least 5 findings. For each finding: the screen code, what is wrong, the heuristic
or criterion, the severity (high, medium, low), and one concrete fix. Only report problems
you can see on the screens.
```

- **Toàn bộ câu trả lời của Claude:**

```
Phản biện UI cuối của Nốt — 9 phát hiện

1. [Cao] 6b3 (trạng thái "Chưa có giai đoạn" và "AI lỗi") — Nút cố định "Tiếp · xem lại"
   ở cuối màn đè lên nút "Thêm giai đoạn" và "Tự nhập tay". Hai nút này là lối ra khi AI
   lỗi, nhưng chỉ còn thấy một nửa và vùng chạm bị che.
   Tiêu chí: Nielsen #9 (giúp người dùng phục hồi lỗi); vùng chạm 48 × 48 dp.
   Sửa: đặt nội dung trong vùng cuộn có lề dưới bằng chiều cao vùng nút (≈ 88 dp), hoặc
   đưa "Thêm giai đoạn" lên ngay dưới danh sách.

2. [Cao] 5 (Deadline) — Nút + che chữ "Còn 30 ngày" của dòng cuối "Nộp paper hội nghị".
   Hạn nộp là thông tin chính của dòng. Lỗi này đã sửa ở vòng Stitch nhưng xuất hiện lại.
   Tiêu chí: Nielsen #1 (hiển thị trạng thái hệ thống).
   Sửa: thêm lề dưới 88 dp cho danh sách để dòng cuối cuộn lên trên nút +.

3. [Trung bình] 5e, 5o1, 5o2, 5o3 — Bốn màn kết quả dùng kiểu danh sách cũ: không có thẻ
   nhóm, hạn nộp là chữ thường thay vì Tag/Hạn nộp, "Còn 6 giờ" màu xanh thay vì cam,
   thiếu nhóm "Sắp tới". Người dùng thấy danh sách "đổi dạng" sau mỗi thao tác.
   Tiêu chí: Nielsen #4 (nhất quán và chuẩn).
   Sửa: dựng lại 4 màn từ instance của màn 5, chỉ thêm snackbar.

4. [Trung bình] 5e — Snackbar "Đã xoá deadline" có chữ "Hoàn tác" màu xanh đậm trên nền
   xanh primary, gần như không đọc được; đồng thời dialog Xoá vừa nói "Không hoàn tác
   được". Hai thông điệp mâu thuẫn.
   Tiêu chí: Nielsen #4; WCAG 1.4.3 (contrast).
   Sửa: chọn một hướng. Nếu cho hoàn tác thì sửa câu trong dialog và đổi chữ Hoàn tác sang
   màu on-primary; nếu không thì bỏ chữ Hoàn tác khỏi snackbar.

5. [Trung bình] 7b (Sửa deadline) và 7, 7s1, 7s2 (Lab 2) — Giai đoạn ở đây là một buổi có
   giờ (19:00–21:00) với nhắc "30 phút / 1 giờ" trước, trong khi 6b4 và 7s (Paper) dùng
   khoảng ngày và "nhắc mỗi ngày lúc 09:00". Một khái niệm có hai cách hiển thị và hai
   cách nhắc.
   Tiêu chí: Nielsen #4; persona Minh (giai đoạn thật kéo dài nhiều ngày).
   Sửa: cập nhật 7b và dữ liệu Lab 2 theo mô hình khoảng ngày + giờ nhắc mỗi ngày.

6. [Trung bình] 2, 2f, 4, 4b — Nhiều dòng nội dung dùng chữ 12–13 sp, ví dụ "Nộp Lab 2
   trước 23:59 để giữ chuỗi" (2), dòng môn và hạn trong thẻ (2f), "Sang T5 và T7 · Rất nặng
   → Nặng" (4), dòng hạn của việc (4b).
   Tiêu chí: yêu cầu chữ nội dung ≥ 14 sp; Minh đọc lướt khi đang di chuyển; Quốc Huy
   phóng to chữ.
   Sửa: đưa các dòng nội dung lên Label/14; giữ 12–13 sp cho nhãn tab, nhãn bước, số lịch.

7. [Thấp] 2 (Hôm nay) — Thẻ trong mục "Cần để ý" chỉ có tên việc ("Tiểu luận chương 3")
   và một icon xoay vòng, không nói vì sao cần để ý (đã dời 3 lần). Người mới như Bảo Ngọc
   phải đoán ý nghĩa icon.
   Tiêu chí: Nielsen #6 (nhận ra thay vì phải nhớ).
   Sửa: thêm dòng phụ "Đã dời 3 lần · chia nhỏ?" dưới tên việc.

8. [Thấp] 15b — Dialog "Đóng app để thử lỗi?" dùng kiểu kính mờ, nút chữ đỏ trên nền
   hồng, khác hẳn component Dialog dùng ở Xoá và Bỏ deadline.
   Tiêu chí: Nielsen #4; WCAG 1.4.3 (chữ nút trên nền nhạt trong suốt khó đạt 4.5:1).
   Sửa: thay bằng instance Dialog Type=Destructive.

9. [Thấp] 10 (Hồ sơ) — Biểu đồ đường "Tuần này" không có trục, đơn vị hay chú giải;
   người dùng không biết đường đo cái gì (số việc xong? giờ làm?).
   Tiêu chí: Nielsen #2 (khớp với thế giới thực); WCAG 1.1.1 nếu dựng thành ảnh.
   Sửa: thêm tiêu đề "Việc xong mỗi ngày" và số ở điểm cao nhất, hoặc thay bằng cột có số.

Không thấy lỗi ở: chỉ dùng màu cho trạng thái (Tag/Hạn nộp, lịch nhiệt đều có chữ hoặc
số), Back trên màn lồng, trạng thái rỗng / đang tải / lỗi của Deadline.
```

- **Bảng quyết định** (Claude đề xuất, Kim xác nhận khi commit):

| # | Màn hình | Phát hiện | Heuristic hoặc tiêu chí | Quyết định | Lý do | Thấy trong Figma ở |
|---|---|---|---|---|---|---|
| 1 | `6b3` | Nút cố định che nút "Thêm giai đoạn" và "Tự nhập tay" | Nielsen #9; vùng chạm 48 dp | Chấp nhận | Đây là lối ra duy nhất khi AI lỗi trong flow C1, flow quan trọng nhất của Minh | Cần sửa: `6b3 · Trạng thái — Chưa có giai đoạn`, `6b3 · Trạng thái — AI lỗi` |
| 2 | `5` | Nút + che hạn nộp của dòng cuối | Nielsen #1 | Chấp nhận | Hạn nộp là thông tin chính; lỗi đã sửa ở vòng Stitch thì không được để quay lại | Cần sửa: `5 · Deadline` |
| 3 | `5e`, `5o1`, `5o2`, `5o3` | Màn kết quả dùng kiểu danh sách cũ | Nielsen #4 | Chấp nhận | Rubric "Consistency": cùng một thành phần không được trông khác nhau giữa các màn | Cần sửa: 4 frame trên, dựng từ instance của `5` |
| 4 | `5e` | Snackbar "Hoàn tác" khó đọc và mâu thuẫn với dialog "Không hoàn tác được" | Nielsen #4; WCAG 1.4.3 | Chỉnh sửa | Giữ câu "Không hoàn tác được" trong dialog (xoá là thao tác phá huỷ, đã có xác nhận) và bỏ chữ Hoàn tác khỏi snackbar, thay vì làm thêm tính năng khôi phục | Cần sửa: `5e · Đã xoá deadline` |
| 5 | `7b`, `7`, `7s1`, `7s2` | Giai đoạn một buổi, nhắc "30 phút trước" khác mô hình khoảng ngày | Nielsen #4; persona Minh | Chỉnh sửa | Sửa `7b` theo `6b4` (từ ngày, đến ngày, giờ nhắc mỗi ngày). Giữ dữ liệu Lab 2 ở `7` vì một giai đoạn dài một buổi vẫn hợp lệ (từ ngày = đến ngày) | Cần sửa: `7b · Sửa deadline` |
| 6 | `2`, `2f`, `4`, `4b` | Chữ nội dung 12–13 sp | Yêu cầu chữ ≥ 14 sp | Chấp nhận | Yêu cầu bắt buộc của đề; trùng với mục "Chưa đạt" trong `design/design-decisions.md` | Cần sửa: các text dùng `Caption/12`, `Label/13` cho nội dung |
| 7 | `2` | Thẻ "Cần để ý" không nói lý do | Nielsen #6 | Chấp nhận | Bảo Ngọc là người mới; một dòng phụ không làm màn dày thêm | Cần sửa: `2 · Hôm nay` |
| 8 | `15b` | Dialog khác component Dialog | Nielsen #4 | Từ chối | Màn `15` chỉ là công cụ demo cho Lab 3 (Crashlytics), người dùng thật không thấy; ràng buộc thời gian, ưu tiên các màn trong flow chính | — |
| 9 | `10` | Biểu đồ "Tuần này" không có nhãn | Nielsen #2 | Chỉnh sửa | Thêm tiêu đề "Việc xong mỗi ngày", không đổi loại biểu đồ | Cần sửa: `10 · Hồ sơ` |

> Lý do hợp lệ phải nhắc tới persona, một heuristic, hoặc một ràng buộc (phạm vi, thời gian, nền tảng). Sau khi sửa trong Figma, đổi cột "Thấy trong Figma ở" từ "Cần sửa" thành tên frame đã sửa và xuất lại PNG vào `assets/figma/`.

---

## Đối chiếu tài liệu với Figma (20/10/2026)

- **Công cụ:** Claude (đọc Figma qua Figma connector, đọc repo GitHub).
- **Vấn đề:** tài liệu trong repo (bản 19/10) đánh số flow khác Figma (ví dụ C2, C3, P2–P6, S1–S2 khác page 01 và 06), thiếu flow C3, P4, P5, P6, S3, dùng mã màn không có trong Figma, ghi các tính năng không có trong Figma (OTP, chế độ Không làm phiền), và ghi token màu khác Variables.
- **Prompt nguyên văn (lần 1):**

```
Bạn hãy truy cập dự án hiện tại là là bản thiết kế figma hiện tại từ 00 - 06 https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=0-1&t=PzBuT0JfW3i7FggS-1
Và đây là link git hiện tại https://github.com/FU-PRM-Projects/prm393-lab2-group9.
Kiểm tra giúp tôi xem repo git đã cập nhật đúng hết nội dung , tính năng hiện tại của web chưa
```

- **Prompt nguyên văn (lần 2):**

```
https://www.figma.com/design/OkTRYkrsoJ0nkluNO4mrHz/PRM393-LAB2-Study-Planner?node-id=786-4&t=y1D6qia5KznSBaTf-1
Đọc toàn bộ các trang và thiết kế Figma từ 00 -> 06 
https://github.com/FU-PRM-Projects/prm393-lab2-group9
Truy cập và đọc xem git đã cập nhật các tài liệu đúng các flow chức năng hiện tại của app ở Figma chưa
```

- **Prompt nguyên văn (lần 3):**

```
Bây giờ bãy viết thêm cập nhật thêm vào đây giúp tôi nhé
```

- **Kết quả:** bảng so sánh 15 flow (2 khớp nội dung, 6 đúng một phần, 7 thiếu hoặc sai) và bản viết lại 7 file nêu ở bảng khai báo. Claude cũng tìm ra 5 chỗ page 04 ghi giá trị khác Variables, 604 lớp chữ dưới 14 sp, và các màu gán cứng trong component (ghi ở `design/design-decisions.md`).
- **Cách kiểm tra:** đọc lại từng file và so với Figma (tên flow ở page 06, tên frame ở page 03, Variables ở page 04).
- **Quyết định** (commit `7eb259e`, 20/10/2026):

| File hoặc đề xuất | Quyết định | Lý do |
|---|---|---|
| `ux/user-flow.md` viết lại theo 15 flow của page 01 và 06 | Chấp nhận | Ràng buộc của đề: file flow và Figma phải khớp, và rubric trừ điểm khi flow không ánh xạ sang màn. Bản cũ đánh số C2, C3, P2–P6, S1–S2 khác Figma và thiếu flow C3 (thông báo), là tính năng quan trọng nhất của Minh |
| `ux/persona.md` theo page 00 (Minh 22 tuổi, tiêu chí "< 60 giây") | Chấp nhận | Đề yêu cầu một tiêu chí thành công đo được; "< 60 giây tạo deadline 4 giai đoạn bằng AI" đo được bằng cách bấm giờ flow C1 |
| Bỏ OTP và chế độ Không làm phiền khỏi tài liệu | Chấp nhận | Hai tính năng này không có trong Figma. Ràng buộc Lab 3: app phải dựng đúng thiết kế, tài liệu ghi tính năng không có trong Figma sẽ thành khoảng trống trong handoff |
| `design/DESIGN.md` lấy màu theo Variables thay vì theo nhãn ở page 04 | Chấp nhận, kèm việc phải làm | Component dùng Variables nên đó là giá trị thật. Nhóm còn phải sửa nhãn ở page 04 cho khớp |
| `design/screen-spec.md` một dòng cho mỗi màn, dữ liệu mẫu chép từ Figma | Chấp nhận | Nielsen #4 (nhất quán): cùng một deadline phải có cùng tên, hạn, số giai đoạn trên mọi màn |
| `design/design-decisions.md` checklist ghi "Chưa đạt" ở cỡ chữ và token | Chấp nhận | Đề yêu cầu checklist có bằng chứng thật. Ghi "Đạt" khi số đo cho thấy 604 lớp chữ dưới 14 sp là không trung thực. Sẽ sửa trong Figma rồi cập nhật |
| Đề xuất đổi `success` sang màu đậm hơn | Chưa quyết, để nhóm chọn | WCAG 1.4.3: `#1F9D63` chỉ đạt 3.46:1. Cần xem lại các màn đang dùng màu này trước khi đổi |
| `handoff/flutter-handoff.md` đặc tả 6 mục cho từng màn | Chấp nhận | Rubric handoff: mỗi màn phải có đủ Layout, Components, States, Interactions, Navigation, Constraints; bản cũ chỉ viết theo nhóm màn |
| Các giá trị handoff tự đặt (giới hạn độ dài, tệp 20 MB, chờ AI 20 giây) | Chỉnh sửa: giữ, ghi rõ là giá trị của đặc tả | Không có trong Figma. Giữ để người dựng không phải hỏi lại; nếu đổi ở Lab 3 thì ghi vào `docs/handoff-gaps.md` |

---

## Đồng bộ tài liệu với bản "Nốt tích cực" (27/10/2026)

- **Công cụ:** Claude (đọc Figma qua Figma connector, đọc repo GitHub).
- **Vấn đề:** ngày 24/10 giảng viên yêu cầu đổi Nốt từ app quản lý deadline sang app ghi chú tích cực (5 ý). Figma đã có Final UI, prototype và kiểm tra accessibility mới, nhưng repo vẫn ở bản Study Planner (commit cuối `5f00bff`, 20/10): persona, 15 flow C1–S3, token `success` cũ `#1F9D63`, handoff cho 74 frame cũ.
- **Prompt nguyên văn (lần 1):**

```
Xem giúp tôi github đã cập nhật các phiên bản mới nhất hiện tại của lab 2 chưa nhỉ
```

- **Prompt nguyên văn (lần 2):**

```
Bạn làm dùm mình luôn đi
```

- **Kết quả:** viết lại 7 file (`README.md`, `ux/persona.md`, `ux/user-flow.md`, `design/DESIGN.md`, `design/screen-spec.md`, `design/design-decisions.md`, `handoff/flutter-handoff.md`) theo section `Final UI · Nốt tích cực (24/10)` ở page 03, page 04–05 (Variables, component mới) và bản persona / user flow 24/10.
- **Cách kiểm tra:** so tên frame ở page 03, tên component và Variables ở page 04–05 với từng file; kiểm tra mọi màn S01–S12 có trong bảng flow → màn.
- **Quyết định:**

| File hoặc đề xuất | Quyết định | Lý do |
|---|---|---|
| Viết lại persona, user flow theo bản 24/10 (Minh kiệt sức; F1–F3, P1–P8, T1–T3) | Chấp nhận | Ràng buộc: đề tài đã đổi theo yêu cầu giảng viên; rubric trừ điểm khi tài liệu và Figma khác nhau |
| Giữ tên biến `heat/*` nhưng đổi nghĩa thành tâm trạng | Chấp nhận | Ràng buộc thời gian: component lịch đã gắn biến này; đổi tên biến sẽ phải sửa lại mọi instance. Ghi rõ nghĩa mới trong `DESIGN.md` |
| Checklist accessibility ghi "Đạt" theo lần quét 24/10 | Chấp nhận | Có số đo thật (thấp nhất 4.56:1) và section kiểm tra 360 / 412 dp trên page 03 |
| Bo góc 14, 16, 32, 999 ghi "chưa có Variable" | Chấp nhận, kèm việc phải làm | Rubric "Design tokens": giá trị gán cứng bị trừ điểm; cần thêm biến `radius/*` trong Figma |
| Giá trị handoff tự đặt (giới hạn ký tự, Hoàn tác 5 giây, lỗi sau 10 giây) | Chỉnh sửa: giữ, ghi rõ là giá trị của đặc tả | Không có trong Figma nhưng người dựng cần để không phải hỏi lại |

> TODO: vòng lặp Stitch, 7 vòng sửa trên Figma (`assets/ai-iterations/`), phản biện AI theo heuristic (20/10) và ảnh `assets/stitch/` hiện vẫn thuộc bản Study Planner. Nếu giảng viên yêu cầu log theo bản mới, thêm vòng lặp và phản biện cho các màn S02, S03, S05.
