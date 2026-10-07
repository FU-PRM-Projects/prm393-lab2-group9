# Flutter handoff

> Đề có template ở Phụ lục B, nhưng phụ lục không có trong file đề mình nhận được. Hãy đối chiếu với template của giảng viên.

## Bảng token sang Flutter
| Token | Giá trị | Tên trong Flutter |
|---|---|---|
| primary | #3D4FD6 | `ColorScheme.primary` |
| on-primary | #FFFFFF | `ColorScheme.onPrimary` |
| surface | #F6F7FB | `ColorScheme.surface` |
| on-surface | #1B1D2A | `ColorScheme.onSurface` |
| error | #B3261E | `ColorScheme.error` |
| Tiêu đề màn hình 28 sp | TODO | `TextTheme.headlineMedium` |
| Tiêu đề dòng 16 sp | TODO | `TextTheme.titleMedium` |
| Chữ phụ 14 sp | TODO | `TextTheme.bodyMedium` |
| Khoảng cách 4–24 dp | TODO | hằng số, ví dụ `AppSpacing.md` |

## Bảng component sang widget
| Component | Widget |
|---|---|
| Button | `FilledButton` |
| Text field | `TextFormField` |
| Card | `Card` |
| Navigation | `NavigationBar` |
| App bar | `AppBar` |
| Dialog | `AlertDialog` |
| Loading state | TODO |
| Empty state | TODO |
| Error state | TODO |
| Mascot | `SvgPicture.asset` (gói `flutter_svg`) |

## Đặc tả từng màn hình
Lặp lại khối dưới đây cho từng màn trong 8 màn.

### Màn: TODO
1. **Layout:** TODO (ví dụ `Scaffold` → `AppBar` → `Column` cuộn được; khoảng cách lấy từ token; phần nào cuộn)
2. **Components:** TODO (tên component và variant)
3. **States:** TODO (default, loading, empty, error, populated)
4. **User interactions:** TODO (chạm, vuốt, nhập liệu, quy tắc validation, kết quả)
5. **Navigation:** TODO (đến từ đâu, mỗi hành động dẫn tới đâu, nút Back làm gì)
6. **Important UI constraints:** TODO (vùng chạm tối thiểu, bàn phím, chữ tràn, độ dài tối đa, màn hình rộng)

## Màn hình rộng (từ 600 dp trở lên)
TODO: mô tả điều gì thay đổi. Không cần thiết kế.
