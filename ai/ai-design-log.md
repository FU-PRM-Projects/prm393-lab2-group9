# AI design log

> Đề có template ở Phụ lục A, nhưng phụ lục không có trong file đề mình nhận được. Hãy đối chiếu với template của giảng viên.
> Quy tắc: prompt phải ghi nguyên văn từng chữ. Nếu prompt dưới đây khác với prompt bạn đã gõ, hãy sửa lại cho đúng.

## Khai báo công cụ AI
| Công cụ | Mục đích |
|---|---|
| Google Stitch | Tạo UI |
| Claude | Phản biện UI, viết prompt sửa, vẽ mascot và họa tiết |

---

## 0. UI ban đầu (Stitch)
- **Prompt nguyên văn:** TODO
- **Ảnh kết quả:** TODO (lưu vào `assets/stitch/`)

---

## Vòng lặp 1 — Mật độ thông tin quá cao, tín hiệu khẩn cấp bị lặp

**Vấn đề:** mỗi dòng task có 7 thành phần, mức khẩn cấp hiển thị ba lần (header nhóm, chip màu, vòng checkbox). Heuristic: Nielsen #8, Aesthetic and minimalist design.

**Ảnh trước:** `assets/stitch/01-deadline-truoc.png`

**Prompt phản biện gửi Claude (nguyên văn):**
```
Cái này nhìn đang bị dày và khó chịu quá
```

**Phát hiện của Claude (màn Deadline):**
| # | Phát hiện | Quyết định | Lý do |
|---|---|---|---|
| 1 | Mức khẩn cấp lặp 3 lần: header nhóm, chip màu, vòng checkbox đỏ | TODO: chấp nhận / chỉnh sửa / từ chối | TODO |
| 2 | Tiến độ lặp 2 lần: chữ "2/3 buổi" và thanh progress | TODO | TODO |
| 3 | Số lượng lặp 2 lần: thẻ thống kê và số đếm ở header nhóm | TODO | TODO |
| 4 | Quá nhiều màu ngang hàng nhau | TODO | TODO |
| 5 | Dòng cao khoảng 44 dp, dưới mức vùng chạm 48 dp | TODO | TODO |
| 6 | Cờ outline và cờ đặc khó phân biệt | TODO | TODO |
| 7 | FAB che chip của dòng cuối và cùng màu với tab đang chọn | TODO | TODO |

TODO: dán toàn bộ câu trả lời của Claude vào đây (đề yêu cầu giữ toàn bộ câu trả lời).

**Prompt gửi Stitch (kiểm tra lại cho đúng nguyên văn):**
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

**Ảnh sau:** `assets/stitch/02-deadline-va-rong-sau-vong-1.png`

**Lỗi còn lại sau vòng 1:** FAB che thời hạn của dòng cuối; tab cuối ghi "Ca làm" ở một màn và "Lịch bận" ở màn kia; màn rỗng có hai nút cùng việc; câu mô tả màn rỗng bị viết lại.

**Prompt sửa (TODO: chạy, rồi lưu ảnh `03-...png`):**
```
Fix these issues. Do not change anything else.
- Deadline screen: add 88dp bottom padding to the list so the FAB does
  not cover the due text of the last row.
- Bottom navigation: the fourth tab label is "Lịch bận" on every screen.
- Empty state screen: remove the FAB. Keep only the "Thêm deadline" button.
- Empty state body text: "Thêm deadline đầu tiên. Nốt sẽ thức dậy và
  nhắc bạn trước hạn."
```

---

## Vòng lặp 2 — TODO: tên vấn đề (phải khác vòng 1)
- **Vấn đề và heuristic:** TODO
- **Ảnh trước:** TODO
- **Prompt nguyên văn:** TODO
- **Ảnh sau:** TODO
- **Quyết định và lý do:** TODO

## Vòng lặp 3 — TODO: tên vấn đề (phải khác vòng 1 và 2)
- **Vấn đề và heuristic:** TODO
- **Ảnh trước:** TODO
- **Prompt nguyên văn:** TODO
- **Ảnh sau:** TODO
- **Quyết định và lý do:** TODO

---

## Phản biện bằng AI theo 10 heuristic của Nielsen
Yêu cầu: ít nhất 5 phát hiện gắn với các màn hình cụ thể, xét cả accessibility và persona.
- **Prompt nguyên văn:** TODO
- **Toàn bộ câu trả lời:** TODO
- **Bảng quyết định (chấp nhận / chỉnh sửa / từ chối + lý do):** TODO
