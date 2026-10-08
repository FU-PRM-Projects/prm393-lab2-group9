# Flutter handoff — Nốt (Study Planner)

Tài liệu cho lập trình viên dựng app bằng Flutter (Material 3) mà không cần hỏi lại người thiết kế. Chỉ mở Figma để xem giao diện; mọi giá trị lấy từ file này và `design/DESIGN.md`.

- Figma: page 03 Final UI (màn hình), page 04 Design System (token), page 05 Components.
- Mã màn hình S01–S10 và overlay D1–D4, BS1–BS2, SB theo `ux/user-flow.md`.
- Gói dự kiến: `google_fonts`, `flutter_svg`, `go_router`.

---

## 1. Bảng token sang Flutter

### 1.1 Màu

| Token | Hex | Tên trong Flutter |
|---|---|---|
| primary | #3D4FD6 | `ColorScheme.primary` |
| on-primary | #FFFFFF | `ColorScheme.onPrimary` |
| primary-container | #DDE1FF | `ColorScheme.primaryContainer` |
| on-primary-container | #2F3FB8 | `ColorScheme.onPrimaryContainer` |
| surface | #F6F7FB | `ColorScheme.surface` (nền `Scaffold`) |
| surface-card | #FFFFFF | `ColorScheme.surfaceContainerLowest` |
| surface-variant | #E7E9F3 | `ColorScheme.surfaceContainerHighest` |
| on-surface | #1B1D2A | `ColorScheme.onSurface` |
| on-surface-variant | #555B6E | `ColorScheme.onSurfaceVariant` |
| outline | #7A8094 | `ColorScheme.outline` |
| error | #B3261E | `ColorScheme.error` |
| on-error | #FFFFFF | `ColorScheme.onError` |
| error-container | #FDE1DF | `ColorScheme.errorContainer` |
| warning | #A84F00 | `AppColors.warning` (`ThemeExtension`) |
| warning-container | #FFE9D1 | `AppColors.warningContainer` |
| success | #1B6B44 | `AppColors.success` |
| success-container | #D8F3E6 | `AppColors.successContainer` |
| heat-0 … heat-5 | #E7E9F3, #A9DCF5, #7FD9B3, #FFD24A, #FF9A3D, #F0524B | `AppColors.heat` (`List<Color>`, chỉ số 0–5) |

Tạo `ColorScheme.fromSeed(seedColor: Color(0xFF3D4FD6))` rồi `copyWith(...)` đúng các giá trị trên. Không dùng màu sinh tự động cho các token đã liệt kê.

### 1.2 Typography

Font `GoogleFonts.beVietnamProTextTheme()`, sau đó ghi đè:

| Token | Cỡ / height | Weight | Tên trong Flutter |
|---|---|---|---|
| Tiêu đề màn top-level | 28 / 1.25 | w700 | `TextTheme.headlineMedium` |
| Tiêu đề App bar màn lồng, dialog | 22 / 1.25 | w700 | `TextTheme.titleLarge` |
| Tiêu đề banner, section | 18 / 1.25 | w600 | `TextTheme.titleMedium` |
| Tên việc | 16 / 1.4 | w600 | `TextTheme.titleSmall` |
| Nội dung, chữ trong ô nhập | 16 / 1.4 | w400 | `TextTheme.bodyLarge` |
| Dòng phụ, giờ | 14 / 1.4 | w400 | `TextTheme.bodyMedium` |
| Chữ nút, chip, thời hạn | 14 / 1.4 | w600 | `TextTheme.labelLarge` |
| Nhãn điều hướng, tiêu đề nhóm, số trên ô | 12 / 1.4 | w600 | `TextTheme.labelMedium` |

Giờ và ngày: thêm `fontFeatures: [FontFeature.tabularFigures()]`.

### 1.3 Khoảng cách, bo góc, elevation

| Token | Giá trị | Tên trong Flutter |
|---|---|---|
| space-1 | 4 | `AppSpacing.xs` |
| space-2 | 8 | `AppSpacing.sm` |
| space-3 | 12 | `AppSpacing.md` |
| space-4 | 16 | `AppSpacing.lg` |
| space-5 | 20 | `AppSpacing.xl` (lề ngang màn hình) |
| space-6 | 24 | `AppSpacing.xxl` |
| space-8 | 32 | `AppSpacing.xxxl` |
| radius-sm | 8 | `AppRadius.sm` |
| radius-md | 12 | `AppRadius.md` |
| radius-lg | 16 | `AppRadius.lg` |
| radius-xl | 20 | `AppRadius.xl` |
| radius-2xl | 28 | `AppRadius.xxl` |
| level-0 | 0 | `CardTheme.elevation` |
| level-2 | 3 | `FloatingActionButtonThemeData.elevation`, `NavigationBarThemeData.elevation`, `SnackBarThemeData.elevation` |
| level-3 | 6 | `DialogTheme.elevation`, `BottomSheetThemeData.elevation` |
| Chiều cao dòng việc | 60 | `AppSizes.taskRowMinHeight` |
| Padding dưới danh sách có FAB | 88 | `AppSizes.fabClearance` |

---

## 2. Bảng component sang widget

| Component (Figma page 05) | Widget | Ghi chú |
|---|---|---|
| Button / filled | `FilledButton` | Một nút filled mỗi màn |
| Button / tonal | `FilledButton.tonal` | |
| Button / text | `TextButton` | Hủy, Hoàn tác |
| Button / destructive | `FilledButton` với `backgroundColor: error` | Xóa, Đăng xuất trong dialog |
| Button / loading | `AppButton(isLoading: true)` | Thay chữ bằng `CircularProgressIndicator` 20 dp, giữ chiều rộng, `onPressed: null` |
| FAB | `FloatingActionButton` | Icon `Icons.add`, `tooltip: 'Thêm deadline'` |
| Text field | `TextFormField` + `InputDecoration(border: OutlineInputBorder())` | Nhãn đặt phía trên bằng `Text` riêng |
| Picker ngày, giờ | `showDatePicker`, `showTimePicker` | Ô chỉ đọc, chạm để mở picker |
| Chọn nhóm việc, mức quan trọng | `SegmentedButton` hoặc `ChoiceChip` | |
| Segmented control | `SegmentedButton<T>` | |
| Task row | `TaskRow` (tự viết từ `InkWell` + `Checkbox` + `Text`) | Props: `title`, `subtitle`, `dueLabel`, `dueTone`, `done`, `onTap`, `onToggle` |
| Card | `Card(elevation: 0, color: surfaceContainerLowest)` | Bo góc `AppRadius.xl` |
| Banner tóm tắt | `SummaryBanner` (tự viết, nền `primary`) | Props: `title`, `subtitle`, `mascot` |
| Ô lịch nhiệt | `HeatCell` (tự viết) trong `GridView.count(crossAxisCount: 7)` | Props: `date`, `level 0–5`, `taskCount`, `isSelected`, `isToday` |
| Khối lịch bận, khung trống | `BusyBlockTile`, `FreeSlotTile` (tự viết) | |
| Lưới giờ trong ngày | `DayTimeline` (tự viết, `Stack` trong `SingleChildScrollView`) | 1 giờ = 60 dp, từ 07:00 đến 24:00 |
| Navigation | `NavigationBar` + 4 `NavigationDestination` | `labelBehavior: alwaysShow` |
| App bar | `AppBar` | Top-level: `centerTitle: false`, không Back |
| Dialog | `AlertDialog` qua `showDialog` | |
| Bottom sheet | `showModalBottomSheet(isScrollControlled: true, useSafeArea: true)` | |
| Snackbar | `SnackBar` + `SnackBarAction(label: 'Hoàn tác')` | `duration: 5s`, `behavior: floating` |
| Loading state | `SkeletonList`, `SkeletonHeatGrid` (tự viết) | Khối màu `surfaceContainerHighest`, không cần gói ngoài |
| Empty state | `EmptyState` (tự viết) | Props: `mascotAsset`, `title`, `body`, `actionLabel`, `onAction` |
| Error state | `ErrorState` (tự viết) | Props: `title`, `cause`, `onRetry`. Mascot cố định Nốt Lạc |
| Mascot, icon nhóm việc | `SvgPicture.asset` (gói `flutter_svg`) | Luôn có `semanticsLabel` |
| Avatar | `CircleAvatar(foregroundImage: NetworkImage(photoUrl))` | Chữ cái đầu khi không có ảnh |

---

## 3. Điều hướng chung

| Route | Màn hình |
|---|---|
| `/login` | S01 Đăng nhập |
| `/today` | S02 Hôm nay |
| `/plan` | S03 Kế hoạch |
| `/deadlines` | S04 Deadline |
| `/busy` | S05 Lịch bận |
| `/deadlines/new`, `/deadlines/:id/edit` | S06 Thêm / sửa deadline |
| `/deadlines/:id` | S07 Chi tiết deadline |
| `/deadlines/:id/submitted` | S08 Đã nộp |
| `/plan/day/:date` | S09 Chi tiết ngày |
| `/profile` | S10 Hồ sơ |

- 4 tab dùng `StatefulShellRoute.indexedStack` để giữ vị trí cuộn khi đổi tab.
- Chưa đăng nhập: mọi route chuyển về `/login`.

---

## 4. Đặc tả từng màn hình

### S01 · Đăng nhập

1. **Layout:** `Scaffold` (nền surface, không App bar) → `SafeArea` → `Padding` ngang `AppSpacing.xl` → `Column` căn giữa dọc: họa tiết nền (`Positioned`, độ mờ 40%) → mascot 160 dp → `AppSpacing.xxl` → "Nốt" (headlineMedium) → `AppSpacing.sm` → câu giới thiệu "Gom deadline từ mọi nhóm chat về một chỗ" (bodyLarge, on-surface-variant) → `Spacer` → nút → `AppSpacing.xxxl`. Không cuộn.
2. **Components:** Button / filled "Đăng nhập bằng Google" (icon Google 20 dp), Button / loading, Error state (dạng dòng chữ dưới nút).
3. **States:** default; loading (nút đang tải); error (dòng chữ màu error dưới nút).
4. **User interactions:** chạm nút → mở Google Sign-In. Thành công → S02. Người dùng đóng hộp chọn tài khoản → về default, không báo lỗi. Lỗi mạng → "Chưa đăng nhập được vì mất kết nối. Thử lại sau khi có mạng."
5. **Navigation:** đến từ: mở app khi chưa đăng nhập, Đăng xuất ở S10. Thành công → `/today` và xóa S01 khỏi ngăn xếp. Back: thoát app.
6. **Important UI constraints:** nút rộng hết chiều ngang trừ lề, cao 56 dp. Chữ giới thiệu tối đa 2 dòng. Chạm nút hai lần liên tiếp chỉ mở một hộp đăng nhập.

### S02 · Hôm nay

1. **Layout:** `Scaffold` → `AppBar` (tiêu đề "Hôm nay" headlineMedium, phụ đề thứ và ngày bodyMedium; action: avatar 40 dp trong vùng chạm 48 dp) → `CustomScrollView` cuộn dọc, lề ngang `AppSpacing.xl`: Banner tóm tắt → `AppSpacing.xxl` → section "Làm tiếp" (một Card) → `AppSpacing.xxl` → section "Lịch bận hôm nay" (tối đa 3 `BusyBlockTile`) → `AppSpacing.xxl` → section "Deadline gần nhất" (tối đa 5 `TaskRow`, link "Xem tất cả") → `NavigationBar` (Hôm nay được chọn).
2. **Components:** App bar / có action, Banner tóm tắt (Nốt Tập Trung), Card / default và pressed, BusyBlockTile, Task row, Navigation / Hôm nay, Skeleton, Empty state, Error state.
3. **States:** loading (skeleton banner và 3 dòng); empty ("Hôm nay trống lịch. Tận dụng để làm sớm việc tuần này." + nút "Xem Kế hoạch"); error (mất mạng mức màn hình, nút Thử lại); populated.
4. **User interactions:** chạm thẻ "Làm tiếp" hoặc một Task row → S07. Chạm checkbox của Task row → đánh dấu xong buổi làm hôm nay, dòng mờ đi, snackbar "Đã xong 1 buổi · Hoàn tác". Chạm avatar → S10. Kéo xuống → tải lại. "Xem tất cả" → tab Deadline.
5. **Navigation:** đến từ: S01, thanh điều hướng, S06 sau khi lưu ở Flow 4. Đi tới: S07, S10, S04. Back: thoát app.
6. **Important UI constraints:** banner luôn một câu tiêu đề ("3 việc hôm nay · 1 quá hạn"), không quá 2 dòng. Tên việc tối đa 2 dòng, cắt bằng dấu ba chấm. Thẻ "Làm tiếp" chọn việc theo thứ tự: quá hạn, hạn sớm nhất, mức quan trọng cao nhất.

### S03 · Kế hoạch

1. **Layout:** `Scaffold` → `AppBar` (tiêu đề "Kế hoạch"; action: nút "Hôm nay" dạng text để về tháng hiện tại) → `CustomScrollView`: hàng chọn tháng (nút trước, "Tháng 10, 2026" titleMedium, nút sau) → hàng tên thứ (T2–CN, labelMedium) → `GridView.count(crossAxisCount: 7)` lề 12 dp, mỗi ô 48 × 48 dp → `AppSpacing.lg` → chú giải 6 mức (ô 16 dp + nhãn chữ "Trống, Nhẹ, Vừa, Khá nặng, Nặng, Quá tải") → `AppSpacing.xxl` → Card tóm tắt ngày đang chọn → `NavigationBar` (Kế hoạch được chọn).
2. **Components:** App bar / có action, HeatCell (6 mức, đang chọn, hôm nay), Card / pressed, Button / tonal "Thêm việc vào ngày này", Button / text "Xem chi tiết", Skeleton lưới, Error state.
3. **States:** loading (lưới ô xám surface-variant); error (mất mạng, Thử lại); populated. Không có empty: tháng không có việc vẫn hiện lưới heat-0.
4. **User interactions:** chạm một ô → chọn ngày đó, Card tóm tắt cập nhật ("Thứ Ba 14/10 · Quá tải · 6 việc"). Chạm ô đang chọn hoặc "Xem chi tiết" → S09. "Thêm việc vào ngày này" → S06 với ngày đã điền sẵn (Flow 4). Vuốt ngang trên lưới → đổi tháng.
5. **Navigation:** đến từ: thanh điều hướng, S05 khi hôm nay hết giờ trống (Flow 4, mở với ngày nhẹ nhất trong 7 ngày tới đã được chọn sẵn). Đi tới: S09, S06. Back: về S02.
6. **Important UI constraints:** màu ô không bao giờ là tín hiệu duy nhất: ô có số việc và khuôn mặt mascot; `Semantics(label: 'Thứ Ba 14 tháng 10, quá tải, 6 việc')`. Ngày không thuộc tháng hiện tại hiện mờ 40% và không chạm được. Số việc từ 10 trở lên hiện "9+".

### S04 · Deadline

1. **Layout:** `Scaffold` → `AppBar` (tiêu đề "Deadline"; action: icon lọc) → `CustomScrollView` lề `AppSpacing.xl`: Banner tóm tắt ("1 việc quá hạn" / "5 việc cần xong trong tuần này", Nốt Tập Trung 72 × 80 dp) → `AppSpacing.lg` → `SegmentedButton` "Theo hạn / Theo nhóm việc" → các nhóm: tiêu đề nhóm (mascot 24 dp + tên nhóm labelMedium viết hoa + số lượng bên phải) rồi các Task row → nhóm "Đã nộp" thu gọn ở cuối → padding dưới 88 dp → FAB → `NavigationBar` (Deadline được chọn).
2. **Components:** App bar / có action, Banner tóm tắt, Segmented control, Task row (default, đã xong), FAB, Snackbar / có action, Skeleton, Empty state (Nốt Ngủ), Error state.
3. **States:** loading (skeleton banner, tiêu đề nhóm và 5 dòng); empty ("Chưa có deadline nào" / "Thêm deadline đầu tiên, Nốt sẽ nhắc bạn trước hạn." / nút "Thêm deadline", không hiện FAB); error; populated.
4. **User interactions:** chạm FAB → S06 (Flow 1). Chạm Task row → S07. Chạm checkbox → mở D1 như ở S07. Đổi segmented → nhóm lại theo Môn học, Đồ án, Nghiên cứu, Khác. Chạm tiêu đề nhóm Đã nộp → mở hoặc thu gọn. "Hoàn tác" trên snackbar → việc trở lại nhóm cũ.
5. **Navigation:** đến từ: thanh điều hướng, S02, S08 ("Về Deadline", kèm snackbar "Đã nộp · Hoàn tác"), S06 sau khi lưu. Đi tới: S06, S07. Back: về S02.
6. **Important UI constraints:** nhóm rỗng thì ẩn cả tiêu đề nhóm. Thời hạn bên phải luôn là chữ ("Trễ 1 ngày" màu error, "Hôm nay 23:59" màu warning, "Còn 2 ngày" màu on-surface-variant). FAB không che dòng cuối nhờ padding 88 dp.

### S05 · Lịch bận

1. **Layout:** `Scaffold` → `AppBar` (tiêu đề "Lịch bận", phụ đề tuần hiện tại) → dải 7 ngày cố định dưới App bar (mỗi ngày là `ChoiceChip` 48 × 64 dp, có thứ và ngày, chấm màu heat của ngày đó) → `ListView` lề `AppSpacing.xl`, xếp theo giờ: `BusyBlockTile` (icon loại, tên, giờ, nền surface-variant) xen `FreeSlotTile` (viền nét đứt primary, "15:00–17:00 · Trống 2 giờ", icon +) → padding dưới 88 dp → FAB → `NavigationBar` (Lịch bận được chọn).
2. **Components:** App bar / default, ChoiceChip, BusyBlockTile, FreeSlotTile, FAB, Bottom sheet BS2, Skeleton, Empty state, Error state.
3. **States:** loading; empty ("Chưa có lịch bận cho ngày này. Cả ngày đang trống." + nút "Thêm lịch bận"); error; populated; ngày không còn khung trống (dòng chữ "Hôm nay không còn khung trống ≥ 45 phút" + nút tonal "Tìm ngày nhẹ hơn").
4. **User interactions:** chạm một ngày trên dải → đổi danh sách. Chạm `FreeSlotTile` → S06 với khung giờ đã điền sẵn (Flow 4). "Tìm ngày nhẹ hơn" → S03. Chạm FAB → BS2 Thêm lịch bận: Tên (bắt buộc, tối đa 60 ký tự), Loại (Lịch học, Họp nhóm, Freelance), Ngày, Giờ bắt đầu, Giờ kết thúc (phải sau giờ bắt đầu: "Giờ kết thúc phải sau giờ bắt đầu"). Chạm `BusyBlockTile` → BS2 ở chế độ sửa, có nút text "Xóa" (snackbar Hoàn tác).
5. **Navigation:** đến từ: thanh điều hướng. Đi tới: S06, S03, BS2. Back: đóng BS2 nếu đang mở, nếu không thì về S02.
6. **Important UI constraints:** chỉ hiện khung trống dài từ 45 phút và nằm trong 07:00–24:00. Khung trống luôn có chữ "Trống", không chỉ dùng viền màu. Dải 7 ngày không cuộn ở 360 dp (7 × 48 = 336 dp).

### S06 · Thêm / sửa deadline

1. **Layout:** `Scaffold(resizeToAvoidBottomInset: true)` → `AppBar` (Back, tiêu đề "Thêm deadline" hoặc "Sửa deadline") → `Form` → `SingleChildScrollView` lề `AppSpacing.xl`, khoảng cách giữa trường `AppSpacing.xl`: Tên → Nhóm việc → Hạn nộp → divider "Tùy chọn" → Mức quan trọng → Khung giờ làm → thanh nút cố định cuối màn (nền surface-card, elevation level-2, padding `AppSpacing.lg`).
2. **Components:** App bar / default, Text field (default, focused, filled, error, disabled), ChoiceChip, Segmented control, Button / filled và loading "Lưu deadline", Dialog D3, Error state dạng banner trên thanh nút.
3. **States:** default; lỗi nhập; đang lưu (nút loading, các trường disabled); lỗi khi lưu (banner error-container "Chưa lưu được vì mất kết nối. Nội dung bạn nhập vẫn còn." + nút "Thử lại", dữ liệu giữ nguyên); chế độ sửa (điền sẵn dữ liệu).
4. **User interactions và validation:**
   - **Tên** (bắt buộc): 1–80 ký tự sau khi bỏ khoảng trắng đầu cuối. Lỗi: "Nhập tên deadline".
   - **Nhóm việc** (bắt buộc): chip Môn học, Đồ án, Nghiên cứu, Khác. Chọn Môn học thì hiện thêm chip mã môn (MLN111, PRM393, WDP301, EXE201, ITE302c). Lỗi: "Chọn nhóm việc".
   - **Hạn nộp** (bắt buộc): chạm mở date picker rồi time picker, mặc định 23:59. Phải sau thời điểm hiện tại. Lỗi: "Chọn hạn nộp" hoặc "Hạn nộp phải sau thời điểm hiện tại".
   - **Mức quan trọng** (tùy chọn): Thấp, Vừa, Cao. Mặc định Vừa.
   - **Khung giờ làm** (tùy chọn): điền sẵn khi mở từ S05 hoặc S03. Phải trước hạn nộp. Để trống thì app tự xếp các buổi 45 phút vào khung trống trước hạn nộp.
   - Lỗi chỉ hiện sau lần bấm Lưu đầu tiên, sau đó kiểm tra lại mỗi khi trường thay đổi. Bấm Lưu khi còn lỗi → cuộn và focus vào trường lỗi đầu tiên.
   - Lưu thành công → về màn trước, snackbar "Đã lưu deadline".
5. **Navigation:** đến từ: S04 (FAB), S05 (khung trống), S03 (Thêm việc vào ngày này), S07 (Sửa). Sau khi lưu: từ S04 về S04 (Flow 1); từ S05 hoặc S03 về S02 (Flow 4); từ S07 về S07. Back: không có thay đổi thì đóng; có thay đổi thì mở D3 "Bỏ thay đổi chưa lưu?" (Tiếp tục sửa / Bỏ).
6. **Important UI constraints:** bàn phím mở thì thanh nút cố định nằm ngay trên bàn phím và ô đang nhập vẫn nhìn thấy. Ô Tên dùng `textInputAction: next`. Đếm ký tự hiện khi còn dưới 10 ký tự. Nút Lưu không bị disable khi form chưa hợp lệ; lỗi được giải thích bằng chữ.

### S07 · Chi tiết deadline

1. **Layout:** `Scaffold` → `AppBar` (Back; tiêu đề trống; action: menu ba chấm với "Sửa", "Xóa") → `SingleChildScrollView` lề `AppSpacing.xl`: tên việc (headlineMedium, tối đa 3 dòng) → hàng chip (icon nhóm việc + mã môn, mức quan trọng) → Card thông tin (Hạn nộp + nhãn trạng thái, Tiến độ "2/3 buổi" + `LinearProgressIndicator`) → `AppSpacing.xxl` → section "Buổi làm" (danh sách Task row, mỗi dòng là một buổi: ngày, giờ, checkbox) → thanh nút cố định cuối màn: "Đánh dấu đã nộp".
2. **Components:** App bar / có action, Card / default, Task row (default, đã xong), Button / filled và loading, Dialog D1 (xác nhận), Dialog D2 (destructive), Skeleton, Error state.
3. **States:** loading; error; populated; đã nộp (nút đổi thành tonal "Đánh dấu chưa nộp", nhãn "Đã nộp" màu success).
4. **User interactions:** chạm "Đánh dấu đã nộp" → D1 "Đánh dấu đã nộp Lab 2: Thiết kế UI?" (Hủy / Đã nộp). Đã nộp → nút loading → S08. Hủy → đóng dialog, giữ nguyên. Chạm checkbox buổi làm → cập nhật tiến độ ngay. Menu "Sửa" → S06 chế độ sửa. Menu "Xóa" → D2 "Xóa deadline này và 3 buổi làm của nó?" (Hủy / Xóa) → về màn trước, snackbar "Đã xóa · Hoàn tác".
5. **Navigation:** đến từ: S02, S04, S09. Đi tới: S08, S06. Back: về màn trước.
6. **Important UI constraints:** chỉ có một nút filled. Thanh tiến độ luôn đi kèm chữ "2/3 buổi". Buổi làm đã qua mà chưa xong hiện chữ "Đã qua" màu error.

### S08 · Đã nộp

1. **Layout:** `Scaffold` (không App bar) → `SafeArea` → `Column` căn giữa, lề `AppSpacing.xl`: họa tiết sao và tick (nền, mờ 40%) → Nốt Xong 160 dp → `AppSpacing.xxl` → "Đã nộp" (headlineMedium) → tên việc (titleMedium) → thời điểm nộp so với hạn ("Sớm 6 giờ so với hạn", bodyLarge, success) → `AppSpacing.xxl` → Card "Tuần này đã nộp 3/7 việc" + thanh tiến độ → `Spacer` → nút filled "Về Deadline".
2. **Components:** Card / default, Button / filled, Mascot.
3. **States:** populated. Nộp trễ: dòng thời điểm đổi thành "Trễ 2 giờ so với hạn" màu on-surface-variant, không dùng màu error, không trách.
4. **User interactions:** chạm "Về Deadline" → S04 và hiện snackbar "Đã nộp · Hoàn tác" (Flow 2). Mascot có hiệu ứng vào 300 ms, không lặp.
5. **Navigation:** đến từ: S07 sau khi xác nhận D1. Đi tới: S04. Back hệ thống: giống "Về Deadline" (không quay lại S07).
6. **Important UI constraints:** tên việc tối đa 2 dòng. Hiệu ứng tắt khi hệ thống bật giảm chuyển động (`MediaQuery.disableAnimations`).

### S09 · Chi tiết ngày

1. **Layout:** `Scaffold` → `AppBar` (Back, tiêu đề "Thứ Ba 14/10", phụ đề nhãn mức "Quá tải · 6 việc" kèm ô màu 12 dp) → `SegmentedButton` "Danh sách / Theo giờ" lề `AppSpacing.xl` → nội dung:
   - **Danh sách:** `ListView`: lịch bận (BusyBlockTile) rồi buổi làm (Task row có nút text "Dời" bên phải).
   - **Theo giờ:** `DayTimeline` cuộn dọc, cột giờ 48 dp bên trái, khối lịch bận nền surface-variant, khối buổi làm nền primary-container; tự cuộn tới giờ hiện tại.
2. **Components:** App bar / default, Segmented control, BusyBlockTile, Task row, DayTimeline, Bottom sheet BS1, Snackbar / có action, Empty state, Skeleton.
3. **States:** loading; empty ("Ngày này trống. Bạn có thể dời việc từ ngày nặng sang đây."); populated; BS1 có lỗi.
4. **User interactions:** chạm "Dời" (hoặc nhấn giữ khối buổi làm ở chế độ Theo giờ) → BS1: tên việc, hạn nộp, dải 7 ngày kế tiếp có màu heat kèm nhãn chữ, nút "Dời sang thứ Năm". Chọn ngày sau hạn nộp → ô ngày bị gạch, cảnh báo warning-container "Ngày này sau hạn nộp (thứ Sáu 23:59). Chọn ngày sớm hơn.", nút Dời bị khóa. Dời thành công → đóng BS1, việc biến mất khỏi ngày, nhãn mức cập nhật, snackbar "Đã dời sang thứ Năm · Hoàn tác". Chạm tên việc → S07.
5. **Navigation:** đến từ: S03. Đi tới: S07, BS1. Back: đóng BS1 nếu đang mở; nếu không thì về S03, lịch nhiệt đã cập nhật màu (Flow 3).
6. **Important UI constraints:** lựa chọn segmented được nhớ trong phiên. Khối trong lưới giờ ngắn hơn 30 phút vẫn cao tối thiểu 48 dp để chạm được. Ngày đã qua không cho dời việc vào.

### S10 · Hồ sơ

1. **Layout:** `Scaffold` → `AppBar` (Back, tiêu đề "Hồ sơ") → `ListView` lề `AppSpacing.xl`: Card tài khoản (avatar 64 dp, tên titleMedium, email bodyMedium) → `AppSpacing.xxl` → section "Nhắc hạn": `SwitchListTile` "Nhắc trước hạn" → `SegmentedButton` "1 giờ / 1 ngày / 2 ngày" (disabled khi tắt công tắc) → `AppSpacing.xxxl` → nút text màu error "Đăng xuất".
2. **Components:** App bar / default, Card / default, Switch, Segmented control (default, disabled), Button / text destructive, Dialog D4.
3. **States:** populated; đang lưu cài đặt (công tắc disabled tạm thời); lỗi lưu (snackbar "Chưa lưu được cài đặt. Thử lại" + action "Thử lại", công tắc trở về giá trị cũ).
4. **User interactions:** bật công tắc → mặc định chọn "1 ngày", lưu ngay, snackbar "Đã bật nhắc trước 1 ngày". Đổi lựa chọn → lưu ngay. Chạm "Đăng xuất" → D4 "Đăng xuất khỏi Nốt?" (Hủy / Đăng xuất) → S01.
5. **Navigation:** đến từ: avatar ở S02. Đi tới: S01 sau khi đăng xuất (xóa toàn bộ ngăn xếp). Back: về S02.
6. **Important UI constraints:** không có nút Lưu riêng; mọi thay đổi lưu ngay và có phản hồi. Email dài cắt giữa bằng dấu ba chấm. Lab 3 thêm vào màn này: danh sách thông báo (FCM) và giá trị Remote Config.

---

## 5. Màn hình rộng (từ 600 dp trở lên)

Không thiết kế riêng trong Lab 2. Khi chiều rộng từ 600 dp:

| Thay đổi | Chi tiết |
|---|---|
| Điều hướng | `NavigationBar` đổi thành `NavigationRail` bên trái, giữ 4 điểm đến và nhãn chữ |
| Bố cục danh sách – chi tiết | S04 Deadline: danh sách bên trái (rộng 360 dp), S07 hiện bên phải thay vì mở màn mới. S03 Kế hoạch: lịch nhiệt bên trái, S09 bên phải |
| S05 Lịch bận | Thay dải 7 ngày bằng 7 cột giờ của cả tuần |
| Form và dialog | S06 mở dạng dialog, rộng tối đa 560 dp. Bottom sheet BS1, BS2 mở dạng dialog |
| Màn một cột | S01, S02, S08, S10: nội dung rộng tối đa 600 dp, căn giữa |
| Ô lịch nhiệt | Ô lớn tối đa 72 dp; dư chỗ thì hiện thêm tên việc đầu tiên trong ô |
