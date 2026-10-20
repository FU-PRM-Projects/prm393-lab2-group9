# DESIGN.md — Nốt (Study Planner)

Bản mô tả thiết kế hiện tại của app Nốt: màu, chữ, khoảng cách, bo góc, elevation, tone và quy tắc component. Nguồn là **Figma Variables, Text Styles và Effect Styles** trong file `PRM393-LAB2-Study-Planner` (page `04 Design System` và `05 Components`), đọc lại ngày 20/10/2026.

> **Bản đưa cho Stitch:** bản brief gốc đã tải lên Google Stitch ngày 06/10/2026 (khi app còn tên "Khe") được giữ nguyên văn ở [`ai/stitch-source/DESIGN-v0-Khe.md`](../ai/stitch-source/DESIGN-v0-Khe.md). File này là bản đã cập nhật theo các vòng lặp và theo Figma hiện tại.

---

## 1. Tóm tắt sản phẩm

| Mục | Nội dung |
|---|---|
| Tên app | **Nốt**. Mascot là "Tụi Nốt": các tờ giấy ghi chú có khuôn mặt |
| Người dùng | Persona chính **Minh**: sinh viên năm cuối, trưởng nhóm nghiên cứu khoa học 4 người, đi làm thêm, đang dùng cùng lúc Calendar, Notion, ClickUp, Linear. Persona phụ: Đăng Khoa (năm 2, làm ca tối), Bảo Ngọc (năm 1, lần đầu dùng app). Persona hỗ trợ: Quốc Huy (lập trình viên đi làm) |
| Vấn đề | Deadline và tài liệu nằm rải rác nhiều app; deadline dài dễ lỡ mốc giữa chừng; không thấy ngày nào quá nặng |
| Việc app làm | Gom deadline theo môn hoặc dự án. Chia một deadline thành giai đoạn phủ kín số ngày tới hạn (AI gợi ý từ mô tả, hoặc tự nhập). Nhắc mỗi ngày theo giai đoạn; thông báo mở thẳng giai đoạn. Ghi chép và tệp theo giai đoạn. Lịch nhiệt theo độ nặng, gợi ý dời việc sang ngày nhẹ hơn trước hạn |
| Nền tảng | Android, điện thoại, khung thiết kế 360 × 800 dp, kiểm tra thêm ở 412 dp. Material 3, light theme |
| Ngôn ngữ | Tiếng Việt, giờ 24 giờ, ngày dạng "T6 16/10" |

---

## 2. Nguyên tắc thiết kế

1. **Mỗi màn một câu hỏi, một hành động chính.** Hôm nay: "Hôm nay làm gì trước?" Kế hoạch: "Ngày nào quá nặng?" Deadline: "Việc nào gấp nhất?" Chi tiết giai đoạn: "Hôm nay làm gì cho giai đoạn này, tài liệu ở đâu?"
2. **Nút chính ở nửa dưới màn hình.** Nút chính cố định cuối màn, nút + và thanh điều hướng nằm trong vùng ngón cái.
3. **Chia việc lớn thành giai đoạn.** Một deadline dài được chia thành giai đoạn có từ ngày, đến ngày và giờ nhắc. App cho biết đã chia bao nhiêu ngày ("Đã chia 31/31 ngày").
4. **AI gợi ý, người dùng quyết định.** AI chỉ đề xuất giai đoạn từ mô tả; người dùng sửa, xoá, tạo lại, hoặc tự nhập. Khi AI lỗi, dữ liệu đã nhập vẫn được giữ.
5. **Không dùng màu làm tín hiệu duy nhất.** Màu đi kèm chữ, số hoặc icon (WCAG 1.4.1).
6. **Hoàn tác được.** Dời việc có Hoàn tác. Thao tác không hoàn tác được (Xoá, Bỏ deadline) phải qua dialog xác nhận.

---

## 3. Màu

Mọi màu là Figma Variable trong collection **Color** (mode Light). Component dùng biến, không dùng mã màu gán cứng.

### 3.1 Màu vai trò

| Variable | Giá trị (Variable) | Dùng cho |
|---|---|---|
| `primary` | `#3D4FD6` | Hành động chính, tab đang chọn, nút + |
| `on-primary` | `#FFFFFF` | Chữ và icon trên `primary` |
| `primary-container` | `#DCE6FF` | Nền tonal của tab đang chọn, avatar |
| `on-primary-container` | `#2F3FB8` | Chữ trên `primary-container`, nút viền |
| `primary-dark` | `#2B399F` | Huy hiệu trên nền `primary` |
| `surface` | `#FFFFFF` | Nền |
| `surface-card` | `#F6F7FB` | Nền thẻ |
| `surface-variant` | `#E7E9F3` | Segmented, skeleton, ngày trống |
| `surface-container` | `#E7E9F3` | Nền khối phụ |
| `outline` | `#7A8094` | Viền ô nhập, checkbox |
| `outline-variant` | `#E3E5EE` | Đường kẻ mảnh |
| `switch-off` | `#C3C7D4` | Công tắc đang tắt |
| `on-surface` | `#1B1D2A` | Chữ chính |
| `on-surface-variant` | `#555B6E` | Chữ phụ |
| `on-surface-muted` | `#3A3F52` | Chữ phụ trên nền màu |
| `error` | `#B3261E` | Quá hạn, lỗi |
| `warning` | `#A84F00` | Đến hạn hôm nay |
| `success` | `#1F9D63` | Việc đã xong (chỉ dùng cho icon, chữ lớn hoặc chữ trên nền nhạt có kiểm tra contrast) |

> **Cần thống nhất trong Figma:** nhãn chữ trên các ô màu ở page 04 chưa khớp với Variables ở 5 chỗ: `primary-container` (nhãn ghi `#DDE1FF`), `surface` và `surface-card` (nhãn ghi ngược: `#F6F7FB` và `#FFFFFF`), `success` (Variable `#1F9D63`; bản cũ `#1B6B44`), `tint/yellow` (nhãn ghi `#FFF4CC`, Variable `#EEF2FE`). Bảng trên lấy theo Variables vì component dùng Variables. Nhóm cần chọn một giá trị và sửa bên còn lại.

### 3.2 Màu nhiệt (độ nặng của ngày)

| Variable | Giá trị | Nhãn ở `12 · Ý nghĩa icon` | Tổng độ nặng của ngày |
|---|---|---|---|
| (trống) | `surface-variant` `#E7E9F3` | Chưa có việc | 0 |
| `heat/1` | `#A9DCF5` | Rất nhẹ | 1 |
| `heat/2` | `#7FD9B3` | Nhẹ | 2–3 |
| `heat/3` | `#FFD24A` | Vừa | 4–5 |
| `heat/4` | `#FF9A3D` | Nặng | 6–7 |
| `heat/5` | `#F0524B` | Rất nặng | 8+ |

**Cách tính:** mỗi loại việc có độ nặng (component `WeightDots`: Nhẹ 1, Vừa 2, Nặng 3). Theo màn `12`: Quiz nhẹ; Lab, Tiểu luận, Thuyết trình vừa; Báo cáo, Đồ án nặng. Độ nặng các việc trong một ngày cộng lại thành màu của ngày. Ngày có tổng trên 5 là ngày quá nặng; app gợi ý dời sang ngày nhẹ trước hạn nộp.

> **Cần thống nhất:** ghi chú ở page 04 nói "Lab, Quiz = vừa; Báo cáo, Tiểu luận = nặng", khác màn `12`. Tài liệu này theo màn `12` vì người dùng thấy màn đó.

Ô ngày luôn có số (tổng độ nặng) và khuôn mặt mascot, nên không dựa vào màu.

### 3.3 Nền nhạt (tint)

| Variable | Giá trị | Dùng cho |
|---|---|---|
| `tint/blue` | `#E3F3FB` | Thông báo Sắp đến giờ, nền mascot Thong Thả |
| `tint/orange` | `#FFEBD6` | Loại Báo cáo, thẻ hạn hôm nay, thông báo Hạn hôm nay |
| `tint/red` | `#FDE1DF` | Loại Thuyết trình, thẻ quá tải, thông báo Quá hạn |
| `tint/green` | `#DDF5EA` | Loại Lab, thông báo Hoàn thành |
| `tint/violet` | `#ECEBFC` | Loại Đồ án, thông báo Gợi ý dời |
| `tint/yellow` | `#EEF2FE` | Loại Quiz |
| `tint/indigo` | `#E4E7FF` | Loại Tiểu luận, giờ bận |
| `tint/gray` | `#ECEEF3` | Nền trạng thái lỗi |
| `tint/lavender` | `#EEF0FE` | Nền trạng thái rỗng |
| `mono/1` … `mono/5` | `#DFE3FD`, `#C0C8F8`, `#9EA9F3`, `#7A88EA`, alias | Thang một màu cho biểu đồ nhỏ |

### 3.4 Contrast (WCAG 2.x, số ghi ở page 04)

| Cặp màu | Tỉ lệ | Ngưỡng | Kết quả |
|---|---|---|---|
| `on-surface` trên nền sáng | 15.6:1 | 4.5:1 | Đạt |
| `on-surface-variant` trên nền sáng | 6.3:1 | 4.5:1 | Đạt |
| `on-surface-muted` trên nền sáng | 9.7:1 | 4.5:1 | Đạt |
| `on-primary` trên `primary` | 6.4:1 | 4.5:1 | Đạt |
| `error` trên nền sáng | 6.1:1 | 4.5:1 | Đạt |
| `warning` trên nền sáng | 5.2:1 | 4.5:1 | Đạt |
| `success` trên nền sáng | 3.2:1 | 4.5:1 chữ thường; 3:1 chữ lớn và icon | **Chỉ đạt cho chữ lớn và icon**. Không dùng cho chữ nội dung 14–16 sp |
| Chữ `on-surface` trên `heat/1` … `heat/5` | 4.8:1 – 11.6:1 | 4.5:1 | Đạt |

---

## 4. Chữ

Font **Be Vietnam Pro**. Chữ nội dung tối thiểu 14 sp. Mỗi kiểu chữ là một Text Style trong Figma.

| Text Style | Cỡ · độ đậm | Line height | Dùng cho |
|---|---|---|---|
| `Display/44 Bold`, `Display/36 Bold` | 44, 36 · Bold | 125% | Màn đăng nhập, màn chúc mừng |
| `Headline/28 Bold` | 28 · Bold | 125% | Tiêu đề màn gốc của tab |
| `Title/24 Bold` | 24 · Bold | 125% | Tiêu đề màn lồng |
| `Headline/22 Bold` | 22 · Bold | 125% | Tiêu đề dialog, tiêu đề bước |
| `Title/20 Bold`, `Title/18 Bold` | 20, 18 · Bold | 125%, 140% | Tiêu đề thẻ lớn, tiêu đề nhóm |
| `Title/17 Bold`, `Title/17 SemiBold` | 17 · Bold, SemiBold | 140% | Tên deadline, tên giai đoạn |
| `Body/17 Regular` | 17 · Regular | 140% | Nội dung dài |
| `Body/16 Regular`, `SemiBold`, `Bold` | 16 | 140% | Nội dung chính, chữ trong ô nhập, chữ nút |
| `Body/15 Regular`, `SemiBold` | 15 | 140% | Dòng việc, dòng thông báo |
| `Label/14 Regular`, `Medium`, `SemiBold`, `Bold` | 14 | 140% | Dòng phụ (mã môn, hạn), chip, nhãn ô nhập |
| `Label/13 Regular`, `SemiBold` | 13 | 140% | Chỉ cho nhãn ngắn không phải nội dung (ví dụ ngày trên lịch) |
| `Caption/12 Regular`, `SemiBold`, `Bold`; `Overline/12 Bold` | 12 | 140% | Nhãn tab, chú thích, nhãn "BƯỚC 1/5". Không dùng cho nội dung |

Giờ và ngày dùng số có độ rộng đều để thẳng cột.

---

## 5. Khoảng cách, bo góc, elevation

### 5.1 Khoảng cách (collection **Size**)

`space/2` 2 · `space/4` 4 · `space/6` 6 · `space/8` 8 · `space/10` 10 · `space/12` 12 · `space/14` 14 · `space/16` 16 · `space/20` 20 · `space/24` 24 (dp).

- Lề trái phải của màn hình: **16 dp**.
- Vùng chạm tối thiểu: **48 × 48 dp**.

### 5.2 Bo góc

Variables: `radius/4` 4 · `radius/6` 6 · `radius/8` 8 · `radius/12` 12 (dp).

Quy ước ghi ở page 04: thẻ bo 20, nút lớn 16, nút nhỏ và ô loại việc 12–14.

> **Cần thống nhất:** các giá trị 14, 16, 20 chưa có Variable. Cần thêm `radius/16` và `radius/20` (và `radius/14` nếu giữ) vào collection Size, rồi gắn vào component, để không còn giá trị gán cứng.

### 5.3 Elevation (Effect Styles)

| Effect Style | Giá trị | Dùng cho |
|---|---|---|
| `Elevation/0 Flat` | Không đổ bóng | Thẻ, thanh điều hướng (tách bằng màu nền) |
| `Elevation/2 FAB` | Drop shadow, blur 16, y 6, độ mờ 22% | Nút + thêm deadline |

Dialog và bottom sheet dùng lớp nền tối phía sau (scrim), không cần thêm mức elevation.

---

## 6. Tone và ngôn ngữ

- Giọng thân thiện, ngắn, như một người bạn nhắc việc. Xưng "bạn", app tự gọi là "Nốt" ("Nốt gợi ý 3 bước…", "Nốt sẽ nhắc bạn trước hạn").
- Không dùng thuật ngữ khó cho người mới (không "sprint", "backlog"). Dùng "giai đoạn", "bước", "dời việc", "giãn việc".
- Nút ghi động từ cụ thể: "Tiếp · nhập deadline", "Dùng 4 giai đoạn · xem lại", "Lưu và bật nhắc", "Hoàn thành deadline", "Dời 2 việc".
- Thông báo lỗi nói nguyên nhân và cách sửa: "Mất kết nối khi gọi AI. Mô tả của bạn vẫn được giữ." · "Sai email hoặc mật khẩu." · "Chưa có ngày đủ nhẹ để dời".
- Thời gian tương đối khi gần ("Vừa xong", "15 phút", "Còn 6 giờ"), ngày tháng khi xa ("16/10").

---

## 7. Quy tắc component

Mọi component ở page 05 dựng bằng Auto Layout, có variant, dùng Variables cho màu và khoảng cách.

| Component | Variant | Quy tắc dùng |
|---|---|---|
| `Button` | Style: Filled, Tonal, Outlined, Text, Destructive × State: Default, Pressed, Disabled, Loading | Mỗi màn chỉ một nút Filled. Destructive chỉ trong dialog Xoá, Bỏ. Loading giữ nguyên bề rộng nút |
| `Text field` | Default, Focused, Filled, Error, Disabled | Lỗi hiện dưới ô, màu `error`, kèm chữ nguyên nhân |
| `PasswordField` | Hidden, Shown | Nút "Hiện" để xem mật khẩu |
| `Card` | Type: Task, Summary × State: Default, Pressed | Cả thẻ là vùng chạm |
| `BottomNav/iPhone · 4 tab` | Active: Hôm nay, Kế hoạch, Deadline, Hồ sơ | Chỉ hiện ở 4 màn gốc |
| `App bar` | Default, With actions | Màn lồng có nút Back |
| `Dialog` | Confirmation, Destructive | Nút huỷ bên trái, nút chính bên phải |
| `Loading state` | Skeleton list, Spinner | Skeleton cho danh sách, spinner cho thao tác ngắn |
| `Empty state` | Context: Deadline, Hôm nay | Mascot, một câu, một nút |
| `Error state` | Type: Offline, Load failed | Mascot Lạc, nguyên nhân, nút Thử lại |
| `Stepper/Thêm deadline` | Step 1–5 | Nhãn "BƯỚC n/5 · TÊN BƯỚC" ở đầu các màn `6`–`6b5` |
| `Tag/Hạn nộp` | Level: Hôm nay, Quá hạn, Sắp tới, Đã nộp | Màu nền đặc theo mức, luôn có chữ ("Trễ 1 ngày", "Còn 6 giờ") |
| `Notification/Row` | Type: Sắp đến giờ, Hạn hôm nay, Gợi ý dời, Hoàn thành, Quá hạn × State: Chưa đọc, Đã đọc | Mỗi loại một cặp tint + màu đậm và một icon. Chưa đọc: chữ đậm, giờ màu `primary`, có chấm |
| `File/Đính kèm` | Type: PDF, DOCX, XLSX, PPTX, ZIP, Ảnh, Link, Đang tải lên | Icon và màu theo loại tệp; Đang tải lên có thanh tiến độ |
| `WeightDots` | Level 1–3 | Độ nặng loại việc |
| `ChipGroup · Môn học`, `OptionGroup · Loại việc`, `SwatchGroup · Màu` | Selected 1–6 | Chọn một trong nhóm |
| `Switch` | On, Off | Màu tắt là `switch-off` |
| `Mascot`, `MascotMini`, `MascotAnim` | 8 trạng thái; MascotMini theo mức hạn | Xem mục 9 |
| `Icon/*` | 19 icon | Back, Close, Plus, Pencil, Filter, Check, Refresh, Right, Bell, Logout, Minus, Clock, Phase, Link, Image, Calendar, File, Upload, More |

---

## 8. Thông báo đẩy

Thẻ thông báo trên màn khoá (`13p`): tên app "NỐT · Nhắc giai đoạn", thời gian, tiêu đề "Tới giờ làm: Chạy thực nghiệm", dòng phụ "Paper · ngày 3/7 · 20:00 mỗi ngày", hai nút: **Mở giai đoạn** và **Nhắc lại 15 phút**.

---

## 9. Mascot Tụi Nốt

8 trạng thái (component `Mascot`): Thong Thả, Vội, Cháy, Xong, Ngủ, Đợi, Lạc, Tập Trung. File SVG gốc ở `assets/mascot/`.

| Mascot | Dùng ở (theo instance ở page 03) |
|---|---|
| Nốt Tập Trung | `1 · Đăng nhập`, `2 · Hôm nay` |
| Nốt Thong Thả | `1`, `7c` (deadline vừa tạo) |
| Nốt Vội | `7`, `7d` (deadline sắp đến hạn) |
| Nốt Cháy | Ngày quá nặng ở `4`, `4d`; nhóm Quá hạn ở `5` |
| Nốt Xong | `8 · Đã nộp`, `10`, `10e`, giai đoạn đã xong `7s1`, `7s2`, `11` |
| Nốt Ngủ, Nốt Đợi | Trạng thái Rỗng, Đang tải; trạng thái chưa có giai đoạn và AI đang chia ở `6b3` |
| Nốt Lạc | Trạng thái Lỗi mất mạng, AI lỗi ở `6b3`, `7o`, `15` |
| `MascotMini` (Quá hạn, Hôm nay, Tuần này, Sắp tới) | Tiêu đề từng nhóm ở `5` |

Màn `12 · Ý nghĩa icon` giải thích ý nghĩa từng khuôn mặt.

Mascot không đặt trong dòng việc để không làm rối danh sách.

---

## 10. Ràng buộc

- Khung thiết kế 360 × 800 dp; kiểm tra ở 412 dp. Nội dung dài cuộn dọc; App bar, nút chính cuối màn và thanh điều hướng đứng yên.
- Vùng chạm ≥ 48 × 48 dp. Chữ nội dung ≥ 14 sp.
- Chữ dài xuống dòng (tối đa 2 dòng ở tiêu đề thẻ), không cắt mất thông tin hạn nộp.
- Không dùng màu làm tín hiệu duy nhất.

## 11. Không làm

- Không có dark theme trong Lab 2.
- Không có chat, mạng xã hội, hay đồng bộ tin nhắn Zalo, Slack.
- Không thiết kế màn cho máy tính bảng (mô tả hành vi màn rộng ở `handoff/flutter-handoff.md`).
