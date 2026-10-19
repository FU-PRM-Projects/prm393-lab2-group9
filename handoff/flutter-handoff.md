# Flutter Handoff — Nốt (Study Planner)

Tài liệu bàn giao kỹ thuật dành riêng cho lập trình viên xây dựng ứng dụng Nốt bằng **Flutter (Material 3)**. Tài liệu phản ánh 100% hệ thống thiết kế trên Figma (`PRM393-LAB2-Study-Planner`), bao gồm **7 phân hệ giao diện**, hơn 25 khung thiết bị, hỗ trợ đầy đủ 4 persona (Minh, Đăng Khoa, Bảo Ngọc, Quốc Huy) và tuân thủ các quy chuẩn trong [`design/DESIGN.md`](file:///e:/prm393-lab2-group9/design/DESIGN.md).

- **Gói thư viện khuyến nghị:** `go_router`, `flutter_svg`, `google_fonts`, `provider` hoặc `flutter_bloc`.
- **Target SDK:** Flutter 3.22+ (hỗ trợ `TextScaler` mới).

---

## 1. Bản đồ Tokens sang Flutter Code

### 1.1 Màu sắc (`ColorScheme` & `ThemeExtension`)

```dart
// app_theme.dart
final ColorScheme appColorScheme = ColorScheme(
  brightness: Brightness.light,
  primary: Color(0xFF3D4FD6),
  onPrimary: Color(0xFFFFFFFF),
  primaryContainer: Color(0xFFDDE1FF),
  onPrimaryContainer: Color(0xFF2F3FB8),
  surface: Color(0xFFF6F7FB),
  surfaceContainerLowest: Color(0xFFFFFFFF), // surface-card
  surfaceContainerHighest: Color(0xFFE7E9F3), // surface-variant
  onSurface: Color(0xFF1B1D2A),
  onSurfaceVariant: Color(0xFF555B6E),
  outline: Color(0xFF7A8094),
  error: Color(0xFFB3261E),
  onError: Color(0xFFFFFFFF),
  errorContainer: Color(0xFFFDE1DF),
);

// Mở rộng màu đặc thù
@immutable
class AppColorsExtension extends ThemeExtension<AppColorsExtension> {
  final Color warning;
  final Color warningContainer;
  final Color success;
  final Color successContainer;
  final List<Color> heat;

  const AppColorsExtension({
    this.warning = const Color(0xFFA84F00),
    this.warningContainer = const Color(0xFFFFE9D1),
    this.success = const Color(0xFF1B6B44),
    this.successContainer = const Color(0xFFD8F3E6),
    this.heat = const [
      Color(0xFFE7E9F3), // heat-0: Trống
      Color(0xFFA9DCF5), // heat-1: Nhẹ
      Color(0xFF7FD9B3), // heat-2: Vừa
      Color(0xFFFFD24A), // heat-3: Khá nặng
      Color(0xFFFF9A3D), // heat-4: Nặng
      Color(0xFFF0524B), // heat-5: Quá tải
    ],
  });

  @override
  AppColorsExtension copyWith({/* ... */}) => AppColorsExtension();
  @override
  AppColorsExtension lerp(ThemeExtension<AppColorsExtension>? other, double t) => this;
}
```

### 1.2 Kiểu chữ (`TextTheme` & Hỗ trợ Text Scaling)

```dart
// app_typography.dart
TextTheme appTextTheme = GoogleFonts.beVietnamProTextTheme().copyWith(
  headlineMedium: TextStyle(fontSize: 28, height: 1.25, fontWeight: FontWeight.w700),
  titleLarge: TextStyle(fontSize: 22, height: 1.25, fontWeight: FontWeight.w700),
  titleMedium: TextStyle(fontSize: 18, height: 1.25, fontWeight: FontWeight.w600),
  titleSmall: TextStyle(fontSize: 16, height: 1.40, fontWeight: FontWeight.w600),
  bodyLarge: TextStyle(fontSize: 16, height: 1.40, fontWeight: FontWeight.w400),
  bodyMedium: TextStyle(fontSize: 14, height: 1.40, fontWeight: FontWeight.w400),
  labelLarge: TextStyle(fontSize: 14, height: 1.40, fontWeight: FontWeight.w600),
  labelMedium: TextStyle(fontSize: 12, height: 1.40, fontWeight: FontWeight.w600),
);
```

*Lưu ý trợ năng:* Mọi component phải bọc bằng `FittedBox(fit: BoxFit.scaleDown)` hoặc sử dụng `SingleChildScrollView` / `Column` linh hoạt (không set cứng `height` cho `TaskRow` hoặc `Card`) để đảm bảo không bị lỗi RenderFlex Overflow khi người dùng kích hoạt `MediaQuery.of(context).textScaler = TextScaler.linear(1.3)`.

---

## 2. Bảng ánh xạ Component sang Flutter Widget

| Component (Figma Page 05) | Widget tương ứng trong Flutter | Thuộc tính & Ghi chú kỹ thuật |
|---|---|---|
| **Phase Stepper** | `PhaseStepperWidget` (Tự dựng) | Hiển thị 4 giai đoạn, hỗ trợ trạng thái completed, in-progress, pending, overdue. |
| **Attachment Chip** | `AttachmentChip(fileName, fileType, sizeBytes)` | Hỗ trợ 4 định dạng DOCX, PDF, XLSX, ZIP. Chạm mở trình xem tệp. |
| **Ô lịch nhiệt (HeatCell)** | `HeatCellWidget(date, heatLevel, taskCount, mascot)` | Hiển thị kích thước hiển thị $42 \times 42$, vùng chạm $48 \times 48$. |
| **Dòng công việc (TaskRow)** | `TaskRow(title, course, deadline, isCompleted, onToggle)` | Min-height $60\text{ dp}$, tự co giãn khi text scale $1.3\times$. |
| **Thanh điều hướng** | `NavigationBar` (4 Destinations) | Hôm nay (`Icons.today`), Kế hoạch (`Icons.calendar_month`), Deadline (`Icons.assignment_late`), Ca bận (`Icons.event_busy`). |
| **FAB Thêm việc** | `FloatingActionButton.extended` hoặc regular | Nền `primary`, icon `Icons.add`. |
| **Notification Tile** | `NotificationListTile(title, subtitle, timestamp, isRead)` | Nền đổi màu nhẹ khi chưa đọc, hỗ trợ vuốt để xóa. |
| **Lock Screen Card** | `LockScreenNotificationCard` | Preview trong màn hình giả lập notification push. |
| **Streak Badge** | `WeeklyStreakBadge(completedDays, totalDays)` | Hiển thị chuỗi hoàn thành công việc kèm mascot Nốt Xong. |
| **Text Scale Tester** | `TextScaleSimulator(scaleFactor: 1.3)` | Dùng trong màn kiểm thử Device 7.4. |

---

## 3. Hệ thống Định tuyến (Routing Architecture với `go_router`)

Cấu trúc route phân cấp đầy đủ phục vụ 7 phân hệ:

```dart
final GoRouter appRouter = GoRouter(
  initialLocation: '/today',
  routes: [
    // 01 · Xác thực
    GoRoute(
      path: '/auth/login',
      builder: (context, state) => const LoginScreen(), // Device 1
      routes: [
        GoRoute(
          path: 'register',
          builder: (context, state) => const RegisterScreen(), // Device 1b
        ),
        GoRoute(
          path: 'forgot-password',
          builder: (context, state) => const ForgotPasswordScreen(), // Device 1e, 1f, 1g, 1h
        ),
      ],
    ),

    // 02 · Làm quen (Onboarding)
    GoRoute(
      path: '/onboarding',
      builder: (context, state) => const OnboardingIntroScreen(), // Device 2a
      routes: [
        GoRoute(
          path: 'quiz',
          builder: (context, state) => const OnboardingQuizScreen(), // Device 2b (3 câu hỏi)
        ),
        GoRoute(
          path: 'finish',
          builder: (context, state) => const OnboardingFinishScreen(), // Device 2c
        ),
      ],
    ),

    // ShellRoute cho 4 Tab chính (StatefulShellRoute giữ vị trí cuộn)
    StatefulShellRoute.indexedStack(
      builder: (context, state, navigationShell) => ScaffoldWithNavBar(navigationShell: navigationShell),
      branches: [
        // Tab 1: 03 · Hôm nay
        StatefulShellBranch(
          routes: [
            GoRoute(
              path: '/today',
              builder: (context, state) => const TodayScreen(), // Device 3
              routes: [
                GoRoute(
                  path: 'chunk-slots',
                  builder: (context, state) => const ChunkSlotsScreen(), // Device 2c0, 2c3
                ),
                GoRoute(
                  path: 'achievements',
                  builder: (context, state) => const WeeklyAchievementsScreen(), // Device 3b
                ),
              ],
            ),
          ],
        ),

        // Tab 2: 04 · Kế hoạch
        StatefulShellBranch(
          routes: [
            GoRoute(
              path: '/plan',
              builder: (context, state) => const PlanHeatmapScreen(), // Device 4
              routes: [
                GoRoute(
                  path: 'day/:date',
                  builder: (context, state) => DayDetailScreen(date: state.pathParameters['date']!), // Device 4a, 4b
                ),
                GoRoute(
                  path: 'weekly-shifts',
                  builder: (context, state) => const WeeklyShiftsScreen(), // Device 4.2
                ),
              ],
            ),
          ],
        ),

        // Tab 3: 06 · Deadline
        StatefulShellBranch(
          routes: [
            GoRoute(
              path: '/deadlines',
              builder: (context, state) => const DeadlineListScreen(), // Device 6.1
              routes: [
                GoRoute(
                  path: 'by-course',
                  builder: (context, state) => const DeadlinesByCourseScreen(), // Device 6.2
                ),
                GoRoute(
                  path: 'new',
                  builder: (context, state) => const AddDeadlineAIScreen(), // Device 6.3
                ),
                GoRoute(
                  path: ':id/phases',
                  builder: (context, state) => DeadlinePhaseDetailScreen(id: state.pathParameters['id']!), // Device 7d, 7s
                ),
                GoRoute(
                  path: ':id/notes-attachments',
                  builder: (context, state) => NotesAndAttachmentsScreen(id: state.pathParameters['id']!), // Device 7t
                ),
                GoRoute(
                  path: ':id/overdue-resolution',
                  builder: (context, state) => OverdueResolutionScreen(id: state.pathParameters['id']!), // Device 5o1, 7o2
                ),
              ],
            ),
          ],
        ),

        // Tab 4: 07 · Hồ sơ & Cài đặt
        StatefulShellBranch(
          routes: [
            GoRoute(
              path: '/profile',
              builder: (context, state) => const ProfileScreen(), // Device 7.1
              routes: [
                GoRoute(
                  path: 'dnd-settings',
                  builder: (context, state) => const DndSettingsScreen(), // Device 7.2 (Giờ họp)
                ),
                GoRoute(
                  path: 'help-guide',
                  builder: (context, state) => const HelpGuideScreen(), // Device 7.3
                ),
                GoRoute(
                  path: 'dev-text-scaler',
                  builder: (context, state) => const TextScaleTesterScreen(), // Device 7.4
                ),
              ],
            ),
          ],
        ),
      ],
    ),

    // 05 · Thông báo
    GoRoute(
      path: '/notifications',
      builder: (context, state) => const NotificationCenterScreen(), // Device 13A, 13B
      routes: [
        GoRoute(
          path: 'lockscreen-preview',
          builder: (context, state) => const LockscreenPreviewScreen(), // Device 13c
        ),
      ],
    ),
  ],
);
```

---

## 4. Đặc tả kỹ thuật cho từng Phân hệ Màn hình

### Phân hệ 01 · Xác thực (Authentication)
- **Màn hình:** Device 1 (Đăng nhập), Device 1b (Đăng ký), Device 1e–1h (Quên mật khẩu & OTP).
- **Thành phần chính:** Mascot Nốt chào mừng ($160\text{ dp}$), form nhập liệu gồm Email / Password với validator trực tiếp, nút Google Sign-In, ô nhập mã OTP 6 chữ số tự động nhảy tiêu điểm (`FocusScope`).
- **Trạng thái:** Default, Loading (nút chuyển sang xoay vòng tròn giữ nguyên bề rộng), Error (banner màu `errorContainer` phía dưới tiêu đề).
- **Offline / Lỗi mạng:** Nếu không có mạng, hiển thị thông báo "Chưa kết nối được với máy chủ. Vui lòng kiểm tra lại 4G/Wi-Fi."

### Phân hệ 02 · Làm quen (Onboarding 3 câu hỏi)
- **Màn hình:** Device 2a, 2b, 2c.
- **Thành phần chính:** Bộ 3 câu hỏi trắc nghiệm (Chọn năm học/chuyên ngành, chọn khung giờ học chính, thói quen chia nhỏ bài tập), tiến trình chỉ số trang (Dots indicator 3 bước), nút "Tiếp tục" / "Bắt đầu ngay".
- **Hành vi:** Lưu cấu hình vào `SharedPreferences` để thiết lập khung giờ sinh hoạt mặc định cho persona Bảo Ngọc hoặc Đăng Khoa.

### Phân hệ 03 · Hôm nay & Chia nhỏ việc
- **Màn hình:** Device 3 (Hôm nay), Device 2c0/2c3 (Chia nhỏ việc 45p), Device 3b (Bảng thành tích tuần).
- **Thành phần chính:**
  - Banner tóm tắt công việc tích hợp mascot Nốt Tập Trung.
  - Thẻ "Làm tiếp" việc ưu tiên cao nhất có thanh tiến độ rõ ràng.
  - Card đề xuất chia nhỏ deadline thành các block 45 phút kèm nút "Kéo vào lịch hôm nay".
  - Bảng thành tích tuần hiển thị số lượng bài đã nộp, chuỗi ngày hoàn thành (streak) và mascot Nốt Xong.

### Phân hệ 04 · Kế hoạch, Lịch nhiệt & Giờ bận
- **Màn hình:** Device 4 (Lịch nhiệt), Device 4a/4b (Chi tiết ngày), Device 4.2 (Tuần & Giờ bận).
- **Thành phần chính:**
  - Lưới `GridView` 7 cột đại diện cho 7 ngày trong tuần, ô hiển thị theo thang `heat-0` đến `heat-5`, có nhãn chữ và số đếm việc.
  - Chạm ô ngày mở Bottom Sheet dời việc. Bottom sheet kiểm tra logic nghiêm ngặt: nếu người dùng chọn ngày sau `deadline.dueDate`, nút Lưu bị vô hiệu hóa (`onPressed: null`) và hiển thị thẻ cảnh báo màu `warningContainer`.
  - Màn hình Device 4.2 cho phép thêm nhanh ca làm việc (như ca quán cà phê 18:00–22:00 của Đăng Khoa) trong $\le 3$ chạm, tự động kích hoạt tính năng đề xuất dời các việc trùng lặp.

### Phân hệ 05 · Trung tâm Thông báo & Màn khóa
- **Màn hình:** Device 13A (Nền nhạt), 13B (Hộp thư), Device 13c (Màn khóa).
- **Thành phần chính:**
  - Danh sách thông báo phân nhóm: Nhắc nhở hạn nộp, Cập nhật lịch làm, Khen ngợi thành tích.
  - Mô phỏng thẻ thông báo đẩy ngoài màn hình khóa (Lock screen notification) với 2 nút hành động nhanh (Action Buttons).

### Phân hệ 06 · Quản lý Deadline, Giai đoạn (Phases) & Tệp đính kèm
- **Màn hình:** Device 6.1 (Danh sách), 6.2 (Lọc theo môn/dự án), 6.3 (Thêm nhanh AI), Device 7d, 7s, 7s1, 7s2 (Chi tiết phase), Device 7t (Ghi chép & tệp), Device 5o1, 7o2, 5o2, 5o3 (Xử lý quá hạn).
- **Thành phần chính:**
  - `PhaseStepperWidget`: Trực quan hóa 4 giai đoạn của đồ án NCKH (Đề cương 25/10, Số liệu 02/11, Bản thảo 10/11, Hoàn thiện 15/11).
  - Khối tệp đính kèm (`AttachmentChip`): Hỗ trợ tệp DOCX, PDF, XLSX, ZIP kèm dung lượng và thao tác mở tệp.
  - Quy trình nộp bài: Nút "Đánh dấu đã nộp" hiển thị hộp thoại xác nhận D1, sau khi nộp chuyển sang màn hình chúc mừng S08 / Device 7s2 và hiển thị `SnackBar` hoàn tác 5 giây.
  - Tam giác xử lý quá hạn: Cho phép chọn Nộp muộn (ghi chú trễ), Dời hạn mới, hoặc Bỏ việc (xóa với dialog xác nhận D2).

### Phân hệ 07 · Hồ sơ cá nhân, Giờ họp (DND) & Kiểm thử Trợ năng
- **Màn hình:** Device 7.1 (Hồ sơ), Device 7.2 (Cài đặt & DND), Device 7.3 (Hướng dẫn), Device 7.4 (Demo kiểm tra lỗi & Text scale 130%).
- **Thành phần chính:**
  - Cấu hình khung giờ họp im lặng (Không làm phiền - DND) từ 14:00 đến 15:30 dành cho Quốc Huy.
  - Màn hình kiểm thử công cụ Device 7.4: Cho phép toggle công tắc giả lập Text Scale $1.3\times$ và giả lập chế độ Offline để kiểm chứng giao diện co giãn không bị lỗi render.

---

## 5. Danh mục Mascot & Asset SVGs

Tất cả các tệp vector được lưu trữ trong thư mục `assets/mascot/` và nhúng vào Flutter bằng `SvgPicture.asset`:

| Asset File | Tên Mascot | Kích thước hiển thị chuẩn | Ngữ cảnh sử dụng |
|---|---|---|---|
| `mascot-tap-trung.svg` | Nốt Tập Trung | $72 \times 80\text{ dp}$ | Banner Hôm nay & Deadline |
| `mascot-chay.svg` | Nốt Cháy | $48 \times 48\text{ dp}$ / $16 \times 16\text{ dp}$ | Nhóm Quá hạn, ô lịch mức 5 |
| `mascot-voi.svg` | Nốt Vội | $48 \times 48\text{ dp}$ / $16 \times 16\text{ dp}$ | Nhóm Đến hạn hôm nay, ô mức 4 |
| `mascot-doi.svg` | Nốt Đợi | $48 \times 48\text{ dp}$ / $16 \times 16\text{ dp}$ | Nhóm Tuần này, ô mức 3 |
| `mascot-thong-tha.svg`| Nốt Thong Thả| $48 \times 48\text{ dp}$ / $16 \times 16\text{ dp}$ | Nhóm Sau đó, ô mức 1 & 2 |
| `mascot-xong.svg` | Nốt Xong | $120 \times 120\text{ dp}$ | Màn Đã nộp, Bảng thành tích tuần |
| `mascot-ngu.svg` | Nốt Ngủ | $100 \times 100\text{ dp}$ | Trạng thái rỗng không có việc |
| `mascot-lac.svg` | Nốt Lạc | $100 \times 100\text{ dp}$ | Trạng thái mất mạng / Ngoại tuyến |
