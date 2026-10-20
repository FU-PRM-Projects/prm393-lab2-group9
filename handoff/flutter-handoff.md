# Flutter handoff — Nốt (Study Planner)

Tài liệu này mô tả cách dựng app Nốt bằng Flutter (Material 3) từ file Figma `PRM393-LAB2-Study-Planner`. Người dựng chỉ cần mở Figma để xem hình; mọi giá trị, trạng thái, tương tác và điều hướng đều ghi ở đây.

- **Mã màn** là mã trong tên frame ở page `03 Final UI` (ví dụ `7s`). Mỗi màn trong Figma là khung 360 × 800 dp nằm bên trong viền điện thoại.
- **Mã flow** (C1–C4, P1–P8, S1–S3) giống page 01 và 06. Xem [`ux/user-flow.md`](../ux/user-flow.md).
- **Token** lấy từ Figma Variables, Text Styles, Effect Styles. Xem [`design/DESIGN.md`](../design/DESIGN.md).
- Figma vẽ thanh trạng thái kiểu iPhone. Trên Android dùng thanh trạng thái của hệ điều hành và bọc nội dung trong `SafeArea`.

> **Giá trị do đặc tả này đặt (không có trong Figma):** giới hạn độ dài các ô nhập, dung lượng tệp tối đa 20 MB, thời gian chờ AI 20 giây, thời gian chờ nút Gửi lại 60 giây, chữ của trạng thái rỗng ở `2`, `2f`, `10f`, dialog "Bỏ deadline đang tạo?" và dialog "Đăng xuất khỏi Nốt?". Nếu nhóm đồng ý, thêm các chi tiết này vào Figma; nếu không, ghi vào `docs/handoff-gaps.md` khi làm Lab 3.

Gói dùng: `go_router`, `provider` hoặc `flutter_riverpod` (theo Lab 3), `google_fonts`, `flutter_svg`, `file_picker`, `image_picker`, `url_launcher`, `intl`.

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
| `surface-card` | `#F6F7FB` | `ColorScheme.surfaceContainerLow` (nền `Card`) |
| `surface-container` | `#E7E9F3` | `ColorScheme.surfaceContainer` |
| `surface-variant` | `#E7E9F3` | `ColorScheme.surfaceContainerHighest` (segmented, skeleton, ngày trống) |
| `on-surface` | `#1B1D2A` | `ColorScheme.onSurface` |
| `on-surface-variant` | `#555B6E` | `ColorScheme.onSurfaceVariant` |
| `on-surface-muted` | `#3A3F52` | `AppColors.onSurfaceMuted` |
| `outline` | `#7A8094` | `ColorScheme.outline` |
| `outline-variant` | `#E3E5EE` | `ColorScheme.outlineVariant` |
| `error` | `#B3261E` | `ColorScheme.error` |
| `tint/red` | `#FDE1DF` | `ColorScheme.errorContainer` và `AppColors.tintRed` |
| `warning` | `#A84F00` | `AppColors.warning` |
| `success` | `#1F9D63` | `AppColors.success` (chỉ cho icon và chữ ≥ 18 sp, xem `design-decisions.md`) |
| `switch-off` | `#C3C7D4` | `SwitchThemeData.trackColor` khi tắt |
| `heat/1` … `heat/5` | `#A9DCF5`, `#7FD9B3`, `#FFD24A`, `#FF9A3D`, `#F0524B` | `AppColors.heat[1..5]`; `heat[0]` = `surface-variant` |
| `tint/blue`, `orange`, `green`, `violet`, `yellow`, `indigo`, `gray`, `lavender` | `#E3F3FB`, `#FFEBD6`, `#DDF5EA`, `#ECEBFC`, `#EEF2FE`, `#E4E7FF`, `#ECEEF3`, `#EEF0FE` | `AppColors.tintBlue` … `AppColors.tintLavender` |

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
| `Overline/12 Bold` | `AppText.overline` (nhãn "BƯỚC 1/5 · …", chữ hoa) | 12 · w700 · 1.4 · letterSpacing 0.5 |

Quy tắc: chữ nội dung dùng tối thiểu 14 sp (`bodySmall` trở lên). Cỡ 12–13 chỉ dùng cho nhãn tab, nhãn bước, số ngày trên lịch. Không đặt `textScaler` cố định; để hệ điều hành phóng to chữ.

### 1.3 Khoảng cách, bo góc, elevation

| Figma | Flutter |
|---|---|
| `space/2`, `4`, `6`, `8`, `10`, `12`, `14`, `16`, `20`, `24` | `AppSpace.s2` … `AppSpace.s24` (`double` const) |
| Lề trái phải màn hình 16 dp (Kế hoạch 12 dp) | `AppSpace.screen = 16`, `AppSpace.screenPlan = 12` |
| `radius/4`, `6`, `8`, `12` | `AppRadius.r4` … `AppRadius.r12` |
| Thẻ bo 20, nút lớn 16, ô loại việc 14 (chưa có Variable) | `AppRadius.card = 20`, `AppRadius.button = 16`, `AppRadius.tile = 14` |
| `Elevation/0 Flat` | `CardTheme(elevation: 0)`, `NavigationBarTheme(elevation: 0)` |
| `Elevation/2 FAB` (shadow blur 16, y 6, 22%) | `FloatingActionButtonThemeData(elevation: 6)` |
| Vùng chạm tối thiểu 48 × 48 | `ThemeData(materialTapTargetSize: MaterialTapTargetSize.padded)`; `IconButton` mặc định 48 |
| Nút chính cao 48 | `FilledButtonThemeData(style: FilledButton.styleFrom(minimumSize: Size.fromHeight(48)))` |
| App bar cao 48, thanh điều hướng cao 64, nút + 56 × 56 | `AppBarTheme(toolbarHeight: 48)`, `NavigationBarThemeData(height: 64)`, `FloatingActionButton` |

---

## 2. Bảng component sang widget

| Component (page 05) | Variant | Widget Flutter |
|---|---|---|
| `Button` Filled | Default, Pressed, Disabled, Loading | `FilledButton`. Disabled: `onPressed: null`. Loading: `onPressed: null`, child là `SizedBox(20, 20, CircularProgressIndicator(strokeWidth: 2))`, giữ nguyên bề rộng |
| `Button` Tonal | như trên | `FilledButton.tonal` |
| `Button` Outlined | như trên | `OutlinedButton` |
| `Button` Text | như trên | `TextButton` |
| `Button` Destructive | như trên | `FilledButton` với `backgroundColor: colorScheme.error` |
| `Text field` | Default, Focused, Filled, Error, Disabled | `TextFormField` + `InputDecoration(labelText, hintText, errorText)`; Disabled: `enabled: false` |
| `PasswordField` | Hidden, Shown | `TextFormField(obscureText)` + `suffixIcon: TextButton('Hiện' / 'Ẩn')` |
| `Card` | Task, Summary × Default, Pressed | `Card(elevation: 0, color: surfaceContainerLow)` + `InkWell` (Pressed là hiệu ứng chạm) |
| `BottomNav/iPhone · 4 tab` | Active: Hôm nay, Kế hoạch, Deadline, Hồ sơ | `NavigationBar` với 4 `NavigationDestination` |
| `App bar` | Default, With actions | `AppBar(leading: BackButton(), title, actions: [IconButton…])` |
| `Dialog` | Confirmation, Destructive | `AlertDialog` (nút trái `TextButton` Huỷ, nút phải `FilledButton` hoặc Destructive) |
| `Loading state` | Skeleton list, Spinner | `SkeletonList` (tự dựng: các `Container` màu `surfaceContainerHighest`, bo 12, có hiệu ứng nhấp nháy) · `CircularProgressIndicator` |
| `Empty state` | Deadline, Hôm nay | `EmptyState(mascot, title, message, actionLabel, onAction)` |
| `Error state` | Offline, Load failed | `ErrorState(mascot: lac, title, cause, onRetry)` |
| `Stepper/Thêm deadline` | Step 1–5 | `StepHeader(step, total: 5, label)`: chữ `AppText.overline` + `LinearProgressIndicator(value: step/5)` |
| `Tag/Hạn nộp` | Hôm nay, Quá hạn, Sắp tới, Đã nộp | `DueTag(level, text)`: `Container` bo 8, nền theo mức, chữ `labelLarge` |
| `Notification/Row` | 5 loại × Chưa đọc, Đã đọc | `NotificationRow(type, title, subtitle, time, unread)` trên nền `ListTile` |
| `File/Đính kèm` | PDF, DOCX, XLSX, PPTX, ZIP, Ảnh, Link, Đang tải lên | `AttachmentTile(type, name, meta, progress)`; Đang tải lên có `LinearProgressIndicator` |
| `WeightDots` | Level 1–3 | `WeightDots(level)` (3 chấm, kèm `Semantics(label: 'Độ nặng: Vừa')`) |
| `ChipGroup · Môn học`, `OptionGroup · Loại việc` | Selected 1–6 | `Wrap` các `ChoiceChip` |
| `SwatchGroup · Màu` | Selected 1–6 | `Wrap` các ô màu 48 × 48 có `Semantics(selected)` |
| `Switch` | On, Off | `Switch` |
| Nút chuyển Tháng / Tuần, Sắp đến hạn / Môn học, Tất cả / Chưa đọc | — | `SegmentedButton<T>` |
| Bottom sheet (`4c`, `6b4`, `7t`, `9d`) | — | `showModalBottomSheet(isScrollControlled: true, useSafeArea: true)` |
| Snackbar (Hoàn tác, Đã xoá…) | — | `ScaffoldMessenger.showSnackBar(SnackBar(action: SnackBarAction('Hoàn tác')))`, hiện 4 giây |
| Ô ngày ở lịch nhiệt | — | `HeatDayCell(date, weight, level, mascot)`: vùng chạm 48 × 48 |
| `Mascot`, `MascotMini` | 8 trạng thái; 4 mức hạn | `SvgPicture.asset('assets/mascot/mascot-not-<tên>.svg')` |
| `MascotAnim` | Phase A, B, C | Chuyển ảnh A → B → C bằng `AnimatedSwitcher` (tuỳ chọn; khi bật "giảm chuyển động" thì chỉ dùng A) |
| Nút + | — | `FloatingActionButton(child: Icon(Icons.add))` |
| `Icon/*` | 19 icon | Xuất SVG từ page 05 hoặc dùng Material Icons tương đương (`arrow_back`, `close`, `add`, `edit`, `filter_list`, `check`, `refresh`, `chevron_right`, `notifications`, `logout`, `remove`, `schedule`, `flag`, `link`, `image`, `calendar_today`, `description`, `upload`, `more_vert`) |

---

## 3. Điều hướng chung

Dùng `go_router`. Bốn tab nằm trong `StatefulShellRoute.indexedStack` để mỗi tab giữ vị trí cuộn.

| Route | Màn | Ghi chú |
|---|---|---|
| `/login` | `1` | `redirect`: chưa đăng nhập thì mọi route khác về `/login` |
| `/login/email` | `1b` (lỗi `1d`) | |
| `/register` | `1c` | |
| `/forgot` → `/forgot/sent` | `1e` → `1f` | |
| `/reset-password?code=…` | `1g` → `1h` | Mở từ link trong email (deep link) |
| `/onboarding` → `/onboarding/q/1..3` | `O1` → `O2`, `O3`, `O4` | Chỉ hiện lần đầu |
| `/today` | `2` | Tab 1 |
| `/today/chunk/:taskId` | `2c0` → `2c` → `2c3` | Một route, 3 bước trong `PageView` |
| `/today/achievements` | `2f` | |
| `/plan?view=month` · `/plan?view=week` | `3` · `9` | Tab 2 |
| `/plan/day/:date` | `4` (biến thể `4d`) | |
| `/plan/day/:date/spread` | `4b` (sheet `4c`) | |
| `/deadlines?tab=upcoming` · `?tab=courses` | `5` · `10b` | Tab 3 |
| `/deadlines/course/:courseId` | `10c` | |
| `/deadlines/new` | `6` → `6b2` → `6b2a` → `6b3` → `6b5` | Một route, 5 bước, giữ dữ liệu nháp trong ViewModel |
| `/courses/new` | `6b` | Trả về môn mới cho `6` hoặc `10b` |
| `/deadlines/:id` | `7` (biến thể `7c`, `7d`) | |
| `/deadlines/:id/edit` | `7b` | |
| `/deadlines/:id/phases/:phaseId` | `7s` (biến thể `7s1`, `7s2`) | Đích của thông báo giai đoạn |
| `/deadlines/:id/overdue` | `7o` (biến thể `7o2`) | |
| `/deadlines/:id/done` | `8` | Thay thế route hiện tại (`go`), không `push` |
| `/notifications` | `13` | |
| `/profile` | `10` | Tab 4 |
| `/profile/submitted` | `10f` | |
| `/settings`, `/settings/help`, `/settings/icons` | `10e`, `11`, `12` | |
| `/settings/demo/config`, `/settings/demo/crash` | `14`, `15` | |

**Back (nút Back trên App bar và nút Back hệ thống):**

- Màn lồng: `context.pop()`.
- `6` đến `6b5`: về bước trước; ở `6` thì đóng luồng. Nếu đã nhập dữ liệu, hỏi bằng dialog "Bỏ deadline đang tạo?" (Huỷ, Bỏ).
- `8`: Back và "Về Deadline" đều `go('/deadlines')`.
- Tab khác Hôm nay: Back chuyển về tab Hôm nay. Ở Hôm nay hoặc `1`: thoát app.
- Bottom sheet và dialog: Back đóng sheet hoặc dialog.

---

## 4. Đặc tả từng màn hình

Mặc định cho mọi màn, trừ khi ghi khác:

- **Màn gốc của tab** (`2`, `3`/`9`, `5`/`10b`, `10`): `Scaffold` → nội dung cuộn → `NavigationBar` (64) và nút + (56) ở góc dưới phải (trừ `10`).
- **Màn lồng**: `Scaffold` → `AppBar` (48, nút Back) → `SingleChildScrollView` (padding 16, trên 16) → vùng nút cố định cuối màn (padding 16, cao 68).
- Chữ tiêu đề thẻ tối đa 2 dòng rồi `…`; dòng phụ 1 dòng rồi `…`. Không cắt chữ hạn nộp.
- Khi bàn phím mở: `Scaffold(resizeToAvoidBottomInset: true)`, vùng nút cố định nằm trên bàn phím, ô đang nhập được cuộn vào giữa màn.
- Lỗi mạng khi lưu: giữ nguyên dữ liệu đã nhập, hiện `SnackBar` "Chưa lưu được. Kiểm tra kết nối rồi thử lại." có nút Thử lại.

### 01 · Xác thực

#### `1` · Đăng nhập
1. **Layout:** `Scaffold` (nền `surface` + họa tiết giấy note) → `Column`: khối hero (mascot Tập Trung, chữ "Nốt" `displayMedium`, câu giới thiệu `bodyLarge`, giãn chiếm chỗ trống) → khối nút (gap 12, padding ngang 16, cách đáy 24). Không cuộn.
2. **Components:** `Button` Filled "Tiếp tục với Google" (icon Google); `Button` Outlined "Đăng nhập bằng email"; `Button` Text "Chưa có tài khoản? Đăng ký"; `Mascot` Tập Trung.
3. **States:** Default; Loading (nút Google ở Loading, hai nút còn lại Disabled); Lỗi (SnackBar "Không đăng nhập được bằng Google. Thử lại.").
4. **Interactions:** Chạm Google → mở Google Sign-In → thành công: tài khoản mới đi `O1`, tài khoản cũ đi `2`; huỷ chọn tài khoản: về Default, không báo lỗi.
5. **Navigation:** Vào khi mở app chưa đăng nhập hoặc sau Đăng xuất. Email → `1b`. Đăng ký → `1c`. Back: thoát app.
6. **Constraints:** Ba nút cao 48, rộng full (328). Ở màn rộng ≥ 600: khối nút rộng tối đa 400, căn giữa.

#### `1b` · Đăng nhập bằng email (lỗi: `1d`)
1. **Layout:** `AppBar` "Đăng nhập" → `Form` cuộn (padding 16, gap 16): Email, Mật khẩu, nút Text "Quên mật khẩu?" căn phải → nút Filled "Đăng nhập" → nút Text "Chưa có tài khoản? Đăng ký".
2. **Components:** `Text field` (Email); `PasswordField`; `Button` Filled, Text.
3. **States:** Default, Focused, Filled; Loading (nút Đăng nhập); Error `1d`: dòng `errorText` dưới ô mật khẩu "Sai email hoặc mật khẩu."
4. **Interactions:** Email bắt buộc, đúng dạng `x@y.z`, tối đa 254 ký tự. Mật khẩu bắt buộc. Kiểm tra khi bấm Đăng nhập; lỗi định dạng hiện ngay dưới ô. Sai thông tin → `1d`, giữ email, xoá mật khẩu. Đúng → `2`.
5. **Navigation:** Từ `1`. Quên mật khẩu → `1e` (mang theo email). Đăng ký → `1c`. Back → `1`.
6. **Constraints:** Bàn phím email (`TextInputType.emailAddress`), ô mật khẩu `TextInputAction.done` gọi Đăng nhập.

#### `1c` · Đăng ký
1. **Layout:** Như `1b`: Tên hiển thị, Email, Mật khẩu (gợi ý "Ít nhất 8 ký tự.") → nút Filled "Tạo tài khoản" → "Đã có tài khoản? Đăng nhập".
2. **Components:** `Text field` × 2, `PasswordField`, `Button` Filled, Text.
3. **States:** Default, Error theo từng ô, Loading.
4. **Interactions:** Tên 1–40 ký tự; email đúng dạng và chưa dùng ("Email này đã có tài khoản."); mật khẩu ≥ 8 ký tự. Thành công → `O1`.
5. **Navigation:** Từ `1`, `1b`. Back → màn trước.
6. **Constraints:** Như `1b`.

#### `1e` · Quên mật khẩu → `1f` · Kiểm tra email → `1g` · Đặt mật khẩu mới → `1h` · Thành công
1. **Layout:** Mỗi màn: `AppBar` → tiêu đề `headlineSmall` → nội dung → nút Filled cuối form.
2. **Components:** `1e`: `Text field` Email, Filled "Gửi link". `1f`: Filled "Mở ứng dụng email", Text "Chưa nhận được? Gửi lại". `1g`: `PasswordField` × 2, Filled "Lưu mật khẩu". `1h`: Filled "Vào Nốt".
3. **States:** Loading trên mỗi nút; `1g` Error "Hai mật khẩu không khớp." / "Ít nhất 8 ký tự."; `1f` nút Gửi lại Disabled 60 giây sau mỗi lần gửi (ghi "Gửi lại sau 45 giây").
4. **Interactions:** `1e` gửi link đặt lại tới email (luôn đi `1f`, không báo email có tồn tại hay không). `1f` "Mở ứng dụng email" mở app mail. Link trong email mở `1g`. `1g` lưu → `1h`. `1h` → đăng nhập và vào `2`.
5. **Navigation:** `1b`/`1d` → `1e` → `1f`; deep link → `1g` → `1h` → `2`. Back ở `1h` → `2`.
6. **Constraints:** Link hết hạn → `1g` hiện `ErrorState` "Link đã hết hạn" với nút "Gửi link mới" → `1e`.

### 02 · Làm quen

#### `O1` · Làm quen
1. **Layout:** Mascot lớn giữa màn, tiêu đề "Làm quen với Nốt nhé!", phụ đề "3 câu hỏi ngắn", nút Filled "Bắt đầu", nút Text "Để sau".
2. **Components:** `Mascot`, `Button` Filled, Text.
3. **States:** Default.
4. **Interactions:** Bắt đầu → `O2`. Để sau → `2` (đánh dấu đã qua làm quen).
5. **Navigation:** Từ `1c` hoặc lần đầu đăng nhập Google. Back → thoát app (đã đăng nhập).
6. **Constraints:** Chỉ hiện một lần cho mỗi tài khoản.

#### `O2`, `O3`, `O4` · Ba câu hỏi
1. **Layout:** `AppBar` (Back, nhãn "1/3", "2/3", "3/3") → tiêu đề câu hỏi → danh sách lựa chọn cuộn (gap 10) → vùng nút cố định (Filled "Tiếp tục" hoặc "Xong"; Text "Bỏ qua bước này" ở `O3`, `O4`).
2. **Components:** `O2`: các `Card` chọn một (radio). `O3`, `O4`: `ChoiceChip` chọn nhiều + chip "+ Thêm khác". `Button` Filled, Text.
3. **States:** Nút Tiếp tục Disabled ở `O2` khi chưa chọn; `O3`, `O4` luôn bật.
4. **Interactions:** "+ Thêm khác" mở `Text field` trong dòng (tối đa 30 ký tự). Tiếp tục lưu câu trả lời vào hồ sơ người dùng. Xong ở `O4` → `2`.
5. **Navigation:** `O1` → `O2` → `O3` → `O4` → `2`. Back → câu trước.
6. **Constraints:** Lựa chọn là vùng chạm ≥ 48. Câu trả lời dùng để chọn gợi ý mặc định (ví dụ dự án ở `6`).

### 03 · Hôm nay

#### `2` · Hôm nay
1. **Layout:** Màn gốc tab 1. `CustomScrollView` (padding 16, gap 16): hàng đầu (ngày "Thứ Tư, 7/10" + nút chuông có badge) → thẻ **Hạn hôm nay** → thẻ chuỗi đúng hạn → dải 7 ngày (cuộn ngang, mỗi ngày một ô nhiệt) → mục **Cần để ý** (tiêu đề + "Xem tất cả", danh sách thẻ). Dưới cùng: `NavigationBar` (Hôm nay chọn), nút +.
2. **Components:** `Card` Summary (Hạn hôm nay, có `Tag/Hạn nộp` Hôm nay và nút Filled "Xem việc cần làm"); `Card` Summary (chuỗi, mascot Xong); `HeatDayCell` × 7; `Card` Task (Cần để ý); `BottomNav` Active=Hôm nay; nút +.
3. **States:** Loading (Skeleton list); Empty (`Empty state` Context=Hôm nay: "Hôm nay chưa có việc" + Thêm deadline); Error (`Error state` Offline, nút Thử lại); Populated. Thẻ Hạn hôm nay chỉ hiện khi có việc đến hạn hôm nay. Mục Cần để ý ẩn khi rỗng.
4. **Interactions:** "Xem việc cần làm" → `7` của việc đó. Chạm thẻ chuỗi → `2f`. Chạm ô ngày → `4` của ngày đó. Chạm "Tiểu luận chương 3 · hay bị dời" → `2c0`. Chạm "Thứ Sáu đang quá nặng" → `4b`. Chuông → `13`. Nút + → `6`. Kéo xuống để làm mới.
5. **Navigation:** Màn mở đầu sau đăng nhập. Back: thoát app.
6. **Constraints:** Tên việc trong thẻ tối đa 2 dòng. Số việc ở Cần để ý tối đa `today_max_tasks` (Remote Config, mặc định 5). Màn rộng: xem mục 5.

#### `2c0` → `2c` (thêm bước `2c2`) → `2c3` · Chia nhỏ việc hay bị dời
1. **Layout:** `AppBar` "Chia nhỏ việc" → thẻ việc (tên, "Hạn T6 9/10", "Đã dời 3 lần") → nhãn "BƯỚC n/3" → nội dung bước → vùng nút cố định.
2. **Components:** `ChoiceChip` (lý do ở `2c0`); danh sách bước có thể sửa tên (`Text field` trong dòng) và xoá; Text "+ Thêm bước" (`2c2`); ở `2c3` mỗi bước có nút chọn giờ (`showDatePicker` + `showTimePicker`); `Button` Filled "Tiếp", "Tiếp: chọn giờ", "Xếp vào lịch".
3. **States:** `2c` mở sẵn 3 bước gợi ý ("Nốt gợi ý 3 bước, mỗi bước khoảng 45 phút"). "Xếp vào lịch" Disabled tới khi mọi bước có giờ. Loading khi lưu.
4. **Interactions:** Chọn lý do (không bắt buộc) → Tiếp. Sửa, xoá, thêm bước (1–6 bước, tên 1–60 ký tự). Giờ phải trước hạn nộp; chọn giờ sau hạn → báo "Giờ này sau hạn nộp." Xếp vào lịch → lưu các bước thành giai đoạn → `3c` (Kế hoạch có 3 buổi mới, SnackBar "Đã xếp 3 buổi").
5. **Navigation:** Từ thẻ ở `2`, menu `9e`, nút ở `4d`. Back → bước trước; ở `2c0` → màn đã mở.
6. **Constraints:** Tối đa 6 bước. Gợi ý thời lượng chỉ là chữ, không khoá.

#### `2f` · Bảng thành tích tuần này
1. **Layout:** `AppBar` → hàng 3 số (ngày liên tiếp đúng hạn, deadline nộp đúng hạn "3/3", giai đoạn đã xong) → câu giải thích → danh sách theo ngày (tiêu đề ngày, các dòng việc).
2. **Components:** `Card` Summary × 3; `Note/Đã làm` (Đúng hạn, Giai đoạn, Nộp muộn); mascot Xong.
3. **States:** Loading, Empty ("Tuần này chưa có việc xong"), Populated.
4. **Interactions:** Chạm một dòng giai đoạn → `7s1`/`7s2`; chạm dòng deadline → `7`.
5. **Navigation:** Từ thẻ chuỗi ở `2`, "Xem cả bảng" ở `10`, thông báo Hoàn thành ở `13`. Back → màn trước.
6. **Constraints:** Tuần tính từ Thứ Hai.

### 04 · Kế hoạch

#### `3` · Kế hoạch — Tháng (biến thể `3c`, `3d`)
1. **Layout:** Màn gốc tab 2. Padding 12, gap 20: `SegmentedButton` Tháng / Tuần → hàng tháng ("Tháng 10, 2026", nút trước, sau) → hàng tên thứ T2–CN → `GridView` 7 cột ô ngày → chú thích mức. `NavigationBar` (Kế hoạch chọn), nút +.
2. **Components:** `SegmentedButton`; `HeatDayCell` (ngày, màu `heat`, số độ nặng, khuôn mặt); `BottomNav` Active=Kế hoạch.
3. **States:** Loading (lưới skeleton), Error (Offline), Populated. `3c`: SnackBar "Đã xếp 3 buổi". `3d`: SnackBar "Đã dời 2 việc" + Hoàn tác.
4. **Interactions:** Chạm ô ngày: nếu còn ngày nhẹ trước hạn cho các việc dời được → `4`; nếu không → `4` ở trạng thái `4d`. Vuốt ngang đổi tháng. Tuần → `9`. Hoàn tác trên SnackBar khôi phục lịch trước khi dời.
5. **Navigation:** Thanh điều hướng. Back → tab Hôm nay.
6. **Constraints:** 7 ô × 48 = 336 dp vừa khung 360 với lề 12. Độ nặng ngày = tổng độ nặng việc trong ngày (Quiz 1; Lab, Tiểu luận, Thuyết trình 2; Báo cáo, Đồ án 3). Màu: 1 Rất nhẹ, 2–3 Nhẹ, 4–5 Vừa, 6–7 Nặng, ≥ 8 Rất nặng.

#### `4` · Chi tiết ngày (biến thể `4d`)
1. **Layout:** `AppBar` (ngày "Thứ Sáu, 9/10") → `SingleChildScrollView` (gap 24): nhãn mức ("Rất nặng") + "5 việc · 3 việc đến hạn ngày này" → thẻ gợi ý giãn việc → "Việc trong ngày" (danh sách).
2. **Components:** `Card` Summary gợi ý (nút Filled "Xem trước"); `Card` Task (tên, môn · hạn, nhãn "dời được"); `Tag/Hạn nộp`; mascot Cháy.
3. **States:** Gợi ý (có ngày nhẹ); `4d` Không dời được: thẻ "Chưa có ngày đủ nhẹ để dời. Các ngày trước hạn nộp đều đã từ mức Vừa trở lên." + nút Filled "Chia nhỏ một việc"; Loading; Error.
4. **Interactions:** Xem trước → `4b`. Chia nhỏ một việc → `2c0` (việc hay bị dời nhất). Chạm một việc → `7`.
5. **Navigation:** Từ ô ngày ở `3` hoặc `2`. Back → `3`.
6. **Constraints:** Nhãn mức luôn là chữ, không chỉ màu.

#### `4b` · Xem trước dời việc (sheet `4c` · Chọn ngày dời)
1. **Layout:** `AppBar` "Giãn việc thứ Sáu" → hàng so sánh độ nặng (T6 Rất nặng → Nặng; T5 Nhẹ → Vừa) → "Chọn việc để dời" (mỗi dòng: tên, hạn, "Dời sang T5 8/10" có thể chạm) → khối "3 việc đến hạn ngay thứ Sáu" (không dời được) → câu giải thích → nút Filled cố định "Dời 2 việc".
2. **Components:** `Card` Task có checkbox; nút ngày (Outlined nhỏ); `Button` Filled; sheet `4c`: lịch tháng với màu độ nặng nếu thêm việc vào, `Button` Filled "Chọn".
3. **States:** Mặc định chọn sẵn các việc dời được và ngày đề xuất; nút "Dời n việc" đổi số theo số việc đã chọn, Disabled khi 0; Loading khi lưu.
4. **Interactions:** Bỏ chọn hoặc chọn việc. Chạm ngày → mở `4c`: chỉ cho chọn ngày từ hôm nay tới trước hạn nộp của việc (ngày sau hạn bị tắt, ghi "Sau hạn nộp"). Dời → lưu → `3` ở trạng thái `3d` với SnackBar Hoàn tác.
5. **Navigation:** Từ `4`, thẻ "Thứ Sáu đang quá nặng" ở `2`, thông báo Gợi ý dời. Back → màn trước; Back trong `4c` đóng sheet.
6. **Constraints:** Việc đến hạn ngay ngày đó không có trong danh sách dời. Đề xuất = ngày gần nhất còn nhẹ trước hạn nộp.

#### `9` · Kế hoạch — Tuần (menu `9e`, sheet `9d`)
1. **Layout:** Màn gốc tab 2 (chế độ Tuần). `SegmentedButton` → hàng ngày T2–CN → lưới giờ cuộn dọc (mỗi giờ 48 dp, cột giờ bên trái) với các khối: giờ bận (nền `tint/indigo`), giai đoạn (nền theo loại việc), việc đã xong (gạch, "Đã xong"). `NavigationBar`, nút +.
2. **Components:** `SegmentedButton`; khối sự kiện (custom `TimeBlock`); `9e`: menu (`showModalBottomSheet` nhỏ) có "Để mai", "Chia nhỏ việc này"; `9d`: sheet với `Text field` Tên, chọn Từ, Đến, `Switch` Mỗi tuần, chọn thứ trong tuần, `Button` Filled "Lưu giờ bận".
3. **States:** Loading, Error, Populated; `9e` hiện nhãn "Đã dời 3 lần" nếu có.
4. **Interactions:** Nút + → `9d`. Tên 1–40 ký tự; "Đến" phải sau "Từ" ("Giờ kết thúc phải sau giờ bắt đầu."). Lưu → về `9`, khối mới hiện. Nhấn giữ một khối giai đoạn → `9e`: Để mai dời sang cùng giờ ngày mai (nếu trước hạn), SnackBar Hoàn tác; Chia nhỏ → `2c0`. Chạm khối → `7s`.
5. **Navigation:** Từ `3` (nút Tuần). Back → tab Hôm nay.
6. **Constraints:** Cuộn sẵn tới giờ hiện tại. Khối ngắn hơn 30 phút chỉ hiện tên 1 dòng.

### 05 · Thông báo

#### `13` · Thông báo (phương án hiển thị `13A` hoặc `13B`)
1. **Layout:** `AppBar` "Thông báo" + nút Text "Đọc hết" → `SegmentedButton` Tất cả / Chưa đọc · n → `ListView` các dòng.
2. **Components:** `Notification/Row` (Sắp đến giờ, Hạn hôm nay, Gợi ý dời, Hoàn thành, Quá hạn × Chưa đọc, Đã đọc).
3. **States:** Loading, Empty ("Chưa có thông báo"), Populated. Dòng chưa đọc: chữ đậm, giờ màu `primary`, có chấm (theo `13A`: thêm nền nhạt).
4. **Interactions:** Chạm dòng → đánh dấu đã đọc và mở: Sắp đến giờ → `7s`; Hạn hôm nay → `7`; Gợi ý dời → `4b`; Hoàn thành → `2f`; Quá hạn → `7o`. Đọc hết → mọi dòng thành Đã đọc, badge chuông về 0.
5. **Navigation:** Từ chuông ở `2`. Back → `2`.
6. **Constraints:** Giờ tương đối: "Vừa xong", "15 phút", "2 giờ", rồi "16/10". Tiêu đề tối đa 2 dòng.

#### `13p` · Thông báo đẩy (màn khoá)
1. **Layout:** Thông báo hệ thống Android: tiêu đề "Tới giờ làm: Chạy thực nghiệm", nội dung "Paper · ngày 3/7 · 20:00 mỗi ngày", 2 action.
2. **Components:** `flutter_local_notifications` (nhắc theo lịch trên máy) hoặc FCM (Lab 3); 2 `AndroidNotificationAction`: "Mở giai đoạn", "Nhắc lại 15 phút".
3. **States:** Không áp dụng.
4. **Interactions:** Chạm thông báo hoặc "Mở giai đoạn" → mở app tại `/deadlines/:id/phases/:phaseId` (`7s`). "Nhắc lại 15 phút" → hẹn lại thông báo sau 15 phút, không mở app.
5. **Navigation:** Mở `7s` với ngăn xếp `2` → `7s`, nên Back về `2`.
6. **Constraints:** Hẹn nhắc mỗi ngày vào giờ của giai đoạn, và trước hạn chót theo "Nhắc trước". Xin quyền thông báo trên Android 13+ khi lưu deadline đầu tiên.

### 06 · Deadline

#### `5` · Deadline — Sắp đến hạn (trạng thái Rỗng, Đang tải, Lỗi; biến thể `5e`, `5o1`–`5o3`)
1. **Layout:** Màn gốc tab 3. Tiêu đề "Deadline" → `SegmentedButton` Sắp đến hạn / Môn học → nhãn "1 quá hạn" → `ListView` theo nhóm Quá hạn, Hôm nay, Tuần này (tiêu đề nhóm có `MascotMini`). `NavigationBar`, nút +.
2. **Components:** `SegmentedButton`; `Card` Task (tên, "PRM393 · 2/3 giai đoạn", `Tag/Hạn nộp`); `MascotMini`; `Loading state` Skeleton list; `Empty state` Context=Deadline; `Error state` Offline.
3. **States:** Đang tải ("Đang đồng bộ deadline…" + skeleton); Rỗng ("Chưa có deadline nào. Nốt sẽ nhắc bạn trước hạn." + nút Filled "Thêm deadline"); Lỗi ("Mất kết nối. Kiểm tra kết nối rồi thử lại." + Thử lại); Populated. `5e`, `5o1`, `5o2`, `5o3`: Populated + SnackBar "Đã xoá deadline", "Đã nộp muộn", "Đã dời hạn", "Đã bỏ deadline".
4. **Interactions:** Chạm việc quá hạn → `7o`; chạm việc khác → `7`. Thử lại → Đang tải → Populated hoặc Lỗi. Nút + hoặc "Thêm deadline" → `6`. Môn học → `10b`. Kéo xuống để làm mới.
5. **Navigation:** Thanh điều hướng; `8` "Về Deadline". Back → tab Hôm nay.
6. **Constraints:** Sắp xếp trong nhóm theo hạn tăng dần. Việc đã bỏ không hiện. Tên việc tối đa 2 dòng.

#### `10b` · Deadline — Môn · Dự án
1. **Layout:** Như `5`, nhưng danh sách là các môn và dự án (tên, mã, số deadline, tiến độ "1/4").
2. **Components:** `Card` Summary; `SegmentedButton`; nút +.
3. **States:** Loading, Empty ("Chưa có môn học" + Thêm môn), Error, Populated.
4. **Interactions:** Chạm môn → `10c`. Nút + ở chế độ này → `6b`.
5. **Navigation:** Từ `5` (nút Môn học), `10e` (Môn học của tôi). Back → `5`.
6. **Constraints:** Tên môn tối đa 1 dòng, mã môn luôn hiện.

#### `10c` · Chi tiết môn học
1. **Layout:** `AppBar` (mã môn) → thẻ môn (tên, "3 còn lại · 1 đã nộp", tiến độ) → danh sách deadline của môn.
2. **Components:** `Card` Summary, `Card` Task, `Tag/Hạn nộp`.
3. **States:** Loading, Empty ("Môn này chưa có deadline" + Thêm deadline), Populated.
4. **Interactions:** Chạm deadline → `7`. Thêm deadline → `6` với môn đã chọn sẵn.
5. **Navigation:** Từ `10b`. Back → `10b`.
6. **Constraints:** —

#### `6b` · Thêm môn học
1. **Layout:** `AppBar` "Thêm môn học" → form: Tên môn, Mã môn, Màu nhận diện → nút Filled cố định "Lưu môn học".
2. **Components:** `Text field` × 2, `SwatchGroup · Màu`, `Button` Filled.
3. **States:** Default, Error, Loading.
4. **Interactions:** Tên 1–60 ký tự bắt buộc; mã 2–10 ký tự, chữ và số, tự viết hoa, không trùng ("Mã môn đã có."); màu mặc định ô đầu. Lưu → quay về màn mở nó với môn mới được chọn.
5. **Navigation:** Từ `6` (Thêm dự án mới), `10b`, `10c`. Back → màn trước (hỏi bỏ thay đổi nếu đã nhập).
6. **Constraints:** Ô màu là vùng chạm 48.

#### `6` → `6b2` → `6b2a` → `6b3` (sheet `6b4`) → `6b5` · Thêm deadline (5 bước)
Chung cho 5 bước: `AppBar` "Thêm deadline" (Back) → `StepHeader` "BƯỚC n/5 · …" → nội dung cuộn → vùng nút cố định (cao 68). Dữ liệu nháp giữ trong `AddDeadlineViewModel` tới khi lưu ở B5.

**`6` · B1 Môn hoặc dự án**
1. **Layout:** Câu hỏi "Deadline này thuộc môn hay dự án?" → `SegmentedButton` Môn học / Dự án → danh sách lựa chọn (mã + tên) → "Thêm dự án mới" → nút "Tiếp · nhập deadline".
2. **Components:** `StepHeader` Step=1; `Card` chọn một; `Button` Text; `Button` Filled.
3. **States:** Nút Tiếp Disabled khi chưa chọn; Loading danh sách; Rỗng (chỉ còn "Thêm môn hoặc dự án").
4. **Interactions:** Chọn một mục → Tiếp → `6b2`. Thêm mới → `6b`.
5. **Navigation:** Từ nút + ở `2`, `3`, `5`; "Thêm deadline" ở trạng thái Rỗng. Back → đóng luồng.
6. **Constraints:** Mục chọn gần nhất lên đầu.

**`6b2` · B2 Deadline**
1. **Layout:** Chip môn đã chọn + "Đổi dự án" → Tên deadline → Loại (chip) + dòng độ nặng ("Bài báo là việc nặng · Cách tính") → Hạn chót (ngày, giờ mặc định 23:59) + dòng "còn n ngày để chia giai đoạn" → Nhắc trước.
2. **Components:** `Text field`; `OptionGroup · Loại việc`; `WeightDots`; nút chọn ngày (`showDatePicker`, `showTimePicker`); `ChoiceChip` Nhắc trước (1 ngày, 3 giờ, 1 giờ, Không nhắc); `Button` Filled "Tiếp".
3. **States:** Error theo ô; Tiếp Disabled tới khi đủ Tên, Loại, Hạn chót.
4. **Interactions:** Tên 1–80 ký tự. Hạn chót phải sau thời điểm hiện tại ("Hạn chót phải sau bây giờ."). "Cách tính" mở `12`. Tiếp → `6b2a`.
5. **Navigation:** `6` → `6b2`. Back → `6` (giữ dữ liệu).
6. **Constraints:** Số ngày = từ hôm nay tới hạn chót, tính cả hai đầu.

**`6b2a` · B3 Mô tả**
1. **Layout:** Thẻ tóm tắt deadline → ô Mô tả nhiều dòng (5–10 dòng) với bộ đếm "142/500" → câu gợi ý "Ghi việc cần làm và ai làm phần nào…" → nút "Tiếp · chia giai đoạn".
2. **Components:** `Text field` (multiline, `maxLength: 500`); `Button` Filled.
3. **States:** Default, Focused, Filled. Không bắt buộc.
4. **Interactions:** Tiếp → `6b3` ở trạng thái Chưa có giai đoạn.
5. **Navigation:** Back → `6b2`.
6. **Constraints:** Tối đa 500 ký tự (không cho gõ thêm).

**`6b3` · B4 Giai đoạn (4 trạng thái) và sheet `6b4`**
1. **Layout:** Thẻ tóm tắt → thanh thời gian "Hôm nay 16/10 → Hạn chót 15/11" (đoạn đã phủ tô màu) → khu vực giai đoạn → nút cố định "Tiếp · xem lại" (hoặc "Dùng n giai đoạn · xem lại").
2. **Components:** `Card` giai đoạn (tên, "T6 16/10 → T5 22/10 · 7 ngày", "Nhắc 20:00 mỗi ngày"); `Button` Tonal "AI gợi ý giai đoạn"; `Button` Outlined "Thêm giai đoạn"; `Button` Text "Tạo lại"; mascot Ngủ, Đợi, Lạc; sheet `6b4`: `Text field` Tên, chọn Từ ngày, Đến ngày, chọn Giờ nhắc, `Button` Filled "Lưu giai đoạn".
3. **States:** **Chưa có giai đoạn** ("Để AI chia theo mô tả, hoặc tự thêm từng giai đoạn."); **AI đang chia** ("AI đang chia 31 ngày theo mô tả…", spinner, các nút Disabled); **Đề xuất của AI** ("AI đề xuất 4 giai đoạn từ mô tả. Chạm để sửa.", Tạo lại); **AI lỗi** ("Chưa chia được giai đoạn. Mất kết nối khi gọi AI. Mô tả của bạn vẫn được giữ." + Filled "Thử lại" + Outlined "Tự nhập tay"); **Có giai đoạn** (danh sách, "Đã chia 31/31 ngày").
4. **Interactions:** AI gợi ý → AI đang chia → Đề xuất (thành công) hoặc AI lỗi (lỗi mạng, hết 20 giây). Chạm một giai đoạn → `6b4` để sửa; vuốt trái để xoá. Thêm giai đoạn hoặc Tự nhập tay → `6b4` trống. Trong `6b4`: Tên 1–40 ký tự; Từ ngày ≥ hôm nay; Đến ngày ≥ Từ ngày và ≤ hạn chót; không chồng ngày với giai đoạn khác ("Trùng ngày với 'Viết báo'."); giờ nhắc mặc định 20:00. Tiếp → `6b5`.
5. **Navigation:** Back → `6b2a`; Back trong `6b4` đóng sheet không lưu.
6. **Constraints:** 1–8 giai đoạn. Cho phép đi tiếp khi chưa phủ kín, nhưng hiện cảnh báo "Còn 5 ngày chưa có giai đoạn". Thời gian chờ AI tối đa 20 giây.

**`6b5` · B5 Xem lại**
1. **Layout:** Thẻ deadline ("Hạn CN 15/11 · 23:59 · 31 ngày") → danh sách giai đoạn → **Lịch thông báo** (các mốc nhắc theo ngày) → nút cố định "Lưu và bật nhắc". Cuộn.
2. **Components:** `Card` Summary; danh sách mốc nhắc; `Button` Filled.
3. **States:** Default; Loading khi lưu; Lỗi lưu (SnackBar + Thử lại, giữ dữ liệu).
4. **Interactions:** Chạm một phần để quay lại bước tương ứng. Lưu → tạo deadline, giai đoạn, lịch nhắc → `7c` với SnackBar "Đã thêm Nộp paper hội nghị".
5. **Navigation:** Back → `6b3`. Sau khi lưu, Back ở `7c` về màn đã mở luồng (`2`, `3` hoặc `5`).
6. **Constraints:** Xin quyền thông báo (Android 13+) ngay trước khi lưu nếu chưa có.

#### `7` · Chi tiết deadline (biến thể `7c`, `7d`; dialog Hoàn thành)
1. **Layout:** `AppBar` (Back; action bút chì) → `SingleChildScrollView` (gap 14): tên + môn → hàng hạn ("Còn 6 giờ · 23:59 hôm nay", `Tag/Hạn nộp`) → "Giai đoạn 2/3 xong" → danh sách giai đoạn (checkbox, tên, ngày, giờ làm) → link nộp → Ghi chú → vùng nút cố định (cao 90): dòng chữ trạng thái + Filled "Hoàn thành deadline".
2. **Components:** `App bar` With actions; `Card` giai đoạn có `Checkbox`; `Tag/Hạn nộp`; `Button` Filled; mascot Vội (khi gần hạn); `Dialog` Confirmation.
3. **States:** Chưa đủ giai đoạn: nút Disabled + "Tick đủ 3 giai đoạn để hoàn thành"; `7d` đủ giai đoạn: nút bật + "Đã xong cả 3 giai đoạn"; `7c` vừa tạo: "0/4 xong", "Thêm link nộp (không bắt buộc)", SnackBar; Loading; Error.
4. **Interactions:** Tick checkbox một giai đoạn → đánh dấu xong (SnackBar Hoàn tác). Chạm tên giai đoạn → `7s`. Chạm link → mở trình duyệt. Hoàn thành deadline → dialog "Hoàn thành Lab 2? Bạn đã xong cả 3 giai đoạn…" → Hoàn thành → `8`; Huỷ → đóng. Bút chì → `7b`.
5. **Navigation:** Từ `2`, `5`, `10c`, `13`. Back → màn trước.
6. **Constraints:** Link nộp tối đa 1 dòng, cắt giữa. Ghi chú tối đa 500 ký tự.

#### `8` · Đã nộp
1. **Layout:** Không có App bar. Hiệu ứng confetti phía trên → mascot Xong → "Đã nộp" `displaySmall` → tên deadline → "Sớm hơn hạn 6 giờ" → "Chuỗi 3 ngày đúng hạn" → hai nút cuối màn.
2. **Components:** `Mascot` Xong (hoặc `MascotAnim`); `Button` Filled "Xem việc tiếp theo"; `Button` Text "Về Deadline".
3. **States:** Đúng hạn ("Sớm hơn hạn …") hoặc đúng giờ ("Đúng 23:59").
4. **Interactions:** Xem việc tiếp theo → `7` của việc có hạn gần nhất (nếu không còn việc → `5`). Về Deadline → `5`.
5. **Navigation:** Từ dialog Hoàn thành ở `7d`. Back → `5` (không quay lại `7d`).
6. **Constraints:** Khi bật "giảm chuyển động" thì tắt confetti.

#### `7s` · Chi tiết giai đoạn (biến thể `7s1`, `7s2`; sheet `7t`)
1. **Layout:** `AppBar` ("Paper · Giai đoạn 1") → cuộn (gap 18): nhãn "GIAI ĐOẠN 1/4 · Ngày 3/7" → tên giai đoạn → "T6 16/10 → T5 22/10 · 7 ngày" → "Nhắc 20:00 mỗi ngày" → **Tài liệu · n** (nút Tải lên) → **Ghi chép · n** → vùng nút cố định: "Thêm ghi chép", "Xong giai đoạn".
2. **Components:** `File/Đính kèm`; thẻ ghi chép (thời gian, nội dung); `Button` Tonal, Filled; sheet `7t`: `Text field` nhiều dòng, nút Tải lên tệp (`file_picker`), Ảnh (`image_picker`: chụp hoặc thư viện), Link (`Text field` URL), danh sách tài liệu đã thêm, Filled "Lưu ghi chép".
3. **States:** Đang làm; `7s1`, `7s2` Đã xong ("Đã xong · Hoàn thành T2 5/10 · đúng ngày dự kiến", nút Xong ẩn); Empty tài liệu ("Chưa có tài liệu"); Đang tải lên (thanh tiến độ trong dòng tệp); Lỗi tải lên (dòng tệp màu `error`, "Tải lên thất bại · Thử lại").
4. **Interactions:** Tải lên → chọn tệp → dòng Đang tải lên → xong. Chạm tệp → mở bằng app mặc định; chạm link → trình duyệt. Thêm ghi chép → `7t`; Lưu → đóng sheet, ghi chép và tài liệu hiện đầu danh sách. Xong giai đoạn → tick giai đoạn, SnackBar "Đã xong Chạy thực nghiệm · Hoàn tác", về `7`.
5. **Navigation:** Từ `7`, `7c`, `13`, `13p`, `2f`, khối ở `9`. Back → màn trước (từ thông báo đẩy → `2`).
6. **Constraints:** Tệp tối đa 20 MB ("Tệp lớn hơn 20 MB."). Ghi chép 1–1000 ký tự. Tên tệp dài cắt giữa, giữ phần mở rộng.

#### `7b` · Sửa deadline (dialog Xoá)
1. **Layout:** `AppBar` "Sửa deadline" → form giống `6b2` (môn + "Đổi môn", Tên, Loại, Hạn chót, Nhắc trước) → nút Text màu `error` "Xoá deadline" → nút Filled cố định "Lưu".
2. **Components:** như `6b2`; `Button` Text (màu error); `Dialog` Destructive.
3. **States:** Lưu Disabled khi chưa đổi gì; Error theo ô; Loading.
4. **Interactions:** Kiểm tra như `6b2`. Lưu → `7` + SnackBar "Đã lưu". Xoá → dialog "Xoá Lab 2: Thiết kế UI? Xoá cả 3 giai đoạn, ghi chép và lời nhắc. Không hoàn tác được." → Xoá → `5` (trạng thái `5e`); Huỷ → đóng.
5. **Navigation:** Từ bút chì ở `7`. Back → `7` (hỏi bỏ thay đổi nếu đã sửa).
6. **Constraints:** Đổi hạn chót sớm hơn ngày cuối của giai đoạn → báo "Có giai đoạn kết thúc sau hạn mới."

#### `7o` · Quá hạn (biến thể `7o2`; dialog Bỏ)
1. **Layout:** `AppBar` → tên + "ITE302c · Quiz" → `Tag/Hạn nộp` Quá hạn "Trễ 1 ngày" + "Hạn 23:59 · T3 6/10 · Chưa nộp" → khối "Vì sao bị tính quá hạn" → giai đoạn 0/1 → "Bạn muốn xử lý thế nào?" → 3 thẻ lựa chọn.
2. **Components:** `Tag/Hạn nộp` Quá hạn; mascot Lạc; 3 `Card` lựa chọn (Đã nộp muộn, Dời hạn, Bỏ deadline); `7o2`: chọn ngày giờ hạn mới + Filled "Lưu hạn mới"; `Dialog` Destructive.
3. **States:** Default; `7o2` (thẻ Dời hạn mở rộng có ô chọn hạn mới); Loading.
4. **Interactions:** Đã nộp muộn → ghi nhận, `5` (`5o1`). Dời hạn → `7o2`: hạn mới phải sau bây giờ, giữ các giai đoạn → Lưu → `5` (`5o2`). Bỏ deadline → dialog "Bỏ Quiz ITE302c tuần 1? Deadline sẽ ẩn khỏi danh sách và không còn nhắc." → Bỏ → `5` (`5o3`); Huỷ → `7o`.
5. **Navigation:** Từ việc quá hạn ở `5`, thông báo Quá hạn. Back → màn trước.
6. **Constraints:** Nộp muộn không tính vào chuỗi đúng hạn.

### 07 · Hồ sơ, Cài đặt

#### `10` · Hồ sơ
1. **Layout:** Màn gốc tab 4. Ảnh bìa (cao 166) + avatar 80 → tên, email → cuộn (gap 12): hàng thống kê (Chuỗi, Đã nộp 3/3, Đúng hạn) → tuần này T2–CN → Bảng thành tích nhỏ ("Xem cả bảng") → nút Cài đặt. `NavigationBar` (Hồ sơ chọn), không có nút +.
2. **Components:** avatar (ảnh Google hoặc chữ cái đầu); `Card` Summary; mascot Xong; `BottomNav` Active=Hồ sơ.
3. **States:** Loading, Error, Populated.
4. **Interactions:** Thẻ thống kê → `10f`. Xem cả bảng → `2f`. Cài đặt → `10e`.
5. **Navigation:** Thanh điều hướng. Back → tab Hôm nay.
6. **Constraints:** Tên tối đa 1 dòng; email cắt giữa.

#### `10f` · Đã nộp tuần này
1. **Layout:** `AppBar` → nhóm theo môn (tên môn, "3 bài · đúng hạn") → danh sách bài đã nộp (tên · môn, thứ).
2. **Components:** `Card` Summary; `Note/Đã làm`.
3. **States:** Loading, Empty ("Tuần này chưa nộp bài nào"), Populated.
4. **Interactions:** Chạm bài → `7`.
5. **Navigation:** Từ `10`. Back → `10`.
6. **Constraints:** —

#### `10e` · Cài đặt
1. **Layout:** Ảnh bìa nhỏ + tên, email → danh sách mục (gap 8): Thông báo nhắc hạn (`Switch`), Nhắc trước hạn ("1 ngày"), Môn học của tôi ("5 môn"), Mục tiêu riêng, Xuất báo cáo tuần ("PDF"), Hướng dẫn sử dụng, Công cụ demo → nút Outlined cố định "Đăng xuất".
2. **Components:** `ListTile` + `Switch`; `ListTile` có giá trị bên phải và `Icon/Right`; `Button` Outlined; `Dialog` Confirmation (Đăng xuất).
3. **States:** Default; Loading khi xuất PDF.
4. **Interactions:** Tắt Thông báo nhắc hạn → huỷ lịch nhắc đã hẹn. Nhắc trước hạn → chọn 1 ngày, 3 giờ, 1 giờ (áp dụng cho deadline mới). Môn học của tôi → `10b`. Xuất báo cáo tuần → tạo PDF, mở bảng chia sẻ (Lab 3: tải lên kho lưu trữ). Hướng dẫn → `11`. Công cụ demo → `14`. Đăng xuất → dialog "Đăng xuất khỏi Nốt?" → `1`.
5. **Navigation:** Từ `10`. Back → `10`.
6. **Constraints:** Mỗi mục là vùng chạm ≥ 48.

#### `11` · Hướng dẫn sử dụng
1. **Layout:** `AppBar` → 4 thẻ mẹo (icon, tiêu đề, một câu) → nút Text "Xem ý nghĩa các icon" → nút Filled "Bắt đầu dùng".
2. **Components:** `Card` Summary × 4; `Button` Text, Filled.
3. **States:** Tĩnh.
4. **Interactions:** Xem ý nghĩa các icon → `12`. Bắt đầu dùng → `2`.
5. **Navigation:** Từ `10e`. Back → `10e`.
6. **Constraints:** —

#### `12` · Ý nghĩa icon
1. **Layout:** `AppBar` → 3 nhóm cuộn: Trạng thái deadline (icon + chữ), Màu ngày trong Kế hoạch (ô màu + nhãn + khoảng số), Loại việc (icon + độ nặng).
2. **Components:** `Tag/Hạn nộp`, ô màu `heat`, `TypeIcon`, `WeightDots`, mascot.
3. **States:** Tĩnh.
4. **Interactions:** Không.
5. **Navigation:** Từ `11`, "Cách tính" ở `6b2`. Back → màn trước.
6. **Constraints:** Bảng giá trị độ nặng phải lấy cùng nguồn với cách tính ở `3`.

#### `14` · Cấu hình ứng dụng (công cụ demo)
1. **Layout:** `AppBar` → câu "Mất mạng thì app dùng giá trị mặc định." → các thẻ khoá Remote Config (tên khoá, giá trị hiện tại, mô tả, "Mặc định trong app: …") → "Tải lần cuối: 14:05 hôm nay" → vùng nút: Filled "Tải lại cấu hình", Text "Kiểm tra lỗi".
2. **Components:** `Card` Summary; `Button` Filled, Text.
3. **States:** Default; Loading khi tải lại; Lỗi (SnackBar, giữ giá trị cũ).
4. **Interactions:** Tải lại → `fetchAndActivate()`, cập nhật giá trị. Kiểm tra lỗi → `15`.
5. **Navigation:** Từ `10e` (Công cụ demo). Back → `10e`.
6. **Constraints:** Khoá: `today_max_tasks` (int, mặc định 5), `show_study_tip` (bool, mặc định false), `reminder_hours_before` (int, mặc định 12).

#### `15` · Kiểm tra lỗi (dialog `15b`)
1. **Layout:** `AppBar` → thẻ "Thử báo cáo lỗi" ("App sẽ đóng, rồi gửi báo cáo khi mở lại.") → trạng thái Crashlytics ("Đang bật", lần gửi gần nhất) → Outlined "Ghi lỗi, không đóng app" → Destructive "Gây lỗi thử".
2. **Components:** `Card` Summary; `Button` Outlined, Destructive; `Dialog` Destructive.
3. **States:** Default; sau khi ghi lỗi: SnackBar "Đã ghi một lỗi".
4. **Interactions:** Ghi lỗi → `FirebaseCrashlytics.instance.recordError(...)`. Gây lỗi thử → dialog `15b` "Đóng app để thử lỗi? App đóng ngay. Mở lại để gửi báo cáo." → Đóng app → `FirebaseCrashlytics.instance.crash()`; Để sau → ở lại `15`.
5. **Navigation:** Từ `14`. Back → `14`.
6. **Constraints:** Chỉ hiện trong bản demo.

---

## 5. Màn hình rộng (từ 600 dp trở lên)

Không thiết kế riêng. Khi dựng, đổi bố cục theo chiều rộng (`LayoutBuilder` hoặc `MediaQuery.sizeOf(context).width`):

| Độ rộng | Thay đổi |
|---|---|
| < 600 dp | Như Figma: `NavigationBar` dưới, một cột |
| 600–839 dp | `NavigationRail` bên trái thay `NavigationBar`; nút + nằm trên rail. Nội dung một cột, rộng tối đa 600, căn giữa. Form (`1b`, `1c`, `6`–`6b5`, `7b`) rộng tối đa 480. Bottom sheet thành `Dialog` rộng 480 |
| ≥ 840 dp | Hai cột: `5` bên trái + `7` bên phải; `3` bên trái + `4` bên phải; `13` bên trái + màn đích bên phải. Lịch tuần `9` hiện đủ 7 cột không cần cuộn ngang |

Ô ngày ở `3` giữ 48 dp; phần dư chia đều làm khoảng cách giữa các cột.
