# Flutter handoff — Nốt (app ghi chú tích cực)

Tài liệu này mô tả cách dựng app Nốt bằng Flutter (Material 3) từ file Figma `PRM393-LAB2-Study-Planner`, page `03 Final UI`, section **Final UI · Nốt tích cực (24/10)**. Người dựng chỉ cần mở Figma để xem hình; mọi giá trị, trạng thái, tương tác và điều hướng đều ghi ở đây.

- **Mã màn** `S01`–`S12` là tiền tố trong tên frame (ví dụ `S03b · Ghi nốt · bước 2 chiến thắng`). Mỗi frame là viền điện thoại 388 × 828 bao khung màn hình 360 × 800 dp.
- **Mã flow** (F1–F3, P1–P8, T1–T3) giống page 01 và 06. Xem [`ux/user-flow.md`](../ux/user-flow.md).
- **Token** lấy từ Figma Variables, Text Styles, Effect Styles. Xem [`design/DESIGN.md`](../design/DESIGN.md).
- Figma vẽ thanh trạng thái kiểu iPhone ("9:41"). Trên Android dùng thanh trạng thái của hệ điều hành và bọc nội dung trong `SafeArea`.

> **Giá trị do đặc tả này đặt (không có trong Figma):** độ dài tối đa các ô nhập (chiến thắng 120, nhật ký 2000, thói quen 40 ký tự), thời gian hiện snackbar Hoàn tác 5 giây, ngưỡng chuyển sang lỗi khi tải 10 giây, dialog "Đăng xuất khỏi Nốt?". Nếu nhóm đồng ý, thêm vào Figma; nếu không, ghi vào `docs/design-traceability.md` khi làm Lab 3.

Gói dùng: `go_router`, `provider` hoặc `flutter_riverpod` (theo Lab 3), `google_fonts`, `flutter_svg`, `fl_chart`, `local_auth` (khoá Tự chủ), `flutter_local_notifications`, `intl`.

---

## 1. Bảng token sang Flutter

### 1.1 Màu

| Figma Variable | Giá trị | Flutter |
|---|---|---|
| `primary` | `#3D4FD6` | `ColorScheme.primary` |
| `on-primary` | `#FFFFFF` | `ColorScheme.onPrimary` |
| `primary-container` | `#DCE6FF` | `ColorScheme.primaryContainer` |
| `on-primary-container` | `#2F3FB8` | `ColorScheme.onPrimaryContainer` |
| `primary-dark` | `#2B399F` | `AppColors.primaryDark` |
| `surface` | `#FFFFFF` | `ColorScheme.surface` (nền `Scaffold`) |
| `surface-card` | `#F6F7FB` | `ColorScheme.surfaceContainerLow` (nền thẻ, ô tâm trạng, chip) |
| `surface-container` | `#E7E9F3` | `ColorScheme.surfaceContainer` |
| `surface-variant` | `#E7E9F3` | `ColorScheme.surfaceContainerHighest` (thẻ đang nhấn, skeleton, ngày chưa ghi) |
| `on-surface` | `#1B1D2A` | `ColorScheme.onSurface` |
| `on-surface-variant` | `#555B6E` | `ColorScheme.onSurfaceVariant` |
| `on-surface-muted` | `#3A3F52` | `AppColors.onSurfaceMuted` |
| `outline` | `#7A8094` | `ColorScheme.outline` |
| `outline-variant` | `#E3E5EE` | `ColorScheme.outlineVariant` |
| `error` | `#B3261E` | `ColorScheme.error` |
| `tint/red` | `#FDE1DF` | `ColorScheme.errorContainer` |
| `warning` | `#A84F00` | `AppColors.warning` |
| `success` | `#187A4D` | `AppColors.success` |
| `switch-off` | `#C3C7D4` | `SwitchThemeData.trackColor` khi tắt |
| `heat/1` … `heat/5` | `#A9DCF5`, `#7FD9B3`, `#FFD24A`, `#FF9A3D`, `#F0524B` | `AppColors.mood[Mood.vui]` … `AppColors.mood[Mood.roi]` (Vui, Ổn, Bình thường, Mệt, Rối) |
| `tint/orange`, `tint/violet`, `tint/green`, `tint/blue` | `#FFEBD6`, `#ECEBFC`, `#DDF5EA`, `#E3F3FB` | `AppColors.noteTint[NoteType.chienThang / tuChu / thuThach / nhatKy]` |
| `tint/gray`, `tint/lavender` | `#ECEEF3`, `#EEF0FE` | `AppColors.tintGray` (nền lỗi), `AppColors.tintLavender` (nền rỗng) |
| `mono/1` … `mono/5` | `#DFE3FD`, `#C0C8F8`, `#9EA9F3`, `#7A88EA`, `primary` | `AppColors.chart[0..4]` (biểu đồ `S11b`) |

`AppColors` là một `ThemeExtension<AppColors>` gắn vào `ThemeData.extensions`. Widget đọc màu bằng `Theme.of(context).colorScheme` hoặc `Theme.of(context).extension<AppColors>()!`, không viết mã màu trong widget.

### 1.2 Chữ

Font `GoogleFonts.beVietnamPro`. Line height ghi theo hệ số (`height`).

| Figma Text Style | Flutter | Cỡ · độ đậm · height |
|---|---|---|
| `Display/44 Bold` | `textTheme.displayMedium` | 44 · w700 · 1.25 |
| `Display/36 Bold` | `textTheme.displaySmall` | 36 · w700 · 1.25 |
| `Headline/28 Bold` | `textTheme.headlineMedium` | 28 · w700 · 1.25 |
| `Title/24 Bold` | `textTheme.headlineSmall` | 24 · w700 · 1.25 |
| `Headline/22 Bold` | `textTheme.titleLarge` | 22 · w700 · 1.25 |
| `Title/20 Bold` | `AppText.title20` | 20 · w700 · 1.25 |
| `Title/18 Bold` | `textTheme.titleMedium` | 18 · w700 · 1.4 |
| `Title/17 SemiBold` | `textTheme.titleSmall` | 17 · w600 · 1.4 |
| `Title/17 Bold` | `AppText.title17Bold` | 17 · w700 · 1.4 |
| `Body/17 Regular` | `AppText.body17` | 17 · w400 · 1.4 |
| `Body/16 Regular` | `textTheme.bodyLarge` | 16 · w400 · 1.4 |
| `Body/16 SemiBold`, `Body/16 Bold` | `bodyLarge.copyWith(fontWeight: w600 / w700)` | 16 · 1.4 |
| `Body/15 Regular` | `textTheme.bodyMedium` | 15 · w400 · 1.4 |
| `Body/15 SemiBold` | `bodyMedium.copyWith(fontWeight: w600)` | 15 · 1.4 |
| `Label/14 Regular` | `textTheme.bodySmall` | 14 · w400 · 1.4 |
| `Label/14 SemiBold` | `textTheme.labelLarge` (chữ trên nút) | 14 · w600 · 1.4 |
| `Label/14 Medium`, `Label/14 Bold` | `labelLarge.copyWith(fontWeight: w500 / w700)` | 14 · 1.4 |
| `Label/13 SemiBold` | `textTheme.labelMedium` | 13 · w600 · 1.4 |
| `Label/13 Regular` | `labelMedium.copyWith(fontWeight: w400)` | 13 · 1.4 |
| `Caption/12 SemiBold` | `textTheme.labelSmall` (nhãn tab) | 12 · w600 · 1.4 |
| `Caption/12 Regular`, `Caption/12 Bold` | `labelSmall.copyWith(...)` | 12 · 1.4 |
| `Overline/12 Bold` | `AppText.overline` ("BƯỚC 1/3", "DŨNG CẢM · 2 PHÚT", chữ hoa) | 12 · w700 · 1.4 · letterSpacing 0.5 |

Quy tắc: chữ nội dung dùng tối thiểu 14 sp (`bodySmall` trở lên). Cỡ 12–13 chỉ cho nhãn tab, nhãn bước, số ngày trên lịch. Không đặt `textScaler` cố định; để hệ điều hành phóng to chữ.

### 1.3 Khoảng cách, bo góc, elevation, kích thước

| Figma | Flutter |
|---|---|
| `space/2`, `4`, `6`, `8`, `10`, `12`, `14`, `16`, `20`, `24` | `AppSpace.s2` … `AppSpace.s24` (`double` const) |
| Lề trái phải màn hình 16 dp | `AppSpace.screen = 16` |
| Khoảng cách lưới tờ nốt 12 dp | `AppSpace.grid = 12` |
| `radius/4`, `6`, `8`, `12` | `AppRadius.r4` … `AppRadius.r12` |
| Tờ nốt 14, thẻ / ô tâm trạng / nút lớn 16, thanh tab 32, chip tròn (chưa có Variable) | `AppRadius.note = 14`, `AppRadius.card = 16`, `AppRadius.nav = 32`, `StadiumBorder()` cho chip |
| `Elevation/0 Flat` | `CardTheme(elevation: 0)` |
| `Elevation/2 FAB` (shadow blur 16, y 6, 22%) | `BoxShadow(blurRadius: 16, offset: Offset(0, 6), color: onSurface.withOpacity(.22))` cho thanh tab nổi |
| Vùng chạm tối thiểu 48 × 48 | `ThemeData(materialTapTargetSize: MaterialTapTargetSize.padded)`; `IconButton` mặc định 48 |
| Nút cao 48, rộng tối thiểu 64 | `FilledButtonThemeData(style: FilledButton.styleFrom(minimumSize: Size(64, 48)))` (tương tự cho Tonal, Outlined, Text) |
| App bar 48, thanh tab 64 (rộng 361, nổi, bo 32) | `AppBarTheme(toolbarHeight: 48)`, `NavigationBarThemeData(height: 64)` |

---

## 2. Bảng component sang widget

| Component (page 05) | Variant | Widget Flutter |
|---|---|---|
| `Button` Filled | Default, Pressed, Disabled, Loading | `FilledButton`. Disabled: `onPressed: null`. Loading: `onPressed: null`, child là `SizedBox.square(dimension: 20, child: CircularProgressIndicator(strokeWidth: 2))`, giữ nguyên bề rộng |
| `Button` Tonal | như trên | `FilledButton.tonal` |
| `Button` Outlined | như trên | `OutlinedButton` |
| `Button` Text | như trên | `TextButton` |
| `Button` Destructive | như trên | `FilledButton(style: FilledButton.styleFrom(backgroundColor: colorScheme.error))` |
| `Text field` | Default, Focused, Filled, Error, Disabled | `TextFormField` + `InputDecoration(labelText, hintText, errorText, counterText)`; Disabled: `enabled: false` |
| `Card/Nốt` | Chiến thắng, Tự chủ, Thử thách, Nhật ký × Default, Pressed | `NoteCard(type, title, meta, date)`: `Material(color: surfaceContainerLow, borderRadius: 16)` + `InkWell` (Pressed = hiệu ứng chạm, nền `surfaceContainerHighest`). Cao 72 |
| `Note/Tờ nốt` | 4 loại | `NoteTile(type, title, date)`: `Container` nền `AppColors.noteTint[type]`, bo 14, padding 12; nhãn loại `labelLarge`, tiêu đề `titleSmall` tối đa 3 dòng |
| `BottomNav · Nốt` | Active: Hôm nay, Hũ, Thử thách, Hành trình | `NavigationBar` với 4 `NavigationDestination`, bọc trong `Container` nổi bo 32, cách đáy 12 |
| `App bar` | Default, With actions | `AppBar(leading: BackButton(), title, actions: [IconButton(edit), IconButton(delete)])` |
| `Dialog` | Confirmation, Destructive | `AlertDialog` (nút trái `TextButton`, nút phải `FilledButton` hoặc Destructive) |
| `Loading state` | Skeleton list, Spinner | `SkeletonGrid` (tự dựng: các `Container` màu `surfaceContainerHighest`, bo 12, nhấp nháy) · `CircularProgressIndicator` |
| `Empty state` | — | `EmptyState(mascot, title, message, actionLabel, onAction)` |
| `Error state` | Offline, Load failed | `ErrorState(mascot: MascotState.lac, title, cause, onRetry)` |
| `MoodOption` | Default, Selected | `MoodOption(mood, selected, onTap)`: 96 × 116, bo 16, mascot 48 + chữ; Selected nền `primaryContainer`; `Semantics(selected: true, label: 'Tâm trạng Ổn')` |
| `Chip/Chiến thắng nhanh` | Default, Selected | `ChoiceChip` cao 48, `StadiumBorder`; Selected nền `primary`, chữ `onPrimary` |
| `Cell/Ngày năng lượng` | 7 mood | `MoodDayCell(date, mood)`: 48 × 56, nền `AppColors.mood[mood]`, số ngày `labelSmall`, mặt mascot 20; `Semantics(label: '24 tháng 10, Ổn')` |
| `Cell/Pixel năm` | 7 mood | `MoodPixel(mood)` 10 × 10, `ExcludeSemantics` (chỉ trang trí, có chú giải chữ) |
| `Sticker/Mốc` | Đã mở, Chưa mở | `MilestoneSticker(month, unlocked)` |
| `SettingRow` | Value, Switch | `ListTile(title, subtitle, trailing: Text(value) / Switch)`, cao tối thiểu 56 |
| `Switch` | On, Off | `Switch` |
| Tab con Con đường / Thống kê / Lịch, Tháng / Năm, Chọn nhanh / Kể tự do | — | `SegmentedButton<T>` cao 48 |
| Snackbar Hoàn tác | — | `ScaffoldMessenger.showSnackBar(SnackBar(duration: Duration(seconds: 5), action: SnackBarAction(label: 'Hoàn tác')))` |
| Banner offline | — | `MaterialBanner` hoặc `Container` nền `tintGray` ở đầu nội dung |
| Biểu đồ `S11b` | — | `fl_chart` `LineChart` (năng lượng 30 ngày), `BarChart` (cân bằng 5 điều tốt), co giãn theo chiều rộng thẻ |
| `Illustration/Hũ chiến thắng`, `Decor/Confetti` | — | `SvgPicture.asset('assets/illustration/hu.svg')`; confetti dùng `AnimatedOpacity` (tắt khi bật "giảm chuyển động") |
| `Mascot` | 8 trạng thái | `SvgPicture.asset('assets/mascot/mascot-not-<tên>.svg')` |
| `MascotAnim` | Phase A, B, C | `AnimatedSwitcher` A → B → C (khi `MediaQuery.disableAnimations` chỉ dùng A) |
| `Icon/*` | 19 icon | Material Icons tương đương (`arrow_back`, `close`, `add`, `edit`, `check`, `refresh`, `chevron_right`, `notifications`, `logout`, `more_vert`…) |

---

## 3. Điều hướng chung

Dùng `go_router`. Bốn tab nằm trong `StatefulShellRoute.indexedStack` để mỗi tab giữ vị trí cuộn.

| Route | Màn | Ghi chú |
|---|---|---|
| `/welcome` | `S01` | `redirect`: chưa đăng nhập thì mọi route khác về `/welcome?next=<route>` |
| `/today` | `S02` | Tab 1, route mặc định sau đăng nhập |
| `/note/new?step=1..3` | `S03` | Toàn màn hình (`fullscreenDialog: true`), 3 bước trong `PageView`, nháp giữ trong ViewModel |
| `/note/saved/:id` | `S04` | Thay thế route `S03` (`go`), không `push` |
| `/jar` | `S05` | Tab 2 |
| `/jar/:noteId` | `S06` | |
| `/challenges` | `S07` | Tab 3 |
| `/challenges/:id` | `S08` | Đích của thông báo thẻ mới |
| `/self-control` | `S09` | Qua `LocalAuthGuard` nếu bật khoá |
| `/breathe` | `S10` | Mở thẳng, không chờ dữ liệu |
| `/journey?tab=path|stats|calendar` | `S11` | Tab 4 |
| `/settings` | `S12` | |

**Back (nút Back trên App bar và nút Back hệ thống):**

- Màn lồng: `context.pop()`.
- `S03`: bước 2, 3 về bước trước; bước 1 đóng luồng. Nếu đã nhập dữ liệu, mở dialog "Giữ nốt đang ghi?" (Bỏ / Giữ nháp).
- `S04`: Back và "Về Hôm nay" đều `go('/today')`.
- `S10` đang đếm giờ: Back dừng đồng hồ và về màn trước, không hỏi.
- Tab khác Hôm nay: Back chuyển về tab Hôm nay. Ở Hôm nay hoặc `S01`: thoát app.
- Dialog: Back đóng dialog (tương đương nút trái).

**Thông báo (flow P7):** chạm thông báo nhắc tối → `/note/new?step=1`; Giờ tỉnh → `/today`; thẻ mới → `/challenges/:id`. Nếu chưa đăng nhập → `/welcome?next=…`, đăng nhập xong mới tới đích.

---

## 4. Đặc tả từng màn hình

Mặc định cho mọi màn, trừ khi ghi khác:

- **Màn gốc của tab** (`S02`, `S05`, `S07`, `S11`): `Scaffold` → nội dung cuộn (padding ngang 16, dưới 96 để không bị thanh tab che) → thanh tab nổi.
- **Màn lồng**: `Scaffold` → `AppBar` (48, nút Back) → `SingleChildScrollView` (padding 16) → vùng nút cố định cuối màn (padding 16, gap 8).
- Khi bàn phím mở: `Scaffold(resizeToAvoidBottomInset: true)`, vùng nút nằm trên bàn phím.
- Lưu khi mất mạng: ghi vào bộ nhớ máy, đánh dấu `pendingSync`, hiện banner "Offline · đã lưu trên máy"; tự đồng bộ khi có mạng lại.

### `S01` · Chào mừng & Đăng nhập
1. **Layout:** `Scaffold` (nền `surface`) → `Column`: khối hero giãn chiếm chỗ trống (3 `MascotAnim` xếp chồng, chữ "Nốt" `displayMedium`, câu "Mỗi ngày một nốt tích cực." `bodyLarge`) → khối nút (gap 12, padding ngang 16, cách đáy 24). Không cuộn.
2. **Components:** `Button` Filled "Tiếp tục với Google"; `Button` Outlined "Đăng nhập bằng email"; `Button` Text "Chưa có tài khoản? Đăng ký"; `MascotAnim` (Thong Thả, Xong, Tập Trung).
3. **States:** Default; Loading (nút Google ở Loading, hai nút kia Disabled); Error (SnackBar "Không đăng nhập được. Thử lại.").
4. **Interactions:** Chạm Google → Google Sign-In → thành công: lần đầu đi P1 (xin quyền thông báo, chọn giờ nhắc ở `S12`) rồi `S02`; tài khoản cũ đi `S02`. Huỷ chọn tài khoản: về Default, SnackBar "Bạn đã huỷ đăng nhập.". Email / Đăng ký mở form email (Email: bắt buộc, dạng `x@y.z`, tối đa 254 ký tự; Mật khẩu: bắt buộc, ≥ 8 ký tự), lỗi hiện ngay dưới ô.
5. **Navigation:** Vào khi chưa đăng nhập hoặc sau Đăng xuất. Đăng nhập xong → `S02` (hoặc `next`). Back: thoát app.
6. **Constraints:** Ba nút cao 48, rộng full. Ô email dùng `TextInputType.emailAddress`. Màn rộng ≥ 600: khối nút rộng tối đa 400, căn giữa.

### `S02` · Hôm nay
1. **Layout:** `Scaffold` → `CustomScrollView`: ngày "Thứ Bảy, 24/10" (`labelLarge`) + số nốt hôm nay (`TopBar/Stats`) → hình hũ lớn (cao 240) với mascot Xong → câu hỏi "Hôm nay bạn làm được gì?" (`headlineMedium`, căn giữa) → `FilledButton` "Ghi nốt" (full) → `Row` 2 nút Tonal "Dừng lại" và "Thở 90 giây" (gap 12) → thẻ "Thử thách" gợi ý. Thanh tab nổi Active = Hôm nay.
2. **Components:** `Illustration/Hũ chiến thắng`, `Mascot` Xong, `Button` Filled / Tonal, `Card/Nốt` (thẻ thử thách), `BottomNav · Nốt[Hôm nay]`.
3. **States:** Populated (mặc định); chưa có nốt hôm nay (số = 0, hũ rỗng một nửa, không có lỗi); có nháp chưa lưu (nút đổi chữ "Tiếp tục ghi nốt"); Offline (banner, nút vẫn dùng được).
4. **Interactions:** "Ghi nốt" → `S03`. "Dừng lại" → +1 lần tự chủ ngay (1 chạm), SnackBar "Đã ghi 1 lần tự chủ" có Hoàn tác 5 giây, số trên hũ tăng 1, không cần mở khoá. "Thở 90 giây" → `S10`. Chạm thẻ thử thách → `S08`. Ngày tâm trạng hôm qua là Mệt / Rối: hũ "rơi ra" 1 nốt cũ, chạm để xem `S06`.
5. **Navigation:** Từ đăng nhập hoặc thanh tab. Back: thoát app.
6. **Constraints:** Nút chính ở nửa dưới màn (vùng ngón cái). Ngày dùng `DateFormat('EEEE, dd/MM', 'vi')`. Màn rộng: hũ và nút đặt 2 cột (hũ trái, nút phải).

### `S03` · Ghi nốt (3 bước)
1. **Layout:** `Scaffold` → `AppBar` "Ghi nốt" (Back) → nhãn "Bước n/3" (`overline`) → `PageView` (không vuốt tay, chỉ chuyển bằng nút):
   - **Bước 1 (`S03a`):** câu hỏi `headlineMedium` → `Wrap` 5 `MoodOption` (gap 12, 3 ô hàng trên, 2 ô hàng dưới). Chọn Rối: thêm dòng "Ngày rối: 1 chip là đủ." và thẻ "Sơ cứu 1 phút: 5-4-3-2-1" với nút Tonal "Làm cùng Nốt".
   - **Bước 2 (`S03b`):** câu hỏi → `TextFormField` "Chiến thắng nhỏ" → nhãn "Hoặc chọn nhanh" → `Wrap` 6 `ChoiceChip` (gap 8).
   - **Bước 3:** `TextFormField` nhiều dòng (minLines 5) "Vài dòng nhật ký".
   - Vùng nút cố định: `FilledButton` "Tiếp" (bước 3: "Lưu vào hũ") + `TextButton` "Bỏ qua nhật ký" (bước 2).
2. **Components:** `App bar` Default, `MoodOption`, `Text field`, `Chip/Chiến thắng nhanh`, `Button` Filled / Text / Tonal, `Dialog` Confirmation, `Mascot`.
3. **States:** Bước 1 chưa chọn (nút Tiếp Disabled); đã chọn; Bước 2 trống (Tiếp Disabled) / có chữ hoặc có chip (Tiếp bật); Đang lưu (nút Loading); Lỗi lưu → vẫn lưu trên máy và đi `S04` với banner offline. Biến thể AI (Final): Kể tự do, đang đọc, gợi ý để xác nhận, AI nghỉ, lần đầu dùng.
4. **Interactions:** Chạm `MoodOption` chọn 1 tâm trạng (chọn lại để đổi). Chiến thắng: tối đa 120 ký tự, cắt khoảng trắng đầu cuối; chạm chip điền tên chip vào ô (có thể sửa tiếp). "Bỏ qua nhật ký" lưu luôn với nhật ký rỗng. Lưu → tạo nốt `{type: chien_thang, mood, title, body?, createdAt}` → `S04`. Back khi đã có dữ liệu → dialog "Giữ nốt đang ghi? Nốt sẽ chờ ở Hôm nay." — "Bỏ" xoá nháp và về `S02`; "Giữ nháp" lưu nháp và về `S02`.
5. **Navigation:** Từ nút "Ghi nốt" ở `S02`, thông báo buổi tối, `S05` rỗng ("Ghi nốt đầu tiên"). Lưu → `S04` (thay route). Back theo mục 3.
6. **Constraints:** Tiêu chí thành công: từ mở bước 1 tới `S04` dưới 30 giây — không có bước tải dữ liệu trong luồng, ô chiến thắng tự focus ở bước 2. Bàn phím: `TextInputAction.done` ở bước 2 gọi "Tiếp". Ô tâm trạng 96 × 116 (≥ 48). Màn rộng: nội dung rộng tối đa 480, căn giữa.

### `S04` · Nốt đã vào hũ
1. **Layout:** `Scaffold` (không AppBar) → `Column` căn giữa: confetti + hũ + mascot Xong → "Đã vào hũ!" (`displaySmall`) → "Nốt thứ 24 tháng này." → `NoteTile` vừa ghi → thanh tiến độ "Mốc tháng 10 · 24/25 nốt" (`LinearProgressIndicator`) → vùng nút: Filled "Về Hôm nay", Text "Viết thêm".
2. **Components:** `Note/Tờ nốt`, `Illustration/Hũ chiến thắng`, `Decor/Confetti`, `Mascot` Xong, `Button` Filled / Text, `Sticker/Mốc`.
3. **States:** Đã lưu online; Lưu khi mất mạng (banner "Offline · đã lưu trên máy" + "Sẽ tự đồng bộ khi có mạng."); Đạt mốc tháng ("Mốc 25 nốt!", dãy nhãn dán các tháng, nút "Gắn vào hũ" / "Để sau").
4. **Interactions:** "Về Hôm nay" → `go('/today')`. "Viết thêm" → `S06` của nốt vừa lưu ở chế độ sửa nhật ký. "Gắn vào hũ" → lưu nhãn dán, về `S02`.
5. **Navigation:** Từ `S03`, `S08` (thử thách xong), `S10` ("Ghi vào hũ"). Back = "Về Hôm nay".
6. **Constraints:** Confetti tắt khi `MediaQuery.disableAnimations`. Tiêu đề nốt tối đa 2 dòng rồi `…`. Màn rộng: nội dung rộng tối đa 480.

### `S05` · Hũ & Nhật ký
1. **Layout:** `Scaffold` → `CustomScrollView`: tiêu đề "Hũ của bạn" (`headlineMedium`) + hũ nhỏ → "24 nốt tháng 10" + liên kết "2 nhãn dán ›" → `SliverGrid` 2 cột (gap 12, tỉ lệ 158 : 137) các `NoteTile`, sắp mới nhất trước. Thanh tab Active = Hũ.
2. **Components:** `Note/Tờ nốt` (4 loại), `Illustration/Hũ chiến thắng`, `Empty state`, `Error state` Offline, `Loading state` Skeleton, `BottomNav · Nốt[Hũ]`.
3. **States:** Loading (lưới skeleton 6 ô); Populated; Empty (mascot Đợi, "Hũ còn trống", "Ghi chiến thắng đầu tiên nhé.", nút "Ghi nốt đầu tiên"); Error (mascot Lạc, "Chưa tải được hũ", "Kiểm tra Wi-Fi rồi thử lại.", nút "Thử lại"); Offline có dữ liệu cũ (lưới + banner); Vừa xoá (snackbar "Đã xoá nốt · còn 5 giây" + "Hoàn tác").
4. **Interactions:** Chạm tờ nốt → `S06`. Kéo xuống để tải lại. "Thử lại" gọi lại tải dữ liệu. "Hoàn tác" khôi phục nốt vào đúng vị trí. Chạm "2 nhãn dán" → danh sách nhãn dán (sheet).
5. **Navigation:** Thanh tab. Back → tab Hôm nay.
6. **Constraints:** Tiêu đề tờ nốt tối đa 3 dòng rồi `…`. Tải theo trang 30 nốt (cuộn tới cuối thì tải tiếp). Quá 10 giây không tải được → Error. Màn rộng: lưới 3 cột (600–839), 4 cột (≥ 840).

### `S06` · Chi tiết nốt
1. **Layout:** `AppBar` "Chi tiết nốt" + actions Sửa, Xoá → nội dung cuộn: "Tâm trạng hôm đó: Ổn" (chip có mặt mascot) → nhãn "✓ CHIẾN THẮNG · 24/10" (`overline`, màu theo loại) → tiêu đề (`headlineSmall`) → đoạn nhật ký (`AppText.body17`) → mascot Thong Thả.
2. **Components:** `App bar` With actions, `Mascot`, `Text field` (chế độ sửa), `Dialog` Destructive, `Button` Text / Destructive.
3. **States:** Xem; Sửa (tiêu đề và nhật ký thành ô nhập, nút "Lưu" cố định cuối màn); Đang lưu; Không tìm thấy nốt (đã bị xoá ở thiết bị khác) → Error state + "Về Hũ".
4. **Interactions:** Sửa → chế độ sửa (giới hạn: tiêu đề 120, nhật ký 2000 ký tự, có bộ đếm). Xoá → dialog "Xoá nốt này? Bạn có 5 giây để hoàn tác." — "Huỷ" đóng; "Xoá" về `S05` và hiện snackbar Hoàn tác 5 giây (xoá thật khi hết giờ). Bí ý khi viết nhật ký: chạm "Gợi ý" thêm 1 câu hỏi gợi mở (flow P4).
5. **Navigation:** Từ `S05`, `S11`, `S02` (nốt cũ rơi ra), `S04` ("Viết thêm"). Back: ở chế độ sửa có thay đổi → dialog "Bỏ thay đổi?"; còn lại `pop`.
6. **Constraints:** Nhật ký cuộn trong `SingleChildScrollView`, không giới hạn số dòng hiển thị. Màn rộng: nội dung rộng tối đa 600.

### `S07` · Thử thách
1. **Layout:** `Scaffold` → tiêu đề "Thử thách" → "Dũng cảm · cấp 2" + "3/5" → thẻ lớn (bo 16, nền `tint/green`): nhãn "DŨNG CẢM · 2 PHÚT", tên thẻ (`headlineSmall`), mascot Tập Trung → `FilledButton` "Nhận thử thách" → chữ gợi ý "Vuốt để đổi thẻ". Thanh tab Active = Thử thách.
2. **Components:** `Mascot` Tập Trung, `Button` Filled / Text, `BottomNav · Nốt[Thử thách]`, `Loading state` Spinner.
3. **States:** Loading (spinner trong thẻ); Populated; Hết thẻ cấp hiện tại (mở thẻ cấp sau); Error (Error state + Thử lại).
4. **Interactions:** Vuốt ngang thẻ (`PageView`) đổi sang thẻ khác cùng cấp. "Nhận thử thách" → `S08`. Chạm "Tự chủ" (lối tắt trong thẻ chủ đề Tự chủ) → `S09`.
5. **Navigation:** Thanh tab, `S04` sau khi xong thử thách. Back → tab Hôm nay.
6. **Constraints:** Thẻ cao tối đa 60% màn. Vuốt có thêm nút mũi tên cho người dùng trình đọc màn hình (`Semantics(onScrollLeft/Right)`). Màn rộng: thẻ rộng tối đa 480, căn giữa.

### `S08` · Chi tiết thử thách
1. **Layout:** `AppBar` "Thử thách" → nội dung cuộn: nhãn "DŨNG CẢM · 2 PHÚT" → tên thẻ → mẹo "Hỏi ngắn thôi, 30 giây là đủ." → "Bạn hồi hộp cỡ nào?" + `SegmentedButton` 1–5 (nhãn hai đầu "Bình tĩnh" / "Run lắm") → câu mẫu trong khung trích dẫn → vùng nút: Filled "Xong rồi", Text "Đổi thẻ dễ hơn".
2. **Components:** `App bar` Default, `Mascot` Tập Trung, `Button` Filled / Text, `SegmentedButton`, `Text field` (cảm giác sau).
3. **States:** Chưa chấm hồi hộp ("Xong rồi" vẫn bật — chấm là không bắt buộc); Sau khi bấm "Xong rồi": sheet "Kết quả?" với 2 lựa chọn "Suôn sẻ" / "Không như ý" + ô 1 dòng cảm giác sau; Đang lưu.
4. **Interactions:** "Xong rồi" → sheet kết quả → "Lưu" tạo nốt `{type: thu_thach, subtype: nguoi_la | van_dong, anxietyBefore, outcome, note}` → `S04`. "Không như ý" lưu với chữ "Mình đã mở lời". "Đổi thẻ dễ hơn" → thẻ cấp thấp hơn cùng chủ đề, ở lại `S08`. Thử thách vận động (P3): có thêm ô số phút; dừng sớm vẫn lưu.
5. **Navigation:** Từ `S07`, `S02`, thông báo thẻ mới. Back → màn trước, thẻ giữ nguyên, không trừ gì ("để mai").
6. **Constraints:** Ô cảm giác tối đa 120 ký tự. `SegmentedButton` mỗi ô ≥ 48 dp. Màn rộng: nội dung rộng tối đa 600.

### `S09` · Tự chủ
1. **Layout:** `AppBar` "Tự chủ" → nội dung cuộn: số lớn "8" + "lần tự chủ tháng này" + mascot Tập Trung → `FilledButton` "Mình vừa dừng lại" → `FilledButton.tonal` "Khó dừng? Thở 90 giây" → nhãn "THÓI QUEN MUỐN BỚT" + `Wrap` chip (Lướt mạng xã hội, Video ngắn, Game quá giờ, Nội dung không lành mạnh, + Thêm) → `SettingRow` "Giờ tỉnh · 23:00 – 01:00" có `Switch`.
2. **Components:** `App bar`, `Mascot`, `Button` Filled / Tonal, `Chip/Chiến thắng nhanh` (Default / Selected), `SettingRow[Switch]`, `Switch`.
3. **States:** Khoá (trước khi vào: `local_auth` sinh trắc học / PIN; thất bại → ở lại màn trước, SnackBar "Chưa mở được phần Tự chủ."); Populated; Vừa ghi (số tăng 1, SnackBar có Hoàn tác); Đã lỡ lướt (sheet "Lúc đó mình đang thấy gì?" + thông điệp "Nhận ra cũng là bắt đầu tự chủ").
4. **Interactions:** "Mình vừa dừng lại" → +1 nốt `{type: tu_chu, habit?}`, ở lại màn. "Thở 90 giây" → `S10`. Chạm chip chọn / bỏ chọn thói quen muốn bớt (lưu ngay). "+ Thêm" → ô nhập (tối đa 40 ký tự). Công tắc Giờ tỉnh bật / tắt nhắc; chạm giờ → `showTimePicker` 2 lần (bắt đầu, kết thúc).
5. **Navigation:** Từ `S02`, `S07`. Back → màn trước. Rời app (paused) → khoá lại.
6. **Constraints:** Danh sách thói quen không hiện ở thông báo hay widget. `FLAG_SECURE` khi ở màn này (ẩn trong ảnh chụp danh sách app gần đây). Màn rộng: nội dung rộng tối đa 600.

### `S10` · Thở 90 giây
1. **Layout:** `AppBar` "Thở cùng Nốt" → `Column` căn giữa: sóng thở (`CustomPaint`, cao 200) + mascot Thong Thả → "Hít vào…" / "Thở ra…" (`headlineMedium`) → "4 giây vào · 6 giây ra" → "Còn 1:12" → vùng nút: Tonal "Đổi kiểu thở", Filled "Cơn sóng đã hạ", Text "Thở thêm 1 vòng".
2. **Components:** `App bar`, `Mascot`, `Button` Filled / Tonal / Text, `Chip/Chiến thắng nhanh` (màn sau khi thở).
3. **States:** Đang thở (đồng hồ đếm 90 giây = 9 nhịp 4+6); Hết giờ (chữ "Xong một vòng"); Sau khi thở ("Bạn đã vượt qua!", "3 lần dừng lại hôm nay", "Làm gì tiếp?" + 4 chip, Filled "Ghi vào hũ", Text "Về Hôm nay").
4. **Interactions:** Mở màn → bắt đầu thở ngay. "Cơn sóng đã hạ" → màn sau khi thở. "Thở thêm 1 vòng" → đặt lại 90 giây. "Đổi kiểu thở" → sheet chọn 4-6 hoặc 4-7-8. Chọn chip việc thay thế + "Ghi vào hũ" → +1 nốt tự chủ → `S04`. Rung nhẹ (`HapticFeedback.lightImpact`) mỗi lần đổi hít / thở.
5. **Navigation:** Từ `S02`, `S09`. Back → dừng và về màn trước.
6. **Constraints:** Mở trong dưới 2 giây: không gọi mạng, không chờ dữ liệu. Giữ màn hình sáng (`wakelock`) khi đang thở. `disableAnimations`: thay sóng bằng chữ và vòng tròn đổi kích thước theo bước. Màn rộng: giữ một cột, rộng tối đa 480.

### `S11` · Hành trình
1. **Layout:** `Scaffold` → tiêu đề "Hành trình" + `SegmentedButton` 3 mục (Con đường, Thống kê, Lịch) → nội dung theo mục, cuộn dọc. Thanh tab Active = Hành trình. Nút bánh răng trên đầu → `S12`.
   - **Con đường (`S11a`):** đường đi dọc các chặng; mỗi chặng có `Sticker/Mốc` (đã mở: tick / ngôi sao; chưa mở: ổ khoá) và thẻ chặng hiện tại "CHẶNG 2 · DŨNG CẢM · 3/5".
   - **Thống kê (`S11b`):** 2 ô số (Nốt tuần này 18 ↑ 20%; Chuỗi ngày 6 · Kỷ lục 9) → thẻ "Năng lượng mỗi ngày" (`LineChart`, 30 ngày, thang 1–5, `DropdownButton` 7 / 30 ngày, tooltip ngày + năng lượng + số nốt, dòng tổng kết) → "Mục tiêu tuần 5/7" → "Cân bằng 5 điều tốt" (`BarChart` ngang + gợi ý) → "Bạn ghi nốt ngày nào?". Nút "Thẻ tuần" mở story (nút Tonal "Lưu thẻ tuần (PDF)").
   - **Lịch (`S11c`):** "Lịch năng lượng" + chuyển Tháng / Năm → lưới 7 cột `MoodDayCell` (T2 … CN) → chú giải "Vui … Rối · Ý nghĩa màu". Chế độ Năm: lưới 12 cột `MoodPixel` + câu tổng kết.
2. **Components:** `SegmentedButton`, `Cell/Ngày năng lượng`, `Cell/Pixel năm`, `Sticker/Mốc`, `Mascot`, `Loading state` Skeleton, `Error state`, `Button` Tonal, `BottomNav · Nốt[Hành trình]`.
3. **States:** Loading (skeleton + mascot Đợi, "Đang tải lịch năng lượng…"); Populated; Ít dữ liệu (< 3 ngày: biểu đồ thay bằng chữ "Ghi thêm vài ngày để thấy xu hướng"); Error (mất mạng / quá 10 giây → Error state + Thử lại, flow T2, T3).
4. **Interactions:** Đổi tab con giữ vị trí cuộn từng tab. Chạm một ngày trên lịch → sheet các nốt ngày đó → chạm nốt → `S06`. Chạm điểm trên biểu đồ → tooltip. "Lưu thẻ tuần (PDF)" → tạo PDF, mở hộp chia sẻ của hệ thống. P6: tâm trạng Mệt / Rối 5 ngày liền → dialog gợi ý nói chuyện với người tin cậy / đường dây hỗ trợ (có nút "Để sau").
5. **Navigation:** Thanh tab. → `S06`, `S12`. Back → tab Hôm nay.
6. **Constraints:** Ô lịch 48 × 56, phần dư chia đều làm khoảng cách. Biểu đồ co giãn theo chiều rộng thẻ (Figma vẽ cố định 294 px). Biểu đồ có `Semantics(label: 'Năng lượng 30 ngày, trung bình 3,8, tăng 0,4 so với tháng 9')`. Màn rộng ≥ 840: Thống kê 2 cột.

### `S12` · Cài đặt
1. **Layout:** `AppBar` "Cài đặt" → `ListView`: nhóm "NHẮC NHỞ" (Nhắc ghi nốt buổi tối · 21:30; Giờ tỉnh · 23:00 – 01:00) → "QUYỀN RIÊNG TƯ" (Nốt AI sắp xếp giúp — "Không gửi tên, email, ảnh"; Khoá phần Tự chủ; Ẩn nội dung thông báo) → "TÀI KHOẢN" (Email) → `OutlinedButton` "Đăng xuất".
2. **Components:** `App bar`, `SettingRow` Value / Switch, `Switch`, `Button` Outlined, `Dialog` Confirmation.
3. **States:** Default; Quyền thông báo bị từ chối (banner "Bạn đang tắt thông báo. Bật lại trong Cài đặt máy." + nút "Mở cài đặt"); Đang đăng xuất (nút Loading).
4. **Interactions:** Chạm giờ nhắc → `showTimePicker`, lưu ngay, đặt lại lịch thông báo. Bật "Khoá phần Tự chủ" → xác thực `local_auth` một lần để bật. Công tắc Nốt AI (Final: đọc cờ `ai_enabled` từ Remote Config; tắt ở máy thì ẩn tab "Kể tự do"). "Đăng xuất" → dialog "Đăng xuất khỏi Nốt?" (Huỷ / Đăng xuất) → xoá dữ liệu trên máy → `S01`.
5. **Navigation:** Từ `S11`. Back → `S11`.
6. **Constraints:** Mỗi dòng cao tối thiểu 56. Email hiển thị 1 dòng rồi `…`. Màn rộng: danh sách rộng tối đa 600.

---

## 5. Màn hình rộng (từ 600 dp trở lên)

Không thiết kế riêng. Khi dựng, đổi bố cục theo chiều rộng (`LayoutBuilder` hoặc `MediaQuery.sizeOf(context).width`):

| Độ rộng | Thay đổi |
|---|---|
| < 600 dp | Như Figma: thanh tab nổi ở dưới, một cột |
| 600–839 dp | `NavigationRail` bên trái thay thanh tab; nút "Ghi nốt" nằm trên rail. Nội dung một cột, rộng tối đa 600, căn giữa. `S03`, `S04`, `S10` rộng tối đa 480. Lưới Hũ 3 cột. Bottom sheet thành `Dialog` rộng 480 |
| ≥ 840 dp | Hai cột: `S05` (lưới 4 cột) bên trái + `S06` bên phải; `S07` bên trái + `S08` bên phải; Thống kê `S11b` hai cột thẻ |

Ô ngày ở `S11c` giữ 48 × 56 dp; phần dư chia đều làm khoảng cách giữa các cột.
