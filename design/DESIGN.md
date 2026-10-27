# DESIGN.md — Nốt (app ghi chú tích cực)

Bản mô tả thiết kế hiện tại của app Nốt: màu, chữ, khoảng cách, bo góc, elevation, tone và quy tắc component. Nguồn là **Figma Variables, Text Styles và Effect Styles** trong file `PRM393-LAB2-Study-Planner` (page `04 Design System` và `05 Components`), đọc lại ngày 27/10/2026.

> **Bản đưa cho Stitch:** bản brief gốc đã tải lên Google Stitch ngày 06/10/2026 (khi app còn tên "Khe", đề tài Study Planner) được giữ nguyên văn ở [`ai/stitch-source/DESIGN-v0-Khe.md`](../ai/stitch-source/DESIGN-v0-Khe.md).
>
> **Đổi hướng 24/10/2026:** theo góp ý giảng viên, Nốt chuyển từ app quản lý deadline sang app ghi chú tích cực. Bảng màu, font, khoảng cách và mascot giữ nguyên; thang màu `heat/*` đổi nghĩa từ "độ nặng của ngày" sang "tâm trạng / năng lượng của ngày"; thêm component cho nốt, tâm trạng, chip chiến thắng, lịch năng lượng.

---

## 1. Tóm tắt sản phẩm

| Mục | Nội dung |
|---|---|
| Tên app | **Nốt**. Mascot là "Tụi Nốt": các tờ giấy ghi chú có khuôn mặt |
| Người dùng | Persona chính **Minh**: 22 tuổi, sinh viên năm cuối, trưởng nhóm nghiên cứu, đi làm thêm, kiệt sức, hay lướt điện thoại đến 1–2h sáng. Persona phụ: **Quốc Huy** (27, đi làm, tối tự học), **Bảo Ngọc** (18, năm nhất, ngại nói chuyện) |
| Vấn đề | Cuối ngày chỉ nhớ việc chưa xong nên thấy thất bại và mất động lực |
| Việc app làm | Mỗi tối ghi 1 chiến thắng nhỏ (dưới 30 giây) vào "hũ chiến thắng". Gom 5 ý vào một vòng lặp: chiến thắng nhỏ, nhật ký, tự chủ trước "dopamine rẻ", nói chuyện với người lạ, vận động. Lịch năng lượng theo tâm trạng; ngày tệ app lấy ra một nốt cũ |
| Nền tảng | Android, điện thoại, khung thiết kế 360 × 800 dp, kiểm tra thêm ở 412 dp. Material 3, light theme |
| Ngôn ngữ | Tiếng Việt, giờ 24 giờ, ngày dạng "Thứ Bảy, 24/10" |

---

## 2. Nguyên tắc thiết kế

1. **Mỗi màn một hình lớn, một hành động chính.** Không chồng nhiều thẻ; dùng lưới tờ nốt thay cho danh sách dòng. Hôm nay: "Hôm nay bạn làm được gì?" → nút "Ghi nốt".
2. **Nút chính ở nửa dưới màn hình.** Minh dùng một tay lúc nằm trên giường; nút chính và thanh tab trong vùng ngón cái.
3. **Không phạt.** Đếm số nốt và số lần tự chủ, không đếm chuỗi bị đứt về 0. Thử thách "để mai" không bị trừ gì. Lỡ lướt quá đà vẫn được ghi nhận "Nhận ra cũng là bắt đầu tự chủ".
4. **Ngày mệt chỉ cần chạm.** Chip chiến thắng có sẵn; bước nhật ký có thể bỏ qua.
5. **Riêng tư là tính năng chính.** Danh sách "Thói quen muốn bớt" ở `S09` khoá bằng PIN / sinh trắc học (nút "Mình vừa dừng lại" vẫn dùng ngay); thông báo có thể ẩn nội dung trên màn khoá.
6. **Không dùng màu làm tín hiệu duy nhất.** Tâm trạng luôn có màu + khuôn mặt mascot + chữ (WCAG 1.4.1).
7. **Hoàn tác được.** Xoá nốt có dialog xác nhận và Hoàn tác 5 giây; thoát giữa chừng được giữ nháp.

---

## 3. Màu

Mọi màu là Figma Variable trong collection **Color** (mode Light). Component dùng biến, không dùng mã màu gán cứng.

### 3.1 Màu vai trò

| Variable | Giá trị | Dùng cho |
|---|---|---|
| `primary` | `#3D4FD6` | Hành động chính, tab đang chọn, chip đang chọn |
| `on-primary` | `#FFFFFF` | Chữ và icon trên `primary` |
| `primary-container` | `#DCE6FF` | Ô tâm trạng đang chọn, nền tonal |
| `on-primary-container` | `#2F3FB8` | Chữ trên `primary-container`, nút viền |
| `primary-dark` | `#2B399F` | Huy hiệu trên nền `primary` |
| `surface` | `#FFFFFF` | Nền màn hình, thanh tab |
| `surface-card` | `#F6F7FB` | Nền thẻ, ô tâm trạng, chip chưa chọn |
| `surface-variant` | `#E7E9F3` | Thẻ đang nhấn, skeleton, ngày chưa ghi |
| `surface-container` | `#E7E9F3` | Nền khối phụ |
| `outline` | `#7A8094` | Viền ô nhập |
| `outline-variant` | `#E3E5EE` | Đường kẻ mảnh |
| `switch-off` | `#C3C7D4` | Công tắc đang tắt |
| `on-surface` | `#1B1D2A` | Chữ chính |
| `on-surface-variant` | `#555B6E` | Chữ phụ, ngày khác tháng |
| `on-surface-muted` | `#3A3F52` | Chữ phụ trên nền màu |
| `error` | `#B3261E` | Lỗi, nút Xoá |
| `warning` | `#A84F00` | Cảnh báo nhẹ |
| `success` | `#187A4D` | Xác nhận đã lưu, tick (đổi từ `#1F9D63` ngày 24/10 để đạt 4.5:1) |

### 3.2 Màu tâm trạng (lịch năng lượng)

Biến vẫn tên `heat/1` … `heat/5` để không phá các component cũ; nghĩa mới là tâm trạng người dùng chọn ở bước 1 của `S03`. Thang đi từ lạnh (vui, nhẹ nhàng) sang ấm (rối, cần quan tâm).

| Tâm trạng | Variable | Giá trị | Mặt mascot | Chữ số ngày trên ô |
|---|---|---|---|---|
| Vui | `heat/1` | `#A9DCF5` | Nốt Xong | `on-surface` |
| Ổn | `heat/2` | `#7FD9B3` | Nốt Thong Thả | `on-surface` |
| Bình thường | `heat/3` | `#FFD24A` | Nốt Đợi | `on-surface` |
| Mệt | `heat/4` | `#FF9A3D` | Nốt Ngủ | `on-surface` |
| Rối | `heat/5` | `#F0524B` | Nốt Lạc | `on-surface` (mặt vẽ màu `on-primary`) |
| Chưa ghi | `surface-variant` | `#E7E9F3` | — | `on-surface` |
| Ngày khác tháng | (không nền) | — | — | `on-surface-variant` |

Thang 1–5 ở `S11b` (Năng lượng mỗi ngày): Vui = 5, Ổn = 4, Bình thường = 3, Mệt = 2, Rối = 1.

### 3.3 Màu loại nốt (nền nhạt)

| Loại nốt | Variable | Giá trị |
|---|---|---|
| Chiến thắng | `tint/orange` | `#FFEBD6` |
| Tự chủ | `tint/violet` | `#ECEBFC` |
| Thử thách (gồm người lạ, vận động) | `tint/green` | `#DDF5EA` |
| Nhật ký | `tint/blue` | `#E3F3FB` |

Các tint khác vẫn có trong file: `tint/red` `#FDE1DF`, `tint/yellow` `#EEF2FE`, `tint/indigo` `#E4E7FF`, `tint/gray` `#ECEEF3` (nền trạng thái lỗi), `tint/lavender` `#EEF0FE` (nền trạng thái rỗng); `mono/1` … `mono/5` (`#DFE3FD`, `#C0C8F8`, `#9EA9F3`, `#7A88EA`, alias `primary`) cho biểu đồ ở `S11b`.

Loại nốt luôn có nhãn chữ trên tờ nốt ("Chiến thắng", "Tự chủ"…), nên màu không phải tín hiệu duy nhất.

### 3.4 Contrast (WCAG 2.x)

Kết quả quét tự động ngày 24/10 trên page 03 (28 màn, 444 lớp chữ): tỉ lệ thấp nhất là **4.56:1**. Chi tiết ở [`design-decisions.md`](design-decisions.md#2-checklist-accessibility-và-responsive).

| Cặp màu | Tỉ lệ | Kết quả |
|---|---|---|
| `on-surface` trên `surface` | 15.6:1 | Đạt |
| `on-surface-variant` trên `surface-card` | 6.3:1 | Đạt |
| `on-primary` trên `primary` | 6.4:1 | Đạt |
| `success` `#187A4D` trên trắng / trên nền xanh nhạt | 5.31:1 / 4.63:1 | Đạt |
| `on-surface` trên `heat/1` … `heat/5` | ≥ 4.8:1 | Đạt (ô "Rối" đã đổi chữ trắng → `on-surface`) |

---

## 4. Chữ

Font **Be Vietnam Pro**. Chữ nội dung tối thiểu 14 sp (nội dung chính dùng 15–16 sp). Mỗi kiểu chữ là một Text Style trong Figma.

| Text Style | Cỡ · độ đậm | Line height | Dùng cho |
|---|---|---|---|
| `Display/44 Bold`, `Display/36 Bold` | 44, 36 · Bold | 125% | Tên app ở `S01`, số lớn (số nốt, số lần tự chủ), "Đã vào hũ!" |
| `Headline/28 Bold` | 28 · Bold | 125% | Tiêu đề màn gốc của tab, câu hỏi chính ("Hôm nay bạn làm được gì?") |
| `Title/24 Bold` | 24 · Bold | 125% | Tiêu đề màn lồng, tên thử thách |
| `Headline/22 Bold` | 22 · Bold | 125% | Tiêu đề dialog |
| `Title/20 Bold`, `Title/18 Bold` | 20, 18 · Bold | 125%, 140% | Tiêu đề khối, tiêu đề thẻ lớn |
| `Title/17 Bold`, `Title/17 SemiBold` | 17 | 140% | Tiêu đề tờ nốt |
| `Body/17 Regular` | 17 | 140% | Nội dung nhật ký dài |
| `Body/16 Regular`, `SemiBold`, `Bold` | 16 | 140% | Nội dung chính, chữ trong ô nhập, chữ nút |
| `Body/15 Regular`, `SemiBold` | 15 | 140% | Nội dung phụ, chip |
| `Label/14 Regular`, `Medium`, `SemiBold`, `Bold` | 14 | 140% | Dòng phụ, nhãn ô nhập, nhãn loại nốt |
| `Label/13 Regular`, `SemiBold` | 13 | 140% | Nhãn ngắn không phải nội dung (ngày trên tờ nốt) |
| `Caption/12 Regular`, `SemiBold`, `Bold`; `Overline/12 Bold` | 12 | 140% | Nhãn tab, chú thích, "BƯỚC 1/3", số ngày trên lịch. Không dùng cho nội dung |

---

## 5. Khoảng cách, bo góc, elevation

### 5.1 Khoảng cách (collection **Size**)

`space/2` 2 · `space/4` 4 · `space/6` 6 · `space/8` 8 · `space/10` 10 · `space/12` 12 · `space/14` 14 · `space/16` 16 · `space/20` 20 · `space/24` 24 (dp).

- Lề trái phải của màn hình: **16 dp**. Khoảng cách giữa các tờ nốt trong lưới: **12 dp**.
- Vùng chạm tối thiểu: **48 × 48 dp**.

### 5.2 Bo góc

| Dùng ở | Giá trị | Variable |
|---|---|---|
| Ô nhập, nút nhỏ | 8–12 | `radius/8`, `radius/12` |
| Tờ nốt (`Note/Tờ nốt`) | 14 | chưa có |
| Thẻ nốt, ô tâm trạng, nút lớn | 16 | chưa có |
| Thanh tab nổi (`BottomNav · Nốt`) | 32 | chưa có |
| Chip | tròn hẳn (999) | chưa có |

> **Cần thống nhất trong Figma:** collection Size mới có `radius/4`, `6`, `8`, `12`. Thêm `radius/14`, `radius/16`, `radius/32`, `radius/full` rồi gắn vào các component trên để không còn giá trị gán cứng.

### 5.3 Elevation (Effect Styles)

| Effect Style | Giá trị | Dùng cho |
|---|---|---|
| `Elevation/0 Flat` | Không đổ bóng | Thẻ, tờ nốt (tách bằng màu nền) |
| `Elevation/2 FAB` | Drop shadow, blur 16, y 6, độ mờ 22% | Thanh tab nổi, nút "Ghi nốt" |

Dialog dùng lớp nền tối phía sau (scrim), không cần thêm mức elevation.

---

## 6. Tone và ngôn ngữ

- Giọng một người bạn ấm áp, ngắn gọn. Xưng "bạn", app tự gọi là "Nốt" ("Thở cùng Nốt", "Nốt tìm thấy 3 điều tốt").
- Không sáo rỗng ("Cố lên nào!"), không chấm điểm, không nói "thất bại", "mất chuỗi".
- Nhắc chuyện nhạy cảm (nội dung không lành mạnh) bằng từ trung tính: "Nội dung không lành mạnh", "thói quen muốn bớt". Không dùng giọng nặng nề, không làm xấu hổ.
- Nút ghi động từ cụ thể: "Ghi nốt", "Mình vừa dừng lại", "Nhận thử thách", "Đổi thẻ dễ hơn", "Giữ nháp", "Gắn vào hũ".
- Lỗi nói nguyên nhân và cách sửa: "Chưa tải được hũ. Kiểm tra Wi-Fi rồi thử lại." · "Offline · đã lưu trên máy. Sẽ tự đồng bộ khi có mạng."

---

## 7. Quy tắc component

Mọi component ở page 05 dựng bằng Auto Layout, có variant, dùng Variables cho màu và khoảng cách. Component của bản Study Planner cũ (TypeIcon, WeightDots, Tag/Hạn nộp, File/Đính kèm, Stepper/Thêm deadline, BottomNav/iPhone · 4 tab, ChipGroup · Môn học…) vẫn còn ở page 05 nhưng **không dùng** trong Final UI mới.

### 7.1 Component bắt buộc theo đề

| Component | Variant | Quy tắc dùng |
|---|---|---|
| `Button` | Style: Filled, Tonal, Outlined, Text, Destructive × State: Default, Pressed, Disabled, Loading | Mỗi màn chỉ một nút Filled. Destructive chỉ trong dialog Xoá. Loading giữ nguyên bề rộng nút (`S03b · AI · đang đọc`). minWidth 64, cao 48 |
| `Text field` | Default, Focused, Filled, Error, Disabled | Lỗi hiện dưới ô, màu `error`, kèm chữ nguyên nhân |
| `Card/Nốt` (và `Card` cũ) | Type: Chiến thắng, Tự chủ, Thử thách, Nhật ký × State: Default, Pressed | Cả thẻ là vùng chạm; Pressed đổi nền sang `surface-variant` |
| `BottomNav · Nốt` | Active: Hôm nay, Hũ, Thử thách, Hành trình | Chỉ hiện ở 4 màn gốc |
| `App bar` | Default, With actions | Màn lồng có nút Back; `S06` có thêm Sửa, Xoá |
| `Dialog` | Confirmation, Destructive | Nút phụ bên trái, nút chính bên phải |
| `Loading state` | Skeleton list, Spinner | Skeleton cho lịch năng lượng `S11c` |
| `Empty state` | Context | Mascot, một câu, một nút (`S05 · hũ rỗng`) |
| `Error state` | Type: Offline, Load failed | Mascot Lạc, nguyên nhân, nút Thử lại |

### 7.2 Component riêng của Nốt

| Component | Variant | Quy tắc dùng |
|---|---|---|
| `MoodOption` | Default, Selected | 5 ô tâm trạng ở `S03a`, mỗi ô có mặt mascot + chữ. 96 × 116 dp |
| `Chip/Chiến thắng nhanh` | Default, Selected | Chip có sẵn ở `S03b`, `S09`, `S10`; cao 48 dp |
| `Note/Tờ nốt` | Type: Chiến thắng, Tự chủ, Thử thách, Nhật ký | Tờ nốt trong lưới 2 cột ở `S05`, `S04`. Nhãn loại + tiêu đề + ngày |
| `Cell/Ngày năng lượng` | Mood: Vui, Ổn, Bình thường, Mệt, Rối, Chưa ghi, Khác tháng | Ô lịch tháng ở `S11c`, 48 × 56 dp, có số ngày và mặt mascot |
| `Cell/Pixel năm` | Mood: … + Không có ngày | Ô nhỏ ở chế độ Năm (chỉ trang trí, có chú giải chữ) |
| `Sticker/Mốc` | Đã mở, Chưa mở | Nhãn dán tháng ở `S04 · đạt mốc tháng`, `S11a` |
| `SettingRow` | Trailing: Value, Switch | Các dòng ở `S12`, `S09` |
| `Switch` | On, Off | Màu tắt là `switch-off` |
| `Illustration/Hũ chiến thắng`, `Decor/Confetti`, `TopBar/Stats`, `Mascot/Avatar` | — | Hình lớn của `S02`, `S04`, `S05` |
| `Mascot`, `MascotAnim` | 8 trạng thái | Xem mục 9 |

---

## 8. Thông báo đẩy

| Loại | Giờ mặc định | Nội dung | Chạm → |
|---|---|---|---|
| Nhắc ghi nốt buổi tối | 21:30 (đổi ở `S12`) | "Hôm nay bạn đã làm được gì?" | `S03` bước 1 |
| Giờ tỉnh | 23:00 – 01:00 (đổi ở `S12`) | Nhắc nhẹ, không chặn app khác | `S02` (nút Dừng lại, Thở 90 giây) |
| Thẻ thử thách mới | Buổi sáng | Tên thẻ | `S08` |

Khi bật "Ẩn nội dung thông báo" ở `S12`, thông báo chỉ hiện "Nốt có lời nhắc cho bạn".

---

## 9. Mascot Tụi Nốt

8 trạng thái (component `Mascot`): Thong Thả, Vội, Cháy, Xong, Ngủ, Đợi, Lạc, Tập Trung. File SVG gốc ở `assets/mascot/`.

| Mascot | Dùng ở |
|---|---|
| Nốt Xong | Tâm trạng Vui; `S02`, `S04`, `S10 · sau khi thở`, Thẻ tuần |
| Nốt Thong Thả | Tâm trạng Ổn; `S01`, `S06`, `S10` |
| Nốt Đợi | Tâm trạng Bình thường; hũ rỗng, đang tải |
| Nốt Ngủ | Tâm trạng Mệt; "Nốt AI đang nghỉ" |
| Nốt Lạc | Tâm trạng Rối; mất mạng |
| Nốt Tập Trung | `S07`, `S08`, `S09`, AI đang đọc |
| Nốt Vội, Nốt Cháy | Không dùng trong bản mới |

Mascot không đặt trong tờ nốt để lưới không bị rối.

---

## 10. Ràng buộc

- Khung thiết kế 360 × 800 dp; kiểm tra ở 412 × 915 dp. Nội dung dài cuộn dọc; App bar, nút chính cuối màn và thanh tab đứng yên.
- Vùng chạm ≥ 48 × 48 dp. Chữ nội dung ≥ 14 sp.
- Tiêu đề tờ nốt tối đa 2 dòng, cắt bằng "…"; chiến thắng tối đa 120 ký tự.
- Không dùng màu làm tín hiệu duy nhất.

## 11. Không làm

- Không có dark theme trong Lab 2.
- Không chặn app khác (ngoài phạm vi; Nốt chỉ nhắc và ghi nhận).
- Không có chuỗi ngày bị phạt về 0, không bảng xếp hạng, không mạng xã hội.
- Không thiết kế màn cho máy tính bảng (mô tả hành vi màn rộng ở `handoff/flutter-handoff.md`).
